Вот как можно реализовать аналогичную функциональность без использования шаблонов в C++:

```cpp
#include <iostream>
#include <string>

using namespace std;

// Отдельные функции для каждого типа данных

// Для целых чисел
int add_int(int a, int b) {
    return a + b;
}

int multiply_int(int a, int b) {
    return a * b;
}

// Для чисел с плавающей точкой
double add_double(double a, double b) {
    return a + b;
}

double multiply_double(double a, double b) {
    return a * b;
}

// Для строк
string add_string(const string& a, const string& b) {
    return a + b;
}

// Отдельные классы для каждого типа данных

// Класс Calculator для int
class IntCalculator {
private:
    int num1;
    int num2;

public:
    IntCalculator(int n1, int n2) : num1(n1), num2(n2) {}

    int sum() {
        return num1 + num2;
    }

    int product() {
        return num1 * num2;
    }
};

// Класс Calculator для double
class DoubleCalculator {
private:
    double num1;
    double num2;

public:
    DoubleCalculator(double n1, double n2) : num1(n1), num2(n2) {}

    double sum() {
        return num1 + num2;
    }

    double product() {
        return num1 * num2;
    }
};

// Пользовательский тип
struct Point {
    int x;
    int y;
    
    Point operator+(const Point& other) {
        return {x + other.x, y + other.y};
    }
    
    Point operator*(const Point& other) {
        return {x * other.x, y * other.y};
    }
};

// Класс Calculator для Point
class PointCalculator {
private:
    Point p1;
    Point p2;

public:
    PointCalculator(Point pt1, Point pt2) : p1(pt1), p2(pt2) {}

    Point sum() {
        return p1 + p2;
    }

    Point product() {
        return p1 * p2;
    }
};

int main() {
    // Работа с функциями
    cout << "Функции:\n";
    cout << "Сумма int: " << add_int(5, 3) << endl;
    cout << "Сумма double: " << add_double(2.5, 3.7) << endl;
    cout << "Конкатенация строк: " << add_string("Hello ", "World!") << endl;
    
    cout << "\nУмножение int: " << multiply_int(4, 5) << endl;
    cout << "Умножение double: " << multiply_double(2.5, 4.0) << endl;

    // Работа с классами
    IntCalculator intCalc(10, 5);
    cout << "\nКласс IntCalculator:\n";
    cout << "Сумма: " << intCalc.sum() << endl;
    cout << "Произведение: " << intCalc.product() << endl;

    DoubleCalculator doubleCalc(2.5, 4.0);
    cout << "\nКласс DoubleCalculator:\n";
    cout << "Сумма: " << doubleCalc.sum() << endl;
    cout << "Произведение: " << doubleCalc.product() << endl;

    // Работа с пользовательским типом
    Point p1{2, 3}, p2{4, 5};
    PointCalculator pointCalc(p1, p2);
    Point sum = pointCalc.sum();
    Point prod = pointCalc.product();
    cout << "\nКласс PointCalculator:\n";
    cout << "Сумма: (" << sum.x << ", " << sum.y << ")\n";
    cout << "Произведение: (" << prod.x << ", " << prod.y << ")\n";

    return 0;
}
```

Основные отличия от версии с шаблонами:

1. **Дублирование кода**:
- Для каждого типа данных созданы отдельные функции:
  ```cpp
  add_int(), add_double(), add_string()
  multiply_int(), multiply_double()
  ```
- Для каждого типа данных созданы отдельные классы:
  ```cpp
  IntCalculator, DoubleCalculator, PointCalculator
  ```

2. **Отсутствие универсальности**:
- Невозможно использовать один класс или функцию для работы с разными типами
- Для добавления нового типа нужно создавать новые функции и классы

3. **Больший объем кода**:
- Каждая новая функциональность требует копирования и модификации существующего кода
- Увеличивается вероятность ошибок при изменении

4. **Меньшая гибкость**:
- Жесткая привязка к конкретным типам данных
- Невозможно использовать с пользовательскими типами без явной реализации

Преимущества шаблонной версии становятся очевидными:
- Уменьшение дублирования кода
- Лучшая поддерживаемость
- Более чистый и компактный код
- Легкое расширение для новых типов

Этот пример показывает, как шаблоны помогают избежать "копипаста" и создавать более универсальные и гибкие решения в C++.
