import telebot
from bs4 import BeautifulSoup as b
import requests
from telebot import types
TOKEN = ""
bot = telebot.TeleBot(TOKEN)

#Бакалавр
UrlBacalawr = "https://apply.innopolis.university/bachelor/?lang=ru&id=12&site=s1&template=university24&landing_mode=edit"
r = requests.get(UrlBacalawr)
bak3 = b(r.text, "html.parser")
fag = bak3.find_all("div", class_="learning-program top-left learning-program_no-padding")
fag_gg= [c.text for c in fag]
baka = bak3.find_all("div", class_="contacts__requisites")
baka_gg= [c.text for c in baka]

#магистрат
UrlMagistrat = "https://apply.innopolis.university/master/datascience/?lang=ru&id=12&site=s1&template=university24&landing_mode=edit"
rems1 = requests.get(UrlMagistrat)
bak2 = b(rems1.text, "html.parser")
Mag = bak2.find_all("div", class_="learning-program top-left learning-program_no-padding")
Mag_gg= [c.text for c in Mag]
Maga = bak2.find_all("div" , class_="contacts__requisites")
Maga_gg= [c.text for c in Maga]

#аспирантура
UrlMaSPIRANT = "https://apply.innopolis.university/postgraduate-study/?lang=ru&id=12&site=s1&template=university24&landing_mode=edit"
rems2 = requests.get(UrlMaSPIRANT)
bak1 = b(rems2.text, "html.parser")
Aspirant = bak1.find_all("div", class_="faq-container uni-center-tech uni-postgraduate-main g-mt-auto g-pr-auto g-pl-auto g-pt-5 g-pb-1")
As = bak1.find_all("div" , class_="contacts__requisites")
As_gg= [c.text for c in As]
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
            bot.send_message(message.chat.id, baka_gg)



    if message.chat.type == 'private':
        if message.text == 'Структура обучения магистратура':
            bot.send_message(message.chat.id, Mag_gg)
            bot.send_message(message.chat.id, Maga_gg)


    if message.chat.type == 'private':
        if message.text == 'Структура обучения аспирантуры':
            bot.send_message(message.chat.id, Aspirant_gg)
            bot.send_message(message.chat.id, As_gg)      



bot.polling(none_stop=True)
