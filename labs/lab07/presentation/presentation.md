---
## Front matter
lang: ru-RU
title: Лабораторная работа №7
subtitle: Управление журналами событий в системе
author:
  - Шаханеоядж Хаоладар
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 5 октября 2025

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

Получить навыки работы с журналами мониторинга событий и управления системными логами в Linux.

# Ход выполнения работы

## Мониторинг системных событий

![Мониторинг системных событий в реальном времени](Screenshot_1.png){ #fig:001 width=70% }

## Мониторинг системных событий

![Ошибка при попытке входа с неверным паролем](Screenshot_2.png){ #fig:002 width=70% }

## Мониторинг системных событий

![Сообщение logger hello в системном журнале](Screenshot_3.png){ #fig:003 width=70% }

## Мониторинг системных событий

![Журнал безопасности /var/log/secure](Screenshot_4.png){ #fig:004 width=70% }

## Настройка rsyslog

![Установка и запуск службы httpd](Screenshot_5.png){ #fig:005 width=70% }

## Настройка rsyslog

![Журнал ошибок Apache](Screenshot_6.png){ #fig:006 width=70% }

## Настройка rsyslog

![Добавление строки ErrorLog syslog:local1 в конфигурацию httpd](Screenshot_7.png){ #fig:007 width=70% }

## Настройка rsyslog

![Создание файла конфигурации rsyslog для httpd](Screenshot_8.png){ #fig:008 width=70% }

## Настройка rsyslog

![Создание файла debug.conf для регистрации отладочных сообщений](Screenshot_9.png){ #fig:009 width=70% }

## Настройка rsyslog

![Отображение отладочного сообщения в системном журнале](Screenshot_10.png){ #fig:010 width=70% }

## Использование journalctl

![Просмотр системного журнала с момента последней загрузки](Screenshot_11.png){ #fig:011 width=70% }

## Использование journalctl

![Просмотр возможных параметров фильтрации журнала](Screenshot_12.png){ #fig:012 width=70% }

## Использование journalctl

![Просмотр последних 20 строк журнала](Screenshot_16.png){ #fig:016 width=70% }

## Использование journalctl

![Просмотр сообщений уровня ошибок](Screenshot_17.png){ #fig:017 width=70% }

## Использование journalctl

![Просмотр сообщений со вчерашнего дня](Screenshot_18.png){ #fig:018 width=70% }

## Использование journalctl

![Просмотр сообщений об ошибках со вчерашнего дня](Screenshot_19.png){ #fig:019 width=70% }

## Использование journalctl

![Просмотр журнала службы SSH](Screenshot_20.png){ #fig:020 width=70% }

## Постоянный журнал journald

![Настройка постоянного хранения системного журнала journald](Screenshot_21.png){ #fig:021 width=70% }

# Итоги работы

## Вывод

- Изучена работа с **rsyslog** и **systemd-journald**  
- Настроено постоянное хранение логов  
- Освоен мониторинг и фильтрация событий через **journalctl**  
- Получены навыки анализа системных сообщений Linux
