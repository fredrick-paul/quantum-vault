# Quantum Vault

## Advanced Collateralized Lending Engine for the Stacks Blockchain

[![Stacks](https://img.shields.io/badge/Stacks-Blockchain-5D4AAE?logo=stacks)](https://www.stacks.co/)
[![Clarity](https://img.shields.io/badge/Smart_Contracts-Clarity-brightgreen)](https://clarity-lang.org/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Tests](https://img.shields.io/badge/Tests-Vitest-green)](https://vitest.dev/)

## 🌟 Overview

Quantum Vault revolutionizes decentralized finance by creating a trustless, intelligent lending ecosystem where digital asset holders can unlock instant liquidity while maintaining ownership of their appreciating assets. Built on cutting-edge risk assessment algorithms and autonomous market mechanisms, this protocol establishes a fully autonomous lending marketplace that transforms illiquid digital assets into productive capital.

### Key Features

- **🔒 Zero Counterparty Risk**: Execute instant collateral-backed lending with complete trustlessness
- **📊 Adaptive Interest Rates**: Deploy dynamic mechanisms based on real-time supply/demand analytics
- **🛡️ Predictive Liquidation**: AI-powered risk assessment with automated liquidation shields
- **⚖️ Dynamic Optimization**: Maintain protocol solvency through intelligent collateral management
- **🌐 Multi-Chain Ready**: Support for cross-chain asset bridging and maximum capital efficiency
- **🏛️ Enterprise Grade**: Institutional-level security with retail-friendly accessibility

## 🏗️ Architecture

### Core Components

- **Collateral Management System**: Secure asset custody with atomic state transitions
- **Intelligent Lending Engine**: Advanced loan origination with comprehensive risk assessment
- **Autonomous Liquidation**: Real-time monitoring and automated position management
- **Oracle Integration**: Real-time price feeds with sanity checking mechanisms
- **Governance Framework**: Dynamic parameter adjustment for optimal market conditions

### Supported Assets

- **BTC**: Bitcoin collateral support
- **STX**: Stacks native token support
- *Extensible architecture for additional assets*

## 🚀 Quick Start

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) v2.0+
- [Node.js](https://nodejs.org/) v18+
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/fredrick-paul/quantum-vault.git
   cd quantum-vault
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Verify installation**

   ```bash
   clarinet check
   ```

### Development Setup

1. **Start local development environment**

   ```bash
   clarinet console
   ```

2. **Run tests**

   ```bash
   npm test
   ```

3. **Watch mode for continuous testing**

   ```bash
   npm run test:watch
   ```

4. **Generate test coverage report**

   ```bash
   npm run test:report
   ```

## 📖 Usage

### Platform Initialization

Before any operations, the platform must be initialized by the contract owner:

```clarity
;; Initialize the platform (owner-only)
(contract-call? .quantum-vault initialize-platform)
```

### Setting Up Price Feeds

Configure asset prices for collateral valuation:

```clarity
;; Set BTC price (in microSTX or preferred denomination)
(contract-call? .quantum-vault update-price-feed "BTC" u5000000000)

;; Set STX price
(contract-call? .quantum-vault update-price-feed "STX" u1000000)
```

### Basic Lending Operations

#### 1. Deposit Collateral

```clarity
;; Deposit BTC as collateral
(contract-call? .quantum-vault deposit-collateral u100000000) ;; 1 BTC
```

#### 2. Request a Loan

```clarity
;; Request loan with collateral
;; Parameters: collateral-amount, loan-amount
(contract-call? .quantum-vault request-loan u100000000 u50000000)
```

#### 3. Repay Loan

```clarity
;; Repay loan with interest
;; Parameters: loan-id, repayment-amount
(contract-call? .quantum-vault repay-loan u1 u52500000)
```

### Administrative Functions

#### Update Collateral Requirements

```clarity
;; Adjust minimum collateral ratio (owner-only)
(contract-call? .quantum-vault update-collateral-ratio u175) ;; 175%
```

#### Modify Liquidation Threshold

```clarity
;; Update liquidation threshold (owner-only)
(contract-call? .quantum-vault update-liquidation-threshold u130) ;; 130%
```

### Query Functions

#### Get Loan Details

```clarity
;; Retrieve comprehensive loan information
(contract-call? .quantum-vault get-loan-details u1)
```

#### Check User Portfolio

```clarity
;; View user's active loans
(contract-call? .quantum-vault get-user-loans 'ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM)
```

#### Platform Statistics

```clarity
;; Get real-time protocol metrics
(contract-call? .quantum-vault get-platform-stats)
```

## 🧪 Testing

### Test Structure

```
tests/
├── quantum-vault.test.ts    # Main contract tests
└── integration/             # Integration test suites
```

### Running Tests

```bash
# Run all tests
npm test

# Run with coverage
npm run test:report

# Watch mode for development
npm run test:watch

# Clarinet specific tests
clarinet test
```

### Example Test Cases

- Platform initialization and security
- Collateral deposit and withdrawal
- Loan origination and validation
- Interest calculation accuracy
- Liquidation trigger mechanisms
- Administrative function access control

## 📊 Risk Management

### Collateral Requirements

- **Minimum Ratio**: 150% (configurable)
- **Liquidation Threshold**: 120% (configurable)
- **Safety Buffer**: Built-in margin for market volatility

### Interest Rate Model

- **Base Rate**: 5% annual (adjustable)
- **Block-Level Precision**: Interest calculated per Stacks block
- **Compound Calculation**: Automatic interest compounding

### Liquidation Mechanics

- **Automated Monitoring**: Continuous collateral ratio assessment
- **Instant Execution**: Automated liquidation below threshold
- **Slippage Protection**: Price feed validation and bounds checking

## 🛠️ Configuration

### Environment Variables

```bash
### Environment Variables

```bash
# Optional: Custom network configuration
STACKS_NETWORK=testnet
STACKS_API_URL=https://api.testnet.hiro.so

# Development settings
CLARINET_MODE=development
```

```

### Contract Parameters

Key parameters can be adjusted via governance functions:

- `minimum-collateral-ratio`: Minimum collateral requirement
- `liquidation-threshold`: Automatic liquidation trigger
- `platform-fee-rate`: Protocol revenue percentage

## 🔧 API Reference

### Public Functions

| Function | Parameters | Description |
|----------|------------|-------------|
| `initialize-platform` | None | Initialize the protocol (owner-only) |
| `deposit-collateral` | `amount: uint` | Deposit collateral assets |
| `request-loan` | `collateral: uint, loan-amount: uint` | Originate new loan |
| `repay-loan` | `loan-id: uint, amount: uint` | Repay existing loan |
| `update-collateral-ratio` | `new-ratio: uint` | Adjust collateral requirements |
| `update-liquidation-threshold` | `new-threshold: uint` | Modify liquidation trigger |
| `update-price-feed` | `asset: string, price: uint` | Update asset prices |

### Read-Only Functions

| Function | Parameters | Returns |
|----------|------------|---------|
| `get-loan-details` | `loan-id: uint` | Complete loan information |
| `get-user-loans` | `user: principal` | User's active loans |
| `get-platform-stats` | None | Protocol health metrics |
| `get-valid-assets` | None | Supported asset list |

### Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| u100 | `ERR-NOT-AUTHORIZED` | Insufficient permissions |
| u101 | `ERR-INSUFFICIENT-COLLATERAL` | Collateral below requirements |
| u102 | `ERR-BELOW-MINIMUM` | Amount below minimum threshold |
| u103 | `ERR-INVALID-AMOUNT` | Invalid amount specified |
| u104 | `ERR-ALREADY-INITIALIZED` | Platform already initialized |
| u105 | `ERR-NOT-INITIALIZED` | Platform not yet initialized |
| u106 | `ERR-INVALID-LIQUIDATION` | Invalid liquidation attempt |
| u107 | `ERR-LOAN-NOT-FOUND` | Loan ID does not exist |
| u108 | `ERR-LOAN-NOT-ACTIVE` | Loan is not in active status |
| u109 | `ERR-INVALID-LOAN-ID` | Invalid loan identifier |
| u110 | `ERR-INVALID-PRICE` | Price outside valid range |
| u111 | `ERR-INVALID-ASSET` | Asset not supported |

## 🚧 Deployment

### Testnet Deployment

1. **Configure Clarinet for testnet**

   ```bash
   clarinet integrate
   ```

2. **Deploy contract**

   ```bash
   clarinet deploy --testnet
   ```

3. **Verify deployment**

   ```bash
   clarinet call --testnet quantum-vault get-platform-stats
   ```

### Mainnet Deployment

⚠️ **Warning**: Ensure thorough testing before mainnet deployment

1. **Final security audit**
2. **Complete test coverage verification**
3. **Deploy with proper access controls**
4. **Initialize price feeds immediately**

## 🔐 Security

### Audit Status

- [ ] External security audit pending
- [x] Internal code review completed
- [x] Test coverage > 90%
- [x] Static analysis passed

### Security Features

- **Access Control**: Owner-only administrative functions
- **Input Validation**: Comprehensive parameter checking
- **State Protection**: Atomic operations and rollback safety
- **Oracle Security**: Price feed validation and bounds checking
- **Liquidation Safety**: Automated risk management

### Best Practices

- Always test on testnet before mainnet deployment
- Monitor collateral ratios during market volatility
- Regularly update price feeds for accurate valuations
- Implement circuit breakers for extreme market conditions

## 🤝 Contributing

We welcome contributions to improve Quantum Vault! Please follow these guidelines:

### Development Process

1. **Fork the repository**
2. **Create a feature branch**

   ```bash
   git checkout -b feature/amazing-feature
   ```

3. **Make your changes**
4. **Add comprehensive tests**
5. **Ensure all tests pass**

   ```bash
   npm test && clarinet check
   ```

6. **Submit a pull request**

### Code Style

- Follow Clarity best practices and conventions
- Include comprehensive inline documentation
- Write descriptive commit messages
- Maintain test coverage above 90%

### Issue Reporting

Please use the GitHub issue tracker to report bugs or request features. Include:

- Clear description of the issue
- Steps to reproduce
- Expected vs actual behavior
- Relevant code snippets or logs

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Stacks Foundation** for the innovative blockchain platform
- **Clarity Language** for safe smart contract development
- **Hiro Systems** for excellent developer tools
- **DeFi Community** for inspiration and best practices
