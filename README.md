# Crypto Trading Bot - Simple Setup Guide

A simple system that connects TradingView alerts to Coinbase for automated crypto trading. Perfect for traders who want to automate their strategies without watching charts all day.

![Trading System Dashboard](https://i.imgur.com/placeholder-image.jpg)

## What This System Does

- Takes buy/sell signals from TradingView and executes trades on Coinbase
- Uses ADX filter to avoid choppy markets
- Confirms trades with volume analysis
- Manages risk with automatic stop-loss and take-profit
- Works with multiple cryptocurrencies (BTC, ETH, SOL, DOGE, AIOC)
- Displays real-time price charts and trading activity

## Values You'll Need to Change

Before setting up, here are the specific values you'll need to personalize:

1. **Trading Pairs**: The system comes with these default pairs:
   - BTC-USD (Bitcoin)
   - ETH-USD (Ethereum)
   - SOL-USD (Solana)
   - DOGE-USD (Dogecoin)
   - AIOC-USD (AI Open Compute)

2. **Order Sizes**: Set amounts that match your investment comfort level:
   - BTC-USD: 0.01 BTC (approximately $650)
   - ETH-USD: 0.1 ETH (approximately $320)
   - SOL-USD: 1.0 SOL (approximately $145)
   - DOGE-USD: 100 DOGE (approximately $16)
   - AIOC-USD: 50 AIOC (approximately $640)

3. **Risk Management**:
   - Stop-Loss: 2.0% - 4.0% (lower = less risk, higher = more potential profit)
   - Take-Profit: 3.0% - 6.0% (when to lock in profits)
   - ADX Threshold: 20 (filter for trending markets)

4. **Test Mode**: Always start with `"testMode": true` in your alerts

## Setup Guide (No Programming Required)

### Step 1: Create Required Accounts

1. **Coinbase Advanced Account**
   - Sign up at [advanced.coinbase.com](https://advanced.coinbase.com)
   - Verify your identity and add payment method

2. **TradingView Account**
   - Sign up at [tradingview.com](https://tradingview.com)
   - Free account works, but paid accounts allow more alerts

3. **Replit Account (for hosting)**
   - Sign up at [replit.com](https://replit.com)
   - This is where your trading bot will run 24/7

### Step 2: Set Up Your Coinbase API

1. Log in to Coinbase Advanced
2. Go to your profile and find "API Management"
3. Create a new API key with these permissions:
   - View
   - Trade
4. Save your API Key and API Secret in a safe place
5. Make sure to set up proper security (IP restrictions if possible)

### Step 3: Deploy on Replit

1. Go to [replit.com](https://replit.com) and log in
2. Click the "+ Create" button
3. Select "Import from GitHub"
4. Paste this repository URL: `YOUR_GITHUB_URL_HERE` (replace with your actual GitHub repository URL)
5. Choose "Node.js" as the language
6. Click "Import"

*After Importing:*
1. You'll need to modify a few settings in the `.replit` file:
   - Click on the `.replit` file in the Files panel
   - Make sure it contains this line: `run = "npm run dev"`
2. Install necessary packages:
   - Click on the Shell tab at the bottom
   - Type `npm install` and press Enter
   - Wait for all packages to install

### Step 4: Configure Your Bot

1. Once your project loads, click on the lock icon (Secrets) in the left sidebar
2. Add these secrets:
   - Key: `COINBASE_API_KEY`, Value: your Coinbase API key
   - Key: `COINBASE_API_SECRET`, Value: your Coinbase API secret
3. Click the "Run" button at the top to start your bot
4. Your bot will now be live at a URL like: `your-project-name.your-username.repl.co`

### Step 5: Connect TradingView

1. Log in to TradingView
2. Open a chart with your preferred cryptocurrency (BTC, ETH, etc.)
3. Add the TradingView strategy from this file: `tradingview_strategy.pine`
   - Click "Pine Editor" at the bottom of the screen
   - Paste the strategy code
   - Click "Save" and then "Add to Chart"
4. Set up an Alert:
   - Right-click on the chart and select "Create Alert"
   - Choose the condition that matches our strategy
   - Under "Alert actions" check "Webhook URL"
   - Enter your webhook URL: `https://your-project-name.your-username.repl.co/api/webhook`
   - In the message box, add this (change the values in CAPS to match your settings):

   ```json
   {
     "action": "buy",
     "symbol": "TRADING_PAIR_HERE",
     "amount": ORDER_SIZE_HERE,
     "params": {
       "adx": ADX_VALUE_HERE,
       "volume": VOLUME_RATIO_HERE
     },
     "testMode": true
   }
   ```

5. Create similar alerts for sell signals with:

   ```json
   {
     "action": "sell",
     "symbol": "TRADING_PAIR_HERE",
     "amount": ORDER_SIZE_HERE,
     "testMode": true
   }
   ```

6. Examples for different trading pairs:

   **Bitcoin Buy Alert:**
   ```json
   {
     "action": "buy",
     "symbol": "BTC-USD",
     "amount": 0.01,
     "params": {
       "adx": 25,
       "volume": 1.5
     },
     "testMode": true
   }
   ```

   **Ethereum Sell Alert:**
   ```json
   {
     "action": "sell",
     "symbol": "ETH-USD",
     "amount": 0.1,
     "testMode": true
   }
   ```

### Step 6: Keep Your Bot Running 24/7

Free Replit projects shut down after 30 minutes of inactivity. To keep yours running:

1. Go to [UptimeRobot.com](https://uptimerobot.com) and create a free account
2. Add a new monitor:
   - Select "HTTP(s)"
   - Enter your bot's URL: `https://your-project-name.your-username.repl.co`
   - Set check interval to 5 minutes
   - Save
3. UptimeRobot will now ping your bot every 5 minutes to keep it awake

### Step 7: Start with Test Mode

1. Always start with `"testMode": true` in your TradingView alerts
2. Monitor your bot's activity page for a few days
3. When you're confident everything works, you can switch to real trading by setting `"testMode": false`

## Using Your Trading Bot

- Visit your bot's URL to see the dashboard
- The dashboard shows:
  - Trading pair information
  - Live price charts
  - Recent activity
  - Trading performance
- You can adjust settings through the dashboard:
  - Change order sizes
  - Adjust stop-loss percentages
  - Enable/disable trading pairs

## Troubleshooting

- **Bot not responding**: Make sure your Replit project is running
- **No trades executing**: Check your TradingView alerts are set up correctly
- **Error messages**: Make sure your API keys are entered correctly
- **Bot going offline**: Verify UptimeRobot is properly configured

## Safety Tips

- Start with small amounts you can afford to lose
- Always use test mode first
- Monitor your bot regularly
- Keep your API keys secure
- Don't share your API secret with anyone

## Need Help?

- Read the TradingView setup guide: `tradingview_to_webhook_setup.md`
- Check the common issues and solutions section

---

*This project is for educational purposes. Trading cryptocurrencies involves risk. Never invest more than you can afford to lose.*