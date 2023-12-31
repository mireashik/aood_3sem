## Графы. Часть 1.
### 1. Основные понятия и определения.
Граф ‒ множества вершин и множества соединяющих их рёбер. Граф G состоит из множества V. 
<br>
Вершины v и w лежат на ребре e, ребро e инцидентно вершинам v и w.

Смежность вершин - 2 вершины называются смежными, если они инцидентны 1 ребру
<br>
Мультиграф - граф с кратными рёбрами
<br>
Псевдомультиграф - граф с петлями и кратными рёбрами
<br>
Изолированная вершина - вершина с 0 степенью
<br>
Висячая вершина - вершина с 1 степенью
<br>
Полный граф - каждые 2 вершины соединены одним ребром: `N * (N - 1) / 2`
<br>
Регулярный граф - степени одинаковые для всех вершин.
<br>
Двудольный граф - вершины графа можно разделить на 2 множества
<br>
Связный граф - пара его вершин соединена маршрутом

![image](https://github.com/mireashik/aood_3sem/assets/49165758/66801ae1-98a7-4176-a6bb-efa7b46762fc)

### 1.1.2. Неориентированные графы
Маршрут/цепь - последовательность различающихся вершин, каждая из которых является смежной по отношению к другой
<br>
Цикло - цепь более 3 вершин, начало = конец

![image](https://github.com/mireashik/aood_3sem/assets/49165758/01c74183-dd6e-470c-bd9e-af31789c6412)

### 1.1.3. Ориентированные графы
Сильносвязный граф - от любой вершины к любой другой вершине имеется направленный маршрут
<br>
Слабосвязный граф - при удалении ребер неориентированный граф получился связным

![image](https://github.com/mireashik/aood_3sem/assets/49165758/2f3d6d21-b0e6-4bdb-91c4-1fd992e02331)

### 1.1.4. Остовное дерево
Остовное дерево графа (или стягивающее, покрывающее дерево, каркас графа, скелет) - дерево со всеми вершинами исходного графа, без циклов и контуров

На связном графе можно построить более чем 1 остовное дерево
<br>
Для взвешенного графа существует по крайней мере 1 минимальное остовное дерево.

Минимальное остовное дерево (или минимальное покрывающее дерево) в (неориентированном) связном взвешенном графе ‒ остовное дерево с минимальным весом
<br>
вес дерева - сумма всех весов рёбер

**Алгоритм Борувки-Соллина** - последовательное добавление рёбер к остовному лесу графа, пока лес не превратится в дерево (1 компонента связности), общее время работы алгоритмы составляет O(ElogV)
<br>
Для планарных графов время может быть уменьшено до O(E)

**Алгоритм Ярника-Прима** - рандомизированный алгоритм МОД, работающий в среднем за линейное время.

- матрица смежности ‒ О(|V|)
- двоичная куча и список смежности ‒О(|Е|log|V|)
- куча Фибоначчи и список смежности ‒ О(|Е|+|V|log|V|)

**Алгоритма Краскала** - для начала необходимо отсортировать рёбра по весу. Текущее множество рёбер - пустое. Затем добавляются рёбра, которые не вызовут цикла, выбирается минимальный вес (жадный алгоритм), и добавляется к текущему множеству
<br>
Остовные деревья нужны в компьютерных сетях. По протоколу STP (Spanning TreeProtocol – протокол остовного дерева) производится управление коммутаторами в локальных сетях Ethernet.

### 2.1. Компьютерное представление
#### Представление в виде множества
Графы - множество вершин, множество пар, множество вершин. 
<br>
Граф G состоит из множества V, называемого вершинами графа G, вершины - подмножество Av множества V
<br>
Для ориентированного графа пара (w,v) не равна паре (v,w)

#### 2.1.2. Реализация множеств
Есть 2 общих способа реализации множества вершин.
<br>
1 способ - представлении множества как списка его элементов
<br>
2 способ - битовая строка, хранит булево значение (т.е. один бит) для каждого члена множества, имеется ли он в множестве или нет.

```c++
type
  vertex = 1..maxvertex; // идентифицируем вершины их индексами
  counter = 0..maxvertex; // счетчик вершин
  adjacencyset = set of vertex;
  graph = record
  size: counter; // число вершин в графе
  A: array[vertex] of adjacencyset
end;
```

A[v] - множество всех вершин, смежных с вершиной v

#### 2.1.3. Таблицы смежности
```c++
type
  vertex = 1..maxvertex; // идентифицируем вершины их индексами
  counter = 0..maxvertex; // счетчик вершин
  adjacencytable = array [vertex, vertex] of Boolean;
  graph = record
  size: counter; // число вершин в графе
  A: adjacencytable
end;
```

Таблица смежности A имеет естественную интерпретацию: элемент A[v, w] истинен, если и только если вершина v смежна с вершиной w.
<br>
Если граф ориентирован, A[v, w] - индикатор наличия ребра от v -> w
<br>
Если граф не ориентирован, таблица смежности симметрична A[v, w] = A[w, v]

![image](https://github.com/mireashik/aood_3sem/assets/49165758/953b2b84-d5a1-4fac-b561-8e03f3199daa)

#### 2.1.4. Списки смежности
Список смежности, каждой вершине графа соответствует список, состоящий из «соседей» этой вершины.

Для представления графа мы должны иметь 2 списка:
- список вершин;
- для каждой вершины, список смежных вершин.

С использованием как непрерывных списков, так и простых связных списков (в виде двоичных или многовариантных деревьев или в виде пирамид)
<br>

#### 2.1.5. Связная реализация
При использовании связных списков и для вершин, и для списков смежности, достигается максимальная гибкость.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/535c0cd4-2975-4228-8321-c133d9043c18)

```c++
type
pointvertex = vertex;
pointedge = edge;
vertex = record
firstedge: pointedge; //начало списка связности
nextvertex: pointvertex //следующая вершина в связном списке
end;
edge = record
endpoint: pointvertex; //вершина, на которую указывает ребро
nextedge: pointedge; //следующее ребро в списке связности
end;
graph = pointvertex; //заголовок списка вершин
```

#### Непрерывная реализация
Поиск в связных списках оказывается весьма утомительным.

Иногда поиск в связных списках (выше) оказывается весьма утомительным. К тому же иногда нужен произвольный доступ к вершинам.
<br>
Для **непрерывного списка** смежности необходимо хранить счетчик, и для него использовать стандартное обозначение из теории графов: валентность вершины.
<br>
**Валентность вершины **- число смежных с ней вершин.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/dd1b3505-0095-4e82-b520-aaa8ec758514)

Реализация через непрерывные списки:
```c++
type
  vertex = 1..maxvertex; // идентифицируем вершины по их индексам
  counter = 0..maxvertex; // счетчик вершин
  adjacencylist = array [vertex] of vertex;
  graph = record
  size: counter; // число вершин в графе
  valence: array [vertex] of counter;
  A: array [vertex] of adjacencylist
end;
```

#### Смешанная реализация
Непрерывный список - для вершин, связная память - для списков смежности

![image](https://github.com/mireashik/aood_3sem/assets/49165758/16bb5fca-541b-4118-846c-298719f2d5a4)

```c++
type
  vertex = 1..maxvertex; // идентифицируем вершины по их индексам
  counter = 0..maxvertex; // счетчик вершин
  pointedge = edge;
  edge = record
  endpoint: vertex;
  nextedge: pointedge
  end;
  graph = record
  size: counter; // число вершин в графе
  firstedge: array [vertex] of pointedge
end;
```

#### Информационные поля
Иногда необходима дополнительная информация о каждой вершины или каждого ребра
<br>
В связных списках - дополнительне поля
<br>
В непрерывных реализациях - через преобразования элементов массива

Особо важным примером является организация сети через веса рёбер. Тогда используем таблицу смежности, где веса, а не 0 или 1.

### 2.2. Просмотр графа
Исследовать все вершины графа (как было у двоичных деревьев), однако при просмотре дерева обычно есть корень, в графах корня нет. Просмотр 1 может начаться с любой произвольно взятой вершины.

#### Метод просмотра графа в глубину
Почти как прямой просмотр упорядоченного дерева
<br>
При новой вершине мы просматриваем в начале все смежные с ней вершины (и идём вниз по уровням), а после все остальные

![image](https://github.com/mireashik/aood_3sem/assets/49165758/b06e874a-af41-4ea9-83d5-9a925a917b60)

#### Метод просмотра графа в ширину
Почти как уровневый просмотр упорядоченного дерева
<br>
При новой вершине мы просматриваем **ВСЕ** смежные с ней вершины в начале только **на 1 уровне**, далее спускаемся вглубь

![image](https://github.com/mireashik/aood_3sem/assets/49165758/55abf83f-0f4d-42b5-b43c-e351c4bbe536)

#### Алгоритм просмотра графа в глубину
Просмотр в глубину - рекурсивный алгоритм
<br>
Если есть циклы - делаем массив visited и устанавлием булевую правду перед посещением какой-то вершины 
<br>
Если граф несвязный (и все вершины мы не просмотрим) - помещаем алгоритм в цикл, который гарантировано пройдёт по всем вершинам

```c++
procedure DepthFirst (var G: graph; procedure Visit(var v: vertex)); //Просмотр в глубину
  // Pre: Граф G уже создан.
  // Post: Процедура Visit была выполнена над каждой вершиной графа G
  в порядке просмотра в глубину.
  // Uses: Использует процедуру Traverse, которая выполняет рекурсивный
  просмотр в глубину
  var
  visited: array [vertex] of Boolean;
  v: vertex;
  begin // процедура DepthFirst 
  for всех v in G do
    visited [v] := false;
  for всех v in G do
    if not visited [v] then
      Traverse(v)
end; // процедура DepthFirst
```

Рекурсия выполняется в следующей процедуре, которая должна быть объявлена внутри предыдущей

```c++
procedure Traverse (var v: vertex; procedure Visit(var v: vertex)); //Просмотр
  // Pre: v является вершиной графа G.
  // Post: Просмотр в глубину посредством процедуры Visit был завершен для v и всех вершин, смежных с v.
  // Uses: Использует процедуру Traverse рекурсивно.
  var w: vertex;
  begin // процедура Traverse
  visited [v] := true;
  Visit(v);
  for всех w смежных to v do
  if not visited [w] then
    Traverse(w)
end; // процедура Traverse
```

#### Алгоритм просмотра графа в ширину
Использование рекурсии и стека - эквивалентны, поэтому можно было использовать стек. Все непосещенные вершины смежные с текущий проталкиваются в стек, выталкивание из стека - следующая вершина.

В ширине используется - очередь.

```c++
procedure BreadthFirst (var G: graph; procedure Visit(var v: vertex)); // Просмотр в ширину
  // Pre: Граф G уже создан.
  // Post: Процедура Visit выполнена для каждой вершины графа G, причем 
  вершины выбирались в порядке просмотра в ширину.
  // Uses: Использует пакет операций с очередью. 
  type
  queueentry = vertex;
  var
  Q: queuetype;
  visited: array [vertex] of Boolean;
  v,
  w: vertex;
  begin // процедура BreadthFirst 
  for всех v in G do
    visited [v] := false;
  CreateQueue(Q);
  for всех v in G do
    if not visited [v] then
    begin
    Append(v, Q);
    repeat
    Serve(v, Q);
  if not visited [v] then
    begin
    visited [v] := true;
    Visit(v)
  end;
  for всех w смежных to v do
    if not visited [w] then
      Append(w, Q)
      until QueueEmpty(Q)
  end
end; // процедура BreadthFirst
```

### 3. Топологическая сортировка
Топологическая сортировка - упорядочивание вершин бесконтурного ориентированного графа согласно частичному порядку, заданному ребрами орграфа на множестве его вершин
<br>
Ориентированный ациклический граф ‒ орграф без циклов, но могут быть «параллельные» пути

Эта сортировка строит корректную последовательность выполнения действий, всякое из которых может зависеть от другого:
- последовательность курсов
- установки программ
- makefile

### 3.1. Постановка задачи
Если G нужный нам граф, то **топологический порядок (сортировка)** - последовательный список всех вершин G, если имеется ребро v -> w, тогда v идёт перед w в списке. 
<br>
Это ациклические ориентированные графы.

Примеры:
1. Учебные курсы - вершины, рёбра - связи между ними, как следует проходить эти курсы
2. Словарь технических терминов - термины имеют последовательность

![image](https://github.com/mireashik/aood_3sem/assets/49165758/66403668-a170-42b9-a3ca-fe83ed2e0fe2)

### 3.2. Алгоритм упорядочения в глубину
В топологическом порядке нам важен последовательно добавлять одну вершину за другой, и проверять все вершины которые следуют до неё.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/cf454ad0-1cce-4c28-bae9-ecb97fa3fd8e)

Мы начинаем с последних вершин, в начале place = число вершин графа. 

```c++
procedure DepthTopSort (var G: graph; var T: toporder); // Топологическое упорядочение в глубину
  //Pre: G является направленным графом без циклов, реализованным с 
  непрерывным списком вершин и связными списками смежности.
  //Post: Процедура выполняет просмотр графа G в глубину и генерирует 
  результирующий топологический порядок в массиве T.
  //Uses: Использует: процедура RecDepthSort выполняет рекурсивный просмотр 
  в глубину.
  var
  visited: array [vertex] of Boolean; // проверяет, что G не содержит циклов
  v: vertex; // очередная вершина, следующие за которой должны быть 
  упорядочены 
  place: counter; // следующая заполняемая позиция в топологическом порядке
  begin //процедура DepthTopSort
  for v := 1 to G.size do
  visited [v] := false;
  place := G.size;
  for v := 1 to G.size do
  if not visited [v] then
  RecDepthSort(v, place, T);
end; // процедура DepthTopSort
```

```c++
procedure RecDepthSort (v: vertex; var place: counter; var T: toporder); // Рекурсивное упорядочение в глубину
  // Pre: Параметр v является вершиной графа G, place является следующим 
  местом в топологическом порядке T, которое следует определить (начиная с конца 
  окончательно упорядоченного списка).
  // Post: Процедура размещает все вершины, следующие за v, и, наконец, саму 
  v, в топологическом порядке T, упорядочивая в глубину.
  20
  // Uses: Использует: глобальный массив visited и глобальный граф G;
  процедуру RecDepthSort рекурсивно. 
  var
  curvertex: vertex; // вершина, смежная с v 
  curedge: pointedge; // просматривает список вершин, смежных с v 
  begin // процедура RecDepthSort 
  visited [v] := true;
  curedge := G.firstedge [v]; //найдем первую вершину, следующую за v 
  while curedge nil do
  begin
  curvertex := curedge .endpoint; //curvertex есть вершина, смежная с v
  if not visited [curvertex] then
  RecDepthSort(curvertex, place, T);
  //упорядочим вершины, следующие за curvertex 
  curedge := curedge .nextedge // перейти к следующей непосредственно за 
  вершиной v
  end;
  T [place] := v; // разместим саму v в топологическом порядке 
  place := place – 1
end; // процедура RecDepthSort
```

### 3.3. Алгоритм упорядочения в ширину
Мы начинаем с поиска вершины, которая должна быть первой в топологическом порядке
<br>
Вершины, помещаемые раньше - которые не расположены после других вершин

```c++
procedure BreadthTopSort (var G: graph; var T: toporder); // Топологическое упорядочение в ширину
  // Pre: G является направленным графом без циклов, реализованным с 
  непрерывным списком вершин и связными списками смежности.
  // Post: Процедура выполняет просмотр графа G в ширину и генерирует 
  результирующий топологический порядок в массиве T.
  // Uses: Использует пакет для обработки очередей.
  var
  predecessorcount: array [vertex] of integer; // число непосредственных
  предшественников каждой вершины 
  Q: queue; // вершины, готовые к размещению в порядке
  v, // вершина, посещаемая в настоящий момент
  succ: vertex; // одна из непосредственно следующих за v вершин
  curedge: pointedge; // просматривает список смежности для v
  place: integer; // следующая позиция в топологическом порядке 
  begin // процедура BreadthTopSort 
  for v := 1 to G.size do // инициализируем все счетчики предшественников 
  нулем 
  predecessorcount [v] := 0;
  for v := 1 to G.size do
  begin // увеличим отсчет предшественников для последующих вершин
  curedge := G.firstedge [v];
  while curedge <> nil do begin
  predecessorcount [curedge .endpoint] :=
  predecessorcount [curedge .endpoint] + 1;
  curedge := curedge .nextedge
  end
  end;
  CreateQueue(Q);
  for v := 1 to G.size do // поместим вершины, не имеющие предшественников, в
  очередь
  if predecessorcount [v] = 0 then
  Append(v, Q);
  place := 0; // начнем просмотр в ширину
  while not QueueEmpty(Q) do begin
  Serve(v, Q); // посетим вершину v, разместив ее в топологическом порядке 
  place := place + 1;
  T [place] := v;
  curedge := G.firstedge [v]; // просмотр следующих за v вершин 
  while curedge <> nil do begin //уменьшим отсчеты предшественников для 
  каждой следующей вершины 
  succ := curedge .endpoint;
  predecessorcount [succ] := predecessorcount [succ] –1;
  if predecessorcount [succ] =0 then // вершина succ не имеет следующих за ней, 
  поэтому она готова к обработке
  Append(succ, Q);
  curedge := curedge .nextedge
  end
  end
end; // процедура BreadthTopSort
```

### Ещё пару примеров
![image](https://github.com/mireashik/aood_3sem/assets/49165758/a3aa6688-fd92-4ffe-834d-ebc717c46f00)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/c00b27f6-46ad-4371-8318-bacb0fc5f9b4)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/dc90b48c-044d-4438-badb-e1048f0c1e8b)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/2a23c425-3f6e-4979-85cc-706fae93b21b)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/e5555e0e-ca1c-422e-8dd4-59e2d0b3644c)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/e74b5cdf-0f7e-4307-8472-acd6f87d5cdf)

Как только увидели вершину в которой нет рёбер:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/753d943e-6a1d-40a2-bb11-cebf5d0461b2)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/a3515df8-f349-4a75-8da1-8ee82a2d48f4)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/1afbbeb8-65d8-44d2-a4b9-104fc5168074)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/29d5ed51-9edb-439b-8de9-e6320c111ff0)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/a3c1ce19-dd71-4325-bb32-af04bac4265d)


### 3.4. Алгоритм экономного продвижения: кратчайшие маршруты
Дан ориентированный граф G, каждое ребро имеет вес (стоимость, время). Нужно найти кратчайший маршрут с минимальными весами. 

![image](https://github.com/mireashik/aood_3sem/assets/49165758/c3a62303-eabc-47e4-995f-8ee847547c7e)

Выбере ИСТОЧНИК - вершину 1. Наша задача в поиске мин. маршруте от вершины 1 к **КАЖДОЙ** вершине графа

Множества S -  вершины, для которых уже известно кратчайшее расстояние от 1
<br>
Таблица D - расстояния для каждой вершины от 1 до v

![image](https://github.com/mireashik/aood_3sem/assets/49165758/24fd5248-327b-4ca1-8642-1200cb36363d)

Множество S (покрашенные вершины), таблица D около каждой смежной вершины

![image](https://github.com/mireashik/aood_3sem/assets/49165758/45df4de2-3057-4adb-8fc5-11f26a1ccc76)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/3691f906-6170-4883-b8d3-45bd91930fc4)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/7b0b027e-eea0-4239-a290-aa5a986f318f)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/2978ae3a-57dd-4635-9012-1f9521d06db6)

Использование таблицы смежности обеспечивает произвольный доступ ко всем вершинам графа
<br>
К тому же таблица говорит не только о смежности, но и о весах

```c++
const
maxvertex = // должно быть предоставлено; максимальное число вершин в графе
infinity = maxint; 
type 
weight = integer;
counter = 0..maxvertex;
vertex = 1..maxvertex;
adjacencytable = array [vertex, vertex] of weight;
distancetable = array [vertex] of weight;
var
size: count; // число вершин в графе 
cost: adjacencytable; // описывает граф
D: distancetable; // кратчайшие расстояния от вершины 1
```

На входе - таблица смежности и число вершин в графе
<br>
На выходе - таблица минимальных расстояний

```c++
procedure Distance (size: counter; var cost: adjacencytable; var D: distancetable);
  // Расстояние
  // Pre: Дан направленный граф, имеющий size вершин с весами ребер, данными в таблице cost.
  // Post: Процедура находит кратчайший путь от вершины 1 к каждой вершине графа и возвращает найденный ею путь в массиве D. 
  var
  final: array [vertex] of Boolean; // Найдено ли окончательное расстояние от 1 до v? Значение final [v] равно true, если и только если v принадлежит множеству S. 
  i, // счетчик повторений для главного цикла
  // В каждом шаге цикла заканчивается обработка одного расстояния.
  w, // вершина, еще не добавленная в множество S 
  v: vertex; // вершина с минимальным пробным расстоянием в D [ ] }
  min: weight; // расстояние для v, равно D [v] 
  begin // процедура Distance
  final [1] := true; // инициализируем с единственной вершиной 1 в множестве S 
  D[1] := 0;
  for v := 2 to size do
  begin
  final [v] := false;
  D[v] :=cost [1, v]
  end;
  for i := 2 to size do
  begin // начнем главный цикл; на каждом шаге добавляем одну вершину v к S
  min := infinity; // найдем вершину, ближайшую к вершине 1
  for w := 2 to size do
  if not final [w] then
  if D[w] < min then
  begin
  v := w;
  min := D[w]
  end;
  final [v] := true; // добавим v к множеству S
  for w := 2 to size do // обновим оставшиеся расстояния в D
  if not final [w] then
  if min + cost [v, w] < D[w] then
  D[w] := min + cost [v, w]
  end
end; // процедура Distance
```

Пример списка смежности 

![image](https://github.com/mireashik/aood_3sem/assets/49165758/3226ec17-6b89-4be7-9526-7a6fcde4bf75) ![image](https://github.com/mireashik/aood_3sem/assets/49165758/8ab35200-c862-4f3e-aa4b-f8a58a9270a2)

```c++
STL
#include <iostream>
#include <vector>
using namespace std;
// Структура данных для хранения ребра Graph
struct Edge {
int src, dest;
};
// Класс для представления graphического объекта
class Graph {
  public:
  // вектор векторов для представления списка смежности
  vector<vector<int>> adjList;
  // Конструктор Graphа
  Graph(vector<Edge> const &edges, int n) {
    // изменить размер вектора, чтобы он содержал `n` элементов типа `vector<int>`
    adjList.resize(n);
    // добавляем ребра в ориентированный graph
    for (auto &edge: edges) {
      // вставляем в конце
      adjList[edge.src].push_back(edge.dest);
      // раскомментируйте следующий код для неориентированного Graph
      // adjList[edge.dest].push_back(edge.src);
    }
  }
};
```

```c++
// Функция для печати представления списка смежности Graph
void printGraph(Graph const &graph, int n) {
  for (int i = 0; i < n; i++) {
  // вывести номер текущей вершины
  cout << i << " ——> ";
  // вывести все соседние вершины вершины `i`
  for (int v: graph.adjList[i]) {
  cout << v << " ";
  }
  cout << endl;
  }
}
```

```c++
// Реализация Graph с использованием STL
int main() {
  // vector ребер Graph согласно схеме выше.
  // Обратите внимание, что vector инициализации в приведенном ниже формате 
  будет
  // нормально работает в C++11, C++14, C++17, но не работает в C++98.
  vector<Edge> edges = {
    {0, 1}, {1, 2}, {2, 0}, {2, 1}, {3, 2}, {4, 5}, {5, 4}
  };
  // общее количество узлов в Graph (от 0 до 5)
  int n = 6;
  // построить Graph
  Graph graph(edges, n);
  // вывести представление списка смежности Graph
  printGraph(graph, n);
  return 0;
}
```

### Выводы
Алгоритмы обхода графов. Основными алгоритмами обхода графов являются:
1. Поиск в ширину.
2. Поиск в глубину.

Поиск в ширину подразумевает поуровневое исследование графа

Каждая вершина может находиться в одном из 3 состояний:
0 ‒ оранжевый – необнаруженная вершина;
1 ‒зеленый – обнаруженная, но не посещенная вершина;
2 ‒ серый – обработанная вершина.
Фиолетовый – рассматриваемая вершина.

```c++
#include <iostream>
#include <queue> // очередь
using namespace std;
int main() {
  queue<int> Queue;
  int mas[7][7] = { { 0, 1, 1, 0, 0, 0, 1 }, // матрица смежности
  { 1, 0, 1, 1, 0, 0, 0 },
  { 1, 1, 0, 0, 0, 0, 0 },
  { 0, 1, 0, 0, 1, 0, 0 },
  { 0, 0, 0, 1, 0, 1, 0 },
  { 0, 0, 0, 0, 1, 0, 1 },
  { 1, 0, 0, 0, 0, 1, 0 } };
  
  int nodes[7]; // вершины графа
  for (int i = 0; i < 7; i++)
    nodes[i] = 0; // исходно все вершины равны 0
  Queue.push(0); // помещаем в очередь первую вершину
  while (!Queue.empty()) { // пока очередь не пуста
    int node = Queue.front(); // извлекаем вершину
    Queue.pop();
    nodes[node] = 2; // отмечаем ее как посещенную
    for (int j = 0; j < 7; j++) { // проверяем для нее все смежные вершины
      if (mas[node][j] == 1 && nodes[j] == 0) { // если вершина смежная и не обнаружена
      Queue.push(j); // добавляем ее в очередь
      nodes[j] = 1; // отмечаем вершину как обнаруженную
      }
    }
    cout << node + 1 << endl; // выводим номер вершины
  }
  cin.get();
  return 0;
}
```

### Задача поиска кратчайшего пути
```c++
#include <iostream>
#include <queue> // очередь
#include <stack> // стек
using namespace std;
struct Edge {
 int begin;
 int end;
};

int main() {
  system("chcp 1251");
  system("cls");
  queue<int> Queue;
  stack<Edge> Edges;
  int req;
  Edge e;
  int mas[7][7] = {
  { 0, 1, 1, 0, 0, 0, 1 },
  { 1, 0, 1, 1, 0, 0, 0 },
  { 1, 1, 0, 0, 0, 0, 0 },
  { 0, 1, 0, 0, 1, 0, 0 },
  { 0, 0, 0, 1, 0, 1, 0 },
  { 0, 0, 0, 0, 1, 0, 1 },
  { 1, 0, 0, 0, 0, 1, 0 }
  };
  
  int nodes[7]; // вершины графа
  for (int i = 0; i < 7; i++) // исходно все вершины равны 0
    nodes[i] = 0;
  cout << "N = "; cin >> req; req--;
  Queue.push(0); // помещаем в очередь первую вершину
  while (!Queue.empty()){
    int node = Queue.front(); // извлекаем вершину
    Queue.pop();
    nodes[node] = 2; // отмечаем ее как посещенную
    for (int j = 0; j < 7; j++) {
      if (mas[node][j] == 1 && nodes[j] == 0) { // если вершина смежная и не обнаружена
        Queue.push(j); // добавляем ее в очередь
        nodes[j] = 1; // отмечаем вершину как обнаруженную
        e.begin = node; e.end = j;
        Edges.push(e);
        if (node == req)
          break;
      }
    }
    cout << node + 1 << endl; // выводим номер вершины
  }
  cout << "Путь до вершины " << req + 1 << endl;
  cout << req + 1;
  while (!Edges.empty()) {
    e = Edges.top();
    Edges.pop();
    if (e.end == req) {
      req = e.begin;
      cout << " <- " << req + 1;
    }
  }
  cin.get();
  cin.get();
  return 0;
}
