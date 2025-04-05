# Blockchain Development Fundamentals

## Part 1: Setting Up Blockchain Development Tools

### 1. Introduction: Why Do We Need Special Tools?

* **Analogy:** Just like web developers need browsers, code editors, and servers, blockchain developers need specialized tools.
* **Core Tasks:** Writing smart contracts, compiling them into bytecode, testing their logic, deploying them to a blockchain network, and interacting with them.
* **Complexity:** Blockchains are distributed, immutable systems. Tools help manage this complexity, automate tasks, and provide a safe testing environment.

### 2. Key Categories of Tools

* **A. Nodes & Networks:** Your gateway to the blockchain.
    * **What is a Node?** Software that connects to the blockchain network, validates transactions/blocks, and holds a copy (or partial copy) of the ledger.
    * **Types of Nodes:** Full Nodes (store all data), Light Nodes (store headers), Archive Nodes (store all historical states).
    * **Running Your Own Node:** Tools like Geth, Nethermind, Besu, Erigon. (Mention this is resource-intensive and often not necessary for beginners).
    * **Node-as-a-Service (NaaS):** Providers like **Infura**, **Alchemy**. They run nodes for you, and you connect via an API key. *This is the most common starting point for developers.*
    * **Local Development Networks:** Simulate a blockchain on your own computer. Instant transactions, free gas. Examples: **Hardhat Network** (built into Hardhat), **Ganache**. Essential for rapid development and testing.

* **B. Smart Contract Languages:** The language you write your logic in.
    * **Solidity:** The most popular language for EVM-compatible chains (Ethereum, Polygon, BSC, etc.). C-like syntax. *Focus on this first.*
    * **Vyper:** Pythonic syntax, aims for simplicity and security.
    * **Others:** Rust (Solana, Near), Go (Hyperledger Fabric). (Mention briefly for context).

* **C. Development Frameworks:** Your integrated development environment.
    * **Purpose:** Streamline compiling, testing, deploying, and managing smart contracts.
    * **Popular Choices (EVM):**
        * **Hardhat (Recommended):** JavaScript/TypeScript based. Flexible, fast local network, great tooling (console, testing utilities), large community support.
        * **Truffle:** Older, well-established JavaScript framework. Includes Ganache GUI/CLI for a local network.
        * **Foundry:** Newer, Rust-based framework. Known for speed, allows writing tests in Solidity. Steeper learning curve if unfamiliar with Rust/command line.
        * **Brownie:** Python-based framework. Good choice for Python developers.

* **D. Code Editors & Extensions:** Where you write the code.
    * **VS Code (Highly Recommended):** Free, powerful, huge extension marketplace.
    * **Essential Extensions:**
        * `Solidity` by Juan Blanco (or Nomic Foundation's Hardhat VSCode) - Syntax highlighting, linting, compilation help.
        * Prettier/Linters - Code formatting.

* **E. Wallets:** For managing accounts and interacting with dApps/contracts.
    * **Browser Extension Wallets:** **MetaMask** is the standard. Allows users (and developers during testing) to sign transactions and interact with dApps directly from the browser.
    * **Hardware Wallets:** Ledger, Trezor (Mention for security context, less critical for initial setup).

* **F. Package Managers:** For installing frameworks and libraries.
    * **npm (Node Package Manager) / yarn:** Used for JavaScript-based tools (Hardhat, Truffle, Ethers.js, Web3.js).

* **G. Version Control:** Essential for any software development.
    * **Git / GitHub (or similar):** Track changes, collaborate, backup code.

### 3. Step-by-Step Setup Guide (Using Hardhat - Recommended Path)

* **(Prerequisites):** Basic command-line familiarity.
* **Step 1: Install Node.js and npm:**
    * Go to <https://nodejs.org/> and download the LTS (Long-Term Support) version for your OS.
    * Verify installation: Open terminal/command prompt and type `node -v` and `npm -v`.
* **Step 2: Install Git:**
    * Go to <https://git-scm.com/> and download/install if you don't have it.
    * Verify: `git --version`.
* **Step 3: Install VS Code:**
    * Go to <https://code.visualstudio.com/> and install.
    * Open VS Code, go to the Extensions view (Ctrl+Shift+X or Cmd+Shift+X) and install the `Solidity` extension (e.g., by Juan Blanco or Nomic Foundation).
* **Step 4: Install MetaMask:**
    * Go to <https://metamask.io/> and install the browser extension for Chrome/Firefox/Brave/Edge.
    * Follow the setup instructions: Create a new wallet, **SECURELY back up your Secret Recovery Phrase (Seed Phrase)**, and set a password. Emphasize the importance of seed phrase security.
* **Step 5: Create Your First Project:**
    * Open your terminal/command prompt.
    * Create a new directory: `mkdir my-blockchain-project`
    * Navigate into it: `cd my-blockchain-project`
    * Initialize npm project: `npm init -y` (This creates a `package.json` file).
* **Step 6: Install Hardhat:**
    * In your project directory terminal: `npm install --save-dev hardhat`
    * *Explanation:* Installs Hardhat and a helpful toolbox plugin (includes ethers.js, waffle testing, etc.). `--save-dev` marks it as a development dependency.
* **Step 7: Initialize Hardhat Project:**
    * Run: `npx hardhat init`
    * Choose "Create a JavaScript/TypeScript project" (select JavaScript for simplicity first).
    * Accept defaults for project root, adding `.gitignore`.
    * Install sample project dependencies if prompted (`npm install`).
    * *Explore:* Look at the generated folders (`contracts/`, `scripts/`, `test/`) and the `hardhat.config.js` file.

### 4. Quick Test - Compile Sample Contract

* In the terminal (in your project directory): `npx hardhat compile`
* This should compile the sample `Lock.sol` contract found in the `contracts/` folder.

---

## Part 2: Hands-on: Interacting with Blockchains

### 1. Understanding Interaction

* **Reading Data (Queries):** Checking balances, reading smart contract state variables, viewing transaction history. Generally free, doesn't require signing.
* **Writing Data (Transactions):** Sending currency (like ETH), deploying contracts, calling functions that change contract state. Requires signing with a private key and usually costs "gas" (transaction fees).

### 2. Choosing Your Network: Where do you want to interact?

* **A. Local Development Network (Hardhat Network):**
    * **Use Case:** Initial development, running automated tests, rapid prototyping.
    * **Pros:** Instant transactions, no real cost (gas is simulated), default accounts pre-funded with fake ETH, state reset on restart (usually).
    * **How to Use:** Often runs automatically when you use Hardhat tasks (like `test` or `run script`). Can also run a persistent local node: `npx hardhat node`.

* **B. Testnets (e.g., Sepolia for Ethereum, Mumbai for Polygon):**
    * **Use Case:** Staging environment before mainnet, testing integrations with other testnet contracts, sharing demos.
    * **Pros:** Mimics mainnet behavior more closely, uses free test tokens (obtained from "faucets").
    * **Cons:** Transactions take time, requires test ETH (faucets can sometimes be slow or limited), network can be reset occasionally by core devs.
    * **How to Get Test ETH:** Find a faucet for the specific testnet (e.g., search "Sepolia faucet Alchemy" or "Mumbai faucet Polygon"). You'll need to provide your wallet address.

* **C. Mainnets (Ethereum, Polygon, BSC, etc.):**
    * **Use Case:** Production deployment, real users, real value.
    * **Pros:** The "real" network.
    * **Cons:** Transactions cost real money (gas fees can be high!), irreversible actions, requires utmost security. **Beginners should interact mainly with Testnets.**

### 3. 🔍 Verifying Your Contracts

Once your contract is ready, the next step is to deploy it to a live network and **verify its source code**.

Verifying a contract means making its source code public—along with the compiler settings you used—so that anyone can compile it and compare the generated bytecode with the one deployed on-chain. This is **crucial for transparency** in an open platform like Ethereum.

In this guide, we'll walk through verifying a contract using the **Etherscan explorer**.

> 💡 **TIP:**
> If your contract was deployed outside Hardhat Ignition, or you'd prefer to verify it on Sourcify, use the [`hardhat-verify`](https://hardhat.org/hardhat-runner/plugins/nomicfoundation-hardhat-verify) plugin instead.

---

## 🗝️ Getting an Etherscan API Key

1. Visit [etherscan.io](https://etherscan.io), log in (or sign up).
2. Go to **API Keys** tab → Click **Add** → Name it (e.g., `Hardhat`).
3. Copy the generated key.

Store the key as a configuration variable:

```bash
npx hardhat vars set ETHERSCAN_API_KEY
```

> 💡 Learn more about setting and using config variables in the [Hardhat Vars Guide](https://hardhat.org/hardhat-runner/docs/guides/using-hardhat-vars).

---

## ⚙️ Update Hardhat Config

Inside `hardhat.config.js`:

```javascript
const { vars } = require("hardhat/config");

const ETHERSCAN_API_KEY = vars.get("ETHERSCAN_API_KEY");

module.exports = {
  // ...rest of your config
  etherscan: {
    apiKey: ETHERSCAN_API_KEY,
  },
};
```

---

### 🌐 Deploying and Verifying on Sepolia Testnet

We'll use the **Sepolia testnet** for deployment.

You need:

- A **JSON-RPC provider** like [Infura](https://infura.io) or [Alchemy](https://alchemy.com)
- Your **Sepolia account private key**
- Sepolia **test ETH** (get from a faucet)

### 🔧 Setup Infura + Sepolia in Config

```javascript
const INFURA_API_KEY = vars.get("INFURA_API_KEY");
const SEPOLIA_PRIVATE_KEY = vars.get("SEPOLIA_PRIVATE_KEY");
const ETHERSCAN_API_KEY = vars.get("ETHERSCAN_API_KEY");

module.exports = {
  networks: {
    sepolia: {
      url: `https://sepolia.infura.io/v3/${INFURA_API_KEY}`,
      accounts: [SEPOLIA_PRIVATE_KEY],
    },
  },
  etherscan: {
    apiKey: {
      sepolia: ETHERSCAN_API_KEY,
    },
  },
};
```

---

## 💧 Get Sepolia Test ETH

Use any of the following faucets:

- [Alchemy Sepolia Faucet](https://sepoliafaucet.com/)
- [QuickNode Faucet](https://faucet.quicknode.com/sepolia)
- [Ethereum Ecosystem Faucet](https://faucet.paradigm.xyz/)

---

## 🛠️ Make Your Contract Unique

To avoid verification collisions, make the contract source **unique** by adding a custom comment:

```solidity
// Author: @janedoe
contract Lock {
    // ...
}
```

---

## 🚀 Deploy with Ignition

Use the Ignition module we created earlier (e.g., `Lock.js`) to deploy:

```bash
npx hardhat ignition deploy ignition/modules/Lock.js --network sepolia --deployment-id sepolia-deployment
```

> 📝 The `--deployment-id` flag is optional but recommended. It makes it easier to reference your deployment when verifying.

---

## ✅ Verify with Ignition

Once deployed, verify the contract:

```bash
npx hardhat ignition verify sepolia-deployment
```

Or combine deployment and verification in one command:

```bash
npx hardhat ignition deploy ignition/modules/Lock.js --network sepolia --verify
```

> ⚠️ If you get an error like `address does not have bytecode`, wait a minute. Etherscan may still be indexing your contract.

After a successful run, you’ll get a link to your **verified contract** on Etherscan! 🎉
