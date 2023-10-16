Title: Управление Arduino и MG995 с помощью Rust
Summary: MG995 - 360градусный сервопривод
Date: 2023-10-21 16:00
Tags: programming, robot, rust, arduino
Url: arduino-with-rust-mg995
Slug: arduino-with-rust-mg995

Привет!

Для управления **MG995** написал [**свой пакет**](https://github.com/dkurchigin/mg995_servo), т.к. каких-либо примеров работы с этим сервоприводом в интернете очень мало.
Ориентировался на библиотеку **Servo** в **Arduino**, т.к. она написана очень приятно - создаешь класс и вызываешь несколько методов для работы.

Сейчас данная библиотека использует порт **D9** и **Timer1**. 
При создании объекта можно установить свой ***duty***, если необходимо подкорректировать настройки сервопривода.

Для моих сервоприводов для вращения по часовой стрелке, остановки, вращения против часовой стрелки использую следующие ***duty*** при инициализации:
```
    pub const LEFT_DUTY: u8 = 12;
    pub const STOP_DUTY: u8 = 22;
    pub const RIGHT_DUTY: u8 = 32;
```
К примеру, если двигатель не останавливается с ***STOP_DUTY = 22***, можно подкорректировать. К примеру, установить 21/23 и тд.

###Пример использования
```
    #![no_std]
    #![no_main]
    
    extern crate arduino_hal;
    extern crate mg995_servo;
    
    use panic_halt as _;
    use arduino_hal::hal::simple_pwm;
    use arduino_hal::simple_pwm::{Timer1Pwm, IntoPwmPin};
    use mg995_servo::{MG995, LEFT_DUTY, STOP_DUTY, RIGHT_DUTY};
    
    #[arduino_hal::entry]
    fn main() -> ! {
        let dp = arduino_hal::Peripherals::take().unwrap();
        let pins = arduino_hal::pins!(dp);
        let timer1 = Timer1Pwm::new(dp.TC1, simple_pwm::Prescaler::Prescale1024);
        let servo_pin = pins.d9.into_output().into_pwm(&timer1);
    
        let mut mg995 = MG995::new(servo_pin, STOP_DUTY, LEFT_DUTY, RIGHT_DUTY);
        mg995.enable();
        loop {
            mg995.stop();
            arduino_hal::delay_ms(500);
            mg995.right();
            arduino_hal::delay_ms(500);
            mg995.stop();
            arduino_hal::delay_ms(500);
            mg995.left();
            arduino_hal::delay_ms(500);
        }
    }
```