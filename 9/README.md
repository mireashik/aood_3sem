## АЛГОРИТМЫ ПОИСКА КРАТЧАЙШЕГО ПУТИ
**Алгоритма поиска кратчайшего пути** - последовательность ребер, соединяющая заданные две вершины и имеющая наименьшую длину среди всех таких последовательностей.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/f9864aa3-6c61-4ec6-baed-cf3859e4bbc7)

Алгоритм построения минимального остовного дерева выберет все ребра веса 1, отбросив единственное ребро веса 2:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/2b39c716-afb4-471a-b680-7f8ba09da2aa)

Ясно, что он не является кратчайшим, поскольку в исходном графе вершины А и В соединены ребром длины 2 (задача о дилижансе)
<br>
GPS-навигаторах

1. Алгоритм Дейкстры. Кратчайший путь от 1 до всех остальных (только для положительных весов)
2. Алгоритм Беллмана-Форда. От 1 вершины графа до всех остальных (вес может быть отрицательным)
3. Алгоритм поиска A*. (алгоритм поиска по первому наилучшему совпадению на графе)
4. Алгоритм Флойда-Уоршелла. Кратчайшие пути между всеми вершинами
5. Алгоритм Джонсона. Кратчайшие пути между всеми парами вершин 
6. Алгоритм Ли (волновой алгоритм). Поиска в ширину (минимальное количество промежуточных вершин / рёбер)
7. Алгоритм Килдала

### 1.2. Алгоритм Дейкстры
Кратчайшие пути от 1 вершины до всех остальных.
<br>
Оригинальный алгоритм Дейкстры - был только путь между 2 узлами
<br>
распространенный вариант фиксирует один узел как «исходный» - создаёт дерево кратчайших путей

Метка исходной вершины a полагается равной 0, метки остальных вершин ‒ бесконечности.
<br>
Если все вершины посещены, алгоритм завершается.

Смежные вершины выбираются по весу, в начале проходятся все вершины по весу начиная с исходной вершины.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/604d5ad3-4925-4685-a5ab-6c6ac3975943)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/581fdb7f-0eb4-4747-8f65-ebe9cae5411a)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/56ce9011-2b2a-4b03-9217-6989146cbb3e)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/53b7a042-11e9-4172-bf35-f825bd1e6173)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/7528991f-db5d-4bfe-844b-0d30a33df8ee)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/cc0ab59d-9ba2-4d92-9850-62d93be6f83d)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/09768965-4d1b-4acf-b3bf-6a5d25a4bf65)

Игнорируем плохие маршруты:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/8fbd50e0-e310-4848-9ff5-a4cc504987fb)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/92201727-edb0-4a1d-abcc-b45ec0091606)

работа алгоритма Дейкстры завершится

- 1→1=0
- 1→2=1
- 1→3=4
- 1→4=10
- 1→5=2
- 1→6=10

### Реализация Алгоритма Дейкстры на С++
Для программной реализации алгоритма понадобиться 2 массива: 
- логический visited – для хранения информации о посещенных вершинах
- численный distance, в который будут заноситься найденные кратчайшие пути

```c++
#include "stdafx.h"
#include <iostream>
using namespace std;
const int V=6;
//алгоритм Дейкстры
void Dijkstra(int GR[V][V], int st) {
  int distance[V], count, index, i, u, m=st+1;
  bool visited[V];
  for (i=0; i<V; i++) {
    distance[i]=INT_MAX; visited[i]=false;
  }
  distance[st]=0;
  for (count=0; count<V-1; count++) {
    int min=INT_MAX;
    for (i=0; i<V; i++)
    if (!visited[i] && distance[i]<=min) {
      min=distance[i]; index=i;
    }
    u=index;
    visited[u]=true;
    for (i=0; i<V; i++)
      if (!visited[i] && GR[u][i] && distance[u]!=INT_MAX && distance[u]+GR[u][i]<distance[i])
        distance[i]=distance[u]+GR[u][i];
  }
  cout<<"Стоимость пути из начальной вершины до остальных:\t\n";
  for (i=0; i<V; i++) if (distance[i]!=INT_MAX)
  cout<<m<<" > "<<i+1<<" = "<<distance[i]<<endl;
  else cout<<m<<" > "<<i+1<<" = "<<"маршрут недоступен"<<endl;
}
//главная функция
void main() {
  setlocale(LC_ALL, "Rus");
  int start, GR[V][V]={
  {0, 1, 4, 0, 2, 0},
  {0, 0, 0, 9, 0, 0},
  {4, 0, 0, 7, 0, 0},
  {0, 9, 7, 0, 0, 2},
  {0, 0, 0, 0, 0, 8},
  {0, 0, 0, 0, 0, 0}};
  cout<<"Начальная вершина >> "; cin>>start;
  Dijkstra(GR, start-1);
  system("pause>>void");
}
```

### 2.3. Алгоритм Беллмана-Форда
От выделенной вершины-источника до всех остальных, применимость к графам с произвольными, в том числе **отрицательными** весами.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/9cc29d8a-d479-48dd-9081-04d8f99b95e1)

Все исходящие ребра записываются в таблице в алфавитном порядке:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/d8b93609-b7f5-403a-bf80-f61e0b600229)

Далее создаётся таблица - расстояние до каждой вершины и предыдущая вершина. Расстояние обозначено переменной d, а предыдущая вершина ‒ переменной π

![image](https://github.com/mireashik/aood_3sem/assets/49165758/715d2ac1-21c1-42d0-8e5c-fcf0820bd5fc)

путь через все рёбра. Всего рёбер 9, поэтому путь этот будет насчитывать до 9 итераций

![image](https://github.com/mireashik/aood_3sem/assets/49165758/bfe9a675-e125-4b00-b83a-fd98b145bcb2)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/4c3c2d18-3268-4925-828c-0e710dc5c663)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/90ccf042-0cca-4d6b-99f1-3b27fb73c938)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/2dc00d1d-e59c-4284-b370-1977eb3dc2c7)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/c5e4a66a-e4b6-497c-9e7a-a864c0d712a6)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/c922226c-78f8-4875-abb9-5b3403379bdf)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/c16e8b6e-ce44-402b-9eef-6bf207691e4f)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/d9853c5f-ae59-49d2-97f7-0caec7fe1603)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/27bd31a6-7bbf-4deb-9f82-5663b10cafde)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/d0a91b6c-ed99-40bf-9596-0a87f2481a05)

Если бы в этом графе существовал отрицательный цикл, то после $n-1$ итераций **алгоритм Беллмана-Форда** теоретически должен был бы найти кратчайшие пути ко всем вершинам

![image](https://github.com/mireashik/aood_3sem/assets/49165758/5395417b-43f4-46d0-a467-21c3b7fb5285)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/d73d5487-ff63-465e-b569-3d7056c4920c)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/29862b53-6cf9-4e19-8f91-60e5465ad980)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/45674637-e258-4407-8694-6a04212cfd32)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/bd6e457b-5449-4bcb-8bef-cf45fdab45be)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/8a9742e0-927d-40ea-b870-90e2c053bb0e)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/807ba2c2-da69-490d-9044-8bd3c9a8a190)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/b4effb77-be59-480c-8937-edd76478aad0)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/a16cdb17-a5e2-47b6-b99d-df707df6940c)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/ddbddd6a-fdd0-4c2f-a794-2c4045dde149)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/e435906a-3402-49b7-abc2-83d7b70185f6)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/763ea92e-120b-4b50-8032-7f80616d74ab)

```c++
#include "stdafx.h"
#include <iostream>
#define inf 100000
using namespace std;
struct Edges {
  int u, v, w;
};
const int Vmax=1000;
const int Emax=Vmax*(Vmax-1)/2;
int i, j, n, e, start;
Edges edge[Emax];
int d[Vmax];
//алгоритм Беллмана-Форда
void bellman_ford(int n, int s) {
  int i, j;
  for (i=0; i<n; i++) d[i]=inf;
  d[s]=0;
  for (i=0; i<n-1; i++)
  for (j=0; j<e; j++)
  if (d[edge[j].v]+edge[j].w<d[edge[j].u])
  d[edge[j].u]=d[edge[j].v]+edge[j].w;
  for (i=0; i<n; i++) if (d[i]==inf)
  cout<<endl<<start<<"->"<<i+1<<"="<<"Not";
  else cout<<endl<<start<<"->"<<i+1<<"="<<d[i];
}
//главная функция
void main() {
  setlocale(LC_ALL, "Rus");
  int w;
  cout<<"Количество вершин > "; cin>>n;
  e=0;
  for (i=0; i<n; i++)
  for (j=0; j<n; j++) {
    cout<<"Вес "<<i+1<<"->"<<j+1<<" > "; cin>>w;
    if (w!=0) {
      edge[e].v=i;
      edge[e].u=j;
      edge[e].w=w;
      e++;
    }
  }
  cout<<"Стартовая вершина > "; cin>>start;
  cout<<"Список кратчайших путей:";
  bellman_ford(n, start-1);
  system("pause>>void");
}
```

## ЗАДАЧА О МАКСИМАЛЬНОМ ПОТОКЕ
Нахождение потока по транспортной сети - сумма потоков из истока, или сумма потоков в сток **максимальна**.

Выделяются 2 вершины: 
- источник s;
- сток t.

Каждое ребро (u,v) ∈ E имеет **неотрицательную** пропускную способность

![image](https://github.com/mireashik/aood_3sem/assets/49165758/dbe58a3d-e8fc-49c5-9a47-4616e9635dfa)

Найти такой поток, где величина потока максимальна

Существуют различные алгоритмы решения задачи поиска максимального потока:
- **Линейное программирование**. Переменные - потоки по рёбрам, ограничения ‒ сохранение потока и ограничение пропускной способности. Сложность зависит от конкурентного алгоритма
- **Алгоритм Форда-Фалкерсона**. Находим любой увеличивающий путь. Увеличить поток по всем его рёбрам на минимальную из их остаточных пропускных способностей. Повторять, пока увеличивающий путь есть.
- **Алгоритм Эдмондса-Карпа**. Каждый раз выбирая кратчайший увеличивающий путь
- **Алгоритм Диница**. Усовершенствование алгоритма Эдмондса-Карпа (но хронологически был найден раньше), поиск в ширину, определяется расстояние от источника до всех вершин в остаточной сети
- **Алгоритм проталкивания предпотока**. Вместо потока алгоритм работает с предпотоком.
- **Алгоритм «поднять в начало»**.

### 2.2. Алгоритм Форда-Фалкерсона
Изначально величине потока присваивается значение 0
<br>
Затем величина потока итеративно увеличивается посредством поиска увеличивающего пути

Если искать не любой путь, а **кратчайший**, тол получится алгоритм **Эдмондса-Карпа**

- ШАГ 1. Обнуляем все потоки. Остаточная сеть изначально совпадает сисходной сетью.
- ШАГ 2. В остаточной сети находим **любой** путь из источника в сток. Если такого пути нет, останавливаемся.
- ШАГ 3. Пускаем через найденный путь (он называется увеличивающим путём или увеличивающей цепью) максимально возможный поток:
- - 3.1. На найденном пути в остаточной сети ищем ребро с **минимальной** пропускной способностью.
- - 3.2. Для каждого ребра на найденном пути увеличиваем поток на cmin, а в противоположном ему ‒ уменьшаем на cmin.
- - 3.3. Модифицируем остаточную сеть. Для всех рёбер на найденном пути, а также для противоположных (антипараллельных) им рёбер, вычисляем новую пропускную способность. Если она стала ненулевой, добавляем  ребро к остаточной сети, а если обнулилась, стираем его.
- ШАГ 4. Возвращаемся на шаг 2.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/2cebc021-8b8b-4879-a6f2-4b6e731baf76)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/2214ed94-3c10-4c28-be17-a81082bcb5c5)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/6ae55d3d-a128-4d16-a0a1-c65233af88b2)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/a957fe0a-ebb0-4cb4-b27c-cc01c9da75ed)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/39e86253-8080-4034-9c6b-2cb46cc7c3e0)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/f7ee17fb-2c58-4ead-8866-41c8cff4aff5)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/360eabfc-2ea8-4283-8c71-3e982abbfd7d)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/6ab572cd-f0f0-48f6-b831-d164179d7263)

ответом к поставленной задаче будет служить сумма потоков всех найденных увеличивающихся путей. Ответ: 10 ед.

## ЗАДАЧА ПОИСКА СИЛЬНОСВЯЗНЫХ КОМПОНЕНТ В ОРИЕНТИРОВАННОМ ГРАФЕ
![image](https://github.com/mireashik/aood_3sem/assets/49165758/92fb4db8-6299-4a7c-9fd3-d7e94764e7ac)

Компонентой сильной связности

![image](https://github.com/mireashik/aood_3sem/assets/49165758/16e9148a-7efb-4b9d-bc8f-cb329731c254)

3 алгоритма, решающих данную задачу за линейное время, то есть в V раз быстрее, чем приведённый выше алгоритм:
- алгоритм Косарайю;
- алгоритм поиска компонент сильной связности с двумя стеками;
- алгоритм Тарьян

### алгоритм Косарайю
![image](https://github.com/mireashik/aood_3sem/assets/49165758/0260c34f-3f4e-4585-9b7c-04d398294e4d)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/cfe19719-1895-48d8-956b-740cb2b94fd3)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/09f84252-033d-43be-90ab-b159ebf4bd39)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/58721593-6ca5-414f-a1f1-59e64eca1477)

У вершины 2 нет соседей. Поэтому нам остаётся лишь рекурсивно вернуться в предыдущую вершину:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/5b7679a8-82fc-4928-8b62-9bbe580b97dd)

Начиная новый такт:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/b1162c7f-4c28-4552-97b0-52d496dede69)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/55c55115-42a7-4efc-90ff-e6f6e1d3ec7e)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/81003f01-9b54-43f9-b57b-5926df06bb2d)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/2e901600-067c-4e63-a44d-0b95d9b5925c)

Алгоритм поиска в глубину завершён
