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

### 3. Methods of Interaction

* **A. Wallets (MetaMask - User/Dev Perspective):**
    * **Connecting to Networks:** MetaMask allows switching between Mainnet, common Testnets (add Sepolia if not default), and even Localhost (for Hardhat Network/Ganache).
    * **Checking Balance:** Shows native currency (ETH) balance for the selected network.
    * **Sending Transactions:** Initiate transfers of ETH/tokens. Requires confirmation (signing) and gas.
    * **Interacting with dApps:** Websites can prompt MetaMask to connect, sign messages, or send transactions to interact with smart contracts.
    * **(Hands-on):**
        1.  Switch MetaMask to the Sepolia network.
        2.  Get Sepolia ETH from a faucet.
        3.  Send a small amount of Sepolia ETH to another account (maybe a classmate's or a second account you create). Observe the process.

* **B. Blockchain Explorers (Read-Only Data):**
    * **Purpose:** Web-based tools to view blocks, transactions, addresses, and contract data/source code (if verified).
    * **Examples:** Etherscan (Ethereum), PolygonScan, BscScan, Sepolia Etherscan.
    * **(Hands-on):**
        1.  Find the transaction hash of the Sepolia ETH transfer you just made (in MetaMask activity).
        2.  Go to `https://sepolia.etherscan.io/` and paste the transaction hash.
        3.  Explore the details: Sender, receiver, amount, gas used, block number, timestamp.
        4.  Look up your own Sepolia address. View its balance and transaction history.

* **C. Development Framework Consoles (Developer Perspective):**
    * **Purpose:** Command-line interface for direct interaction with a network (local or remote) using JavaScript commands, often with pre-loaded libraries like Ethers.js.
    * **Hardhat Console:** `npx hardhat console [--network networkName]`
        * `--network localhost`: Connects to the persistent node started with `npx hardhat node`.
        * `--network sepolia`: Connects to the Sepolia testnet (requires configuration in `hardhat.config.js`).
    * **(Hands-on - Local Network):**
        1.  Make sure the default `Lock.sol` contract is compiled (`npx hardhat compile`).
        2.  In one terminal, start a local node: `npx hardhat node` (Note the available accounts and private keys - **NEVER SHARE REAL PRIVATE KEYS**).
        3.  In *another* terminal (in the same project directory), run: `npx hardhat console --network localhost`
        4.  Inside the console, try JavaScript commands using `ethers` (Hardhat automatically injects it):
            * `await ethers.provider.getBlockNumber()`
            * `const signers = await ethers.getSigners()`
            * `const balance = await ethers.provider.getBalance(signers[0].address)`
            * `console.log(ethers.formatEther(balance))` // Display balance in Ether
        5.  Deploy the `Lock` contract from the console:
            * `const Lock = await ethers.getContractFactory("Lock")`
            * `const unlockTime = Math.floor(Date.now() / 1000) + 60` // Set unlock time to 1 minute from now
            * `const lockedAmount = ethers.parseEther("0.001")` // Lock 0.001 fake ETH
            * `const lock = await Lock.deploy(unlockTime, { value: lockedAmount })`
            * `await lock.waitForDeployment()`
            * `console.log("Lock deployed to:", await lock.getAddress())`
        6.  Interact with the deployed contract:
            * `const deployedAddress = await lock.getAddress()`
            * `const lockContract = await ethers.getContractAt("Lock", deployedAddress)`
            * `await lockContract.unlockTime()` // Read the unlock time
            * // Wait a minute, then try: `await lockContract.withdraw()` (This sends a transaction)

* **D. Scripts (Automated Interaction - Developer Perspective):**
    * **Purpose:** Write scripts (usually JavaScript using Ethers.js/Web3.js via Hardhat/Truffle) to automate tasks like deployment, contract calls, testing complex interactions.
    * **Hardhat Scripts:** Use the `scripts/` folder. Run with `npx hardhat run scripts/yourScript.js [--network networkName]`.
    * **(Hands-on):**
        1.  Examine the `scripts/deploy.js` file created by Hardhat. Understand how it uses `ethers.getContractFactory` and `deploy`.
        2.  Modify `deploy.js` slightly if needed (e.g., change the `lockedAmount`).
        3.  Configure `hardhat.config.js` for Sepolia:
            * You'll need a Sepolia RPC URL (from Infura/Alchemy).
            * You'll need a private key for an account funded with Sepolia ETH. **Use environment variables (`dotenv` package) to handle private keys securely, don't hardcode them!**
            * Example `hardhat.config.js` snippet (install `dotenv` first: `npm install dotenv --save-dev`):
                ```javascript
                require("@nomicfoundation/hardhat-toolbox");
                require("dotenv").config(); // Add this line

                /** @type import('hardhat/config').HardhatUserConfig */
                module.exports = {
                  solidity: "0.8.24", // Match your contract's pragma (Update if needed)
                  networks: {
                    sepolia: {
                      url: process.env.SEPOLIA_RPC_URL || "", // Get from Infura/Alchemy
                      accounts: process.env.PRIVATE_KEY !== undefined ? [process.env.PRIVATE_KEY] : [], // Your funded account's private key
                    },
                    // You can add other networks like mainnet, polygon, etc.
                  },
                };
                ```
            * Create a `.env` file in your project root (add it to `.gitignore`!):
                ```dotenv
                SEPOLIA_RPC_URL="YOUR_ALCHEMY_OR_INFURA_SEPOLIA_URL"
                PRIVATE_KEY="YOUR_SEPOLIA_TESTNET_ACCOUNT_PRIVATE_KEY"
                ```
        4.  Run the deployment script on Sepolia: `npx hardhat run scripts/deploy.js --network sepolia`
        5.  Verify the deployment: Check Etherscan for the contract address printed by the script.

* **E. SDKs (Ethers.js / Web3.js / Web3.py etc. - Programmatic Interaction):**
    * **Purpose:** Libraries used within applications (backend scripts, frontend dApps) to communicate with the blockchain (via Node RPC). Frameworks like Hardhat bundle these.
    * **Key Concepts:** Provider (connection to node), Signer (account/wallet), Contract object (abstraction to call functions).
    * **(Brief Mention):** Explain that the Console and Scripts examples were using Ethers.js under the hood via the Hardhat environment.

