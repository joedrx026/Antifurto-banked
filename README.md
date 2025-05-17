# Antifurto-banked
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, ContextTypes
import requests

async def bloquear(update: Update, context: ContextTypes.DEFAULT_TYPE):
    requests.post('https://SEU_BACKEND/api/control', json={"action": "lock"})
    await update.message.reply_text("Dispositivo bloqueado remotamente.")

async def desbloquear(update: Update, context: ContextTypes.DEFAULT_TYPE):
    requests.post('https://SEU_BACKEND/api/control', json={"action": "unlock"})
    await update.message.reply_text("Dispositivo desbloqueado.")

app = ApplicationBuilder().token("SEU_TOKEN_DO_BOT").build()
app.add_handler(CommandHandler("bloquear", bloquear))
app.add_handler(CommandHandler("desbloquear", desbloquear))
app.run_polling()
