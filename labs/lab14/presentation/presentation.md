---
## Front matter
lang: ru-RU
title: Лабораторная работа №14
subtitle: Партиции, файловые системы и монтирование
author:
  - Шаханеоядж Хаоладар
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 14 ноября 2025

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

Освоение создания разделов MBR и GPT, работы с файловыми системами и навыков монтирования (вручную и через `/etc/fstab`).

# Выполнение работы

## Просмотр дисков

![Просмотр всех дисков](Screenshot_1.png){ #fig:001 width=70% }

## Работа с fdisk

![Справка по командам fdisk](Screenshot_2.png){ #fig:002 width=70% }

## Работа с fdisk

![Создание основного раздела](Screenshot_3.png){ #fig:003 width=70% }

## Проверка изменений

![Проверка разделов](Screenshot_4.png){ #fig:004 width=70% }

## Создание extended + logical

![Создание расширенного и логического разделов](Screenshot_5.png){ #fig:005 width=70% }

## Проверка структуры

![Проверка разделов](Screenshot_6.png){ #fig:006 width=70% }

## Формирование и включение swap

![Создание разделов](Screenshot_7.png){ #fig:007 width=70% }

## Формирование и включение swap

![Активация swap](Screenshot_8.png){ #fig:008 width=70% }

## Создание GPT структур

![Создание GPT-раздела](Screenshot_9.png){ #fig:009 width=70% }

## Проверка после partprobe

![Проверка диска после partprobe](Screenshot_10.png){ #fig:010 width=70% }

## Создание XFS и EXT4

![Создание XFS и Создание EXT4](Screenshot_11.png){ #fig:011 width=70% }

## Временное монтирование EXT4

![Монтирование и вывод blkid](Screenshot_12.png){ #fig:012 width=70% }

## Автоматическое монтирование

![Редактирование /etc/fstab](Screenshot_13.png){ #fig:013 width=70% }

## Проверка результата

![Результат автоматического монтирования](Screenshot_14.png){ #fig:014 width=70% }

# Самостоятельная работа

## Создание двух GPT-разделов

![Создание раздела и изменение его типа](Screenshot_15.png){ #fig:015 width=70% }

## Форматирование и настройка swap

![Форматирование ext4 и создание swap](Screenshot_16.png){ #fig:016 width=70% }

## Настройка fstab

![Настройка /etc/fstab](Screenshot_17.png){ #fig:017 width=70% }

## Проверка монтирования и swap

![Проверка монтирования и swap](Screenshot_18.png){ #fig:018 width=70% }

# Итоги работы

## Выводы

- Освоены инструменты **fdisk** и **gdisk**
- Получены навыки разметки MBR и GPT
- Отработано создание файловых систем **XFS** и **EXT4**
- Настроено пространство подкачки **swap**
- Выполнено ручное и автоматическое монтирование файловых систем через `/etc/fstab`
