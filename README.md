# snow-crash
Проект для знакомства с основами кибернетической безопасности

> Проект [School21](https://21-school.ru/)


## Краткое описание задачи

Дана виртуальная машина, в которой 15 уровней.
На каждом уровне нужно найти флаг, который является паролем для перехода на следующий уровень.

## Решение

### level00

В полном описании задания была дана подсказка для флага первого уровня. Звучит она так:

```
FIND this first file who can run only as flag00...
```

Не мудрствуя лукаво находим такие файлы
![](img/level00_1.png)

Видим набор букв... явно шифр... очень похож на шифр Цезаря. Привет декодер
![](img/level00_2.png)

С ключом 15 получился адекватный набор слов `nottoohardhere`, так что берем его

Пароль подходит, переходим дальше
![](img/level00_3.png)

### level01

Итак. Что мы поняли на предыдущем уровне?
Флаги представляют из себя unix пользователя


На текущем уровне ни команда `ls`, ни `find` не дает результатов.
Поэтому я решил заглянуть в файл, где хранятся пароли от всех пользователей `/etc/passwd`.

![](img/level01_1.png)
![](img/level01_2.png)

Видим хеш пароля `42hDRfypTqqnwz`.
В описании проекта так же были перечислены утилиты, которые нам могут потребоваться. Среди них утилита __John the Ripper__ (https://github.com/openwall/john)

Сохраняем результат предыдущей команды в отдельный файл на своей машине и спускаем Джона с поводка
![](img/level01_3.png)

`42hDRfypTqqnw` -> `abcdefg`

Добро пожаловать на level02!

![](img/level01_4.png)

### level02

В этот раз команда `ls` выдает результаты
![](img/level02_1.png)

Расширение файла легко гуглится
![](img/level02_2.png)

Это tcpdump. Для интерпретации воспользуемся программой WireShark

АГА, это пароль! Только что за точки...
![](img/level02_3.png)

Посмотрим в hex формате
![](img/level02_4.png)

В Ascii-таблице:
`7f` - клавиша Del
`0d` - перевод строки

Складываем 1+1. Точка, это нажатие на клавишу Del, а последняя точка, на Enter.
![](img/level02_5.gif)

Получаем пароль, не задерживаемся.
![](img/level02_6.png)

### level03
