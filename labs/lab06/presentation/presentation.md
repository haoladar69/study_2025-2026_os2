---
## Front matter
lang: ru-RU
title: Лабораторная работа №6
subtitle: Управление процессами
author:
  - Шаханеоядж Хаоладар
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 29 сентября 2025

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

Получение навыков управления заданиями и процессами в операционной системе Linux.

# Ход выполнения работы

## Управление заданиями

![Продолжение выполнения job в фоне](Screenshot_1.png){ #fig:001 width=70% }

## Управление заданиями

![Перевод процессов на передний план и завершение](Screenshot_2.png){ #fig:002 width=70% }

## Управление заданиями

![Фоновый процесс в другом терминале](Screenshot_3.png){ #fig:003 width=70% }

## Управление заданиями

![Просмотр процессов через top](Screenshot_4.png){ #fig:004 width=70% }

## Управление заданиями

![Завершение процесса dd через top](Screenshot_5.png){ #fig:005 width=70% }

## Управление процессами

![Запуск фоновых процессов dd](Screenshot_6.png){ #fig:006 width=70% }

## Управление процессами

![Завершение процессов через kill](Screenshot_7.png){ #fig:007 width=70% }

## Задание 1

![Изменение приоритета процесса](Screenshot_8.png){ #fig:008 width=70% }

## Задание 2

![Работа yes на переднем плане и завершение](Screenshot_9.png){ #fig:009 width=70% }

## Задание 2

![Перевод процесса на передний план](Screenshot_10.png){ #fig:010 width=70% }

## Задание 2

![Вывод top с процессами yes](Screenshot_11.png){ #fig:011 width=70% }

## Задание 2

![Завершение процессов по PID и job ID](Screenshot_12.png){ #fig:012 width=70% }

## Задание 2

![Сравнение приоритетов процессов](Screenshot_13.png){ #fig:013 width=70% }

# Итоги работы

## Вывод

- Получены навыки управления заданиями в Linux (**jobs, fg, bg**)  
- Освоены приёмы завершения процессов (**kill, killall, top**)  
- Изучены механизмы изменения приоритета процессов (**nice, renice**)  
- На практике проверены особенности сигналов и работы с nohup  
- Сформированы базовые умения администрирования процессов в Linux
