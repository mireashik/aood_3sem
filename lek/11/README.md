## АЛГОРИТМЫ ВНУТРЕННЕЙ СОРТИРОВКИ
### 1.1. Сортировка кучей, пирамидальная сортировка (Heapsort)
Пирамидальная сортировка ‒ это алгоритм сортировки, в котором используется такая структура данных, как двоичная куча
<br>
неустойчивый алгоритм сортировки с временем работы O(NlogN)
<br>
использующий O(1) дополнительной памяти

**Законченное двоичное дерево** ‒ это двоичное дерево, в котором каждый уровень, за исключением, возможно, последнего, имеет полный набор узлов, и все листья расположены как можно левее

![image](https://github.com/mireashik/aood_3sem/assets/49165758/b95fd50c-0fdb-4293-b652-5d3c14d8f549)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/f94f7028-f6da-4b8a-af6b-7ab0815c7e26)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/55561b7a-8582-46de-9d53-becc03e595e0)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/43add3e4-b74b-4027-87e8-a12e724f47e1)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/823f398a-21eb-4753-b1f0-c5c6e838feaa)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/868c4bec-fc05-4329-96e3-e97767f6b240)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/73e411c5-69e0-4235-8a00-918f54d0cc23)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/8eefbd13-0d61-4704-84f5-aa13c10aaee8)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/fe886153-ece9-45e6-ac9f-a32a32d5e1d7)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/846499d3-304d-4bab-8b09-70f4af37e2a6)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/771cf7f9-23d7-449b-9f77-eb0e0f02a9a2)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/fa8ac42e-b04b-4116-b259-1d3b3110d131)

### 1.2. Сортировка TimSort
Сортировка Timsort (двоичное дерево) ‒ гибридный алгоритм сортировки, который сочетает в себе два алгоритма сортировки: сортировку вставками и сортировку слиянием

1. По специальному алгоритму разделяем входной массив на подмассивы.
2. Сортируем каждый подмассив обычной сортировкой вставками.
3. Собираем отсортированные подмассивы в единый массив с помощью модифицированной сортировки слиянием.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/8b63ae59-b2f7-498d-80aa-a512c73e5ec5)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/df5f6d98-fe8f-45ee-921e-069ed130282a)

Тим Петерс, ссылаясь на собственные эксперименты. показавшие, что $minrun > 256$ нарушается 1 пункт, а при $minrun < 8$ 2 пункт
<br>
если $N < 64$, тогда $N = minrun$ и алгоритм Timsort становится сортировкой вставками.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/47a4528d-edca-45d8-b58d-6ad97fb65f83)
