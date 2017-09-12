---
layout: post
title:  "Raspberry Pi 3 - Static IP"
date:   2016-06-22 19:21:00 +0300
categories: raspberrypi network
---
Привет!

Столкнулся с проблемой - не могу по гайдам из интернета на своей малине настроить статический айпишник (правка файла **/etc/network/interfaces**). Оказывается в **Raspbian Jessie** всем рулит **dhcpcd.service** и статический нужно задавать **ТАМ**!

Для начала необходимо остановить сервис:

    sudo systemctl stop dhcpcd

Добавить в конфиг вышеупомянутого сервиса такие строки (**/etc/dhcpcd.conf**):

    interface eth0

    static ip_address=192.168.1.2/24
    static routers=192.168.1.1
    static domain_name_servers=192.168.1.1

В файле **/etc/network/interfaces** наш интерфейс должен иметь вид:

    iface eth0 inet manual

И только после этого можно включать сервис и наслаждаться жизнью!
