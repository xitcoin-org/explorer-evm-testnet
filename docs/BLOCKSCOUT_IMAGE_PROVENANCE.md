# Blockscout image provenance

The Xitcoin EVM Testnet explorer uses images built from immutable official
Blockscout source commits.

## Backend

- Upstream repository: https://github.com/blockscout/blockscout
- Release: `v11.2.7`
- Commit: `c60abc6d680a151abce634649283cf2934fee503`
- Dockerfile: `docker/Dockerfile`
- Build arguments:
  - `RELEASE_VERSION=11.2.7`
  - `BLOCKSCOUT_VERSION=v11.2.7`

## Frontend

- Upstream repository: https://github.com/blockscout/frontend
- Release: `v2.10.3`
- Commit: `10d8428db2f3b5a832640ea2e68ddcc33eff3a49`
- Dockerfile: `Dockerfile`
- Build arguments:
  - `GIT_COMMIT_SHA=10d8428db2f3b5a832640ea2e68ddcc33eff3a49`
  - `GIT_TAG=v2.10.3`

## Publication policy

The workflow publishes version-tagged and commit-tagged images to the Xitcoin
GitHub Container Registry. It also publishes SBOM and build-provenance
attestations.

The deployment Compose files must use an immutable digest produced by a
successful workflow run. Mutable `latest` tags are prohibited.
