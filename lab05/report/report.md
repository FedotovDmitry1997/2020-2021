---
# Front matter
lang: ru-RU
title: "Лабораторная работа №5"
subtitle: "Дискреционное разграничение прав в Linux. Дискреционное разграничение прав в Linux. Исследование влияния дополнительных атрибутов"
author: "Федотов Дмитрий Константинович"

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

Изучение механизмов изменения идентификаторов, применения SetUID- и Sticky-битов. Получение практических навыков работы в консоли с дополнительными атрибутами. Рассмотрение работы механизма смены идентификатора процессов пользователей, а также влияние бита Sticky на запись и удаление файлов. [1]

# Задание

1. Подготовить лабораторный стенд
2. Рассмотреть компиляцию программ
3. Создать программы
4. Исследовать Sticky-бит

# Выполнение лабораторной работы

1. Установил компилятор gcc с помощью команды \texttt{yum install gcc} (рис - @fig:001).

![Установка компилятора gcc](image/1.png){ #fig:001 width=70% }

Отключил систему защиты SELinux с помощью команды \texttt{setenforce 0}. После этого команда \texttt{getenforce} вывела \texttt{Permissive} (рис -@fig:002).

![Отключение системы запретов](image/2.png){ #fig:002 width=70% }

2. Изучил компиляцию программ. Компилятор языка С называется gcc. Компилятор языка С++ называется g++ и запускается с параметрами почти так же, как gcc. Проверил это с поомщью команд \texttt{whereis gcc} и \texttt{whereis g++} (рис -@fig:003).

![Проверка названий компиляторов](image/3.png){ #fig:003 width=70% }

3. Вошел в в систему от имени пользователя \texttt{guest} и создал программу \texttt{simpleid.c} (рис -@fig:004 и рис -@fig:005).

![Создание файла simpleid.c](image/4.png){ #fig:004 width=70% }

![Создание программы simpleid.c](image/5.png){ #fig:005 width=70% }

Скомпилировал программу  (рис -@fig:006)

![Компиляция программы](image/6.png){ #fig:006 width=70% }

Выполнил программу \texttt{simpleid} (рис -@fig:007)

![Выполнение созданной программы](image/7.png){ #fig:007 width=70% }
  
Усложнил программу, добавив вывод действительных идентификаторов (рис -@fig:008)

![Усложнение программы](image/8.png){ #fig:008 width=70% }

Скомпилировал и запустил \texttt{simpleid2.c} (рис -@fig:009)

![Компиляция и запуск файла](image/9.png){ #fig:009 width=70% }

От имени суперпользователя выполнил следующие команды (рис -@fig:010)

![Смена владельца и атрибутов от имени суперпользователя](image/10.png){ #fig:010 width=70% }
 
Запустил \texttt{simpleid2} и \texttt{id} (рис -@fig:011)

![Проверка id пользователя и группы](image/11.png){ #fig:011 width=70% }

Создал программу \texttt{readfile.c} (рис -@fig:012)

![Создание программы \texttt{readfile.c}](image/13.png){ #fig:013 width=70% }

Откомпилировал созданную программу (рис -@fig:013)

![Компиляция программы](image/14.png){ #fig:013 width=70% }

Сменил владельца у файла readfile.c и изменил права так, чтобы только суперпользователь мог прочитать его, а guest не мог (рис -@fig:015)

![Смена владельца и изменение прав файла](image/16.png){ #fig:015 width=70% }

Проверил, что пользователь \texttt{guest} не может прочитать файл \texttt{readfile.c} (рис -@fig:016)

![Попытка прочесть файл](image/17.png){ #fig:016 width=70% }

Сменил у программы \texttt{readfile} владельца и утсановил SetUID-бит (рис -@fig:017)

![Смена владельца и установка SetUID-бита](image/18.png){ #fig:017 width=70% }

Проверил, может ли программа \texttt{readfile} прочитать файл \texttt{readfile.c}. Да, может. (рис -@fig:018)

![Проверка чтения файла](image/19.png){ #fig:018 width=70% }

Проверил, может ли программа \texttt{readfile} прочитать файл \texttt{/etc/shadow}. Да, может. (рис -@fig:019)

![Проверка чтения файла \texttt{/etc/shadow}](image/20.png){ #fig:019 width=70% }

4. Исследовал Sticky-бит  
Выяснил, что атрибут Sticky установлен на директорию \texttt{/tmp}, для чего выполнил команду \texttt{ls -l / | grep tmp} (рис -@fig:020)

![Проверка нахождения атрибута Sticky на директории \texttt{/tmp}](image/21.png){ #fig:020 width=70% }

От имени пользователя \texttt{guest} создал файл \texttt{file01.txt} в директории \texttt{/tmp} со словом \texttt{test} (рис -@fig:021):

![Создание файла и внесение записи в него](image/22.png){ #fig:021 width=70% }

Просмотрел атрибуты у только что созданного файла и разрешил чтение и запись для категории пользователей "все остальные" (рис -@fig:022):

![Просмотр атрибутов файла и установление прав на чтение и запись для категории "все остальные"](image/23.png){ #fig:022 width=70% }

От имени пользователя \texttt{guest2} (не являющегося владельцем) прочитал файл \texttt{/tmp/file01.txt} (рис -@fig:023):

![Чтение файла от имени пользователя \texttt{guest2}](image/24.png){ #fig:023 width=70% }

От имени пользователя \texttt{guest2} дозаписал в файл \texttt{/tmp/file01.txt} слово \texttt{test2} (рис -@fig:024):

![Дозапись слова в файл от имени пользователя \texttt{guest2}](image/25.png){ #fig:024 width=70% }

От имени пользователя \texttt{guest2} попробовал удалить файл \texttt{/tmp/file01.txt} (рис -@fig:025):

![Попытка удаления файла от имени пользователя \texttt{guest2}](image/27.png){ #fig:025 width=70% }

Мне не удалось удалить файл.  

Повысил свои права до суперпользователя и выполнил после этого команду, снимающую атрибут \texttt{t} (Sticky-бит) с директории \texttt{/tmp}(рис -@fig:026):

![Повышение прав до суперпользователя. Снятие атрибута \texttt{t}](image/28.png){ #fig:026 width=70% }

Повторил предыдущие шаги (рис -@fig:029):

![Повтор предыдущих шагов](image/29.png){ #fig:029 width=70% }

Как видно из рисунка, удалось выполнить все команды, которые были рассмотрены выше, включая удаление.  

Повысил свои права до суперпользователя и вернул атрибут \texttt{t} на директорию \texttt{/tmp} (рис -@fig:030):

![Переход в режим суперпользователя и возврат атрибута \texttt{t}](image/30.png){ #fig:030 width=70% }

# Выводы

Изучил механизмы изменения идентификаторов, применения SetUID- и Sticky-битов. Получил практические навыки работы в консоли с дополнительными атрибутами. Рассмотрел работу механизма смены идентификатора процессов пользователей, а также влияние бита Sticky на запись и удаление файлов.

