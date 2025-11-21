---
## Front matter
lang: ru-RU
title: Лабораторная работа №13
subtitle: Фильтр пакетов (firewalld)
author:
  - Шаханеоядж Хаоладар
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 2025

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
Получить навыки настройки пакетного фильтра в Linux с помощью **firewall-cmd** и **firewall-config**.

# Ход выполнения работы

## Определение активной зоны

![Список сервисов](Screenshot_1.png){width=70%}

## Просмотр параметров зоны

![Просмотр параметров зоны](Screenshot_2.png){width=70%}

## Добавление сервиса (runtime)

![Добавление VNC](Screenshot_3.png){width=70%}

## Добавление сервиса (permanent)

![Permanent добавление](Screenshot_4.png){width=70%}

## Добавление порта

![Добавление порта](Screenshot_5.png){width=70%}

## Выбор режима конфигурации

![Добавление через GUI](Screenshot_6.png){width=70%}

## Добавление порта через GUI

![Порт UDP](Screenshot_7.png){width=70%}

## Применение конфигурации

![Примененные изменения](Screenshot_8.png){width=70%}

## Добавление служб

![Итоговая конфигурация](Screenshot_9.png){width=70%}

# Итоги работы

## Вывод

- Изучено управление брандмауэром через **firewall-cmd** и **firewall-config**
- Получены навыки добавления сервисов и портов
- Освоено применение временных и постоянных правил
- Выполнено управление зонами и интерфейсами в Linux

