# 🚀 Web 3.0 Cryptocurrency Exchange DApp

A fully functional decentralized cryptocurrency exchange (DEX) built with React, Solidity, and Ethereum. This DApp allows users to swap tokens, provide liquidity, and earn trading fees.

## ✨ Features

- **Token Swapping**: Swap ERC20 tokens with minimal slippage using an automated market maker (AMM)
- **Liquidity Pools**: Add and remove liquidity to earn 0.3% trading fees
- **MetaMask Integration**: Seamless wallet connection with MetaMask
- **Real-time Quotes**: Get instant price quotes before swapping
- **Slippage Protection**: Customizable slippage tolerance
- **Responsive UI**: Beautiful gradient design with TailwindCSS
- **Smart Contracts**: Auditable Solidity contracts with OpenZeppelin libraries

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v18 or higher) - [Download here](https://nodejs.org/)
- **MetaMask** browser extension - [Install here](https://metamask.io/)
- **Git** - [Download here](https://git-scm.com/)

## 🛠️ Installation

### 1. Install Node.js

Download and install Node.js from [nodejs.org](https://nodejs.org/). This will also install npm (Node Package Manager).

Verify installation:
```bash
node --version
npm --version
```

### 2. Install Dependencies

Navigate to the project directories and install dependencies:

**Smart Contracts:**
```bash
cd smart_contracts
npm install
```

**Frontend:**
```bash
cd ../client
npm install
```

## 🚀 Deployment

### Step 1: Deploy Smart Contracts

#### Option A: Deploy to Local Hardhat Network (Recommended for Testing)

1. **Start a local blockchain:**
   ```bash
   cd smart_contracts
   npx hardhat node
   ```
   Keep this terminal running. It will show you test accounts with private keys.

2. **Deploy contracts (in a new terminal):**
   ```bash
   cd smart_contracts
   npm run deploy
   ```

3. **Import test account to MetaMask:**
   - Open MetaMask
   - Click on the account icon → Import Account
   - Copy one of the private keys from the Hardhat node terminal
   - Paste and import

4. **Add Hardhat Network to MetaMask:**
   - Open MetaMask → Settings → Networks → Add Network
   - Network Name: `Localhost`
   - RPC URL: `http://127.0.0.1:8545`
   - Chain ID: `31337`
   - Currency Symbol: `ETH`

#### Option B: Deploy to Sepolia Testnet

1. **Get Sepolia ETH:**
   - Visit [Sepolia Faucet](https://sepoliafaucet.com/)
   - Request test ETH

2. **Configure environment:**
   ```bash
   cd smart_contracts
   cp .env.example .env
   ```

3. **Edit `.env` file:**
   - Add your MetaMask private key (NEVER share this!)
   - Add Alchemy or Infura RPC URL
   - Get API key from [Alchemy](https://www.alchemy.com/) or [Infura](https://infura.io/)

4. **Deploy:**
   ```bash
   npm run deploy:sepolia
   ```

### Step 2: Configure Frontend

1. **Copy deployment addresses:**
   After deployment, you'll see contract addresses in the terminal. Copy them.

2. **Update frontend config:**
   Open `client/src/config.js` and update:
   ```javascript
   export const CONTRACT_ADDRESS = "YOUR_EXCHANGE_CONTRACT_ADDRESS";
   
   export const TOKEN_ADDRESSES = {
     tokenA: "YOUR_TOKEN_A_ADDRESS",
     tokenB: "YOUR_TOKEN_B_ADDRESS",
     tokenC: "YOUR_TOKEN_C_ADDRESS"
   };
   ```

3. **Update network config (if using Sepolia):**
   ```javascript
   export const NETWORK_CONFIG = {
     chainId: 11155111,
     chainName: "Sepolia",
     rpcUrl: "https://eth-sepolia.g.alchemy.com/v2/YOUR_KEY"
   };
   ```

### Step 3: Run Frontend

```bash
cd client
npm run dev
```

Open your browser and navigate to `http://localhost:3000`

## 📱 Using the DApp

### 1. Connect Wallet
- Click "Connect Wallet" button
- Approve the connection in MetaMask
- Make sure you're on the correct network (Localhost or Sepolia)

### 2. Get Test Tokens

If using local network:
```bash
cd smart_contracts
npx hardhat console --network localhost
```

Then in the console:
```javascript
const tokenA = await ethers.getContractAt("MockERC20", "TOKEN_A_ADDRESS");
await tokenA.mint("YOUR_ADDRESS", ethers.parseEther("1000"));
```

### 3. Swap Tokens
- Select tokens to swap
- Enter amount
- Set slippage tolerance
- Click "Swap Tokens"
- Confirm transaction in MetaMask

### 4. Add Liquidity
- Go to "Liquidity" tab
- Select token pair
- Enter amounts (ratio will auto-calculate)
- Click "Add Liquidity"
- Approve both tokens
- Confirm transaction

### 5. Remove Liquidity
- Go to "Liquidity" tab
- Click "Remove Liquidity"
- Click "Remove All Liquidity"
- Confirm transaction

## 🧪 Testing

Run smart contract tests:
```bash
cd smart_contracts
npm test
```

## 📁 Project Structure

```
crypto-exchange-dapp/
├── smart_contracts/
│   ├── contracts/
│   │   ├── CryptoExchange.sol      # Main DEX contract
│   │   └── MockERC20.sol            # Test token contract
│   ├── scripts/
│   │   └── deploy.js                # Deployment script
│   ├── test/
│   │   └── CryptoExchange.test.js   # Contract tests
│   ├── hardhat.config.js            # Hardhat configuration
│   └── package.json
├── client/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Navbar.jsx           # Navigation bar
│   │   │   ├── SwapCard.jsx         # Token swap interface
│   │   │   └── LiquidityCard.jsx    # Liquidity management
│   │   ├── context/
│   │   │   └── Web3Context.jsx      # Web3 integration
│   │   ├── App.jsx                  # Main app component
│   │   ├── config.js                # Contract addresses
│   │   └── abi.js                   # Contract ABIs
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
└── README.md
```

## 🔧 Smart Contract Features

### CryptoExchange.sol

- **createPool**: Create new token pair pools
- **addLiquidity**: Add liquidity to pools and receive LP tokens
- **removeLiquidity**: Remove liquidity and burn LP tokens
- **swap**: Swap tokens with 0.3% fee
- **getAmountOut**: Get quote for token swap
- **getReserves**: Get pool reserves

## 🔐 Security Features

- ReentrancyGuard protection
- Slippage protection
- Proper approval checks
- OpenZeppelin audited contracts

## 🐛 Troubleshooting

### Issue: MetaMask not connecting
- Make sure MetaMask is installed
- Check if you're on the correct network
- Try disconnecting and reconnecting

### Issue: Transaction failing
- Check if you have enough ETH for gas
- Verify token approvals
- Check slippage settings

### Issue: "Insufficient liquidity" error
- Pool needs initial liquidity
- Try adding liquidity first before swapping

### Issue: Contract addresses not found
- Make sure contracts are deployed
- Update `config.js` with correct addresses
- Check you're on the correct network

## 📚 Technologies Used

- **Frontend**: React, Vite, TailwindCSS
- **Web3**: ethers.js v6
- **Smart Contracts**: Solidity 0.8.20
- **Development**: Hardhat
- **Testing**: Chai, Mocha
- **Libraries**: OpenZeppelin Contracts

## 🌐 Networks

- **Local**: Hardhat Network (ChainID: 31337)
- **Testnet**: Sepolia (ChainID: 11155111)
- **Mainnet**: Can be deployed to Ethereum mainnet (not recommended without audit)

## 📄 License

MIT License - feel free to use this project for learning and development.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## ⚠️ Disclaimer

This is a educational project. Do not use in production without proper security audits. Never share your private keys. Always test on testnets first.

## 📞 Support

For issues and questions:
- Open an issue on GitHub
- Check existing issues for solutions

## 🎓 Learn More

- [Solidity Documentation](https://docs.soliditylang.org/)
- [Hardhat Documentation](https://hardhat.org/docs)
- [ethers.js Documentation](https://docs.ethers.org/)
- [React Documentation](https://react.dev/)

---

Built with ❤️ for the Web3 community
