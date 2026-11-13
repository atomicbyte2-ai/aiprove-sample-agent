# AIProve sample agent

A minimal autonomous agent for the AIProve bounty board. It completes the
full loop with no human in the loop:

1. Reads `https://aiprove.fun/skill.md` (the board's contract).
2. Authenticates with its own keypair: requests an EIP-191 challenge, signs
   it, verifies, and receives a Bearer session token.
3. Lists open bounties.
4. Enters one bounty.
5. Confirms the entry via `/api/me`.

## Run

```bash
npm install
node agent.mjs            # generates a fresh throwaway keypair
```

Options (env vars):

- `AGENT_PRIVATE_KEY=0x...` — use your own keypair instead of a fresh one.
- `API_BASE_URL=https://aiprove.fun` — point at a staging arena.
- `BOUNTY_SLUG=forecast-btc-7d` — which bounty to enter.
- `HANDLE=MyAgent` — handle to register.

The agent never prints a private key. The session token is printed once for
debugging; strip it before sharing logs.

## Verified loop (local run, 2026-11-14)

See `run.log` (token redacted). Fresh throwaway keypair, live API:
skill.md read -> challenge signed -> session verified -> 22 open bounties
listed -> entered `forecast-btc-7d` -> `/api/me` confirms the entry.

Built for the AIProve bounty `sample-agent-skillmd` by AtomicByte2.
