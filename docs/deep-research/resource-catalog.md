## Classic PDF Manuals

This section catalogs foundational, authoritative guides to Commodore 64 assembly language from the platform's heyday in the early 1980s. Preserved as PDFs, these manuals offer comprehensive instruction and serve as indispensable references for understanding the C64's architecture at a low level.

### Commodore 64 Programmer's Reference Guide

*   **Author/Publisher**: Commodore Business Machines (1982)
*   **Overview**: Considered the definitive and canonical technical manual for the C64, this guide was published by Commodore itself to give programmers the essential information needed to fully utilize the machine's capabilities [citation: 13] [citation: 16]. It is a comprehensive resource that covers the system's architecture from hardware to software, making it an invaluable tool for both beginners and advanced developers [citation: 11] [citation: 17]. The guide is widely available for download from sites like the Internet Archive [citation: 12] [citation: 14].
*   **Key Topics Covered**:
    *   **System Memory Map**: Detailed layouts of RAM, ROM, and I/O addresses [citation: 11] [citation: 17].
    *   **KERNAL Routines**: A complete reference for the C64's operating system routines, including entry points for screen output, keyboard input, and file operations [citation: 16].
    *   **6502/6510 Instruction Set**: A full reference for every instruction, including opcodes, addressing modes, and cycle counts [citation: 12].
    *   **BASIC Internals**: Information on how the BASIC interpreter works and how to interface machine language with it [citation: 13].
*   **Strategy Example: Using KERNAL Routines**
    The guide teaches the strategy of leveraging built-in KERNAL routines to perform complex tasks without reinventing the wheel. For example, to print a character to the screen, instead of writing a routine to manipulate video memory directly, a programmer can simply call the `CHROUT` routine at address `$FFD2`.
    ```
    ; This example prints the letter 'A' to the screen
    LDA #$41       ; Load the Accumulator with the ASCII code for 'A'
    JSR $FFD2      ; Jump to Subroutine CHROUT (character output)
    RTS            ; Return from Subroutine
    ```

### Assembly Language Programming with the Commodore 64

*   **Author/Publisher**: Marvin L. De Jong / Brady Communications Company (1984)
*   **Overview**: This book is a foundational tutorial designed to teach 6502 assembly language from the ground up, specifically for the C64 [citation: 1]. It provides detailed explanations of core concepts, emphasizing practical techniques for beginners. The content progresses from basic architecture to more complex programming examples [citation: 1].
*   **Key Topics Covered**:
    *   **6502 Architecture**: Explanations of the accumulator, index registers (X and Y), stack pointer, and status flags [citation: 1].
    *   **Addressing Modes**: In-depth coverage of immediate, zero-page, absolute, and indexed addressing [citation: 1].
    *   **Instruction Set**: Practical examples for data transfer, arithmetic, and logical operations.
    *   **Programming Techniques**: Examples involving memory manipulation, stack usage, and interfacing with the operating system [citation: 1].
*   **Strategy Example: Direct Memory Manipulation**
    The book explains the fundamental strategy of directly writing to memory-mapped hardware registers to control the computer's behavior. This example demonstrates how to change the border and screen color by writing values to the VIC-II chip's registers.
    ```
    ; This example sets the border to black and the screen to white
    LDA #$00       ; Load Accumulator with 0 (Black)
    STA $D020      ; Store in border color register
    LDA #$01       ; Load Accumulator with 1 (White)
    STA $D021      ; Store in screen color register
    RTS
    ```

### C64 Macro Assembler Development System Manual

*   **Author/Publisher**: Commodore Business Machines
*   **Overview**: This is the official manual for Commodore's own assembler, providing authoritative instructions on how to write, assemble, and debug machine code on the C64 [citation: 2]. It introduces the crucial strategy of using a macro assembler to streamline development, a key technique for writing more efficient and readable code. The manual covers the assembler's syntax, pseudo-opcodes, and the use of macros [citation: 2].
*   **Key Topics Covered**:
    *   **Assembler Directives**: Instructions for the assembler itself, such as setting the program origin (`* = $C000`) and defining data (`.BYTE`, `.WORD`).
    *   **Labels and Symbols**: The use of labels to create readable, relocatable code.
    *   **Macro Definitions**: How to define reusable blocks of code with replaceable parameters.
    *   **Instruction Set and Addressing**: Reference for the 6510 instruction set and its syntax within the assembler [citation: 2].
*   **Strategy Example: Using Macros**
    A core strategy taught by this manual is the creation of macros to simplify repetitive tasks. A macro allows a programmer to define a template for a sequence of instructions. The example below shows a hypothetical macro to set a sprite's X/Y position.
    ```
    ; Define a macro named SET_SPRITE_POS
    .MACRO SET_SPRITE_POS, SPRITE_NUM, X_POS, Y_POS
      LDA #X_POS
      STA $D000 + (SPRITE_NUM * 2) ; Set Sprite X position
      LDA #Y_POS
      STA $D001 + (SPRITE_NUM * 2) ; Set Sprite Y position
    .ENDM

    ; How the macro would be used in code
    SET_SPRITE_POS 0, 100, 50     ; Set sprite 0 to position (100, 50)
    SET_SPRITE_POS 1, 150, 75     ; Set sprite 1 to position (150, 75)
    ```
## Online Blog and Markdown Series

Modern developers benefit from a wealth of accessible, web-based tutorials that demystify Commodore 64 assembly language. These resources, often presented as blog posts or hosted on platforms like GitHub, leverage modern tools and teaching methods to guide newcomers through the intricacies of 6502 programming. They provide a vital bridge between the classic hardware and contemporary development practices.

### Setting Up a Modern Workflow

A significant hurdle for new C64 developers is establishing an efficient coding environment. Modern tutorials excel at guiding users through this initial setup, recommending a combination of emulators and cross-assemblers that run on today's operating systems.

*   **Toolchain Guidance**: Blog series often begin by instructing the user on how to install the **VICE emulator** for running and testing code, alongside a cross-assembler like **dasm**, **ACME**, or **KickAssembler** [citation: 31] [citation: 37]. This approach allows developers to write code in a familiar text editor on a PC or Mac and quickly assemble and run it on a virtual C64.
*   **Build Automation**: More advanced guides introduce the strategy of using `makefiles` to automate the build process [citation: 36]. This allows a developer to compile assembly source, link objects, and launch the resulting program in the emulator with a single command, streamlining the code-test-debug cycle significantly [citation: 36].

### Foundational "Hello World" Tutorials

The quintessential first step in any programming language is getting "Hello World" to appear on the screen. Online tutorials for C64 assembly break this process down into manageable steps, introducing core concepts along the way.

A popular example is David Roberts's introductory blog post, which provides a complete, commented program to display a message [citation: 31]. This single exercise teaches several fundamental strategies:

1.  **Memory Allocation**: Using the `* = $C000` or `.org $C000` directive to place the program's starting address in a safe area of RAM, avoiding conflicts with BASIC or the KERNAL ROM [citation: 31].
2.  **Using KERNAL Routines**: Leveraging the C64's built-in operating system by calling subroutines. The tutorial demonstrates using `JSR $FFD2` (CHROUT) to print a single character to the screen, a crucial technique for simplifying I/O operations [citation: 31].
3.  **Data Storage and Loops**: Storing the text string in memory using the `.byte` directive and creating a loop to print it character-by-character. This introduces index registers (`X`), comparison instructions (`CMP`), and branching (`BEQ`) [citation: 31].

```assembly
; Code strategy from Dave's Blog tutorial
* = $C000      ; Set program start address to 49152

  ldx #0       ; Initialize X register (our loop counter) to 0
Loop:
  lda Message,x  ; Load a character from Message, offset by X
  beq Done       ; If it's 0 (end of string), branch to Done
  jsr $FFD2      ; Call KERNAL CHROUT to print the character
  inx          ; Increment X to point to the next character
  jmp Loop     ; Jump back to the start of the loop
Done:
  rts          ; Return from subroutine

Message:
  .byte "HELLO WORLD",0 ; The string to print, terminated by 0
```

### Architecture and Addressing Modes

Accessible markdown guides, like the one by Spiro Harvey on GitHub, focus on the prerequisite knowledge needed to write any assembly code [citation: 35]. These guides emphasize that a solid understanding of the 6502's architecture is non-negotiable.

*   **CPU Registers**: They explain the purpose of the Accumulator (A), the Index Registers (X and Y), the Stack Pointer (S), and the Program Counter (PC) [citation: 34].
*   **Addressing Modes**: The guides provide clear definitions and simple examples for key addressing modes, which are fundamental to understanding how instructions access data [citation: 35].
    *   **Immediate**: `LDA #$01` (Load the value 1 directly into the Accumulator).
    *   **Absolute**: `STA $D020` (Store the Accumulator's value at memory address $D020).
    *   **Zero-Page**: A faster version of absolute addressing for the first 256 bytes of memory.
*   **The Stack**: Tutorials explain how the stack, a last-in-first-out (LIFO) structure in memory from `$0100` to `$01FF`, is used to temporarily store register values (e.g., with `PHA`) and manage subroutine calls (`JSR`/`RTS`) [citation: 34].

By breaking down these foundational concepts with clear, concise examples, modern online tutorials provide an approachable and effective entry point for anyone looking to begin their journey into Commodore 64 assembly programming.


## Advanced Web Tutorials

Beyond the fundamentals of memory and loops, mastering the Commodore 64 requires a deep understanding of its custom chips, particularly the VIC-II graphics controller. Advanced web tutorials provide the specialized knowledge needed to push the machine's hardware to its limits, enabling effects that define the C64's iconic visual style. These guides focus on precise, cycle-counted timing and direct hardware manipulation.

### Mastering the VIC-II: Raster Interrupts

Raster interrupts are the cornerstone of advanced C64 programming, allowing a developer to trigger code execution at a specific vertical scanline as the electron beam draws the screen [citation: 44]. This timing mechanism is the key to creating stable in-game timers, split-screen displays, and synchronized multimedia effects [citation: 41] [citation: 43]. Web-based guides and wikis offer detailed breakdowns of this technique.

The core strategy involves a precise sequence of hardware register manipulations:
1.  **Disable Interrupts**: The process must begin with a `SEI` (Set Interrupt Disable) instruction to prevent the system from firing an interrupt before the setup is complete.
2.  **Set Interrupt Vector**: The 6510's default IRQ vector at memory locations `$0314` and `$0315` is redirected to point to the starting address of a custom Interrupt Service Routine (ISR) [citation: 46].
3.  **Specify Raster Line**: The desired scanline for the interrupt is written to the VIC-II's raster register at `$D012` [citation: 44].
4.  **Enable Raster Interrupts**: The VIC-II's interrupt control register at `$D01A` is modified to enable raster interrupts [citation: 44].
5.  **Re-enable Interrupts**: A `CLI` (Clear Interrupt Disable) instruction allows the system to respond to interrupts again.

The ISR itself must acknowledge the interrupt by writing to `$D019` before executing its primary task (like changing colors or playing a sound) and then typically jumps to the KERNAL's default handler to maintain system stability [citation: 44].

```assembly
; Strategy for setting up a single raster interrupt
  sei              ; 1. Disable interrupts
  lda #<MyISR       ; 2. Point IRQ vector to our routine
  sta $0314
  lda #>MyISR
  sta $0315
  lda #100         ; 3. Set interrupt to trigger at scanline 100
  sta $D012
  lda #%00000001   ; 4. Enable raster interrupts in the VIC-II
  sta $D01A
  cli              ; 5. Re-enable interrupts

MyISR:
  lda #%00000001   ; Acknowledge the raster interrupt
  sta $D019
  
  inc $d020        ; Do something: change the border color
  
  jmp $ea31        ; Jump to the default KERNAL IRQ handler
```

### Overcoming Hardware Limits: Sprite Multiplexing

While the C64 can only display eight sprites simultaneously by default, developers quickly devised a technique known as **sprite multiplexing** to overcome this limitation. Advanced tutorials, such as the detailed breakdown by Cadaver, explain how to use raster interrupts to rapidly reposition and reuse the eight hardware sprites multiple times down the screen [citation: 21].

The strategy hinges on sorting a list of "virtual" sprites by their Y-coordinate and using precisely timed raster interrupts to update the hardware sprite registers just before they are needed for a new set of sprites on a lower portion of the screen [citation: 21] [citation: 27].

#### Key Multiplexing Strategies

*   **Y-Coordinate Sorting**: The most critical part of a multiplexer is its sorting algorithm. Tutorials discuss the trade-offs between different methods, with the "Ocean" algorithm often cited for its efficiency [citation: 21]. The goal is to create an ordered list of which sprites are visible on which scanlines with minimal CPU overhead per frame.
*   **Zone Splitting**: A simpler form of multiplexing where the screen is divided into horizontal zones. A raster interrupt fires at the start of each zone, reassigning the eight hardware sprites to a new set of virtual sprites within that zone [citation: 21].
*   **Flicker Mitigation**: If more than eight sprites need to appear on the same scanline, a multiplexer must decide which ones to drop. Tutorials discuss strategies like round-robin assignment to distribute the flicker evenly, making it less perceptible to the human eye [citation: 21].

A GitHub repository from user zendar provides a well-commented example of a 32-sprite multiplexer, demonstrating an efficient sorting routine and the necessary VIC-II register updates within an interrupt handler [citation: 27]. These advanced web resources, complete with source code, provide the strategic blueprints for creating graphically rich and dynamic C64 software.## YouTube Video Guides

This analysis compiled a catalog of basic and advanced Commodore 64 assembly language tutorials, drawing from classic 1980s PDF manuals, modern blog series, and advanced web-based hardware guides. The resources provide both the foundational "how" through code examples and the strategic "why" behind core C64 development techniques.

**Key Findings:**
*   Foundational knowledge is preserved in comprehensive PDF manuals from the 1980s, such as the *Commodore 64 Programmer's Reference Guide*, which provides a complete overview of the system memory map, KERNAL routines, and the 6502/6510 instruction set [citation: 11] [citation: 16] [citation: 17].
*   Modern web-based tutorials and blogs offer an accessible entry point for beginners, guiding users through setting up a contemporary development workflow with emulators and cross-assemblers, and teaching core concepts via "Hello World" examples [citation: 31] [citation: 37].
*   Advanced programming strategies for overcoming hardware limitations are detailed in specialized web tutorials, focusing on techniques like using raster interrupts for precise timing effects and sprite multiplexing to display more than the default eight sprites [citation: 21] [citation: 27] [citation: 44].
*   A common strategy across tutorials is leveraging the C64's built-in KERNAL ROM routines, such as calling the `CHROUT` subroutine at address `$FFD2` to simplify screen output operations [citation: 16] [citation: 31].

This catalog addresses the user's request for a curated list of basic and advanced Commodore 64 assembly language tutorials with code examples and strategic explanations.