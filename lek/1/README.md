## Линейные и циклические списки
### 2. Классификация структур данных. Последовательное распределение: массивы и векторы
**Структура данных** - способ организации данных в памяти компьютера (или на диске).
<br>
Примеры: массивы, связанные списки, стеки, очереди, двоичные деревья, хеш-таблицы и т.д.
<br>
**Алгоритмы** обеспечивают выполнение различных операций с этими структурами - например, поиск определенного элемента данных или сортировку данных.

Структуры данных помогают решить задачи:
- Хранение реальных данных (данные, описывающие физические сущности, внешние по отношению к компьютеру)
- Инструментарий программиста (не для пользователя, а для использования программистом внутри самой программы, *стеки, очереди*)
- Моделирование (ситуаций из реального мира, *графы, очереди*)

Структура данных - логическая или математическая модель организации данных

Данные могут быть организованы различными способами.
- Логическая структура (совокупность элементов данных и их отношение, *элементы скалярного типа, одного типа, разного типа*)
- Физическая структура (способ представления логических структур в машинном представлении)

Классификация структур данных:
1) Место хранения (оперативные / файловые)
2) Связь элементов (несвязные (*массивы*) / связные (*структуры*) / односвязные (*списки*) / двусвязные / многосвязные)
3) Изменчивость (статические (положение не меняются) / полустатические / динамические (положение по закону, кол-ву)
4) Упорядоченность элементов (линейные / нелинейные)

Типовые операции над структурами данных:
- создать
- уничтожить
- выбрать и изменить

![image](https://github.com/mireashik/aood_3sem/assets/49165758/92cb20c2-ca86-410a-ab9b-aab3ebc4425e)

### ПСЕВДОКОД
**Псевдокод** - естественный язык + конструкции языка программирования

Стандартные конструкции:
- Выражения (1, 2, 3, =, <, >)
- Объявление метода
- Условия (if, else)
- Циклы (while, for)

Он записывается для анализа человеком, а не компьютером.

### МАССИВ
![image](https://github.com/mireashik/aood_3sem/assets/49165758/cc3ab01f-a18b-469c-b934-8c8777052fbc)

Массив - самая простая и широко используемая структура данных. Другие структуры данных (стеки и очереди) - производные от массива. Доступ по index (индексам).

- Одномерные
- Многомерные

Операции:
- Insert
- Get
- Delete
- Size

### Последовательное распределение
Список элементов в последовательных ячейках памяти, множество это массив и требует непрерывную область памяти.

Операция включения вставляет `z` в позицию `i` так: смещение элементов `xi, xi+1, ..., xn` на 1 позицию вправо ▶
<br>
В позицию `i` помещается элемент `z`.

Операция исключения удаляет элемент из позиции `i`: элементы `xi + 1, ..., xn` на 1 позицию ◀. Время O(n).

Плюсы:
- Прямой доступ к любому элементу памяти (index в массивах)
- Ячейки памяти - небольшие расходы памяти (для статистических)

Минусы:
- Динамические структуры плохо реализуются
- Размер массива задаётся изначально (невозможно изменять, неэффективно в памяти)
- Операции включения / исключения зависят от размера массива


### ВЕКТОР
**Вектор** - линейная последовательность элементов. Доступ по разряду.

Методы доступа к обычным элементам последовательности + методы обновления, удаление и добавление элементов с определенным индексом.

Первый элемент имеет разряд 0
<br>
Последний элемент имеет разряд `n - 1`

Разряд, который получит новый элемент после его добавления (insert at rank 2).
<br>
Разряд также указывает на элемент, который должен быть удален из вектора (remove the element at rank 2).

S – линейная последовательность из n элементов. Вектор S является абстрактным типом данных, который поддерживает следующие основные методы:
1. elemAtRank(r) - возвращает элемент `S` с разрядом `r`
2. replaceAtRank (r,e) - замещает объектом `е` элемент `r` и возвращает его
3. insertAtRank (r,e) - добавляет в `S` новый элемент `e`
4. removeAtRank(r) - удаляет из `S` элемент с разрядом `r`

#### Реализация с помощью массива
Вектор наа основе массива А, где A[i] содержит ссылку на элемент разряда i.

- elemAtRank(r) - возвращение элемента A[r]
- insertAtRank(r,e) - перемещение элементов вперед для вставки нового элемента с разрядом r
- removeAtRank(r) перемещение элементов назад для заполнения разряда r удаленного элемента

![image](https://github.com/mireashik/aood_3sem/assets/49165758/768eb754-a1d8-4c09-bec3-5ea5f468a6ea)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/da270f9e-a0b1-4938-a278-1e06b31c7727)

### 3.1. Связное распределение. Связной список
Связный список - структура данных, каждый элемент содержит информацию о следующем элементе. По сравнению с массивом - эффективное изменения расположения элементов. Хуже доступ к элементу списка (надо проходить по всему списку от начала)

Связный список — это набор элементов, причем каждый из них является частью узла (`node`), который также содержит ссылку (`link`) на узел.

Связное распределение - не нужна непрерывная память (в отличии от последовательного распределения). Элементы располагаются произвольно в памяти. Структуры динамические.

Каждый узел 2 части: info - сам элемент множества, next - указатель на следующий элемент. Доступ к узлу возможен только в том случае, если на него указывает хотя бы один указатель.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/c7a286bc-b822-4073-ad88-73ca501ea73e)

Если память заранее не резервируется, нужен отдельный механизм. Операция new (p) - новый пустой узел и указатель p на него.
<br>
Если у узла пропадает доступ, нужно удалить его (сборка мусора), чтобы память не занималась. Операция dispose(p).

Включение элемента `z` в позицию `i` - создание нового узла, запись значения `z` в поле `info` этого узла и установку 2 указателей

![image](https://github.com/mireashik/aood_3sem/assets/49165758/2f154038-deeb-45ca-9ef0-42ba0727b5ef)

Исключение элемента `xi` - удаление из списка узла `xi`, установку значения одного указателя и освобождение памяти
<br>
Процедура DELETE НЕ МОЖЕТ исключить элемент из начала списка.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/f0805876-9664-4bfe-a755-4d629e68b257)

Для сцепления 2 списков достаточно установить значение поля next последнего элемента первого списка
<br>
Разбиение на 2 списка можно выполнить (если обеспечен доступ к узлу разбиения)

Операции и их время не зависит от размера. Прямой доступ невозможен, только последовательный (нельзя обратиться по индексу, нужно проходить весь список). Доп. память для указателей.

### 3.2. Операции над списком
Отойдём от понятия "разряд". Узел - место в списке.

Позиция - место относительно своих соседей. Всегда "за" какой-то позицией, и перед "некоторой". Позиция не меняется при одинаковом размере списка.

1. first() - позиция 1 элемента списка
2. last() - позиция последнего элемента списка
3. isFirst(p) - является ли позиция первой
4. isLast(p) - является ли позиция последней
5. before(p) - позиция перед позицией p
6. after - позиция после позиции p

### 4.1. Реализация связного списка с помощью массива
![image](https://github.com/mireashik/aood_3sem/assets/49165758/67b4f85d-0ef8-4abf-9020-44a9af21cf6d)

В массиве info хранятся элементы множества
<br>
В массиве next указатели, индексы позиций в массивах, где расположены последующие элементы.

Пусть требуется включить элемент f в список Y после элемента e, хранящегося в info[10].
<br>
Процедура new(p) установит указатель p=5 и исключит позицию 5 из списка свободных позиций.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/c83bce19-0ba9-427b-a58e-b61fbe45a3e4)

Вместо нескольких массивов, можно использовать 1 массив, элементы -  объекты комбинированного типа (записи). Каждая запись - узел списка и несколько полей.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/e3d37669-09d1-40fa-bc18-8b40df0d8fc9)

Реализация списков с помощью массивов - требует указания размера списка (если размер не ограничен, то использовать указатель 4.2)

### 4.2. Реализация связного списка с помощью указателя
Список состоит из ячеек и указателя, на следующую ячейку списка. Ячейка, содержащая элемент `аn` имеет указатель `nil`.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/f6d2cfd0-1996-45b7-bf09-8b5d88ac5624)

### 4.3. Разновидности связных списков
Существуют различные виды связных списков, ориентированных на облегчение выполнения тех или иных операций.

#### 4.3.1 Линейные списки
Упорядоченный набор элементов, включение новых элементов и исключение существующих в любом месте

![image](https://github.com/mireashik/aood_3sem/assets/49165758/4017e184-ab30-4393-8261-a53d63b29fe0)

**4.3.1.2. Линейный односвязный список**

![image](https://github.com/mireashik/aood_3sem/assets/49165758/3f19be50-b960-4946-879c-5655b0da3f2f)

**4.3.1.3. Связный список с заголовками**

В начало связного списка дополнительный фиктивный элемент (заголовок списка)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/eb3cbd24-801c-4e5c-b575-b4b1e1ab4861)

Упрощение включения и исключения (начало и конец списка не затрагивается, только после или перед заголовками). Достаточно процедур INSERT и DELETE.

**4.3.1.4. Линейный двусвязный список**

![image](https://github.com/mireashik/aood_3sem/assets/49165758/e3550342-d9b5-4859-98c0-58dc650d9874)

Если нужно прямое и обратное перемещение

#### 4.3.2. Циклический список
Чтобы не просматривать список с начала - используем кольцо

![image](https://github.com/mireashik/aood_3sem/assets/49165758/d1c67838-38a6-4880-a25a-304fc386f61b)

В любой из любого (но не прямой доступ!)

**4.3.2.1 Односвязный циклический список**

![image](https://github.com/mireashik/aood_3sem/assets/49165758/4d203902-c3bf-4be2-bae1-0c52da35580c)

Циклический список не имеет первого и последнего элемента.

**4.3.2.2 Двусвязный циклический список**

![image](https://github.com/mireashik/aood_3sem/assets/49165758/030b9363-f855-46ee-a1f8-a504b65530c0)

Внешний указатель - на 1 элемент списка. Последний - слева от 1-ого.

### Выводы
Использование той или иной разновидности связных списков позволяет упростить выполнение одних операций со списками, но усложнить другие. Поэтому выбор представления должен осуществляться на основе анализа типов операций, которые будут выполняться над множеством. Реализация операций для различных видов связных списков предлагается в качестве упражнений для самостоятельной разработки.

- элемент двустороннесвязанного списка — это запись, содержащая 3 поля: key, next, prev
- в одностороннесвязанных списках отсутствуют поля prev
- в упорядоченном списке поля расположены в порядке возрастания ключей, так что у головы списка ключ наименьший, а у хвоста - наибольший, в отличие от неупорядоченного списка.
