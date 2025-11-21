---
## Front matter
lang: ru-RU
title: Лабораторная работа №10
subtitle: Основы работы с модулями ядра операционной системы
author:
  - Шаханеоядж Хаоладар
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 23 октября 2025

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

Получение практических навыков управления модулями ядра, их загрузки, выгрузки и обновления ядра в операционной системе **Rocky Linux**.

# Ход выполнения работы

## Управление модулями ядра

![Список устройств и модулей ядра (lspci -k)](Screenshot_1.png){ #fig:001 width=70% }

## Управление модулями ядра

![Просмотр загруженных модулей ядра (lsmod)](Screenshot_2.png){ #fig:002 width=70% }

## Управление модулями ядра

![Загрузка модуля ext4](Screenshot_3.png){ #fig:003 width=70% }

## Управление модулями ядра

![Попытка выгрузки модулей ext4 и xfs](Screenshot_4.png){ #fig:004 width=70% }

## Проверка и загрузка модуля bluetooth

![Загрузка и выгрузка модуля bluetooth](Screenshot_5.png){ #fig:005 width=70% }

## Проверка параметров модуля bluetooth

![Информация о параметрах bluetooth](Screenshot_6.png){ #fig:006 width=70% }


## Проверка и обновление ядра

![Список пакетов ядра и обновление системы](Screenshot_7.png){ #fig:007 width=70% }

## Завершение обновления и проверка версии

![Проверка версии ядра после обновления](Screenshot_9.png){ #fig:008 width=70% }

# Итоги работы

## Вывод

- Освоены команды управления модулями ядра (`lsmod`, `modprobe`, `modinfo`)  
- Получены навыки загрузки и выгрузки модулей с параметрами  
- Изучен процесс обновления ядра ОС **Rocky Linux**  
- Закреплены практические приёмы администрирования системы
