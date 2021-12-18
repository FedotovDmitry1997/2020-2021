---
# Front matter
lang: ru-RU
title: "Лабораторная работа №8"
subtitle: "Элементы криптографии. Шифрование (кодирование) различных исходных текстов одним ключом"
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

Освоить на практике применение режима однократного гаммирования на примере кодирования различных исходных текстов одним ключом.

Ответить на вопросы.

# Выполнение лабораторной работы

1. Написал функцию шифрования, которая определяет вид шифротекста при известном ключе и известных открытых текстах (рис - @fig:001), а также работа данной функции (рис - @fig:002).

![Функция, шифрующая данные](image/1.png){ #fig:001 width=70% }

![Результат работы функции](image/2.png){ #fig:002 width=70% }

2. Написал функцию дешифровки, которая определяет вид одного из текстов, зная вид другого открытого текста и  зашифрованный вид обоих текстов, не используя ключ. (рис - @fig:003). А также представил результаты работы программы (рис - @fig:004).

![Функция, дешифрующая данные](image/3.png){ #fig:003 width=70% }

![Результат работы функции](image/4.png){ #fig:004 width=70% }

# Выводы

Освоил на практике применение режима однократного гаммирования на примере кодирования различных исходных текстов одним ключом.

# Ответы на контрольные вопросы

1. $C_1 \oplus C_2 \oplus + P_1 = P_1 \oplus P_2 \oplus + P_1 = P_2$, где $C_1$ и $C_2$ - шифротексты. Т.е. ключ в данной формуле не используется.
2. При повторном использовании ключа при шифровании текста получим исходное сообщение.  
3. с помощью формулы:
$$C_1 = P_1 \oplus + K$$
$$C_2 = P_2 \oplus + K,$$
где $C_i$ - шифротексты, $P_i$ - открытые тексты, $K$ - единый ключ шифровки  
4. Недостатки шифрования одним ключом двух открытых текстов:
Зная одно сообщение и два шифротекста, можно расшифровать без ключа.  
Зная шаблон сообщений, можно определить те символы сообщения $P_2$, которые находятся на позициях известного шаблона сообщения $P_1$.  
5. Преимущества шифрования одним ключом двух открытых текстов:  
Процесс шифровки и дешифровки становится проще. 
Между двумя компьютерами, удобнее пользоваться одним ключом.

