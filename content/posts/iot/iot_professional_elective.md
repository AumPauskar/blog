+++
title = 'IOT Professional elective'
date = 2024-03-27T12:26:43+05:30
tags = ["iot", "sem6", "arduino", "raspberry pi"]
author = "Aum Pauskar"
showToc = true
TocOpen = false
draft = false
hidemeta = false
comments = false
description = "Set of notes and documentation regarding iot open elective of semester 6"
disableShare = false
disableHLJS = false
hideSummary = false
searchHidden = true
ShowReadingTime = true
ShowBreadCrumbs = true
ShowPostNavLinks = true
ShowWordCount = true
ShowRssButtonInSectionTermList = true
UseHugoToc = true
[editPost]
    URL = "https://github.com/AumPauskar/blog/content/posts/"
    Text = "Suggest Changes"
    appendFilePath = true
+++

# IOT Professional elective 

- IOT: A dynamic globan network infrastructure with a self-configuring capability based on standard protocols and inter operatble communication protocols where physical and virtual things have identities, physical attributes, and virtual personalities use intelligent interfaces and are seamlessly integrated into the information network often communicate data associated with users and external environment.

- Charecteristics
    - Dynamic and self-configuring
    - Self configuring
    - Interopeable communications protocols
    - Unique identity
    - Integrated info network

- Block diagram of an iot device
    1. Connectivity
        - USB host
        - RJ45/Ethernet
    2. Memory interfaces
        - DDR1/DDR2/DDR3
        - NAND/NOR
    3. Processor
        - CPU
    4. Graphics
        - GPU
    5. A/V intefaces
        - HDMI
        - 3.5mm jack
        - RCA
    6. Storage interfaces
        - SD
        - MMC
        - SDIO
    7. IO interfaces
        - UART
        - SPI
        - I2C
        - CAN

- Link layer (wired)
    1. 802.3 and ethernet (wired)
        - coaxial cable, twisted pair, fiber optic
        - 10mbps - 10gbps

    2. 802.11 wifi (wireless) \
        IEEE 802.11a and IEEE 802.11ac are both standards for wireless network transmissions set by the Institute of Electrical and Electronics Engineers (IEEE).

        Here are some key differences between the two:

        1. **Frequency Band:** 802.11a operates in the 5 GHz frequency band, while 802.11ac operates in both the 5 GHz and 2.4 GHz bands.

        2. **Data Rate:** 802.11a supports a maximum data rate of 54 Mbps, while 802.11ac supports a much higher maximum data rate, up to 1.3 Gbps (Gigabits per second) with three spatial streams.

        3. **MIMO:** 802.11ac supports Multi-User Multiple Input Multiple Output (MU-MIMO), which allows multiple devices to receive multiple data streams at the same time. 802.11a does not support this feature.

        4. **Channel Width:** 802.11ac supports wider channel widths than 802.11a. 802.11ac can use 20, 40, 80, or even 160 MHz channels, while 802.11a is limited to 20 MHz channels.

        5. **Beamforming:** 802.11ac supports beamforming, which allows the router to focus its signal towards certain devices rather than sending it out equally in all directions. This can improve performance and range. 802.11a does not support this feature.

- Protocols
    - 802.3
    - 802.11
    - 802.16
    - 802.15.4
    - Mobile networks(3g/4g/5g etc)

## Application layer protocols
1. HTTP
    - Hyper Text Transfer Protocol
    - Uses TCP
    - request response model
2.  CoAP
    - Constrained Application Protocol
    - Uses UDP
    - request response model
    - M2M communication
    - Meant for constrained devices
3. Web Socket
    - Full duplex communication
    - Uses TCP
    - Real time communication
4. MQTT (Message Queuing Telemetry Transport)
    - Publish subscribe model
    - Uses TCP
    - Meant for IOT devices
5. XMPP (Extensible Messaging and Presence Protocol)
    - Uses XML
    - Real time communication
    - Presence information
    - Decentralized
    - Client server model
6. DDS (Data Distribution Service)
    - Publish subscribe model
    - Uses UDP
    - Real time communication
    - Meant for real time systems
7. AMQP (Advanced Message Queuing Protocol)
    - Publish subscribe model2
    - Uses TCP
    - Meant for enterprise systems

## Communication models
* Request response communication model
    - Client sends a request to the server
    - Server processes the request and sends a response to the client
* Publish subscribe communication model
    - Publisher publishes a message to the broker
    - Broker sends the message to the subscriber
* Push pull communication model
    - Publisher pushes the message to the broker
    - Subscriber pulls the message from the broker
* Exclusive pair communication model
    - Two devices communicate with each other
    - No broker involved
    - Full duplex communication