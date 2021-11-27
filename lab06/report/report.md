---
# Front matter
lang: ru-RU
title: "Лабораторная работа №6"
subtitle: "Мандатное разграничение прав в Linux"
author: "Дмитрий Константинович Федотов"

# Formatting
toc-title: "Содержание"
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4paper
documentclass: scrreprt
polyglossia-lang: russian
polyglossia-otherlangs: english
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
indent: true
pdf-engine: lualatex
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Развить навыки администрирования ОС Linux. Получить первое практическое знакомство с технологией SELinux. [1]    
Проверить работу SELinx на практике совместно с веб-сервером Apache.

# Задание

1. Подготовить лабораторный стенд и ознакомиться с методическими рекомендациями.
2. С помощью различных примеров ознакомиться с работой SELinux и веб-сервисом Apache.

# Выполнение лабораторной работы

1. Подготовил лабораторный стенд и ознакомился с методическими рекомендациями.  
Предварительно установил веб-сервис Apache с помощью команды \texttt{yum install httpd} (рис - @fig:001).

![Установка Apache](image/1.png){ #fig:001 width=70% }

В конфигурационном файле \texttt{/etc/httpd/httpd.conf} задал параметр ServerName: \texttt{ServerName test.ru}. Это делается для того, чтобы при запуске веб-сервиса не выдавались лишние сообщения об ошибках, не относящихся к лабораторной работе (рис - @fig:002 ).

![Внемение информации в конфигурационный файл](image/2.png){ #fig:002 width=70% }

Также отключил пакетный фильтр (рис - @fig:003).

![Отключение пакетного фильтра](image/3.png){ #fig:003 width=70% }

2. С помощью различных примеров ознакомился с работой SELinux и веб-сервисом Apache.  

Вошел в систему с полученными учетными данными и убедился, что SELinux работает в режиме enforcing политики targeted с помощью команд \texttt{getenforce} и \texttt{sestatus} (рис - @fig:004).

![Проверка режима работы SELinux](image/4.png){ #fig:004 width=70% }

Обралится с помощью браузера к веб-серверу, запущенному на моем компьютере, и убедился, что последний работает с помощью команды \texttt{/etc/rc.d/init.d/httpd status}, предварительно запустив его с помощью команды \texttt{/etc/rc.d/init.d/httpd start} (рис - @fig:005).

![Проверка работы веб-сервера](image/5.png){ #fig:005 width=70% }

Нашел веб-сервер Apache в списке процессов и определил его контекст безопасности с помощью команды \texttt{ps auxZ | grep httpd} (рис - @fig:006).

![Поиск веб-сервера Apache и определение его контекста безопасности](image/6.png){ #fig:006 width=70% }

Посмотрел текущее состояние переключателей SELinux для Apache с помощью команды \texttt{sestatus -b} (рис - @fig:007).

![Ттекущее состояние переключателей SELinux для Apache](image/7.png){ #fig:007 width=70% }

Посмотрел статистику по политике с помощью команды \texttt{seinfo}, а также определил множество пользователей, ролей, типов (рис - @fig:008).

![Статистика по политике](image/8.png){ #fig:008 width=70% }

Определил тип файлов и поддиректорий, находящихся в директории \texttt{/var/www}, с помощью команды \texttt{ls -lZ /var/www} (рис - @fig:009).

![Определение типов файлов и поддиректорий, находящихся в директории \texttt{/var/www}](image/9.png){ #fig:009 width=70% }

Определил тип файлов, находящихся в директории \texttt{/var/www/html} с помощью команды \texttt{ls -lZ /var/www/html} (рис - @fig:010).

![Определение типов файлов и поддиректорий, находящихся в директории \texttt{/var/www/html}](image/10.png){ #fig:010 width=70% }

Консоль ничего не выводит, поскольку дирректория пуста.

Определил круг пользователей, которым разрешено создание файлов в директории \texttt{/var/www/html} (рис - @fig:011).

![Пользователи, которым разрешено создание файлов в директории](image/11.png){ #fig:011 width=70% }

Создал от имени суперпользователя html-файл \texttt{/var/www/html/test.html} следующего содержания (рис - @fig:012):

![html-файл и его содержимое](image/12.png){ #fig:012 width=70% }

Проверил контекст созданного мною файла (рис - @fig:013):

![Контекст html-файл](image/13.png){ #fig:013 width=70% }

Обратился к файлу через веб-сервис, введя в браузере адрес \texttt{http://127.0.0.1/test.html} (рис - @fig:014):

![Обращение к файлу через браузер](image/14.png){ #fig:014 width=70% }

Проверил контекст файла с помощью команды \texttt{ls -Z /var/www/html/test.html} (рис - @fig:015).

![Выяснение контекста файла](image/15.png){ #fig:015 width=70% }

Изменил контекст файла \texttt{/var/www/html/test.html} с httpd_sys_content_t на samba_share_t.

Попробовал еще раз получить доступ к файлу через веб-сервер, введя в браузере адрес \texttt{http://127.0.0.1/test.html}. Получил ошибку (рис - @fig:016).

![Попытка получить доступ к файлу через веб-сервер](image/16.png){ #fig:016 width=70% }

Проанализировал ситуацию. Просмотрел log-файлы веб-сервера Apache, а также посмотрел системный лог-файл с помощью команды \texttt{tail /var/log/messages}.

Попробовал запустить веб-сервер Apache на прослушивание TCP-порта 81. Для этого в файле \texttt{/etc/httpd/httpd.conf} нашел строчку \texttt{Listen 80} и заменил ее на \texttt{Listen 81} (рис - @fig:017).

![Изменение строки файла](image/17.png){ #fig:017 width=70% }

Просмотрел файл /var/log/http/error_log.

Просмотрел файл /var/log/http/access_log.

Просмотрел файл var/log/audit/audit.log.

Выполнил команду semanage port -a -t http_port_t -p tcp 81. После этого проверил список портов командой semanage port -l | grep http_port_t. Убедился, что порт 81 появился в списке.

Вернул контекст httpd_sys_content_t к файлу \texttt{/var/www/html/test.html} с помощью команды chcon -t httpd_sys_content_t /var/www/html/test.htmlэ После этого попробовал получить доступ к файлу через веб-сервер, введя в браузере адрес \texttt{http://127.0.0.1:81/test.html}.

Исправил обратно конфигурационный файл apache, вернув \texttt{Listen 80}.

Попытался удалить привязку http_port_t к 81 порту.

Удалил файл.

# Выводы

Развил навыки администрирования ОС Linux. Получил первое практическое знакомство с технологией SELinux.

Проверил работу SELinx на практике совместно с веб-сервером Apache.

# Список литературы

1. Кулябов Д. С., Королькова А. В., Геворкян М. Н. Информационная безопасность компьютерных сетей. Лабораторная работа № 6. Мандатное разграничение прав в Linux.
