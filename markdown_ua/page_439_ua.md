Кожен часовий ряд розглядається як окрема одиниця, тоді як часові кореляції набагато слабші для багатовимірних даних. У цьому розділі буде розглянуто лише виявлення аномалій у багатовимірних потоках даних, тоді як методи для часових рядів будуть розглянуті в Розділі 14.

Сценарій багатовимірного потоку даних подібний до статичного багатовимірного аналізу аномалій. Єдина відмінність полягає у додаванні часової компоненти до аналізу, хоча ця часова компонента набагато слабша, ніж у випадку часових рядів. У контексті багатовимірних потоків даних ефективність є важливою проблемою, оскільки аномалії потрібно виявляти швидко. Існує два види аномалій, які можуть виникати в контексті багатовимірних потоків даних.

1. Перший ґрунтується на виявленні аномалій окремих записів. Наприклад, перша новина на певну тему є аномалією цього типу. Таку аномалію також називають новизною.

2. Другий ґрунтується на змінах в агрегованих тенденціях багатовимірних даних. Наприклад, незвичайна подія, така як терористичний акт, може призвести до сплеску новин на певну тему. Це представляє агреговану аномалію на основі певного часового вікна. Другий вид зміни майже завжди починається з індивідуальної аномалії першого типу. Однак індивідуальна аномалія першого типу не завжди розвивається в агреговану точку зміни. Це тісно пов'язано з концепцією дрейфу концепції. Хоча дрейф концепції зазвичай є поступовим, різку зміну можна розглядати як аномальний момент часу, а не аномальну точку даних.

Обидва види аномалій (або точок зміни) будуть розглянуті в цьому розділі.

## 12.5.1 Окремі точки даних як аномалії

Проблема виявлення окремих точок даних як аномалій тісно пов'язана з проблемою невідомого виявлення новизни, особливо коли використовується вся історія потоку даних. Ця проблема широко вивчається в текстовій області в контексті проблеми виявлення першої історії. Такі новинки часто є трендсеттерами і врешті-решт можуть стати частиною нормальних даних. Однак, коли окремий запис оголошується аномалією в контексті вікна точок даних, він не обов'язково є новизною. У цьому контексті алгоритми, засновані на близькості, особливо легко узагальнюються на інкрементний сценарій шляхом майже прямого застосування відповідних алгоритмів до вікна точок даних.

Алгоритми, засновані на відстані, можна легко узагальнити на потоковий сценарій. Початкове визначення аномалій на основі відстані модифікується наступним чином:

*Оцінка аномалії точки даних визначається за її відстанню до k-найближчих сусідів у часовому вікні довжиною $W$.*

Зверніть увагу, що це відносно пряма модифікація початкового визначення аномалій на основі відстані. Коли все вікно точок даних можна зберігати в оперативній пам'яті, досить легко визначити аномалії, обчисливши оцінку кожної точки даних у вікні. Однак інкрементне обслуговування оцінок точок даних є більш складним завданням через додавання та видалення точок даних з вікна. Крім того, деякі алгоритми, такі як LOF, вимагають перерахунку статистик, таких як відстані досяжності. Алгоритм LOF був розширений на інкрементний сценарій. У цьому процесі виконуються два кроки: