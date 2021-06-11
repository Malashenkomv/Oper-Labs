---
# Front matter
lang: ru-RU
title: "Отчёт по лабораторной работе №15"
subtitle: "Именованные каналы"
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
---

# Цель работы:
Приобрести практические навыки работы с именованными каналами.

# Теоретическое введние:

Одним из видов взаимодействия между процессами в операционных системах является обмен сообщениями. Под сообщением понимается последовательность байтов, передаваемая от одного процесса другому.

В операционных системах типа UNIX есть 3 вида межпроцессорных взаимодействий: общеюниксные (именованные каналы, сигналы), System V Interface Definition (SVID — разделяемая память, очередь сообщений, семафоры) и BSD (сокеты).

Для передачи данных между неродственными процессами можно использовать **механизм именованных каналов (named pipes)**. Данные передаются по принципу FIFO (First In First Out) (первым записан — первым прочитан), поэтому они называются также FIFO pipes или просто FIFO. Именованные каналы отличаются от неименованных наличием идентификатора канала, который представлен как специальный файл (соответственно имя именованного канала — это имя файла). Поскольку файл находится на локальной файловой системе, данное IPC используется внутри одной системы.

Файлы именованных каналов создаются функцией ``mkfifo(3)``.

```

#include <sys/types.h> 

#include <sys/stat.h>

int mkfifo(const char *pathname, mode_t mode);

```

Первый параметр — имя файла, идентифицирующего канал,второй параметр — маска прав доступа к файлу.

После создания файла канала процессы, участвующие в обмене данными, должны открыть этот файл либо для записи, либо для чтения. При закрытии файла сам канал продолжает существовать. Для того чтобы закрыть сам канал, нужно удалить его файл, например с помощью вызова unlink(2).

Рассмотрим работу именованного канала на примере системы клиент–сервер. Сервер создаёт канал, читает из него текст, посылаемый клиентом, и выводит его на терминал.

Вызов функции ``mkfifo()`` создаёт файл канала (с именем, заданным макросом ``FIFO_NAME``):

``mkfifo(FIFO_NAME, 0600);``

В качестве маски доступа используется восьмеричное значение 0600, разрешающее процессу с аналогичными реквизитами пользователя чтение и запись. Можно также установить права доступа 0666.

Открываем созданный файл для чтения:

``f = fopen(FIFO_NAME, O_RDONLY);``

Ждём сообщение от клиента. Сообщение читаем с помощью функции ``read()`` и печатаем на экран. После этого удаляется файл ``FIFO_NAME`` и сервер прекращает работу.

Клиент открывает ``FIFO`` для записи как обычный файл:

``f = fopen(FIFO_NAME, O_WRONLY);``

Посылаем сообщение серверу с помощью функции ``write()``.
Для создания файла ``FIFO`` можно использовать более общую функцию ``mknod(2)``, предназначенную для создания специальных файлов различных типов (FIFO, сокеты, файлы устройств и обычные файлы для хранения данных).

```

#include <sys/types.h>

#include <sys/stat.h>

#include <fcntl.h> 

#include <unistd.h>

int mknod(const char *pathname, mode_t mode, dev_t dev);

```

Тогда, вместо 

``mkfifo(FIFO_NAME, 0600);``

пишем

``mknod(FIFO_NAME, S_IFIFO | 0600, 0);``

*Каналы представляют собой простое и удобное средство передачи данных, которое, однако, подходит не во всех ситуациях. Например, с помощью каналов довольно трудно организовать обмен асинхронными сообщениями между процессами.*


# Ход работы

**1.** Изучили приведённые в тексте программы ``server.c`` и ``client.c.`` Взяв данные примеры за образец, написали аналогичные программы, внеся следующие изменения:

1.	Работает не 1 клиент, а несколько (например, два).
2.	Клиенты передают текущее время с некоторой периодичностью (например, раз в пять секунд). Используйте функцию sleep() для приостановки работы клиента.
3.	Сервер работает не бесконечно, а прекращает работу через некоторое время (например, 30 сек). Используйте функцию clock() для определения времени работы сервера.


![рис.1 Терминал](screen/1.jpg)

рис.1 Терминал

![рис.2 Файл common.h](screen/2.jpg)

рис.2 Файл common.h

![рис.3 Файл server.c](screen/3.jpg)

рис.3 Файл server.c

![рис.4 Файл client.c](screen/4.jpg)

рис.4 Файл client.c

![рис.5 Файл client2.c](screen/5.jpg)

рис.5 Файл client2.c

- - -

**2.** Создадим Makefile:

![рис.6 Файл makefile](screen/6.jpg)

рис.6 Файл makefile

![рис.7 Команда make (gss1)](screen/7.jpg)

рис.7 Команда make (gss1)

![рис.8 Команда make (gss2)](screen/8.jpg)

рис.8 Команда make (gss2)

- - -

**3.** Приступим к запуску канала: 

Откроем второй терминал

![рис.9 Второй терминал](screen/9.jpg)

рис.9 Второй терминал

Запустим в первом терминале скрипт сервера, а во втором - скрипт клиента

![рис.10 Канал](screen/10.jpg)

рис.10 Канал

Сообщения передевалась с периодичностью в несколько секунд, а по истечении 30 секунд - канал закрылся, и вывелось сообщение об этом.


Что будет в случае, если сервер завершит работу, не закрыв канал?

При завершении программы каналы автоматически закрываются.

- - -

## Вывод
Я приобрела практические навыки работы с именованными каналами.

- - -
## Контрольные вопросы

1.	Именованные каналы отличаются от неименованных наличием идентификатора канала, который представлен как специальный файл (соответственно имя именованного канала — это имя файла).

2.	Создание неименованного канала из командной строки возможно командой pipe.

3.	Создание именованного канала из командной строки возможно с помощью mkfifo.

4.	Функция языка С, создающая неименованный канал:
int read(int pipe_fd, void *area, int cnt); int write(int pipe_fd, void *area, int cnt);
Первый аргумент этих вызовов - дескриптор канала, второй - указатель на область памяти, с которой происходит обмен, третий - количество байт. Оба вызова возвращают число переданных байт (или -1 - при ошибке).

5.	Функция языка С, создающая именованный канал:
int mkfifo (const char *pathname, mode_t mode);
Первый параметр — имя файла, идентифицирующего канал, второй параметр маска прав доступа к файлу. Вызов функции mkfifo() создаёт файл канала (с именем, заданным макросом FIFO_NAME):
mkfifo(FIFO_NAME, 0600);

6.	При чтении меньшего числа байтов, возвращается требуемое число байтов, остаток сохраняется для следующих чтений.
При чтении большего числа байтов, возвращается доступное число байтов 7. Запись числа байтов, меньшего емкости канала или FIFO, гарантированно
атомарно. Это означает, что в случае, когда несколько процессов одновременно записывают в канал, порции данных от этих процессов не перемешиваются.
При записи большего числа байтов, чем это позволяет канал или FIFO, вызов write(2) блокируется до освобождения требуемого места. При этом атомарность операции не гарантируется. Если процесс пытается записать данные в канал, не открытый ни одним процессом на чтение, процессу генерируется сигнал SIGPIPE, а вызов write(2) возвращает 0 с установкой ошибки (errno=ЕР1РЕ) (если процесс не установил обработки сигнала SIGPIPE, производится обработка по умолчанию -- процесс завершается).

8.	Два и более процессов могут читать и записывать в канал.

9.	Функция write записывает length байтов из буфера buffer в файл, определенный дескриптором файла fd. Эта операция чисто 'двоичная' и без буферизации. При единице возвращает действительное число байтов.
Функция write возвращает число действительно записанных в файл байтов или -1 при ошибке, устанавливая при этом errno.

10.	Строковая функция strerror - функция языков C/C++, транслирующая код ошибки, который обычно хранится в глобальной переменной errno, в сообщение об ошибке, понятном человеку.

- - -

## Библиография

- The Linux Programmer’s Guide: Named Pipes: https://tldp.org/LDP/lpg/node15.html

- Linux Journal: Introduction to Named Pipes: https://www.linuxjournal.com/article/2156

- MSDN Library: Named Pipes: https://docs.microsoft.com/ru-ru/windows/win32/ipc/named-pipes?redirectedfrom=MSDN

- Programing with named pipes (from Sun and for Solaris, but a general enough intro for anyone): https://web.archive.org/web/20120626103458/http://developers.sun.com/solaris/articles/named_pipes.html

