---
title: MMC Stuff
description: Notes on Microprocessors and Microcontrollers
---

# MMC Stuff

## Unit 3

##### Page Translation

- In the second phase of address transformation, the Pentium transforms a linear address into a physical address.
- It is needed for page-oriented virtual-memory systems and page-level protection.
- The page-translation step is optional.

##### Paging


- When operating in protected mode, the Intel Architecture permits the linear address space to be mapped directly into a large physical memory
(for example, 4 GBytes of RAM) or indirectly (using paging) into a smaller physical memory and disk storage.
- This method of mapping the linear address space is commonly referred to as virtual memory or demand-paged virtual memory.
- When paging is used, the processor divides the linear address space into fixed-size pages (generally 4 KB in length) that can be mapped into
physical memory and/or disk storage.
- Paging is different from segmentation through its use of fixed-size pages.
- If segmentation is the only form of address translation used, a data structure present in physical memory will have all of its parts in memory.
- If paging is used, a data structure can be partly in memory and partly in disk storage.
- To minimize the number of bus cycles required for address translation, the most recently accessed page-directory and page-table entries are
cached in the processor in devices called translation lookaside buffers (TLBs).

##### Paging Options
Paging is controlled by three flags in the processor’s control registers:

1. PG (paging) flag, bit 31 of CR0: Enables the page-translation mechanism. The operating system or executive usually sets this flag during processor initialization.
2. PSE (page size extensions) flag, bit 4 of CR4: Enables large page sizes. 4-MByte pages or 2-MByte pages. When the PSE flag is clear, the more common page length of 4 KBytes is used.
3. PAE (physical address extension) flag, bit 5 of CR4: Enables 36-bit physical addresses.

Components of the paging mechanism

1. Page directory - Array of 32bit PDEs in a 4KB page. Points to a page table
2. Page table - Array of 32bit PTEs in a 4KB page. Points to page frame
3. Page - A 4KB, 2MB, or 4MB flat address space
4. Page directory-pointer table - An array of 4 64bit entries each of which points to a page directory. This DS is only when PAE is enabled

PDE/PTE - Page Directory Entry/Page Table Entry

- One Page Directory can address a million pages
- Since each page has 4K bytes, the tables of one page directory can span the entire physical address space
- The physical address of the current page directory is stored in the CPU register CR3, also called the page directory base register (PDBR)
- MM software has the option of using one page directory for all tasks, one page directory for each task, or some combination of the two.

To select various table entries, the linear address is divided into 3 sections

- PDE - Bits 22-31 provide an offset to an entry in the page directory. Provides the base physical address of a page table.
- PTE - Bits 12-21 provide an offten to an entry in the selected page table. Provides the base physical address of a page in physical memory.
- Page offset - Bits 0-11 provide an offset to a physical address in the page

PDBR

- The physical address of the current page directory is stored in CR3 (also called PDBR)
- CR2 is the page fault linear address register, which holds the 32 bit linear address which caused the last page fault.
- If paging is to be used, PDBR must be loaded as part of the processor initialization process (prior to enabling paging)
- The PDBR can then be changed either explicity by loading a new value in CR3 with a MOV instruction or implicitly as part of a task switch.

CR2 is used for handling page faults when PG is set
Since the page directory table is always 4KB aligned, the lowest 12 bytes of CR3 are ignored


#### Page level protection

The paging mechanism has 2 levels of protection

- User - level 3 of segementation based protection
- Supervisor - Encompasses all of the other levels (0, 1, 2)

Programs executing at 0/1/2 bypass page protection, segmentation based protection is still enforced by the hardware

The U/S and R/W bits are used to provide protection for individual pages or for all pages

|U/S|R/W|Permitted Level 3|Permitted Levels 0,1,2|
|---|---|---|---|
|0|0|None|R/W|
|0|1|None|R/W|
|1|0| R/O|R/W|
|1|1| R/W|R/W|


#### Translation Lookaside Buffer

- Pentium keeps a cache of the most recently accessed pages, this cache is called TLB
- To minimize the number of bus cycles required for address translation, the most recently accessed page-directory and page-table entries are cached in the processor in devices called TLBs.
- It is a four-way associative 32-entry page table cache
- Most paging is performed using the contents of the TLBs
- They are inaccessible to application programs and tasks (privilege level > 0), i.e. they cannot invalidate TLBs. Only the OS or executive procedures running as a privilege level of 0 can invalidate TLBs or selected TLB entries.
- The INVLGP instruction is used to invalidate a specific page-table entry in the TLB.

##### TLB Hit
- The paging unit hardware receives a 32bit linear address from the segmentation unit
- The upper 20 linear address bits are compared with all 32 entries in the TLB to check for a match
- If there is a match, i.e. a TLB hit, then the 32bit physical address is calculated and placed on the address bus.

##### TLB Miss

- If P=1 on the PDE indicating that the page table is in memory, then Pentium will read the appropriate PTE.

The operating system is responsible for setting up the initial page tables, and handling any page faults.
The OS is also required to invalidate/flush the TLB when changes are made to PTEs.
It is done by loading CR3 with the address of the page directory, and allocating space for the page directory and the page tables.


##### Multitasking

- This involves the sharing of one system by many users
- Time sharing is used - each user is alloted a time slice (a small fraction of a second)
- Computer will attend one user at a time every slice
- This will go on as a cycle

Timesharing

- Allows multiple users to use the same computer
- Provides economical use of processing resources
- Is invisible to the users
- Can work for any number of users

To main timesharing

- Computer must store the current state of the program and restart the next user's program as it was previously left when its time slice expired.
- Saving the current state is called context, changing to the next program is called context switch.

Context switch is necessary to perform timesharing. It

- saves the state of the current program,
- loads another program from its saved state,
- allow any program to be restarted at any time.

##### Task

It is the basic unit of multitasking

- A program or a group of programs can be defined by OS as a task
- For multiuser system, a task can be assigned to each user
- It is a unit of work that a processor that dispatch, execute, and suspend
- When operating in protected mode, all processor execution takes places from within a task
- A task is invoked by an interrupt, exception, jump, or call.
- Even simple systems must define atleast one task.


##### Task structure

- A task is made up of two parts - Task execution space, and a task state segment
- TES consists of a code, stack, and one or more data segments
- TSS stores the segments that make up TES and provides a storage spaces for task state information.
- In multitasking systems, the TSS also provides a mechanism for linking tasks.
- A task is identified by the segment selector for its TSS.
- When a task is loaded into CPU for execution, segment selector, base address, limit, and segment description attributes for the TSS are loaded into the task register.
- If paging is implemented for a task, base address of page directory used by the task is loaded into control register CR3.

##### Task State

The task's current execution space, defined by segment selectors in the segment registers
CS, DS, SS, ES, FS, GS

##### Executing a task

- An explicit call to a task with CALL instruction
- An explicit call to a task with JMP instruction
- An implicit call to an interrupt-handler task  (by the CPU)
- An implicit call to an exception-handler task
- A return (initiated with IRET) when NT flag in EFLAGS is set

When task is dispatched for execution, task switch automatically occurs between the currently running task and the dispatched task.
During the switch, execution environment of the currently executing task (state/context) is saved in TSS, and it is suspended.
The context for the dispatched task is then loaded into the CPU, and execution of that task begins with the instruction pointed to by the newly loaded EIP register.
If currently executing called dispatched, TSS of calling is stored in TSS of called to provide a link for callback

##### Task Management DS

1. Task State Segment - TSS
2. Task State Segment Descriptor
3. Task Register
4. Task Gate Descriptor
5. NT flag in EFLAGS register

In protected mode, TSS and TSS descriptor must be created for atleast one task, and the segment selector for the TSS must be loaded into the task register, using LTR instruction

TSS stores all the information the CPU needs in order to manage a task
TSS is identified by a special register in the Task State Segment Register (TR)
This register contains a selector referring to the descriptor that defines the current TSS

It is a dynamic set updated by the CPU with each switch from the task. It includes

- General registers - EAX, ECX, EDX, EBX, ESP, EBP, ESI, EDi
- Saved in same order as PUSHAD saves
- Segment registers - ES, CS, SS, DS, FS, GS
- Flag register - EFLAGS
- Instruction pointer - EIP

Previous task link field - back link field
Contains segment selector for TSS of previous task, so it can switch back on IRET

There is a static set the CPU reads but does not change

- Selector of the task's LDT
- CR3 (PDBR) - base address of page directory - read only when paging is enabled
- Pointers to the stacks for privilege levels 0-2
- T bit (debug trap bit) which causes the processor to raise a debug exception when a task switch occuirs

I/O map base address

- 16bit offset from the base of the TSS to the I/O permission bit map and interrupt redirection bitmap
- When present, these maps are stored in the TSS at higher addresses
- Points to the beginning of I/O permission bitmap and end of interrupt redirection bitmap


- TSS like all segments is defined by a descriptor which holds the base address of TSS assigned to that task
- TSSD may only be plced in GDT, not LDT or IDT
- An attempt to identify a TSS with a selector that has TI=1 (current LDT), results in an exception


## Unit 4

Microprocessors - less components, less specific, more generalized, more expensive, cannot function standalone.
Microcontrollers - More components, very specific, can function standalone, cheaper

##### Features of 8051

- 40 pin 8 bit CPU optimized for control applications
- Extensive boolean (single bit logic) processing capabilities
- 64K program memory address space
- 64K data memory address space
- 4K on-chip program memory
- 128 bytes on-chip data RAM
    - 4 register banks of 8 registers each
    - 16 bytes, bit addressable
    - 8 bytes general purpose data memory
- 32 bidirectional, individually addressable I/O lines
- 2 16 bit timer/counters
- Full duplex serial UART communication (SBUF)
- 6 source / 5 vector interrupt structure with two priority levels
- On-chip clock oscillator
- 8 bit data bus, 16 bit address bus
- 4 8bit I/O ports (P0-P3, 32 pins)
- Registers A(accumulator) and B
- 16 bit PC and DPTR (program counter and data pointer)
- 8 bit PSW and SP (program status word and stack pointer)
- Control registers - TCON, TMOD, SCON, PCON, IP, IE
- 2 external and 3 internal interrupt sources
- Oscillator and clock circuits

Pins

- RST - Pin 9 - Reset
Input pin, active high (usually low)
On applying high, it will reset and all values will be lost
- /EA - Pin 31 - External access
Connected to ground to indicate that code is stored externally
For 8051, /EA pin is connected to VCC
/ means active low
- I/O port pins - P0, P1, P2, and P3
Each port uses 8 bidirectional pins

Ports

- 4 8bit, bit addressable ports
- Upon reset, all are configured as input
- Ports can be accessed in whole or in part
- Instructions used are SETB, CLR, CPL
- They are identified as P1.0-P1.7
(When 0 is written - output, when 1 is written - input)

- Port 0 - 80H
    - A normal bidirectional I/O port, or
    - Can be used for address / data interfacting for accessing external memory
- Port 1 - 90H
    - Dedicated solely for I/O interfacing
- Port 2 - A0H
    - Higher external address byte, or
    - A normal input/output port
- Port 3 - B0H
    - Each pin can be individually programmed for I/O operation or for alternate function


|Port Pin|Alternate Function|
|---|---|
|P3.0|RXD|
|P3.1|TXD|
|P3.2|INT0|
|P3.3|INT1|
|P3.4|T0|
|P3.5|T1|
|P3.6|WR|
|P3.7|RD|

Register set

- A - accumulator
    - One of the most used SFRs, as it is involved in many instructions
    - Used for all data transfers between 8051 and external memory
- B - F0H
    - Very similar to accumulator
    - Only used by 2 8051 instructions - MUL and DIV


- PSW (flag register)
- Stack and stack pointer
- Data pointer
- Program counter
- Special function registers

PSW format

- CY  - Carry
- AC  - Auxillary carry
- F0  - Available to the user for a general purpose
- RS1 - Register bank selector 1
- RS0 - Register bank selector 0
- OV  - Overflow
- _   - User defineable bit
- P   - Parity

|RS1|RS0|Register Bank|Address|
|---|---|---|---|
|0|0|0|00H - 07H|
|0|1|1|08H - 0FH|
|1|0|2|10H - 17H|
|1|1|3|18H - 1FH|

Register used to access the stack is SP - stack pointer

The stack pointer in 8051 is oonly 8 bits wide - 00 - FF limits
When it is powered up, SP contains the value 07

PC and DPTR

- They are both 16 bit registers
- Each is to hold the address of a byte in the memory
- PC contains the address of the next instruction to be executed
- DPTR is made up of 2 8 bit registers, i.e. DPH and DPL
- It contains the address of internal and external code, and the data that has to be accessed.


Internal RAM - 00H to 7FH
SFRs - 80H to FFH

The collection of general purpose registers (R0-R7) are register banks, which accept one byte of data
8051 has 4, which are selected by PSW
They are present in the internal RAM and are used to process the data when the microcontroller is programmed

The SFRs act as a control table to monitor and control the operation of 8051
Out of 128 locations (80H to FFH), only 21 are actually assigned to SFRs
Each has one byte address and a unique name specifying their purpose.


##### Addressing modes

- Register addressing: Uses registers to hold the data
MOV A, R0
MOV R2, A
- Direct byte addressing: The entire 128 bytes of RAM can be accessed
MOV R0, 40H
MOV 56H, A
- Register indirect addressing: A register is used as a pointer to the data
MOV A, @R0
MOV @R1, B
- Immediate addressing: Immediate data must be prepended with #
MOV A, #25H
MOV R4, #62
- Register specific addressing
- Index addressing: Widely used in accessing data elements of look up table entries
MOVC A, @A+DPTR

The 8051 has another 64K Bytes of memory set aside for data storage, referred to as external memory, which can be accessed only by the MOX instruction


##### Instruction Set

- The 8051 has 255 instructions - every 8bit op code from 00 to FF
- The instruction are grouped into 5 groups
    1. Arithmetic
        - ADD
        - ADDC
        - SUB
        - INC
        - DEC
        - MUL
        - DIV - Stores result in accumulator, remainder in B
    2. Logic
    3. Data transfer
        - MOV
        - MOVC
        - MOVX
        - PUSH
        - POP
        - XCH - Exchange data bytes, uses register A
        - XCHD
    4. Boolean
        - CLR - Clear accumulator, or bit
        - SETB - Operate on direct addressable bits
        - CPL - Complement accumulator
    5. Branching
        - JBC - Jump if bit=1 and clear bit
        - JNB - Jump is bit = 0
        - JB - Jump is bit = 1
        - JNC - Jump if CY = 0
        - JC - Jump if CY = 1
        - CJNE - Jump if a!=b
        - DJNZ - Decrement and jump if A != 0
        - JNZ - Jump if A != 0
        - JZ - Jump if A = 0
        - SJMP - Short jump - 2 byte instruction. opcode and relative address of target.
        - LJMP - Long jump - 3 byte instruction. opcode, relative address.


##### Interrupts
An interrupt is an external or internal event that interrupts the microcontroller to inform it that a device needs its service
A single microcontroller can serve several devices by two ways:
- Interrupt
    1. Whenever a device wants service from microcontroller, it interrupts the microcontroller.
    2. Device gets attention of microcontroller based on the Priority assigned to it.
    3. A microcontroller can ignore a device request for service.
    4. Microcontroller can perform other tasks till an interrupt occurs.

- Polling       
    1. Microcontroller continuously monitors the status of the device to check whether it needs service.
    2. Priority is not assigned. It checks all the devices in round robin fashion.
    3. Device request for service cannot be ignored.
    4. Polling wastes much of the microcontroller’s time by polling devices that do not need service.


- Device notifies a microcontroller that it needs service by sending an interrupt signal.
- The microcontroller interrupts whatever it is doing when it receives the signal and services the device.
- The program associated with the interrupt is called the interrupt service routine - ISR or the interrupt handler.
- On receiving an interrupt signal, microcontroller finishes the currently executing instruction, and saves the address of the next instruction on the stack.
- It saves the current status of all interrupts internally.
- It jumps to a fixed location in memory IVT.
- It gets the address of ISR from IVT and jumps to it and executes ISR.
- When it reads RETI instruction, it returns to the place where it was interrupted.

8051 has 6 interrupts allocated
1. Reset - power-up reset (0000)
2. 2 interrupts for timers (timer 0 and timer 1)
3. 2 interrupts for hardware external interrupts (P3.2, P3.3) for INT0(EX1) and INT1(EX2)
4. Serial communication has a single interrupt that belongs to both receive and transfer

IVT - Interrupt Vector Table

| Vector | Address | Interrupt Number |   Description   |
|--------|---------|------------------|-----------------|
|  IE0   |  0003H  |         0        |   External 0    |
|  TF0   |  000BH  |         1        | Timer/counter 0 |
|  IE1   |  0013H  |         2        |   External 1    |
|  TF1   |  001BH  |         3        | Timer/counter 1 |
| Serial |  0023H  |         4        |   Serial port   |


We can configure the 8051 so that any of these events will cause an interrupt
- Timer 0/1 overflow
- Reception/transmission of a serial character
- External event 0/1

The appropriate interrupt handler routines will be called

Interrupt related registers

- TCON - Edge and type bits for external interrupt 0/1
- SCON - RI and TI interrupt flags for RS232
- IE - Enable interrupt sources (address A8h)
- IP - Specify priority of interrupts (address B8h)

##### Special function registers

Interrupt Control:

- IE - Interrupt enable
- IP - Interrupt priority
Timers:
- TMOD - Timer mode
- TCON - Timer control
- TH0 - Timer 0 high byte
- TL0 - Timer 0 low byte
- TH1 - Timer 1 high byte
- TL1 - Timer 1 low byte


8051 - 2 timers/counters - t/c0 and t/c1

- The timer is used as a time delay generator - clock source is the internal crystal frequency
- It can also be used as an event counter - external input from input pin to count the number of events on registers. These clock pulses could represent the number of people passing through an entrance, or the number of rotations of a wheel, or any other event that could be converted into pulses.

Both timer0 and timer1 are 16 bits wide
Each can be accessed as 2 seprate registers of low and high byte

TMOD is an 8 bit register - lower 4 bits for 0, upper for 1. Sets the usage mode. Not bit addressable

TMOD has:

- GATE - Gating control when set. 0 = internal control, 1 = external
- C/T - 0 for timer 1 for counter
- M1 - Mode bit 1
- M0 - Mode bit 2

|M1|M0|Mode|Operating Mode|
|---|---|---|---|
|0|0|0|13 bit timer|
|0|1|1|16 bit timer|
|1|0|2|8 bit auto reload|
|1|1|3|Split timer mode|


Serial port programming features

- Single data line
- Covers long distance
- Cheaper
- Modern
- Synchronus and asynchronus
- Simplex, half and full duplex transmission
- Start, stop bit - framing
- Data transfer rate - bps, baud rate

8051 connection to RS232

- A line driver such as MAX232 is required to convert RS232 voltage levels to TTL levels, and vice verse
- 8051 has 2 pins that are used specifically for serial data transfer (TxD and RxD)

Serial communication programming
To allow data transfer between a PC and 8051 without errors:

- Baud rate of 8051 must match PC's
- We can program this with the help of timer1
- 8051 divides the crystal frequency by 12 to get machine cycle frequency
- 8051's serial communication UART circuit divides the machine cycle frequency by 32 once more before it used by timer1 to set the baud rate.

SBUF register

- It is an 8 bit register solely for serial communication
- It is used to send and receive data via the on-board serial port
- These are 2 physical register - one only for reading, one only for writing
- Transmission starts when the SBUF is written with data
- For byte data to be transferred via TxD, it must be placed in SBUF
- SBUF holds a data bytewhen RxD receives it

SCON register

- It is an 8 bit register to program the start, stop bits and the data bits of data framing

- SM0, SM1 - Determine the framing of data by specifying the number of bits per character
- SM2 - Enables the multiprocessing capability of the 8051
- REN - Receive enable, when high 8051 is allowed to receive data on RxD
- TI - Transmit interrupt - When 8051 finishes the transfer of an 8 bit character, it raises TI flag to indicate that it is ready to transfer another byte. It is raised at the beginning of the stop bit.
- RI - Receive interrupt - When 8051 receives serial data via RxD, gets rid of start and stop bits and places the byte in SBUF, raises RI flag to indicate that byte has to be picked up.

PCON register

- 8 bit, bit addressable, can be used to change baud rate
- When 8051 is powered on, SMOD is 0
- Set it to high via software to double the baud rate