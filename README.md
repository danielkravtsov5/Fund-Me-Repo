This project implements a decentralized funding contract using Solidity and Foundry.
It allows users to fund the contract with ETH and enables the owner to withdraw the collected funds.
A Chainlink price feed is integrated to ensure a minimum USD-denominated funding threshold.

📂 Project Structure
src/
 ├─ FundMe.sol             # Main funding contract
 ├─ PriceConverter.sol     # Library for ETH/USD conversion
 └─ mockV3Aggregator.sol   # Mock Chainlink price feed for local tests

script/
 ├─ DeployFundMe.s.sol     # Deployment script (local/testnet)
 ├─ HelperConfig.s.sol     # Configures Chainlink or mock feeds
 └─ Interactions.s.sol     # Scripts for funding and withdrawing

test/
 ├─ FundMeTest.t.sol       # Unit tests for core functionality
 └─ InteractionsTest.t.sol # Integration tests for user interactions

⚙️ Deployment

Deploy to Sepolia testnet:

forge script script/DeployFundMe.s.sol:DeployFundMe \
  --rpc-url $SEPOLIA_RPC_URL \
  --private-key $PRIVATE_KEY \
  --broadcast --verify --etherscan-api-key $ETHERSCAN_API_KEY -vvvv

🧪 Testing

Run all local tests:

forge test -vvv


Run integration tests on a Sepolia fork:

forge test --fork-url $SEPOLIA_RPC_URL -vvvv

🧰 Environment Variables

Create a .env file in your project root and fill it with:

SEPOLIA_RPC_URL="https://eth-sepolia.g.alchemy.com/v2/..."
PRIVATE_KEY="your_private_key_here"
ETHERSCAN_API_KEY="your_etherscan_api_key_here"

🪙 Features

Fund the contract using ETH, converted to USD via Chainlink price feeds

Withdraw funds restricted to the contract owner

Configurable for both local and testnet environments

Fully tested using Foundry cheatcodes (vm.deal, vm.prank, vm.startBroadcast, etc.)

🧱 Makefile Shortcuts

You can simplify commands using the included Makefile:

make build          # Compile contracts
make test           # Run all tests
make deploy-sepolia # Deploy to Sepolia networks