Вот готовая шпора с кодом и кратким объяснением для каждой задачи в формате Markdown.

---

### **Задача 1319. Отель**

*   **Суть:** Заполнить матрицу $N \times N$ числами от $1$ до $N^2$ по диагоналям (справа-налево, сверху-вниз).
*   **Логика:** Ддва цикла. 1-й заполняет диагонали, стартующие с верхней строки. 2-й заполняет диагонали, стартующие с левого столбца.
*   **Сложность:** $O(N^2)$.

```cpp
#include <iostream>
#include <vector>

int main() {
    int N;
    std::cin >> N;

    std::vector<std::vector<int>> matrix(N, std::vector<int>(N, 0));
    int num = 1;

    // Заполняем по диагоналям, начинающимся сверху
    for (int start_col = N - 1; start_col >= 0; --start_col) {
        int row = 0;
        int col = start_col;
        while (row < N && col < N) {
            matrix[row][col] = num++;
            row++;
            col++;
        }
    }

    // Заполняем по диагоналям, начинающимся слева
    for (int start_row = 1; start_row < N; ++start_row) {
        int row = start_row;
        int col = 0;
        while (row < N and col < N) {
            matrix[row][col] = num++;
            row++;
            col++;
        }
    }

    // Выводим результат
    for (int i = 0; i < N; ++i) {
        for (int j = 0; j < N; ++j) {
            std::cout << matrix[i][j];
            if (j < N - 1) std::cout << " ";
        }
        std::cout << std::endl;
    }
    return 0;
}
```

---

### **Задача 1567. SMS-спам**

*   **Суть:** Посчитать стоимость SMS (цена символа = номеру на кнопке телефона).
*   **Логика:** Проходим по строке. Группируем символы через `if/else`: `a-c` $\to$ +1, `d-f` $\to$ +1, знаки препинания имеют свою цену.
*   **Сложность:** $O(L)$ (длина строки).

```cpp
#include <iostream>
#include <string>

int main() {
    std::string msg;
    std::getline(std::cin, msg);

    int ans = 0;

    for (char c : msg) {
        if (c >= 'a' and c <= 'c') ans += (c - 'a' + 1);
        else if (c >= 'd' and c <= 'f') ans += (c - 'd' + 1);
        else if (c >= 'g' and c <= 'i') ans += (c - 'g' + 1);
        else if (c >= 'j' and c <= 'l') ans += (c - 'j' + 1);
        else if (c >= 'm' and c <= 'o') ans += (c - 'm' + 1);
        else if (c >= 'p' and c <= 'r') ans += (c - 'p' + 1);
        else if (c >= 's' and c <= 'u') ans += (c - 's' + 1);
        else if (c >= 'v' and c <= 'x') ans += (c - 'v' + 1);
        else if (c >= 'y' and c <= 'z') ans += (c == 'y' ? 1 : 2);
        else if (c == ' ' or c == '.') ans += 1;
        else if (c == ',') ans += 2;
        else if (c == '!') ans += 3;
    }

    std::cout << ans << std::endl;
    return 0;
}
```

---

### **Задача 1581. Работа в команде**

*   **Суть:** Сжатие последовательности (RLE). Вывести количество подряд идущих чисел и само число.
*   **Логика:** Если `a[i] == a[i+1]`, увеличиваем счетчик. Если нет — выводим счетчик и число, сбрасываем счетчик.
*   **Сложность:** $O(N)$.

```cpp
#include <iostream>
#include <vector>

int main() {
    int n;
    std::cin >> n;
    if (n == 0) return 0;

    std::vector<int> a(n);
    for (int i = 0; i < n; ++i) std::cin >> a[i];

    int cnt = 1;
    for (int i = 0; i < n; ++i) {
        if (i == n - 1 or a[i] != a[i + 1]) {
            std::cout << cnt << " " << a[i];
            if (i != n - 1) std::cout << " ";
            cnt = 1;
        } else {
            cnt++;
        }
    }
    std::cout << std::endl;
    return 0;
}
```

---

### **Задача 1585. Пингвины**

*   **Суть:** Найти самую часто встречающуюся строку ("Emperor", "Little", "Macaroni").
*   **Логика:** 3 счетчика. Читаем строки через `getline`, сравниваем, инкрементируем нужный счетчик. В конце выводим победителя.
*   **Сложность:** $O(N)$.

```cpp
#include <iostream>
#include <string>

int main() {
    int n;
    std::cin >> n;
    int emperor_count = 0, little_count = 0, macaroni_count = 0;

    std::string name;
    std::getline(std::cin, name); // Считываем \n после числа n

    for (int i = 0; i < n; ++i) {
        std::getline(std::cin, name);
        if (name == "Emperor Penguin") emperor_count++;
        else if (name == "Little Penguin") little_count++;
        else if (name == "Macaroni Penguin") macaroni_count++;
    }

    if (emperor_count > little_count and emperor_count > macaroni_count)
        std::cout << "Emperor Penguin" << std::endl;
    else if (little_count > emperor_count and little_count > macaroni_count)
        std::cout << "Little Penguin" << std::endl;
    else
        std::cout << "Macaroni Penguin" << std::endl;

    return 0;
}
```

---

### **Задача 1910. Руины титанов**

*   **Суть:** Найти тройку подряд идущих элементов с максимальной суммой.
*   **Логика:** Проход окном размером 3. Если сумма текущей тройки больше максимума, обновляем. Ответ: `max_sum` и индекс `i + 2` (середина тройки в 1-нумерации).
*   **Сложность:** $O(N)$.

```cpp
#include <iostream>
#include <vector>

int main() {
    int n;
    std::cin >> n;
    std::vector<int> a(n);
    for (int i = 0; i < n; ++i) std::cin >> a[i];

    int max_sum = 0;
    int middle_pos = 0;

    for (int i = 0; i < n - 2; ++i) {
        int current_sum = a[i] + a[i + 1] + a[i + 2];
        if (current_sum > max_sum) {
            max_sum = current_sum;
            middle_pos = i + 2; 
        }
    }
    std::cout << max_sum << " " << middle_pos << std::endl;
    return 0;
}
```

---

### **Задача 1924. Четыре чертёнка**

*   **Суть:** Определить победителя (четность суммы чисел от $1$ до $N$).
*   **Логика:** Зависит от `n % 4`. Если 0 или 3 $\to$ "black", иначе $\to$ "grimy".
*   **Сложность:** $O(1)$.

```cpp
#include <iostream>

int main() {
    int n;
    std::cin >> n;
    int remainder = n % 4;

    if (remainder == 0 or remainder == 3) {
        std::cout << "black" << std::endl;
    } else {
        std::cout << "grimy" << std::endl;
    }
    return 0;
}
```

---

### **Задача 2023. Дональд-почтальон**

*   **Суть:** Посчитать шаги между тремя ящиками (позиции 1, 2, 3) в зависимости от имени адресата.
*   **Логика:** Три списка имен. Определяем, в каком списке имя (получаем `target`). Добавляем к пути `abs(target - current)`.
*   **Сложность:** $O(N)$.

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <cmath>

int determine_group(const std::string& name,
                   const std::vector<std::string>& g1,
                   const std::vector<std::string>& g2,
                   const std::vector<std::string>& g3) {
    if (std::find(g1.begin(), g1.end(), name) != g1.end()) return 1;
    if (std::find(g2.begin(), g2.end(), name) != g2.end()) return 2;
    return 3;
}

int main() {
    std::vector<std::string> g1 = {"Alice", "Ariel", "Aurora", "Phil", "Peter", "Olaf", "Phoebus", "Ralph", "Robin"};
    std::vector<std::string> g2 = {"Bambi", "Belle", "Bolt", "Mulan", "Mowgli", "Mickey", "Silver", "Simba", "Stitch"};
    std::vector<std::string> g3 = {"Dumbo", "Genie", "Jiminy", "Kuzco", "Kida", "Kenai", "Tarzan", "Tiana", "Winnie"};

    int n;
    std::cin >> n;
    std::cin.ignore(); 

    int current_pos = 1;
    int steps = 0;

    for (int i = 0; i < n; ++i) {
        std::string name;
        std::getline(std::cin, name);
        int target = determine_group(name, g1, g2, g3);
        steps += std::abs(target - current_pos);
        current_pos = target;
    }
    std::cout << steps << std::endl;
    return 0;
}
```

---

### **Задача 2056. Стипендия**

*   **Суть:** Определить тип стипендии по оценкам.
*   **Логика:** Флаги `t` (есть тройка) и `f` (все пятерки). Если есть 3 $\to$ None. Если все 5 $\to$ Named. Если средний балл $\ge 4.5$ $\to$ High. Иначе $\to$ Common.
*   **Сложность:** $O(N)$.

```cpp
#include <iostream>

int main() {
    int n;
    std::cin >> n;

    int x;
    int s = 0;
    bool t = false; // Есть тройка?
    bool f = true;  // Все пятерки?

    for (int i = 0; i < n; ++i) {
        std::cin >> x;
        s += x;
        if (x == 3) t = true;
        if (x != 5) f = false;
    }

    if (t) std::cout << "None" << std::endl;
    else if (f) std::cout << "Named" << std::endl;
    else {
        double a = static_cast<double>(s) / n;
        if (a >= 4.5) std::cout << "High" << std::endl;
        else std::cout << "Common" << std::endl;
    }
    return 0;
}
```
