---
## Front matter
lang: ru-RU
title: Лабораторная работа №8
subtitle: Планировщики событий
author:
  - Шаханеоядж Хаоладар
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 13 октября 2025

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
---

# Цель работы

## Основная цель

Получение навыков работы с планировщиками событий **cron** и **at** в операционной системе Linux.

# Ход выполнения работы

## Проверка службы cron

![Проверка статуса службы crond](Screenshot_1.png){ #fig:001 width=70% }

## Файл /etc/crontab

![Содержимое файла /etc/crontab](Screenshot_2.png){ #fig:002 width=70% }

## Создание задания через crontab -e

![Создание нового задания cron](Screenshot_3.png){ #fig:003 width=70% }

## Проверка активных заданий cron

![Проверка списка заданий cron](Screenshot_4.png){ #fig:004 width=70% }

## Изменение расписания cron

![Изменённая запись crontab](Screenshot_5.png){ #fig:005 width=70% }

## Создание сценария /etc/cron.hourly/eachhour

![Создание сценария eachhour](Screenshot_6.png){ #fig:006 width=70% }

## Создание задания /etc/cron.d/eachhour

![Создание задания eachhour в /etc/cron.d](Screenshot_7.png){ #fig:007 width=70% }

## Проверка службы atd

![Проверка статуса службы atd](Screenshot_8.png){ #fig:008 width=70% }

# Итоги работы

## Заключение

- Освоены принципы планирования заданий в Linux с помощью **cron** и **at**  
- Получены навыки создания, редактирования и проверки расписаний  
- Изучены способы ограничения доступа пользователей к планировщику  
- Закреплены умения анализа системных журналов для контроля выполнения задач
