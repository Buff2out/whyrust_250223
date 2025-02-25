- [Почему я выбрал Rust](#Почему-я-выбрал-Rust)
- [От отрицания сразу к принятию](#От-отрицания-сразу-к-принятию)
- [Установка Rust](#Установка-Rust)
- [Начало работы как я создал этот проект](#Начало-работы-как-я-создал-этот-проект)
- [Переменные и иммутабельность](#Переменные-и-иммутабельность)
- [Типы данных](#Типы-данных)
- [Функции](#Функции)
- [Циклы](#Циклы)
- [Работа с памятью ownership и borrowing](#Работа-с-памятью-ownership-и-borrowing)
- [Structs](#Structs)
- [enums](#enums)
- [match null и использование Option Result](#match-null-и-использование-Option-Result)
- [Unsafe rust.](#Unsafe-rust)


# Почему я выбрал Rust

![alt text](image-6.png)

> рейтинг любимых языков программирования по опросу stackoverflow:

Опрос:
https://survey.stackoverflow.co/2024/technology#admired-and-desired

![alt text](image-4.png)

Что меня первично оттолкнуло:

> Излишняя любовь сообществом - подозрительно.

Складывается вопрос - почему так любят?

# От отрицания сразу к принятию

Проект начал своё начало в Mozilla у одного из сотрудников как хобби. Интерес в компании к проекту увеличился.

Сейчас разработкой занимается не Mozilla, Rust Foundation. Привлекаются инвестиции и разработки ведутся из разных компаний, одни из крупных: 

##### Cloudflare

Cloudflare открыла код Rust-фреймворка для программируемых сетевых сервисов — Pingora

https://habr.com/ru/articles/797015/ 

##### Dropbox

Использует Rust в своих продуктах

https://github.com/orgs/dropbox/repositories?q=rust

##### Microsoft:

Инвестиции: 

https://blobstreaming.org/microsofts-1m-vote-of-confidence-in-rusts-future/

Поиск работников для переписывания кода: 

https://devdigest.today/goto/2435

Репозиторий: 

https://github.com/orgs/microsoft/repositories?q=rust


##### Amazon

Инвестиции и совместная разработка проекта вместе с Rust Foundation над улучшением безопасности в Unsafe Mode:

(https://aws.amazon.com/blogs/opensource/verify-the-safety-of-the-rust-standard-library/)

##### Linux Foundation

Позиция Линуса Торвальдса по продвижению Rust в ядро.

https://www.opennet.ru/opennews/art.shtml?num=62764


> Производительность сопоставимая с C и C++ как решение проблем ЯП с Garbage Collector

Latency vs Throughput  

    Latency  — это время, необходимое для завершения одной операции.
    Throughput  — это количество операций, которые система может обработать за единицу времени.

Пример: 

    Если у вас низкая latency (быстрый отклик), но маленький throughput, система будет быстро отвечать на каждый запрос, но сможет обработать их ограниченное количество.
    Если у вас высокий throughput, но большая latency, система сможет обработать много запросов, но каждый из них будет выполняться медленнее.
     

![alt text](image-8.png)


![alt text](image-9.png)

исследование:
https://arxiv.org/html/2405.11182v1
https://nuancesprog.ru/p/14464/

> Фокус на безопасности - как решение проблем C и C++

Иммутабельность переменных по умолчанию, новая парадигма работы с памятью: borrowing и ownership. Решение Race Condition, Memory leaks, dangling pointers, buffer overflows, double free memory.

# Установка Rust

Скачивал Rust на Arch официально рекомендуемым способом - через менеджер обновлений rustup.

(Гайд: https://wiki.archlinux.org/title/Rust_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9))

    Компилятор Rust (rustc) : 
        Основной компилятор Rust, который преобразует ваш код на Rust в машинный код.
         

    Cargo : 
        Система сборки и управление зависимостями для Rust-проектов.
        Позволяет создавать проекты, управлять зависимостями из crates.io, компилировать и запускать программы.
         

    Standard Library : 
        Стандартная библиотека Rust, которая предоставляет базовые типы данных, коллекции, потоки, I/O и другие функциональные возможности.
         

    Rust Source Code  (при необходимости): 
        Источники стандартной библиотеки Rust, которые могут быть полезны для отладки или расширения.
         

    Документация  (опционально): 
        Локальная копия документации Rust, включая The Book, API справочник и другие ресурсы.
         

    Дополнительные компоненты : 
        Например, RLS (Rust Language Server) для поддержки IDE, rust-analyzer, Clippy (анализатор кода), Miri (инструмент для проверки безопасности памяти) и другие инструменты.

### LLVM

Rust через rustup автоматически скачивает предварительно скомпилированную версию LLVM, которая используется для компиляции кода.

### Какие зависимости требуются для работы Rust? 

1. LLVM : 

    Rust использует LLVM как backend для генерации машинного кода.
     

2. C++ Standard Library : 

    Для некоторых платформ (например, Linux) требуется C++ стандартная библиотека (обычно libstdc++ или libc++), так как Rust использует её для некоторых низкоуровневых операций.
     

3. Системные зависимости : 

    На разных системах могут потребоваться дополнительные пакеты для успешной работы Rust. Например:
        Linux : build-essential, clang, cmake, pkg-config.
        macOS : Xcode Command Line Tools (xcode-select --install).
        Windows : MSVC или MinGW (в зависимости от выбранного компилятора).
         
     

4. Для некоторых задач могут потребоваться дополнительные инструменты : 

    Если вы работаете с FFI (Foreign Function Interface) или вызываете системные API, может потребоваться установка соответствующих заголовочных файлов и библиотек.
     

>Для дебаггинга В VScode потребуется CodeLLDB

### Обновление до новой версии Rust:

`rustup update`

![alt text](image-10.png)

# Начало работы как я создал этот проект

Команда

`cargo new whyrust_250223`

Cоздаёт и инициализирует проект вместе с cargo.toml - конфигурационным файлом с зависимостями и описанием как менеджер cargo будет билдить и запускать проект.

    my_project/
    ├── Cargo.toml
    ├── src/
    │   └── main.rs
    └── .gitignore
         

Команда

`cargo init`

Инициализирует аналогичную схему в уже созданной директории

Но если директории не существует, то команды 

`cargo new <projectname>`

и

`cargo init <projectname>`

Будут аналогичны

![alt text](image.png)

Минимум ручной работы.

# Переменные и иммутабельность

По умолчанию в Расте переменные иммутабельны и чтобы сказать что переменная изменяется, нужно это указать явно

```Rust
fn main() {
    let mut x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
}
```

### Константы.

```Rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```

Внимание на нейминг.

Отличие иммутабельных переменных от контсант - константы определяются во врея компиляции и им не могут быть присвоены переменные (строго литералы или статические выражения), а переменные в результате выполнения.

### Shadowing (как я называю "затенение")

Посмотрим на любопытный код:

```Rust
fn main() {
    let x = 5;

    let x = x + 1;

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}");
    }

    println!("The value of x is: {x}");
}
```

Выведет:
```Shell
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.31s
     Running `target/debug/variables`
The value of x in the inner scope is: 12
The value of x is: 6
```

Так можно

```Rust
    let spaces = "   ";
    let spaces = spaces.len();
```

А так нельзя:

```Rust
    let mut spaces = "   ";
    spaces = spaces.len();
```

```Shell
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
error[E0308]: mismatched types
 --> src/main.rs:3:14
  |
2 |     let mut spaces = "   ";
  |                      ----- expected due to this value
3 |     spaces = spaces.len();
  |              ^^^^^^^^^^^^ expected `&str`, found `usize`

For more information about this error, try `rustc --explain E0308`.
error: could not compile `variables` (bin "variables") due to 1 previous error
```

# Типы данных

Питоньи фокусы не прокатят

Такое не скомпилируется:

```Rust
let guess = "42".parse().expect("Not a number!");
```

```Shell
$ cargo build
   Compiling no_type_annotations v0.1.0 (file:///projects/no_type_annotations)
error[E0284]: type annotations needed
 --> src/main.rs:2:9
  |
2 |     let guess = "42".parse().expect("Not a number!");
  |         ^^^^^        ----- type must be known at this point
  |
  = note: cannot satisfy `<_ as FromStr>::Err == _`
help: consider giving `guess` an explicit type
  |
2 |     let guess: /* Type */ = "42".parse().expect("Not a number!");
  |              ++++++++++++

For more information about this error, try `rustc --explain E0284`.
error: could not compile `no_type_annotations` (bin "no_type_annotations") due to 1 previous error
```

Rust статически типизированный, ему надо понимать, что мы хотим записать в guess.

```Rust
let guess: u32 = "42".parse().expect("Not a number!");
```

*Кстати expect - это что то вроде исключений, что меня тоже зацепило лаконичностью или как в Go 

```Go
if err != nil {}
```

Но в Rust. То есть при выполнении функции 

`.parse()`

Она ожидает что мы будем делать на случай если что-то пойдёт не так

### Типы:

![alt text](image-13.png)

Arch - архитектура (x32 или x64 итд, хм, а может даже и x128)

Кстати, насчёт выхода за границы - если мы тестируем в режиме debug (по умолчанию при cargo run) то при выходе за границы диапазона - вылезет ошибка.

Если в режиме "--release", то он просто циклично посчитает с конца в начало (что-то вроде 127 + 2 = -126) 

Как это ловить в релизной версии сказано тут

https://doc.rust-lang.org/book/ch03-02-data-types.html#integer-overflow

![alt text](image-12.png)

#### Float

Так же числа с плавающей точкой

f32, f64.

в соответствии с IEEE-754 standard.

Операции:

```Rust
fn main() {
    // addition
    let sum = 5 + 10;

    // subtraction
    let difference = 95.5 - 4.3;

    // multiplication
    let product = 4 * 30;

    // division
    let quotient = 56.7 / 32.2;
    let truncated = -5 / 3; // Results in -1

    // remainder
    let remainder = 43 % 5;
}
```

#### char

```Rust
fn main() {
    let c = 'z';
    let z: char = 'ℤ'; // with explicit type annotation
    let heart_eyed_cat = '😻';
}
```

По умолчанию char 4 байта.

Подробнее про строки:

https://doc.rust-lang.org/book/ch08-02-strings.html#storing-utf-8-encoded-text-with-strings

#### Tuple

```Rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The value of y is: {y}");
}
```

#### Array (не путать с векторами!)

>NOTE!

Размер Array определяется на этапе компиляции. И задать размер как переменную невозможно! Для этого созданы вектора, когда размер нам заранее неизвестен.!

```Rust
fn main() {
    let months = ["January", "February", "March", "April", "May", "June", "July",
              "August", "September", "October", "November", "December"];
    let first = a[0];
    let second = a[1];
}
```

```Rust
fn main() {
    let a: [i32; 5] = [1, 2, 3, 4, 5];
}
```

```Rust
fn main() {
    let a: [i32; 5] = [1, 2, 3, 4, 5];
}
```

Проинициализирует пять троек:

```Rust
fn main() {
    let a = [3; 5];
}
```

Выход за пределы массива в таком коде выдадут ошибку даже в режиме --release

```Rust
use std::io;

fn main() {
    let a: [i8; 5] = [1, 2, 3, 4, 5];

    println!("Please enter an array index.");

    let mut index = String::new();

    io::stdin()
        .read_line(&mut index)
        .expect("Failed to read line");

    let index: usize = index
        .trim()
        .parse()
        .expect("Index entered was not a number");

    let element = a[index] + 127;

    println!("The value of the element at index {index} is: {element}");
}
```

![alt text](image-14.png)

# Функции

```Rust
fn main() {
    another_function(5);
}

fn another_function(x: i32) {
    println!("The value of x is: {x}");
}
```
Прошу обратить внимание
snake_case.

## Statements and Expressions

внутри statement находится expression (выражение)
То есть выражение внутри. А statement как обёртка над выражением.

В то же время мы не может присвоить statement statement'у.

Не скомпилируется:

```Rust
fn main() {
    let x = let y = 6;
}
```

![alt text](image-16.png)

А такое скомпилируется, поскольку statement let y = ... закрылся выражением;, а не другим statement.

```Rust
fn main() {
    let y = {
        let x = 3;
        x + 1
    };

    println!("The value of y is: {y}");
}
```

## Return values

Скомпилируется, мы опускаем return:

Кстати внимание на сигнатуру возвращаемого значения.

```Rust
fn five() -> i32 {
    5
}

fn main() {
    let x = five();

    println!("The value of x is: {x}");
}
```

Прелесть!

А теперь внимание! Квиз!

Какой из этих двух скомпилируется, а какой нет?

![alt text](image-17.png)

Number One

```Rust
fn main() {
    let x = plus_one(5);

    println!("The value of x is: {x}");
}

fn plus_one(x: i32) -> i32 {
    x + 1
}
```

Number Two

```Rust
fn main() {
    let x = plus_one(5);

    println!("The value of x is: {x}");
}

fn plus_one(x: i32) -> i32 {
    x + 1;
}
```

```Shell
$ cargo run
   Compiling functions v0.1.0 (file:///projects/functions)
error[E0308]: mismatched types
 --> src/main.rs:7:24
  |
7 | fn plus_one(x: i32) -> i32 {
  |    --------            ^^^ expected `i32`, found `()`
  |    |
  |    implicitly returns `()` as its body has no tail or `return` expression
8 |     x + 1;
  |          - help: remove this semicolon to return this value

For more information about this error, try `rustc --explain E0308`.
error: could not compile `functions` (bin "functions") due to 1 previous error
```

# Control flow if statements

Отвыкаем от излишней свободы в Си

Не скомпилируется. Поскольку ожидает ЯВНО bool.

```Rust
fn main() {
    let number = 3;

    if number {
        println!("number was three");
    }
}
```

```Shell
$ cargo run
   Compiling branches v0.1.0 (file:///projects/branches)
error[E0308]: mismatched types
 --> src/main.rs:4:8
  |
4 |     if number {
  |        ^^^^^^ expected `bool`, found integer

For more information about this error, try `rustc --explain E0308`.
error: could not compile `branches` (bin "branches") due to 1 previous error
```

```Rust
fn main() {
    let number = 3;

    if number {
        println!("number was three");
    }
}
```

*Не обращайте внимания на 

`0 != number`

*Это не рекомендации так писать в Rust, а лично мои. Мозгу проще воспринимать сначала литерал а потом то, с чем идёт сравнение, чем держать в памяти сначала абстрактный number а потом сравнивать с нулём. Это действует доли секунды, да, но немного помогает. 

```Rust
fn main() {
    let number = 3;

    if 0 != number {
        println!("number was three");
    }
}
```

#### else if

```Rust
fn main() {
    let number = 6;

    if number % 4 == 0 {
        println!("number is divisible by 4");
    } else if number % 3 == 0 {
        println!("number is divisible by 3");
    } else if number % 2 == 0 {
        println!("number is divisible by 2");
    } else {
        println!("number is not divisible by 4, 3, or 2");
    }
}
```

#### Вместо тернарного оператора

```Rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}");
}
```

Не скомпилируется

```Rust
fn main() {
    let condition = true;

    let number = if condition { 5 } else { "six" };

    println!("The value of number is: {number}");
}
```

```Shell
$ cargo run
   Compiling branches v0.1.0 (file:///projects/branches)
error[E0308]: `if` and `else` have incompatible types
 --> src/main.rs:4:44
  |
4 |     let number = if condition { 5 } else { "six" };
  |                                 -          ^^^^^ expected integer, found `&str`
  |                                 |
  |                                 expected because of this

For more information about this error, try `rustc --explain E0308`.
error: could not compile `branches` (bin "branches") due to 1 previous error
```

# Циклы

Тут уже ничего особенного, поэтому долго не задержимся

```Rust
fn main() {
    loop {
        println!("again!");
    }
}
```

*Мне больше по душе конечно цикл у Go - любой цикл можно через оператор for реализовать.

Тут видимо всё же хотят разграничить 

>loop - без условий, 

>while - с одним условием

>for - перебирает коллекции либо с тремя классическими

Можно и такие фокусы. break тут как return работает.

```Rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```

## Labels (для break)

```Rust
#![allow(unreachable_code, unused_labels)]

fn main() {
    'outer: loop {
        println!("Entered the outer loop");

        'inner: loop {
            println!("Entered the inner loop");

            // This would break only the inner loop
            //break;

            // This breaks the outer loop
            break 'outer;
        }

        println!("This point will never be reached");
    }

    println!("Exited the outer loop");
}
```

## while

```Rust
fn main() {
    // A counter variable
    let mut n = 1;

    // Loop while `n` is less than 101
    while n < 101 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }

        // Increment counter
        n += 1;
    }
}
```

## for

```Rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
}
```

>rev() - значит reverse

```Rust
fn main() {
    for number in (1..4).rev() {
        println!("{number}!");
    }
    println!("LIFTOFF!!!");
}
```

если хотим итерироваться через кастомное значение, то используем 

`.step_by(2)`

```Rust
fn main() {
    for number in (1..4).rev().step_by(2) {
        println!("{number}!");
    }
    println!("LIFTOFF!!!");
}
```

```Rust
fn main() {
    // `n` will take the values: 1, 2, ..., 100 in each iteration
    for n in 1..=100 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }
    }
}
```

>Немного забежали вперёд, тут из нового вектор из стрингов, итератор, синтаксический сахар: match, который убирает нагромождения из if else операторов.

```Rust
fn main() {
    let names = vec!["Bob", "Frank", "Ferris"];

    for name in names.iter() {
        match name {
            &"Ferris" => println!("There is a rustacean among us!"),
            // TODO ^ Try deleting the & and matching just "Ferris"
            _ => println!("Hello {}", name),
        }
    }
    
    println!("names: {:?}", names);
}
```

# Работа с памятью ownership и borrowing

>Вот мы и добрались до самого интересного, как Rust'у удалось решить проблему memory leaks (утечки памяти), dangling pointers (висячие указатели) без использования garbage collector (сборщик мусора), что позволяет быть равным по производительности C/C++, а где то даже и быстрее. Этот раздел я бы назвал важнейшим, ведь он и рассказывает о главных особенностях Rust...

Если в кратце - две концепции которые автоматизируют выделение/освобождение памяти как в C/C++ и не требуют для этого сборщик мусора в рантайме, который замедляет работу.

Если подробнее:

Правила владения

Сначала давайте рассмотрим правила владения:

    - У каждого значения в Rust есть владелец
    - В каждый момент времени может быть только один владелец
    - Когда владелец выходит из области действия, значение будет сброшено

Область действия (всё тоже самое что и в других ЯП):

Пример со строковым литералом, строго закодированном на этапе компиляции

```Rust
{                       // s is not valid here, it’s not yet declared
    let s = "hello";    // s is valid from this point forward
                        // do stuff with s but not mutating
}                       // this scope is now over, and s is no longer valid

```

Выделение string в куче. Если хотим менять

Память автоматически возвращается, как только переменная, которой она принадлежит, выходит из области видимости.

```Rust
{
    let s = String::from("hello");
    s.push_str(", world!"); // push_str() appends a literal to a String
    println!("{s}"); // This will print `hello, world!`
}
```

Когда она выходит из области видимости Rust вызывает деструктор drop автоматически.

https://doc.rust-lang.org/std/ops/trait.Drop.html#tymethod.drop

В C++ этот шаблон освобождения ресурсов в конце жизненного цикла элемента иногда называется Resource Acquisition Is Initialization (RAII)

![alt text](image-18.png)

![alt text](image-19.png)

>Важно! Чтобы не было двойного освобождения, Rust сделает s1 недействительной! Это сделано, чтобы уйти от проблемы двойного освобождения. 

Не скомпилируется:

```Rust
fn main() {
    let s1 = String::from("hello");
    let s2 = s1;

    println!("{s1}, world!");
}
```

```Shell
$ cargo run
   Compiling ownership v0.1.0 (file:///projects/ownership)
error[E0382]: borrow of moved value: `s1`
 --> src/main.rs:5:15
  |
2 |     let s1 = String::from("hello");
  |         -- move occurs because `s1` has type `String`, which does not implement the `Copy` trait
3 |     let s2 = s1;
  |              -- value moved here
4 |
5 |     println!("{s1}, world!");
  |               ^^^^ value borrowed here after move
  |
  = note: this error originates in the macro `$crate::format_args_nl` which comes from the expansion of the macro `println` (in Nightly builds, run with -Z macro-backtrace for more info)
help: consider cloning the value if the performance cost is acceptable
  |
3 |     let s2 = s1.clone();
  |                ++++++++

For more information about this error, try `rustc --explain E0382`.
error: could not compile `ownership` (bin "ownership") due to 1 previous error
```

> Другой пример тоже сработает. 
> Здесь область памяти выделенная под "hello" освободится после того 
> как на неё перестанет что-либо ссылаться. drop() вызовется сразу (immediately).

```Rust
fn main() { 
    let mut s = String::from("hello");
    s = String::from("ahoy");
    println!("{s}, world!");
}
```

![alt text](image-20.png)

>Глубокое копирование.

```Rust
fn main() { 
    let s1 = String::from("hello");
    let s2 = s1.clone();
    println!("s1 = {s1}, s2 = {s2}");
}
```

>Здесь данные копируются на стеке. И не происходит ссылка. При изменении y не поменяется x.

```Rust
fn main() { 
    let x = 5;
    let y = x;

    println!("x = {x}, y = {y}");
}
```

Причина в том, что такие типы, как целые числа, имеющие известный размер во время компиляции, 
хранятся полностью в стеке, поэтому копии фактических значений создаются быстро. 
Это означает, что нет причин, по которым мы хотели бы предотвратить 
x 
недействительность после создания переменной y. 
Другими словами, здесь нет разницы между глубоким и поверхностным копированием, 
поэтому вызов cloneне будет делать ничего, отличного от обычного поверхностного копирования, 
и мы можем его пропустить.

## Ownership (владение)

Пример того как передаётся право собственности и как это работает с простейшими литералами.

```Rust
fn main() {
    let s = String::from("hello");  // s comes into scope

    takes_ownership(s);             // s's value moves into the function...
                                    // ... and so is no longer valid here

    let x = 5;                      // x comes into scope

    makes_copy(x);                  // because i32 implements the Copy trait,
                                    // x does NOT move into the function,
    println!("{}", x);              // so it's okay to use x afterward

} // Here, x goes out of scope, then s. But because s's value was moved, nothing
  // special happens.

fn takes_ownership(some_string: String) { // some_string comes into scope
    println!("{some_string}");
} // Here, some_string goes out of scope and `drop` is called. The backing
  // memory is freed.

fn makes_copy(some_integer: i32) { // some_integer comes into scope
    println!("{some_integer}");
} // Here, some_integer goes out of scope. Nothing special happens.
```

>Пример передачи владения и взятия обратно

```Rust
fn main() {
    let s1 = gives_ownership();         // gives_ownership moves its return
                                        // value into s1

    let s2 = String::from("hello");     // s2 comes into scope

    let s3 = takes_and_gives_back(s2);  // s2 is moved into
                                        // takes_and_gives_back, which also
                                        // moves its return value into s3
} // Here, s3 goes out of scope and is dropped. s2 was moved, so nothing
  // happens. s1 goes out of scope and is dropped.

fn gives_ownership() -> String {             // gives_ownership will move its
                                             // return value into the function
                                             // that calls it

    let some_string = String::from("yours"); // some_string comes into scope

    some_string                              // some_string is returned and
                                             // moves out to the calling
                                             // function
}

// This function takes a String and returns one
fn takes_and_gives_back(a_string: String) -> String { // a_string comes into
                                                      // scope

    a_string  // a_string is returned and moves out to the calling function
}
```

>Пример возвращений (и передачи владения обратно) кортежом

```Rust
fn main() {
    let s1 = String::from("hello");

    let (s2, len) = calculate_length(s1);

    println!("The length of '{s2}' is {len}.");
}

fn calculate_length(s: String) -> (String, usize) {
    let length = s.len(); // len() returns the length of a String

    (s, length)
}
```


>Пример с циклом когда данные удаляются. Демонстрация работы ownership.

```Rust
fn main() {
    let names = vec!["Bob", "Frank", "Ferris"];

    for name in names.into_iter() {
        match name {
            "Ferris" => println!("There is a rustacean among us!"),
            _ => println!("Hello {}", name),
        }
    }
    
    println!("names: {:?}", names);
    // FIXME ^ Comment out this line
}
```

## Borrowing (заимствование)

А теперь borrowing. Основная концепция взятия в аренду на примере картины "Моны Лизы", 
Давайте лучше называть это заимствованием.  

Только при мутабельном заимствовании  (&mut T) возникает ситуация, где владелец теряет доступ к ресурсу, как если бы картину действительно украли.

    В Rust есть строгие правила заимствования:
        Вы можете иметь либо несколько неизменяемых ссылок, либо одну мутабельную ссылку.
         
    В контексте аналогии: музей может позволить многим людям одновременно смотреть на картину (неизменяемые ссылки), но если кто-то хочет её изменить (мутабельное заимствование), все остальные должны подождать.
     
Представьте, что музей владеет картиной Моны Лизы: 

    Неизменяемое заимствование (&T):  
        Несколько людей могут одновременно смотреть на картину в музее.
        Это безопасно, потому что никто не может её изменить.
         

    Мутабельное заимствование (&mut T):  
        Один человек забирает картину для реставрации.
        Пока он её держит, никто другой не может взаимодействовать с оригиналом (ни смотреть, ни реставрировать).
         

    Возвращение картины:  
        Как только реставратор возвращает картину музею, владелец снова может ею распорядиться.
         

    Клонирование (clone):  
        Если кто-то делает копию картины, это уже не оригинал. Теперь у нас есть два независимых объекта: оригинал в музее и копия у другого человека.

Тобишь гарантии. Это предотвращает проблему Race Condition в многопоточности.

Но давайте рассмотрим примеры в однопоточном режиме для понимания.


```Rust
fn main() {
    let mona_lisa = String::from("Retired Mona Lisa"); // Музей владеет картиной

    {
        let borrowed1 = &mona_lisa; // Неизменяемое заимствование: несколько человек могут смотреть
        let borrowed2 = &mona_lisa; // Неизменяемое заимствование: несколько человек могут смотреть
        println!("Looking at: {}{}", borrowed1, borrowed2);
    } // Заимствование завершено, владелец снова может использовать ресурс

    {
        let restorer = &mut mona_lisa; // Мутабельное заимствование: реставратор берёт картину
        *restorer = String::from("Restored Mona Lisa"); // Реставрация
    } // После реставрации реставратор автоматически перестаёт владеть картиной.

    println!("Final version: {}", mona_lisa); // Владелец снова может использовать ресурс
}
```

>(я специально оставил код с ошибкой, чтобы была возможность интерактивно показать работу с компиляцией)
        


Не скомпилируется

```Rust
fn main() {
    let mut s = String::from("hello");

    let r1 = &s; // no problem
    let r2 = &s; // no problem
    let r3 = &mut s; // BIG PROBLEM

    println!("{}, {}, and {}", r1, r2, r3);
}
```

```Shell
$ cargo run
   Compiling ownership v0.1.0 (file:///projects/ownership)
error[E0502]: cannot borrow `s` as mutable because it is also borrowed as immutable
 --> src/main.rs:6:14
  |
4 |     let r1 = &s; // no problem
  |              -- immutable borrow occurs here
5 |     let r2 = &s; // no problem
6 |     let r3 = &mut s; // BIG PROBLEM
  |              ^^^^^^ mutable borrow occurs here
7 |
8 |     println!("{}, {}, and {}", r1, r2, r3);
  |                                -- immutable borrow later used here

For more information about this error, try `rustc --explain E0502`.
error: could not compile `ownership` (bin "ownership") due to 1 previous error
```


```Rust
fn main() {
    let mut s = String::from("hello");

    let r1 = &s; // no problem
    let r2 = &s; // no problem
    println!("{r1} and {r2}");
    // variables r1 and r2 will not be used after this point

    let r3 = &mut s; // no problem
    println!("{r3}");
}
```

>Rust без висячих указателей

Не скомпилируется

```Rust
fn main() {
    let reference_to_nothing = dangle();
}

fn dangle() -> &String {
    let s = String::from("hello");

    &s
}
```

>Пример когда данные сохраняются, работа ссылки. Работа borrowing

```Rust
fn main() {
    let mut names = vec!["Bob", "Frank", "Ferris"];

    for name in names.iter_mut() {
        *name = match name {
            &mut "Ferris" => "There is a rustacean among us!",
            _ => "Hello",
        }
    }

    println!("names: {:?}", names);
}
```

# Structs

```Rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}
```

>Пример инициализации (можно улучшить своим конструктором, билдером) а так же сокращения.

```Rust
fn main() {
    let user1 = User {
        active: true,
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };
    let user2 = User {
        email: String::from("another@example.com"),
        ..user1
    };
}
```

>Пример билдера

```Rust
fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username: username,
        email: email,
        sign_in_count: 1,
    }
}
```

>Верхнее можно сократить

```Rust
fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username,
        email,
        sign_in_count: 1,
    }
}
```

Когда можно обойтись кортежами

```Rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}
```




<!-- Право собственности на данные Struct

В Userопределении структуры в листинге 5-1 мы использовали Stringтип owned вместо &strтипа string slice. Это преднамеренный выбор, поскольку мы хотим, чтобы каждый экземпляр этой структуры владел всеми своими данными и чтобы эти данные были действительными до тех пор, пока действительна вся структура.

Структуры также могут хранить ссылки на данные, принадлежащие чему-то другому, но для этого требуется использование времени жизни — функции Rust, которую мы обсудим в Главе 10. Время жизни гарантирует, что данные, на которые ссылается структура, будут действительными до тех пор, пока существует структура. Допустим, вы пытаетесь сохранить ссылку в структуре без указания времени жизни, как в следующем примере; это не сработает:

```Rust
struct User {
    active: bool,
    username: &str,
    email: &str,
    sign_in_count: u64,
}

fn main() {
    let user1 = User {
        active: true,
        username: "someusername123",
        email: "someone@example.com",
        sign_in_count: 1,
    };
}
``` -->

>Если хотим просмотреть структуру через принт. Просто введём внешний атрибут. 

```Rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!("rect1 is {rect1:#?}");
}
```

> Использование dbg!()

```Rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let scale = 2;
    let rect1 = Rectangle {
        width: dbg!(30 * scale),
        height: 50,
    };

    dbg!(&rect1);
}
```

## Method

>Мы можем выбрать, чтобы дать методу то же имя, что и одно из полей структуры

```Rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
    fn width(&self) -> bool {
        self.width > 0
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```

![alt text](image-22.png)

# enums

```Rust
enum IpAddrKind {
    V4,
    V6,
}
/*
enum IpAddr {
    V4(String),
    V6(String),
}
enum IpAddr {
    V4(u8, u8, u8, u8),
    V6(String),
}
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}
*/
struct IpAddr {
    kind: IpAddrKind,
    address: String,
}

let home = IpAddr {
    kind: IpAddrKind::V4,
    address: String::from("127.0.0.1"),
};

let loopback = IpAddr {
    kind: IpAddrKind::V6,
    address: String::from("::1"),
};
```

Как в библиотеке организована работа с IpV4, IpV6.

https://doc.rust-lang.org/std/net/enum.IpAddr.html

## Null

![alt text](image-23.png)

## Option

```Rust
enum Option<T> {
    None,
    Some(T),
}
```

<T> - это generic. Пока углубляться не буду

>Не скомпилируется:

```Rust
fn main() {
    let x: i8 = 5;
    let y: Option<i8> = Some(5);

    let sum = x + y;
}
```

need impl

```Shell
$ cargo run
   Compiling enums v0.1.0 (file:///projects/enums)
error[E0277]: cannot add `Option<i8>` to `i8`
 --> src/main.rs:5:17
  |
5 |     let sum = x + y;
  |                 ^ no implementation for `i8 + Option<i8>`
  |
  = help: the trait `Add<Option<i8>>` is not implemented for `i8`
  = help: the following other types implement trait `Add<Rhs>`:
            `&'a i8` implements `Add<i8>`
            `&i8` implements `Add<&i8>`
            `i8` implements `Add<&i8>`
            `i8` implements `Add`

For more information about this error, try `rustc --explain E0277`.
error: could not compile `enums` (bin "enums") due to 1 previous error
```

Подробнее об Option:

https://doc.rust-lang.org/std/option/enum.Option.html

Подробнее как их складывать в следующем разделе:

# match null и использование Option Result

>Spoiler к предыдущему:

```Rust
fn main() {
    let x: Option<i8> = Some(5);
    let y: Option<i8> = Some(5);

    let sum = match (x, y) {
        (Some(a), Some(b)) => Some(a + b), // Если оба значения есть, складываем их
        _ => None,                       // В остальных случаях возвращаем None
    };

    println!("{:?}", sum); // Выводит: Some(10)

    /*    
    let x: Option<i8> = Some(5);
    let y: Option<i8> = Some(5);

    if let (Some(a), Some(b)) = (x, y) {
        println!("Sum: {}", a + b); // Выводит: Sum: 10
    } else {
        println!("One of the values is None");
    }
    */
    // unwrap() !Важно!:  Если хотя бы одно из значений будет None, программа вызовет panic!.
    /*
    let x: Option<i8> = Some(5);
    let y: Option<i8> = Some(5);

    let sum = x.unwrap() + y.unwrap(); // Просто извлекаем значения

    println!("Sum: {}", sum); // Выводит: Sum: 10
    */
    // или ещё можно .unwrap_or(<туть значение по умолчанию по типу, если внезапно null>):
}
```

## match

```Rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => {
            println!("Lucky penny!");
            1
        },
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```

>из предыдущего раздела:

```Rust
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        None => None,
        Some(i) => Some(i + 1),
    }
}

let five = Some(5);
let six = plus_one(five);
let none = plus_one(None);
```

>Не скомпилируется

```Rust
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        Some(i) => Some(i + 1),
        /*
        other => move_player(other),
        _ => (),
        */
    }
}
```

```Shell
$ cargo run
   Compiling enums v0.1.0 (file:///projects/enums)
error[E0004]: non-exhaustive patterns: `None` not covered
   --> src/main.rs:3:15
    |
3   |         match x {
    |               ^ pattern `None` not covered
    |
note: `Option<i32>` defined here
   --> file:///home/.rustup/toolchains/1.82/lib/rustlib/src/rust/library/core/src/option.rs:571:1
    |
571 | pub enum Option<T> {
    | ^^^^^^^^^^^^^^^^^^
...
575 |     None,
    |     ---- not covered
    = note: the matched value is of type `Option<i32>`
help: ensure that all possible cases are being handled by adding a match arm with a wildcard pattern or an explicit pattern as shown
    |
4   ~             Some(i) => Some(i + 1),
5   ~             None => todo!(),
    |

For more information about this error, try `rustc --explain E0004`.
error: could not compile `enums` (bin "enums") due to 1 previous error
```

## if let

>Следующие два идентичны

```Rust
let config_max = Some(3u8);
match config_max {
    Some(max) => println!("The maximum is configured to be {max}"),
    _ => (),
}
```

```Rust
let config_max = Some(3u8);
if let Some(max) = config_max {
    println!("The maximum is configured to be {max}");
}
```

> по желанию после if let можно добавить else



## Slice (срезы)

Так же как и в питоне, в Rust есть срезы. Долго не задержимся, просто покажу общий синтаксис.

```Rust
fn main() {
    let s = String::from("hello world");

    let hello = &s[0..5];
    let world = &s[6..11];

    let len = s.len();

    // equal
    let slice = &s[3..len];
    let slice = &s[3..];

    // also equal
    let slice = &s[0..len];
    let slice = &s[..];

}
```

![alt text](image-21.png)

```Rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let slice = &a[1..3];

    assert_eq!(slice, &[2, 3]);
}
```



![alt text](image-5.png)

# Cargo

my_project/
├── Cargo.toml
├── src/
│   ├── main.rs
│   ├── lib.rs
│   ├── utils/
│   │   ├── file_io.rs
│   │   └── network.rs
│   └── geometry/
│       └── shapes.rs
└── tests/
    └── integration_test.rs

    Cargo.toml — файл конфигурации пакета.
    src/main.rs — точка входа для исполняемого файла.
    src/lib.rs — определение библиотечного crate.
     
         Crate  — это минимальная единица компиляции в Rust.
    Каждый пакет содержит хотя бы один crate.
    Существует два типа crates:
        Binary crate:  Создает исполняемый файл (обычно с main.rs).
        Library crate:  Создает библиотеку (обычно с lib.rs).
         
     
```toml
[package]
name = "my_project"
version = "0.1.0"
edition = "2021"

# Binary crate
[[bin]]
name = "my_binary"
path = "src/bin/my_binary.rs"

# Library crate
[lib]
name = "my_library"
```

my_project/
├── Cargo.toml
├── src/
│   ├── main.rs
│   └── math.rs

math.rs
```Rust
pub fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

main.rs
```Rust
mod math; // Подключаем модуль из math.rs

fn main() {
    let result = math::add(2, 3);
    println!("Result: {}", result);
}
```

my_project/
├── Cargo.toml
├── src/
│   ├── main.rs
│   ├── math.rs
│   └── geometry/
│       └── shapes.rs


geometry/shapes.rs:
```Rust
pub fn area_of_square(side: i32) -> i32 {
    side * side
}
```

math.rs:
```Rust
pub mod geometry; // Подключаем подмодуль geometry

pub fn calculate_area(side: i32) -> i32 {
    geometry::shapes::area_of_square(side)
}
```

main.rs:
```Rust
mod math;

fn main() {
    let area = math::calculate_area(5);
    println!("Area: {}", area);
}
```

Разделение на библиотеки и исполняемые файлы:  

    src/lib.rs для основной логики.
    src/main.rs для точки входа.
    src/bin/ для дополнительных исполняемых файлов.
     


### Экосистема crates.io

Внешние библиотеки от пользователей

### Сборка проекта из исходников на C и C++ если в кратце:

![alt text](image-2.png)

### Сборка проекта из исходников на Rust:

![alt text](image-1.png)

`cargo install --path "project_to_build" --locked`

Затем добавление в path через командную строку.

![alt text](image-11.png)


4. Интерактивные элементы:  

    Live-демонстрации :
        Напишите простой код на Rust и покажите его компиляцию и выполнение.
        Демонстрация работы cargo (например, создание проекта, добавление зависимости).
         

# Unsafe rust.

> Rust стремится быть безопасным и производительным языком. Его система типов и модель владения обеспечивают надежные гарантии безопасности; однако эта модель может быть слишком ограничительной (для эффективности, доступа к оборудованию, наследования и т. д.). Чтобы преодолеть это, Rust предоставляет механизм для выполнения небезопасных операций (Unsafe Rust), которые обходят гарантии компилятора.

(Это выжимка из статьи об инвестициях Амазон)

Зачем нужен unsafe Rust?

    Доступ к низкоуровневым деталям: 
        В Rust многие аспекты безопасности памяти обеспечиваются компилятором через систему владения (ownership) и заимствования (borrowing). Однако иногда нужно обойти эти ограничения для работы с низкоуровневыми деталями системы.
        Пример: работа с указателями на уровне железа или использование внешних библиотек, написанных на C/C++.
         

    Интерфейс с внешним кодом (FFI): 
        Для взаимодействия с кодом на других языках (например, C/C++) часто требуется использовать unsafe-операции, так как такие библиотеки могут не соответствовать правилам безопасности Rust.
        Пример: вызов функций из libc или других системных библиотек.
         

    Выполнение операций, которые невозможно выразить безопасно : 
        Некоторые операции, такие как создание циклических ссылок или работа с raw-указателями, невозможно безопасно выразить в Rust без использования unsafe.
         

    Оптимизация производительности : 
        В некоторых случаях использование unsafe-кода может дать возможность оптимизировать производительность, отказавшись от проверок безопасности, которые выполняет компилятор.
         
     

Какие задачи решает unsafe Rust?  
1. Работа с raw-указателями  

    В Rust есть два типа raw-указателей: *const T и *mut T. Они позволяют работать с памятью напрямую, минуя систему владения и заимствования.
    
    Пример:

```Rust
let mut num = 5;
let r1 = &num as *const i32; // Создание immutable raw-указателя
let r2 = &mut num as *mut i32; // Создание mutable raw-указателя

unsafe {
    println!("r1 is: {}", *r1); // Чтение значения через raw-указатель
    *r2 = 10; // Изменение значения через raw-указатель
}
```

2. Вызов extern-функций  

    Для вызова функций из внешних библиотек (например, libc) используется ключевое слово extern.
    
    Пример:

```Rust
extern "C" {
    fn abs(input: i32) -> i32;
}

fn main() {
    unsafe {
        println!("Absolute value of -3 is: {}", abs(-3));
    }
}
```

# Продукты на rust

Godot Engine:  

    Если вас интересует использование Rust для игровых проектов, обратите внимание на Godot Engine, который имеет официальную поддержку Rust через GDExtension API.
    Это более простой и прямолинейный путь для разработки игр на Rust.

Solana

npm
     

# Rust в DevOps

# Type assertion

# Конфликт разработки драйверов на rust

<!-- # Примеры реальных проблем, которые решает Rust : 

    Race conditions.
    Memory leaks.
    dangling pointers.
    buffer overflows. -->

# Комьюнити, документация, экосистема : 

    Активное сообщество.
    Регулярные релизы (каждые 6 недель).
    Хорошая документация и учебные материалы.

О чём можно рассказать потом:

![alt text](image-24.png)

![alt text](image-25.png)

![alt text](image-26.png)

![alt text](image-27.png)

![alt text](image-28.png)

    Многопоточность и распараллеливание.

    async/await

    traits 
    
    Будущее Rust 

        Планы по улучшению языка (например, async closures, const generics).
        Расширение использования в разных областях (IoT, WebAssembly, AI).

# Ищу всех кто готов изучать Rust вместе!

https://t.me/s21_rust - я создал неофициальный канал школы по Rust. Разбил по тредам

> Читаем Rust Book, делимся материалами и вакансиями, решаем leetcode, делаем пет-проекты, организовываем групповые проекты для портфолио, мотивируем и формируем сообщество Rustaceans в Школе 21!

## Полезные ссылки

https://www.youtube.com/watch?v=5C_HPTJg5ek - Rust за 100 секунд с анимациями.

https://doc.rust-lang.org/book/ - Rust book

https://doc.rust-lang.org/cargo/ - Cargo book

https://t.me/rust_code - Новостной канал про новенькое и с полезными утилитами на Rust'е

https://t.me/rust_chats - чат новостного канала

https://t.me/rustlang_ru - основной русскоязычный чат, 5000 участников

https://t.me/rust_beginners_ru - чат для начинающих

https://t.me/rust_offtopic - оффтоп

https://t.me/ruRust_msk - митапы, встречи

https://t.me/books_englishhh - книги