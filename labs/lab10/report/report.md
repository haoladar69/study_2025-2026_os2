---
## Front matter
title: "Отчёт по лабораторной работе №10"
subtitle: "Основы работы с модулями ядра операционной системы"
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

Получить навыки работы с утилитами управления модулями ядра операционной системы.

# Отчёт по выполнению работы  

## Управление модулями ядра из командной строки  

1. В терминале были получены полномочия администратора с помощью команды `su -`.  

2. Командой `lspci -k` был выведен список устройств и связанных с ними модулей ядра.  
   Среди них: контроллеры **VGA (VMware SVGA II Adapter)**, **Ethernet (Intel PRO/1000 MT)**, **аудио (Intel AC'97)**, **USB**, **SATA** и др.  
   Для каждого устройства указаны активные драйверы (`Kernel driver in use`) и доступные модули (`Kernel modules`).  

   ![Вывод команды lspci -k](Screenshot_1.png){ #fig:001 width=80% }  

3. Список загруженных модулей ядра был просмотрен с помощью команды `lsmod | sort`.  
   Среди активных модулей присутствовали **ahci**, **ata_piix**, **vmwgfx**, **snd_intel8x0**, **e1000**, **isofs**, **loop** и другие.  

   ![Просмотр загруженных модулей ядра](Screenshot_2.png){ #fig:002 width=80% }  

4. Проверка загрузки модуля **ext4** (`lsmod | grep ext4`) показала его отсутствие в памяти.  
   После выполнения команды `modprobe ext4` модуль успешно загрузился, что подтвердилось повторным вызовом `lsmod | grep ext4`.  

   ![Загрузка модуля ext4](Screenshot_3.png){ #fig:003 width=80% }  

5. Команда `modinfo ext4` вывела подробную информацию о модуле: имя, версию, лицензию GPL, авторов, зависимости (`jbd2`, `mbcache`), а также путь к бинарному файлу `/lib/modules/.../fs/ext4/ext4.ko.xz`.  
   У модуля отсутствуют настраиваемые параметры, что указано в выводе.  

6. При попытке выгрузить модуль **ext4** с помощью `modprobe -r ext4` система выдала сообщение об ошибке, так как модуль был задействован.  
   Аналогичная ситуация возникла при попытке выгрузить модуль **xfs** — команда завершилась ошибкой `FATAL: Module xfs is in use`.  

   ![Попытка выгрузки модулей ext4 и xfs](Screenshot_4.png){ #fig:004 width=80% }  

---

## Загрузка модулей ядра с параметрами  

1. Проверка наличия модуля **bluetooth** (`lsmod | grep bluetooth`) показала, что он не был загружен.  
   После выполнения команды `modprobe bluetooth` модуль появился в списке активных.  

2. Информация о модуле, полученная через `modinfo bluetooth`, содержит сведения о версии (2.22), лицензии (GPL), авторе (**Marcel Holtmann**), зависимостях (`rfkill`), а также список параметров:  
   - `disable_esco` — отключение eSCO;  
   - `disable_ertm` — отключение улучшенного режима передачи;  
   - `enable_ecred` — включение улучшенного управления потоком.  

3. После тестирования модуль был успешно выгружен командой `modprobe -r bluetooth`.  

   ![Загрузка и выгрузка модуля bluetooth](Screenshot_5.png){ #fig:005 width=80% }  
   ![Параметры модуля bluetooth](Screenshot_6.png){ #fig:006 width=80% }  

---

## Обновление ядра системы  

1. Проверка версии ядра командой `uname -r` показала использование версии **6.12.0-55.12.1.el10_0.x86_64**.  

2. Список доступных пакетов ядра был выведен командой `dnf list kernel`.  
   Обнаружено обновление до версии **6.12.0-55.37.1.el10_0.x86_64**. 

   ![Обновление ядра и системы](Screenshot_7.png){ #fig:007 width=80% }     

3. Для обновления системы были последовательно выполнены команды:  
   - `dnf upgrade --refresh`  
   - `dnf update kernel`  
   - `dnf update`  

   После установки пакетов обновлённое ядро было добавлено в систему.  

   ![Обновление ядра и системы](Screenshot_8.png){ #fig:008 width=80% }  

4. После перезагрузки команда `uname -r` подтвердила использование нового ядра **6.12.0-55.37.1.el10_0.x86_64**.  
   Команда `hostnamectl` показала, что система работает под управлением **Rocky Linux 10.0 (Red Quartz)** с поддержкой до 2035 года.  

   ![Проверка версии ядра и сведений о системе](Screenshot_9.png){ #fig:009 width=80% }  
   
   
# Контрольные вопросы  

1. Какая команда показывает текущую версию ядра, которая используется на вашей системе?  
   **uname -r** — отображает версию загруженного ядра Linux.  

2. Как можно посмотреть более подробную информацию о текущей версии ядра операционной системы?  
   **hostnamectl** — выводит сведения о системе, включая версию ядра, дистрибутив и архитектуру.  

3. Какая команда показывает список загруженных модулей ядра?  
   **lsmod** — выводит таблицу всех модулей, загруженных в память ядра.  

4. Какая команда позволяет вам определять параметры модуля ядра?  
   **modinfo <имя_модуля>** — показывает информацию о модуле, включая параметры, которые можно задать при его загрузке.  

5. Как выгрузить модуль ядра?  
   **modprobe -r <имя_модуля>** — удаляет модуль из памяти, если он не используется другими процессами или зависимостями.  

6. Что вы можете сделать, если получите сообщение об ошибке при попытке выгрузить модуль ядра?  
   Необходимо убедиться, что модуль не используется, проверить зависимости командой **lsmod**, а при необходимости завершить процессы, использующие данный модуль, или выгрузить зависимые модули.  

7. Как определить, какие параметры модуля ядра поддерживаются?  
   **modinfo <имя_модуля>** — в выводе содержится раздел *parm*, где перечислены доступные параметры и их описание.  

8. Как установить новую версию ядра?  
   Последовательно выполнить команды:  
   - **dnf upgrade --refresh** — обновить репозитории и существующие пакеты.  
   - **dnf update kernel** — установить обновлённую версию ядра.  
   - После установки перезагрузить систему и убедиться, что загружено новое ядро с помощью **uname -r**.  


# Заключение  

Освоены основные приёмы управления модулями ядра и обновления версии ядра в операционной системе **Rocky Linux** с использованием командной строки.  
