## ХЕШ-ФУНКЦИИ
Хеш-таблицей называется структура данных, которая позволяет осуществлять очень быстро такие операции как вставка и поиск
<br>
При пользовании хеш-таблицами обращение к данным осуществляется, практически, моментально

Хеш-таблицы значительно превосходят деревья
<br>
быстродействие значительно падает при заполнении таблицы, поэтому размер должен быть фиксирован (на основе массивов)
<br>
не существует удобного способа перебора элементов

**Хеш-функция** представляет собой функцию, преобразующую число из большего диапазона (множества) в число из меньшего диапазона (множества). Меньший диапазон соответствует **индексам** массива.
<br>
Массив, в который вставляются данные с использованием ХЕШ-ФУНКЦИИ - **ХЕШ-ТАБЛИЦА**

1. ЭФФЕКТИВНОСТЬ
2. РАВНОМЕРНОСТЬ
3. ЛАВИННОСТЬ (при почти одинаковых входных данных очень разный результат)
4. НЕОБРАТИМОСТЬ

**Коллизия**  - совпадение значений функции для разных значений ключа

Множество хеш-функций считается УНИВЕРСАЛЬНЫМ, если для каждой пары ключей Ki, Kj, i≠j количество хеш-функций удовлетворяет выражению (3):

![image](https://github.com/mireashik/aood_3sem/assets/49165758/d586ef32-1161-4480-8a83-e9e24be5d885)

Преобразование, производимое хеш-функцией, называется **ХЕШИРОВАНИЕМ**

### 1 ВАРИАНТ
Особенностью 1 варианта является то, что пространство имен очень мало. 

![image](https://github.com/mireashik/aood_3sem/assets/49165758/55c46454-5437-4910-b0c1-960b74bc74f7)

Рассмотренный вариант является идеальным случаем хеширования, когда размер хеш-таблицы оказался равным размеру пространства имен. На практике это выполняется редко, обычно память слишком мала, чтобы вместить все пространство имен

### 2 ВАРИАНТ
Особенностью данного варианта является то, что пространство имен велико (не умещается в память), а таблица **СТАТИЧЕСКАЯ**.
<br>
хеш-функцию можно выбрать ПОСЛЕ того, как станет известно содержимое таблицы (она ж не меняется!)
<br>
значит можно найти легкую функцию, которая однозначно задаёт таблицу имён в таблицу адресов (даже с сохранением естественного порядка), особенно легко найти такую хэш-функцию если хеш-таблица содержит больше ячеек, чем имен
<br>
данный вариант сводится к ПЕРВОМУ варианту

### 3 ВАРИАНТ
пространство имен велико (не умещается в память), а таблица динамическая
<br>
содержимое таблицы естветвенно меняется, и в таком случае заранее не известно
<br>
Хэш-функция тогда строится независимо по другой информации таблицы (например некоторые имена встречаются чаще чем другие)
<br>
От этого можно выбрать размер хеш-таблицы m и построитьхеш-функцию h

Допустим выбрана хэш-функция, которая отображает цепочку из 3 самых правых разрядов:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/357fe6cf-6080-4971-b0c0-8e67c4ef3206)

h отображает x2 и x5 на один и тот же адрес, это **коализия**, значит меняем ячейку по каким-то правилам, например сдвигаем в первую свободную ячейку

![image](https://github.com/mireashik/aood_3sem/assets/49165758/11bad8c1-237f-47e3-a315-2b010d5b19bf)

Для реализации исключения необходимо иметь три состояния ячейки памяти: «занято», «пусто» и «исключено». Тогда исключение имени выполняется пометкой его ячейки как «исключено»

Поэтому хеш-функция должна быть построена так, чтобы равномерно **рассеять по памяти те подмножества** множества S, которые могут встретиться в качестве содержимого **таблицы**. 

Необходимо избегать хеш-функций, которые склонны отображать СКУЧЕННЫЕ ИМЕНА (например, x1, x2, x3 или a1, b1, c1 и тому подобное) в СКУЧЕННЫЕ АДРЕСА, поскольку они могут вызвать чрезмерное число коллизий

Большинство используемых на практике хеш-функций основано на другом  подходе, связанном с требованием, чтобы **каждый** из $l_{addr}$ разрядов адреса зависел от **ВСЕХ** $l_{name}$ разрядов имени

Многочисленные тесты показали хорошую работу двух основных методов определения хеш-функций:
1. Метод мультипликативного хеширования
2. Метод деления с остатком

### Метод мультипликативного хеширования
умножение на константу

![image](https://github.com/mireashik/aood_3sem/assets/49165758/65107a93-8e7c-4fd9-a6aa-05b73a9ca767)

Частным случаем выбора константы A является значение, обратное золотому сечению:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/320a21d6-9197-4f8b-8339-9a707c50d68e)

### Метод деления с остатком
![image](https://github.com/mireashik/aood_3sem/assets/49165758/d3846628-b2f5-4fde-b2f1-770705ddb2c8)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/ade3a8f3-6ab4-4770-930e-a598fef38988)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/92af43e4-3934-4748-b9ff-0e4767372865)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/29a2392e-acd0-4082-9294-6d7973dd76d4)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/06822e68-628f-42dd-ab11-38daafdcc550)

## ХЕШ-ТАБЛИЦЫ
Применение хеш-функции к ключу даст нам индекс в этом массиве

![image](https://github.com/mireashik/aood_3sem/assets/49165758/a20145a1-3d5e-43cb-a629-e793418dedc1)

**Коэффициент заполнения** - среднее число на 1 ячейку таблицы.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/b329d0a1-ee78-4bb5-b57b-5493d2b2ea81)

Для противодействия с **коллизиями** существует несколько способов организации хеш-таблиц:
- ПРЯМАЯ (ЗАКРЫТАЯ)
- ОТКРЫТАЯ

![image](https://github.com/mireashik/aood_3sem/assets/49165758/609ac14d-9ee7-45f9-95cd-a7a4ba408191)

### Хеш-таблицы с прямой (закрытой) адресацией
При коллизии во время создания элемента создаётся связный список конфликтующих.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/16aa3dc1-7215-429b-a1b9-b2a80f826502)

### Хеш-таблицы с открытой адресацией
Вторичные структуры данных не используются ‒ и все пары ключ/значение хранятся в самой таблице

Малейшая неравномерность при генерации значений приводит к большим кластерам коллизий.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/e862137d-dbba-4a83-8c9c-8a03b5967bfe)

### Расширение хеш-таблицы
![image](https://github.com/mireashik/aood_3sem/assets/49165758/7f106c00-76ea-4aa4-9031-95a8e7d066e1)

### Рекомендации по организации хеш-таблиц
При закрытой адресации ухудшается локальность обращения к кэш-памяти, что часто приводит к потере производительности
