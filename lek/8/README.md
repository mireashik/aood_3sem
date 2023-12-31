## АЛГОРИТМЫ ПОИСКА МИНИМАЛЬНОГО ОСТОВНОГО ДЕРЕВА
## 1.1. Остовное дерево

![image](https://github.com/mireashik/aood_3sem/assets/49165758/14b57cb0-8d96-4fe7-a766-713f134bd015)

Минимальное остовного дерева ‒ остовного дерева с минимальным возможным весом

![image](https://github.com/mireashik/aood_3sem/assets/49165758/7ba3eb37-909c-4ec6-b710-1b751330e869)

1. Минимальный остов **УНИКАЛЕН**, если веса всех рёбер различны (иначе может существовать несколько минимальных остовов)
2. Минимальный остов является также и остовом с минимальным **произведением** весов рёбер
3. Минимальный остов является также и остовом с минимальным весом самого **тяжелого** ребра
4. Остов **МАКСИМАЛЬНОГО** веса ищется аналогично остову МИНИМАЛЬНОГО веса,

На задачу о нахождении минимального остовного дерева похожа ЗАДАЧА о **дереве Штейнера** - несколько точек на плоскости с мин. суммой длин путей (однако там разрешается добавлять дополнительные точки ветвления)

Типичное применение остовных деревьев минимальной стоимости можно найти при разработке коммуникационных сетей

Для нахождения минимального остовного дерева графа существуют 4 алгоритма:
- Алгоритм Прима (нередко в литературе встречается название этого алгоритма – **алгоритм Дейкстры-Прима**)
- Алгоритм Краскала (или алгоритм Крускала)
- Алгоритм Борувки
- Алгоритм обратного удаления (получение минимального остовного  дерева из связного рёберно взвешенного графа)

алгоритм Прима и алгоритм Крускала частные случаи алгоритма Борувки, все они для **неориентированных** графов

### 1.2. Расширение кругозора
### 1.2.1. Жадный алгоритм
Перед тем как рассмотреть алгоритмы поиска минимального остовного дерева, рассмотрим жадный алгоритм. 

Чтобы не стрелять наугад и не искать лучший выбор, в **ЖАДНОМ** алгоритме выбирается лучший выбор на **текущий** момент. И мы надеемся что этот **локальный** выбор приведёт глобально к лучшему.
<br>
**Жадные** алгоритмы **не всегда** приводят к оптимальному решению, но во многих задачах они дают нужный результат.

1. жадный выбор на первом шаге не закрывает пути к оптимальному решению
2. подзадача на первом шаге аналогична исходной

**Оптимальное решение задачи** - это оптимальные решения для всех её подзадач.

### 1.2.2. Динамическое программирование
**Алгоритм Флойда** (мин. путь между всеми вершинами) - не жадный алгоритм, он использует динамическое программирование.
<br>
Динамическое программирование - решение сложной задачи путём разбиения их на более простые подзадачи

Метод программирования сверху ‒ запоминание результатов подзадач, которые могут повторно встретиться далее
<br>
Метод программирования снизу - переформулирование сложной задачи в виде рекурсии более простых подзадач

## 1.3. Алгоритм Дейкстры-Прима
### 1.3.1. Описание алгоритма
Каждый шаг - выбираем из множества рёбер, ребро с минимальным весом

Разобьем вершины графа на 3 класса: 
- ВЕРШИНЫ, вошедшие в уже построенную часть дерева
- ВЕРШИНЫ, окаймляющие построенную часть
- ВЕРШИНЫ еще не рассмотренные

Начнем с произвольной вершины графа и включим ее в остовное дерево (выбор исходной вершины не влияет на результат)
<br>
Все вершины, соединенные с данной, заносим в **КАЙМУ**
<br>
Цикл поиска ребра с наименьшим весом
<br>
Это ребро вместе с новой вершиной добавляется в дерево и происходит обновление КАЙМЫ

Допустим начальная вершина будет А:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/ab9d0362-1a46-4fe6-98c9-e050b67f9ea1)

Все вершины, непосредственно связанные с А:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/6f173c66-4c4a-4983-b493-6f6cd0979a16)

Миниальное ребро с B, добавляем его в кайму:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/34985588-61ee-44f3-9dea-9cdb3d5dc9ff)

Из 5 рёбер минимальный вес BE (3):

![image](https://github.com/mireashik/aood_3sem/assets/49165758/940d78a2-1272-4ad4-b731-fabd0b4fff82)

Теперь смотрим вершину А, там минимальный вес 4:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/044969a1-5b40-4846-84ec-e3a97566c246)

Далее вершина F:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/d6fe5c1a-eb9d-47ba-812f-cd063fc5ed41)

Добавляем вершину D:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/4b51e163-c4ab-4032-a5ea-5e14e31fe534)

Осталось одна вершина G:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/7094034a-1e03-404d-9a89-d96c8d9a2491)

### 1.3.2 Реализации алгоритма Дейкстры-Прима с использованием языка программирования С++
**Случай плотных графов или алгоритм за $O(n^2)$**

**Плотный граф **– граф, в котором число рёбер E близко к максимально возможному:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/9c8014d3-e545-47bf-a3e1-2762fa4e0217)

Полный граф ‒ простой неориентированный граф, в котором каждая пара различных вершин смежна

Реализация алгоритма Прима для графа, заданного матрицей смежности:
```c++
// входные данные
int n; // На вход подаются число вершин n
vector < vector<int> > g; // и матрица g[i,j] размера 𝒏 × m
const int INF = 1000000000; // значение "бесконечность"
// алгоритм
vector<bool> used (n); // флаг used[i]=true означает, что вершина i включена в остов
// величина min_e[i] хранит вес наименьшего допустимого ребра из вершины i
// элемент sel_e[i] содержит конец этого наименьшего ребра 
vector<int> min_e (n, INF), sel_e (n, -1);
min_e[0] = 0;
for (int i=0; i<n; ++i) {
  int v = -1;
  for (int j=0; j<n; ++j)
    if (!used[j] && (v == -1 || min_e[j] < min_e[v]))
  v = j;
  if (min_e[v] == INF)  {
    cout << "No MST!";
    exit(0);
  }
  used[v] = true;
  if (sel_e[v] != -1)
  cout << v << " " << sel_e[v] << endl;
  for (int to=0; to<n; ++to)
    if (g[v][to] < min_e[to]) {
      min_e[to] = g[v][to];
      sel_e[to] = v;
    }
}
```

**Случай разреженных графов или алгоритм за O(m log n)**
```c++
// входные данные
int n;
vector < vector < pair<int,int> > > g;
const int INF = 1000000000; // значение "бесконечность"
// алгоритм
vector<int> min_e (n, INF), sel_e (n, -1);
min_e[0] = 0;
set < pair<int,int> > q;
q.insert (make_pair (0, 0));
for (int i=0; i<n; ++i) {
  if (q.empty()) {
    cout << "No MST!";
    exit(0);
  }
  int v = q.begin() -> second;
  q.erase (q.begin());
  if (sel_e[v] != -1)
    cout << v << " " << sel_e[v] << endl;
  for (size_t j=0; j<g[v].size(); ++j) {
    int to = g[v][j].first,
    cost = g[v][j].second;
    if (cost < min_e[to]) {
      q.erase (make_pair (min_e[to], to));
      min_e[to] = cost;
      sel_e[to] = v;
      q.insert (make_pair (min_e[to], to));
    }
  }
}
```

Рассмотрим ещё одну реализацию алгоритма Прима.
<br>
Для нахождения ближайшей вершины воспользуемся очередью с приоритетом, в которой будем хранить пары (расстояние от остова до вершины, номер вершины)

```c++
include <bits/stdc++.h>
using namespace std;
const int INF = 1e9 + 7;
vector<pair<int, int>> graph[100000];
bool used[100000]; //включили ли мы соответствующую вершину в остов
int main() {
  //Ввод графа...
  int mst_weight = 0; //Текущий вес остова.
  priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> 
  q;
  q.push({0, 0}); //Начнём с вершины 0.
  while (!q.empty()) {
    pair<int, int> c = q.top();
    q.pop();
    int dst = c.first, v = c.second;
    if (used[v]) { //вершина уже добавлена в остов
      continue;
    }
    used[v] = true;
    mst_weight += dst;
    for (pair<int, int> e: graph[v]) {
      int u = e.first, len_vu = e.second;
      if (!used[u]) {
        q.push({len_vu, u}); //Заметьте: мы учитываем только длину ребра.
      }
    }
  }
  cout << "Minimum spanning tree weight: " << mst_weight << endl;
}
```

## 1.4. Алгоритм Крускала
### 1.4.1. Описание алгоритма
Алгоритм Дейкстры-Прима начинает с конкретной вершины, **алгоритм Крускала** делает упор на рёбрах графа

Алгоритм Крускала изначально помещает каждую вершину в своё дерево, а затем постепенно объединяет эти деревья, **рёбра** сортируются по весу (в порядке возрастания)
<br>
Если ребра закончатся до всех вершин, значит исходный граф - несвязный

![image](https://github.com/mireashik/aood_3sem/assets/49165758/1cb0ff27-2c69-4289-8e33-a95f31cf512d)

Начнём с ребра наименьшего веса 1:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/fb52b3b2-9e62-4993-a879-2e390c0f19b2)

Следующим добавляется ребро имеющее вес 2:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/95428c06-c16f-4d32-8e75-f0e6b5e007dd)

Добавляем ребро, имеющее вес 3:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/68c504ed-0386-4ac0-bb6c-3e8276d44df9)

И так далее:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/ae30479c-f120-4829-a91b-37e21f802a27)

Неприсоединённой осталась лишь вершина G. Но какое ребро выбрать? Некоторые рёбра приведут к циклу - **отбросим** их. Однако есть 2 ребра которые не создаст **циклов**, выбираем любое из них:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/e34564a0-1230-4fa8-8235-78f4a118581a)

**Лемма о безопасном ребре**

**Безопасный остов** - подграф без циклов, который можно дополнить, добавляя (но не удаляя!) в него рёбра, до некоторого минимального остовного дерева (миностова)
<br>
**Безопасным ребром** для безопасного остова мы будем называть ребро, добавление  которого сохраняет безопасность.

```c++
edgeCount=l
  while edgeCount<=E and includedCount<=N-l do 
   parentl=FindRoot(edge[edgeCount] .start)
   parent2=FindRoot(edge[edgeCount].end)
   if parentl/=parent2 then 
   добавить edge[edgeCount] в остовное дерев
   includedCount=includedCount=l Union(parent1,parent2)
   end if
   edgeCount=edgeCount+l
end while
```

### 1.4.2 Реализации алгоритма Крускала с использованием языка программирования С++
<br>
Простейшая реализация

```c++
int m;
vector < pair < int, pair<int,int> > > g (m); // вес - вершина 1 - вершина 2
int cost = 0;
vector < pair<int,int> > res;
sort (g.begin(), g.end());
vector<int> tree_id (n);
for (int i=0; i<n; ++i)
tree_id[i] = i;
for (int i=0; i<m; ++i) {
  int a = g[i].second.first, b = g[i].second.second, l = g[i].first;
  if (tree_id[a] != tree_id[b]) {
    cost += l;
    res.push_back (make_pair (a, b));
    int old_id = tree_id[b], new_id = tree_id[a];
    for (int j=0; j<n; ++j)
    if (tree_id[j] == old_id)
    tree_id[j] = new_id;
  }
}
```

## 1.5. Алгоритм Борувки
### 1.5.1. Описание алгоритма
Исторически первый алгоритм для построения MST, не хуже более поздних

На каждом шаге для каждой вершины - выбирается ребро наименьшего веса. Некоторые рёбра при этом выбираются дважды, а некоторые лишь один раз. Все эти рёбра добавляются в остовное дерево, а в исходном графе все они стягиваются

![image](https://github.com/mireashik/aood_3sem/assets/49165758/0ca655f8-650e-4089-bc62-b0a00b805e9e)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/a8dd95d3-40da-407b-b468-b8aeb37ab99e)

Строится минимальный покрывающий лес, состоящий только из вершин, каждая из которых является КОМПОНЕНТОЙ СВЯЗНОСТИ

![image](https://github.com/mireashik/aood_3sem/assets/49165758/290b3502-d3ad-43f5-b6e5-15b20f19cce2)

Для каждой компоненты находим рёбра минимального веса:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/87af7b2b-0a91-434b-ba40-d3fcfd1480d4)

Добавляем найденные рёбра к минимальному оставному дереву:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/ec97266a-a503-4122-a61e-0c64f24c79a6)

Снова находим рёбра минимального веса:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/046c3d46-8db9-4649-acb0-1f9da6ff8754)

Добавляем:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/6b56657f-7eaf-401a-b741-a8daf3ba8d7b)

Расчёт окончен. Получилось 1 компонента связности. Осталось подсчитать минимальный остовный вес:
<br>
<Н1,Н2>+<Н2,Н5>+<Н3,Н5>+<Н5,Н4>+<Н5,Н7>+<Н4,Н6>+<Н4,П> = 4+4+3+2+5+5+2 = 25

![image](https://github.com/mireashik/aood_3sem/assets/49165758/67b0f4d3-0e0f-4f99-9b5d-ee5fbe79d553)

### 1.5.2. Реализация Алгоритм Борувки
```c++
1: function MST(Input_matrix)
2: Result = ∅
3: М = Input_matrix
4: E = MATRiX_NVALS(М)
5: N = MATRiX_NROWS(М)
6: v1 = VECTOR_BUiLD([0..N-1])
7: while E ̸= 0 do
8: (w, v2) = MXV(M, v1, min, (,))
9: for all i ∈ [0..N-1] do
10: v1[i].pointer = v2[i]
11: for all i ∈ [0..N-1] do
12: if v1[i].pointer == (v1[i].pointer).pointer then
13: super = super ∪ MiN(v1[i], v1[i].pointer)
14: Result = Result ∪ SELECT(M, select_edge(v1, v2))
15: (w, v2) = MXV(Result, v1, min, (,))
16: Result = MATRiX_BUiLD(v1, v2, w)
17: for all v ∈ super do
18: for all u ∈ СOMPONENT(v) do
19: u.pointer = v
20: SELECT(M, diff_components())
21: E = MATRiX_NVALS(М)
22: return Result
```

### 1.5.2. Реализация Алгоритм Борувки
Впервые алгоритм появился в статье Краскала, но не следует его путать с алгоритмом Краскала, который появился в той же статье.

Алгоритм является **жадным** алгоритмом, дающим лучшее решение.
<br>
Он противоположен алгоритму Краскала, который является другим жадным алгоритмом поиска минимального остовного дерева

Алгоритм Краскала начинает с ПУСТОГО графа и добавляет РЁБРА
<br>
**Алгоритм обратного удаления** начинает с ИСХОДНОГО графа и УДАЛЯЕТ рёбра из него

Проходим через E в порядке убывания веса рёбер. Для каждого ребра проверяем, не приводит ли его удаление к несвязному графу. Удаляем рёбра если граф связный.

```c++
1 функция ReverseDelete(рёбра[] E)
2 сортируем E в убывающем порядке
3 Определяем индекс i ← 0
4 пока i < размер(E)
5 Определяем ребро ← E[i]
6 удаляем E[i]
7 если граф не связен
8 E[i] ← ребро
9 i ← i + 1
10 возвращаем рёбра[] E
```

Алгоритм работает за время $O(E log V (log log V )3^)$

ЗЕЛЁНЫМ цветом - ребра просматриваются алгоритмом
<br>
КРАСНЫЕМ цветом - ребра, которые алгоритмом удалены

![image](https://github.com/mireashik/aood_3sem/assets/49165758/1b7f5133-abeb-4604-9b13-e1afd4aa7b17)

Работа алгоритма начинается с самого тяжелого веса:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/54ced448-4898-49d3-bb5a-af1e901401b1)

Поскольку удаление ребра DE не нарушает связность графа, алгоритм его удаляет:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/e03ab2e8-a72c-4bcf-ad82-acdb7f9bc7a5)

Следующим самым ребром графа с самым большим весом является ребро BD:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/352c5778-6d70-4641-93ba-1d57a54152cb)

Следующим ребром, обладающим самым большим весом, является ребро EG вес 9, однако граф будет несвязный, поэтому берем вес 8:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/4dd31c0f-a9df-40cc-bebc-035cdaccb994)

Следующим ребром с самым большим весом является ребро EF, вес = 8:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/b148e1d6-e9c8-4189-8571-c5c57de4db7d)

Просмотр показывает, что оставшиеся рёбра не пригодны для удаления, поскольку их удаление приведёт нарушению связности графа
<br>
окончательный вариант:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/7c8c55fd-e8ce-4783-a53a-14b6fe00ffd7)

## АЛГОРИТМЫ ПОИСКА МИНИМАЛЬНОГО ОСТОВНОГО ДЕРЕВА В ОРИЕНТИРОВАННОМ ГРАФЕ
Рассмотренные нами алгоритмы поиска минимального остовного дерева правильно работают для взвешенных, но исключительно **неориентированных** графов. 
<br>
Как быть в ориентированных графах?

### Алгоритм Эдмондса (Чу‒Лью/Эдмондса)
Поиск минимального остовного дерева во взвешенном ориентированном графе с корнем в заданной вершине

Для каждой вершины (кроме корня) найдем ребро, которое будет входить в неё в ответе.
<br>
Для каждой вершины (кроме корня) найдем минимальное ребро, которое в неё входит и вычтем его вес из всех ребер, входящих в неё
<br>
В новом графе для каждой вершины (кроме корня) зафиксируем одно ребро нулевого веса

![image](https://github.com/mireashik/aood_3sem/assets/49165758/3878f61b-8d06-40c0-a3a0-a51ad40e2bf5)

Для каждой вершины исходного графа G найдём ребро минимального веса. 

- Для вершины А=>m(A)=1 – минимальный вес ребра, входящего в вершину А.
- Для вершины B=>m(B)=1 – минимальный вес ребра, входящего в вершину B.
- Для вершины C=>m(C)=1 – минимальный вес ребра, входящего в вершину C
- Для вершины D=>m(D)=1 – минимальный вес ребра, входящего в вершину D.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/398704a2-ad94-46d0-ac78-0efb763581bb)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/50386e68-9cc1-4d0a-8608-5424842b785c)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/f2348708-4951-4e36-8482-388bed1b21cc)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/ae14403f-1323-4eab-b45e-341f3027260a)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/3792f1cf-7797-4582-bbcf-a125f1f1f130)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/9a96ca57-aabc-4090-b8e1-ec8dc5796589)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/3a76f309-d3d2-49eb-b736-6f2b8296cf9a)
