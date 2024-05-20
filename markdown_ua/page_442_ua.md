Позитивне значення густини швидкості відповідає збільшенню густини даних у певній точці. Негативне значення густини швидкості відповідає зменшенню густини даних у певній точці. Загалом було показано, що коли просторово-часова ядрова функція визначена як нижче, то густина швидкості прямо пропорційна швидкості зміни густини даних у певній точці.

$$
K_{(h_s,h_t)}(X,t) = (1 - t/h_t) \cdot K'_{h_s}(X).
$$

Ця ядрова функція визначена лише для значень $t$ у діапазоні $(0, h_t)$. Гаусівська просторова ядрова функція $K'_{h_s}(\cdot)$ була використана через її відому ефективність. Зокрема, $K'_{h_s}(\cdot)$ є добутком $d$ ідентичних гаусівських ядрових функцій, а $h_s = (h_s^1, \ldots, h_s^d)$, де $h_s^i$ є параметром згладжування для виміру $i$.

Густина швидкості пов'язана з точкою даних, а також з моментом часу, тому це визначення дозволяє позначати як точки даних, так і моменти часу як викиди. Однак інтерпретація точки даних як викиду в контексті аналізу сукупних змін дещо відрізняється від попередніх визначень у цьому розділі. Викид визначається на агрегованій основі, а не конкретним чином для цієї точки. Оскільки викиди є точками даних у регіонах, де відбулися різкі зміни, викиди визначаються як точки даних $\overline{X}$ у моменти часу $t$ з незвично великими абсолютними значеннями локальної густини швидкості. За бажанням, нормальний розподіл можна використовувати для визначення екстремальних значень серед абсолютних значень густини швидкості. Таким чином, підхід густини швидкості здатний перетворити багатовимірні розподіли даних на кількісну оцінку, яку можна використовувати у поєднанні з аналізом екстремальних значень.

Важливо зазначити, що точка даних $\overline{X}$ є викидом лише в контексті сукупних змін, що відбуваються в її околиці, а не її власних властивостей як викиду. У контексті прикладу з новинами це відповідає новині, що належить до певного спалаху пов'язаних статей. Таким чином, такий підхід міг би виявляти раптову появу локальних кластерів у даних і своєчасно повідомляти відповідні точки даних. Крім того, також можливо обчислити сукупний абсолютний рівень змін (по всіх регіонах), що відбуваються в основному потоці даних. Це досягається шляхом обчислення середньої абсолютної густини швидкості по всьому просторі даних шляхом підсумовування змін у контрольних точках простору. Моменти часу з великими значеннями сукупної густини швидкості можуть бути оголошені викидами.

# 12.6 Класифікація потоків

Проблема класифікації потоків є особливо складною через вплив дрейфу концепції. Один простий підхід полягає у використанні резервуарної вибірки для створення стислого представлення навчальних даних. Це стисле представлення можна використовувати для створення офлайн-моделі. За бажанням можна використати резервуарну вибірку з затуханням для обробки дрейфу концепції. Такий підхід має перевагу в тому, що можна використовувати будь-який звичайний алгоритм класифікації, оскільки проблеми, пов'язані з парадигмою потоків, вже були вирішені на етапі вибірки. Також було запропоновано кілька спеціальних методів для класифікації потоків.

## 12.6.1 Сімейство VFDT

Дуже швидкі дерева рішень (VFDT) базуються на принципі дерев Хоффдінга. Основна ідея полягає в тому, що дерево рішень можна побудувати на вибірці дуже великого набору даних, використовуючи ретельно розроблений підхід, так що результуюче дерево буде таким самим, як і те, що було б