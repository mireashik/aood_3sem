## Деки и итераторы
### 1. Очереди с приоритетом
Очередь, можно создать:
- массив
- односвязный список

### 1.1. Кольцевая очередь
Первый элемент не удаляется и не выходит, он переходит в конец очереди.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/b1709e71-a12e-485d-96ca-b23f690a1684)

- добавить новый элемент в очередь;
- проверка, очереди на пустоту;
- проверка, очередь на полноту;
- очистка очереди (удаление всех элементов очереди);
- вытянуть 1 элемент из очереди и поместить в конец очереди.

```c++
#include <iostream>
using namespace std;

template <typename T>
class QueueRing {
private:
    T* queue;       // очередь в виде массива
    int count;      // текущая длина очереди
    int maxCount;   // максимальный размер очереди

    void Copy(const QueueRing<T>& obj) {
        // Метод, осуществляющий копирование очереди
        // ... (см. ваш код для полного описания)
    }

public:
    // Конструктор
    QueueRing(int _maxCount) {
        // ... (см. ваш код для полного описания)
    }

    // Конструктор копирования
    QueueRing(const QueueRing& obj) {
        Copy(obj);
    }

    // Оператор копирования
    QueueRing<T> operator=(const QueueRing& obj) {
        Copy(obj);
        return *this;
    }

    // Деструктор
    ~QueueRing() {
        // ... (см. ваш код для полного описания)
    }

    // Очистка очереди
    void Clear() {
        count = 0;
    }

    // Проверка, пуста ли очередь?
    bool isEmpty() {
        return count == 0;
    }

    // Получить количество элементов очереди
    int Count() {
        return count;
    }

    // Проверка, заполнена ли очередь?
    bool isFull() {
        return count == maxCount;
    }

    // Добавить новый элемент в очередь
    void Add(T item) {
        if (!isFull())
            queue[count++] = item;
    }

    // Вытянуть первый элемент из очереди и поместить в конец очереди
    bool Move() {
        if (!isEmpty()) {
            // ... (см. ваш код для полного описания)
            return true;
        } else {
            return false;
        }
    }

    // Метод, выводящий очередь
    void Print(string msg) {
        // ... (см. ваш код для полного описания)
    }
};

int main() {
    // Пример использования кольцевой очереди
    QueueRing<int> Q(4);
    Q.Print("Q(4): ");

    Q.Add(25);
    Q.Add(30);
    Q.Add(70);
    Q.Add(10);
    Q.Add(7);
    Q.Print("Q.Add(...): ");

    Q.Move();
    Q.Print("Q.Move(): ");

    Q.Move();
    Q.Print("Q.Move(): ");

    QueueRing<int> Q2 = Q;
    Q2.Print("Q2: ");

    QueueRing<int> Q3 = Q;
    Q3.Print("Q3: ");

    return 0;
}
```

### 1.2. Очередь с приоритетом С++
Очередь где элементы отсортированы по приоритету - число, константа и т.д.
<br>
Извлекаются в таком случае - в начале элементы с высшим приоритетом

Например, чем меньше число - тем больше приоритет.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/67430f83-2dc9-4696-8e43-36791cc8b078)


#### 1.2.1 Очередь с приоритетным включением
Упорядочены в момент ВХОДА (хранятся по приоритету), выходят в обычном порядке. Самый большой приоритет - на первом месте. При включении добавляем в конец элементов с одинаковым приоритетом.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/16ca0860-4caf-426f-9399-da47dcfcbe83)

```c++
#include <iostream>
#include <queue>

using namespace std;

int main() {
    // Объявляем приоритетную очередь
    priority_queue<int> priority_q;

    // Вводим 7 чисел и добавляем их в очередь
    cout << "Введите 7 чисел: " << endl;
    for (int j = 0; j < 7; j++) {
        int a;
        cin >> a;
        priority_q.push(a);
    }

    // Выводим первый элемент очереди
    cout << "Первый элемент очереди: " << priority_q.top() << endl;

    return 0;
}
```

#### 1.2.2 Очереди с приоритетным исключением
В момент входа просто добавляются (в порядке поступления), а ВЫХОДЯТ по приоритету

![image](https://github.com/mireashik/aood_3sem/assets/49165758/2f13ecdb-74de-4c20-9e3e-eef0a0aca6ed)

```c++
#include <iostream>
#include <string.h>
#include <time.h>

using namespace std;

class QueuePriority {
private:
    int *Wait;           // Очередь
    int *Pri;            // Приоритет
    int MaxQueueLength;  // Максимальный размер очереди
    int QueueLength;     // Текущий размер очереди

public:
    QueuePriority(int m);  // Конструктор
    ~QueuePriority();     // Деструктор
    void Add(int c, int p);  // Добавление элемента
    int Extract();           // Извлечение элемента
    void Clear();            // Очистка очереди
    bool IsEmpty();          // Проверка существования элементов в очереди
    bool IsFull();           // Проверка на переполнение очереди
    int GetCount();          // Количество элементов в очереди
    void Show();             // Демонстрация очереди
};

QueuePriority::QueuePriority(int m) {
    MaxQueueLength = m;      // Получаем размер
    Wait = new int[MaxQueueLength];  // Создаем очередь
    Pri = new int[MaxQueueLength];
    QueueLength = 0;         // Изначально очередь пуста
}

QueuePriority::~QueuePriority() {
    delete[] Wait;  // Удаление очереди
    delete[] Pri;
}

void QueuePriority::Clear() {
    QueueLength = 0;  // Эффективная «очистка» очереди
}

bool QueuePriority::IsEmpty() {
    return QueueLength == 0;  // Пуста?
}

bool QueuePriority::IsFull() {
    return QueueLength == MaxQueueLength;  // Полна?
}

int QueuePriority::GetCount() {
    return QueueLength;  // Количество присутствующих в стеке элементов
}

void QueuePriority::Show() {
    cout << "\n-------------------------------------\n";
    // Демонстрация очереди
    for (int i = 0; i < QueueLength; i++) {
        cout << Wait[i] << " - " << Pri[i] << "\n\n";
    }
    cout << "\n-------------------------------------\n";
}

void QueuePriority::Add(int c, int p) {
    if (!IsFull())  // Если в очереди есть свободное место, то увеличиваем количество значений и вставляем новый элемент
    {
        Wait[QueueLength] = c;
        Pri[QueueLength] = p;
        QueueLength++;
    }
}

int QueuePriority::Extract() {
    if (!IsEmpty())  // Если в очереди есть элементы, то возвращаем тот, у которого наивысший приоритет и сдвигаем очередь
    {
        int max_pri = Pri[0];  // Пусть приоритетный элемент – нулевой
        int pos_max_pri = 0;   // А приоритетный индекс = 0
        for (int i = 1; i < QueueLength; i++)  // Ищем приоритет
            // Если встречен более приоритетный элемент
            if (max_pri < Pri[i]) {
                max_pri = Pri[i];
                pos_max_pri = i;
            }
        // Вытаскиваем приоритетный элемент
        int temp1 = Wait[pos_max_pri];
        int temp2 = Pri[pos_max_pri];

        // Сдвинуть все элементы
        for (int i = pos_max_pri; i < QueueLength - 1; i++) {
            Wait[i] = Wait[i + 1];
            Pri[i] = Pri[i + 1];
        }
        QueueLength--;  // Уменьшаем количество
        return temp1;   // Возврат извлеченного элемента
    } else
        return -1;
}

int main() {
    srand(time(0));
    QueuePriority QUP(25);  // Создание очереди
    for (int i = 0; i < 5; i++)  // Заполнение части элементов
    {
        QUP.Add(rand() % 100, rand() % 12);  // Значения от 0 до 99 (включительно) и приоритет от 0 до 11 (включительно)
    }
    QUP.Show();    // Показ очереди
    QUP.Extract();  // Извлечение элемента
    QUP.Show();     // Показ очереди
}
```

### 2.1. Дек – общие сведения
Дек - список, одновременно работает по 2 принципам FIFO и LIFO. Это очередь с 2 сторонами, или стек с 2 концами. Двухсторонний доступ, возможность выбора одной из его сторон

![image](https://github.com/mireashik/aood_3sem/assets/49165758/dba18aee-eb4c-4cdb-833e-4dffde4f384a)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/7fd0640b-c85a-4b59-ba44-019f8510bb4f)

### 2.2. Операции над деком
- добавление элемента в начало
- добавление элемента в конец
- удаление 1 элемента
- удаление последнего элемента
- чтение 1 элемента
- чтение последнего элемента

### 2.3. Реализация дека на основе массива
```c++
#include "stdafx.h"
#include <iostream>

using namespace std;

const int N = 5; // Размер дека

struct Deque {
    int data[N]; // Массив данных
    int last;     // Указатель на конец
};

void Creation(Deque* D) // Создание дека
{
    D->last = 0;
}

bool Full(Deque* D) // Проверка дека на пустоту
{
    if (D->last == 0)
        return true;
    else
        return false;
}

void AddL(Deque* D) // Добавление элемента в начало
{
    if (D->last == N) {
        cout << "\nДек заполнен\n\n";
        return;
    }
    int value;
    cout << "\nЗначение > ";
    cin >> value;
    for (int i = D->last; i > 0; i--)
        D->data[i] = D->data[i - 1];
    D->data[0] = value;
    D->last++;
    cout << endl << "Элемент добавлен\n\n";
}

void AddR(Deque* D) // Добавление элемента в конец
{
    if (D->last == N) {
        cout << "\nДек заполнен\n\n";
        return;
    }
    int value;
    cout << "\nЗначение > ";
    cin >> value;
    D->data[D->last++] = value;
    cout << endl << "Элемент добавлен\n\n";
}

void DeleteL(Deque* D) // Удаление первого элемента
{
    for (int i = 0; i < D->last; i++) // Смещение элементов
        D->data[i] = D->data[i + 1];
    D->last--;
}

void DeleteR(Deque* D) // Удаление последнего элемента
{
    D->last--;
}

int OutputL(Deque* D) // Вывод первого элемента
{
    return D->data[0];
}

int OutputR(Deque* D) // Вывод последнего элемента
{
    return D->data[D->last - 1];
}

int Size(Deque* D) // Размер дека
{
    return D->last;
}

int main() // Главная функция
{
    setlocale(LC_ALL, "Rus");
    Deque D;
    Creation(&D);
    char number;

    do {
        cout << "1. Добавить элемент в начало" << endl;
        cout << "2. Добавить элемент в конец" << endl;
        cout << "3. Удалить первый элемент" << endl;
        cout << "4. Удалить последний элемент" << endl;
        cout << "5. Вывести первый элемент" << endl;
        cout << "6. Вывести последний элемент" << endl;
        cout << "7. Узнать размер дека" << endl;
        cout << "0. Выйти\n\n";

        cout << "Номер команды > ";
        cin >> number;

        switch (number) {
        case '1':
            AddL(&D);
            break;
        case '2':
            AddR(&D);
            break;
        case '3':
            if (Full(&D))
                cout << endl << "Дек пуст\n\n";
            else {
                DeleteL(&D);
                cout << endl << "Элемент удален из дека\n\n";
            }
            break;
        case '4':
            if (Full(&D))
                cout << endl << "Дек пуст\n\n";
            else {
                DeleteR(&D);
                cout << endl << "Элемент удален\n\n";
            }
            break;
        case '5':
            if (Full(&D))
                cout << endl << "Дек пуст\n\n";
            else
                cout << "\nПервый элемент: " << OutputL(&D) << "\n\n";
            break;
        case '6':
            if (Full(&D))
                cout << endl << "Дек пуст\n\n";
            else
                cout << "\nПоследний элемент: " << OutputR(&D) << "\n\n";
            break;
        case '7':
            if (Full(&D))
                cout << endl << "Дек пуст\n\n";
            else
                cout << "\nРазмер дека: " << Size(&D) << "\n\n";
            break;
        case '0':
            break;
        default:
            cout << endl << "Команда не определена\n\n";
            break;
        }
    } while (number != '0');

    system("pause");
    return 0;
}
```

### 2.4. Реализация дека с помощью библиотеки STL
- front – возврат значения 1 элемента
- back – возврат значения последнего элемента
- push_front – добавление элемента в начало
- push_back – добавление элемента в конец
- pop_front – удаление 1 элемента
- pop_back – удаление последнего элемента
- size – возврат числа элементов дека
- clear – очистка дека

```c++
#include "stdafx.h"
#include <deque>
#include <iostream>

using namespace std;

int main() // Главная функция
{
    setlocale(LC_ALL, "Rus");
    deque<int> D; // Создание дека D размером 5
    deque<int>::iterator out;
    int value;
    char number;

    do {
        cout << "1. Добавить элемент в начало" << endl;
        cout << "2. Добавить элемент в конец" << endl;
        cout << "3. Удалить первый элемент" << endl;
        cout << "4. Удалить последний элемент" << endl;
        cout << "5. Вывести первый элемент" << endl;
        cout << "6. Вывести последний элемент" << endl;
        cout << "7. Узнать размер дека" << endl;
        cout << "0. Выйти\n\n";
        cout << "Номер команды > ";
        cin >> number;

        switch (number) {
        case '1':
            cout << "\nЗначение > ";
            cin >> value;
            D.push_front(value);
            cout << endl << "Элемент добавлен\n\n";
            break;
        case '2':
            cout << "\nЗначение > ";
            cin >> value;
            D.push_back(value);
            cout << endl << "Элемент добавлен\n\n";
            break;
        case '3':
            if (D.empty())
                cout << "\nДек пуст\n\n";
            else {
                D.erase(D.begin());
                cout << endl << "Элемент удален\n\n";
            }
            break;
        case '4':
            if (D.empty())
                cout << "\nДек пуст\n\n";
            else {
                D.erase(D.end() - 1);
                cout << endl << "Элемент удален\n\n";
            }
            break;
        case '5':
            if (D.empty())
                cout << endl << "Дек пуст\n\n";
            else {
                out = D.begin();
                cout << "\nПервый элемент: " << *out << "\n\n";
            }
            break;
        case '6':
            if (D.empty())
                cout << "\nДек пуст\n\n";
            else {
                out = D.end() - 1;
                cout << "\nПоследний элемент: " << *out << "\n\n";
            }
            break;
        case '7':
            if (D.empty())
                cout << endl << "Дек пуст\n\n";
            else
                cout << "\nРазмер дека: " << D.size() << "\n\n";
            break;
        case '0':
            break;
        default:
            cout << endl << "Команда не определена\n\n";
            break;
        }
    } while (number != '0');

    system("pause");
    return 0;
}
```

### 2.5. Деки в языке С++
Дек (deque) - это сокращенная фраза «double-ended-queue», что, в переводе с английского, означает - двусторонняя очередь. Контейнер Дек очень похож на контейнер - Вектор. Разница между Вектором и Деком состоит лишь в том, что в деках динамический массив открыт с 2 сторон. Это позволяет очень быстро добавлять новые элементы как в конец так и в начало контейнера.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/2dd8ea0d-cf95-4e6a-8e48-49d51bc2fd32)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/70a0c57a-3799-4aae-bd10-c32c2d89fa17)

### 3.1. Итераторы
Итераторы - сущности для взаимодействия с элементами. Схожи с указателями, но они отличаются. Итератор - оболочка над указателем, определяют как указатели будут работать. Итератор у вектора работает и пересобирает элементы по другому, в отличии от списка. Хотя функционально они выполняют одну и ту же операцию.

**Итератор** - структура данных для обращения к элементу в контейнерах STL. Обычно их используют с контейнерами set, list, у вектора - индексы.

set (множество) - контейнер, автоматически сортирует элементы в порядке возрастания. Но при добавлении одинаковых значений, set будет хранить только 1 его экземпляр.

Подробнее можно почитать [здесь](https://github.com/mireashik/oop_2sem/tree/main/exam#25-контейнеры-и-итераторы)

### 3.2. Операции с итераторами
- begin() возвращает итератор, который указывает на 1 элемент контейнера
- end() возвращает итератор, который указывает на последний элемент контейнера
- *iter - получение элемента, на который указывает итератор
- ++iter перемещение итератора вперед
- --iter перемещение итератора назад
- iter1 == iter2 2 итератора равны, если указывают на один и тот же элемент

```c++
vector<int> iterator1 = { 1,2,3,4 };
vector<int>::iterator iter = iterator1.begin(); // получаем итератор
```

Итераторы позволяют не только получать элементы, но и изменять их:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/449a7e31-6e9e-4fa7-bca4-9700d35c4061)

В данном случае в цикле while элементы вектора возводятся в квадрат.

### Константные итераторы
Если контейнер - константа, то ТОЛЬКО константный итератор (элементы изменять НЕЛЬЗЯ)
<br>
Если контейнер - не константа, то константный итератор всё-равно не даст изменить элементы

### Реверсивные итераторы
Перебирают элементы контейнера в обратном направлении, rbegin() и rend()

- iter + n возвращает итератор, который смещен от итератора iter на n позиций вперед
- iter - n возвращает итератор, который смещен от итератора iter на n позиций назад
- iter += n перемещает итератор на n позиций вперед
- iter -= n перемещает итератор на n позиций назад

![image](https://github.com/mireashik/aood_3sem/assets/49165758/19f3c035-fddd-4611-b86e-01fb67c51cfb)
