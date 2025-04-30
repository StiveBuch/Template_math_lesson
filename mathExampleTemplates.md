Учебный пример на C++, демонстрирующий использование шаблонов для реализации операций сложения и умножения:

```cpp
#include <iostream>
#include <string>

using namespace std;

// Шаблонная функция для сложения двух значений любого типа
template <typename T>
T add(T a, T b) {
    return a + b;
}

// Шаблонная функция для умножения двух значений любого типа
template <typename T>
T multiply(T a, T b) {
    return a * b;
}

// Шаблонный класс Calculator для работы с разными типами данных
template <class T>
class Calculator {
private:
    T num1;
    T num2;

public:
    Calculator(T n1, T n2) : num1(n1), num2(n2) {}

    T sum() {
        return num1 + num2;
    }

    T product() {
        return num1 * num2;
    }
};

// Пользовательский тип для демонстрации работы с классами
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

int main() {
    // Работа с шаблонными функциями
    cout << "Функции:\n";
    cout << "Сумма int: " << add(5, 3) << endl;
    cout << "Сумма double: " << add(2.5, 3.7) << endl;
    cout << "Конкатенация строк: " << add(string("Hello "), string("World!")) << endl;
    
    cout << "\nУмножение int: " << multiply(4, 5) << endl;
    cout << "Умножение double: " << multiply(2.5, 4.0) << endl;

    // Работа с шаблонным классом
    Calculator<int> intCalc(10, 5);
    cout << "\nКласс Calculator (int):\n";
    cout << "Сумма: " << intCalc.sum() << endl;
    cout << "Произведение: " << intCalc.product() << endl;

    Calculator<double> doubleCalc(2.5, 4.0);
    cout << "\nКласс Calculator (double):\n";
    cout << "Сумма: " << doubleCalc.sum() << endl;
    cout << "Произведение: " << doubleCalc.product() << endl;

    // Работа с пользовательским типом
    Point p1{2, 3}, p2{4, 5};
    Calculator<Point> pointCalc(p1, p2);
    Point sum = pointCalc.sum();
    Point prod = pointCalc.product();
    cout << "\nКласс Calculator (Point):\n";
    cout << "Сумма: (" << sum.x << ", " << sum.y << ")\n";
    cout << "Произведение: (" << prod.x << ", " << prod.y << ")\n";

    return 0;
}
```

Объяснение основных концепций:

1. **Шаблонные функции**:
- `template <typename T>` указывает, что функция работает с произвольным типом T
- Одна реализация работает для разных типов (int, double, string и т.д.)
- Автоматическая подстановка типа при вызове функции

2. **Шаблонные классы**:
- Класс Calculator может работать с любым типом данных
- При создании объекта необходимо явно указать тип: `Calculator<int>`
- Все методы класса автоматически адаптируются к указанному типу

3. **Пользовательские типы**:
- Для работы с шаблонами необходимо определить соответствующие операторы
- Пример с типом Point показывает расширяемость шаблонов

Преимущества шаблонов:
- Универсальность кода
- Избегание дублирования
- Типобезопасность
- Поддержка любых типов с необходимыми операциями

Этот пример демонстрирует основную идею шаблонов в C++: написание общего кода, который автоматически адаптируется к используемым типам данных.
