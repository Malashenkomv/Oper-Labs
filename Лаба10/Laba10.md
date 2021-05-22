-—
# Front matter
lang: ru-RU
title: **"Отчёт по лабораторной работе №10"**

subtitle: **"Текстовой редактор emacs"**

author: "Малашенко Марина Владимировна"

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
--—
-—



# Цель работы

Познакомиться с операционной системой Linux. Получить практические навы-ки работы с редактором Emacs.



# Ход работы



**1.** Открыли emacs.

![рис.1 Открытие](screen/1.jpg)
![рис.2 Emacs](screen/2.jpg)


**2.** Создали файл lab7.sh. Используя команду ```C-x C-f```.

![рис.3 lab7.sh](screen/3.jpg)


**3.** И внесли текст:
#!/bin/bash
HELL=Hello
function hello {
    LOCAL HELLO=World
    echo $HELLO
    }
    echo $HELLO
    hello

![рис.4 текст](screen/4.jpg)


**4.** Сохранили файл, используя сочетание команд ```C-x C-s```. Проделали с текстом стандартные процедуры редактирования, каждое действие должно осуществляться комбинациейклавиш:
(a) Вырезали одной командой целуюс троку ```С-k```.

![рис.5 Вырезание](screen/5.jpg)

(b) Вставили эту строку в конец файла ```C-y```.

![рис.6 Вставка](screen/6.jpg)

(c) Выделили область текста, команда ```C-space```.

![рис.7 Выделение](screen/7.jpg)

(d) Скопировали область в буфер обмена ```M-w```.
(e) Вставили область в конец файла

![рис.8 Конец файла](screen/8.jpg)

(f) Вновь выделили эту область и вырезали ее ```C-w```.

![рис.9 Вырезание](screen/9.jpg)

(g) Отменили последнее действие ```C-/```.

![рис.10 Отмена](screen/10.jpg)


**5.** Научились использовать команды по перемещению курсора.

(a) Переместим курсор в начало строки ```C-a```.

![рис.11 Начало строки](screen/11.jpg)

(b) Переместили курсор в конец строки ```C-e```.

![рис.12 Конец строки](screen/12.jpg)

(c) Переместили курсор в начало буфера ```M-<```.

![рис.13 Начало буфера](screen/13.jpg)

(d) Переместили курсор в конец буфера ```M->```.

![рис.14 Конец буфера](screen/14.jpg)

**7.** Управление буферами.

(a) Вывели список активных буферов на экран ```C-x C-b```.

![рис.15 Активные буферы](screen/15.jpg)

(b) Переместились в открытое окно ```C-x о``` со списком открытых буферов и переключились на другой буфер.

![рис.16 Другой буфер](screen/16.jpg)

(c) Закрыли это окно ```C-x 0```.

(d) Теперь вновь переключились между буферами, но уже без вывода их списка на экран ```C-x b```.

![рис.17 Переключение](screen/17.jpg)

**8.** Управление окнами. 

(а) Поделили фрейм на 4 части: разделили фрейм на два окна по вертикали ```C-x 3```, а затем каждое из этих окон на две части по горизонтали ```C-x 2```.

![рис.18 2 части](screen/18.jpg)

![рис.19 4 части](screen/19.jpg)

(b) В каждом из четырех созданных окон откроем новый буфер (файл) и введём несколько строк текста.

![рис.20 Текст](screen/20.jpg)

**9.** Режим поиска

(a) Переключились в режимпоиска ```C-s``` и нашли несколько слов, присутствующих в тексте. 

(b) Переключилисьмеждурезультатамипоиска, нажимая ```C-s```.

![рис.21 Результаты поиска](screen/21.jpg)

(c) Вышлиизрежимапоиска, нажав ```C-g```.

![рис.22 Выход](screen/22.jpg)

(d) Перейдём в режим поиска и замены ```M-%```. Ввели текст, который следует найти и заменить, нажали Enter, затем ввели текст для замены.
(Заменили точку на ////)
После того, как будут подсвечены результаты поиска нажали ```!``` для подтверждения замены.

![рис.23 Режим поиска и замены 1](screen/23.jpg)

(e) Испробовали другой режим поиска, нажав ```M-s o```. Он отличается от обычного поиска тем,что переводит курсор на конец найденного слова, а не выделяет его.

![рис.24 Режим поиска и замены 2](screen/24.jpg)




# Вывод
Мы познакомились с операционной системой Linux. Получили практические навыки работы с редактором emacs.



## Ответы на контрольные вопросы
1.	Emacs представляет собой мощный экранный редактор текста, написанный на языке высокого уровня Elisp.
2.	Для работы с emacs используется система меню и комбинаций клавиш. Используются сочетания c клавишами <ctrl> и <meta>. Сложности могут возникнуть так как на клавиатуре для IBM PC совместимых ПК клавиши <meta> нет, то вместо нее можно использовать <alt> или <esc>\verb . Для доступа к системе меню используйте клавишу F10.
3.	В терминологии emacs’а буфер- это область где мы набираем текст, а окно область, которая объединяет открытые буферы.
4.	Можно открыть больше 10 буферов в одном окне.
5.	Создаются по умолчанию при запуске emacs:
% *GNU Emacs* 844 Fundamental *scratch* 191 Lisp Interaction %* *Messages* 5257 Messages 
% *Quail Completions* 0 Fundamental
6.	Клавиши: Ctrl,C,Shift,\,] и <esc>,Ctrl,C Ctrl,Shift,\,]
7.	Разделите фрейм на два окна по вертикали C-x 3, окно на две части по горизонтали C-x 2
8.	В файле Emacs хранятся настройки редактора emacs.
9.	Kнопка backspace( стереть букву ) = функции C-k и ее можно переназначить.
10.	Emacs оказался намного удобнее. В нём больше функций, в нём интересно редактировать информацию.

## Библиография

-Emacs Timeline

-Stallman R. 7. History // EMACS (англ.): The Extensible, Customizable Self-Documenting Display Editor — 1981. — P. 18.

-Emacs 27.1 released. mail-archive.com.

-Bernard S. Greenberg. Multics Emacs: The History, Design and Implementation. Архивировано 29 июня 2013 года.

-GNU Emacs FAQ. Архивировано 29 июня 2013 года.

-Jamie Zawinski. Emacs Timeline.

