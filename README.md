# ChainVerse Onchain

> Soroban smart-contract infrastructure for the ChainVerse Academy Web3 education platform on Stellar.

## Overview

ChainVerse Onchain provides the blockchain layer for ChainVerse Academy. It implements reusable Rust/Soroban contracts for tokens, courses, certificates, escrow, payouts, rewards and staking, with an integration layer that connects the individual contracts into the wider platform.

## Smart Contracts

| Contract | Purpose |
|---|---|
| `chv_token` | CHV utility token: mint, burn, transfer and admin handoff |
| `token` | Generic token implementation with royalty support |
| `certificates` | Course completion certificate issuance and revocation |
| `course_registry` | Course metadata and enrollment records |
| `escrow` | Holds buyer funds until delivery confirmation or expiry |
| `escrow-vault` | Multi-signature vault with threshold approvals |
| `payout-automation` | Batched token payouts to instructors |
| `reward` | One-time learner rewards using signed backend proofs |
| `staking` | Tiered CHV staking, lock periods and emergency unstake |
| `chainverse-core` | Integration/orchestration layer |

## Architecture

```text
Student
  |
  +--> Escrow / Escrow Vault --> Instructor
  |
  +--> Certificates
  |
  +--> Staking --> CHV Token
  |
Backend --> signed reward proof --> Reward --> CHV Token

Course Registry --> course metadata
Payout Automation --> batched instructor payments
ChainVerse Core --> contract integration/orchestration
```

## Technology Stack

- Rust
- Soroban
- Stellar network
- Cargo
- Stellar CLI
- GitHub Actions

## Requirements

- Rust toolchain with `wasm32-unknown-unknown`
- Stellar CLI 21.x (as pinned/configured by the repository)

## Local development

```bash
git clone https://github.com/Oluwatobi843/chainVerse-onchain.git
cd chainVerse-onchain
rustup target add wasm32-unknown-unknown
stellar contract build
cargo test --workspace
```

## Testnet Deployment

The repository includes scripts and documentation for setting up a funded Stellar testnet identity, deploying contracts, initializing them and running smoke tests.

Typical flow:

```bash
./scripts/deploy-testnet.sh
cp .env.testnet.example .env.testnet
./scripts/init-contracts.sh
./scripts/smoke-test.sh
```

Contract IDs should be stored in local environment configuration and must not be committed as secrets.

## Engineering Considerations

The contracts are separated by business responsibility, making the system easier to test, reason about and evolve. Administrative operations and sensitive contract actions are designed around explicit authorization rather than unrestricted public mutation.

## Testing

```bash
cargo test --workspace
```

Additional contract-specific checks and deployment smoke tests are documented under `docs/` and `scripts/`.

## Documentation

See the repository documentation for:

- Contract architecture
- Testnet identity setup
- Testnet deployment
- Contract overview
- Upgrade procedures
- Contribution guidelines

## Portfolio Value

This project demonstrates blockchain backend engineering with **Rust, Soroban, Stellar, smart-contract architecture, escrow, token economics, staking, automated payouts and testnet deployment**.

## Author

**Oluwatobi843**  
https://github.com/Oluwatobi843
