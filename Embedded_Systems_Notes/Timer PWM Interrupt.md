<h4><div  align = "center">TIMER PWM INTERRUPT</div></h4>

Is it possible to mix modes within one timer but on different channels? For example;  TIM1_CH1 – PWM, TIM1_CH2 – PWM, TIM1_CH3 - CNT

Yes, but they will share the <i><strong>counter</strong></i> and <i><strong>reload register</strong></i>. (Reload Register:  <strong>ARR</strong>)
Each timer has <i>only one counter</i>, which is shared by its 4 channels. It can either count some clock events (<strong>APB</strong> clock, which usually equals the system clock), or one external trigger input. To generate a PWM signal, the counter must supply the <i>PWM frequency</i>.

<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/Timer_PWM_Interrupt/Timer_Counter.png" alt="Timer Counter Schematic"></img>
</p>
<br>
<br>

<div align="center"><strong>f<sub>CK_CNT<sub> = f<sub>CL_PSC</sub> / (PSC + 1)</strong></div></p>

Compare & Capture Register (<strong>CCR</strong>) compares Reload value which is in ARR and products output. (Timer Output: <strong>OCREF</strong>) (This output is like, <i>HIGH</i> or <i>LOW</i> )

<h4>Up-Counting Mode</h4>
<br>
<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/Timer_PWM_Interrupt/Up_Counting_Mode.png" alt="Up Counting Mode"></img>
</p>
<br>

Auto Reload Register holds <i>Maximum Counter value</i>.

<strong>PWM Period</strong>:

<p>
	<div align="center"><strong>Period = (1 + ARR) * Clock_Period</strong></div></p>

<h4>Down-Counting Mode</h4>
<br>
<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/Timer_PWM_Interrupt/Down_Counting_Mode.png" alt="Down Counting Mode"></img>
</p>
<br>

<h4>Center-Aligned Mode</h4>
<br>
<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/Timer_PWM_Interrupt/Center_Aligned_Mode.png" alt="Center Aligned Mode"></img>
</p>
<br>

<p>
	<div align="center"><strong>Period = 2 * ARR * Clock_Period</strong></div></p>
<br>

<h5><i>PWM Mode 1 (Low-True Mode)</i></h5>
<br>
<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/Timer_PWM_Interrupt/PWM_Mode_1.png" alt="PWM Mode 1 (Low-True Mode)"></img>
</p>
<br>

<p>
	<div align="center"><strong>Duty Cycle = CCR / (ARR + 1)</strong></div></p>
<br>

<h5><i>Multi Channel Outputs</i></h5>

Typically a single Timer can generate up to <strong>4</strong> PWM signals with <strong>independent</strong> duty cycles. Each timer has <i>4 channels</i>. Each channel has own Capture & Compare Registers (CCR): <i>CCR1, CCR2, CCR3, CCR4</i>.

<br>
<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/Timer_PWM_Interrupt/Multi_Channel_Outputs.png" alt="Multi Channel Outputs"></img>
</p>
<br>

They have <strong>same Period</strong>. However, their <strong>duty</strong> cycles can be <strong>different</strong>, because CCR values are different.

<h5><i>Multi Channel Outputs</i></h5>

In PWM mode 2 (High-True mode) PWM’s positive and zero sections are swapped.

Duty Cycle = 1 – (CCR / (ARR + 1))    (<i>Up Counting Mode</i>)

Duty Cycle = 1 – (CCR / ARR)    (<i>Center aligned Mode</i>)

<h5><i>Auto Reload Register (ARR)</i></h5>

Auto reload value is also called <strong>Counter Period</strong>.

Auto Reload Preload Enable (<strong>ARPE</strong>) bit in <strong>TIMx_CR1</strong>   (Control Register)

ARR can be updated <strong>synchronously</strong> or <strong>asynchronously</strong>.

When <strong>ARPE</strong> bit is <strong>HIGH</strong>; an update to ARR will be <strong>buffered</strong> in a register, named the <strong>Preload Register</strong>.

<br>
<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/Timer_PWM_Interrupt/ARPE.png" alt="ARPE Schematic"></img>
</p>
<br>

Sync Update mechanism is synchronous to timer’s input clock and timer’s output period. It prevents SW from updating the output frequency or period, when timer is still performing comparison operations.

<h5><i>Repetition Counter Register (RCR)</i></h5>


Update events (<strong>UEV</strong>) are generated with respect to the counter overflows and underflows, if the <strong>Update Disable bit</strong> equals <strong>0</strong> in the timer CR1 Register.   (<strong>UDIS = 0</strong>)

If the UDIS bit is <strong>1</strong>, generation of update events are <strong>disabled</strong>.

In addition Update events are only <strong>generated</strong> when the <strong>Repetition Counter</strong> has reached <strong>0</strong>.

<br>
<p align="center">
    <img src="https://github.com/Ata-Pab/Embedded_Systems/blob/master/Embedded_Systems_Notes/Images/Timer_PWM_Interrupt/Repetition_Counter_Register.png" alt="Repetition Counter Register"></img>
</p>

<div align="center">Overflow and underflow Points</div>

<br>
<h5><i>Extras</i></h5>

What is PWM Resolution?

The PWM resolution is defined as the <strong>maximum</strong> number of <strong>pulses</strong> that you can pack into one PWM <strong>period</strong>.











