# Public Stats

Stats is served at `https://evm-explorer-testnet.xitcoin.org/stats-service/`.
The main-page endpoint is `/api/v1/pages/main` under that prefix.
The accepted selection is total blocks, total transactions and daily new
transactions, with a 60-second schedule and frontend refetch interval.
`newTxnsWindow` presents 30 completed days; `newTxns` retains its separate
current-day behavior. Counts use Tx/day, while native amounts use XTC/18 decimals.

The 13 September 2026 public browser evidence consumed Stats HTTP 200 responses
63.049 and 60.037 seconds apart and rendered 1 transaction on 2 September and
2 on 9 September. Source SQL and Stats timestamps advanced. Stats lagged the
block samples by 5–8 blocks; those observations do not establish a permanent
lag bound. Compare matching periods and timestamps, not an old counter with a
new RPC height. The main page is an indexing view, not consensus proof.
