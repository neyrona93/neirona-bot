# neirona-bot
Нейрона — умный и дружелюбный цифровой собimport openai
from telegram import Update
from telegram.ext import ApplicationBuilder, CommandHandler, MessageHandler, filters, ContextTypes

TELEGRAM_BOT_TOKEN = "8018459053:AAFS2VxlR2I7_HztGltI0o387PzJAwVKBZs"
OPENAI_API_KEY = "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"

openai.api_key = OPENAI_API_KEY

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text("Привет! Я Нейрона, твой консультант по товарам и услугам. Чем могу помочь?")

async def handle_message(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user_message = update.message.text

    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[
            {"role": "system", "content": "Ты — чат-бот Нейрона. Вежливо и понятно помогаешь клиентам выбрать товар, оформить заказ и отвечаешь на часто задаваемые вопросы."},
            {"role": "user", "content": user_message}
        ]
    )

    reply = response.choices[0].message.content
    await update.message.reply_text(reply)

if __name__ == '__main__':
    app = ApplicationBuilder().token(TELEGRAM_BOT_TOKEN).build()
    app.add_handler(CommandHandler("start", start))
    app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, handle_message))
    app.run_polling()
еседник, созданный для того, чтобы упростить общение, автоматизировать ответы и помогать людям 24/7. Она легко интегрируется в сайты, мессенджеры или бизнес-платформы и может быть настроена под любую сферу: от клиентского сервиса до образовательных проектов.
python-telegram-bot==20.0
openai
