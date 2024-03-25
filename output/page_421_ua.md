Алгоритм BloomConstruct(Потік: $S$, Розмір: $m$, Кількість хеш-функцій: $w$)
початок
  Ініціалізувати всі елементи в бітовому масиві $B$ розміру $m$ до 0;
  повторювати
    Отримати наступний елемент потоку $x \in S$;
    для $i = 1$ до $w$ зробити
      Оновити $h_i(x)$-й елемент у бітовому масиві $B$ до 1;
    до кінця потоку $S$;
  повернути $B$;
кінець

[Рисунок 12.2: Оновлення блум-фільтра, сторінка 400]

неможливі з блум-фільтром. З іншого боку, якщо всі записи $h_1(y) \ldots h_w(y)$ у бітовому масиві мають значення 1, то повідомляється, що $y$ траплявся у потоці даних. Це можна ефективно перевірити, застосувавши логічну операцію "AND" до всіх бітових записів, що відповідають індексам $h_1(y) \ldots h_w(y)$ у бітовому масиві. Загальна процедура перевірки членства ілюструється на рис. 12.3. Бінарний результат для проблеми прийняття рішення щодо перевірки членства відстежується змінною $BooleanFlag$. Цей бінарний прапорець повідомляється в кінці процедури.

Підхід блум-фільтра може призводити до хибних позитивних результатів, але не до хибних негативних. Хибний позитивний результат виникає, якщо всі $w$ різних елементів масиву блум-фільтра $h_i(y)$ для $i = 1 \ldots w$ були встановлені на 1 деяким сторонніми елементом, відмінним від $y$. Це прямий результат колізій. Зі збільшенням кількості елементів у потоці даних, всі елементи у блум-фільтрі врешті-решт встановлюються на 1. У такому випадку всі запити на перевірку членства дадуть позитивну відповідь. Звичайно, це не є корисним застосуванням блум-фільтра. Тому доцільно обмежити ймовірність хибного позитивного результату в залежності від розміру фільтра та кількості різних елементів у потоці даних.

Лема 12.2.2 Розглянемо блум-фільтр $B$ з $m$ елементами та $w$ різними хеш-функціями. Нехай $n$ - кількість різних елементів у потоці $S$ на даний момент. Розглянемо елемент $y$, який ще не з'являвся у потоці. Тоді ймовірність $F$ того, що елемент $y$ буде повідомлений як хибний позитивний результат, задається наступним чином:

$$
F = \left[ 1 - \left( 1 - \frac{1}{m} \right)^{wn} \right]^w
$$

(12.18)