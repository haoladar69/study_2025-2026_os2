---
## Front matter
lang: ru-RU
title: Лабораторная работа №9
subtitle: Управление SELinux
author:
  - Шаханеоядж Хаоладар
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 16 октября 2025

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

Получить навыки работы с контекстом безопасности и политиками **SELinux**.

# Ход выполнения работы

## Управление режимами SELinux

![Проверка статуса SELinux](Screenshot_1.png){ #fig:001 width=70% }

## Управление режимами SELinux

![Переключение режима SELinux в Permissive](Screenshot_2.png){ #fig:002 width=70% }

## Управление режимами SELinux

![Редактирование конфигурационного файла SELinux](Screenshot_3.png){ #fig:003 width=70% }

## Управление режимами SELinux

![Проверка отключения SELinux](Screenshot_4.png){ #fig:004 width=70% }

## Управление режимами SELinux

![Сообщение о необходимости relabeling](Screenshot_5.png){ #fig:005 width=70% }

## Управление режимами SELinux

![Повторная проверка SELinux после relabeling](Screenshot_6.png){ #fig:006 width=70% }

## Восстановление контекста безопасности

![Проверка и исправление контекста файла hosts](Screenshot_7.png){ #fig:007 width=70% }

## Восстановление контекста безопасности

![Процесс relabeling SELinux при загрузке](Screenshot_8.png){ #fig:008 width=70% }

## Изменение DocumentRoot и прав доступа

![Настройка Apache: изменение каталога веб-сервера](Screenshot_9.png){ #fig:009 width=70% }

## Настройка контекста безопасности веб-сервера

![Стандартная страница Apache при первом запуске](Screenshot_10.png){ #fig:010 width=70% }

## Настройка контекста безопасности веб-сервера

![Применение контекста httpd_sys_content_t](Screenshot_11.png){ #fig:011 width=70% }

## Настройка контекста безопасности веб-сервера

![Отображение пользовательской страницы веб-сервера](Screenshot_12.png){ #fig:012 width=70% }

## Переключатели службы FTP

![Просмотр и изменение переключателей SELinux](Screenshot_13.png){ #fig:013 width=70% }

# Итоги работы

## Заключение

Изучены режимы работы **SELinux**, способы их переключения и восстановление контекстов безопасности.  
Освоены приёмы настройки политик, работы с веб-каталогами и управления переключателями SELinux.
