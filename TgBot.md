import telebot
from bs4 import BeautifulSoup as b
import requests
from telebot import types
TOKEN = ""
bot = telebot.TeleBot(TOKEN)
URL = "https://apply.innopolis.university/bachelor/?lang=ru&id=12&site=s1&template=university24&landing_mode=edit"
r = requests.get(URL)
soup = b(r.text, "html.parser")
fag = soup.find_all("div", class_="learning-program top-left learning-program_no-padding")
fag_gg= [c.text for c in fag]
print(fag_gg)
@bot.message_handler(commands=['start'])
def welcome(message):
     item2 = types.KeyboardButton("Информация")
    # keyboard
     markup = types.ReplyKeyboardMarkup(resize_keyboard=True) 
     bot.send_message(message.chat.id, "Добро пожаловать, {0.first_name}!\nЯ - <b>{1.first_name}</b>".format(message.from_user, bot.get_me()), parse_mode='html', reply_markup=markup)
@bot.message_handler(content_types=['text'])
def lalala(message):
    if message.chat.type == 'private':
        if message.text == 'Информация':
            bot.send_message(message.chat.id, fag_gg)
bot.polling(none_stop=True)
