-—
# Front matter
lang: ru-RU
title: **"Отчёт по лабораторной работе №7"**

subtitle: **"Поиск файлов. Перенаправление ввода-вывода. Просмотр запущенных процессов"**

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

Ознакомление с инструментами поиска файлов и фильтрации
текстовых данных. Приобретение практических навыков: по управлению процессами (и заданиями), по проверке использования диска и обслуживанию файловых систем.



# Ход работы

**1.** Вошла в систему

**2.** Запишем в файл file.txt названия файлов, содержащихся в каталоге /etc(используем команду ls /etc > file.txt).
Допишем в этот же файл названия файлов, содержащихся в нашем домашнем каталоге. Использовали программу ls >> file.txt

![рис.1 file](screen/1.jpg)


**3.** Выведем имена всех файлов из file.txt имеющих расширение .conf, использовав команду
grep .conf file.txt
Затем запишем их в новый текстовой файл conf.txt.

![рис.2 conf](screen/2.jpg)

**4.**	Определим, какие файлы в нашем домашнем каталоге имеют имена, начинавшиеся с символа c.

![рис.3 grep c*](screen/3.jpg)


**5.** Выведем на экран имена файлов из каталога /etc, начинающиеся с символа h. Используем команду find /etc -name 'h*' -print | more

![рис.4 name 'h*'](screen/4.jpg)


**6.** Запустим в фоновом режиме процесс, который будет записывать в файл ~/logfile файлы, имена которых начинаются с log. Используем команду find ~ -name "log*" -print > logfile
 
**7.** Удалим файл ~/logfile, используя команду rm -i ~/logfile

![рис.5 удаление](screen/5.jpg)

**8.** Запустим в фоновом режиме редактор gedit, используя команду gedit &.

**9.** Определим идентификатор процесса gedit используя команду ps, конвейер и фильтр grep.
Использовали команду ps axu | grep gedit

![рис.6 gedit](screen/6.jpg)

**10.** Прочтём справку (man) команды kill

![рис.7 справка](screen/7.jpg)

после чего используем ее для завершения процесса gedit

![рис.8 kill](screen/8.jpg)

**11.** Предварительно получив более подробную информацию о командах df и du, с помощью команды man, выполним их.

![рис.9 df](screen/9.jpg)

![рис.10 du](screen/10.jpg)

**12.** Воспользовавшись справкой команды find выведем имена всех директорий, имеющихся в нашем домашнем каталоге. Для этого используем команду find -type d

![рис.11 find](screen/11.jpg)






# Вывод
Я ознакомилась с инструментами поиска файлов и фильтрации текстовых данных. А также приобрела практические навыки: по управлению процессами (и заданиями), по проверке использования диска и обслуживанию файловых систем.



## Ответы на контрольные вопросы
*1. Какие потоки ввода вывода вы знаете*

**Ответ:** 1.	– stdin — стандартный поток ввода (клавиатура),

–	stdout — стандартный поток вывода (консоль),

–	stderr — стандартный поток вывод сообщений об ошибках на экран


*2. Объясните разницу между операцией > и >>.*

**Ответ:** Символ < используется для переназначения стандартного ввода команды.
Символ >> используется для присоединения данных в конец файла стандартного вывода команды(файл открывается в режиме добавления)


*3. Что такое конвейер?*

**Ответ:** Конвейер - способ связи между двумя программами.Конвейер (pipe) служит для объединения простых команд или утилит в цепочки, в которых результат работы предыдущей команды передается последующей. Синтаксис следующий: команда1 | команда 2

*4. Что такое PID и GID?*

**Ответ:** Process ID(PID) - идентификатор порожденного процесса. Group ID (GID-идентификация группы пользователей.

*5. Что такое процесс? Чем это понятие отличается от программы??*

**Ответ:**	Процесс - это программа, которая выполняется в отдельном виртуальном адресном пространстве. Когда пользователь регистрируется в системе, автоматически создается процесс, в котором выполняется оболочка (shell), например, /bin/bash.
Компьютерная программа сама по себе — это только пассивная совокупность инструкций, в то время как процесс — это непосредственное выполнение этих инструкций.


*6. Что такое задачи и какая команда позволяет ими управлять?*

**Ответ:** Запущенные фоном программы называются задачами (jobs). Ими можно управлять с помощью команды jobs, которая выводит список запущенных в данный момент задач. Для завершения задачи необходимо выполнить команду :
kill %номер задачи
