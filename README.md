# ALALAimport requests
import datetime
from telegram import Bot

# Telegram credentials
BOT_TOKEN = '8384091601:AAFzMdbHpayuVlKj7_XFf-mO_xMKxZLO5ak'
CHAT_ID = '5461153356'

# Function to fetch SGX Nifty
def get_sgx_nifty():
    try:
        res = requests.get("https://www.sgxnifty.org/", timeout=10)
        if "GIFT Nifty" in res.text:
            return "+ve"  # Simplified mock
    except:
        return "unknown"

# Function to mock FII/DII, US data etc.
def fetch_market_data():
    return {
        "sgx_nifty": "+245 pts",
        "us_market": "Dow -0.38%, Nasdaq +0.15%",
        "fii_dii": "FII -₹850 Cr, DII +₹1829 Cr",
        "asia": "Nikkei +1%, Hang Seng -1.1%",
        "news": "Trump 25% tariff on India goods",
        "prediction": "🔻 Gap-Down"
    }

# Format message
def format_message(data):
    today = datetime.datetime.now().strftime("%d %b %Y")
    return f"""📊 Nifty/BankNifty Gap Prediction — {today}

🔹 SGX Nifty: {data['sgx_nifty']}
🔹 US Markets: {data['us_market']}
🔹 FII/DII: {data['fii_dii']}
🔹 Asia/Europe: {data['asia']}
🔸 News: {data['news']}

📈 Market Likely to Open: {data['prediction']}
"""

# Send to Telegram
def send_to_telegram(message):
    bot = Bot(token=BOT_TOKEN)
    bot.send_message(chat_id=CHAT_ID, text=message)

# Run
if __name__ == "__main__":
    market_data = fetch_market_data()
    msg = format_message(market_data)
    send_to_telegram(msg)
