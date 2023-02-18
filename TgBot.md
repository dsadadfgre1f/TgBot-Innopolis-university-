import time
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
    button0 = types.KeyboardButton('📖 Баклавриату')
    button1 = types.KeyboardButton('🎓 Магистру')
    button2 = types.KeyboardButton('📃 Аспиранту')
    button3 = types.KeyboardButton('😆 Бот дай стикеры')
    button4 = types.KeyboardButton('📞 Контактная информация')

    markup.add(button0,button1,button2,button3,button4)

    bot.send_message(message.chat.id, "Добро пожаловать, {0.first_name}!\nЯ - <b>{1.first_name}</b>".format(message.from_user, bot.get_me()), parse_mode='html', reply_markup=markup)
    bot.send_sticker(message.chat.id, 'CAACAgIAAxkBAAIf62Pw2KlFkiCLyrnLh2g3YNYxoF7xAAJWHwACDX0hSL8dU9iFVCIjLgQ')



@bot.message_handler(content_types=['text'])
def bacalavr(message):
    if message.chat.type == 'private':
        if message.text == '📖 Баклавриату':
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Бакалавриата🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, fag_gg)


    if message.chat.type == 'private':
        if message.text == '🎓 Магистру':
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Магистратуры🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, Mag_gg)


    if message.chat.type == 'private':
        if message.text == '📃 Аспиранту':
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Аспирантуры🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, Aspirant_gg)

    if message.chat.type == 'private':
        if message.text == '😆 Бот дай стикеры':
            bot.send_message(message.chat.id, "Я думаю дать ли Вам стикеры 🤔")
            time.sleep(3)
            bot.send_message(message.chat.id, "Я подумал, в общем держите, приятного пользования 😁😁😁")
            bot.send_sticker(message.chat.id, 'CAACAgIAAxkBAAIf22Pw1nMbY3B0sMCvOJHkFQEvFQABsgACviMAAjz1iUvsum-B48V8IS4E')
            bot.send_message(message.chat.id, "https://t.me/addstickers/SovetPiton")

    if message.chat.type == 'private':
        if message.text == '📞 Контактная информация':
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('📖 Контакты Бакалавриата')
            button1 = types.KeyboardButton('🎓 Контакты Магистратуры')
            button2 = types.KeyboardButton('📃 Контакты Аспирантуры')
            back = types.KeyboardButton('⬅ Назад')
            markup.add(button0, button1, button2, back)
            bot.send_message(message.chat.id, "📞 Контактная информация", reply_markup=markup)
    if message.chat.type == 'private':
        if message.text == '📖 Контакты Бакалавриата':
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Контакты Бакалавриата🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, baka_gg)
    if message.chat.type == 'private':
        if message.text == '🎓 Контакты Магистратуры':
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Контакты Магистратуры🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, Maga_gg)
    if message.chat.type == 'private':
        if message.text == '📃 Контакты Аспирантуры':
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Контакты Аспирантуры🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, As_gg)

    if message.chat.type == 'private':
        if message.text == '⬅ Назад':
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('📖 Баклавриату')
            button1 = types.KeyboardButton('🎓 Магистру')
            button2 = types.KeyboardButton('📃 Аспиранту')
            button3 = types.KeyboardButton('😆 Бот дай стикеры')
            button4 = types.KeyboardButton('📞 Контактная информация')

            markup.add(button0, button1, button2, button3, button4)

            bot.send_message(message.chat.id, "⬅ Назад", reply_markup=markup)




print("Бот успешно запущен")
bot.polling(none_stop=True)
