Title: Программирование Arduino с помощью Rust
Summary: Шьём Arduino через Rust
Date: 2023-10-15 16:00
Tags: programming, robot, rust, arduino
Url: arduino-with-rust
Slug: arduino-with-rust

Привет!

Дошли руки и появилось настроение написать статью как я стал прошивать **Arduino Nano** через **Rust**.

###Как всё это выглядит
- прошиваю через **USB**, запоминаю название этого **COM**-порта
- для прошивки использую [**этот пакет**](https://github.com/Rahix/avr-hal/tree/main)
- **PROFIT!**

<br/>

###А теперь по порядку
Подключаю плату к компьютеру, затем надо установить все необходимые зависимости для [**avr-hal**](https://github.com/Rahix/avr-hal/tree/main#quickstart), ну и сам **Rust**, разумеется.
Следуя инструкции к пакету выполняю все шаги и делаю:
```
    cargo build
```
Если не установлена нужная настройка фичи (***в виде  вашей платы***), то пакет это сообщит и спросит наш выбор. 
У меня настройка выглядит так: 
```
    features = ["arduino-nano"]
``` 
После написания программы необходимо ее залить с помощью команды:
```
    cargo run
```
Настройки прошивалки можно посмотреть в файле ***.cargo/config.toml*** У меня он выглядит так:
```
    [build]
    target = "avr-specs/avr-atmega328p.json"
    
    [target.'cfg(target_arch = "avr")']
    runner = "ravedude nano -cb 57600 -P COM5"
    
    [unstable]
    build-std = ["core"]
```
Дополнительные настройки платы формируются пакетом автоматически. Посмотреть можно по этому пути ***avr-specs/avr-atmega328p.json***
```
    {
      "arch": "avr",
      "atomic-cas": false,
      "cpu": "atmega328p",
      "data-layout": "e-P1-p:16:8-i8:8-i16:8-i32:8-i64:8-f32:8-f64:8-n8-a:8",
      "eh-frame-header": false,
      "exe-suffix": ".elf",
      "executables": true,
      "late-link-args": {
        "gcc": [
          "-lgcc"
        ]
      },
      "linker": "avr-gcc",
      "llvm-target": "avr-unknown-unknown",
      "max-atomic-width": 8,
      "no-default-libraries": false,
      "pre-link-args": {
        "gcc": [
          "-mmcu=atmega328p"
        ]
      },
      "target-c-int-width": "16",
      "target-pointer-width": "16"
    }
```