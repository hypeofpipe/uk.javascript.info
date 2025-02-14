# Базові оператори, математика

Зі шкільної програми, ми знаємо багато арифметичний операцій, такі як додавання `+`, множення `*`, віднімання `-` тощо.

У цьому розділі ми почнемо з простих операторів, потім зосередимося на специфічних для JavaScript аспектах, які не охоплені шкільною арифметикою.

## Терміни: "унарний", "бінарний", "операнд"

Перш ніж ми почнемо, давайте розберемо певну загальну термінологію.

- *Операнд* -- це те, до чого заcтосовуються оператори. Наприклад, у множенні `5 * 2` є два операнди: лівий операнд `5` і правий операнд `2`. Іноді їх називають "аргументами", а не "операндами".
- Оператор є *унарним*, якщо він має один операнд. Наприклад, унарне заперечення `-` змінює знак числа:

    ```js run
    let x = 1;

    *!*
    x = -x;
    */!*
    alert( x ); // -1, було застосоване унарне заперечення
    ```
- Оператор є *бінарним*, якщо він має два операнди. Цей же мінус існує також в бінарній формі:

    ```js run no-beautify
    let x = 1, y = 3;
    alert( y - x ); // 2, бінарний мінус віднімає значення
    ```

    Формально, в прикладах вище ми маємо два різні оператори, які позначаються однаковим символом: оператор заперечення – унарний оператор, який змінює знак числа, та оператор віднімання – бінарний оператор, який віднімає одне число від іншого.

## Математика

JavaScript підтримує такі математичні операції:

- Додавання `+`,
- Віднімання `-`,
- Множення `*`,
- Ділення `/`,
- Остача від ділення `%`,
- Піднесення до степеня (експоненція) `**`.

Перші чотири операції зрозумілі, а от про `%` та `**` потрібно сказати декілька слів.

### Остача від ділення %

Оператор остачі `%`, незважаючи на свій зовнішній вигляд, не пов’язаний з відсотками.

Результатом `a % b` є [остача](https://uk.wikipedia.org/wiki/Остача) цілочислового ділення `a` на `b`.

Наприклад:

```js run
alert( 5 % 2 ); // 1 — остача від ділення 5 на 2
alert( 8 % 3 ); // 2 — остача від ділення 8 на 3
```

### Піднесення до степеня (експоненція) **

Оператор піднесення до степеня `a ** b` множить `a` саме на себе `b` разів.

Наприклад:

```js run
alert( 2 ** 2 ); // 4  (2 помножене на себе 2 рази)
alert( 2 ** 3 ); // 8  (2 * 2 * 2, 3 рази)
alert( 2 ** 4 ); // 16 (2 * 2 * 2 * 2, 4 рази)
```

Математично, піднести до степеня також можна дробові числа. Наприклад, квадратний корінь це піднесення до степеня `1/2`:

```js run
alert( 4 ** (1/2) ); // 2 (степінь 1/2 — це теж саме, що квадратний корінь)
alert( 8 ** (1/3) ); // 2 (степінь 1/3 — це теж саме, що кубічний корінь)
```


## Об’єднання рядків через бінарний +

Розглянемо особливості операторів JavaScript, які виходять за межі шкільної арифметики.

Зазвичай оператор плюс `+` додає числа.

Але якщо бінарний `+` застосовується до рядків, він об’єднує їх:

```js
let s = "мій" + "рядок";
alert(s); // мійрядок
```

Зверніть увагу, якщо будь-який з операндів є рядком, тоді інший також перетворюється на рядок.

Наприклад:

```js run
alert( '1' + 2 ); // "12"
alert( 2 + '1' ); // "21"
```

Бачите, не має значення, чи перший операнд є рядком, чи другий.

Ось складніший приклад:

```js run
alert(2 + 2 + '1' ); // "41", а не "221"
```

Тут оператори виконуються один за одним. Перший `+` додає два числа, тому він поверне `4`; а наступний оператор `+` вже додасть (об’єднає) попередній результат з рядком `1`. У підсумку ми отримаємо рядок `41` (`4 + '1'`).

Лише бінарний `+` працює з рядками таким чином. Інші арифметичні оператори працюють тільки з числами і завжди перетворюють свої операнди на числа.

Ось приклад, як працює віднімання й ділення:

```js run
alert( 6 - '2' ); // 4, '2' перетворюється на число
alert( '6' / '2' ); // 3, обидва операнди перетворюються на числа
```

## Числове перетворення, унарний +

Плюс `+` існує у двох формах: бінарна форма, яку ми використовували вище, та унарна форма.

Унарний плюс або, іншими словами, оператор плюс `+`, застосований до єдиного операнда, нічого не зробить, якщо операнд є числом. Але якщо операнд не є числом, унарний плюс перетворить його на число.

Наприклад:

```js run
// Нема ніякого впливу на числа
let x = 1;
alert( +x ); // 1

let y = -2;
alert( +y ); // -2

*!*
// Перетворює нечислові значення
alert( +true ); // 1
alert( +"" );   // 0
*/!*
```

Він насправді працює як і `Number(...)`, але виглядає коротше.

Необхідність перетворення рядків на числа виникає дуже часто. Наприклад, якщо ми отримуємо значення з полів HTML форми, вони зазвичай є рядками. Що робити, якщо ми хочемо їх підсумувати?

Бінарний плюс додав би їх як рядки:

```js run
let apples = "2";
let oranges = "3";

alert( apples + oranges ); // "23", бінарний плюс об’єднує рядки
```

Якщо ми хочемо використовувати їх як числа, нам потрібно конвертувати, а потім підсумувати їх:

```js run
let apples = "2";
let oranges = "3";

*!*
// обидва значення перетворюються на числа перед застосуванням бінарного плюса
alert( +apples + +oranges ); // 5
*/!*

// довший варіант
// alert( Number(apples) + Number(oranges) ); // 5
```

З погляду математика надмірні плюси можуть здатися дивними. Але з погляду програміста тут немає нічого особливого: спочатку застосовуються унарні плюси, вони перетворюють рядки на числа, а потім бінарний плюс підсумовує їх.

Чому унарні плюси застосовуються до значень перед бінарними плюсами? Як ми побачимо далі, це пов’язано з їх *вищим пріоритетом*.

## Пріоритет оператора

Якщо вираз має більше одного оператора, порядок виконання визначається їх *пріоритетом*, або, іншими словами, типовим порядком першості операторів.

Зі школи ми всі знаємо, що множення у виразі `1 + 2 * 2` повинно бути обчислене перед додаванням. Саме це і є пріоритетом. Кажуть, що множення має *вищий пріоритет*, ніж додавання.

Дужки перевизначають будь-який пріоритет, тому, якщо ми не задоволені типовим пріоритетом, ми можемо використовувати дужки, щоб змінити його. Наприклад: `(1 + 2) * 2`.

У JavaScript є багато операторів. Кожен оператор має відповідний номер пріоритету. Першим виконується той оператор, який має найбільший номер пріоритету. Якщо пріоритет є однаковим, порядок виконання — зліва направо.

Ось витяг із [таблиці пріоритетів](https://developer.mozilla.org/uk/docs/Web/JavaScript/Reference/Operators/Operator_Precedence) (вам не потрібно її запам’ятовувати, але зверніть увагу, що унарні оператори мають вищий пріоритет за відповідні бінарні):

| Пріоритет | Ім’я | Знак |
|------------|------|------|
| ... | ... | ... |
| 17 | унарний плюс | `+` |
| 17 | унарне заперечення | `-` |
| 16 | піднесення до степеня | `**` |
| 15 | множення | `*` |
| 15 | ділення | `/` |
| 13 | додавання | `+` |
| 13 | віднімання | `-` |
| ... | ... | ... |
| 3 | присвоєння | `=` |
| ... | ... | ... |

Як ми бачимо, "унарний плюс" має пріоритет `17`, що вище за `13` — пріоритет "додавання" (бінарний плюс). Саме тому, у виразі `"+apples + +oranges"`, унарні плюси виконуються перед додаванням (бінарним плюсом).

## Присвоєння

Зазначимо, що присвоєння `=` також є оператором. Воно є в таблиці з пріоритетами і має дуже низький пріоритет `3`.

Тому, коли ми присвоюємо значення змінній, наприклад, `x = 2 * 2 + 1`, спочатку виконуються обчислення, а потім виконується присвоєння `=` із збереженням результату в `x`.

```js
let x = 2 * 2 + 1;

alert( x ); // 5
```

### Присвоєння = повертає результат

Той факт, що `=` є оператором, а не "магічною" конструкцією мови, має цікаве значення.

Більшість операторів в JavaScript повертають значення. Це очевидно для `+` та `-`, але це також правдиво для `=`.

Виклик `x = значення` записує `значення` у `x`, *а потім повертає його*.

Ось демонстрація, яка використовує присвоєння як частину більш складного виразу:

```js run
let a = 1;
let b = 2;

*!*
let c = 3 - (a = b + 1);
*/!*

alert( a ); // 3
alert( c ); // 0
```

У наведеному вище прикладі результат виразу `(a = b + 1)` є значенням, яке присвоювалося змінній `a` (тобто `3`). Потім воно використовується для подальших обчислень.

Чудернацький код, чи не так? Ми повинні розуміти, як це працює, бо іноді ми бачимо подібне у бібліотеках JavaScript.

Однак, будь ласка, не пишіть свій код таким чином. Такі трюки, безумовно, не роблять код більш зрозумілим або читабельним.

### Ланцюгові присвоєння

Іншою цікавою особливістю є здатність ланцюгового присвоєння:

```js run
let a, b, c;

*!*
a = b = c = 2 + 2;
*/!*

alert( a ); // 4
alert( b ); // 4
alert( c ); // 4
```

Ланцюгове присвоєння виконується справа наліво. Спочатку обчислюється самий правий вираз `2 + 2`, а потім результат присвоюється змінним ліворуч: `c`, `b` та `a`. Зрештою всі змінні мають спільне значення.

Знову таки, щоб покращити читабельність коду, краще розділяти подібні конструкції на декілька рядків:

```js
c = 2 + 2;
b = c;
a = c;
```
Так легше прочитати, особливо коли швидко переглядати код.

## Оператор "модифікувати та присвоїти"

Часто нам потрібно застосувати оператор до змінної і зберегти новий результат у ту ж саму змінну.

Наприклад:

```js
let n = 2;
n = n + 5;
n = n * 2;
```

Цей запис можна скоротити за допомогою операторів `+=` та `*=`:

```js run
let n = 2;
n += 5; // тепер n = 7 (те ж саме, що n = n + 5)
n *= 2; // тепер n = 14 (те ж саме, що n = n * 2)

alert( n ); // 14
```

Короткі оператори "модифікувати та присвоїти" існують для всіх арифметичних та побітових операторів: `/=`, `-=` тощо.

Ці оператори мають такий же пріоритет, як і звичайне присвоєння, тому вони виконуються після більшості інших обчислень:

```js run
let n = 2;

n *= 3 + 5;

alert( n ); // 16  (права частина обчислюється першою, так само, як n *= 8)
```

## Інкремент/декремент

<!-- Не можна використовувати -- в заголовку, тому що вбудований парсер перетворює це на довге тире – -->

Збільшення або зменшення на одиницю є однією з найпоширеніших числових операцій.

Тому для цього існують спеціальні оператори:

- **Інкремент** `++` збільшує змінну на 1:

    ```js run no-beautify
    let counter = 2;
    counter++;        // працює так само, як counter = counter + 1, але запис коротше
    alert( counter ); // 3
    ```
- **Декремент** `--` зменшує змінну на 1:

    ```js run no-beautify
    let counter = 2;
    counter--;        // працює так само, як counter = counter - 1, але запис коротше
    alert( counter ); // 1
    ```

```warn
Інкремент/декремент можуть застосовуватись лише до змінних. Спроба використати їх із значенням, як от `5++`, призведе до помилки.
```

Оператори `++` та `--` можуть розташовуватись до або після змінної.

- Коли оператор йде за змінною, він знаходиться у "постфіксній формі": `counter++`.
- "Префіксна форма" – це коли оператор йде попереду змінної: `++counter`.

Обидві ці інструкції роблять те ж саме: збільшують `counter` на `1`.

Чи є різниця? Так, але ми можемо побачити її тільки при використанні значення, яке повертають `++/--`.

Давайте розберемось. Як нам відомо, усі оператори повертають значення. Інкремент/декремент не є винятком. Префіксна форма повертає нове значення, тоді як постфіксна форма повертає старе значення (до збільшення/зменшення).

Щоб побачити різницю, наведемо приклад:

```js run
let counter = 1;
let a = ++counter; // (*)

alert(a); // *!*2*/!*
```

У рядку `(*)`, *префіксна* форма `++counter` збільшує `counter` та повертає нове значення, `2`. Отже, `alert` показує `2`.

Тепер скористаємося постфіксною формою:

```js run
let counter = 1;
let a = counter++; // (*) змінили ++counter на counter++

alert(a); // *!*1*/!*
```

У рядку `(*)`, *постфіксна* форма `counter++` також збільшує `counter`, але повертає *старе* значення (до інкременту). Отже, `alert` показує `1`.

Підсумки:

- Якщо результат збільшення/зменшення не використовується, немає ніякої різниці, яку форму використовувати:

    ```js run
    let counter = 0;
    counter++;
    ++counter;
    alert( counter ); // 2, у рядках вище робиться одне і те ж саме
    ```
- Якщо ми хочемо збільшити значення *та* негайно використати результат оператора, нам потрібна префіксна форма:

    ```js run
    let counter = 0;
    alert( ++counter ); // 1
    ```
- Якщо ми хочемо збільшити значення, але використати його попереднє значення, нам потрібна постфіксна форма:

    ```js run
    let counter = 0;
    alert( counter++ ); // 0
    ```

````smart header="Інкремент/декремент серед інших операторів"
Оператори `++/--` також можуть використовуватись всередині виразів. Їх пріоритет вищий за більшість інших арифметичних операцій.

Наприклад:

```js run
let counter = 1;
alert( 2 * ++counter ); // 4
```

Порівняйте з:

```js run
let counter = 1;
alert( 2 * counter++ ); // 2, тому що counter++ повертає "старе" значення
```

Хоча з технічного погляду це допустимо, такий запис робить код менш читабельним. Коли один рядок робить кілька речей -- це не добре.

При читанні коду швидке "вертикальне" сканування оком може легко пропустити щось подібне до `counter++`, і не буде очевидним, що змінна була збільшена.

Ми рекомендуємо стиль "одна лінія -- одна дія":

```js run
let counter = 1;
alert( 2 * counter );
counter++;
```
````

## Побітові оператори

Побітові оператори розглядають аргументи як 32-бітні цілі числа та працюють на рівні їх двійкового представлення.

Ці оператори не є специфічними для JavaScript. Вони підтримуються у більшості мов програмування.

Список операторів:

- AND(і) ( `&` )
- OR(або) ( `|` )
- XOR(побітове виключне або) ( `^` )
- NOT(ні) ( `~` )
- LEFT SHIFT(зсув ліворуч) ( `<<` )
- RIGHT SHIFT(зсув праворуч) ( `>>` )
- ZERO-FILL RIGHT SHIFT(зсув праворуч із заповненням нулями) ( `>>>` )

Ці оператори використовуються тоді, коли нам потрібно "возитися" з числами на дуже низькому (побітовому) рівні (тобто — вкрай рідко). Найближчим часом такі оператори нам не пригодяться, оскільки у веб-розробці вони майже не використовуються. Проте в таких областях, як криптографія, вони корисні. Ви можете прочитати [розділ про них](https://developer.mozilla.org/uk/docs/Web/JavaScript/Guide/Вирази_та_оператори#Бітові_оператори) на MDN, якщо виникне потреба.

## Кома

Оператор "кома" (`,`) незвичайний і застосовується дуже рідко. Іноді цей оператор використовують для написання коротшого коду, тому нам потрібно знати його, щоб розуміти, що відбувається.

Оператор кома дозволяє обчислити кілька виразів, розділивши їх комою `,`. Кожен з них обчислюється, але повертається тільки результат останнього.

Наприклад:

```js run
*!*
let a = (1 + 2, 3 + 4);
*/!*

alert( a ); // 7 (результат обчислення 3 + 4)
```

Тут обчислюється перший вираз `1 + 2` і його результат викидається. Потім обчислюється `3 + 4` і повертається як результат.

```smart header="Кома має дуже низький пріоритет"
Зверніть увагу, що оператор "кома" має дуже низький пріоритет, нижчий за `=`, тому дужки є важливими в наведеному вище прикладі.

Без дужок, у виразі `a = 1 + 2, 3 + 4` спочатку обчислюються оператори `+`, підсумовуючи числа у `a = 3, 7`; потім оператор присвоєння `=` присвоює `a = 3`, а решта (число `7` після коми) ігнорується. Це як записати вираз `(a = 1 + 2), 3 + 4`.
```

Чому нам потрібен оператор, що викидає все, окрім останнього виразу?

Іноді його використовують в більш складних конструкціях, щоб помістити кілька дій в один рядок.

Наприклад:

```js
// три операції в одному рядку
for (*!*a = 1, b = 3, c = a * b*/!*; a < 10; a++) {
 ...
}
```

Такі трюки використовуються в багатьох фреймворках JavaScript. Саме тому ми їх згадуємо. Але зазвичай вони не покращують читабельність коду, тому ми повинні добре подумати перед їх використанням.
