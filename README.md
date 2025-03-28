# StackAssets: Stacks-Backed Synthetic Assets

StackAssets is a Clarity smart contract platform that allows users to create, trade, and manage synthetic assets backed by STX tokens on the Stacks blockchain.

## Overview

StackAssets enables users to mint synthetic assets representing various real-world assets (like stocks, commodities, or other cryptocurrencies) using STX as collateral. The system maintains a minimum backing ratio to ensure the synthetic assets remain fully collateralized.

## Key Features

- **Synthetic Asset Creation**: Mint synthetic assets backed by STX tokens
- **Price Oracle Integration**: Decentralized price feeds for supported assets
- **Flexible Collateralization**: Maintain positions with a minimum backing ratio of 150%
- **Fee Structure**: Small fees for minting and redemption to support protocol sustainability
- **Governance Controls**: Role-based permissions for contract administration
- **Emergency Controls**: Ability to pause the contract in case of emergencies

## How It Works

1. **Initialization**: Admin initializes supported synthetic assets
2. **Price Feeds**: Authorized data providers update asset prices
3. **Minting**: Users deposit STX and mint synthetic assets
4. **Management**: Users can add more backing to their positions
5. **Redemption**: Users can redeem synthetic assets to get back their STX

## Contract Architecture

The contract includes several key components:

- **Asset Registry**: Manages supported synthetic assets
- **Position Management**: Tracks user positions and collateralization ratios
- **Price Oracle**: Maintains current asset prices
- **Fee System**: Collects and manages protocol fees
- **Governance Module**: Controls protocol parameters and authorized participants

## Function Documentation

### Administrative Functions

- `add-admin(admin)`: Add a governance admin
- `remove-admin(admin)`: Remove a governance admin
- `add-data-provider(data-provider)`: Add an oracle data provider
- `remove-data-provider(data-provider)`: Remove an oracle data provider
- `set-pause-state(paused)`: Emergency pause/unpause contract
- `update-protocol-fees(new-minting-fee, new-redemption-fee, new-liquidation-penalty)`: Update fee structure
- `update-cooldown-period(new-redemption-cooldown)`: Set cooldown period for redemptions
- `withdraw-protocol-fees(recipient)`: Withdraw accumulated protocol fees
- `initialize-asset(token-id, decimals)`: Initialize a new synthetic asset

### Oracle Functions

- `update-price(token-id, price)`: Update asset price

### User Functions

- `mint-synthetic(token-id, backing-amount, synthetic-amount)`: Create a new synthetic position
- `add-backing(token-id, amount)`: Add backing to an existing position
- `redeem-synthetic(token-id, synthetic-amount)`: Redeem synthetic assets for STX

### Read-Only Functions

- `get-position(user, token-id)`: Get position details
- `check-backing-ratio(user, token-id)`: Calculate current backing ratio
- `get-asset-info(token-id)`: Get asset configuration
- `get-asset-stats(token-id)`: Get asset total backing and supply
- `get-current-price(token-id)`: Get current asset price
- `get-protocol-fees()`: Get accumulated protocol fees
- `get-fee-rates()`: Get current fee structure
- `get-protocol-settings()`: Get protocol parameters

## Security Features

- Input validation for all user-provided parameters
- Role-based access control for administrative functions
- Price expiration checks to prevent using stale data
- Cooldown periods to prevent flash loan attacks
- Minimum and maximum limits for minting operations

## Error Codes

| Code | Description |
|------|-------------|
| 100 | Owner only operation |
| 101 | Insufficient backing |
| 102 | Below minimum mint amount |
| 103 | Exceeds maximum mint amount |
| 104 | Invalid asset |
| 105 | Unsafe backing ratio |
| 106 | Position not found |
| 107 | Unauthorized operation |
| 108 | Price data expired |
| 109 | Transfer failed |
| 110 | Position not closed |
| 111 | Invalid fee |
| 112 | Governance only operation |
| 113 | Oracle only operation |
| 114 | Contract paused |
| 115 | Cooldown period active |

## Development and Deployment

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet): Clarity development environment
- [Stacks CLI](https://github.com/blockstack/stacks.js): Stacks blockchain interaction tools

### Local Testing

```bash
# Install dependencies
npm install

# Run tests
clarinet test

# Check contract
clarinet check
```

### Deployment

```bash
# Build contract
clarinet build

# Deploy contract (testnet)
stacks deploy --testnet stackassets.clar
```

## License

[MIT License](LICENSE)

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the project
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Security

If you discover a security vulnerability, please send an email to security@stackassets.com instead of using the issue tracker.