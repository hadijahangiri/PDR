# Product Requirement Document (PRD)

**Feature Name:** Automated Forex Trading Robot  
**Product Context:** Algorithmic Trading System for Forex Markets  
**Version:** 1.0  
**Date:** 2025-12-24  
**Author:** Product Team

---

## 1. Overview

### Summary
An automated trading robot that connects to MetaTrader 5 (MT5) platform to execute forex trades based on technical analysis strategies including Market Structure (MTR), Change of Character (CHOCH), and Fair Value Gap (FVG). The system integrates volume data from Rithmic for trade confirmation, implements comprehensive risk management, and provides detailed performance reporting.

### Problem Statement
Manual forex trading requires constant market monitoring, quick decision-making, and emotional discipline. Traders struggle to consistently identify support/resistance levels, execute strategies precisely, and maintain proper risk management across multiple timeframes. Missing trading opportunities during off-hours and emotional decision-making lead to inconsistent results and potential losses.

### Goal
Automate forex trading execution with proven technical analysis strategies to achieve consistent 60%+ win rate, reduce emotional trading decisions, enable 24/5 market monitoring, and provide traders with a reliable system that follows strict risk management rules while capturing high-probability trading opportunities based on market structure and volume confirmation.

---

## 2. Scope & Out of Scope

### In Scope
- MT5 platform integration via API for order execution and market data
- Configuration interface for trading parameters (currency pairs, timeframes, risk settings)
- Automated detection of support and resistance levels across multiple timeframes
- Implementation of MTR (Market Structure), CHOCH (Change of Character), and FVG (Fair Value Gap) strategies
- Rithmic volume data integration for trade confirmation
- Money management system with position sizing based on account equity
- Automated Stop Loss (SL) and Take Profit (TP) placement
- Trailing stop functionality to maximize profits
- Comprehensive reporting dashboard with trade history and performance metrics
- Real-time notifications for trade execution and system events
- Backtesting capability on historical data

### Out of Scope
- Support for other trading platforms (MT4, cTrader, TradingView) - future consideration
- Cryptocurrency or stock trading (forex only in v1.0)
- Social trading or signal sharing features
- Mobile application (desktop/server only)
- Fundamental analysis integration (news events, economic calendar)
- Multi-account management
- Custom strategy builder/editor (predefined strategies only)
- AI/Machine learning-based pattern recognition (rule-based only)

---

## 3. User Personas & Use Cases

### Personas

#### Persona 1: Professional Day Trader
An experienced forex trader with 3-5 years of trading experience who understands technical analysis but wants to automate execution to remove emotions and capture more opportunities. Trades multiple currency pairs and wants consistent application of their proven strategies.

#### Persona 2: Part-Time Trader
A professional with a full-time job who wants to participate in forex markets without constant monitoring. Needs a reliable system that can trade during their working hours and wants clear reports to review performance.

#### Persona 3: Trading Strategy Developer
A quantitative analyst who develops trading strategies and wants to test and deploy them in live markets. Requires detailed performance metrics and the ability to fine-tune parameters based on backtesting results.

### Use Cases

#### UC-001: Initial System Setup and Configuration
- **Description:** User configures the trading robot with their trading preferences, risk parameters, and account settings
- **Pre-conditions:** MT5 account is active; robot software is installed; Rithmic account credentials are available
- **Post-conditions:** System is configured and ready to start trading; all connections are validated
- **Main Flow:**
  1. User launches the trading robot application
  2. User enters MT5 account credentials and server information
  3. System validates MT5 connection and retrieves account details
  4. User enters Rithmic API credentials for volume data
  5. System validates Rithmic connection
  6. User selects currency pairs to trade (e.g., EUR/USD, GBP/USD, USD/JPY)
  7. User sets trading timeframe for analysis (e.g., H1 for structure, M15 for entry)
  8. User configures risk parameters (risk per trade %, max daily loss, max positions)
  9. User enables/disables specific strategies (MTR, CHOCH, FVG)
  10. User sets trading hours (e.g., London/New York session only)
  11. System validates all settings and saves configuration
  12. System displays ready status
- **Alternate/Error Flows:**
  - If MT5 connection fails, display specific error and suggest troubleshooting steps
  - If Rithmic credentials are invalid, allow user to continue with basic volume from MT5 (with warning)
  - If selected currency pairs are not available, show list of available pairs
  - If risk parameters exceed recommended limits, show warning but allow override

#### UC-002: Automated Trade Execution Based on Strategy Signal
- **Description:** System identifies a trading opportunity, validates it with volume confirmation, and executes a trade automatically
- **Pre-conditions:** System is running; configuration is complete; market is open; sufficient account balance
- **Post-conditions:** Trade is executed in MT5; position is tracked; SL/TP are set; user is notified
- **Main Flow:**
  1. System continuously analyzes configured currency pairs in real-time
  2. System identifies support/resistance levels on structure timeframe
  3. Price action triggers a strategy signal (e.g., FVG detected after CHOCH)
  4. System checks Rithmic volume data for confirmation (volume spike or divergence)
  5. System validates volume confirmation against threshold settings
  6. System calculates position size based on money management rules (account equity × risk%)
  7. System determines optimal entry price based on strategy rules
  8. System calculates SL placement based on market structure (below/above key level)
  9. System calculates TP placement based on risk:reward ratio (minimum 1:2)
  10. System sends order to MT5 with all parameters
  11. MT5 confirms order execution and returns order ID
  12. System records trade in database with timestamp, entry price, SL, TP
  13. System sends notification to user (app notification, email, or telegram)
  14. System begins monitoring position for trailing stop conditions
- **Alternate/Error Flows:**
  - If volume confirmation fails, reject signal and log the rejected opportunity
  - If account has reached max daily loss limit, skip trade and alert user
  - If max open positions reached, queue signal or skip based on settings
  - If order execution fails (insufficient margin, spread too wide), retry once then alert user
  - If MT5 connection lost during execution, reconnect and verify order status
  - If price moves significantly before execution (slippage), cancel order if exceeds tolerance

#### UC-003: Position Management with Trailing Stop
- **Description:** System monitors open positions and adjusts trailing stop as price moves favorably
- **Pre-conditions:** At least one position is open; trailing stop is enabled in settings
- **Post-conditions:** Stop loss is moved to protect profits; position may be closed by trailing stop
- **Main Flow:**
  1. System monitors all open positions every tick/candle
  2. For profitable position, system checks if price has moved sufficient distance to activate trailing stop (e.g., 1:1 risk:reward reached)
  3. System calculates new trailing stop level based on configured method (fixed pips, ATR, or structure-based)
  4. If new stop level is better than current stop, system modifies order in MT5
  5. MT5 confirms stop loss modification
  6. System updates position record with new SL
  7. System logs the modification with timestamp
  8. Process repeats as price continues to move favorably
  9. If price reverses and hits trailing stop, position is closed
  10. System records final trade outcome and calculates P&L
- **Alternate/Error Flows:**
  - If MT5 modification fails, retry up to 3 times with exponential backoff
  - If position was closed before modification (hit TP or manual close), skip update
  - If price gaps through stop level, accept actual fill price and log slippage

#### UC-004: Support and Resistance Level Detection
- **Description:** System automatically identifies key support and resistance levels across timeframes
- **Pre-conditions:** Historical price data is available; currency pair is configured
- **Post-conditions:** Support/resistance levels are identified and stored; levels are used for strategy decisions
- **Main Flow:**
  1. System loads historical candle data for the structure timeframe (e.g., H4, D1)
  2. System identifies swing highs and swing lows using configurable lookback period
  3. System clusters nearby levels within tolerance range (e.g., 10 pips)
  4. System ranks levels by number of touches and recency
  5. System identifies current market structure (uptrend, downtrend, or range)
  6. System marks key levels on internal chart representation
  7. System monitors price interaction with identified levels
  8. When price approaches a level (within threshold), system increases monitoring frequency
  9. System detects breakouts, false breakouts, or bounces at levels
  10. System updates levels periodically as market structure evolves
- **Alternate/Error Flows:**
  - If insufficient historical data, system requests additional data from MT5
  - If no clear levels found, system widens search criteria or uses fixed pivot points
  - If too many levels identified, system applies stricter filtering

#### UC-005: Daily Performance Report Generation
- **Description:** System generates comprehensive daily trading report with key metrics
- **Pre-conditions:** Trading day has ended or user requests report; trade history exists
- **Post-conditions:** Report is generated and made available; user is notified
- **Main Flow:**
  1. User requests daily report or system generates automatically at end of trading day
  2. System retrieves all trades executed in the period
  3. System calculates key metrics:
     - Total trades, winning trades, losing trades, win rate
     - Total profit/loss in currency and percentage
     - Best trade, worst trade, average trade
     - Risk:reward ratio achieved
     - Maximum drawdown during period
     - Profit factor (gross profit / gross loss)
  4. System generates strategy-specific breakdown (MTR vs CHOCH vs FVG performance)
  5. System generates currency pair performance comparison
  6. System creates equity curve chart showing account growth
  7. System identifies top performing and worst performing hours/sessions
  8. System compiles report in PDF format with charts and tables
  9. System saves report to reports directory
  10. System sends report via email if configured
  11. System displays summary notification
- **Alternate/Error Flows:**
  - If no trades executed, generate summary report showing market monitoring activity
  - If report generation fails, log error and retry once
  - If email sending fails, save report locally and alert user

#### UC-006: Risk Management and Position Sizing
- **Description:** System calculates appropriate position size for each trade based on risk management rules
- **Pre-conditions:** Trade signal is generated; account information is available
- **Post-conditions:** Position size is calculated; trade is executed or rejected based on risk limits
- **Main Flow:**
  1. Trade signal is generated with entry price and stop loss level
  2. System retrieves current account equity from MT5
  3. System calculates risk amount (account equity × risk percentage per trade, e.g., 2%)
  4. System calculates distance from entry to stop loss in pips
  5. System calculates position size (lot size) = Risk Amount / (Stop Loss Distance × Pip Value)
  6. System rounds position size to nearest valid lot size (e.g., 0.01 lot increments)
  7. System checks if position size is within broker limits (min/max lot size)
  8. System checks total exposure (current positions + new position) against max exposure limit
  9. System verifies required margin for new position
  10. System checks daily loss limit has not been reached
  11. If all checks pass, system approves trade for execution
  12. If any check fails, system rejects trade and logs reason
- **Alternate/Error Flows:**
  - If calculated position size is below minimum, reject trade (stop loss too wide)
  - If calculated position size exceeds maximum, reduce to maximum allowed
  - If insufficient margin, reject trade and alert user about funding needs
  - If daily loss limit reached, pause trading and alert user

#### UC-007: Strategy Signal - Change of Character (CHOCH)
- **Description:** System detects Change of Character pattern indicating potential trend reversal
- **Pre-conditions:** Market data is streaming; price structure analysis is active
- **Post-conditions:** CHOCH signal is generated or rejected; if valid, trade setup is created
- **Main Flow:**
  1. System monitors price action for higher highs and higher lows (uptrend) or lower lows and lower highs (downtrend)
  2. System identifies most recent structural high/low in current trend
  3. System detects when price breaks previous structural point in opposite direction
  4. In uptrend: price breaks below most recent higher low = CHOCH signal
  5. In downtrend: price breaks above most recent lower high = CHOCH signal
  6. System verifies break is decisive (close beyond level, not just wick)
  7. System checks Rithmic volume data for confirmation (increased volume on break)
  8. System identifies potential Fair Value Gap (FVG) in break move
  9. If FVG exists, system sets alert for price to retrace into FVG for entry
  10. System calculates entry level (within FVG), stop loss (beyond invalidation point), and take profit (next major level)
  11. System creates trade setup and monitors for entry conditions
- **Alternate/Error Flows:**
  - If volume doesn't confirm, downgrade signal strength or reject
  - If no clear FVG for entry, use alternative entry method (limit order at structural level)
  - If price doesn't retrace to entry zone within X candles, cancel signal

#### UC-008: System Monitoring and Health Check
- **Description:** System continuously monitors its own health and connectivity status
- **Pre-conditions:** System is running
- **Post-conditions:** System status is updated; user is alerted to any issues
- **Main Flow:**
  1. System performs health check every 60 seconds
  2. System verifies MT5 connection is active (ping server)
  3. System verifies Rithmic connection is active
  4. System checks if data feed is current (no stale data)
  5. System monitors system resources (CPU, memory, disk space)
  6. System verifies all configured currency pairs are receiving updates
  7. System checks if any errors are logged since last check
  8. System updates status indicator (green = healthy, yellow = degraded, red = error)
  9. System records heartbeat in log file
  10. If all checks pass, continue normal operation
- **Alternate/Error Flows:**
  - If MT5 connection lost, attempt reconnection up to 5 times with exponential backoff
  - If reconnection fails, alert user and enter safe mode (monitor only, no new trades)
  - If Rithmic connection lost, continue with MT5 volume but alert user about degraded mode
  - If system resources critically low, pause new trade signals and alert user
  - If data feed is stale, attempt to restart feed; if failed, stop trading

---

## 4. Functional Requirements

- **FR-1:** System shall establish and maintain connection to MT5 platform via MetaTrader 5 API
- **FR-2:** System shall authenticate with MT5 server using user-provided credentials
- **FR-3:** System shall retrieve real-time price quotes for all configured currency pairs
- **FR-4:** System shall retrieve account information (balance, equity, margin, open positions) from MT5
- **FR-5:** System shall execute market orders, limit orders, and stop orders via MT5 API
- **FR-6:** System shall modify existing orders (change SL/TP) via MT5 API
- **FR-7:** System shall close positions manually or when SL/TP is hit
- **FR-8:** System shall provide configuration interface for setting currency pairs, timeframes, risk parameters, and strategy settings
- **FR-9:** System shall persist configuration settings in configuration file or database
- **FR-10:** System shall validate all configuration inputs before saving
- **FR-11:** System shall identify support levels by analyzing swing lows across specified timeframe
- **FR-12:** System shall identify resistance levels by analyzing swing highs across specified timeframe
- **FR-13:** System shall cluster nearby support/resistance levels within configurable tolerance
- **FR-14:** System shall track number of times price touches each support/resistance level
- **FR-15:** System shall detect when price breaks above resistance or below support levels
- **FR-16:** System shall implement Market Structure (MTR) strategy detecting trend direction and structural points
- **FR-17:** System shall implement Change of Character (CHOCH) strategy detecting trend reversals
- **FR-18:** System shall implement Fair Value Gap (FVG) strategy detecting liquidity gaps
- **FR-19:** System shall combine multiple strategies for higher-probability trade setups
- **FR-20:** System shall connect to Rithmic data feed for volume information
- **FR-21:** System shall retrieve real-time volume data for configured currency pairs from Rithmic
- **FR-22:** System shall compare current volume to average volume for confirmation
- **FR-23:** System shall require volume confirmation before executing trades (configurable threshold)
- **FR-24:** System shall implement fixed fractional position sizing based on account equity percentage
- **FR-25:** System shall calculate position size based on stop loss distance and risk amount
- **FR-26:** System shall enforce maximum position size limit per trade
- **FR-27:** System shall enforce maximum number of concurrent open positions
- **FR-28:** System shall enforce maximum daily loss limit (stop trading when reached)
- **FR-29:** System shall enforce maximum account drawdown limit
- **FR-30:** System shall calculate optimal stop loss placement based on market structure
- **FR-31:** System shall calculate take profit based on minimum risk:reward ratio (configurable, default 1:2)
- **FR-32:** System shall place stop loss and take profit orders immediately upon trade entry
- **FR-33:** System shall implement trailing stop functionality with configurable activation point
- **FR-34:** System shall support multiple trailing stop methods (fixed pips, ATR-based, structure-based)
- **FR-35:** System shall modify stop loss in real-time as price moves favorably
- **FR-36:** System shall never move stop loss in unfavorable direction
- **FR-37:** System shall generate daily trading reports with key performance metrics
- **FR-38:** System shall generate weekly and monthly summary reports
- **FR-39:** System shall display real-time dashboard with current positions, account status, and recent signals
- **FR-40:** System shall maintain trade history database with all trade details
- **FR-41:** System shall export trade history to CSV format
- **FR-42:** System shall calculate and display win rate, profit factor, average win/loss
- **FR-43:** System shall generate equity curve chart showing account growth over time
- **FR-44:** System shall send real-time notifications for trade execution (entry, SL, TP)
- **FR-45:** System shall send alerts for system errors and connection issues
- **FR-46:** System shall support notification channels (email, Telegram, push notification)
- **FR-47:** System shall log all significant events (trades, errors, signals) to log file
- **FR-48:** System shall implement log rotation to prevent disk space issues
- **FR-49:** System shall support backtesting mode using historical data
- **FR-50:** System shall generate backtest reports with same metrics as live trading

---

## 5. Non-Functional Requirements

### Performance
- System must process price updates and strategy analysis within 100ms per currency pair
- System must execute orders via MT5 within 500ms of signal generation
- System must support monitoring of at least 10 currency pairs simultaneously without degradation
- System must retrieve and process volume data from Rithmic with less than 200ms latency
- Database queries for trade history must complete within 1 second
- Report generation must complete within 10 seconds for daily reports
- System must handle market opening surge (Sunday evening) without missing signals
- Trailing stop adjustments must be executed within 1 second of price movement

### Security
- MT5 credentials must be encrypted at rest using AES-256 encryption
- Rithmic API keys must be stored securely in encrypted configuration
- Configuration file must have restricted file permissions (read/write for owner only)
- All API communications must use secure protocols (HTTPS/TLS)
- System must implement rate limiting to prevent API abuse
- System must validate all inputs to prevent injection attacks
- Session tokens must expire after configurable timeout period
- System must log all access attempts and authentication events
- Database credentials must not be hardcoded in application code
- Sensitive information must not be logged in plain text

### Reliability & Monitoring
- System must automatically reconnect to MT5 if connection is lost (up to 5 retries)
- System must automatically reconnect to Rithmic if connection is lost
- System must gracefully handle broker server downtime or maintenance
- System must detect and alert on stale price data (no update for 60 seconds)
- System must implement watchdog process to restart application if it crashes
- System must maintain operation during network interruptions (queue orders locally)
- System must verify order execution and retry on failure
- System must reconcile local position tracking with MT5 actual positions every 5 minutes
- System must log all errors with timestamp, severity, and context
- System must monitor system resources and alert if CPU >80% or memory >90%
- System must implement heartbeat mechanism to prove system is alive
- System must backup trade history database daily
- System must achieve 99% uptime during market hours

### UX & Accessibility
- Configuration interface must be intuitive with clear labels and help text
- System must provide real-time visual feedback on system status (connection, trading state)
- Dashboard must update in real-time showing current positions and P&L
- Error messages must be clear and actionable
- System must provide user manual and quick start guide
- Charts and reports must be easily readable with proper legends and labels
- Color scheme must be configurable (light/dark mode)
- All notifications must be concise and contain relevant information
- System must support multiple languages (English, Persian/Farsi initially)

---

## 6. Integration & API Hints

### MT5 Integration

#### Connection & Authentication
- **Endpoint:** `MT5.Initialize(server, login, password)`
- **Input:** `{server: string, login: int, password: string}`
- **Output:** `{success: boolean, error: string}`
- **Purpose:** Establish connection to MT5 trading platform

#### Market Data
- **Endpoint:** `MT5.CopyRates(symbol, timeframe, start_pos, count)`
- **Input:** `{symbol: "EURUSD", timeframe: TIMEFRAME_H1, start_pos: 0, count: 1000}`
- **Output:** `{bars: Array<{time, open, high, low, close, volume}>}`
- **Purpose:** Retrieve historical price data for analysis

#### Order Execution
- **Endpoint:** `MT5.OrderSend(request)`
- **Input:** `{action: TRADE_ACTION_DEAL, symbol, volume, type: ORDER_TYPE_BUY, price, sl, tp, comment}`
- **Output:** `{retcode, deal, order, volume, price, comment}`
- **Purpose:** Execute trading orders

#### Position Management
- **Endpoint:** `MT5.OrderModify(ticket, price, sl, tp)`
- **Input:** `{ticket: order_id, price: 0, sl: new_stop_loss, tp: take_profit}`
- **Output:** `{retcode, comment}`
- **Purpose:** Modify existing order stop loss and take profit levels

### Rithmic Integration

#### Authentication
- **Endpoint:** `Rithmic.Connect(credentials)`
- **Input:** `{username, password, app_name, app_version}`
- **Output:** `{session_token, error}`
- **Purpose:** Authenticate and establish connection to Rithmic data feed

#### Volume Data
- **Endpoint:** `Rithmic.SubscribeVolume(symbol)`
- **Input:** `{symbol: "6E" (EUR futures), subscribe: true}`
- **Output:** `{stream: VolumeStream}`
- **Purpose:** Subscribe to real-time volume data for forex instruments

#### Volume Confirmation
- **Endpoint:** `Rithmic.GetVolumeStats(symbol, period)`
- **Input:** `{symbol, period: "1h", stat_type: "average"}`
- **Output:** `{current_volume, average_volume, std_dev, percentile}`
- **Purpose:** Get volume statistics for confirmation logic

### Internal Database Schema

#### Trades Table
```
- trade_id (PK)
- open_time
- close_time
- symbol
- direction (BUY/SELL)
- entry_price
- exit_price
- volume (lot size)
- stop_loss
- take_profit
- profit_loss
- profit_loss_pips
- strategy_used (MTR/CHOCH/FVG)
- volume_confirmed (boolean)
- commission
- swap
- comment
```

#### Support_Resistance Table
```
- level_id (PK)
- symbol
- level_price
- level_type (SUPPORT/RESISTANCE)
- strength (1-10)
- touches_count
- first_detected
- last_confirmed
- timeframe
```

### Dependencies
- **MetaTrader 5 Platform:** Must be installed and accessible; MT5 Python API library required
- **Rithmic API:** Account credentials and API access required for volume data
- **PostgreSQL or SQLite:** Database for storing trade history and configuration
- **Python Libraries:** pandas (data analysis), numpy (calculations), matplotlib (charting)
- **Notification Services:** SMTP server for email, Telegram Bot API (optional)

---

## 7. Analytics & Success Metrics

### Key Metrics
- **Win Rate:** Percentage of profitable trades (target: 60%+)
- **Profit Factor:** Gross profit divided by gross loss (target: 2.0+)
- **Risk:Reward Ratio:** Average reward per trade divided by average risk (target: 1:2+)
- **Maximum Drawdown:** Largest peak-to-trough decline (target: <15%)
- **Average Trade Duration:** Time from entry to exit (monitoring metric)
- **Signals Generated:** Number of strategy signals per day per pair
- **Signals Executed:** Percentage of signals that pass volume confirmation (target: 40-60%)
- **Strategy Performance:** Win rate and profit by strategy type (MTR vs CHOCH vs FVG)
- **Currency Pair Performance:** Profit by currency pair to identify best performers
- **Slippage:** Average difference between expected and actual execution price
- **System Uptime:** Percentage of market hours system was operational (target: 99%+)

### KPIs
- **Primary KPI:** Monthly Return on Account - Achieve 5-10% monthly return on starting capital
- **Secondary KPI:** Win Rate - Maintain 60% or higher win rate over rolling 100 trades
- **Risk KPI:** Maximum Drawdown - Never exceed 20% drawdown from peak equity
- **Consistency KPI:** Profitable Months - 8 out of 12 months should be profitable
- **Efficiency KPI:** Profit per Trade - Average profit per winning trade should be 2x average loss per losing trade
- **Reliability KPI:** System Uptime - Maintain 99%+ uptime during market hours (Mon-Fri trading sessions)
- **Execution KPI:** Order Execution Success Rate - 99%+ of generated signals successfully executed
- **Volume Confirmation Accuracy:** Trades with volume confirmation should have 10%+ higher win rate than those without

### Monitoring Dashboards
- Real-time P&L tracker showing today's performance
- Equity curve showing account growth over time
- Open positions monitor with current P&L and distance to SL/TP
- Strategy performance comparison (side-by-side metrics)
- Currency pair performance heatmap
- System health indicator (connections, latency, error rate)

---

## 8. Risks & Open Questions

### Main Risks

- **Risk 1: Broker Compatibility and Reliability**  
  MT5 brokers vary in API implementation, execution speed, and reliability. Poor execution or connection issues could result in significant losses.  
  **Mitigation:** Test extensively with specific broker in demo account; implement robust error handling and reconnection logic; choose reputable broker with good API stability; implement slippage monitoring and rejection of orders with excessive slippage.

- **Risk 2: Rithmic Data Cost and Availability**  
  Rithmic data feed may have subscription costs, and volume data for forex spot might not be directly available (forex futures may be used as proxy).  
  **Mitigation:** Research Rithmic pricing and data availability before development; implement fallback to MT5 volume data if Rithmic unavailable; make volume confirmation optional (degraded mode); consider alternative volume data sources (CME, ICE).

- **Risk 3: Market Regime Changes**  
  Strategies optimized for trending markets may perform poorly in ranging markets, leading to consecutive losses and drawdown.  
  **Mitigation:** Implement market regime detection to pause trading during unfavorable conditions; include range-detection logic to filter signals; set maximum daily loss limits; allow manual pause/resume of trading; implement adaptive position sizing during uncertain conditions.

- **Risk 4: Over-Optimization and Curve Fitting**  
  Extensive backtesting and parameter optimization may lead to strategies that work on historical data but fail in live trading.  
  **Mitigation:** Use walk-forward analysis during backtesting; test strategies on out-of-sample data; avoid excessive parameter optimization; start with conservative position sizing in live trading; implement paper trading mode before going live; monitor strategy performance and halt if significantly deviates from backtest.

- **Risk 5: Technical Failures During Critical Moments**  
  System crashes, internet outages, or server downtime during important market moves or when positions are open could result in unmanaged risk.  
  **Mitigation:** Implement all stop losses and take profits at the broker level (not just locally); use VPS hosting with high uptime SLA; implement redundant internet connections; create manual intervention procedures; set up mobile alerts for system failures; ensure broker has good customer support for emergency position closure.

- **Risk 6: Regulatory and Compliance Issues**  
  Automated trading may be subject to regulations depending on jurisdiction; leverage restrictions vary by region.  
  **Mitigation:** Clearly document that system is for personal use; add disclaimer about trading risks; ensure compliance with local regulations; consult with legal advisor if deploying commercially; implement adjustable leverage settings to comply with regional restrictions.

- **Risk 7: Insufficient Testing and Edge Cases**  
  Real market conditions may present scenarios not covered in development and testing, leading to unexpected behavior.  
  **Mitigation:** Comprehensive testing plan including unit tests, integration tests, and scenario tests; extended demo account testing (minimum 3 months); start with small position sizes in live account; implement extensive logging to diagnose issues; create circuit breakers that halt trading on unexpected conditions.

### Open Questions

- [ ] Which specific MT5 broker will be used? (affects API implementation and testing)
- [ ] What is the exact Rithmic subscription plan and cost structure?
- [ ] Is Rithmic volume data available for forex spot pairs, or will we use futures as proxy?
- [ ] What is the minimum and target account size for initial deployment?
- [ ] Should the system support multiple MT5 accounts simultaneously?
- [ ] What is the maximum acceptable latency for volume data confirmation?
- [ ] Should backtesting use tick data or candle data? (tick data is more accurate but more expensive)
- [ ] What are the specific trading hours? (24/5, or specific sessions only like London/NY overlap)
- [ ] How should the system handle high-impact news events? (pause trading, widen stops, or continue normally)
- [ ] What is the plan for strategy parameter updates? (manual configuration file, or admin interface)
- [ ] Should the system support paper trading mode for testing new strategies?
- [ ] What hosting solution will be used? (local PC, VPS, cloud server)
- [ ] Who will monitor the system and how often? (24/5 monitoring vs periodic checks)
- [ ] What is the escalation procedure if system encounters critical errors?
- [ ] Are there any specific regulatory requirements based on target user location?
- [ ] Should the system include any social/community features (sharing performance, signals)?

---

## 9. Acceptance Criteria

### Core Functionality
- [ ] System successfully connects to MT5 platform and authenticates
- [ ] System can retrieve real-time quotes for all configured currency pairs
- [ ] System can execute market buy and sell orders via MT5
- [ ] System can retrieve current account balance, equity, and margin information
- [ ] Configuration interface allows setting all required parameters (pairs, timeframes, risk settings)
- [ ] Configuration is persisted and loaded correctly on system restart

### Support/Resistance Detection
- [ ] System identifies at least 3 support levels and 3 resistance levels for each currency pair
- [ ] Identified levels are validated to correspond with actual swing points in historical data
- [ ] System correctly detects when price breaks above resistance or below support
- [ ] System updates levels periodically as market structure evolves

### Strategy Implementation
- [ ] MTR strategy correctly identifies uptrends (higher highs, higher lows) and downtrends (lower lows, lower highs)
- [ ] CHOCH strategy correctly detects Change of Character when price breaks key structural level
- [ ] FVG strategy correctly identifies Fair Value Gaps (liquidity voids) on price charts
- [ ] Strategies generate at least 2-5 signals per day per currency pair in backtesting
- [ ] Combined strategy signals show higher win rate than individual strategies in backtesting

### Volume Integration
- [ ] System successfully connects to Rithmic data feed
- [ ] System retrieves real-time volume data for configured instruments
- [ ] Volume confirmation logic correctly compares current volume to average volume
- [ ] Trades with volume confirmation show measurably higher win rate in backtesting (>10% improvement)
- [ ] System continues operating with MT5 volume if Rithmic connection fails (degraded mode alert)

### Money Management
- [ ] Position size is correctly calculated based on account equity and risk percentage
- [ ] Position size respects minimum and maximum lot size limits
- [ ] System prevents new trades when maximum daily loss limit is reached
- [ ] System prevents new trades when maximum open positions limit is reached
- [ ] System correctly calculates required margin before executing trade

### Stop Loss and Take Profit
- [ ] Stop loss is automatically placed on every trade at calculated level
- [ ] Take profit is automatically placed on every trade at calculated level
- [ ] Risk:reward ratio is correctly calculated and meets minimum requirement (e.g., 1:2)
- [ ] SL/TP orders are confirmed executed by MT5 broker

### Trailing Stop
- [ ] Trailing stop activates when position reaches specified profit level (e.g., 1:1 R:R)
- [ ] Stop loss is moved in favorable direction as price moves
- [ ] Stop loss is never moved in unfavorable direction
- [ ] Trailing stop correctly uses selected method (fixed pips, ATR, or structure-based)
- [ ] Modified stop loss orders are confirmed by MT5 broker

### Reporting and Monitoring
- [ ] Daily report includes all required metrics (win rate, profit factor, total P&L, etc.)
- [ ] Report is generated automatically at end of trading day
- [ ] Report can be manually generated on demand
- [ ] Trade history is correctly stored in database with all details
- [ ] Equity curve chart accurately reflects account growth over time
- [ ] Dashboard shows real-time updates of open positions and P&L

### Notifications and Alerts
- [ ] User receives notification when trade is entered
- [ ] User receives notification when trade is closed (hit SL or TP)
- [ ] User receives alert when system encounters errors or connection issues
- [ ] User receives alert when daily loss limit is approaching or reached
- [ ] Notifications are delivered within 30 seconds of event

### Reliability and Error Handling
- [ ] System automatically reconnects to MT5 after connection loss
- [ ] System automatically reconnects to Rithmic after connection loss
- [ ] System gracefully handles broker server downtime without crashing
- [ ] All errors are logged with timestamp and context information
- [ ] System recovers correctly after restart (reloads configuration, resumes monitoring)

### Security
- [ ] MT5 credentials are encrypted in configuration file
- [ ] Rithmic credentials are encrypted in configuration file
- [ ] Configuration file has restricted permissions (owner read/write only)
- [ ] All API communications use secure protocols

### Testing and Validation
- [ ] All unit tests pass (minimum 80% code coverage)
- [ ] Integration tests pass for MT5 connection and order execution
- [ ] Backtesting produces consistent results across multiple runs
- [ ] Demo account testing runs successfully for minimum 1 month without critical errors
- [ ] Paper trading mode allows testing without real money risk
- [ ] System passes all security scan and vulnerability tests
- [ ] Performance testing confirms system can handle 10 currency pairs simultaneously

---

**Status:** Draft  
**Reviewers:** Trading Strategy Expert, Software Architect, Risk Manager, DevOps Engineer

---

## Additional Notes

### Recommended Development Phases

**Phase 1 (Weeks 1-4):** Core Infrastructure
- MT5 connection and API integration
- Configuration management
- Basic order execution
- Database setup and trade logging

**Phase 2 (Weeks 5-8):** Technical Analysis
- Support/Resistance detection
- Market structure analysis
- Strategy implementation (MTR, CHOCH, FVG)

**Phase 3 (Weeks 9-12):** Risk Management
- Position sizing logic
- SL/TP calculation
- Trailing stop implementation
- Risk limits enforcement

**Phase 4 (Weeks 13-16):** Volume Integration & Optimization
- Rithmic integration
- Volume confirmation logic
- Backtesting framework
- Strategy optimization

**Phase 5 (Weeks 17-20):** Reporting & Monitoring
- Dashboard development
- Report generation
- Notification system
- Performance analytics

**Phase 6 (Weeks 21-24):** Testing & Deployment
- Comprehensive testing (unit, integration, end-to-end)
- Demo account testing
- Bug fixes and refinements
- Documentation and user training
- Production deployment to VPS

### Technology Stack Recommendation

- **Programming Language:** Python 3.9+ (excellent MT5 API support, rich ecosystem for trading)
- **MT5 Integration:** MetaTrader5 Python package
- **Data Processing:** pandas, numpy
- **Charting:** matplotlib, plotly
- **Database:** SQLite (simple deployment) or PostgreSQL (scalable)
- **Web Dashboard:** Flask or FastAPI + React (optional, for web-based monitoring)
- **Notifications:** smtplib (email), python-telegram-bot (Telegram)
- **Testing:** pytest, unittest
- **Logging:** Python logging module with rotation
- **Deployment:** Docker container on VPS with systemd for auto-restart

### Glossary

- **MT5:** MetaTrader 5 - Popular trading platform for forex, stocks, and futures
- **Rithmic:** Professional market data provider offering real-time volume and order flow data
- **MTR:** Market Structure - The pattern of highs and lows indicating trend direction
- **CHOCH:** Change of Character - A break in market structure suggesting potential trend reversal
- **FVG:** Fair Value Gap - A price gap indicating unfilled orders and potential retracement zone
- **Support:** Price level where buying pressure is expected to overcome selling pressure
- **Resistance:** Price level where selling pressure is expected to overcome buying pressure
- **SL:** Stop Loss - Order to close position at predetermined loss level
- **TP:** Take Profit - Order to close position at predetermined profit level
- **Trailing Stop:** Dynamic stop loss that moves in favorable direction as price moves
- **Lot:** Standard trading size in forex (1 standard lot = 100,000 units of base currency)
- **Pip:** Point in Percentage - Smallest price move (0.0001 for most pairs, 0.01 for JPY pairs)
- **Risk:Reward Ratio:** Ratio of potential profit to potential loss on a trade
- **Drawdown:** Peak-to-trough decline in account value
- **Profit Factor:** Gross profit divided by gross loss (>1.0 means profitable system)
