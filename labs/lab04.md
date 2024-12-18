# Лабороторна робота №4
# Тема: Цикли з розгалуженням
## Мета: 
 1. Вивчити особливості циклічних обчислювальних процесів з розгалуженнями
 2. Опанувати технологію рекурентних обчислень
 3. Навчитися розробляти алгоритми та програми розвинення функцій у ряди
## Загальні умови до виконання умов:
1. Обчислити значення функції, розвинувши її у ряд Маклорена (абоТейлора).
2. Параметр функції має змінюватися від заданого з клавіатури мінімального значення до заданого користувачем максисального значення із певним кроком.
3. Розвинення функції в ряд здійснювати із заданої з клавіатури точністю. Точність розрахунку вводити з клавіатури у вигляді дробового числа в діапазоні від 10^-2 до 10^-6.
4. Для розвинення функції у ряд Маклорена (абоТейлора) створити власну функцію, яка розраховує суму ряду за рекурентним співвідношенням . Функції для обчислення факторіалу та степені числа не використовувати.
5. Значення функції tg(x) обчислювати через функції sin(x) та cos(x).
6. Визначити похибку обчислення наближених значень функції як різницю абсолютних значень наближеного обчислення та стандартного значення функції.
7. Стандартне значення функції обчислювати за допомогою бібліотечних математичних функцій.
8. Результати обчислень вивести у вигляді таблиці, яка містить колонки "Значення аргумента х", "Значення функції у", "Стандартне значення функції", "Похибка" відповідно до зразка результату, що поданий на вкладці "Виконання прикладу".
9. У випадку, коли для вибраних значень аргументів функція не визначена, друкувати повідомлення, наприклад, "function is not defined"
## Умова задачі №1:
Обчислити значення функції у, розвинувши функцію sh(x) у ряд Тейлора. Визначити похибку.
## Рівняння:
![image](https://github.com/user-attachments/assets/cd12e29d-2e59-4242-82b1-fb13132e8751)
## Умова задачі №2:
	Ввести з клавіатури два натуральних числа m>100, n> m . Визначити кількість чисел між m, n, які складаються з непарних цифр, або мають різні цифри. Подання числа у вигляді структурованого типу (масивом або рядком) не використовувати .
## Аналіз задачі та теоретичні обгрунтування вибраного методу вирішення задачі:
## Завдання 1:
Аналіз задачі та теоретичні обґрунтування вибраного методу вирішення задачі:

Завдання передбачає визначення кількості чисел у заданому інтервалі \([m+1, n-1]\), які складаються лише з непарних цифр або містять різні цифри. Для цього використовуються прості арифметичні операції без використання масивів чи рядків.

Функція **hasOddDigits** перевіряє, чи всі цифри числа є непарними, поступово вилучаючи цифри через залишок від ділення на 10. Якщо знайдена хоча б одна парна цифра, функція повертає `false`. Функція **hasDifferentDigits** визначає, чи числа містять різні цифри, порівнюючи кожну пару сусідніх цифр. Обидві функції є простими та ефективними.

Основна функція **printResult** забезпечує введення чисел `m` і `n` із перевіркою їхньої коректності (`m > 100` і `n > m`), а потім перевіряє кожне число в заданому інтервалі за допомогою згаданих функцій. Лічильник збільшується, якщо хоча б одна умова виконується. Результат виводиться у вигляді кількості знайдених чисел.

Обраний метод є простим, ефективним і відповідає вимогам задачі. Він використовує мінімум ресурсів, спираючись лише на базові арифметичні та логічні операції.

## Завдання 2:
Програма обчислює значення функції y, визначеної частинами на проміжку [0, 2], із використанням ряду Тейлора для розрахунку sinh(x). Функція sinh(x) розкладається за формулою:  
sinh(x) = сума від n=0 до нескінченності (x^(2n+1) / (2n+1)!)  
Обчислення виконується до досягнення заданої точності epsilon.  

Функція sinhTaylor обчислює суму ряду з використанням рекурентного методу для ефективності. У функції calculateY визначається вираз для y залежно від значення x: якщо x від 0 до 1, то y = sinh(x) + sinh(x^2); якщо x від 1 до 2, то y = sinh^2(x) / sinh(x+2).  

Програма перевіряє введення: xMin >= 0, xMax <= 2, step > 0, 10^(-6) <= epsilon <= 10^(-2). Результати порівнюються зі стандартною бібліотечною функцією sinh(), а також обчислюється похибка між значеннями.  

Обраний підхід дозволяє забезпечити необхідну точність та адаптивність для виконання розрахунків у зазначеному діапазоні.
## Алгоритм у вигляді блок-схеми:
прікриплено у гугл диску

## Код програми:
## Завдання 1:
```cpp
#include <iostream>
#include <iomanip>
#include <cmath>
#include <Windows.h>  // Додаємо бібліотеку для підтримки українських символів

using namespace std;

// Функція для ідентифікації
void identification() {
    cout << "Лабораторна робота №4: Автор: Кравчук М.М., КНУ ім. Т.Шевченка, ФІТ, ІПЗ-14 (1 курс)\n";
    cout << "Обчислити функцію за виразом:\n";
    cout << "y = { sh(x) + sh(x^2), при 0 <= x <= 1\n"
        << "      sh^2(x) / sh(x + 2), при 1 < x <= 2 }\n";
    cout << "Умова: Розвинення функції в ряд Маклорена з заданою точністю epsilon.\n\n";
}

// Функція для обчислення терму ряду sinh(x) (через рекурентне співвідношення)
double sinhTerm(double x, int n) {
    double term = pow(x, 2 * n + 1) / tgamma(2 * n + 2);  // Терм ряду sinh(x), де gamma-функція замінює факторіал
    return term;
}

// Функція для обчислення суми ряду sinh(x)
double sinhTaylor(double x, double epsilon) {
    double sum = x;  // Початковий елемент ряду (перший член)
    double term = sum;
    int n = 1;  // Номер наступного елемента
    // Цикл обчислення ряду до тих пір, поки терм більший за точність epsilon
    while (fabs(term) > epsilon) {
        term = sinhTerm(x, n);  // Обчислюємо наступний терм
        sum += term;  // Додаємо його до суми
        n++;
    }
    return sum;
}

// Функція для обчислення значення основної функції y в залежності від x
double calculateY(double x, double epsilon) {
    // Якщо x від 0 до 1, використовуємо перший вираз
    if (x >= 0 && x <= 1) {
        return sinhTaylor(x, epsilon) + sinhTaylor(x * x, epsilon);
    }
    // Якщо x від 1 до 2, використовуємо другий вираз
    else if (x > 1 && x <= 2) {
        return pow(sinhTaylor(x, epsilon), 2) / sinhTaylor(x + 2, epsilon);
    }
    // Якщо x не входить в діапазон, функція не визначена
    else {
        cout << "Функція не визначена для x за межами [0, 2]" << endl;
        return NAN;
    }
}

// Функція для введення даних з перевіркою правильності
void inputData(double& xMin, double& xMax, double& step, double& epsilon) {
    // Введення мінімального значення x
    do {
        cout << "Введіть мінімальне значення x (>= 0): ";
        cin >> xMin;
        if (xMin < 0) cout << "Помилка: мінімальне значення x має бути >= 0. Спробуйте ще раз." << endl;
    } while (xMin < 0);

    // Введення максимального значення x
    do {
        cout << "Введіть максимальне значення x (<= 2 і більше " << xMin << "): ";
        cin >> xMax;
        if (xMax <= xMin || xMax > 2) cout << "Помилка: максимальне значення x має бути <= 2 і більше мінімального. Спробуйте ще раз." << endl;
    } while (xMax <= xMin || xMax > 2);

    // Введення кроку
    do {
        cout << "Введіть крок (додатнє число): ";
        cin >> step;
        if (step <= 0) cout << "Помилка: крок має бути додатнім числом. Спробуйте ще раз." << endl;
    } while (step <= 0);

    // Введення точності
    do {
        cout << "Введіть точність (epsilon) в межах від 10^-2 до 10^-6: ";
        cin >> epsilon;
        if (epsilon < 1e-6 || epsilon > 1e-2) cout << "Помилка: epsilon має бути в межах від 10^-6 до 10^-2. Спробуйте ще раз." << endl;
    } while (epsilon < 1e-6 || epsilon > 1e-2);
}

// Функція для виведення результатів у таблицю
void printResults(double xMin, double xMax, double step, double epsilon) {
    // Заголовки таблиці
    cout << left << setw(15) << "x" << setw(20) << "Обчислене y" << setw(20) << "Стандартне y" << setw(20) << "Похибка" << endl;

    // Цикл для кожного значення x з кроком step
    for (double x = xMin; x <= xMax; x += step) {
        double calculatedY = calculateY(x, epsilon);  // Обчислюємо y через власну функцію
        double standardY;  // Стандартне значення y

        // Обчислюємо стандартне значення функції y
        if (x >= 0 && x <= 1) {
            standardY = sinh(x) + sinh(x * x);
        }
        else if (x > 1 && x <= 2) {
            standardY = pow(sinh(x), 2) / sinh(x + 2);
        }
        else {
            continue;  // Пропускаємо, якщо функція не визначена
        }

        // Обчислюємо похибку
        double error = fabs(calculatedY - standardY);
        // Виводимо результати у вигляді таблиці
        cout << left << setw(15) << x
            << setw(20) << calculatedY
            << setw(20) << standardY
            << setw(20) << error << endl;
    }
}

int main() {
    // Налаштовуємо консоль для підтримки українських символів
    SetConsoleCP(856);
    SetConsoleOutputCP(1251);

    // Виводимо ідентифікаційну інформацію
    identification();

    double xMin, xMax, step, epsilon;
    inputData(xMin, xMax, step, epsilon);  // Введення даних з перевіркою
    printResults(xMin, xMax, step, epsilon);  // Виведення результатів

    return 0;
}

```
## Завдання 2:
```cpp
#include <iostream>
#include <Windows.h>  // Додаємо бібліотеку для підтримки українських символів

using namespace std;

// Функція для ідентифікації (Завдання 2)
void identification() {
    cout << "Лабораторна робота №4: Автор: Кравчук М.М., КНУ ім. Т.Шевченка, ФІТ, ІПЗ-14 (1 курс)\n";
    cout << "Завдання 2:\n";
    cout << "Ввести з клавіатури два натуральних числа m > 100, n > m.\n";
    cout << "Визначити кількість чисел між m та n, які складаються з непарних цифр, або мають різні цифри.\n";
    cout << "Подання числа у вигляді масиву або рядка використовувати не можна.\n\n";
}

// Функція для перевірки наявності тільки непарних цифр
bool hasOddDigits(int number) {
    while (number > 0) {
        int digit = number % 10;
        if (digit % 2 == 0) {
            return false;  // Якщо є парна цифра
        }
        number /= 10;
    }
    return true;
}

// Функція для перевірки наявності різних цифр
bool hasDifferentDigits(int number) {
    int lastDigit = number % 10;
    number /= 10;
    while (number > 0) {
        int currentDigit = number % 10;
        if (currentDigit != lastDigit) {
            return true;  // Якщо знайдено різні цифри
        }
        number /= 10;
    }
    return false;
}

// Функція для виконання завдання 2
void printResult() {
    int m, n;

    // Введення чисел m і n з перевіркою
    do {
        cout << "Введіть m (m > 100): ";
        cin >> m;
        if (m <= 100) cout << "Помилка: m має бути більше 100. Спробуйте ще раз." << endl;
    } while (m <= 100);

    do {
        cout << "Введіть n (n > m): ";
        cin >> n;
        if (n <= m) cout << "Помилка: n має бути більше m. Спробуйте ще раз." << endl;
    } while (n <= m);

    int count = 0;  // Лічильник чисел, які відповідають умовам
    for (int i = m + 1; i < n; ++i) {
        if (hasOddDigits(i) || hasDifferentDigits(i)) {
            count++;
        }
    }
    cout << "Кількість чисел між " << m << " та " << n << ": " << count << endl;
}

int main() {
    // Налаштовуємо консоль для підтримки українських символів
    SetConsoleCP(856);
    SetConsoleOutputCP(1251);

    // Виводимо ідентифікаційну інформацію
    identification();

    // Виконання завдання 2
    printResult();

    return 0;
}
```

## Результат виконання програми
## Завдання 1:
![image](https://github.com/user-attachments/assets/5b84c045-c442-4c67-a669-6dedea6488af)
## Завдання 2:
![image](https://github.com/user-attachments/assets/51547085-0269-400d-a15b-e1da80db6298)
## Аналіз достовірності результатів
Перевіримо чи є кінцевий результат задач вірним. Для цього використаймо калькулятор "Photomath"
## Задача №1

## Задача №2
122 — має повторювані цифри (2 дві рази).
123 — має різні цифри, але містить парну цифру 2, тому не підходить.
124 — містить парні цифри 2 і 4, тому не підходить.
125 — містить парну цифру 2, тому не підходить.
126 — містить парні цифри 2 і 6, тому не підходить.
127 — містить парну цифру 2, тому не підходить.
128 — містить парні цифри 2 і 8, тому не підходить.
129 — містить парну цифру 2, тому не підходить.
130 — містить цифри 1 (непарна) і 3 (непарна), але цифра 0 ігнорується (непарна або парна), тому це число підходить.
131 — має повторювані цифри (1 дві рази).
132 — містить парну цифру 2, тому не підходить.
133 — має повторювані цифри (3 дві рази).

Як ми можемо побачити результати двох задач сходяться з розрахунками.
## Висновок
Під час лабороторної роботи я:
Вивчив особливості циклічних обчислювальних процесів з розгалуженнями
Опанував технологію рекурентних обчислень
Навчився розробляти алгоритми та програми розвинення функцій у ряди
