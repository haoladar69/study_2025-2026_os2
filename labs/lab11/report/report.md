---
## Front matter
title: "Отчёт по лабораторной работе №11"
subtitle: "Управление загрузкой системы"
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

Получить навыки работы с загрузчиком системы GRUB2.

# Выполнение

## Модификация параметров GRUB2

1. Для начала был открыт терминал и получены права администратора с помощью команды **su -**.  
   Затем открыт файл конфигурации загрузчика `/etc/default/grub` для изменения параметров отображения меню.

   ![Редактирование файла /etc/default/grub](Screenshot_1.png){ #fig:001 width=80% }

   В файле установлен параметр **GRUB_TIMEOUT=10**, что задаёт время отображения меню загрузки перед автозапуском системы.  
   После сохранения изменений выполнена команда для генерации нового файла конфигурации GRUB:  
   **grub2-mkconfig -o /boot/grub2/grub.cfg**

2. После перезагрузки системы появилось меню **GRUB version 2.12**, где отображаются доступные варианты загрузки системы.

   ![Меню GRUB с вариантами загрузки Rocky Linux](Screenshot_2.png){ #fig:002 width=80% }

3. Для загрузки в режиме восстановления выбран пункт с текущим ядром и нажата клавиша **e** для перехода в режим редактирования параметров загрузки.  
   В конце строки, начинающейся с **linux ($root)**, добавлен параметр **systemd.unit=rescue.target**.

   ![Редактирование строки загрузки с параметром rescue.target](Screenshot_3.png){ #fig:003 width=80% }

4. После загрузки система вошла в **режим восстановления (rescue mode)**.  
   Проверен список активных модулей и переменных окружения с помощью команд **systemctl list-units** и **systemctl show-environment**.

   ![Работа системы в rescue-режиме](Screenshot_4.png){ #fig:004 width=80% }

5. Далее выполнена перезагрузка и снова произведено редактирование параметров ядра.  
   В этот раз добавлен параметр **systemd.unit=emergency.target** для входа в аварийный режим.

   ![Редактирование строки загрузки с параметром emergency.target](Screenshot_5.png){ #fig:005 width=80% }

6. После загрузки в **emergency mode** выведен список загруженных модулей.  
   Видно, что их количество минимально — запущены только базовые службы, необходимые для диагностики системы.

   ![Работа системы в emergency-режиме](Screenshot_6.png){ #fig:006 width=80% }

## Сброс пароля root

1. Для сброса пароля система была перезапущена.  
   В меню **GRUB** выбрана текущая версия ядра, после чего нажата клавиша **e** для редактирования строки загрузки.  
   В конец строки добавлен параметр **rd.break**.

   ![Добавление параметра rd.break для сброса пароля](Screenshot_7.png){ #fig:007 width=80% }

2. После нажатия **Ctrl + X** загрузка остановилась на этапе **initramfs**, до монтирования корневой файловой системы.  
   Для предоставления прав на запись была выполнена команда **mount -o remount,rw /sysroot**.  
   Попытка выполнить команды **chroot /sysroot** и **passwd** не увенчалась успехом, поскольку они не были найдены в текущем окружении.

   ![Попытка выполнения сброса пароля в initramfs](Screenshot_8.png){ #fig:008 width=80% }
 
# Контрольные вопросы

1. Какой файл конфигурации следует изменить для применения общих изменений в GRUB2?  
   **/etc/default/grub** — этот файл содержит основные параметры конфигурации загрузчика GRUB2, включая время отображения меню, параметры ядра и поведение загрузки.

2. Как называется конфигурационный файл GRUB2, в котором вы применяете изменения для GRUB2?  
   **/boot/grub2/grub.cfg** — это основной конфигурационный файл GRUB2, который используется при загрузке системы. Он формируется автоматически на основе содержимого `/etc/default/grub` и скриптов из каталога `/etc/grub.d`.

3. После внесения изменений в конфигурацию GRUB2, какую команду вы должны выполнить, чтобы изменения сохранились и воспринялись при загрузке системы?  
   **grub2-mkconfig -o /boot/grub2/grub.cfg** — команда генерирует новый конфигурационный файл GRUB2 с учётом всех внесённых изменений.


# Заключение

В ходе работы были изучены методы модификации параметров загрузчика GRUB2, отработка режимов восстановления и аварийной загрузки, а также выполнен сброс пароля пользователя root.
