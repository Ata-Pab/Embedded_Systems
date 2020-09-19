### **VOLATILE KEYWORD**

Volatile Qualifier: An Object has **Memory location**, **hardware Register** or **SFR** which can be updated **Interrupts**, **DMA**, **External Inputs** (as keypad), **Shared Resources**. 
Volatile prevents compiler to perform any **optimization** on that object that can change in ways that compiler can not determine.


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

When Compiler has **Optimization Level0** and if value in 20000004h address is changed by 45, program jumps to *second while loop*.
Optimization Levels change Assambly code size and Compile type of SW.

