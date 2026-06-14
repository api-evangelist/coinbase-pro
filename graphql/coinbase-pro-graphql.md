# Coinbase Advanced Trade GraphQL Schema

## Overview

This conceptual GraphQL schema models the Coinbase Advanced Trade API (formerly Coinbase Pro). The schema covers the full surface of the Advanced Trade REST API as documented at https://docs.cdp.coinbase.com/advanced-trade/docs/ and reflected in the official Python SDK at https://github.com/coinbase/coinbase-advanced-py.

Coinbase Advanced Trade is a professional-grade cryptocurrency trading platform offering spot trading, order management, portfolio tracking, payment methods, and market data.

## Schema Source

- **API Docs**: https://docs.cdp.coinbase.com/advanced-trade/docs/
- **Python SDK**: https://github.com/coinbase/coinbase-advanced-py
- **Schema File**: coinbase-pro-schema.graphql

## Domain Coverage

### Accounts and Portfolios
- `Account` — a user's trading account with balance and currency info
- `AccountCurrency` — currency details attached to an account
- `AccountBalance` — available, hold, and total amounts for an account
- `Portfolio` — a named grouping of positions and balances
- `PortfolioBalance` — aggregate value of a portfolio in a target currency
- `PortfolioPositions` — collection of open positions within a portfolio
- `Position` — a single open position in a product

### Orders
- `Order` — the core order object covering all order types
- `MarketOrder` — configuration for market orders (quote or base size)
- `LimitOrder` — configuration for limit orders with price and size
- `StopOrder` — stop order triggering at a specified price
- `StopLimitOrder` — stop-limit combination order
- `OrderStatus` — enumeration of order lifecycle states
- `OrderSide` — BUY or SELL
- `OrderType` — MARKET, LIMIT, STOP, or STOP_LIMIT
- `TimeInForce` — GTC, GTD, IOC, FOK
- `OrderFill` — a single execution fill against an order

### Trades and Fills
- `FillRecord` — detailed record of a trade fill including fee and liquidity
- `Trade` — a completed trade on the exchange

### Market Data
- `ProductData` — metadata about a tradeable product
- `TradingPair` — base and quote currency pairing details
- `MarketData` — real-time snapshot of a product's market state
- `BookOrder` — a single price level in the order book
- `OrderBook` — full or aggregated order book for a product
- `Ticker` — latest price, volume, and bid/ask for a product
- `Candle` — OHLCV candlestick data point
- `Stats24h` — 24-hour rolling statistics for a product
- `DailyStats` — open, high, low, volume, last for the current day
- `TradingVolume` — volume metrics across multiple products
- `ProductStats` — aggregated statistics for a product

### Currencies and Rates
- `CurrencyInfo` — details about a supported currency
- `CurrencyType` — CRYPTO or FIAT
- `FiatCurrencies` — list of supported fiat currencies
- `ExchangeRate` — conversion rate between two currencies
- `ConversionQuote` — a quoted price for a fiat-to-fiat conversion
- `Conversion` — a completed currency conversion record
- `Convert` — request/response wrapper for conversion operations

### Transactions and History
- `Transaction` — a general ledger entry (deposit, withdrawal, trade, fee)

### Payments and Banking
- `FiatPayment` — a fiat payment transaction record
- `PaymentMethod` — a stored payment method (bank, card, etc.)
- `BankAccount` — bank account linked for ACH or wire transfers
- `BankDetails` — routing and account number details
- `WireTransfer` — an outgoing or incoming wire transfer
- `ACHTransfer` — an ACH bank transfer

### Crypto Addresses and Transfers
- `CryptoAddress` — a deposit address for a crypto currency
- `CryptoAddressInfo` — metadata and network info for a crypto address
- `DepositInfo` — details of a crypto or fiat deposit
- `WithdrawalInfo` — details of a crypto or fiat withdrawal
- `FeeEstimate` — estimated network fee for a withdrawal

### API Credentials
- `APIKey` — an API key name and permission set
- `APISecret` — secret associated with an API key (write-only in practice)
- `Token` — a short-lived authentication token

### Webhooks and Notifications
- `Webhook` — a registered webhook endpoint
- `WebhookEvent` — an event type delivered to a webhook
- `Notification` — a user notification triggered by account activity

## Query Design

The schema exposes a `Query` type for read operations and a `Mutation` type for writes. Subscriptions are modeled for real-time market data feeds that mirror the Advanced Trade WebSocket channels.

## Notes

- This is a **conceptual schema** — Coinbase Advanced Trade does not expose a public GraphQL endpoint. The schema is derived from the REST API structure and SDK models.
- Scalar types `Decimal`, `DateTime`, and `JSON` supplement the built-in GraphQL scalars.
- Pagination follows a cursor-based pattern consistent with the REST API's `cursor` field.
