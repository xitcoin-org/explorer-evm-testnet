# Public deployment and recovery

Observed on 13 September 2026: backend **11.2.8**, corrected frontend and Stats
serve the public EVM explorer. The accepted Compose project is
`xitcoin-upgrade-20260913t114659z`. Its six services are backend, frontend,
Stats, backend PostgreSQL, Stats PostgreSQL and Redis. Exact image identities
are in [the inventory](PUBLIC_DEPLOYMENT.json).

Backend, frontend and Stats bind only to loopback ports 15100, 15101 and 15002.
The existing Nginx HTTPS origin routes `/api/` and `/socket` to the backend,
`/stats-service/` to Stats, and the page to the frontend. Database and Redis ports
are not published. All six services use `unless-stopped`.

The old `/opt/xitcoin-testnet/blockscout-testnet` deployment note and the repository's
11.2.7 Compose/build recipe do not identify the accepted installation. Exact
host paths and recovery files belong in the private operator handoff. Do not
run the old recipe against the public project.

## Acceptance scope

The backend runtime, persisted version and API report 11.2.8. Three observations
showed indexed heights 232454, 232467 and 232479 equal to RPC height, with latest
blocks 7.7–10.4 seconds old. Browser checks covered icons, the chart and periodic
Stats responses. Backend and Stats counters retain their periodic lag.
This accepts the targeted explorer update, not the entire testnet.

## Recovery boundary

The cutover used a new final dump, new volumes and official migrations after a
representative private rehearsal. The first post-reload request encountered a
transient 502 from an old Nginx worker. The recorded state
`MANUAL_RETURN_REQUIRED_POSSIBLE_NEW_WRITES` remains historical evidence;
subsequent independent public checks passed. No rollback followed exposure.

For a future incident:

1. Identify the active project and capture a sanitized, read-only status and
   timestamp. Preserve its backend DB, Stats DB and Redis, including all writes
   acquired since exposure.
2. Identify and protect the existing dumps, image archives, old volumes and
   accepted image manifest. Keep at least 5 GiB free; do not prune globally.
3. Plan a new consistent backup and recovery in isolated new volumes under the
   incident's authorization. Reconcile non-reconstructible writes and Redis
   state before selecting any replacement installation.
4. Validate the adapted recovery plan and its data oracle before any switch.
   The private return took 60.07 seconds on its measured copy; this is not a
   public RTO guarantee, and zero data loss is not established.

Never restart the former backend blindly, restore its dump over the active
public DB, or rerun an old upgrade orchestrator. The later v3 convergence helper
was checked separately; a complete second v3 upgrade was not executed.
Blockchain nodes, signing keys and transactions are outside explorer recovery.

## Preserved evidence

The operator handoff retains the original activation report, immutable evidence
hashes, image provenance, dump manifests and private recovery records. The
public inventory contains selected non-secret observations only. The old
backend/frontend and temporary rehearsal containers are stopped; recovery DBs,
Redis, volumes, images, dumps and archives are intentionally retained.
