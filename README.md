# goit-de-hw-04

## Висновоки:
 Кількість Jobs зменшується при використанні `cache()` завдяки тому, що Spark зберігає проміжні результати в пам'яті, що дозволяє уникнути повторного обчислення тих самих перетворень. Це значно підвищує ефективність і швидкість виконання, особливо при роботі з великими наборами даних, де однакові обчислення виконуються декілька разів.

При використанні функції `cache()` кількість Jobs у Spark зменшується завдяки оптимізації повторного доступу до даних. Ось основні причини, чому ми зменшили кількість Jobs у наведеному прикладі:

1. **Кешування в пам'яті**: Коли ми викликаємо `cache()` на DataFrame, Spark зберігає результати цього проміжного обчислення в пам'яті. Це означає, що при виконанні подальших дій (`action`) над тими самими даними, Spark не потребує повторно обчислювати попередні перетворення. Замість цього він просто отримує дані з кешу, що значно скорочує кількість необхідних Jobs.

2. **Зменшення перерахунків**: У попередніх прикладах, де `cache()` не використовувалась, кожен раз при виклику `collect()` або іншої дії, Spark був змушений повторно виконувати всі перетворення для отримання результату. Це включає весь процес — від читання даних до групування та обчислення. Використовуючи `cache()`, Spark зберігає результат проміжних перетворень і виконує лише необхідні дії, що зменшує кількість Jobs.

3. **Ліниве виконання (Lazy Evaluation)**: Spark використовує механізм лінивого виконання, що означає, що обчислення починаються лише тоді, коли є необхідність отримати результат (при виконанні дій — `action`). Використання `cache()` призводить до того, що обчислення для кешування виконуються один раз, і потім результати використовуються повторно без створення нових Jobs.

