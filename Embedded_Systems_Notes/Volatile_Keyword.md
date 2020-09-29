<h4><div align="center"><strong>VOLATILE KEYWORD</strong></div></h4>
<br>

Volatile Qualifier: An Object has <strong>Memory location</strong>, <strong>hardware Register</strong> or <strong>SFR</strong> which can be updated <strong>Interrupts</strong>, <strong>DMA</strong>, <strong>External Inputs</strong> (as keypad), <strong>Shared Resources</strong>. 
Volatile prevents compiler to perform any <strong>optimization</strong> on that object that can change in ways that compiler can not determine. It tells the compiler that the value of the variable may change at any time <strong>without any action</strong> being taken by the code the compiler finds nearby. 

https://barrgroup.com/embedded-systems/how-to/c-volatile-keyword#:~:text=C's%20volatile%20keyword%20is%20a,code%20the%20compiler%20finds%20nearby.

```c
#include <stdint.h>

#define SRAM_ADDRESS1 0x20000004U

int main(void)
{
    uint32_t value = 0;
    uint32_t* valuePtr = (uint32_t*) SRAM_ADDRESS1

    while(1)
    {
        value = *valuePtr;
        if(value) break;
    }

    while(1);
    
    return 0;
}
```

When Compiler has <strong>Optimization Level0</strong> and if value in 20000004h address is changed by 45, program jumps to <i>second while loop</i>.
Optimization Levels change Assambly code size and Compile type of SW.

