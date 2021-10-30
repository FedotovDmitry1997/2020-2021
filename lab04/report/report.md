---
# Front matter
lang: ru-RU
title: "Лабораторная работа №4"
subtitle: "Дискреционное разграничение прав в Linux. Расширенные атрибуты"
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

Получение практических навыков работы в консоли с расширенными атрибутами файлов.

# Задание

1. Добавление атрибута а и базовые операции
2. Добавление атрибута i и базовые операции

# Выполнение лабораторной работы

1. От имени пользователя guest определите расширенные атрибуты файла /home/guest/dir1/file1 командой lsattr /home/guest/dir1/file1 (рис -@fig:001).

![Определение расширенных атрибутов файла file1](image/1.png){ #fig:001 width=70% }

Установил командой chmod 600 file1 на файл file1 права, разрешающие чтение и запись для владельца файла (рис -@fig:002).

![Установка прав file1](image/2.png){ #fig:002 width=70% }

Попробовал установить на файл /home/guest/dir1/file1 расширенный атрибут a от имени пользователя guest: chattr +a /home/guest/dir1/file1. Операция не удалась (рис -@fig:003).

![Установка атрибута а на файл file1](image/3.png){ #fig:003 width=70% }

Я повысил свои права с помощью команды su. Установил расширенный атрибут a на файл /home/guest/dir1/file1 от имени суперпользователя: chattr +a /home/guest/dir1/file1 (рис -@fig:004).

![Установка атрибута а на файл file1 с повышенными правами](image/4.png){ #fig:004 width=70% }

Проверил правильность установления атрибута: lsattr /home/guest/dir1/file1 (рис -@fig:005).

![Правильность установления атрибута](image/5.png){ #fig:005 width=70% }

Выполнил дозапись в файл file1 слова «test» командой echo "test" /home/guest/dir1/file1 (рис -@fig:006). 

![Дозапись в файл file1](image/6.png){ #fig:006 width=70% }

Попробовал удалить файл file1 либо стереть имеющуюся в нём информацию командой echo "abcd" > /home/guest/dirl/file1. (рис -@fig:007).

![Удаление файла file1](image/7.png){ #fig:007 width=70% }

Попробовал переименовать файл. Получила отказ (рис -@fig:008).

![Переименование файла file1](image/8.png){ #fig:008 width=70% }

Попробовал с помощью команды chmod 000 file1 установить на файл file1 права, например, запрещающие чтение и запись для владельца файла.(рис -@fig:009).

![Изменение прав файла](image/009.png){ #fig:009 width=70% }

Снял расширенный атрибут a с файла /home/guest/dirl/file1 от имени суперпользователя командой chattr -a /home/guest/dir1/file1 (рис -@fig:010).

![Снятие с директории атрибута а](image/10.png){ #fig:010 width=70% }

Повторил операции, которые мне ранее не удавалось выполнить. Мне удалось дозаписать и перезаписать файл, переименование файла тоже прошло успешно (рис -@fig:011).

![Повторение операций без атрибута а](image/11.png){ #fig:011 width=70% }

2. Заменил атрибут «a» атрибутом «i». 

Установил расширенный атрибут i на файл /home/guest/dir1/file1 от имени суперпользователя: chattr +i /home/guest/dir1/file1 (рис -@fig:012).

![Установка атрибута i на файл file1 с повышенными правами](image/12.png){ #fig:012 width=70% }

Выполнил дозапись в файл file1 слова «test» командой echo "test" /home/guest/dir1/file1.  После этого выполнил чтение файла file1 командой cat /home/guest/dir1/file1. (рис -@fig:013).  

![Дозапись в файл file1](image/13.png){ #fig:013 width=70% }


Попробовал удалить файл file1 либо стереть имеющуюся в нём информацию командой echo "abcd" > /home/guest/dirl/file1. (рис -@fig:014).

![Удаление файла file1](image/14.png){ #fig:014 width=70% }

Попробовал переименовать файл. (рис -@fig:015).

![Переименование файла file1](image/15.png){ #fig:015 width=70% }

Попробовал с помощью команды chmod 000 file1 установить на файл file1 права, например, запрещающие чтение и запись для владельца файла. (рис -@fig:016).

![Изменение прав файла](image/16.png){ #fig:016 width=70% }

# Выводы

В процессе выполнения лабораторной работы 4 я получил практические навыки работы в консоли с расширенными атрибутами файлов.




