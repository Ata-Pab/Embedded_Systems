### **TIMER PWM INTERRUPT**
Is it possible to mix modes within one timer but on different channels? For example;  TIM1_CH1 – PWM, TIM1_CH2 – PWM, TIM1_CH3 - CNT
Yes, but they will share the counter and reload register. (Reload Register:  ARR)
Each timer has only one counter, which is shared by its 4 channels. It can either count some clock events (APB clock, which usually equals the system clock), or one external trigger input. To generate a PWM signal, the counter must supply the PWM frequency.

![Timer_Counter](https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/Timer_Counter.png)