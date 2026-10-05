
## Flag Analysis: `mul1.asm`
### 1. Exit Logic Point (`xor ebx, ebx`)
- **State at `_start+24`:** `eax = 0x1` (sys_exit), `ebx = 0x0`, `edx = 0x0`
- **EFLAGS:** `0x246` `[ PF ZF IF ]`
**ZF** (Zero Flag) | The bitwise XOR operation (`xor ebx, ebx`) evaluated to exactly `0`
**PF** (Parity Flag) | The low 8 bits of the result (`0x00`) contain an even number (zero) of set `1` 
**IF** (Interrupt Flag)| Hardware interrupts remain enabled by default


## Flag Analysis: `mul2.asm`
### 1. Multiplication Operation Point (`mul`)
- **State at `_start+13`:** `eax = 0x27c0` (10176), `edx = 0x9` (9)
- **Combined 64-bit Result (`edx:eax`):** `0x9000027c0` (38,653,536,192)
- **EFLAGS:** `0xa03` `[ CF IF OF ]`
**CF** (Carry Flag)| The upper half of the multiplication result (`edx = 0x9`) is non-zero. For an unsigned `mul` instruction in x86, `CF` is set to `1` whenever the product does not fit within the destination register (`eax`) alone and spills into the high-order register (`edx`)
**OF** (Overflow Flag) | In x86 multiplication, `OF` mirrors `CF`. Because significant upper bits overflowed into `edx` (`edx != 0`), `OF` is set to `1`
**IF** (Interrupt Flag) | System hardware interrupts are enabled by default
### 2. Exit Logic Point (`xor ebx, ebx`)
- **State at `_start+33`:** `eax = 0x1` (sys_exit), `ebx = 0x0`
- **EFLAGS:** `0x246` `[ PF ZF IF ]`
**ZF** (Zero Flag) |The bitwise XOR operation (`ebx ^ ebx`) cleared the register to exactly `0`
**PF** (Parity Flag) |The low 8 bits of `ebx` (`0x00`) contain zero `1` bits, which counts as even parity.
**IF** (Interrupt Flag) | Hardware interrupts remain enabled by default