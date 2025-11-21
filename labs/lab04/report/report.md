---
## Front matter
title: "Отчёт по лабораторной работе №4"
subtitle: "Работа с программными пакетами"
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

Получить навыки работы с репозиториями и менеджерами пакетов.

# Выполнение

## Работа с репозиториями

1. Сначала был выполнен переход в режим суперпользователя с помощью команды **su -**.  
   Затем открыт каталог `/etc/yum.repos.d`, где находятся файлы конфигурации репозиториев.  

   ![Содержимое каталога /etc/yum.repos.d и файл rocky.repo](Screenshot_1.png){ #fig:001 width=80% }

   Файл `rocky.repo` содержит описание репозиториев **BaseOS** и **BaseOS-DebugInfo**. Здесь задаются параметры: `mirrorlist`, `baseurl`, ключи GPG и настройки проверки пакетов.  

2. Для проверки доступных репозиториев использовалась команда **dnf repolist**.  
   В результате отображен список:  
   - `BaseOS` — базовые пакеты системы  
   - `AppStream` — дополнительные пакеты приложений  
   - `Extras` — вспомогательные пакеты  

   ![Список репозиториев](Screenshot_2.png){ #fig:002 width=80% }

3. Для поиска пакетов, содержащих слово **user**, применена команда **dnf search user**.  
   На экран был выведен список библиотек и утилит, связанных с пользователями: `libuser`, `usermode`, `xdg-user-dirs` и другие.  

## Работа с пакетом nmap

1. Для начала был выполнен поиск пакета **nmap** с помощью команд **dnf search nmap** и **dnf info nmap**.  
   На экране отображена информация о версии пакета, его назначении (сетевой сканер) и месте хранения в репозитории.  

   ![Информация о пакете nmap](Screenshot_3.png){ #fig:003 width=80% }

2. Далее произведена установка пакета с помощью команд **dnf install nmap** и **dnf install nmap\***.  
   Первая команда устанавливает только пакет **nmap**, а вторая — все пакеты, имена которых начинаются с `nmap` (например, `nmap-ncat`).  

   ![Установка пакета nmap](Screenshot_4.png){ #fig:004 width=80% }

3. Удаление пакета выполнялось командами **dnf remove nmap** и **dnf remove nmap\***.  
   При этом были удалены как сам nmap, так и сопутствующие пакеты (`nmap-ncat`).  

   ![Удаление nmap](Screenshot_5.png){ #fig:005 width=80% }

## Работа с группами пакетов

1. Для получения списка доступных групп использовалась команда **dnf groups list**.  
   На экране появились как установленные, так и доступные группы пакетов (например, `Development Tools`, `Security Tools`, `System Tools`).  

   ![Список групп пакетов](Screenshot_6.png){ #fig:006 width=80% }

2. Получение подробной информации о группе **RPM Development Tools** выполнено командой **dnf groups info "RPM Development Tools"**.  
   Здесь перечислены обязательные (`rpm-build`, `redhat-rpm-config`) и дополнительные пакеты.  

   ![Информация о группе RPM Development Tools](Screenshot_7.png){ #fig:007 width=80% }

3. Установка группы осуществлялась командой **dnf groupinstall "RPM Development Tools"**.  
   Были установлены пакеты `rpmdevtools` и зависимость `python3-argcomplete`.  

4. Удаление группы выполнено с помощью команды **dnf groupremove "RPM Development Tools"**.  
   В результате пакеты были удалены, а место освобождено.  

   ![Удаление группы RPM Development Tools](Screenshot_8.png){ #fig:008 width=80% }

## История операций dnf

1. Для просмотра истории транзакций использовалась команда **dnf history**.  
   Вывод показал все действия: установка, удаление пакетов и групп.  

2. Для отмены последнего (6-го) действия применена команда **dnf history undo 6**.  
   Это позволило восстановить ранее удаленную группу **RPM Development Tools**.  

   ![История dnf и откат действия](Screenshot_9.png){ #fig:009 width=80% }

## Использование rpm

1. Для начала был выполнен поиск и загрузка пакета **lynx**.  
   Команда **dnf list lynx** показала доступность пакета в репозитории, а **dnf install lynx --downloadonly** загрузила его без установки.  

   ![Загрузка пакета lynx](Screenshot_10.png){ #fig:010 width=80% }

2. Чтобы найти каталог, в который был помещен пакет, использовалась команда **find /var/cache/dnf/ -name lynx\***.  
   После этого переход в каталог позволил обнаружить файл `lynx-2.9.0-6.el10.x86_64.rpm`.  

   ![Поиск и установка rpm-пакета lynx](Screenshot_11.png){ #fig:011 width=80% }

3. Установка выполнена вручную командой **rpm -Uhv lynx-2.9.0-6.el10.x86_64.rpm**.  
   После завершения операции проверено расположение исполняемого файла с помощью **which lynx**.  
   Вывод показал путь `/usr/bin/lynx`.  

4. Для определения принадлежности файла к пакету использовалась команда **rpm -qf $(which lynx)**.  
   Дополнительно команда **rpm -qi lynx** вывела подробные сведения о пакете: версия, размер, дата сборки, лицензионная информация и краткое описание.  

   ![Информация о пакете lynx](Screenshot_12.png){ #fig:012 width=80% }

5. Список всех файлов в пакете был получен через **rpm -ql lynx**, а список документации — через **rpm -qd lynx**.  
   Для изучения документации был использован **man lynx**.  

   ![Документация lynx](Screenshot_13.png){ #fig:013 width=80% }  
   ![Руководство man lynx](Screenshot_14.png){ #fig:014 width=80% }

6. Проверка работы программы осуществлялась запуском текстового браузера **lynx**.  
   В качестве примера была открыта стартовая страница Rocky Linux.  

   ![Запуск lynx и отображение сайта](Screenshot_15.png){ #fig:015 width=80% }

7. Для вывода списка конфигурационных файлов применена команда **rpm -qc lynx**.  
   В результате показаны файлы `/etc/lynx.cfg`, `/etc/lynx-site.cfg`, `/etc/lynx.lss`.  

   ![Конфигурационные файлы lynx](Screenshot_16.png){ #fig:016 width=80% }

8. Для просмотра скриптов, выполняемых при установке пакета, использовалась команда **rpm -q --scripts lynx**.  
   Такие скрипты обычно предназначены для выполнения служебных операций: настройки окружения, обновления кэша, пост-установочных действий.  

9. После проверки корректности работы браузер был удалён с помощью команды **rpm -e lynx**.  
   Команда **ls** показала, что пакет удален, но файл rpm остался в каталоге кэша.  

   ![Удаление lynx](Screenshot_17.png){ #fig:017 width=80% }

## Использование rpm для работы с dnsmasq

1. Для начала был выполнен поиск пакета **dnsmasq** командой **dnf list dnsmasq**.  
   Затем произведена его установка через **dnf install dnsmasq**.  
   Расположение исполняемого файла определялось командой **which dnsmasq** — путь оказался `/usr/sbin/dnsmasq`.  

   ![Установка dnsmasq и определение исполняемого файла](Screenshot_18.png){ #fig:018 width=80% }

2. Для определения, какому пакету принадлежит исполняемый файл, использовалась команда **rpm -qf $(which dnsmasq)**.  
   Дополнительно команда **rpm -qi dnsmasq** вывела сведения о пакете: версия, дата сборки, лицензия, URL проекта и краткое описание (легковесный DHCP/DNS сервер).  

   ![Информация о пакете dnsmasq](Screenshot_19.png){ #fig:019 width=80% }

3. Для получения списка всех файлов, входящих в пакет, применена команда **rpm -ql dnsmasq**.  
   Команда **rpm -qd dnsmasq** показала перечень документации.  
   Для изучения возможностей программы использовалась команда **man dnsmasq**.  

   ![Список файлов и документация dnsmasq](Screenshot_20.png){ #fig:020 width=80% }  
   ![Man-страница dnsmasq](Screenshot_21.png){ #fig:021 width=80% }

4. Для просмотра конфигурационных файлов пакета использовалась команда **rpm -qc dnsmasq**.  
   В выводе отображены файлы `/etc/dnsmasq.conf`, `/etc/dnsmasq.d` и конфигурации для systemd.  

   ![Конфигурационные файлы dnsmasq](Screenshot_22.png){ #fig:022 width=80% }

5. С помощью команды **rpm -q --scripts dnsmasq** был выведен список установочных скриптов.  
   В пакете присутствуют:
   - **preinstall** — создание системной группы и пользователя `dnsmasq`;  
   - **postinstall** — регистрация службы `dnsmasq.service` в systemd;  
   - **preuninstall** и **postuninstall** — удаление службы при деинсталляции.  

   Эти скрипты обеспечивают корректное добавление/удаление службы и учетных записей при работе пакета.  

6. После проверки работы сервиса пакет был удален с помощью команды **rpm -e dnsmasq**.  

  
   
# Контрольные вопросы

1. Какая команда позволяет вам искать пакет rpm, содержащий файл useradd?  
   **rpm -qf /usr/sbin/useradd** — если файл уже установлен.  
   **dnf provides */useradd** или **repoquery -f */useradd** — если нужно найти пакет, в который входит этот файл.

2. Какие команды вам нужно использовать, чтобы показать имя группы dnf, которая содержит инструменты безопасности и показать, что находится в этой группе?  
   - **dnf group list** — список всех групп.  
   - **dnf group info "Security Tools"** — подробности о содержимом группы.

3. Какая команда позволяет вам установить rpm, который вы загрузили из Интернета и который не находится в репозиториях?  
   **rpm -Uhv имя_пакета.rpm**  
   (или с проверкой зависимостей: **dnf install ./имя_пакета.rpm**).

4. Вы хотите убедиться, что пакет rpm, который вы загрузили, не содержит никакого опасного кода сценария. Какая команда позволяет это сделать?  
   **rpm -qp --scripts имя_пакета.rpm** — показывает скрипты, которые выполняются при установке/удалении.

5. Какая команда показывает всю документацию в rpm?  
   **rpm -qd имя_пакета**  

6. Какая команда показывает, какому пакету rpm принадлежит файл?  
   **rpm -qf /путь/к/файлу**


# Заключение  

Освоены базовые навыки работы с пакетным менеджером **dnf** и утилитой **rpm** для установки, поиска, изучения и удаления пакетов и групп в Linux.  
