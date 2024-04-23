from telegram.ext import Updater, CommandHandler, MessageHandler, Filters

# Define a function to handle the /start command
def start(update, context):
    update.message.reply_text('Hello! I am your Telegram bot. You can type /echo <message> to echo back your message.')

# Define a function to echo back incoming messages
def echo(update, context):
    message = update.message.text.split('/echo ', 1)[1]
    update.message.reply_text('You said: ' + message)

# Define a function to handle the /caps command
def caps(update, context):
    message = ' '.join(context.args).upper()
    update.message.reply_text(message)

# Define a function to handle unknown commands
def unknown(update, context):
    update.message.reply_text("Sorry, I don't understand that command.")

def main():
    # Replace 'YOUR_TOKEN' with your actual Telegram bot token
    updater = Updater(token='YOUR_TOKEN', use_context=True)

    # Get the dispatcher to register handlers
    dp = updater.dispatcher

    # Register command handlers
    dp.add_handler(CommandHandler("start", start))
    dp.add_handler(CommandHandler("caps", caps))
    dp.add_handler(MessageHandler(Filters.command, unknown))  # Handle unknown commands

    # Register a message handler for all non-command messages
    dp.add_handler(MessageHandler(Filters.text & ~Filters.command, echo))

    # Start the Bot
    updater.start_polling()

    # Run the bot until you press Ctrl-C
    updater.idle()

if name == 'main':
    main()
