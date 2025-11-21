---
## Front matter
title: "Отчёт по лабораторной работе №13"
subtitle: "Фильтр пакетов"
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

Получить навыки настройки пакетного фильтра в Linux.

# Выполнение

## Управление брандмауэром с помощью firewall-cmd

1. Получены привилегии администратора с помощью команды `su -`.

2. Определена зона, активная по умолчанию. Вывод показал, что используется зона **public**.  

3. Просмотрены все зоны, доступные в firewalld.  

4. Отображён перечень доступных сервисов, поддерживаемых брандмауэром.  
   ![Список доступных сервисов](Screenshot_1.png){ #fig:001 width=80% }

5. Проверены службы, уже разрешённые в активной зоне.  

6. Выполнено сравнение вывода двух команд: `firewall-cmd --list-all` и `firewall-cmd --list-all --zone=public`.  
   Оба результата совпали, что подтверждает: активная зона — **public**.  
   ![Просмотр параметров зоны public](Screenshot_2.png){ #fig:002 width=80% }

7. Временное добавление сервиса `vnc-server` в конфигурацию брандмауэра.  
   ![Добавление сервиса VNC](Screenshot_3.png){ #fig:003 width=80% }

8. Выполнена проверка — сервис появился в списке разрешённых.  

9. Служба firewalld была перезапущена. После перезапуска сервис `vnc-server` исчез.

10. Причина: ранее сервис был добавлен только во время выполнения, а конфигурация не была сохранена как постоянная.

11. Повторное добавление `vnc-server`, теперь в постоянную конфигурацию.  
    ![Добавление сервиса permanent](Screenshot_4.png){ #fig:004 width=80% }

12. Проверка конфигурации показывает, что сервис пока отсутствует — изменения сохранены на диск, но не активированы.

13. Выполнена перезагрузка конфигурации. После этого `vnc-server` стал активным.  

14. В конфигурацию добавлен порт `2022/tcp` как постоянное правило. После перезагрузки конфигурации порт появился в списке.  
    ![Добавление порта 2022](Screenshot_5.png){ #fig:005 width=80% }


## Управление с помощью графического интерфейса firewall-config

1. Запущено приложение `firewall-config`.

2. В параметре *Configuration* выбрано значение **Permanent**, чтобы сохранить изменения на постоянной основе.

3. В зоне **public** включены службы `http`, `https`, `ftp`.  
   ![Добавление служб в GUI](Screenshot_6.png){ #fig:006 width=80% }

4. На вкладке **Ports** добавлен порт `2022` с протоколом `udp`.  
   ![Добавление порта UDP через GUI](Screenshot_7.png){ #fig:007 width=80% }

5. После закрытия утилиты изменения были сохранены, но не применены к текущему состоянию.

6. Для применения изменений выполнена перезагрузка конфигурации. После этого они стали активны.  
   ![Применённая конфигурация](Screenshot_8.png){ #fig:008 width=80% }

## Самостоятельная работа

1. Настроена конфигурация межсетевого экрана, разрешающая доступ к службам:
   - telnet  
   - imap  
   - pop3  
   - smtp

2. Служба `telnet` добавлена через командную строку. Сервисы `imap`, `pop3`, `smtp` включены через `firewall-config`.

3. После выполнения `firewall-cmd --reload` конфигурация стала активной. В списке сервисов появились требуемые службы.  
   ![Итоговая конфигурация](Screenshot_9.png){ #fig:009 width=80% }
   
# Контрольные вопросы

1. Какая служба должна быть запущена перед началом работы с менеджером конфигурации брандмауэра firewall-config?  
   **firewalld.service** — именно эта служба должна быть активна для работы firewall-config.

2. Какая команда позволяет добавить UDP-порт 2355 в конфигурацию брандмауэра в зоне по умолчанию?  
   **firewall-cmd --add-port=2355/udp** — временно (runtime)  
   **firewall-cmd --add-port=2355/udp --permanent** — в постоянную конфигурацию

3. Какая команда позволяет показать всю конфигурацию брандмауэра во всех зонах?  
   **firewall-cmd --list-all-zones**

4. Какая команда позволяет удалить службу vnc-server из текущей конфигурации брандмауэра?  
   **firewall-cmd --remove-service=vnc-server**

5. Какая команда firewall-cmd позволяет активировать новую конфигурацию, добавленную опцией --permanent?  
   **firewall-cmd --reload**

6. Какой параметр firewall-cmd позволяет проверить, что новая конфигурация была добавлена в текущую зону и теперь активна?  
   **firewall-cmd --list-all**

7. Какая команда позволяет добавить интерфейс eno1 в зону public?  
   **firewall-cmd --zone=public --add-interface=eno1**

8. Если добавить новый интерфейс в конфигурацию брандмауэра, пока не указана зона, в какую зону он будет добавлен?  
   В **зону по умо**

# Заключение

В ходе работы освоено управление брандмауэром с использованием **firewall-cmd** и **firewall-config**. На практике выполнено добавление сервисов и портов, применение временных и постоянных правил, а также управление зонами и интерфейсами. Получены навыки работы как с командной строкой, так и с графическим интерфейсом настройки межсетевого экрана.
