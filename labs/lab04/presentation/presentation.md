---
## Front matter
lang: ru-RU
title: Лабораторная работа №4
subtitle: Работа с программными пакетами
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

Получение навыков работы с репозиториями, пакетным менеджером **dnf** и утилитой **rpm** в Linux.

# Ход выполнения работы

## Работа с репозиториями

![Каталог /etc/yum.repos.d и файл rocky.repo](Screenshot_1.png){ #fig:001 width=70% }

## Работа с репозиториями

![Список репозиториев](Screenshot_2.png){ #fig:002 width=70% }

## Работа с пакетом nmap

![Информация о пакете nmap](Screenshot_3.png){ #fig:003 width=70% }

## Работа с пакетом nmap

![Установка пакета nmap](Screenshot_4.png){ #fig:004 width=70% }

## Работа с пакетом nmap

![Удаление пакета nmap](Screenshot_5.png){ #fig:005 width=70% }

## Работа с группами пакетов

![Список групп пакетов](Screenshot_6.png){ #fig:006 width=70% }

## Работа с группами пакетов

![Информация о группе RPM Development Tools](Screenshot_7.png){ #fig:007 width=70% }

## Работа с группами пакетов

![Удаление группы RPM Development Tools](Screenshot_8.png){ #fig:008 width=70% }

## История операций dnf

![История dnf и откат действия](Screenshot_9.png){ #fig:009 width=70% }

## Использование rpm (lynx)

![Загрузка пакета lynx](Screenshot_10.png){ #fig:010 width=70% }

## Использование rpm (lynx)

![Поиск и установка lynx](Screenshot_11.png){ #fig:011 width=70% }

## Использование rpm (lynx)

![Информация о пакете lynx](Screenshot_12.png){ #fig:012 width=70% }

## Использование rpm (lynx)

![Документация lynx](Screenshot_13.png){ #fig:013 width=70% }

## Использование rpm (lynx)

![Руководство man lynx](Screenshot_14.png){ #fig:014 width=70% }

## Использование rpm (lynx)

![Запуск lynx](Screenshot_15.png){ #fig:015 width=60% }

## Использование rpm (lynx)

![Конфигурационные файлы lynx](Screenshot_16.png){ #fig:016 width=70% }

## Использование rpm (lynx)

![Удаление lynx](Screenshot_17.png){ #fig:017 width=70% }

## Использование rpm (dnsmasq)

![Установка dnsmasq](Screenshot_18.png){ #fig:018 width=70% }

## Использование rpm (dnsmasq)

![Информация о пакете dnsmasq](Screenshot_19.png){ #fig:019 width=70% }

## Использование rpm (dnsmasq)

![Список файлов и документация dnsmasq](Screenshot_20.png){ #fig:020 width=70% }

## Использование rpm (dnsmasq)

![Man-страница dnsmasq](Screenshot_21.png){ #fig:021 width=70% }

## Использование rpm (dnsmasq)

![Конфигурационные файлы dnsmasq](Screenshot_22.png){ #fig:022 width=70% }

# Итоги работы

## Вывод

- Изучена работа с репозиториями, установкой и удалением пакетов через **dnf**  
- Получены навыки работы с группами пакетов  
- Освоены приёмы установки, анализа и удаления пакетов через **rpm**  
- Сформированы практические умения администрирования ПО в Linux
