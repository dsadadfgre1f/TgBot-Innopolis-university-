import telebot
from bs4 import BeautifulSoup as b
import requests
from telebot import types
TOKEN = ""
bot = telebot.TeleBot(TOKEN)

#Бакалавр
UrlBacalawr = "https://apply.innopolis.university/bachelor/?lang=ru&id=12&site=s1&template=university24&landing_mode=edit"
r = requests.get(UrlBacalawr)
bak = b(r.text, "html.parser")
fag = bak.find_all("div", class_="learning-program top-left learning-program_no-padding")
fag_gg= [c.text for c in fag]

#магистрат
UrlMagistrat = "https://apply.innopolis.university/master/datascience/?lang=ru&id=12&site=s1&template=university24&landing_mode=edit"
rems1 = requests.get(UrlMagistrat)
bak = b(rems1.text, "html.parser")
Mag = bak.find_all("div", class_="learning-program top-left learning-program_no-padding")
Mag_gg= [c.text for c in Mag]

#аспирантура
UrlMaSPIRANT = "https://apply.innopolis.university/postgraduate-study/?lang=ru&id=12&site=s1&template=university24&landing_mode=edit"
rems2 = requests.get(UrlMaSPIRANT)
bak = b(rems2.text, "html.parser")
Aspirant = bak.find_all("div", class_="faq-container uni-center-tech uni-postgraduate-main g-mt-auto g-pr-auto g-pl-auto g-pt-5 g-pb-1")
Aspirant_gg= [c.text for c in Aspirant]

@bot.message_handler(commands=['start'])
def welcome(message):
    # keyboard
     markup = types.ReplyKeyboardMarkup(resize_keyboard=True) 
     bot.send_message(message.chat.id, "Добро пожаловать, {0.first_name}!\nЯ - <b>{1.first_name}</b>".format(message.from_user, bot.get_me()), parse_mode='html', reply_markup=markup)

@bot.message_handler(content_types=['text'])
def lalala(message):
    if message.chat.type == 'private':
        if message.text == 'Структура обучения бакалавриат':
            bot.send_message(message.chat.id, fag_gg)


    if message.chat.type == 'private':
        if message.text == 'Структура обучения магистратура':
            bot.send_message(message.chat.id, Mag_gg)

    if message.chat.type == 'private':
        if message.text == 'Структура обучения аспирантуры':
            bot.send_message(message.chat.id, Aspirant_gg)
