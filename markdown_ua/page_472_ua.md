Формулювання оптимізації (OP2) відрізняється від (OP1) тим, що воно має лише одну змінну нестачі $\xi$, але $2^n$ обмежень, які представляють суму кожної підмножини обмежень у (OP1). Можна показати, що існує взаємно однозначна відповідність між розв'язками (OP1) та (OP2).

**Лема 13.5.1**
*Існує взаємно однозначна відповідність між розв'язками (OP1) та (OP2), з рівними значеннями $W = W^*$ в обох моделях, та $\xi^* = \frac{\sum_{i=1}^n \xi_i}{n}$.*

**Доведення:** Ми покажемо, що якщо зафіксувати те саме значення $W$ для (OP1) та (OP2), то це призведе до однакового значення цільової функції. Перший крок - вивести змінні нестачі в термінах цього значення $W$ для (OP1) та (OP2). Для задачі (OP1) можна вивести з обмежень нестачі, що оптимальне значення $\xi_i$ досягається для $\xi_i = \max \{0, 1 - y_i W \cdot X_i \}$, щоб мінімізувати штраф за нестачу. Для задачі OP2 можна отримати аналогічний результат для $\xi$:

$$
\xi = \max_{u_1, \ldots, u_n} \left\{ \frac{\sum_{i=1}^n u_i}{n} - \frac{1}{n} \sum_{i=1}^n u_i y_i W \cdot X_i \right\}. \tag{13.24}
$$

Оскільки ця функція є лінійно роздільною за $u_i$, можна перенести максимум всередину суми та незалежно оптимізувати для кожного $u_i$:

$$
\xi = \frac{1}{n} \sum_{i=1}^n \max_{u_i} u_i \left\{ \frac{1}{n} - \frac{1}{n} y_i W \cdot X_i \right\}. \tag{13.25}
$$

Для оптимальності значення $u_i$ слід обрати рівним 1 лише для додатних значень $\left\{ \frac{1}{n} - \frac{1}{n} y_i W \cdot X_i \right\}$ та 0 в іншому випадку. Тому можна показати наступне:

$$
\xi = \frac{1}{n} \sum_{i=1}^n \max \left\{ 0, \frac{1}{n} - \frac{1}{n} y_i W \cdot X_i \right\} \tag{13.26}
$$

$$
= \frac{1}{n} \sum_{i=1}^n \max \{0, 1 - y_i W \cdot X_i \} = \frac{\sum_{i=1}^n \xi_i}{n} \tag{13.27}
$$

Ця взаємно однозначна відповідність між оптимальними значеннями $W$ у (OP1) та (OP2) означає, що дві задачі оптимізації є еквівалентними.

Таким чином, визначивши оптимальний розв'язок задачі (OP2), можна також визначити оптимальний розв'язок задачі (OP1). Звичайно, поки що не зрозуміло, чому формулювання (OP2) є кращим за (OP1). Зрештою, задача (OP2) містить експоненційну кількість обмежень, і здається, що неможливо навіть перерахувати обмеження, не кажучи вже про їх розв'язання.

Проте формулювання оптимізації (OP2) має деякі переваги над (OP1). По-перше, єдина змінна нестачі вимірює виконання всіх обмежень. Це означає, що всі обмеження можна виразити через $(W, \xi)$. Тому, якщо розв'язати задачу оптимізації лише з підмножиною $2^n$ обмежень, а решту задовольнити з точністю $\epsilon$ за допомогою $(W, \xi)$, то гарантовано, що $(W, \xi + \epsilon)$ є допустимим для повного набору обмежень.

Ключ у тому, щоб ніколи не використовувати всі обмеження явно. Натомість використовується невелика підмножина $\mathcal{WS}$ з $2^n$ обмежень як робоча множина. Ми починаємо з порожньої робочої множини $\mathcal{WS}$. Відповідна задача оптимізації розв'язується, і до робочої множини додається найбільш порушене обмеження серед обмежень, яких немає в $\mathcal{WS}$. Вектор $U$ для найбільш порушеного обмеження відносно легко знайти. Це робиться шляхом присвоєння $u_i$ значення 1, якщо $y_i W \cdot X_i < 1$, і 0 в іншому випадку. Отже, ітераційні кроки для додавання до робочої множини $\mathcal{WS}$ є такими: