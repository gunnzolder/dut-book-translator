# 13.2 Підготовка документів та обчислення подібності

Оскільки текст безпосередньо не доступний у багатовимірному поданні, першим кроком є перетворення необроблених текстових документів у багатовимірний формат. У випадках, коли документи отримуються з Інтернету, потрібні додаткові кроки. У цьому розділі будуть обговорюватися ці різні кроки.

1. **Видалення стоп-слів**: Стоп-слова - це часто вживані слова в мові, які не дуже інформативні для додатків з видобутку даних. Наприклад, слова "a", "an" та "the" є поширеними словами, які надають дуже мало інформації про фактичний зміст документа. Зазвичай артиклі, прийменники та сполучники є стоп-словами. Іноді займенники також вважаються стоп-словами. Для текстового аналізу доступні стандартизовані списки стоп-слів різними мовами. Ключовим моментом є розуміння того, що майже всі документи будуть містити ці слова, і вони зазвичай не вказують на тематичний або семантичний зміст. Тому такі слова додають шум до аналізу, і їх доцільно видалити.

2. **Стемінг**: Варіації одного й того ж слова потрібно консолідувати. Наприклад, однина та множина одного й того ж слова, а також різні часи одного й того ж слова консолідуються. У багатьох випадках стемінг стосується вилучення спільного кореня зі слів, і витягнутий корінь може навіть не бути словом сам по собі. Наприклад, спільний корінь слів "hopping" та "hope" - "hop". Звичайно, недоліком є те, що слово "hop" має власне значення та вживання. Тому, хоча стемінг зазвичай покращує повноту в пошуку документів, він іноді може трохи погіршити точність. Тим не менш, стемінг зазвичай забезпечує результати вищої якості в додатках з видобутку даних.

3. **Розділові знаки**: Після виконання стемінгу видаляються розділові знаки, такі як коми та крапки з комою. Крім того, видаляються цифрові розряди. Дефіси видаляються, якщо їх видалення призводить до утворення окремих і змістовних слів. Зазвичай для цих операцій може бути доступний базовий словник. Крім того, окремі частини слова з дефісом можна розглядати як окремі слова або об'єднати їх в одне слово.

Після вищезазначених кроків результуючий документ може містити лише семантично релевантні слова. Цей документ розглядається як мішок слів (bag-of-words), в якому відносний порядок не має значення. Незважаючи на очевидну втрату інформації про порядок у цьому поданні, подання мішка слів (bag-of-words) дивовижно ефективне.