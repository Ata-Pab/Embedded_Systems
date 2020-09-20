<h4><div  align = "center">  SYSTEM TIMER (SysTick)</div></h4>
<br>
<p>
Executing tasks periodically, in order to support multitasking and improve the CPU utilization. Almost all ARM Cortex MCU’s have the System Timer. If enabled the system timer can periodically generate <strong>SysTick Interrupts</strong>. The Nested Vector Interrupt Controller (<strong>NVIC</strong>) monitors and handles all interrupt requests. 
</p><br>

<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/System_Timer_SysTick/System_Timer_Img1.png" alt="NVIC General Schematic"></img>
</p>
<br>

<div align=center>Microcontroller General NVIC Diagram</div> 

<br>

```c
void SysTick_Handler(void) {
       ……
} 
```
<br>
<br>

<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/System_Timer_SysTick/System_Timer_Img2.png" alt="24-Bit Down Counter System Timer"></img>
</p>
<br>

<div align=center>The System Timer is 24-bit Down Counter.</div>
<br>

<div align=center><strong>SysTick Interrupt Time Period = (SysTick_Load + 1) * Clock_Period</strong></div>

<br>
SysTick_Load is like ARR in Timer Interrupts.
<br>
<br>

<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/System_Timer_SysTick/System_Timer_Img3.png" alt="SysTick_CTRL"></img>
</p>
<br>

SysTick Control Status Register (<strong>SysTick_CTRL</strong>)

<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/System_Timer_SysTick/System_Timer_Img4.png" alt="SysTick Interrupt Schematic"></img>
</p>
<br>

SysTick Reload Value Register (<strong>SysTick_LOAD</strong>)

<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/System_Timer_SysTick/System_Timer_Img5.png" width="671" height="128" alt="SysTick_LOAD"></img>
</p>
<br>

SysTick Current Value Register (<strong>SysTick_VAL</strong>)

<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/System_Timer_SysTick/System_Timer_Img6.png" width="671" height="128" alt="SysTick_VAL"></img>
</p>
<br>

SysTick Calibration Register (<strong>SysTick_CALIB</strong>)

<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/System_Timer_SysTick/System_Timer_Img7.png" width="671" height="160" alt="SysTick_CALIB"></img>
</p>
<br>

<h4>SysTick_LOAD</h4>

Writing <i>RELOAD</i> to 0 disables SysTick, independently of <i>TICKINT</i>.
<i>24 Bits</i>, max value: 0x00FF FFFF. The Interval of two consecutive SysTick interrupts is;
<div align=center><strong>Interval = (RELOAD + 1) * Source_Clock_Period</strong></div>

<h4>SysTick_VAL</h4>

Reading it returns current counter value. When it transits from 1 to 0, it generates an interrupt.
Writing to SysTick_VAL clears Counter and <i>COUNTFLAG</i> to zero but does not trigger SysTick Interrupt. It has random value on Reset. <strong><i>Always clear it before enabling the timer</i></strong>.
<br>
<br>

<h4>SysTick_CALIB</h4>

A <strong>read only</strong> register. 10ms holds the reload value (<strong><i>TENMS</i></strong>). May not be implemented or may be defined differently by chip designers.
<br>

<h5>Example Initialization Code</h5>

```c
void SysTick_Initialize(unsigned_32 ticks) {
    SysTick -> CTRL = 0;    // Disable SysTick
    SysTick -> LOAD = ticks -1;  // Set Reload Register
// Set Interrupt priority of SysTick to least urgency (Largest priority value)
	NVIC_SetPriority(SysTick_IRQn, (1 << __NVIC_PRIO_BITS) - 1);
	SysTick -> VAL = 0  // Clear the SysTick Counter value
// Select processor clock: 1 = Processor Clock,  0 = External Clock
	SysTick -> CTRL |= SysTick_CTRL_CLKSOURCE;
// Enables SysTick Interrupt 1 = Enable,  0 = Disable
	SysTick -> CTRL |= SysTick_CTRL_TICKINT;
	SysTick -> CTRL |= SysTick_CTRL_ENABLE;   // Enable SysTick 
}
```
<br>

<h5>Calculation of Reload Value</h5>

Suppose Clock Source is <i>80 MHz</i>,   SysTick Interval = <i>10 milliseconds</i>.

<strong>Reload = (10 ms / (Clock_Period)) - 1  =  (10 ms * Clock_Frequency) - 1</strong><br>
<i>Reload = 799999</i>
<br>
<br>

<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/System_Timer_SysTick/System_Timer_Img8.png" alt="SysTick Interrupts"></img>
</p>
<br>


