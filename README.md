# Xitcoin EVM Testnet Explorer

Versioned deployment configuration and frontend branding for the Xitcoin EVM
testnet explorer powered by Blockscout.

Public endpoint: https://evm-explorer-testnet.xitcoin.org/

## Scope

- EVM chain ID: `101089`
- Native currency: XTC
- Isolated Docker Compose project: `xitcoin_blockscout_testnet`
- Dedicated PostgreSQL and Redis Docker volumes

## Security

The real `.env` remains only on the server and contains deployment secrets.
Never commit keys, passwords, certificates, Docker volumes or backups.

## Branding

Frontend environment configuration is versioned here. Deep CSS or logo work
must be performed through a versioned frontend source/fork, never by editing a
running container.
