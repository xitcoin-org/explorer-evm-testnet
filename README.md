# Xitcoin EVM Testnet Explorer

Reproducible Blockscout configuration and Xitcoin branding for the public EVM explorer.

## Network

| Property | Value |
|---|---|
| Network | Xitcoin Testnet |
| EVM chain ID | `101089` |
| Native currency | XTC |
| Decimals | 18 |
| Explorer | https://evm-explorer-testnet.xitcoin.org/ |
| JSON-RPC | https://evm-rpc-testnet.xitcoin.org/ |

Cosmos-style and EVM-style addresses coexist on Xitcoin Testnet. This does not imply a bridge or a second token: XTC is the native asset exposed through both interfaces.

Canonical public network configuration is maintained in [`xitcoin-org/testnets`](https://github.com/xitcoin-org/testnets). Node software is maintained in [`xitcoin-org/pos-chain`](https://github.com/xitcoin-org/pos-chain).

## Configuration

Create the local environment file, provide the required deployment values, then validate the complete Compose configuration:

```bash
cp .env.example .env

docker compose \
  --env-file .env \
  -f docker-compose.yml \
  -f frontend-compose.yml \
  config
```

The `.env` file is excluded from version control. Runtime values are supplied by the deployment environment.

## Branding and contract references

Official logo assets are loaded from [`xitcoin-org/brand`](https://github.com/xitcoin-org/brand). Cronos token and contract references are maintained in [`xitcoin-org/contracts`](https://github.com/xitcoin-org/contracts).

## API

The public API reference is stored at [`docs/api/xitcoin-testnet-api-v2.json`](docs/api/xitcoin-testnet-api-v2.json).

## Image provenance

Image source commits, build parameters, SBOMs and provenance attestations are documented in [`docs/BLOCKSCOUT_IMAGE_PROVENANCE.md`](docs/BLOCKSCOUT_IMAGE_PROVENANCE.md).

## Upstream

The explorer uses Blockscout. Xitcoin configuration is maintained separately from upstream source code so deployments remain reproducible and upgrades can be reviewed independently.

## Security

Security reports follow [`SECURITY.md`](SECURITY.md).

## License

Original Xitcoin-authored configuration and documentation are available under the [MIT License](LICENSE). Blockscout images and other third-party components retain their upstream terms; see [third-party notices](THIRD_PARTY_NOTICES.md).

## Public deployment observed on 13 September 2026

The public explorer serves backend **11.2.8**, the corrected frontend and Stats.
See [deployment and recovery](docs/DEPLOYMENT.md), the
[deployment inventory](docs/PUBLIC_DEPLOYMENT.json) and [Stats](docs/STATS.md).

The checked-in Compose files and manual image-build workflow describe an earlier
11.2.7 recipe. They are not the manifest of this accepted installation and must
not be replayed over it. The public images were qualified separately; no new GHCR
publication or complete distribution attestation is claimed. See the
[remaining notice provenance](docs/NOTICE_PROVENANCE.md).
