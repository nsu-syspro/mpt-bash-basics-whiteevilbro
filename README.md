[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/g5qqA0-e)
# Знакомство с Bash

<img alt="points bar" align="right" height="36" src="../../blob/badges/.github/badges/points-bar.svg" />

[![Очередная смешная картинка](https://imgs.xkcd.com/comics/the_general_problem.png)](https://xkcd.com/974/)


Для решения каждого из заданий необходимо выписать последовательность команд,
выполняющих то, что требуется в условии, в *исполняемый* файл `solution/<name>`,
где `<name>` - название скрипта, указанное в соответствующем задании.

> [!IMPORTANT]
> Файл с решением `solution/<name>` необходимо сделать исполняемым, с помощью команды
> ```console
> $ chmod +x solution/<name>
> ```

<details>
  <summary>Добавление в PATH</summary>

Для запуска скрипта без указания полного пути до него, можно его скопировать
(или создать [символическую ссылку](https://en.wikipedia.org/wiki/Symbolic_link#POSIX_and_Unix-like_operating_systems)
на скрипт) в какую-либо директорию, входящую в переменную окружения `PATH`.

Стандартной директорией для пользовательских скриптов является `~/.local/bin`,
которая по умолчанию должна быть включена в `PATH`.

</details>

<details>
  <summary>Отладка</summary>

Для локальной отладки можно запустить ваше решение с помощью следующей команды:
```console
$ bash -xe solution/<name>
```
Параметры `-xe` (`-x` и `-e`) включают логирование выполненных команд и
завершение исполнения при первой ошибке, что бывает очень полезно при отладке скриптов.
Более подробное описание этих и других опций утилиты `bash` можно получить с помощью
```console
$ bash -c "help set"
```
</details>

## Задание №1 (2 балла)

Требуется написать скрипт `untar`, который принимает параметром имя архива `<archive>`
и распаковывает в директорию `<archive>.unpacked` (если такой директории не существует,
то требуется ее создать).

**Пример использования**
```console
$ ls -1
test.tar
$ untar test.tar
$ ls -1
test.tar
test.tar.unpacked
```

> Вам понадобится работа с [позиционными параметрами](https://www.gnu.org/software/bash/manual/bash.html#Shell-Parameters) в Bash.

## Задание №2 (2 балла)

Требуется написать скрипт `reverse`, который выводит строки из входного потока
в обратном порядке.

**Пример использования**
```console
$ cat foo.txt
baz
bar
foo
$ reverse <foo.txt
foo
bar
baz
```

> Вам понадобится [read](https://www.gnu.org/software/bash/manual/bash.html#index-read)
> и [циклы](https://www.gnu.org/software/bash/manual/bash.html#Looping-Constructs) в Bash.

## Задание №3 (3 балла)

Требуется написать скрипт `addsuffix`, который принимает суффикс,
список файлов и добавляет указанный суффикс ко всем переданным файлам.

**Пример использования**
```console
$ ls -1
foo.c
hello.c
hello.sh
test.sh
test.tar
$ addsuffix '.bak' ./*.sh
$ ls -1
foo.c
hello.c
hello.sh.bak
test.c
test.sh.bak
test.tar
$ addsuffix 'pp' foo.c hello.c
$ ls -1
foo.cpp
hello.cpp
hello.sh.bak
test.c
test.sh.bak
test.tar
```

> Вам понадобится работа с [позиционными параметрами](https://www.gnu.org/software/bash/manual/bash.html#Shell-Parameters),
> [циклами](https://www.gnu.org/software/bash/manual/bash.html#Looping-Constructs)
> и [подстановка параметров](https://www.gnu.org/software/bash/manual/bash.html#Shell-Parameter-Expansion) в Bash.

## Задание №4 (3 балла)

Требуется написать скрипт `fizzbuzz.sh`, который принимает аргументом положительное число `n`
и выводит все числа от 1 до `n` по следующим правилам:

- Если число делится на 3, вместо числа выводить `Fizz`;
- Если число делится на 5, вместо числа выводить `Buzz`;
- Если число делится и на 3 и на 5, вместо числа выводить `Fizz Buzz`;
- Иначе выводить само число.

**Пример использования**
```console
$ fizzbuzz.sh 20
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
Fizz Buzz
16
17
Fizz
19
Buzz
```

> Вам понадобится работа с [арифметическими вычислениями](https://www.gnu.org/software/bash/manual/bash.html#Shell-Arithmetic)
> и [циклами](https://www.gnu.org/software/bash/manual/bash.html#Looping-Constructs) в Bash.

## Бонусное задание

Для проверки корректности ваших скриптов можно воспользоваться статическим анализатором [ShellCheck](https://github.com/koalaman/shellcheck),
который помогает найти потенциальные источники ошибок в Shell скриптах.
Например, большинство проблем, связанных с отсутствием двойных кавычек при использовании переменных.

Помимо онлайн версии, эту утилиту также можно установить и запустить локально, чтобы
автоматически проверять корректность ваших скриптов, как это сделано в "workflow"
в этом задании. Вы могли заметить, что после прохождения тестов, запускается
еще один "job" под названием `Check solutions`, который запускает `ShellCheck` на всех
скриптах в директории `solution`.

Бонусное задание заключается в прохождении всех проверок, которые репортует `ShellCheck` в этом "job"'е.
