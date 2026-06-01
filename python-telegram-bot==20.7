import os
import sqlite3
import logging
from datetime import datetime

from telegram import Update
from telegram.ext import Application, CommandHandler, MessageHandler, ContextTypes, filters

# ---------------- TOKEN (RENDER 24/7 SAFE) ----------------
TOKEN = os.environ.get("TOKEN")

# ---------------- LOGGING ----------------
logging.basicConfig(
    format="%(asctime)s - %(name)s - %(levelname)s - %(message)s",
    level=logging.INFO
)

# ---------------- DATABASE ----------------
def init_db():
    conn = sqlite3.connect("checkin.db")
    c = conn.cursor()

    c.execute("""
        CREATE TABLE IF NOT EXISTS checkins (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            user_id INTEGER,
            username TEXT,
            first_name TEXT,
            lat REAL,
            lon REAL,
            time TEXT
        )
    """)

    conn.commit()
    conn.close()


def save_checkin(user_id, username, first_name, lat, lon):
    conn = sqlite3.connect("checkin.db")
    c = conn.cursor()

    c.execute("""
        INSERT INTO checkins (user_id, username, first_name, lat, lon, time)
        VALUES (?, ?, ?, ?, ?, ?)
    """, (
        user_id,
        username,
        first_name,
        lat,
        lon,
        datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    ))

    conn.commit()
    conn.close()


def get_today_checkins(user_id):
    today = datetime.now().strftime("%Y-%m-%d")

    conn = sqlite3.connect("checkin.db")
    c = conn.cursor()

    c.execute("""
        SELECT COUNT(*)
        FROM checkins
        WHERE user_id = ?
        AND date(time) = ?
    """, (user_id, today))

    total = c.fetchone()[0]

    conn.close()
    return total


# ---------------- HANDLERS ----------------
async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(
        "📍 Send your location to check in.\n"
        "⚠️ Only 1 check-in per day allowed."
    )


async def location_handler(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user = update.effective_user
    loc = update.message.location

    # check already checked in today
    if get_today_checkins(user.id) >= 1:
        await update.message.reply_text(
            "❌ You already checked in today!"
        )
        return

    save_checkin(
        user.id,
        user.username or "NoUsername",
        user.first_name or "NoName",
        loc.latitude,
        loc.longitude
    )

    await update.message.reply_text(
        "✅ Check-in successful!\n"
        f"👤 {user.first_name}\n"
        "📍 Saved for today"
    )


# ---------------- MAIN ----------------
def main():
    init_db()

    if not TOKEN:
        print("ERROR: TOKEN not found in environment variables")
        return

    app = Application.builder().token(TOKEN).build()

    app.add_handler(CommandHandler("start", start))
    app.add_handler(MessageHandler(filters.LOCATION, location_handler))

    print("Bot is running...")
    app.run_polling()


if __name__ == "__main__":
    main()   