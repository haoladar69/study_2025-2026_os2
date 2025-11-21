---
## Front matter
lang: ru-RU
title: Лабораторная работа №12
subtitle: Настройки сети в Linux
author:
  - Шаханеоядж Хаоладар
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 2 ноября 2025

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

Получение практических навыков настройки сетевых параметров системы с использованием утилит **ip**, **nmcli** и **nmtui** в ОС семейства RHEL.

# Проверка конфигурации сети

## Информация о сетевых интерфейсах

![Вывод команды ip -s link](Screenshot_1.png){ #fig:001 width=70% }

## Адреса интерфейсов

![Вывод ip addr show](Screenshot_2.png){ #fig:002 width=70% }

## Проверка подключения к интернету

![Проверка подключения к интернету](Screenshot_3.png){ #fig:003 width=70% }

## Добавление дополнительного IP-адреса

![Добавление адреса к интерфейсу](Screenshot_4.png){ #fig:004 width=70% }

## Адреса интерфейсов

![Вывод ifconfig](Screenshot_5.png){ #fig:005 width=70% }

## Прослушиваемые порты

![Прослушиваемые порты TCP и UDP](Screenshot_6.png){ #fig:006 width=70% }

## Просмотр и создание соединений

![Просмотр существующих подключений](Screenshot_7.png){ #fig:007 width=70% }

## Создание соединений dhcp и static

![Создание соединений](Screenshot_8.png){ #fig:008 width=70% }

## Переключение между соединениями

![Переключение между DHCP и Static](Screenshot_9.png){ #fig:009 width=70% }

## Изменение параметров static

![Активация статического соединения после изменений](Screenshot_10.png){ #fig:010 width=70% }

## Проверка адресов

![Вывод ip addr после изменений](Screenshot_11.png){ #fig:011 width=70% }

## Просмотр через nmtui

![Просмотр параметров в nmtui](Screenshot_12.png){ #fig:012 width=70% }

## Просмотр через графический интерфейс

![Настройки сети в GUI](Screenshot_14.png){ #fig:013 width=70% }

## Возврат к DHCP

![Переключение на DHCP](Screenshot_15.png){ #fig:014 width=70% }

# Итоги работы

## Вывод

- Освоены утилиты **ip**, **nmcli**, **nmtui**  
- Настроены статические и динамические соединения  
- Изучены DNS и маршрутизация  
- Получены навыки работы с сетевыми профилями и параметрами интерфейсов
