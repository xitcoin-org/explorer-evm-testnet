# Blockscout Frontend Configuration

The Xitcoin explorer uses Blockscout's supported network-logo, network-icon and favicon environment variables.

Canonical artwork:

- network logo: `assets/png/standard/xitcoin-symbol-500.png`;
- network icon: `assets/png/standard/xitcoin-symbol-200.png`;
- source repository: https://github.com/xitcoin-org/brand.

No source patch is required for token branding. This keeps frontend upgrades aligned with upstream Blockscout and avoids maintaining version-specific wordmark changes.

Validate the resolved frontend configuration before building or deploying:

```bash
docker compose -f frontend-compose.yml config
```
