## 13.2.1 Нормалізація документів та обчислення подібності

Проблема нормалізації документів тісно пов'язана з обчисленням подібності. Хоча питання подібності тексту обговорюється в Розділі 3, воно також обговорюється тут для повноти. До документів застосовуються два основні типи нормалізації:

1. **Зворотна частота документа:** Слова з вищою частотою, як правило, вносять шум у операції data mining, такі як обчислення подібності. Видалення стоп-слів мотивоване цим аспектом. Концепція зворотної частоти документа узагальнює цей принцип м'якшим способом, де слова з вищою частотою мають меншу вагу.

2. **Згладжування частоти:** Повторна присутність слова в документі, як правило, значно зміщує обчислення подібності. Для забезпечення більшої стабільності обчислення подібності до частот слів застосовується функція згладжування, щоб частоти різних слів ставали більш подібними одна до одної. Слід зазначити, що згладжування частоти є необов'язковим, і його ефекти варіюються залежно від застосування. Деякі застосування, такі як кластеризація, показали порівнянну або кращу продуктивність без згладжування. Це особливо справедливо, якщо вихідні набори даних є відносно чистими і містять мало спам-документів.

Далі будуть обговорюватися ці різні типи нормалізації. Зворотна частота документа $id_i$ для $i$-го терміна є спадною функцією кількості документів $n_i$, в яких він зустрічається:

$$
id_i = \log(n/n_i). \tag{13.1}
$$

Тут $n$ позначає кількість документів у колекції. Можливі й інші способи обчислення зворотної частоти документа, хоча вплив на функцію подібності зазвичай обмежений.

Далі обговорюється концепція згладжування частоти. Ця нормалізація забезпечує, щоб надмірна присутність одного слова не спотворювала обчислення подібності. Розглянемо документ з вектором частот слів $X = (x_1 \ldots x_d)$, де $d$ - розмір лексикону. Функція згладжування $f(\cdot)$, наприклад, квадратний корінь або логарифм, застосовується до частот перед обчисленням подібності:

$$
f(x_i) = \sqrt{x_i}
$$

$$
f(x_i) = \log(x_i).
$$

Згладжування частоти є необов'язковим і часто опускається. Це еквівалентно встановленню $f(x_i)$ рівним $x_i$. Нормалізована частота $h(x_i)$ для $i$-го слова може бути визначена наступним чином:

$$
h(x_i) = f(x_i) id_i. \tag{13.2}
$$

Ця модель популярно називається моделлю tf-idf, де tf представляє частоту терміна, а idf - зворотну частоту документа.

Нормалізоване представлення документа використовується для алгоритмів data mining. Популярною мірою є косинусна міра. Косинусна міра між двома документами з необробленими частотами $X = (x_1 \ldots x_d)$ та $\mathbf{Y} = (y_1 \ldots y_d)$ визначається за допомогою їх нормалізованих представлень:

$$
\cos(X, Y) = \frac{\sum_{i=1}^{d} h(x_i) h(y_i)}{\sqrt{\sum_{i=1}^{d} h(x_i)^2} \sqrt{\sum_{i=1}^{d} h(y_i)^2}} \tag{13.3}
$$

Іншою мірою, яка рідше використовується для тексту, є коефіцієнт Жаккара $J(X, Y)$:

$$
J(X, Y) = \frac{\sum_{i=1}^{d} h(x_i) h(y_i)}{\sum_{i=1}^{d} h(x_i)^2 + \sum_{i=1}^{d} h(y_i)^2 - \sum_{i=1}^{d} h(x_i) h(y_i)} \tag{13.4}
$$