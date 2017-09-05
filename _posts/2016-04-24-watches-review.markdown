---
layout: post
title:  "Настольные часы на Ардуино - Обзор"
date:   2016-04-24 20:02:00 +0300
categories: arduino programming
---
Привет!

Наконец-то дошли руки до завершающего поста по настольным часам на **Ардуино**. Удалось реализовать установку, просмотр и сброс будильника, таймера, текущего времени. Таймер и будильник работают независимо друг от друга. Если в **RTC** села батарейка — на экране появится надпись **RTC**.

Была идея реализовать возможность установки нескольких таймеров и будильников, а также установку будильника на конкретные дни недели, но это было бы ни к чему.

![Часы крупным планом](/images/tumblr_inline_odwa39wXHU1td8cty_500.jpg)

Пример работы представлен на видео:

[![Видеообзор часов на ардуино](https://img.youtube.com/vi/_cTB6HarbBY/0.jpg)](https://www.youtube.com/watch?v=_cTB6HarbBY)

**Компоненты:**

- Китайская [**Arduino Nano**](https://ru.aliexpress.com/item/1PCS-Nano-3-0-controller-compatible-with-nano-CH340-USB-driver-NO-CABLE-for-Arduino-NANO/32473529871.html?dp=b3b7663955133352c3b7f3788a027df2&af=240682&cv=47843&afref=http%253A%252F%252Ft.umblr.com&mall_affr=pr3&aff_platform=aaf&cpt=1504545854821&sk=VnYZvQVf&aff_trace_key=9a1c35f46c6f4fc7bd922dc609b729bb-1504545854821-00944-VnYZvQVf)
- [**LED**](https://www.chipdip.ru/product/cc04-41srwa)
- [**RTC от Амперки**](http://amperka.ru/product/troyka-rtc?utm_source=itashobby&utm_medium=partner&utm_campaign=itashobby)
- 74HC595*2
- Резистор 220 Ом*14
- Резистор10 кОм*4
- Резистор 1кОм*2
- Транзистор*2
- Кнопки*4
- Пищалка
- И немного колодок…
