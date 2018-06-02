# Hello-World
"Distributed lighting system project"

Dear Github Community,
I'm Salva, I'm post doctoral researcher in economics and management, I'm curretly focusing on distributed computer programs, in particular virtual teams that cooperate via remote access in order to develop a software (for instance), in a distribuited value chain. My study goal consists to create a small distributed lighting systems based on "3 raspberry PI 3 model B +", each one, connected to a led unit via dmx512 (2 dmx interface for raspberry).

I thought: 1 board works as master device and the 2 boards as slave devices. The 2 boards have to work in syncro with the master and they have to do what the master order them ( show, simultaneously, the same light effect of the master).

I'm not an engineer so it's quite hard for me this little project, by the way I'm studying and applying.

At the moment I have bought:

two DMX interface for Raspberry pi with usb (FT245RL)

two raspeberry Pi 3 model B +

My first problem is the communication between raspberry board --> DMX interface through GPIO --> led unit. I need to use the DMX interface for Raspberry Pi 3 model B+ without USB (FT245RL) and directly from GPIO, but checking on the web, I didn't find a low level driver (or a library) for dmx control directly from GPIO.

For that reasons I contacted the DMX interface producer (bitwizard) and he suggested me to:

<< To do DMX from the raspberry pi, you have to do a few things.

Send a break for about 100 microseconds.
Wait a small while (12microseconds IIRC)
send the DMX data. at 250000 bps and Repeat this say every 40ms...
You can program that yourself, or use standard software.
The OLA software has a driver for my hardware. Inside OLA this driver is called "uartdmx".
If you want to write your own driver, this is a nice example.

When you clone the git directory, in plugins/uartdmx/UartWidget.cpp
you find:

For example,
bool UartWidget::SetBreak(bool on) {
there you find the code to turn the BREAK on or off.
The routine below that is the example for writing the data.
and two routines down you find the example code to initialize the
port. When you are using OLA as the example code, note that it has a
mainloop (which I didn't see in the "Widget" file, it is probably in
the "Thread" file)

This mainloop does what I just said:
break
wait
write data
sleep

But it has a bug: The sleep starts when the write call returns and not
when the write finishes. So the sleep counts from the start-of-data, and
not from "end-of-data". The name of the config file entry and the name
of the variables hint that it starts at end-of-data (But that was a mistake
from that author) >>.

I understood (from DMX board producer) that I need a driver (in c or c++ compiled) or a library, after that I have to create a small program in C or in C++ that uses that driver or library. Obviously I can't use complete softwares as OLA or QLC+ because the project goal is different. I never programmed, I'm just able to copy and paste, or modify some paramaters of a programmed code.

Basing on your experience what could I do? Is it hard job? Could you help me or suggest me how proceed?

Thanks in advance for your patience!

Best Regards
Salva
