---
## Front matter
title: "Отчёт по лабораторной работе №5"
subtitle: "Управление системными службами"
author: "Шаханеоядж Хаоладар"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true
toc-depth: 2
lof: true
lot: true
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
    - spelling=modern
    - babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float}
  - \floatplacement{figure}{H}
---

# Цель работы

Получить навыки управления системными службами операционной системы посредством systemd.

# Выполнение

## Управление сервисом vsftpd

1. Для начала была проверена доступность службы **vsftpd** с помощью команды  
   **systemctl status vsftpd**  
   Система вернула сообщение о том, что сервис отсутствует.  

   ![Попытка проверки статуса до установки](Screenshot_23.png){ #fig:001 width=80% }

2. Далее выполнена установка службы Very Secure FTP:  
   **dnf -y install vsftpd**  
   В процессе загрузки и установки пакет `vsftpd` был успешно добавлен в систему.  

   ![Установка пакета vsftpd](Screenshot_24.png){ #fig:002 width=80% }

3. После установки служба была запущена командой  
   **systemctl start vsftpd**  
   Проверка состояния показала, что сервис работает, но при перезапуске ОС автоматически не запускается.  

   ![Запуск и проверка работы vsftpd](Screenshot_25.png){ #fig:003 width=80% }

4. Чтобы добавить сервис в автозагрузку, была использована команда  
   **systemctl enable vsftpd**  
   Теперь статус изменился на `enabled`. Для проверки была выполнена команда **systemctl disable vsftpd**, которая убрала службу из автозагрузки.  

   ![Изменение состояния автозапуска](Screenshot_26.png){ #fig:004 width=80% }

5. Для анализа символических ссылок, отвечающих за запуск сервисов, был выполнен вывод содержимого каталога  
   **ls /etc/systemd/system/multi-user.target.wants/**  
   После включения vsftpd появилась соответствующая символьная ссылка на юнит `/usr/lib/systemd/system/vsftpd.service`.  

   ![Символические ссылки для автозапуска сервисов](Screenshot_27.png){ #fig:005 width=80% }

6. Повторная проверка статуса показала, что состояние службы изменилось с **disabled** на **enabled**, а сервис продолжает работу.  

   ![Повторная проверка статуса vsftpd](Screenshot_28.png){ #fig:006 width=80% }

7. Для анализа зависимостей была выполнена команда  
   **systemctl list-dependencies vsftpd**  
   Также выведен список юнитов, зависящих от данного сервиса, с помощью  
   **systemctl list-dependencies vsftpd --reverse**.  

   ![Анализ зависимостей vsftpd](Screenshot_28.png){ #fig:007 width=80% }

## Конфликты юнитов: firewalld и iptables

1. Сначала были получены полномочия администратора и выполнена установка пакета **iptables**:  
   **dnf -y install iptables\***  

   ![Установка iptables](Screenshot_29.png){ #fig:008 width=80% }

2. Проверка состояния сервисов показала, что **firewalld** активен и включён в автозагрузку, а **iptables** отключён и находится в состоянии inactive:  

   ![Статус firewalld и iptables](Screenshot_30.png){ #fig:009 width=80% }

3. Попытка запуска обоих сервисов показала конфликт: при старте **iptables** служба **firewalld** останавливается. Аналогично, запуск **firewalld** деактивирует **iptables**.  

   ![Запуск firewalld и iptables](Screenshot_31.png){ #fig:010 width=80% }

4. Для анализа конфигурации были просмотрены юнит-файлы:  
   - В `/usr/lib/systemd/system/firewalld.service` явно указан параметр **Conflicts=iptables.service**, что запрещает одновременную работу двух сервисов.  
   - В `/usr/lib/systemd/system/iptables.service` конфликты не описаны.  

   ![Юнит-файл firewalld](Screenshot_32.png){ #fig:011 width=80% }  
   ![Юнит-файл iptables](Screenshot_33.png){ #fig:012 width=80% }

5. Для исключения случайного запуска **iptables** сервис был замаскирован командой  
   **systemctl mask iptables**.  
   В результате создана символьная ссылка `/etc/systemd/system/iptables.service → /dev/null`, что делает невозможным его запуск.  

   ![Маскирование iptables](Screenshot_34.png){ #fig:013 width=80% }

6. Попытка запуска замаскированного сервиса завершилась ошибкой:  
   **Failed to start iptables.service: Unit iptables.service is masked.**  
   Аналогично, при добавлении в автозагрузку система выдала сообщение о том, что юнит замаскирован.  

## Изолируемые цели

1. Получив права администратора, был выполнен переход в каталог `/usr/lib/systemd/system` и поиск целей, которые могут быть изолированы. Для этого использовалась команда  
   **grep Isolate \*.target**  
   В списке присутствуют такие цели, как `multi-user.target`, `graphical.target`, `rescue.target`, `reboot.target`, `poweroff.target` и другие, содержащие строку **AllowIsolate=yes**.  

   ![Список изолируемых целей](Screenshot_34.png){ #fig:014 width=80% }

2. Далее система была переведена в режим восстановления командой  
   **systemctl isolate rescue.target**  
   Для входа потребовался пароль суперпользователя.  

   ![Переход в rescue.target](Screenshot_35.png){ #fig:015 width=80% }

3. Перезапуск системы был выполнен с помощью команды  
   **systemctl isolate reboot.target**  

## Цель по умолчанию

1. Для начала был определён текущий режим загрузки:  
   **systemctl get-default**  
   По умолчанию система загружалась в **graphical.target**.  

2. Для перевода системы в текстовый режим по умолчанию использована команда  
   **systemctl set-default multi-user.target**  
   После перезагрузки ОС загрузилась в консольный режим.  

   ![Установка multi-user.target по умолчанию](Screenshot_36.png){ #fig:016 width=80% }

3. Чтобы вернуть графический режим по умолчанию, была применена команда  
   **systemctl set-default graphical.target**  
   После перезагрузки система снова загрузилась в графическую оболочку.  

   ![Возврат к graphical.target по умолчанию](Screenshot_37.png){ #fig:017 width=80% }

# Контрольные вопросы

1. Что такое юнит (unit)? Приведите примеры.  
   **Юнит (unit)** — это объект, которым управляет systemd. Он описывает ресурсы или службы системы.  
   Примеры:  
   - `sshd.service` — сервис OpenSSH  
   - `multi-user.target` — цель, соответствующая многопользовательскому режиму  
   - `home.mount` — юнит монтирования каталога  

2. Какая команда позволяет вам убедиться, что цель больше не входит в список автоматического запуска при загрузке системы?  
   **systemctl disable имя_юнита** — удаляет юнит из автозагрузки.  
   Для проверки: **systemctl status имя_юнита** или просмотр каталога `/etc/systemd/system/*.wants/`.  

3. Какую команду вы должны использовать для отображения всех сервисных юнитов, которые в настоящее время загружены?  
   **systemctl list-units --type=service**  

4. Как создать потребность (wants) в сервисе?  
   **systemctl enable имя_юнита** — создаёт символьную ссылку в каталоге `*.wants/`, выражая зависимость *wants*.  

5. Как переключить текущее состояние на цель восстановления (rescue target)?  
   **systemctl isolate rescue.target**  

6. Поясните причину получения сообщения о том, что цель не может быть изолирована.  
   Это происходит, если в юнит-файле цели отсутствует строка **AllowIsolate=yes**. Такие цели не предназначены для изоляции.  

7. Вы хотите отключить службу systemd, но, прежде чем сделать это, вы хотите узнать, какие другие юниты зависят от этой службы. Какую команду вы бы использовали?  
   **systemctl list-dependencies имя_юнита --reverse**  

# Заключение

В ходе работы были изучены механизмы управления юнитами systemd, включая установку, запуск, автозагрузку, конфликты и изолируемые цели.
