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

Canonical network identity is maintained in [`xitcoin-org/pos-chain`](https://github.com/xitcoin-org/pos-chain).

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

## Upstream

The explorer uses Blockscout. Xitcoin configuration is maintained separately from upstream source code so deployments remain reproducible and upgrades can be reviewed independently.

## Security

Security reports follow [`SECURITY.md`](SECURITY.md).

## License

Original Xitcoin-authored configuration and documentation are available under the [MIT License](LICENSE). Blockscout images and other third-party components retain their upstream terms; see [third-party notices](THIRD_PARTY_NOTICES.md).
