### ПОИСК ПОДСТРОКИ В СТРОКЕ
АЛФАВИТ ‒ конечное множество символов.

СТРОКА (слово) – это последовательность символов из некоторого алфавита

ДЛИНА СТРОКИ – количество символов в строке

ПРЕФИКС, СУФИКС

![image](https://github.com/mireashik/aood_3sem/assets/49165758/704d457f-5379-4649-9aff-b952da82ecb0)

### Прямой поиск (наивный метод)
В посимвольном сравнении строки с подстрокой

![image](https://github.com/mireashik/aood_3sem/assets/49165758/14847be6-c34c-457a-8727-1465171cbbda)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/9be4c9ba-0250-4240-8d21-b13bb632df8e)

### Алгоритм Кнута-Морриса-Пратта
сдвиг подстроки выполняется не на один символ на каждом шаге алгоритма, а на некоторое переменное количество символов.
<br>
Поэтому нужно определить величину сдвига

![image](https://github.com/mireashik/aood_3sem/assets/49165758/15c2b773-15f8-402f-be4c-367d3de5ac7c)

Алгоритм основан на построении префикс-функции.
<br>
**Префикс-функция** - мак. префикс строки, который не совпадает с этой строкой и суффикс
<br>
Для строки S удобно представлять префикс-функцию в виде массива длиной |S|-1.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/6f48fddb-17e6-4eca-824f-14eb11a28e78)

Пусть дана строка «cbacbc». Определим её префикс-функцию

![image](https://github.com/mireashik/aood_3sem/assets/49165758/fa55000d-5579-4df2-b0d7-d36b15ba6ccb)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/f65f7fe7-05ff-49fa-be72-60596f7144cd)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/1c9514c0-fa4f-4c0d-ae29-8f4385cf0313)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/8dc6d1d7-2946-48c3-a3d0-d9b80104b655)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/a0618697-a581-4eef-b247-d31c2fa382df)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/0d078795-7781-4c0f-90fd-c2d2fce3a1e5)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/59b9b7a0-acaf-48a6-b73c-c37b718b2a43)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/522887cf-9dd0-45ae-9419-38718c49d6fa)

Как мы отметили выше, идея алгоритма Кнута-Морриса-Пратта состоит в том, что по вычисленной префикс-функции для ОБРАЗЦА делается вывод о необходимом размере шага смещения

![image](https://github.com/mireashik/aood_3sem/assets/49165758/083b07f1-6f3a-49bc-b03a-095ebf6902d2)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/91a2fbe9-56f4-4762-9c56-870926770487)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/8292ae6a-78fa-47cd-805e-c4e130726ca4)

Поскольку крайним **совпавшим** элементом образца является 4 элемент, то смотрим на 4 элемент префикс-функции (элемент в чётвёртой ячейки массива). В данном случае этот элемент равен **2**
<br>
Поэтому, возможно произвести смещение на 4 – 2 = 2 позиции

![image](https://github.com/mireashik/aood_3sem/assets/49165758/6287ec07-d9bd-45a1-96c0-84871e7ef63c)

На это раз смотрим на 5 элемент массива ‒ это элемент 0. Поэтому  мы можем произвести сдвиг на 5 – 0 = 5 позиций. То есть, на 5 шагов вправо

![image](https://github.com/mireashik/aood_3sem/assets/49165758/278f5b6c-e053-456e-8b26-a5b08f6deec0)

На ШАГЕ 4 (третье сравнение) все элементы образца совпали, соответственно задача нахождения входа образца S в строку T решена.

Другой пример:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/9ab4d747-17fa-48bc-847b-c55b54003e56)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/8903a190-9f03-44ff-86ef-30bb34559d25)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/66537d4e-262a-4951-bfed-142a685f8dc5)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/af125a68-d2b2-400a-93c6-8b4d106755f8)

### Алгоритм Бойера и Мура
Алгоритм считается наиболее быстрым
<br>
требуется сделать ряд предварительных вычислений над образцом, часть пропускать как заведомо не дающие результата

- ПРИНЦИП ПЕРВЫЙ. Поиск СЛЕВА НАПРАВО, сравнение СПРАВА НАЛЕВО
- ПРИНЦИП ВТОРОЙ. ПРИНЦИП СТОП-СИМВОЛА

![image](https://github.com/mireashik/aood_3sem/assets/49165758/5260c5b3-4f95-46bd-b9ff-1ddac8fe16a1)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/d0c35e73-51aa-463a-9dc2-f7cb64bdcf11)

- ПРИНЦИП ТРЕТИЙ. ПРИНЦИП СОВПАВШЕГО СУФФИКСА

![image](https://github.com/mireashik/aood_3sem/assets/49165758/2147ab29-2fdf-4ff5-8ac1-faa8519c3c34)

Иными словами, мы сдвигаем образец вправо до ближайшего суффикса «АВ»

Для каждого возможного суффикса t указывается **наименьшая** величина, на которую нужно сдвинуть **вправо** образец

![image](https://github.com/mireashik/aood_3sem/assets/49165758/c855f882-b6f9-4d39-b970-409d133798c0)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/9374b0bf-bd7e-426a-8f02-7447b33f0b0f)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/979e2b27-251f-43b9-a98c-6382db34c830)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/2f88c2ec-0858-4bfe-844e-cacc057050ef)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/188ad4cb-3bdb-42ea-a59b-8bdaf8b25e6f)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/0bb3f254-c6d1-4d63-b937-58f4a039a911)

Существует упрощенная версия алгоритма Бойера- Мура, алгоритм Бойера-Мура-Хорспула. За стоп-символ в этом алгоритме берется символ строки, расположенный непосредственно над последним символом шаблона.

### Алгоритм Бойера-Мура-Хорспула
![image](https://github.com/mireashik/aood_3sem/assets/49165758/d46ecb96-0013-4192-9292-a5367bf4b98b)

Пример:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/1d1fb41f-7b40-4890-9bb4-8d89f7c470fc)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/0bf1727a-bd3a-4f11-a4d8-65de55e17b14)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/c3f7b624-19cd-4058-ad1b-b87a62b57248)

Поскольку сравнение показало несовпадение первых элементов, то продолжительность смещения в таблице мы ищем по символу из ТЕКСТА, то есть, строки. В нашем случае, это символ «**И**»
<br>
а значит в таблице это ячейка с символом *, а, следовательно, продолжительность смещения на этом шаге составляет 6

![image](https://github.com/mireashik/aood_3sem/assets/49165758/dba67be1-e2d7-4c23-8131-1d42ead7b20a)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/734d664d-2dff-4947-9ac7-893f8f7df7be)

Поскольку сравнение показало несовпадение уже **НЕ первых элементов**, то продолжительность смещения в таблице мы станем искать по символу из **ОБРАЗЦА**. В нашем случае, это символ «Ы», а в таблице это смещений этому символу соответствует продолжительность смещения равная 1

![image](https://github.com/mireashik/aood_3sem/assets/49165758/8e4503c9-0d14-4b97-a420-fcaed5f7e196)

Символ «О», а значит в таблице это ячейка с символом *. Следовательно, продолжительность смещения на этом шаге составляет 6.

![image](https://github.com/mireashik/aood_3sem/assets/49165758/d1706682-2843-4991-809f-26b4c5754a5d)

### Алгоритм Рабина-Карпа
![image](https://github.com/mireashik/aood_3sem/assets/49165758/8a22cbe7-46ff-4fe4-b757-b65608958e7b)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/d67c7de9-0b96-4ee9-af85-d7521036ae46)

Другой пример:

![image](https://github.com/mireashik/aood_3sem/assets/49165758/240dd637-d56c-46fd-8e1f-650e2e10f453)

![image](https://github.com/mireashik/aood_3sem/assets/49165758/dd0097d3-caa7-449b-ac60-8ab50feecf18)

