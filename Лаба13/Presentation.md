---
marp: true
---

# Защита лабораторной работы №13
 **"Программирование в командном процессоре ОС UNIX. Расширенное программирование"**

author: "Малашенко Марина Владимировна"

- - -

# Цель работы:

Изучить основы программирования в оболочке ОС UNIX. Научиться писать более сложные командные файлы с использованием логических управляющих конструкций и циклов.

- - -

# Ход работы

**1.** Я написала командный файл, реализующий упрощённый механизм семафоров. Командный файл должен в течение некоторого времени t1 дожидаться освобождения ресурса, выдавая об этом сообщение, а дождавшись его освобождения, использовать его в течение некоторого времени t2<>t1, также выдавая информацию о том, что ресурс используется соответствующим командным файлом (процессом)

- - -

**2.** Я реализовала команду man с помощью командного файла. Изучили содержимое каталога ```/usr/share/man/man1```. В нем находятся архивы текстовых файлов, содержащих справку по большинству установленных в системе программ и команд. Каждый архив можно открыть командой less сразу же просмотрев содержимое справки. Командный файл должен получать в виде аргумента команднойстроки название команды и в виде результата выдавать справку об этой команде или сообщение об отсутствии справки, если соответствующего файла нет вкаталоге ```man1```.

- - -

**3.** Используя встроенную переменную $RANDOM, я написала командный файл, генерирующий случайную последовательность букв латинского алфавита. Учтя,что $RANDOM выдаёт псевдослучайные числа в диапазоне от 0 до 32767.

- - -

## Вывод
Я изучила основы программирования в оболочке ОС UNIX, научилась писать более сложные командные файлы с использованием логических управляющих конструкций и циклов.

- - -

## Библиография

- Bash Reference Manual — Перевод man-страницы от 2004 года. Архивировано 23 апреля 2012 года.
- Advanced Bash-Scripting Guide — Расширенное руководство по написанию bash-скриптов. Дата обращения: 6 августа 2011. Архивировано 28 августа 2011 года.
- Частые ошибки программирования на Bash. Дата обращения: 22 ноября 2010. Архивировано 23 августа 2011 года.
- Введение в программирование на bash. Дата обращения: 22 ноября 2010. Архивировано 27 августа 2011 года.
- Описание команд bash (англ.). Дата обращения: 22 ноября 2010. Архивировано 23 августа 2011 года.
- Ян Шилдс (Ian Shields). Полезные советы Linux: Параметры bash и расширения параметров. Архивировано 15 октября 2012 года.



