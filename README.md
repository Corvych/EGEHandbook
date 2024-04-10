# Подручный справочник для ЕГЭ по Информатике
Задачи берутся с РешуЕГЭ, к каждому написан номер. **Хэндбук бесплатен и приветствует дополнения!**  
Стараюсь написать максимально сжато, чтобы успеть прочитать, пока идешь в ППЭ
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

## 12 Задача - переводчик (исполнитель Редактор)
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
