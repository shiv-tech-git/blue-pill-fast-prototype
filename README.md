# Library for fast prototyping on BluePill STM32C8T6

## One action - one line!

## UART1
No need to init. UART starts automatically  on 9600 baud when you send massage in first time. Just type something in old good printf style.
```c
print_msg("%d. My massage: %s", number, massage);	
```

If you 9600 is not fast enough you can init uart manualy.
```c
init_UART1(UART_SPEED_9600);
init_UART1(UART_SPEED_19200);
init_UART1(UART_SPEED_38400);
init_UART1(UART_SPEED_57600);
init_UART1(UART_SPEED_115200);
```
Receiving message from PC. You need to put message which will appear in PC terminal. It is inviting message. It tells you in which moment controller is waiting for the response. Second argument is a buffer in which recived message will be stored. The third one is the buffer size.
```c
receive_msg(transmitting_message, buffer, buffer_size);	
```


## PIN INITIALIZATION
Just as datasheet says but using one function.
```c
init_pin(GPIOX, pin, MODE, CNF);
```
MODE:
* INPUT
* OUTPUT_2Mhz
* OUTPUT_10Mhz
* OUTPUT_50Mhz

CNF if input:
* ANALOG
* FLOATING
* PULL_UP
* PULL_DOWN

CNF if output:
* PUSH_PULL
* OPEN_DRAIN
* ALTERNATE_PUSH_PULL
* ALTERNATE_OPEN_DRAIN


## DELAY
Delay is using timer 2.
```c
delay_us(microseconds);
delay_ms(milliseconds);
```


## LED
PC13 Led
```c
led_turn_on();
led_turn_off();
led_toggle();
```


## SYSTEM TIMER
It is millisecond timer on timer 3. Just type needed period in header file. 20 ms for example.
```c
#define SYSTEM_TIMER_MULTIPLIER 20
```
Now you only need to start timer.
```c
start_system_timer();
```
You could also get the number of system ticks, stop it or set the counter to zero.
```c
get_sys_tick(void);
set_sys_tick_to_zero(void);
stop_system_timer(void);
```


## ADC
No need to init. For single conversion just type one line.
```c
ADC_single_conversion(channel);
```
According to the BluePill schematic:
0 ADC0 - PA0 
1 ADC1 - P1
2 ADC2 - PA2
3 ADC0 - PA3
4 ADC4 - PA4
5 ADC5 - PA5
6 ADC6 - PA6
7 ADC0 - PA7
8 ADC8 - PB0
9 ADC9 - PB1


## PWM
Using timer 4. First you need to explicitly initialize timer. Frequency is up to 720 kHz, duty cycle is up to 100%.
```c
init_timer4_pwm(chanel, frequency, duty_cycle);
```
Timer 4 channel 1 - PB6
Timer 4 channel 2 - PB7
Timer 4 channel 3 - PB8
Timer 4 channel 4 - PB9

Than just set duty cycle.
```c
pwm_set_duty_cycle(channel, duty_cycle);
```
