# Подручный справочник для ЕГЭ по Информатике
Задачи берутся с РешуЕГЭ, к каждому написан номер. **Хэндбук бесплатен и приветствует дополнения!**  
Стараюсь написать максимально сжато, чтобы успеть прочитать, пока идешь в ППЭ
## Содержание
* [1 Задание - Граф](#1-задание---граф)
* [2 Задание - Логическое выражение и таблица истинности](#2-задание---логическое-выражение-и-таблица-истинности)
* [3 Задание - Магазины](#3-задание---магазины)
* [4 Задание - Условие Фано](#4-задание---условие-фано)
* [5 Задание - Алгоритмы Исполнителей](#5-задание---алгоритмы-исполнителей)
* [6 Задание - Черепашка](#6-задание---черепашка)
* [7 Задание - Картинки, звук, цвета, сжатие, расширение](#7-задание---картинки-звук-цвета-сжатие-расширение)
* [8 Задание - Перебор слов](#8-задание---перебор-слов)
* [9 Задание - Работа с таблицами](#9-задание---работа-с-таблицами)
* [10 Задание - Слова в книжках](#10-задание---слова-в-книжках)
* [11 Задание - Пароли](#11-задание---пароли-могут-быть-с-допсведениями)
* [12 Задание - Исполнитель Редактор](#12-задание---переводчик-исполнитель-редактор)
* [13 Задание - IP адреса и URL](#13-задание---ip-адреса-и-url)
* [14 Задание - Выражение в конкретной системе счисления](#14-задание----выражение-в-конкретной-системе-счисления)
* [15 Задание - Преобразование логических выражений](#15-задание---преобразование-логических-выражений)
* [16 Задание - Рекурсивные алгоритмы](#16-задание---рекурсивные-алгоритмы)
* [17 Задание - Обработка числовой последовательности](#17-задание---обработка-числовой-последовательности)
## 1 Задание - Граф
Решения однозначного нет - опирайся только на логику. Делай скрин в Paint, так удобнее обозначать точки. Начиркать на листке бумаги тоже хороший вариант
## 2 Задание - Логическое выражение и таблица истинности
Пробегись глазами по таблице логических операторов:
| В выражении | Для Python |
|-------------|------------|
| `∧`         | `and`      |
| `∨`         | `or`       |
| `≡`         | `==`       |
| `→`         | `<=`       |
| `¬`         | `not`      |

Твой порядок действий: написать цикл, получить таблицу, подумать мозгом и соотнести буковки (сложна)
### Решение РешуЕГЭ [14688](https://inf-ege.sdamgia.ru/problem?id=14688 "Задачка на портале")
Перед началом проанализируем задачку - в данной таблице у функции нулевой результат, это и отметим в нашем коде

Начнем с таблицы истиности:
**Напишем цикл на Python**
```python
print("x y z") # Если есть w или нужно чекать результат, дополни!
# На каждую букву по циклу for...range(2), так как перебираем каждое
for x in range(2):
    for y in range(2):
        for z in range(2):
            if not ((x or y) <= (z == x)): # Здесь записываем логическое выражение. У меня перед ним стоит not потому что в задаче рассматривается нулевой результат функции. Если единичка, not не надо
                print(x, y, z)
```
Результат выполнения:
```
x y z
0 1 1
1 0 0
1 1 0
```
Путем соотнесения в голове или на бумажке получаем ответ **xzy**
## 3 Задание - Магазины
Посмотри любое на РешуЕГЭ, оно вполне себе понятное
## 4 Задание - Условие Фано
Тут выгоднее строить дерево на листочке.

**Условие Фано**: *Никакое кодовое слово не может быть началом другого кодового слова.*  
**Иными словами**: *То, что уже известно, не может быть продолжено и известные данные являются конечной точкой дерева.*  
*Например*, известно что есть код **011**, применив **условие Фано** мы знаем, что не может быть кодовых слов **0110, 0111, 01100** и так далее

Следуя этому условию, нарисуй дерево

Далее, есть 2 типа:
- **Выбор кода при неиспользуемых сигналах:**
  Записываешь по кодам из дерева нужное слово, сичтаешь сколько циферок получилось и пиши количество в ответ
- **Выбор кода:**
  Считаешь количество чисел всех точек. Например, у тебя дерево **0, 10, 110, 1110 и 1111**, считай количество каждого - **1 + 2 + 3 + 4 + 4 = 14** - это твой ответ

## 5 Задание - Алгоритмы исполнителей
**Десятичное преобразование - простой вид, не частый гость:**
---
РешуЕГЭ [7663](https://inf-ege.sdamgia.ru/problem?id=7663 "Задачка на портале")

```python
for i in range(100, 1000): # перебор числа, меняй диапазон по своему желанию, но не борщи
    s = str(i) # Преобразуй чиселку в строчку, так удобнее будет работать

    # Выполняем команды
    # Начало команды 1
    k1 = int(s[0]) + int(s[1])
    k2 = int(s[1]) + int(s[2])
    # Конец команды 1

    # Начало команды 2
    first = str(max(k1, k2))
    second = str((min(k1, k2)))
    s1 = first + second
    # Конец команды 2

    # Проверка, чтоб узнать ответ
    if s1 == '1412':
        print(i) # Выводим ответ
        break # Останавливаем выполнение, так как минималка, если иначе, это не ставь, а в ответ пихай максимум
```

**Двоичное кодирование - сложнее, дают часто:**
---
РешуЕГЭ [362](https://inf-ege.sdamgia.ru/test?theme=362 "Задачка на портале")

```python
for n in range (1,100): # перебор числа, меняй диапазон по своему желанию, но не борщи
    s = bin(n)[2:] # 1 команда, мы переводим в двоичку, а срез в конце чтобы отрезать первые два символа 0b

    # 2 команда - остаток от деления
    if s.count('1') % 2 == 0:
        s += '00'
    else:
        s += '10'
    r = int(s,2) # переводим в десятичку
    # Проверяем
    if r>43:
        print(r) # Выводим ответ
        break # Останавливаем выполнение, так как минималка, если иначе, это не ставь, а в ответ пихай максимум
```

## 6 Задание - Черепашка
### Кумира может не быть! Поэтому решаем в Python с помощью `turtle`
Импортируется `turtle` так:
```python
from turtle import *
```

### Таблички команд
---

**Основные команды:**
| В задаче  | Команды в Python |
|-----------|------------------|
|Повтори x[]|`for i in range(x):`|
|Вперед x   |`forward(x)`        |
|Назад x    |`back(x)`           |
|Налево x   |`left(x)`           |
|Направо x  |`right(x)`          |

Служебные команды:
| Команда | Описание |
|---------|----------|
|`goto(x, y)`|Перемещает черепаху по координатам `x, y`|
|`dot(size, color)`|Поставить точку размера `size` и цвета `color` (`color` строкой, например "red")|
|`up()`|Поднимает перо (хвост)|
|`down()`|Опускает перо (хвост)|
|`done()`|Замораживает программу, обязательно для подсчета|

Контроль рисования:
| Команда | Описание |
|---------|----------|
|`speed(n)`|Задает скорость рисования `n`|
|`tracer(n)`|Настраивает трассировку линий черепахи. **Сложно?** Проще говоря, это прорисовка, отключить которую можно задав `0`, чтобы не ждать|

### Масштабирование
---
Чтоб все разглядеть, воспользуемся масштабированием. Для этого вводим значение **коэффициент** и работаем с ним.  
*Например*, в коде ниже переменная `k` - коэффициент масштабирования.  
Где его нужно применить:
- в командах движения `forward()`, `back()`
- при выставлении точек (цикл в коде ниже подходит под все, но можно играться со значениями, если не хватает)

### Решим задачку [46275](https://inf-ege.sdamgia.ru/test?theme=46275 "Задачка на портале")

```python
from turtle import * # Можно и по-нормальному, но так удобнее

k = 40 # Коэффициент масштаба
tracer(0) # Чтоб долго не ждать, повысить скорость

# Рисуем фигурку
for i in range(5):
    forward(9 * k) # Движения умножаем на коэффициент масштабирования, повороты не надо!
    right(120)
up()

# Ставим точки (цикл стандартный для всего)
for x in range(-10 * k, 10 * k, k):
    for y in range(-10 * k, 10 * k, k):
        goto(x,y)
        dot(3, "red")
done() # Морозим прогу для подсчета ответа
```
> Читай внимательно свое задание и считай что нужно!

## 7 Задание - Картинки, звук, цвета, сжатие, расширение
### Картинки
---
#### Основная формула - $`N = 2^i`$
Где $`N`$ - **количество цветов**, а $`i`$ - **глубина цвета**

### Звук
---
#### Хранение
##### Формула дискретизации - $`V = M * i * t`$
Где $`V`$ - **объем файла в битах**, $`M`$ - **частота дискретизации (в Гц)**, $`i`$ - **разрешение в битах**, $`t`$ - время звучания в секундах
#### Передача
> Пока сам не знаю

## 8 Задание - Перебор слов
Будем использовать инструмент `product` в модуле `itertools`
### 1 тип - Слова по порядку
---
Решим задачку [3193](https://inf-ege.sdamgia.ru/problem?id=3193 "Задачка на портале")
```python
from itertools import product # импортируем только product из itertools
words = list(product('АОУ', repeat=5)) # задаем в product наш алфавит, сколькобуковенные слова в параметре repeat и преобразуем из объекта product в list для удобства поиска
print("".join(words[209])) # красивоско выводим используя пустую строчку и join, в join пихаем полученный список слов, из которого выбираем 209 по порядку
```
### 2 тип - Подсчет количества разных последовательностей
---
Решим задачку [10473](https://inf-ege.sdamgia.ru/problem?id=10473 "Задачка на портале")
```python
from itertools import product # импортируем только product из itertools
cnt = 0 # создаем счетчик
for i in product('1234', repeat=5):  # задаем в product наш алфавит, сколькобуковенные слова в параметре repeat
    if i.count('1') == 2: # считаем, что в каждом сгенерированном коде 2 единички
        cnt += 1 # если да, засчитываем
print(cnt) # в конце выводим
```
### 3 тип - Подсчет количества слов с ограничениями
---
Решим задачку [7986](https://inf-ege.sdamgia.ru/problem?id=7986 "Задачка на портале")
```python
from itertools import product # импортируем только product из itertools
con = "ЗМ" # алфавит согласных букв
vol = "ИА" # алфавит гласных букв
ar = list(product("ЗИМА", repeat=5)) # задаем в product наш алфавит, сколькобуковенные слова в параметре repeat и преобразуем из объекта product в list для удобства поиска
cnt = 0 # создаем счетчик
for e in ar: # проходимся по каждому слову из массива
    if e[0] in con and e[-1] in vol: # проверка того, что первая буква согласная, а последняя - гласная
        cnt += 1 # если да, засчитываем
print(cnt) # выводим счетчик
```
## 9 Задание - Работа с таблицами
### Предлагаю решать тоже в Python, ибо сейчас они не халявные, а километровые формулы держать в голове неохота
#### Как переделать Excel для решения в Python:
1. `Файл` -> `Сохранить Как...`
2. Имя файла не важно, а тип файла выбрать `Текст (MS-DOS)`
3. Перетащить полученный TXTшник в проект Pycharm или указать полный путь в коде
4. Убери последнюю строчку в файле (которая пустая, без данных) на всякий случай
#### Решение
Конкретного рецепта, к сожалению, нету, но я подскажу начало и дам хинты)  
**Начало:**
```python
f = open('9.txt').readlines() # открываем файл 9.txt и получаем в список строки
cnt = 0 # создаем счетчик
for line in f: # проходимся по каждой строчке в файлике
    elems = list(map(int, line.split())) # переводим строку в список из чисел
    работаем с ним дальше...
```
**Посказочки:**
- подсчет количества кого-то одного числа (повторения) - `elems.count(что_нужно_посчитать)`, выдаст количество
- `set()` можно использовать для хранения повторяющегося числа и его количества, так как множество не дает дублировать информацию
- множество можно перевести в список - `list(множество_которое_переводим)`
- сумма чисел считается функцией `sum(суммируемый_список_или_множество)`
- количество чисел считается функцией `len(что_считаем)`
- среднее арифметическое - `сумма / количество`
- если удовлетворяет условию, инкрементируй счетчик :-)
## 10 Задание - Слова в книжках
**Святая комбинация `Ctrl + F`**
Далее просто следуй условиям и считай. *Комментарии здесь излишние...*
## 11 Задание - Пароли (могут быть с доп.сведениями)
### Формула $`N = 2^i`$

Решим задачу [7670](https://inf-ege.sdamgia.ru/problem?id=7670 "Задачка на портале")

1. Прочти задачку и высмотри ключевые моменты:
   - количество символов в словаре для пароля
     > В данной задачке это буквы `А, Б, В, Г, Д, Е`, их `6`
   - количество символов в пароле
     > В данной задачке длина пароля дана `11` символов
   - сколько паролей надо хранить
     > В данной задачке нужно посчитать место для `20` паролей
   - единица измерения, в которой дать ответ
     > В данной задачке это `байты`
2. Выясни, сколько бит займет кодирование одного символа из словаря. Для этого обратимся к степеням двойки из формулы.
   Берем `количество символов в словаре для пароля` и подставляем это число в формулу как $`N`$, получится как-то так: $`6 = 2^i`$  
   > **Заметим**, что `6` не является степенью двойки, поэтому мы находим $`i`$ исходя из ближайшего **большего** числа, в нашем случае, ближайшее большее к `6` будет `8`, что есть `3` степень двойки, ее и запомним
3. Считаем длину одного пароля: умножаем число, полученное выше на `количество символов в пароле`
   > У нас это $`3 * 11 = 33`$ бита на один пароль
4. Переводим в необходимую единицу измерения:
   > 1 байт = 8 бит, значит у нас 33 бита будут 5 байт, потому что также выбираем целое количество байт. Ближайшее большее к 33 битам - 40 бит, что будет 5 байт, запомним
5. Уже финалочка - считаем место для хранения: умножаем число, полученное выше на `сколько паролей надо хранить`
   > У нас это $`5 * 20 = 100`$ байт на хранение 20 паролей - **это наш ответ**

### Теперь рассмотрим подвид с дополнительными сведениями:
Задача [8101](https://inf-ege.sdamgia.ru/problem?id=8101 "Задачка на портале")

Выполняем действия с `1-4` и прибавляем объем доп.данных

То есть, наши действия:
1. Прочти задачку и высмотри ключевые моменты:
   - количество символов в словаре для пароля
     > В данной задачке это буквы ` А, В, C, D, Е, F, G, H, К, L, M, N`, их `12`
   - количество символов в пароле
     > В данной задачке длина пароля дана `15` символов
   - отведенное место для доп.данных
     > В данной задачке под доп.данные отводится `12` байт на каждого пользователя
   - сколько паролей надо хранить
     > В данной задачке нужно посчитать место для `50` паролей с данными
   - единица измерения, в которой дать ответ
     > В данной задачке это `байты`
2. Выясни, сколько бит займет кодирование одного символа из словаря. Для этого обратимся к степеням двойки из формулы.
   Берем `количество символов в словаре для пароля` и подставляем это число в формулу как $`N`$, получится как-то так: $`12 = 2^i`$  
   > **Заметим**, что `12` не является степенью двойки, поэтому мы находим $`i`$ исходя из ближайшего **большего** числа, в нашем случае, ближайшее большее к `12` будет `16`, что есть `4` степень двойки, ее и запомним
3. Считаем длину одного пароля: умножаем число, полученное выше на `количество символов в пароле`
   > У нас это $`4 * 15 =  60`$ бит на один пароль
4. Переводим в необходимую единицу измерения:
   > 1 байт = 8 бит, значит у нас 60 бит будут 8 байт, потому что также выбираем целое количество байт. Ближайшее большее к 60 битам - 64 бита, что будет 8 байт, запомним
5. Добавляем доп.данные к паролю:
   > $`8 + 12 = 20`$ - конечный вес записываемых данных
5. Уже финалочка - считаем место для хранения: умножаем число, полученное выше на `сколько паролей надо хранить`
   > У нас это $`20 * 50 = 1000`$ байт на хранение 50 паролей с данными - **это наш ответ**

## 12 Задание - переводчик (исполнитель Редактор)
### На самом деле, все просто - сконструируй входные данные и переведи код с алгоритмического языка в Python (словарик будет ниже), нажми на кнопку, получишь результат :-)

Алгоритмическо-Питонический словарик:
| Алгоритмический | Python |
|-----------------|--------|
|заменить(v, w)|`s.replace(v, w, 1)`|
|напшлось(v)|`v in s`|
|пока|`while`|

> При выполнении `s.replace(v, w, 1)` не забывай присвоить его к входным данным, иначе ничего не поменяется

Решим [9365](https://inf-ege.sdamgia.ru/problem?id=9365 "Задачка на портале")
```python
s='8'*68 # конструируем входные данные 
while ('222' in s) or ('888' in s): # цикл пока и два нашлось(v)
    # для замены нужно присваивать замененные данные в исходную строку, не забудь!
    if ('222' in s): 
        s=s.replace ('222','8',1)
    else:
        s=s.replace ('888','2',1)
print(s) # выведи результат
```
## 13 Задание - IP адреса и URL
### URL:
Возьмем за пример такой адрес: `http://www.ftp.ru/index.html` и разберем его на составляющие

|Составляющая|Описание, какие бывают еще|
|------------|--------------------------|
|`http://`|Это протокол, используемый для передачи ресурса. Ещё встречаются такие: `https://`, `ftp://`, `smb://`|
|`www.ftp.ru`|Это сервер, на котором находятся данные|
|`index.html`|Это получаемый файл, сначала название, через точку пишется расширение `html`, `txt`, `net` (абсурдно, дано чтобы запутать, рассмотрим в задачке)|

#### Расспотрим несложную задачку [7258](https://inf-ege.sdamgia.ru/problem?id=7258 "Задачка на портале")
Просто посмотри на URL и первая часть и будет протокол, ответ `http`

#### Рассмотрим хитрую задачку [2225](https://inf-ege.sdamgia.ru/problem?id=2225 "Задачка на портале")
Внимательно прочтем задачку:
> На **сервере info.edu** находится **файл exam.net**, доступ к которому осуществляется по **протоколу http**.  
  
Помним правило, что протокол всегда на первом месте, то есть первая часть будет состоять из

> http:// - `eg`
 
Далее всегда идет сервер обращения, в нашем случае, это `info.edu`, получаем:

> http://info.edu - `egad`  

Далее прописываем путь к файлу, у нас он в корне, поэтому через `/` запишем файл, который у нас `exam.net`:

> http://info.edu/exam.net - `egadbfc` - **наш ответ**  


### IP адреса:
**Их особенности:**
- IP адрес состоит из 4 чисел (их назвают октеты), записанных через точку, _например_, `192.168.1.10`
- Каждый октет меньше 256, то есть максимальное значение октета - `255`

#### Уже с этими знаниями мы можем решить задачку с восстановлением IP адреса по кусочкам ([2203](https://inf-ege.sdamgia.ru/problem?id=2203 "Задачка на портале")):

Посмотрим внимательнее на данные фрагменты: под буквой А мы видим «.64». Число, на которое указывает этот фрагмент, начинается с 64. Так как числа в IP-адресе не могут быть больше 255, мы не можем добавить в конце этого числа еще один разряд, а фрагментов, начинающихся с точки, больше нет, следовательно, этот фрагмент – последний.

Посмотрим на фрагмент под буквой Г. В нем стоит число без точек, значит, это либо последний фрагмент, либо первый. Место последнего фрагмента уже занято, значит, фрагмент Г на первом месте.

В конце фрагмента В - число 133, отделенное точкой. Так как в IP-адресе не может быть числа, большего 255, то за фрагментом В должен следовать фрагмент, начинающийся с точки. Значит, фрагмент В идет перед фрагментом А.

**Итого получаем ГБВА.**

Освежи в голове эти понятия:
- IP адрес в сети - рандомный IP адрес из сети
- Адрес сети - зарезервированный IP адрес, используемый для обозначения всей сети
- Маска сети - битовая маска для определения по IP-адресу адреса подсети и адреса узла (хоста, компьютера, устройства) этой подсети

Правила:
- если октет маски `255`, то октет IP адреса останется **таким же**, а $`255_{10} = 11111111_{2}`$
- если октет маски `0`, то октет IP адреса будет `0`

#### Приступим к харду?
Тогда решим задачку [2238](https://inf-ege.sdamgia.ru/problem?id=2238 "Задачка на портале") на определение **адреса сети**

```python
table = {0: 'А', 145: 'B', 255: 'C', 137 : 'D', 128 : 'E', 240 : 'F', 88 : 'G', 92 : 'H'} # Создаем буковенный список для сразу получения решения
ip_msk = [145 & 255, 92 & 255, 137 & 240, 88 & 0] # Сразу сложенный список
ans = ""
for i in ip_msk:
    if i in table: # если элемент из списка встречается в словаре, то выводим элемент словаря
        ans += table[i]
print(ans)
```

Теперь решим [7669](https://inf-ege.sdamgia.ru/problem?id=7669 "Задачка на портале") на определение **маски**

Решать будем с помощью встроенной библиотеки `ipaddress`
```python
from ipaddress import ip_network, IPv4Address

for mask in range(32):  # Перебираем маски
    net = ip_network(f"224.128.112.142/{mask}", strict=False) # создаем сеть

    if str(net.network_address) == "224.128.64.0": # Проверяем адрес сети
        mask = str(IPv4Address(int(("1" * mask).ljust(32, "0"), 2))) # конструируем маску
        print(mask.split(".")[2]) # выводим ответ
```

Теперь **подсчет количества адресов в сети** - [2231](https://inf-ege.sdamgia.ru/problem?id=2231 "Задачка на портале")

Также заиспользуем `ipaddress`
```python
from ipaddress import *
def calculate_host_number(subnet_mask, ip_address):
    network = IPv4Network(ip_address + '/' + subnet_mask, strict=False) # создаем сеть
    host_number = int(IPv4Address(ip_address)) - int(network.network_address) # считаем номер компьютера
    return host_number
print(calculate_host_number('255.255.255.224', '162.198.0.157'))
```
## 14 Задание -  выражение в конкретной системе счисления

Для начала разберемся с системами счисления **больше 10**:
В `10`-ую систему счисления входят числа `0123456789`, а далее в ход идут буквы **латинского** алфавита
_Таким образом_, в `11`-ую идет в конец к `10`-ой буква `A` и итогом будет `0123456789A`, тоже самое с `16`-ой - `0123456789ABCDEF`

Встроенные функции перевода систем счисления в Python:
|Функция|Описание|
|-------|--------|
|`bin(n)`|Переводит `n` в двоичную систему счисления|
|`hex(n)`|Переводит `n` в шестнадцатеричную систему счисления|
|`int(n, base)`|Переводит `n` системы счисления `base` в десятичную систему счисления| 

**Заметим**, что обе функции возвращают строку с двумя символами спереди - `0b`, которые мы откинем, используя срез `[2:]`, прямо с ним и вызовем функцию, _например_, `bin(n)[2:]` и на выходе получим чистое двоичное число

Универсальная функция перевода:
```python
def convert_to(number, base, upper=False):
    digits = '0123456789abcdefghijklmnopqrstuvwxyz'
    result = ''
    while number > 0:
        result += digits[number % base]
        number //= base
    return result[::-1].upper() if upper else result[::-1]
```

Рассмотрим несколько типов задач:
### Прямое сложение в системе счисления - [7761](https://inf-ege.sdamgia.ru/problem?id=7761 "Задачка на портале")

> Возведение в степень в Python происходит через операцию `**`, `n**m` = $`n^m`$  

У нас есть **два** варианта решения - с помощью `универсальной функции` и с помощью встроенной функции перевода `bin(n)[2:]`

Первый вариант - универсальная функция:
```python
def convert_to(number, base, upper=False):
    digits = '0123456789abcdefghijklmnopqrstuvwxyz'
    result = ''
    while number > 0:
        result = digits[number % base]
        number //= base
    return result[::-1].upper() if upper else result[::-1]

x = 4**2020 + 2**2017 - 15 # конструируем выражение
print(сonvert_to(x, 2).count("1")) # вызываем функцию и выводим количество единиц
```

Второй вариант - функция `bin(n)[2:]`:
```python
x = 4**2020 + 2**2017 - 15 # конструируем выражение
s = bin(x)[2:] # переводим в двоичную
print(s.count("1")) # выводим количество единиц
```

### Операции в одной системе счисления - [47218](https://inf-ege.sdamgia.ru/problem?id=47218 "Задачка на портале")
Число из `15`-ой системы будет находиться где-то среди `01234567890ABCDE`, что мы и переберем в цикле
```python
for x in '0123456789ABCDE': # перебор значения
    x1 = '123' + str(x) + '5' # собираем 1 слагаемое
    x2 = '1' + str(x) + '233' # собираем 2 слагаемое
    res = int(x1, 15) + int(x2, 15) # складываем, переводя числа в двесятичную
    if res % 14 == 0: # удовлетворяет ли условию
        print(res // 14) # выводим значение
        break # останавливаем, так как минимальное
```

### Операции в разных системах счисления с одной переменной - [48399](https://inf-ege.sdamgia.ru/problem?id=48399 "Задачка на портале")
Здесь внимательно читай задание, так как в первых строках может содержаться важная информация, например в этой задаче
> В записи чисел переменной x **обозначены допустимые в данных системах счисления неизвестные** цифры

Смотрим по максимальной - это `16`, а значит будем перебирать по `0123456789ABCDEF`  
Но может быть и записано в задаче, какие задачи допустимы, например в номере [48394](https://inf-ege.sdamgia.ru/problem?id=48394 "Задачка на портале")
> В записи чисел переменной x обозначена неизвестная цифра из алфавита **десятичной системы счисления**  

Решим же [48399](https://inf-ege.sdamgia.ru/problem?id=48399 "Задачка на портале")
```python
for x in '0123456789ABCDE': # перебор значения
    x1 = '3D4' + str(x) # собираем 1 слагаемое
    x2 = '4' + str(x) + 'C4' # собираем 2 слагаемое
    res = int(x1, 16) + int(x2, 14) # складываем, переводя числа в двесятичную (не забудь сменить системы счисления)
    if res % 154 == 0: # удовлетворяет ли условию
        print(res // 154) # выводим значение
        break # останавливаем, так как минимальное
```
### Операции в разных системах счисления с разными переменными - [48384](https://inf-ege.sdamgia.ru/problem?id=48384 "Задачка на портале")
То же самое, что и выше, только вкладываем второй цикл в первый с перебором `y`
```python
for x in '0123456789A':
    for y in '0123456789A':
        x1 = '88' + str(x) + '4' + str(y) # собираем 1 слагаемое
        x2 = '7' + str(x) + '44' + str(y) # собираем 2 слагаемое
        res = int(x1, 9) + int(x2, 11) # складываем, переводя числа в двесятичную (не забудь сменить системы счисления)
        if res % 61 == 0: # удовлетворяет ли условию
            print(res // 61) # выводим значение
            break # останавливаем, так как минимальное
```
## 15 Задание - преобразование логических выражений

На самом деле, это задание является "мутацией" 2 задания. Только тут нужно не заполнить таблицу истинности, а посчитать количество чисел/максимальное/минимальное число

### Координатная плоскость (частый тип) - [13745](https://inf-ege.sdamgia.ru/problem?id=13745 "Задачка на портале")
Наш старый знакомый метод решения - перебор:
```python
for a in range(300, 1, -1): # идем в обратную сторону
    k = 0 # счетчик
    for x in range(0, 300): # перебираем x и y
        for y in range(0, 300):
            if ((x <= 9) <= (x * x <= a)) and ((y*y <= a) <= (y <= 9)): # условие из задания (проверка на истинность, если на ложность, допиши == 0 в конец)
                k += 1 # прибавляем счетчик
    if k == 90000: # если сработали все значения (300 * 300)
        print(a) # выводим A
        break # стопорим
```

### Побитовая коньюнкция (2 в топе) - [9804](https://inf-ege.sdamgia.ru/problem?id=9804 "Задачка на портале")
Тоже самое, что и в первом:
```python
for a in range(0, 1000): # перебираем a
    k = 0 # счетчик
    for x in range(0, 1000): # перебираем x
        if (x & 29 != 0) <= ((x & 17 == 0) <= (x & a != 0)): # условие из задания (проверка на истинность, если на ложность, допиши == 0 в конец)
            k += 1 # прибавляем счетчик
    if k == 1000: # если сработали все значения
        print(a) # выводим A
        break # стопорим
```

### Числовые отрезки (3 в топе) - [7763](https://inf-ege.sdamgia.ru/problem?id=7763 "Задачка на портале")
```python
P = list(range(5,31)) # Задаем отрезок P
Q = list(range(14,24)) # Задаем отрезок Q
A = [i for i in range(5,31)] # Зададим A по большему отрезку
for x in range(5,31): # переберем x по большему
    if ((x in P) == (x in Q)) <= (not(x in A)): # условие из задания (проверка на истинность, если на ложность, допиши == 0 в конец)
        A.remove(x) # удаляем x из A, если подходит условию
print(max(A) - min(A)) # Выводим ответ
```

### Разное (вообще-то с штукой ДЕЛ(m, n)) - [8106](https://inf-ege.sdamgia.ru/problem?id=8106 "Задачка на портале")
Прикол в том, что `ДЕЛ(m,n)` в Python выглядит так: `m % n == 0`

Если видишь `¬ДЕЛ(m,n)`, пиши `m % n != 0`
```python
for a in range(100, 0, -1): # пойдем в обратку
    k = 0 # счетчик
    for x in range(1, 1000): # с запасом
        if (x % a != 0) <= ((x % 6 == 0) <= (x % 4 != 0)): # условие из задания (проверка на истинность, если на ложность, допиши == 0 в конец)
            k += 1 # прибавляем счетчик
    if k == 999: # если сработали все значения
        print(a) # выводим A
        break # стопорим
```
## 16 Задание - рекурсивные алгоритмы
Кодом проще, чем руками. Убъешь минут 20-30 впустую иначе, плюс руками проще запустаться

Нужно просто расписать функцию по условию

Просто запомни, что конструкция `F(x) = y` в Python выглядит так:
```python
if n == x: return y
```
А если задано так: `F(n) = y, при n > x`, то в Python:
```python
if n > x: return y
```

### Алгоритмы, опирающиеся на несколько предыдущих значений (частый тип) - [4645](https://inf-ege.sdamgia.ru/problem?id=4645 "Задачка на портале")
```python
def F(n): # определяем функцию
    if n == 1: return 1 # F(1) = 1
    if n == 2: return 3 # F(2) = 3
    if n > 2: return F(n-1) * n + F(n-2) * (n-1) # F(n) = F(n–1) * n + F(n–2) * (n – 1) , при n > 2
print(F(5)) # вызываем функцию, выдаем ответ
```

### Алгоритмы, опирающиеся на одно предыдущее значение (2 в топе) - [4558](https://inf-ege.sdamgia.ru/problem?id=4558 "Задачка на портале")
Тоже самое, просто одно условие:
```python
def F(n): # определяем функцию
    if n == 1: return 1 # F(1) = 1
    if n > 1: return F(n-1) * n # F(n) = F(n–1) * n , при n > 1
print(F(5)) # вызываем функцию, выдаем ответ
```

### Рекурсивные функции с возвращаемыми значениями (3 в топе) - [36871](https://inf-ege.sdamgia.ru/problem?id=36871 "Задачка на портале")
Тут сложнее, но не сильно - перебирай `n` и проверяй выходное значение, если подходит, инкриментируй счетчик:
```python
def f(n): # определяем функцию
    if n == 0: return 0 # F(0) = 0
    if n > 0 and n % 2 == 0: return f(n / 2) # F(n) = F(n / 2), если n > 0 и при этом чётно
    if n % 2 != 0: return 1 + f(n - 1) # F(n) = 1 + F(n − 1), если n нечётно
k = 0 # счетчик
for n in range(1, 1001): # перебираем n
    if f(n) == 3: # проверяем условие
        k += 1 # инкриментируем счетчик
print(k) # выводим ответ
```

## 17 Задание - Обработка числовой последовательности
Все просто - открываешь файл, бежишь по циклу, итерируешь (тут придется бежать по индексу чтобы считать пары), проверяешь на условие, инкрементируешь счетчик, сравниваешь максимум/минимум функцией

### Решим задачку [37336](https://inf-ege.sdamgia.ru/problem?id=37336 "Задачка на портале")
```python
count = 0 # счетчик
m = -20001 # храним максимальное значение (оно отрицательное, так как максимальное число может быть и отрицательным), если минимальное, то значение положительное, но побольше (можно тоже 20000)
f = open('17.txt').readlines() # открываем файл, вытаскивем строки
s = list(map(int, f)) # создаем список из целочисленных значений
for i in range(len(s) - 1): # идем по индексу, так как нужно будет брать соседнее значение
    if (s[i] % 3 == 0) or (s[i + 1] % 3 == 0): # проверка на условие
        count += 1 # инкремент счетчика
        m = max(m, s[i]+ s[i + 1]) # считаем максимальное значение
print(count, m) # выводим результат сразу в консоль
```
