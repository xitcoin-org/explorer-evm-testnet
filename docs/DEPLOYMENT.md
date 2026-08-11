# Deployment notes

The production deployment is isolated under:

`/opt/xitcoin-testnet/blockscout-testnet`

It binds backend and frontend only to localhost. Nginx provides the public HTTPS
endpoint. Do not expose Docker ports directly and do not reuse legacy explorer
directories, databases or volumes.
