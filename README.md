# SentinelX — Autonomous Risk Engine for Solana Perpetuals

**An intelligent, cross-venue risk management and on-chain risk enforcement system for Solana perpetual markets.**

SentinelX is a full-stack decentralized finance (DeFi) risk management platform designed to monitor perpetual futures markets across multiple Solana-based trading venues. It continuously aggregates market data, calculates real-time financial risk and divergence metrics, identifies potential systemic imbalances, and dynamically enforces leverage limits and collateral requirements through on-chain smart contracts.

The project combines blockchain technology, financial analytics, real-time data processing, and interactive visualization to provide a unified risk intelligence layer for decentralized perpetual markets.

---

## Table of Contents

- [Project Overview](#-project-overview)
- [Project Objectives](#-project-objectives)
- [Key Features](#-key-features)
- [System Architecture](#-system-architecture)
- [Technology Stack](#-technology-stack)
- [How SentinelX Works](#-how-sentinelx-works)
- [Getting Started](#-getting-started)
- [Testing](#-testing)
- [Repository Structure](#-repository-structure)
- [Team Members](#-team-members)
- [Future Enhancements](#-future-enhancements)
- [License](#-license)

---

## Project Overview

Decentralized perpetual markets operate across multiple trading venues, each with its own liquidity, funding rates, open interest, and price dynamics.

When significant differences emerge between these venues, they can create market instability, increase liquidation risk, and potentially trigger cascading failures.

SentinelX addresses this challenge by introducing an autonomous risk management and intelligence layer that:

- Aggregates market information from multiple perpetual trading venues.
- Evaluates market conditions using financial and statistical risk metrics.
- Detects price divergence, liquidity imbalances, and potential contagion.
- Generates an Ecosystem Risk Score between 0 and 100.
- Dynamically adjusts leverage caps and collateral requirements.
- Enforces risk policies through Solana smart contracts.

The platform provides both a backend risk engine and an interactive dashboard, allowing users to monitor market conditions, understand risk factors, and interact with a test trading environment.

## Project Objectives

1. Develop a unified risk monitoring system for multiple Solana perpetual trading venues.
2. Implement real-time financial and statistical risk calculations.
3. Identify cross-venue divergence and systemic contagion conditions.
4. Develop an on-chain mechanism for enforcing risk policies.
5. Provide an interactive dashboard for risk visualization and position management.
6. Demonstrate the integration of full-stack development, financial analytics, and blockchain smart contracts in a single application.

---

## Key Features

### 1. Multi-Venue Data Aggregation

SentinelX integrates market data from multiple Solana perpetual trading venues.

**Phoenix**
- Orderbook depth and liquidity information.
- Mark and index prices.
- Funding rates and trading volume.

**Velocity**
- Perpetual market account information through its SDK.
- Open interest and market spreads.
- Venue-specific market conditions.

Additional venue adapters are included in the project architecture for extensibility.

### 2. Cross-Venue Risk and Divergence Engine

The risk engine calculates an Ecosystem Risk Score from 0 to 100 and identifies systemic imbalances across five major dimensions.

| Risk Dimension | Description |
|---|---|
| Price Divergence | Measures differences between venue mark prices using spread and coefficient of variation. |
| Funding Rate Divergence | Identifies deviations in funding rates across venues. |
| Open Interest Concentration | Uses the Herfindahl-Hirschman Index (HHI) to measure concentration of open interest. |
| Liquidity Spread Divergence | Measures differences in bid-ask spreads and liquidity conditions. |
| Liquidation Concentration | Evaluates liquidation imbalances and potential cascading liquidation risk. |

The individual risk metrics are combined into a composite risk score that provides an overall indication of ecosystem risk.

### 3. On-Chain Risk Policy Enforcement

SentinelX uses a Solana Anchor smart contract to enforce risk policies on-chain.

Key capabilities include:

- Dynamic maximum leverage limits.
- Collateral requirements based on calculated risk.
- Pyth oracle-based price validation.
- Configurable price staleness tolerance.
- On-chain enforcement of risk policy constraints.

The policy risk is calculated using the maximum risk across the monitored venues and the overall ecosystem:

\[
\text{Policy Risk} =
\max(
\text{Phoenix Risk},
\text{Velocity Risk},
\text{Ecosystem Risk}
)
\]

This ensures that elevated risk in an individual venue or across the ecosystem can influence the resulting risk policy.

**Deployment:** Solana Devnet

**Anchor Program ID:** `H1DeHTackptYWeK8EAjLGG6UXG7xFQhkMUgWsdNrm45H`

### 4. Interactive Live Dashboard

The SentinelX dashboard provides a visual interface for monitoring risk conditions and interacting with the test trading environment.

**Ecosystem Overview**
- Live venue comparisons.
- Risk score visualization.
- Divergence breakdowns.
- Risk methodology explanations.

**Position Execution**
- Test USDC faucet.
- Deposit and manage collateral.
- Increase, reduce, and close positions.
- Simulate transactions before on-chain submission.

**Contagion Monitor**
- Identifies isolated risk conditions.
- Detects active systemic contagion states.
- Provides visibility into potential cross-venue risk propagation.

---


### 5. Architecture Components

| Component | Responsibility |
|---|---|
| Frontend Dashboard | Displays market conditions, risk metrics, and position management interfaces. |
| Backend API | Provides endpoints for market data, risk calculations, and dashboard communication. |
| Venue Adapters | Retrieve and normalize market information from supported trading venues. |
| Risk Engine | Calculates financial risk metrics, divergence scores, and ecosystem risk. |
| Risk Publisher | Publishes calculated risk information for on-chain enforcement. |
| Anchor Smart Contract | Enforces leverage and collateral policies on Solana. |
| Pyth Oracle | Supplies price information used for on-chain validation. |

---

## Technology Stack

| Layer | Technologies |
|---|---|
| Frontend | React, Vite, TypeScript |
| Backend | Express, Bun, Node.js |
| Data Validation | Zod |
| Financial Analytics | TypeScript, statistical and financial risk metrics |
| Blockchain | Solana, Anchor, Rust |
| Oracle Integration | Pyth |
| Package Management | Bun / npm |
| Testing | Unit tests, frontend tests, Anchor program tests |

---

## How SentinelX Works

The system follows a continuous risk monitoring and enforcement workflow.

1. Market data is collected from supported perpetual trading venues.
2. Venue adapters normalize the incoming market information.
3. The risk engine calculates financial metrics and cross-venue divergence.
4. A composite Ecosystem Risk Score is generated.
5. The risk publisher communicates the calculated risk state for on-chain enforcement.
6. The Solana smart contract validates the relevant oracle price and risk policy conditions.
7. Leverage and collateral constraints are enforced according to the configured policy.
8. The dashboard displays the resulting risk conditions and market intelligence.

---

## Getting Started

### Prerequisites

Install the following tools before running the project:

- [Bun](https://bun.sh/) version 1.1 or later, or Node.js version 20 or later.
- [Solana CLI](https://solana.com/docs/intro/installation) — optional for Anchor and local contract interactions.
- [Anchor](https://www.anchor-lang.com/) — required for smart contract development and testing.

### Installation

Clone the repository:

```bash
git clone YOUR_REPOSITORY_URL
cd sentinelx
```

Install the project dependencies:

```bash
bun install
```

Alternatively, use npm if your project configuration supports it:

```bash
npm install
```

### Start the Application

Run the automated startup script:

```bash
npm run start
```

Alternatively:

```bash
bun run start
```

Or execute the startup shell script:

```bash
./start.sh
```

The startup process installs dependencies, builds shared packages, and starts the backend and frontend services.

| Service | Local URL |
|---|---|
| Risk API Server | http://localhost:3000 |
| Risk Dashboard | http://localhost:5173 |

### Run Services Individually

Start the backend API:

```bash
npm run api:dev
```

Start the frontend dashboard:

```bash
npm run dashboard:dev
```

---

## Testing

SentinelX includes testing commands for the backend, frontend, and smart contracts.

### Unit Tests

```bash
npm run test:unit
```

### Dashboard Tests

```bash
npm run test:dashboard
```

### Anchor Smart Contract Tests

```bash
npm run test:anchor
```

### Full Test Suite

```bash
npm run test:all
```

These tests help validate the risk calculation logic, dashboard functionality, and smart contract behavior.

---

## Repository Structure

```text
sentinelx/
│
├── anchor/
│   └── risk_vault/          # Solana Anchor smart contracts
│
├── apps/
│   ├── api/                 # Backend API service
│   ├── dashboard/           # React + Vite risk dashboard
│   └── risk-publisher/      # On-chain risk state publisher
│
├── packages/
│   ├── adapters/            # Venue adapters
│   ├── api-contracts/       # Zod schemas and shared types
│   ├── cross-venue/         # Divergence and contagion models
│   ├── metrics/             # Financial and statistical metrics
│   └── risk/                # Risk scoring and threshold logic
│
├── tests/                   # Project testing
├── docs/                    # Project documentation
├── start.sh                 # Automated startup script
├── package.json             # Root project configuration
└── README.md                # Project documentation
```

---

## Team Members

SentinelX is developed as a collaborative full-stack development course project.

| Name | Roll Number | Contribution Area |
|---|---|---|
| Ujwal Akotkar | 24BCS012 | Backend Development |
| Shreyash Gadling | 24BDS023 | Frontend Development |
| Akash Purbhi | 24BDS061 | Risk Engine and Analytics |
| Varad Solanke | 24BDS079 | Smart Contracts and Testing |

The project combines the contributions of all four members to develop an integrated risk management platform.

---

## Future Enhancements

Potential future improvements include:

- Integration with additional Solana perpetual trading venues.
- Enhanced risk forecasting using machine learning.
- Historical risk analytics and backtesting.
- Improved liquidation cascade prediction.
- More advanced risk visualization and alerting.
- Expanded automated testing and deployment workflows.

---

## License

This project is licensed under the MIT License.

See the [LICENSE](LICENSE) file for details.
