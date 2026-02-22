# Foundry Fundamental

A collection of Solidity smart contract projects built while learning [Foundry](https://book.getfoundry.sh/) through the [Cyfrin Updraft](https://updraft.cyfrin.io/) course.

## Projects

### 1. Simple Storage

> Foundry basics: contracts, scripts, and tests.

A basic contract that stores a favorite number and maintains a list of people mapped to their numbers. Covers `forge build`, `forge test`, and deployment scripting with `vm.startBroadcast()`.

### 2. Fund Me

> Chainlink price feeds, multi-chain deployment, and gas optimization.

A crowdfunding contract that enforces a minimum $5 USD contribution using Chainlink ETH/USD price feeds. Features:
- `PriceConverter` library for on-chain ETH/USD conversion
- `HelperConfig` pattern for multi-chain deployment (Sepolia, Mainnet, Anvil)
- `MockV3Aggregator` for local testing
- Gas-optimized `cheaperWithdraw()` vs standard `withdraw()` comparison
- Interaction scripts using `foundry-devops` to target the latest deployment
- Unit and integration tests

### 3. Fund Me Frontend

> Web frontend stub for the Fund Me contract.

A bare HTML/JS scaffold intended to connect a browser wallet to the deployed `FundMe` contract.

### 4. ERC-20

> Token standards with OpenZeppelin.

A minimal ERC-20 token inheriting from OpenZeppelin's `ERC20`. Mints 1,000,000 tokens to the deployer on construction.

### 5. ERC-721

> NFT minting with URI storage.

A basic ERC-721 NFT contract using OpenZeppelin's `ERC721URIStorage`. Supports minting with auto-incrementing token IDs and IPFS metadata URIs.

### 6. Dynamic ERC-721

> Mutable NFT metadata.

An ERC-721 variant where token URIs can be updated after minting, demonstrating dynamic/evolving NFTs. Token IDs are caller-supplied rather than auto-incremented.

### 7. Lottery (Raffle)

> Chainlink VRF V2 Plus + Automation for a provably fair lottery.

The most complex project. A fully automated raffle system where:
- Users enter by paying an entrance fee
- Chainlink Automation (`checkUpkeep` / `performUpkeep`) triggers the draw after a time interval
- Chainlink VRF V2 Plus provides verifiable randomness to pick a winner
- The winner receives the entire contract balance
- Deploy scripts handle VRF subscription creation, funding, and consumer registration

Includes extensive tests using `vm.warp`, `vm.roll`, and `vm.recordLogs` to simulate the full lifecycle.

### 8. Slots Demo

> EVM storage layout internals.

An educational deep-dive into how Solidity assigns storage slots. Demonstrates `keccak256`-based slot computation for mappings, dynamic arrays, and nested structures using inline assembly (`sload`) and `console2` logging.

## Tech Stack

| Dependency | Used In |
|---|---|
| [Foundry](https://book.getfoundry.sh/) (forge-std) | All projects |
| [OpenZeppelin Contracts](https://github.com/OpenZeppelin/openzeppelin-contracts) | ERC-20, ERC-721, Dynamic ERC-721 |
| [Chainlink](https://github.com/smartcontractkit/chainlink-brownie-contracts) | Fund Me (Price Feeds), Lottery (VRF V2 Plus, Automation) |
| [foundry-devops](https://github.com/Cyfrin/foundry-devops) | Fund Me, ERC-721, Lottery |

## Getting Started

### Prerequisites

- [Foundry](https://book.getfoundry.sh/getting-started/installation)

### Build & Test

Each project is self-contained. Navigate into any project directory and run:

```bash
cd simple-storage  # or any other project
forge install
forge build
forge test
```

### Deploy (Local Anvil)

```bash
# Start a local node
anvil

# Deploy (in a separate terminal)
forge script script/Deploy.s.sol --rpc-url http://localhost:8545 --broadcast
```

## Acknowledgements

- [Cyfrin Updraft](https://updraft.cyfrin.io/) - Course material and curriculum
- [Patrick Collins](https://github.com/PatrickAlpworker) - Course instructor
