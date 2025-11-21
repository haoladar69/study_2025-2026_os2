---
## Front matter
title: "Отчёт по лабораторной работе №8"
subtitle: "Планировщики событий"
author: "Шаханеоядж Хаоладар"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true
toc-depth: 2
lof: true
lot: true
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
    - spelling=modern
    - babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float}
  - \floatplacement{figure}{H}
---

# Цель работы

Получение навыков работы с планировщиками событий cron и at.

# Выполнение

## Планирование задач с помощью cron и at

1. В терминале был получен доступ администратора с помощью команды **su -**.  
   После этого проверен статус службы **crond**, отвечающей за планирование периодических заданий.  

   ![Проверка статуса службы crond](Screenshot_1.png){ #fig:001 width=80% }

   Из вывода видно, что служба **crond.service** находится в состоянии **active (running)** и запущена автоматически при старте системы.  

2. Для ознакомления с системным файлом расписаний был просмотрен файл **/etc/crontab**.  
   Он содержит переменные окружения и пример формата задания в cron.  

   ![Содержимое файла /etc/crontab](Screenshot_2.png){ #fig:002 width=80% }

   Каждое задание в этом файле имеет шесть полей: минута, час, день месяца, месяц, день недели и пользователь, от имени которого выполняется команда.  
   Такой формат определяет расписание и пользователя, от имени которого выполняется задача.

3. С помощью команды **crontab -e** было открыто расписание текущего пользователя и добавлена строка  
   ***/1 * * * * logger This message is written from root cron***.  
   Эта запись означает запуск команды **logger** каждую минуту.  

   ![Создание нового задания cron через crontab -e](Screenshot_3.png){ #fig:003 width=80% }

4. После сохранения изменений список заданий был проверен с помощью **crontab -l**.  
   В нём отобразилась добавленная запись.  

   ![Проверка расписания и результатов выполнения задания](Screenshot_4.png){ #fig:004 width=80% }

   В журнале **/var/log/messages** появились записи, подтверждающие выполнение задачи каждую минуту:  
   *This message is written from root cron.*

5. Затем расписание было изменено на  
   **0 */1 * * 1-5 logger This message is written from root cron.**  
   Эта запись означает выполнение задания каждый час, с понедельника по пятницу.  

   ![Изменённая запись crontab](Screenshot_5.png){ #fig:005 width=80% }

6. Для автоматического выполнения скрипта каждый час был создан сценарий **/etc/cron.hourly/eachhour**.  

   ![Создание сценария eachhour в /etc/cron.hourly](Screenshot_6.png){ #fig:006 width=80% }

   Его содержимое:  
   **#!/bin/sh**  
   **logger This message is written at $(date)**  
   После создания скрипт был сделан исполняемым с помощью команды **chmod +x eachhour**.

7. Также был создан файл задания **/etc/cron.d/eachhour** со следующим содержимым:  

   ![Создание задания eachhour в /etc/cron.d](Screenshot_7.png){ #fig:007 width=80% }

   **11 * * * * root logger This message is written from /etc/cron.d**  
   Эта строка означает, что каждые сутки в 11-й минуте каждого часа команда **logger** будет запускаться от имени пользователя **root**.  

8. Для выполнения одноразового задания использовался планировщик **at**.  
   Сначала была проверена работа службы **atd**.  

   ![Проверка статуса службы atd](Screenshot_8.png){ #fig:008 width=80% }

   Она также находится в состоянии **active (running)**.  
   Далее было запланировано задание на определённое время с помощью **at 15:31** и команды **logger message from at**.  
   После чего выполнена проверка очереди заданий **atq** и просмотр журнала сообщений **grep 'from at' /var/log/messages**.  
   В результате в журнале появилась запись: *message from at*, что подтверждает успешное выполнение задания в назначенное время.

   
# Контрольные вопросы

1. Как настроить задание cron, чтобы оно выполнялось раз в 2 недели?  
   Задания cron можно запускать по дням месяца или неделям. Так как напрямую интервал «раз в 2 недели» не поддерживается, используется комбинация проверки дня недели и числа месяца.  
   Пример: **0 0 */14 * * команда** — выполняет задание каждые 14 дней в полночь.

2. Как настроить задание cron, чтобы оно выполнялось 1-го и 15-го числа каждого месяца в 2 часа ночи?  
   **0 2 1,15 * * команда** — запуск каждый месяц 1-го и 15-го числа в 2:00.

3. Как настроить задание cron, чтобы оно выполнялось каждые 2 минуты каждый день?  
   ***/2 * * * * команда** — выполнение каждые 2 минуты независимо от даты и времени суток.

4. Как настроить задание cron, чтобы оно выполнялось 19 сентября ежегодно?  
   **0 0 19 9 * команда** — запуск ежегодно 19 сентября в 00:00.

5. Как настроить задание cron, чтобы оно выполнялось каждый четверг сентября ежегодно?  
   **0 0 * 9 4 команда** — запуск каждого четверга (день недели 4) в сентябре (месяц 9) в 00:00.

6. Какая команда позволяет вам назначить задание cron для пользователя alice? Приведите подтверждающий пример.  
   **crontab -u alice -e** — открыть и отредактировать расписание пользователя **alice**.  
   Пример записи: **0 8 * * * /home/alice/backup.sh** — выполнение скрипта резервного копирования каждый день в 8:00 от имени alice.

7. Как указать, что пользователю bob никогда не разрешено назначать задания через cron? Приведите подтверждающий пример.  
   В файл **/etc/cron.deny** нужно добавить имя пользователя **bob**.  
   Пример:  


# Заключение  

В ходе работы были освоены основные принципы планирования заданий в Linux с использованием утилит **cron** и **at**.  
