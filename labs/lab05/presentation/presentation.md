---
## Front matter
lang: ru-RU
title: Лабораторная работа №5
subtitle: Управление системными службами
author:
  - Шаханеоядж Хаоладар
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 24 сентября 2025

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

Получить навыки управления системными службами операционной системы посредством **systemd**.

# Ход выполнения работы

## Управление сервисом vsftpd

![Проверка статуса до установки](Screenshot_23.png){ #fig:001 width=70% }

## Управление сервисом vsftpd

![Установка пакета vsftpd](Screenshot_24.png){ #fig:002 width=70% }

## Управление сервисом vsftpd

![Запуск и проверка работы vsftpd](Screenshot_25.png){ #fig:003 width=70% }

## Управление сервисом vsftpd

![Изменение состояния автозапуска](Screenshot_26.png){ #fig:004 width=70% }

## Управление сервисом vsftpd

![Символические ссылки для автозапуска](Screenshot_27.png){ #fig:005 width=70% }

## Управление сервисом vsftpd

![Повторная проверка статуса vsftpd](Screenshot_28.png){ #fig:006 width=70% }

# Ход выполнения работы

## Конфликты юнитов: firewalld и iptables

![Установка iptables](Screenshot_29.png){ #fig:007 width=70% }

## Конфликты юнитов: firewalld и iptables

![Статус firewalld и iptables](Screenshot_30.png){ #fig:008 width=70% }

## Конфликты юнитов: firewalld и iptables

![Запуск firewalld и iptables](Screenshot_31.png){ #fig:009 width=70% }

## Конфликты юнитов: firewalld и iptables

![Юнит-файл firewalld](Screenshot_32.png){ #fig:010 width=70% }

## Конфликты юнитов: firewalld и iptables

![Юнит-файл iptables](Screenshot_33.png){ #fig:011 width=70% }

## Конфликты юнитов: firewalld и iptables

![Маскирование iptables](Screenshot_34.png){ #fig:012 width=70% }

# Ход выполнения работы

## Изолируемые цели

![Список изолируемых целей](Screenshot_34.png){ #fig:013 width=70% }

## Изолируемые цели

![Переход в rescue.target](Screenshot_35.png){ #fig:014 width=70% }

## Изолируемые цели

![Перезапуск системы через reboot.target](Screenshot_36.png){ #fig:015 width=70% }

# Ход выполнения работы

## Цель по умолчанию

![Проверка цели по умолчанию](Screenshot_37.png){ #fig:016 width=70% }

## Цель по умолчанию

![Установка multi-user.target по умолчанию](Screenshot_36.png){ #fig:017 width=70% }

## Цель по умолчанию

![Возврат к graphical.target по умолчанию](Screenshot_37.png){ #fig:018 width=70% }

# Итоги работы

## Вывод

- Получены навыки управления сервисами через **systemctl**  
- Изучены конфликты юнитов и способы их разрешения  
- Освоены принципы работы с изолируемыми целями  
- Научились изменять цель загрузки по умолчанию  
- Сформированы практические умения администрирования systemd
