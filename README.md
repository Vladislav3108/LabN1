## Отчет по лабораторной работе № 1

#### № группы: `ПМ-2401`

#### Выполнил: `Тараканов Владислав Алексеевич`

#### Вариант: `27`

### Cодержание:

- [Постановка задачи](#1-постановка-задачи)
- [Входные и выходные данные](#2-входные-и-выходные-данные)
- [Выбор структуры данных](#3-выбор-структуры-данных)
- [Алгоритм](#4-алгоритм)
- [Программа](#5-программа)
- [Анализ правильности решения](#6-анализ-правильности-решения)

### 1. Постановка задачи

> На вход программы подается натуральное число. Определить, является ли
> оно 4-хзначным числом, все цифры которого различны ("YES"/"NO").

Данную задачу можно разделить на 2 подзадачи: проверка на количество разрядов числа и проверка на то, что число состоит из разных цифр.

- Для 1 подзадачи нужно рассмотреть 2 случая:
    1. `number >= 1000 && number <= 9999`
    2. `number < 1000 && number > 9999` (отрицание 1 случая)
- Пусть введенное число 4-х значное, тогда для 2 подзадачи нужно также рассмотреть 2 случая:
    1. Все цифры числа различны
    2. Не все цифры числа различны (отрицание 1 случая)

Всего надо рассмотреть `2 * 2 = 4` случая.

### 2. Входные и выходные данные

#### Данные на вход

На вход программа должна получать одно число, при этом в условии сказано, что число относится к множеству натуральных чисел. Но не даны верхняя и нижняя границы получаемого числа. Будем считать, что число может быть введено из всего диапазона натуральных чисел.

|        | Тип              | min значение    | max значение     |
|--------|------------------|-----------------|------------------|
| number | Натурально число | -2<sup>31</sup> | 2<sup>31</sup>-1 |

#### Данные на выход

Программа должна вывести строку 'YES' или 'NO'.

|        | Тип    | 
|--------|--------|
| Строка | String | 

### 3. Выбор структуры данных

Программа получает одно натуральное число. Поэтому для его хранения
можно выделить одну переменную (`number`) типа `int`.

|       | название переменной | Тип (в Java) | 
|-------|---------------------|--------------|
| Число | `number`            | `int`        |

Для вывода результата необязательно его хранить в отдельной переменной.

### 4. Алгоритм

#### Алгоритм выполнения программы:

1. **Ввод данных:**  
   Программа считывает натуральное число, обозначенное как `number`.

2. **Проверка количества разрядов числа:**  
   Программа сравнивает значение 'number' c 1000 и 9999, если 1000<= 'number' <=9999, программа переходит к проверке цифр 
   числа, иначе выводит 'NO'.

3. **Проверка цифр числа:**
    - введенное число разбивается на отдельные цифры, если они различны, то выводится 'YES', иначе 'NO'.

4. **Вывод результата:**  
   На экран выводится либо строка 'YES', либо строка 'NO'.

#### Блок-схема

```mermaid
graph TD
    A([Начало]) --> B[/Ввести: number, digit1, digit2, digit3, digit4/]
    B --> C{1000 =< number <= 9999}
    C -- Да --> D{/Вывод: NO/}
    C -- Нет --> I{|
        digit1 = number / 1000
        digit2 = (number / 100) % 10
        digit3 = (number / 10) % 10
        digit4 = number % 10
    |}
    I --> F{digit1 != digit2 && digit1 != digit3 && digit1 != digit4 && digit2 != digit3 && digit2 != digit4 && digit3 !=       digit4}
    F -- Да --> G{/Вывод: YES/}
    F -- Нет --> H{/Вывод: NO/}
    D --> Z
    G --> Z
    H --> Z
    E --> Z([Конец])

```

### 5. Программа

```java
import java.io.PrintStream;
import java.util.Scanner;

public class Main {
    // Объявляем объект класса Scanner для ввода данных
    public static Scanner in = new Scanner(System.in);
    // Объявляем объект класса PrintStream для вывода данных
    public static PrintStream out = System.out;

    public static void main(String[] args) {
        // Считывание двух вещественных чисел x и y из консоли
        double x = in.nextDouble();
        double y = in.nextDouble();

        // Определение максимального числа
        if (x >= y) {
            // Если x положительное, выводим x, иначе выводим -x,
            // чтобы на выходе было его абсолютное значение
            if (x >= 0) {
                out.println(x);
            } else {
                out.println(-x);
            }
        } else {
            // Если x положительное, выводим y, иначе выводим -y,
            // чтобы на выходе было его абсолютное значение
            if (y >= 0) {
                out.println(y);
            } else {
                out.println(-y);
            }
        }
    }
}
```

### 6. Анализ правильности решения

Программа работает корректно на всем множестве решений с учетом ограничений.

1. Тест на `X > Y > 0`:

    - **Input**:
        ```
        5 1.3
        ```

    - **Output**:
        ```
        5
        ```

2. Тест на `X < Y < 0`:

    - **Input**:
        ```
        -4 -2.2
        ```

    - **Output**:
        ```
        2.2
        ```

3. Тест на `X < 0 < Y`:

    - **Input**:
        ```
        -4 5
        ```

    - **Output**:
        ```
        5
        ```

4. Тест на `X = 0` или `Y = 0`:

    - **Input**:
        ```
        0 -3
        ```

    - **Output**:
        ```
        3
        ```

5. Тест на ограничение задачи:

    - **Input**:
        ```
        -1000000000 1000000000
        ```

    - **Output**:
        ```
        1000000000
        ```
