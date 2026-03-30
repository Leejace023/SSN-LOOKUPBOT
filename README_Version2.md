# 🤖 Telegram SSN Lookup Bot

A Python-based Telegram bot that validates and verifies Social Security Numbers (SSNs) with full name and zip code verification.

## Features

✅ SSN format validation (XXX-XX-XXXX)  
✅ Invalid SSN range detection (000, 666, 900-999)  
✅ Full name verification  
✅ Zip code verification  
✅ API integration ready (third-party SSN verification services)  
✅ User-friendly conversation flow  
✅ Error handling and logging  

## Prerequisites

- Python 3.8 or higher
- Telegram account
- Telegram Bot Token (from BotFather)

## Setup Instructions

### 1. Create Your Telegram Bot Token

1. Open Telegram and search for **@BotFather**
2. Send `/newbot` command
3. Follow the prompts to create a new bot
4. Copy your **API Token** (looks like: `123456789:ABCdefGHIjklmnoPQRstuvWXYZ`)

### 2. Clone/Download the Project

```bash
git clone <your-repo-url>
cd telegram-ssn-bot
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure the Bot

Create a `.env` file in the project root:

```
TELEGRAM_BOT_TOKEN=your_bot_token_here
```

Or directly update `config.py`:

```python
API_TOKEN = 'your_bot_token_here'
```

### 5. Run the Bot

```bash
python bot.py
```

You should see:
```
🤖 Bot is starting...
```

### 6. Test Your Bot

1. Open Telegram
2. Search for your bot (the username you created)
3. Send `/start` to begin SSN verification
4. Follow the prompts to enter:
   - SSN (format: XXX-XX-XXXX)
   - Full Name
   - Zip Code

## Usage

### Commands

- `/start` - Begin SSN verification process
- `/help` - Show available commands
- `/cancel` - Cancel current operation

### Example Conversation

```
You: /start
Bot: 🔐 Welcome to SSN Lookup Bot!
     Please enter your Social Security Number (format: XXX-XX-XXXX):

You: 123-45-6789
Bot: ✅ SSN received. Now, please enter your full name:

You: John Doe
Bot: ✅ Name received. Now, please enter your zip code:

You: 10001
Bot: ✅ **SSN VERIFIED**
     SSN: 123-45-6789
     Name: John Doe
     Zip Code: 10001
     Status: VALID
```

## API Integration (Production)

For production use, integrate with a real SSN verification API:

### Recommended Services:
- **IDology** - Industry standard for identity verification
- **Experian** - Credit bureau with verification services
- **Equifax** - Another major credit bureau
- **TrueListic** - Identity verification platform

Update the `verify_ssn_with_api()` function in `ssn_validator.py` with your API endpoint and authentication credentials.

### Example API Integration:

```python
def verify_ssn_with_api(ssn: str, full_name: str, zip_code: str) -> Tuple[bool, Dict]:
    headers = {
        'Authorization': f'Bearer {API_KEY}',
        'Content-Type': 'application/json'
    }
    
    payload = {
        "ssn": ssn.replace('-', ''),
        "name": full_name,
        "zip_code": zip_code
    }
    
    response = requests.post(SSN_API_ENDPOINT, json=payload, headers=headers)
    return response.status_code == 200, response.json()
```

## File Structure

```
telegram-ssn-bot/
├── bot.py                 # Main bot application
├── ssn_validator.py       # SSN validation logic
├── config.py              # Configuration settings
├── requirements.txt       # Python dependencies
├── .env                   # Environment variables (create this)
└── README.md             # This file
```

## Error Handling

The bot includes error handling for:
- Invalid SSN format
- Invalid SSN ranges
- API errors
- User input validation
- Network errors

## Security Considerations

⚠️ **Important:**
- Never hardcode your bot token in production
- Use environment variables (`.env` file)
- Add `.env` to `.gitignore` if using version control
- Ensure compliance with FCRA, GDPR, and privacy laws
- Sanitize and validate all user input
- Use HTTPS for API calls
- Implement rate limiting for production use

## Troubleshooting

### Bot not responding
- Check if bot is running: `python bot.py`
- Verify bot token is correct in config
- Ensure internet connection

### Module not found errors
- Run: `pip install -r requirements.txt`
- Verify Python version is 3.8+

### API errors
- Check API endpoint and credentials
- Verify network connection
- Check API service status

## Contributing

Feel free to fork and submit pull requests for improvements!

## License

MIT License - feel free to use this project for your needs.

## Support

For issues or questions:
1. Check Telegram's Bot API documentation
2. Review error logs in the console
3. Test with `/help` command

---

**Created with ❤️ for SSN verification via Telegram**