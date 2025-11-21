---
## Front matter
lang: ru-RU
title: Лабораторная работа №11
subtitle: Управление загрузкой системы
author:
  - Шаханеоядж Хаоладар
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 27 октября 2025

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

Получить навыки работы с загрузчиком системы **GRUB2**.

# Ход выполнения работы

## Модификация параметров GRUB2

![Редактирование файла /etc/default/grub](Screenshot_1.png){ #fig:001 width=70% }

## Модификация параметров GRUB2

![Меню GRUB с вариантами загрузки Rocky Linux](Screenshot_2.png){ #fig:002 width=70% }

## Модификация параметров GRUB2

![Редактирование строки загрузки с параметром rescue.target](Screenshot_3.png){ #fig:003 width=70% }

## Режим восстановления (rescue mode)

![Работа системы в rescue-режиме](Screenshot_4.png){ #fig:004 width=70% }

## Аварийный режим (emergency mode)

![Редактирование строки загрузки с параметром emergency.target](Screenshot_5.png){ #fig:005 width=70% }

## Аварийный режим (emergency mode)

![Работа системы в emergency-режиме](Screenshot_6.png){ #fig:006 width=70% }

# Сброс пароля root

## Редактирование параметров загрузки

![Добавление параметра rd.break для сброса пароля](Screenshot_7.png){ #fig:007 width=70% }

## Попытка сброса пароля

![Попытка выполнения сброса пароля в initramfs](Screenshot_8.png){ #fig:008 width=70% }

# Итоги работы

## Заключение

В ходе работы были изучены методы модификации параметров загрузчика **GRUB2**, отработка режимов восстановления и аварийной загрузки, а также выполнен сброс пароля пользователя **root**.
