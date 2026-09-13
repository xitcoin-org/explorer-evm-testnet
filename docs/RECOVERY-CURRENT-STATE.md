# Recovery from the current explorer state

This procedure supplements the public deployment documentation and PR #5.
The accepted backend 11.2.8 activation remains acquired. The historical
upgrade orchestrator must never be rerun. This document authorizes no public
switch, service stop, migration or rollback.

## Observed data boundary — 13 September 2026, 16:01 UTC

The active project is `xitcoin-upgrade-20260913t114659z`. Its backend database
service is `db`, database `xitcoin_blockscout`, volume ending `_backend_db`;
Stats uses `stats-db`, database `stats`, volume ending `_stats_db`;
Redis uses `redis`, volume ending `_redis_data`. All belong to this project.
Do not select the still-running former canonical DB/Redis by image or age alone.

Both databases report PostgreSQL 17.11, `wal_level=replica` and
`archive_mode=off`. Observed sizes were 194,598,579 and 8,033,971 bytes.
A WAL position from one database cluster is not comparable with the other.
An old dump plus unarchived WAL is not a demonstrated point-in-time recovery.

Redis reports AOF enabled, no keys at this observation, no pending rewrite,
AOF size zero, `maxmemory=268435456`, and `noeviction`.
An empty observation is not evidence that Redis will remain empty.
Do not delete its volume or replace future state with this observation.

## Private exercise completed

New logical dumps of the two active databases were restored on 13 September
in a new PostgreSQL container using the installed image identity, no network,
no published ports, one CPU, 768 MiB memory and a 512 MiB temporary data mount.
No backend, indexer, Stats worker or public route ran in the exercise.
The temporary container was removed after validation; dumps were retained in
the private operator recovery inventory, outside the distributable handoff.

Backend restore: 72 application tables, 360 schema migrations, 279,669 block
rows, maximum block number 235306. Capture plus restore and queries took 27.17 s.
Stats restore: three application tables, seven charts, ten chart-data rows,
four migrations; 1.68 s. These are private measurements, not a public RTO.
`pg_restore --exit-on-error` completed for each database. Row observations
characterize the restored copies; they are not a source-versus-copy checksum
comparison within an exported snapshot.

Redis was not copied or restored. The two dumps have independent consistent
PostgreSQL snapshots, not one atomic snapshot across all three stores. The
running public stores retained subsequent writes. No public zero-loss recovery
or replacement of public data was performed.

## Capture and restore procedure

1. Reidentify the active containers by Compose project and service labels;
   match their image IDs, mounts and start times against the current operator
   inventory. Record UTC, database version, size, WAL position, migrations,
   indexed height and Redis persistence/keyspace metadata. Read metadata only;
   do not export account data, credentials, environment blocks or Redis values
   into reports. Stop the exercise if identities differ unexpectedly.
2. Require at least 5 GiB free **after** the estimated backup allocation, plus
   memory for the bounded copy. At the measured sizes, reserve 1 GiB above the
   disk floor and run one private PostgreSQL instance, one database at a time.
   Use a new uniquely named recovery directory; refuse to overwrite an old one.
3. For each active DB use its installed PostgreSQL client with
   `pg_dump --format=custom --no-owner --no-acl --lock-wait-timeout=5s` and a
   90-second outer timeout. Resolve credentials inside the existing authorized
   container; never place them in a command transcript. Preserve failed partial
   artifacts with a failure label; never promote them as valid dumps.
4. Compute SHA256, byte size, source identity, start/end UTC and exit status for
   each successful dump. For a stronger data oracle, maintain a read-only
   repeatable-read transaction, export its snapshot, pass that snapshot to
   pg_dump, and calculate table counts/checksums within that same transaction.
   Bound the snapshot duration to avoid retaining old row versions indefinitely.
5. Restore only into a newly created database in a new container with
   `--network none`, no host/public volumes, no published ports, bounded CPU,
   memory, PIDs and temporary storage. Use the exact installed PostgreSQL image;
   `pg_restore --no-owner --no-acl --exit-on-error` must succeed within 100 s.
   Check migrations, schemas, application tables, latest block and Stats data.
   Keep indexers and background jobs disabled by not starting application images.
6. Redis requires a separately consistent capture if it has state. Inventory
   DB numbers, types, TTLs and persistence settings without publishing keys or
   values. Do not copy an actively changing AOF directory and call it atomic.
   An existing coherent storage snapshot may be used only where already
   authorized and demonstrated. Otherwise a Redis snapshot/replication capture
   needs separate assessment of its server-side impact; it was not run here.
   Record this component as missing until its restore and TTL oracle pass.
7. Remove only the temporary container created by the exercise, including its
   temporary data mount, using a finally/exit handler. Preserve new dumps,
   manifests and existing recovery volumes, images, archives and caches.
   Recheck public container IDs/start times and the 5 GiB disk floor afterward.

## Preserving writes for a future public recovery

Keep the current public DBs and Redis authoritative while preparing copies.
Classify data before choosing a recovery point: chain-indexed rows can be
replayed, but account identities, API plans/keys, tags, watchlists, contact
records, verification sources, background jobs and compensation records may
not be reconstructible from chain history. Zero estimated rows in a table
is not permission to omit it. Capture every schema, including
`xitcoin_compensation`, together with sequences and migration metadata.

Stats data and progress must be matched to the recovered backend height; decide
explicitly which derived series can be regenerated. Redis jobs, locks and TTLs
must not be blindly replayed in a way that repeats external effects.

For any actual replacement, first establish a validated mechanism covering
inserts, updates, deletes and sequences after the snapshots across all stores,
or obtain a separately authorized coordinated write fence and final capture.
Neither mechanism exists in this exercise. Current `archive_mode=off` and the
absence of a demonstrated cross-store change capture leave RPO unestablished.
Do not enable replication slots, alter persistence, fence public writers or
switch Nginx under this procedure. A later explicitly authorized maintenance
must reconcile the final delta and independent acceptance before a switch.

The original public stores, later writes and all historical dumps remain
preserved. Successful private restoration is one recovery component, not
global testnet acceptance or authorization to restore onto production.
