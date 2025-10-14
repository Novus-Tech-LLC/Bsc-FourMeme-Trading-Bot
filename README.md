![](assets/fourmeme-bot.png)

## BSC FourMeme Trading Bot

A modular, CLI‑driven trading toolkit for the Four.meme ecosystem on BNB Chain. It provides wallet mirroring, route bundling, and volume simulation modules designed to operate fully on‑chain without third‑party market data services.

## Features
- **Bundler**: Execute predefined swap routes (e.g., `WBNB → TOKEN`) with slippage and deadline controls; extensible toward multicalls.
- **Volume Bot**: Programmatic buy/sell loops on a schedule for liquidity and organic activity testing.
- **Copy Trader**: Mirror transactions from a target wallet with configurable risk ceilings.
- **Sniper**: Event‑driven buys on new or specified tokens; supports dry‑run and slippage tuning.
- **Notifications**: Optional Telegram alerts for lifecycle events and errors.
- **Risk Controls**: Allow/deny lists, max spend per trade and per day, basic MEV‑aware settings.

## Architecture overview
- Single entrypoint (`dist/index.js`) with module subcommands.
- Config‑first design using JSON files per module.
- EVM interactions via PancakeSwap V2 Router and standard ERC‑20 approvals.

## Requirements
- [Node.js 22.15+](https://nodejs.org/en/download)
- BNB Chain RPC endpoint (public default supported)
- Wallet private key funded with BNB for gas

## Installation
```bash
npm install
```

## Environment
Copy `.env.example` to `.env` and fill in required values. Defaults for RPC, PancakeV2, and WBNB mainnet are provided.

Optional Telegram notifications:
```
TELEGRAM_BOT_TOKEN=YOUR_TELEGRAM_BOT_TOKEN
TELEGRAM_CHAT_ID=YOUR_CHAT_ID
```

## Configuration
Start from the provided examples and tailor as needed:
- `config.copy.example.json`
- `config.sniper.example.json`
- `config.bundle.example.json`
- `config.volume.example.json`

Notes:
- For Sniper, replace `0xTokenAddressHere` with the target token address.
- For Copy Trader, set `0xLeaderWalletAddress` to the source wallet you intend to mirror.
- Adjust amounts, slippage, deadlines, and lists according to your risk policy.

## Build
```bash
npm run build
```

## Usage
```bash
# Copy Trader
node dist/index.js copy -c config.copy.example.json

# Sniper (start with dry‑run)
node dist/index.js sniper -c config.sniper.example.json --dry-run

# Bundler
node dist/index.js bundle -c config.bundle.example.json

# Volume Bot
node dist/index.js volume -c config.volume.example.json
```

Tip: All commands accept standard flags and module‑specific options. Use `--help` on any command to see available parameters.

## Operating guidance
- Begin in dry‑run where available; scale position size gradually.
- Maintain deny lists and verify token/router addresses before enabling live trades.
- In fast markets, sniper slippage of 3–8% can be typical—validate with small notional first.
- For copy trading, enforce per‑trade caps and a daily max exposure.

## Security
- Never commit secrets or private keys; use environment variables or a secrets manager.
- Prefer a dedicated hot wallet for experimentation; keep treasury in cold storage.
- Double‑check token and router contract addresses; avoid interacting with unverified contracts.
- Test in dry‑run, then small sizes in production before scaling.

## Troubleshooting
- Ensure Node.js version matches the requirement.
- If RPC rate limits occur, switch to a higher‑throughput provider or add retries/backoff.
- For failed swaps, review slippage/deadline settings and token allowance/approval status.

## Contact

| Platform | Link |
|----------|------|
| 📱 Telegram | [t.me/novustch](https://t.me/novustch) |
| 📲 WhatsApp | [wa.me/14105015750](https://wa.me/14105015750) |
| 💬 Discord | [discordapp.com/users/985432160498491473](https://discordapp.com/users/985432160498491473)

<div align="center">
    <a href="https://t.me/novustch" target="_blank"><img alt="Telegram"
        src="https://img.shields.io/badge/Telegram-26A5E4?style=for-the-badge&logo=telegram&logoColor=white"/></a>
    <a href="https://wa.me/14105015750" target="_blank"><img alt="WhatsApp"
        src="https://img.shields.io/badge/WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white"/></a>
    <a href="https://discordapp.com/users/985432160498491473" target="_blank"><img alt="Discord"
        src="https://img.shields.io/badge/Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white"/></a>
</div>

Feel free to reach out for implementation assistance or integration support.


## Disclaimer
This software is provided “as is” with no warranties. You are solely responsible for compliance, risk management, and any financial outcomes. Use at your own risk.