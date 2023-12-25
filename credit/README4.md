### 66. Поиск: основные понятия и определения. Классификация методов поиска.
конечное множество $T$ из $n$ элементов, которое будем называть **ТАБЛИЦЕЙ**
<br>
Элементы таблицы связаны с **ключом.**

Поиск представляет собой запрос, возвращает указатель на имя из таблицы, совпадающее с z (успешный поиск).
<br>
В противном случае - пустое значение указателя, безуспешный поиск
<br>
любые 2 элемента на множестве $S$ сравнивы $x, y ∈ S$

![image](https://github.com/mireashik/aood_3sem/assets/49165758/de5116e8-ce65-40ca-a204-98c21afeda56)

Табличный порядок - определенный на таблице $T$
<br>
Статистические таблицы - не изменяются
<br>
Динамические таблицы - меняются (операции добавление / исключение, сортировка, объединение)

- Поиск z
- Включение z (включить)
- Исключение z (удаление)
- Распечатка (вывод всех имён)

Если табличный порядок не соответствует **ЕСТЕСТВЕННОМУ**, предполагается предварительная СОРТИРОВКА

### 67. Задача поиска. Последовательный (линейный) поиск.
**Сформулируем задачу поиска**

${k_1, k_2, k_3, … , k_n}$

- Сбор информации
- Организация информации
- Извлечение информации

![image](https://github.com/mireashik/aood_3sem/assets/49165758/141fddc2-f85c-4004-b65b-69f4eddc3746)

- ВНЕШНИМ поиск
- ВНУТРЕННИМ поиск

### 68. Методы оптимизации поиска. Индексно-последовательный поиск.
Простейший вид поиска заданного элемента на некотором множестве, последовательное сравнение

![image](https://github.com/mireashik/aood_3sem/assets/49165758/9f1130b4-9c0a-4a40-979f-a9377bb86517)

```c++
int dummysearch(int a[], int N, int key) { 
  for (int i = 0; i < N; i++) {
    if (a[i] == key) { 
      return i; 
    } 
  } 
  return N; 
}
```

![image](https://github.com/mireashik/aood_3sem/assets/49165758/c0c28e94-aa28-4ffc-9b36-f4b9dd38bd9b)

В порядке невозрастания частот обращения

ШАГ 1. [Начальная установка]. Установить i:=1.
<br>
ШАГ 2. [Сравнение]. Если k=ki, алгоритм завершён, удача нам благоволит.
<br>
ШАГ 3. [Продвижение]. Увеличить i на 1.
<br>
ШАГ 4. [Конец файла?]. Если $i < N$, то вернуться к ШАГУ 2. В ином случае, что-то пошло не так и алгоритм завершается неудачей.

#### Методы оптимизации поиска
Вся таблица поиска может быть представлена как система с дискретными состояниями, а вероятность поиска $i-го$ элемента ‒ это вероятность $p(i)$

![image](https://github.com/mireashik/aood_3sem/assets/49165758/9271018e-0404-4ffa-9046-849c7b11b024)

Так как последовательный поиск начинается с первого элемента, то на это место надо поставить элемент, к которому чаще всего обращаются

- переупорядочивание таблицы поиска путем перестановки найденного элемента в начало списка
- метод транспозиции

#### Переупорядочивание таблицы поиска путем перестановки найденного элемента в начало списка
остальные элементы сдвигаются

![image](https://github.com/mireashik/aood_3sem/assets/49165758/3a164596-3db3-4b0a-b5d9-d1a21bdb01fe)

- р ‒ рабочий указатель;
- q ‒ вспомогательный указатель, отстает на один шаг от р

### 69. Задача поиска. Бинарный поиск.
Бинарный (двоичный) поиск предъявляет ряд требований: 
- имена в таблице должны храниться в их естественном (отсортированном) порядке
- прямой доступ к именам таблицы

Бинарный поиск требует отсортированной таблицы, организованной в виде массива:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/b7fdbe23-8ecf-4773-894b-1a984b23a47c)

Первое сравнение − это корень дерева

![image](https://github.com/mireashik/aood_3sem/assets/49165758/485ed2af-5642-40f5-bdbb-0476edf13028)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/f1c049ed-512b-495e-9518-13b7d743423d)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/09a6474d-8d15-4625-8fb0-bc80dafdddae)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/9bcfa083-53ee-4b57-acbd-bff4100fa9e4)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/d22526f3-fd05-4081-9174-7aeb1608b98d)

#### Встроенные функции
binary_search,  lower_bound возвращает итератор первого элемента, upper_bound, которая возвращает итератор на элемент, который строго больше искомого в заданном диапазоне упорядоченных элементов.

#### Однородный бинарный поиск
Однородный (равномерный) бинарный поиск является модификацией обычного бинарного поиска

Вместо 3 указателей – l (нижняя граница интервала), h (верхняя граница интервала) и m (середина интервала) – используется только 2:
- текущая позиция m;
- величина его изменения δ.

в виде расширенного бинарного дерева, константа разности между вершинами

### 70. Задача поиска. Поиск Фибоначчи.
Последовательность фибоначчи: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89

Расширенное бинарное дерево (дерево Фибоначчи), соответствующее поиску Фибоначчи, показано на рисунке 6. Это дерево Фибоначчи порядка 6, то есть, корню дерева сопоставлено имя i=F6

![image](https://github.com/mireashik/aood_3sem/assets/49165758/cb97ee23-8b08-4780-b45f-a3314c49daa8)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/f610d7c0-74dd-4e2a-8e01-f20d6bfb26e7)

Последовательное сравнение отыскиваемого ключа будет производиться с элементами исходного множества ключей, расположенными в позициях, равных числам Фибоначчи

![image](https://github.com/mireashik/aood_3sem/assets/49165758/d702ce08-1ffa-4ed0-86ed-5c7e28f3d272)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/35714d2c-3cb7-4c23-832c-0747651f33fb)

### 71. Задача поиска. Интерполяционный поиск.
- $i$ ‒ номер первого рассматриваемого элемента;
- $j$ ‒ номер последнего рассматриваемого элемента;
- $K$ ‒ отыскиваемый ключ;
- $K_i$ ‒ значение ключа в позиции i;
- $K_j$ ‒ значение ключа в позиции j.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/f038f6ab-a972-42ce-a0a7-1dbee857bcb1)

Требуется найти ключ К=70

![image](https://github.com/mireashik/aood_3sem/assets/49165758/3144a903-450b-4ce0-89dc-2a37ab7a2f27)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/31c47297-4a5d-49d8-93b6-3463b5beb6de)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/4ab8a83f-da9e-49a7-8d99-f98271ed84fa)

Требуется найти ключ К = 90

![image](https://github.com/mireashik/aood_3sem/assets/49165758/d95b1225-7ca6-4057-a8eb-01c10a06fbd3)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/fed00872-d7e5-4f1a-b7e9-d29e290c99fc)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/f542a9d5-ffc6-4dcf-b32d-74a5bb28c11f)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/655312f8-0375-42c1-b6a4-d634b9f47c8f)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/96b6a858-7ba5-4b91-ab82-a067db8be5e8)

### 72. Деревья бинарного поиска.
Для динамических таблиц необходима такая структура данных, которая была бы  приспособлена как к методу бинарного поиска, так и к эффективному выполнению  операций включения и исключения. Такой структурой данных является ДЕРЕВО  БИНАРНОГО ПОИСКА

Связные списки не позволяют использовать прямой доступ (только последовательный доступ)

СИММЕТРИЧНЫЙ (слева-направо) порядок прохождения вершин совпадает с естественным порядком имен

![image](https://github.com/mireashik/aood_3sem/assets/49165758/d0b6d8e1-b114-4fc3-ada3-9ad5121a4453)

Поиск
- z **предшествует** имени в корне (меньше), поиск продолжается рекурсивно в **левом** поддереве
- z **следует** за именем в корне (больше), поиск продолжается рекурсивно в  **правом** поддереве корня

Распечатка z - симметричный проход

Включение z - еслп поиск безуспешен. 

Исключение несколько сложнее включения, поскольку в дереве бинарного поиска исключается внутренний узел, который может:
- быть листом;
- иметь 1 потомка;
- иметь 2 потомков

![image](https://github.com/mireashik/aood_3sem/assets/49165758/eafaf23e-bf80-4338-a1a3-7f7ae3cef432)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/12a96337-b221-40a4-8cc5-03e8d53a69c6)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/a183b0f6-432c-478e-a54f-752b959b3c78)

Требуется найти SAG. При просмотре от корня дерева видно, что по первой букве латинского алфавита название SAG больше названия CAP

![image](https://github.com/mireashik/aood_3sem/assets/49165758/6c958dbe-e348-430a-a7bf-3aba0117bd03)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/5ee9642c-762e-4982-b551-d6e1f339c408)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/c18c91bd-cc4b-4c59-a435-f24ccb7d3fc2)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/41c94704-bcf3-4a3d-8ecc-062af98eb9ea)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/76ad3663-5e27-4741-af43-dda91ee864fe)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/fd001205-1691-4c5a-b250-34726dcc0765)