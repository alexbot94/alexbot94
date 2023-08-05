from telegram import Update
from telegram.ext import Updater, CommandHandler, MessageHandler, Filters, CallbackContext

# Replace 'alexbot94' with your Telegram bot token obtained from BotFather
TOKEN = 'alexbot94'

# Function to handle the '/start' command
def start(update: Update, _: CallbackContext):
    update.message.reply_text("Hello! I'm your friendly bot. Send me a message and I'll greet you back.")

# Function to handle messages
def echo(update: Update, _: CallbackContext):
    user_message = update.message.text
    response = f"Hello, you said: {user_message}"
    update.message.reply_text(response)

def main():
    updater = Updater(TOKEN)

    # Get the dispatcher to register handlers
    dp = updater.dispatcher

    # Register command handler
    dp.add_handler(CommandHandler("start", start))

    # Register message handler
    dp.add_handler(MessageHandler(Filters.text & ~Filters.command, echo))

    # Start the Bot
    updater.start_polling()

    # Run the bot until the user presses Ctrl-C
    updater.idle()

if __name__ == '__main__':
    main()
    
