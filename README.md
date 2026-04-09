# Bot Gmail - Automated Gmail Account Creator

Automated Gmail/YouTube account registration bot using **LDPlayer** (Android emulator) + **Firefox** browser via ADB and UIAutomator2.

## Demo

https://github.com/user-attachments/assets/demo

> Video demo of the bot in action is available. Contact me for the full video.

## Features

- Fully automated signup flow (name, DOB, gender, username, password, phone verification, consent)
- Randomized identity generation using Faker (name, date of birth, gender)
- Smart username handling — picks Gmail suggestions or retries with custom usernames if taken
- SMS verification via **TextVerified** or **SMSPool** (selectable at runtime)
- Auto-retry on rejected phone numbers (up to 3 attempts)
- Auto-retry on failed steps (clears browser data and restarts)
- Accounts saved to `account_data.csv`
- Batch creation — specify how many accounts to create in one session
- Password masked in terminal output
- Clean terminal UI with spinners, colors, and step-by-step progress

## Requirements

- **LDPlayer** (or any Android emulator accessible via ADB)
- **Firefox** installed on the emulator
- **ADB** connected to emulator (`emulator-5556` by default)
- **Python 3.7+**
- SMS provider account (**TextVerified** or **SMSPool**)

## Installation

```bash
pip install uiautomator2 faker requests
```

For TextVerified:
```bash
pip install textverified
```

## Configuration

Edit the config section in `bot-gmail.py`:

```python
DEVICE      = "emulator-5556"       # ADB device ID
PSWD        = "YourPassword123#"    # Default password for created accounts

# TextVerified
TV_API_KEY  = "your-api-key"
TV_USERNAME = "your-username"

# SMSPool
SMSPOOL_API_KEY = "your-api-key"
```

## Usage

```bash
python bot-gmail.py
```

1. Select SMS provider (TextVerified or SMSPool)
2. Enter number of accounts to create
3. Bot runs automatically — retries on failure

### Output

Created accounts are saved to `account_data.csv`:

| username | password | firstName | lastName | dob | gender |
|----------|----------|-----------|----------|-----|--------|
| john.doe42.real | ******** | John | Doe | 15-06-1995 | male |

## How It Works

1. **Name** — Fills first and last name with Faker-generated data
2. **Birthday & Gender** — Selects random DOB (1990-2000) and gender
3. **Username** — Picks suggested Gmail address or enters custom username
4. **Password** — Sets account password
5. **Phone Verification** — Requests a number from SMS provider, enters it, and waits for the OTP code
6. **Recovery Email** — Skips
7. **Consent** — Scrolls through and accepts Google's terms
8. **Done** — Waits for YouTube redirect, saves account to CSV

## Disclaimer

> **This project is for educational and research purposes only.**
>
> The author is not responsible for any misuse of this tool. Using this software to violate Google's Terms of Service or any applicable laws is strictly prohibited. Use at your own risk.

## Contact

Telegram: [@johnmayer](https://t.me/johnmayer)
