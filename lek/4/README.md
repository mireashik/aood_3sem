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

### 2.3. Реализация дека на основе массива

### 2.4. Реализация дека с помощью библиотеки STL

### 2.5. Деки в языке С++

### 3.1. Итераторы

### 3.2. Операции с итераторами

### Константные итераторы

### Реверсивные итераторы
