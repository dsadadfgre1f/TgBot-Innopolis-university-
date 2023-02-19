import time
import telebot
from bs4 import BeautifulSoup as b
import requests
from telebot import types
TOKEN = "5118005232:AAHy6trbCdhAxTCuj8b1tae4ZvwPykE6Kuw"
bot = telebot.TeleBot(TOKEN)

#Бакалавр Иннополис
UrlBacalawr = "https://apply.innopolis.university/bachelor/?lang=ru&id=12&site=s1&template=university24&landing_mode=edit"
r = requests.get(UrlBacalawr)
bak3 = b(r.text, "html.parser")
fag = bak3.find_all("div", class_="block-wrapper block-columns-bachelor-page-lp")
fag_gg= [c.text for c in fag]
baka = bak3.find_all("div", class_="contacts__requisites")
baka_gg= [c.text for c in baka]

#магистрат Иннополис
UrlMagistrat = "https://apply.innopolis.university/master/datascience/?lang=ru&id=12&site=s1&template=university24&landing_mode=edit"
rems1 = requests.get(UrlMagistrat)
bak2 = b(rems1.text, "html.parser")
Mag = bak2.find_all("div", class_="learning-programs-wrap")
Mag_gg= [c.text for c in Mag]
Maga = bak2.find_all("div" , class_="contacts__requisites")
Maga_gg= [c.text for c in Maga]

#аспирантура Иннополис
UrlMaSPIRANT = "https://apply.innopolis.university/postgraduate-study/?lang=ru&id=12&site=s1&template=university24&landing_mode=edit"
rems2 = requests.get(UrlMaSPIRANT)
bak1 = b(rems2.text, "html.parser")
Aspirant = bak1.find_all("div", class_="faq-container uni-center-tech uni-postgraduate-main g-mt-auto g-pr-auto g-pl-auto g-pt-5 g-pb-1")
As = bak1.find_all("div" , class_="contacts__requisites")
As_gg= [c.text for c in As]
Aspirant_gg= [c.text for c in Aspirant]

#СФУ МАГИСТРАТ
UrlCFYMaga = "https://admissions.sfu-kras.ru/magisters/reasons"
UrlCFYMaga1 = "https://admissions.sfu-kras.ru/magisters"
rezalut1 = requests.get(UrlCFYMaga1)
BakBan1 = b(rezalut1.text, "html.parser")

rezalut = requests.get(UrlCFYMaga)
BakBan = b(rezalut.text, "html.parser")
gegeg = BakBan.find_all("div", class_="text")
gegeg_gg= [c.text for c in gegeg]

gegeg1 = BakBan1.find_all("div", class_="admission-general-contacts")
gegeg_gg1= [c.text for c in gegeg1]

#СФУ aспирантура
UrlCFYAsp = "https://admissions.sfu-kras.ru/post-graduates"
Aspir = requests.get(UrlCFYAsp)
Aspirantura = b(Aspir.text, "html.parser")
asa1 = Aspirantura.find_all("div", class_="useful-links")
asa_gg1= [c.text for c in asa1]

#СФУ ДОКТОРАНТУРА
urldok = "https://research.sfu-kras.ru/doktorantura"
dok = requests.get(urldok)
dokrantura = b(dok.text, "html.parser")
dokrantura1 = dokrantura.find_all("div", class_="text")
dokrantura_gg1= [c.text for c in dokrantura1]
urldok1 = "https://edu.ru/vuz/card/sibirskij-federalnyj-universitet/contacts"
dok1 = requests.get(urldok1)
dokrantura1 = b(dok1.text, "html.parser")
dokrantura11 = dokrantura1.find_all("div",class_="vz-contact-descr__group")
dokrantura_gg= [c.text for c in dokrantura11]


@bot.message_handler(commands=['start'])
def welcome(message):
    # keyboard
    markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
    button0 = types.KeyboardButton('🏙️ Выбрать город вуза')
    button1 = types.KeyboardButton('😆 Бот дай стикеры')

    markup.add(button0,button1)

    bot.send_message(message.chat.id, "Добро пожаловать, {0.first_name}!\nЯ - <b>{1.first_name}</b>".format(message.from_user, bot.get_me()), parse_mode='html', reply_markup=markup)
    bot.send_sticker(message.chat.id, 'CAACAgIAAxkBAAIf62Pw2KlFkiCLyrnLh2g3YNYxoF7xAAJWHwACDX0hSL8dU9iFVCIjLgQ')
    bot.send_message(message.chat.id, "Добро пожаловать")




@bot.message_handler(content_types=['text'])
def bacalavr(message):
    if message.chat.type == 'private':
        if message.text == '😆 Бот дай стикеры': #Основная команда выдачи стикеров, она же всплывающая ссылка=кнопке
            bot.send_message(message.chat.id, "Я думаю дать ли Вам стикеры 🤔")
            time.sleep(3)
            bot.send_message(message.chat.id, "Я подумал, в общем держите)")
            bot.send_sticker(message.chat.id, 'CAACAgIAAxkBAAIf22Pw1nMbY3B0sMCvOJHkFQEvFQABsgACviMAAjz1iUvsum-B48V8IS4E')
            markup = types.InlineKeyboardMarkup()
            button1 = types.InlineKeyboardButton("СтикерПак Советский Питон!", url='https://t.me/addstickers/PythonUSSR')
            markup.add(button1)
            bot.send_message(message.chat.id, "Приятного пользования 😁😁😁!", reply_markup=markup)
    if message.chat.type == 'private':
        if message.text == '🏙️ Выбрать город вуза': #Выбор городов вуза
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('🌆 Иннополис')
            button1 = types.KeyboardButton('🌁 Красноярск')
            button2 = types.KeyboardButton('🏙 Новосибирск')
            back = types.KeyboardButton('⬅ Назад к меню')
            markup.add(button0, button1, button2, back)
            bot.send_message(message.chat.id, "🏙️ Выбрать город вуза", reply_markup=markup)



    

    #Иннополис всё что под этим комментом только об этом городе, за исключением выходов назад
    if message.chat.type == 'private':
        if message.text == '🌆 Иннополис': #Выбор города
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('🎓 Университет Иннополис')
            button1 = types.KeyboardButton('😆 Бот дай стикеры')
            button2 = types.KeyboardButton('⬅ Назад к выбору города')
            markup.add(button0, button1, button2)
            bot.send_message(message.chat.id, "Выберите университет", reply_markup=markup)
    if message.chat.type == 'private':
        if message.text == '🎓 Университет Иннополис': #Выбор университета
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('📖 Баклавриату Иннополиса')
            button1 = types.KeyboardButton('🎓 Магистру Иннополиса')
            button2 = types.KeyboardButton('📃 Аспиранту Иннополиса')
            button3 = types.KeyboardButton('📞 Контактная информация Иннополиса')
            button4 = types.KeyboardButton('🌐 Cайт Иннополиса')
            button5 = types.KeyboardButton('⬅ Университеты Иннополиса')
            markup.add(button0, button1, button2, button3, button4, button5)
            bot.send_message(message.chat.id, "🎓 Университет Иннополис", reply_markup=markup)

    if message.chat.type == 'private':
        if message.text == '🌐 Cайт Иннополиса': #Реализация всплывающей ссылки сайта
            markup = types.InlineKeyboardMarkup()
            button1 = types.InlineKeyboardButton("🌐 Cайт Иннополиса", url='https://innopolis.university/')
            markup.add(button1)
            bot.send_message(message.chat.id, "🌐 Основной сайт университета Иннополиса", reply_markup=markup)

    if message.chat.type == 'private':
        if message.text == '📖 Баклавриату Иннополиса': #Кнопка информации
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Бакалавриата🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, fag_gg)


    if message.chat.type == 'private':
        if message.text == '🎓 Магистру Иннополиса': #Кнопка информации
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Магистратуры🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, Mag_gg)


    if message.chat.type == 'private':
        if message.text == '📃 Аспиранту Иннополиса': #Кнопка информации
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Аспирантуры🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, Aspirant_gg)

    if message.chat.type == 'private':
        if message.text == '📞 Контактная информация Иннополиса': #Меню контактной информации
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('📞 Бакалавриата Иннополиса')
            button1 = types.KeyboardButton('📞 Магистратуры Иннополиса')
            button2 = types.KeyboardButton('📞 Аспирантуры Иннополиса')
            back = types.KeyboardButton('⬅ Назад к меню Иннополиса')
            markup.add(button0, button1, button2, back)
            bot.send_message(message.chat.id, "📞 Контактная информация Иннополиса", reply_markup=markup)

    if message.chat.type == 'private': #Кнопки контактной информации
        if message.text == '📞 Бакалавриата Иннополиса':
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Контакты Бакалавриата🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, baka_gg)
    if message.chat.type == 'private':
        if message.text == '📞 Магистратуры Иннополиса':
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Контакты Магистратуры🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, Maga_gg)
    if message.chat.type == 'private':
        if message.text == '📞 Аспирантуры Иннополиса':
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Контакты Аспирантуры🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, As_gg)
    #Иннополис




    if message.chat.type == 'private':
        if message.text == '⬅ Назад к меню':
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('🏙️ Выбрать город вуза')
            button1 = types.KeyboardButton('😆 Бот дай стикеры')
            markup.add(button0, button1)
            bot.send_message(message.chat.id, "⬅ Назад к меню", reply_markup=markup)
    if message.chat.type == 'private':
        if message.text == '⬅ Назад к выбору города':
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('🌆 Иннополис')
            button1 = types.KeyboardButton('🌁 Красноярск')
            button2 = types.KeyboardButton('🏙 Новосибирск')
            back = types.KeyboardButton('⬅ Назад к меню')
            markup.add(button0, button1, button2, back)
            bot.send_message(message.chat.id, "🏙️ Выбрать город вуза", reply_markup=markup)
    if message.chat.type == 'private':
        if message.text == '⬅ Университеты Иннополиса':
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('🎓 Университет Иннополис')
            button1 = types.KeyboardButton('😆 Бот дай стикеры')
            button2 = types.KeyboardButton('⬅ Назад к выбору города')
            markup.add(button0, button1, button2)
            bot.send_message(message.chat.id, "Выберите университет", reply_markup=markup)
    if message.chat.type == 'private':
        if message.text == '⬅ Назад к меню Иннополиса':
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('📖 Баклавриату Иннополиса')
            button1 = types.KeyboardButton('🎓 Магистру Иннополиса')
            button2 = types.KeyboardButton('📃 Аспиранту Иннополиса')
            button3 = types.KeyboardButton('📞 Контактная информация Иннополиса')
            button4 = types.KeyboardButton('🌐 Cайт Иннополиса')
            button5 = types.KeyboardButton('⬅ Университеты Иннополиса')
            markup.add(button0, button1, button2, button3, button4, button5)
            bot.send_message(message.chat.id, "🎓 Университет Иннополис", reply_markup=markup)







    #Красноярск всё что под этим комментом только об этом городе, за исключением выходов назад
    if message.chat.type == 'private':
        if message.text == '🌁 Красноярск': #Выбор города
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('🎓 СФУ')
            button1 = types.KeyboardButton('😆 Бот дай стикеры')
            button2 = types.KeyboardButton('⬅ Назад к выбору города')
            markup.add(button0, button1, button2)
            bot.send_message(message.chat.id, "Выберите университет", reply_markup=markup)
    if message.chat.type == 'private':
        if message.text == '🎓 СФУ': #Выбор университета
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('📖 Докторантура')
            button1 = types.KeyboardButton('🎓 Аспирантура')
            button2 = types.KeyboardButton('📃 Магистратура')
            button3 = types.KeyboardButton('📞 Контактная информация СФУ')
            button4 = types.KeyboardButton('🌐 Cайт СФУ')
            button5 = types.KeyboardButton('⬅ Университеты')
            markup.add(button0, button1, button2, button3, button4, button5)
            bot.send_message(message.chat.id, "🎓 СФУ", reply_markup=markup)

    if message.chat.type == 'private':
        if message.text == '🌐 Cайт СФУ': #Реализация всплывающей ссылки сайта
            markup = types.InlineKeyboardMarkup()
            button1 = types.InlineKeyboardButton("🌐 Cайт СФУ", url='https://www.sfu-kras.ru/')
            markup.add(button1)
            bot.send_message(message.chat.id, "🌐 Основной сайт университета СФУ", reply_markup=markup)

    if message.chat.type == 'private':
        if message.text == '📖 Докторантура': #Кнопка информации
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Докторантуры🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, dokrantura_gg1)
            


    if message.chat.type == 'private':
        if message.text == '🎓 Аспирантура': #Кнопка информации
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Аспирантуры🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, "Аспирантура является основной формой подготовки кадров высшей квалификации для работы в сфере образования, науки, высоких технологий и других видов интеллектуальной деятельности.Сибирский федеральный университет осуществляет подготовку научных и научно-педагогических кадров в аспирантуре по 26 группам научных специальностей и 115 программам аспирантуры, в аспирантуре обучается более 700 аспирантов. Научное руководство аспирантами в СФУ осуществляют свыше 350 учёных, действуют 15 диссертационных советов.Подготовка аспирантов, зачисленных в аспирантуру до 2022 года, осуществляется в соответствии с Федеральными государственными образовательными стандартами (ФГОС).С 2022 года аспирантура перешла на принципиально новый формат. Набор 2022 года проведен в соответствии с новой номенклатурой научных специальностей. Обучение осуществляется по Федеральными государственными требованиями (ФГТ). Переход на ФГТ подразумевает сокращение образовательной компоненты и смещение фокуса на научную компоненту.Также подготовка диссертационной работы может осуществляться в рамках прикрепления для подготовки диссертации на соискание ученой степени кандидата наук без освоения программ аспирантуры. Прикрепление для выполнения работы осуществляется на срок до 3 лет.")


    if message.chat.type == 'private':
        if message.text == '📃 Магистратура': #Кнопка информации
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Магистратуры🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, gegeg_gg)

    if message.chat.type == 'private':
        if message.text == '📞 Контактная информация СФУ': #Меню контактной информации
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('📞 Докторантура СФУ')
            button1 = types.KeyboardButton('📞 Аспирантура СФУ')
            button2 = types.KeyboardButton('📞 Магастратура СФУ')
            back = types.KeyboardButton('⬅ Университеты')
            markup.add(button0, button1, button2, back)
            bot.send_message(message.chat.id, "📞 Контактная информация СФУ", reply_markup=markup)

    if message.chat.type == 'private': #Кнопки контактной информации
        if message.text == '📞 Докторантура СФУ':
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Контакты Бакалавриата🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, dokrantura_gg)
    if message.chat.type == 'private':
        if message.text == '📞 Аспирантура СФУ':
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Контакты Магистратуры🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, asa_gg1)
    if message.chat.type == 'private':
        if message.text == '📞 Магастратура СФУ':
            bot.send_message(message.chat.id, "Ищу нужную Вам информацию по теме Контакты Аспирантуры🔎")
            time.sleep(0.2)
            bot.send_message(message.chat.id, "Вот что удалось найти!")
            bot.send_message(message.chat.id, gegeg_gg1)
    #сфу




    if message.chat.type == 'private':
        if message.text == '⬅ Назад к меню':
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('🏙️ Выбрать город вуза')
            button1 = types.KeyboardButton('😆 Бот дай стикеры')
            markup.add(button0, button1)
            bot.send_message(message.chat.id, "⬅ Назад к меню", reply_markup=markup)
    if message.chat.type == 'private':
        if message.text == '⬅ Назад к выбору города':
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('🌆 Иннополис')
            button1 = types.KeyboardButton('🌁 Красноярск')
            button2 = types.KeyboardButton('🏙 Новосибирск')
            back = types.KeyboardButton('⬅ Назад к меню')
            markup.add(button0, button1, button2, back)
    if message.chat.type == 'private':
        if message.text == '⬅ Университеты':
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('🎓 СФУ')
            button1 = types.KeyboardButton('😆 Бот дай стикеры')
            button2 = types.KeyboardButton('⬅ Назад к выбору города')
            markup.add(button0, button1, button2)
            bot.send_message(message.chat.id, "Выберите университет", reply_markup=markup)
    if message.chat.type == 'private':
        if message.text == '⬅ Назад к меню СФУ':
            markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
            button0 = types.KeyboardButton('📖 Докторантура')
            button1 = types.KeyboardButton('🎓 Аспирантура')
            button2 = types.KeyboardButton('📃 Магистратура')
            button3 = types.KeyboardButton('📞 Контактная информация СФУ')
            button4 = types.KeyboardButton('🌐 Cайт СФУ')
            button5 = types.KeyboardButton('⬅ Университеты')
            markup.add(button0, button1, button2, button3, button4, button5)
            bot.send_message(message.chat.id, "🎓 СФУ", reply_markup=markup)


print("Бот успешно запущен")
bot.polling(none_stop=True)
