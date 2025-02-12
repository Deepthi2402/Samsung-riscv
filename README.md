<html lang="en"><body>
<h1>samsung-riscv</h1>
<h2>Basic Details</h2>
<b>Name:</b> Deepthi S R
<br>
<b>College:</b> Dayananda Sagar College Of Engineering
<br>
<b>Email:</b> <a href="mailto:deepthisr237@gmail.com">deepthisr237@gmail.com</a>
<br>
<b>GitHub Profile:</b> <a href="https://github.com/Deepthi2402">Deepthi2402</a>
<hr>
<!-- Task 1 -->
    <details>
      <p><summary>
      <b>Task 1:</b> Task is to install RISC-V toolchain using VDI link provided,Compiling the C code 
    </summary></p>
    <b>1. Compiling C code</b>
    <br><br>
    <pre><code>
    cd
    gedit summ.c
    gcc summ.c
    ./a.out</code></pre>
    <br>
    <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task%201/cprog_ex1.jpg"  alt=C code>
    <br><br>
    <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task%201/cprog_output.jpg"      alt=commands for c compilation>
    <br><br>
    <b>2. Object Dump and O1, Ofast Output</b>
    <br><br>
    <pre><code>
    cat summ.c
    riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o summ.o summ.c
    ls -ltr summ.o
    </code></pre>
    <br>
    <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task%201/cmd_risc.jpg"    alt=Commands >
    <br><br>
    <pre><code>riscv64-unknown-elf-objdump -d summ.o |less</code></pre>
    <br>
    <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task%201/obj_dump.jpg" alt=Object dump>
      <br>
      <br>
      <b>For O1: The number of instructions were 15</b><br><br>
    <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task%201/o1_ass.jpg" alt=O1 output>
    <br><br>
    <pre><code>riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o summ.o summ.c</code></pre>
    <br>
      <b>For Ofast: the number of instructions were 12</b>
      <br><br>
    <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task%201/fast_ass.jpg"  alt=Ofast output>
    <br><br>
    </details>
<hr>
<!--End of Task 1-->
 <!-- Task 2 -->
     <!-- Spike for Sum1ton -->				
<details>
<p><summary>
<b>Task 2:</b> Running the SPIKE Simulation and observe the performance under the -O1 and -Ofast Compiler optimization flags.
</summary></p>
<details>
<p><summary>1. Sum of Integers from 1 to n</summary></p>
<b>Debugging sum.o for O1</b>
<pre><code>riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum.o sum.c
ls -ltr sum.o
spike pk sum.o
spike -d pk sum.o</code></pre>
<b>O1 assembly output</b>
<pre>0000000000010184 &lt;main&gt;:
   10184:       ff010113                addi    sp,sp,-16
   10188:       00113423                sd      ra,8(sp)
   1018c:       04600793                li      a5,70
   10190:       fff7879b                addiw   a5,a5,-1
   10194:       fe079ee3                bnez    a5,10190 &lt;main+0xc&gt;
   10198:       00001637                lui     a2,0x1
   1019c:       96f60613                addi    a2,a2,-1681 # 96f &lt;register_fini-0xf741&gt;
   101a0:       04500593                li      a1,69
   101a4:       00021537                lui     a0,0x21
   101a8:       19050513                addi    a0,a0,400 # 21190 &lt;__clzdi2+0x48&gt;
   101ac:       26c000ef                jal     ra,10418 &lt;printf&gt;
   101b0:       00000513                li      a0,0
   101b4:       00813083                ld      ra,8(sp)
   101b8:       01010113                addi    sp,sp,16
   101bc:       00008067                ret
</pre>
<p>15 instructions for O1</p>
<br>
<img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task%202/O1_spike_sum.png" alt=debugging O1>
<br><br>
<b>Debugging sum.o for Ofast</b>
<pre><code>riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum.o sum.c
spike pk sum.o
spike -d pk sum.o</code></pre>
<b>Ofast assembly output</b>
<pre>00000000000100b0 &lt;main&gt;:
   100b0:       00001637                lui     a2,0x1
   100b4:       00021537                lui     a0,0x21
   100b8:       ff010113                addi    sp,sp,-16
   100bc:       96f60613                addi    a2,a2,-1681 # 96f &lt;main-0xf741&gt;
   100c0:       04500593                li      a1,69
   100c4:       18050513                addi    a0,a0,384 # 21180 &lt;__clzdi2+0x44&gt;
   100c8:       00113423                sd      ra,8(sp)
   100cc:       340000ef                jal     ra,1040c &lt;printf&gt;
   100d0:       00813083                ld      ra,8(sp)
   100d4:       00000513                li      a0,0
   100d8:       01010113                addi    sp,sp,16
   100dc:       00008067                ret
</pre>
<p>12 instructions for Ofast</p>
<br>
<img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task%202/Ofast_spike_sum.png",alt="debugging Ofast">
</details>	   
                                             <!-- Spike for EvenOdd -->	   
<details>
<p><summary>2. Even Odd detector</summary></p>
<b>Compiling Evenodd C program</b>
<pre><code>gedit odd.c
gcc odd.c
./a.out</code></pre>
<pre>#include  &lt;stdio.h&gt;
int main() {
    int number;
    printf("Enter an integer: ");
    scanf("%d", &amp;number);
    if (number % 2 == 0) {
        printf("%d is an even number.\n", number);
    } else {
        printf("%d is an odd number.\n", number);
    }
return 0;
}
</pre>
<br><br>
<img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task%202/c%20langauge_odd.png",alt="odd Compilation">
<br><br>
<b>Debugging odd.o for O1</b>
<pre><code>riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o odd.o odd.c
spike pk odd.o
spike -d pk odd.o</code></pre>
<b>O1 assembly output</b>
<pre>10184:       fe010113                addi    sp,sp,-32
   10188:       00113c23                sd      ra,24(sp)
   1018c:       0002b537                lui     a0,0x2b
   10190:       c3050513                addi    a0,a0,-976 # 2ac30 &lt;__clzdi2+0x44&gt;
   10194:       2a4000ef                jal     ra,10438 &lt;printf&gt;
   10198:       00c10593                addi    a1,sp,12
   1019c:       0002b537                lui     a0,0x2b
   101a0:       c4850513                addi    a0,a0,-952 # 2ac48 &lt;__clzdi2+0x5c&gt;
   101a4:       2e8000ef                jal     ra,1048c &lt;scanf&gt;
   101a8:       00c12583                lw      a1,12(sp)
   101ac:       0015f793                andi    a5,a1,1
   101b0:       02079063                bnez    a5,101d0 &lt;main+0x4c&gt;
   101b4:       0002b537                lui     a0,0x2b
   101b8:       c5050513                addi    a0,a0,-944 # 2ac50 &lt;__clzdi2+0x64&gt;
   101bc:       27c000ef                jal     ra,10438 &lt;printf&gt;
   101c0:       00000513                li      a0,0
   101c4:       01813083                ld      ra,24(sp)
   101c8:       02010113                addi    sp,sp,32
   101cc:       00008067                ret
   101d0:       0002b537                lui     a0,0x2b
   101d4:       c6850513                addi    a0,a0,-920 # 2ac68 &lt;__clzdi2+0x7c&gt;
   101d8:       260000ef                jal     ra,10438 &lt;printf&gt;
   101dc:       fe5ff06f                j       101c0 &lt;main+0x3c&gt;
</pre>
<p>23 instructions for O1</p>
<br>
<img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task%202/O1_spike_odd.png",alt="Debug O1">
<br><br>
<b>Debugging odd.o for Ofast</b>
<pre><code>riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o odd.o odd.c
spike pk odd.o
spike -d pk odd.o</code></pre>
<b>Ofast assembly output</b>  
<pre>100b0:       0002b537                lui     a0,0x2b
   100b4:       fe010113                addi    sp,sp,-32
   100b8:       c3050513                addi    a0,a0,-976 # 2ac30 &lt;__clzdi2+0x44&gt;
   100bc:       00113c23                sd      ra,24(sp)
   100c0:       378000ef                jal     ra,10438 &lt;printf&gt;
   100c4:       0002b537                lui     a0,0x2b
   100c8:       00c10593                addi    a1,sp,12
   100cc:       c4850513                addi    a0,a0,-952 # 2ac48 &lt;__clzdi2+0x5c&gt;
   100d0:       3bc000ef                jal     ra,1048c &lt;scanf&gt;
   100d4:       00c12583                lw      a1,12(sp)
   100d8:       0015f793                andi    a5,a1,1
   100dc:       02079063                bnez    a5,100fc &lt;main+0x4c&gt;
   100e0:       0002b537                lui     a0,0x2b
   100e4:       c5050513                addi    a0,a0,-944 # 2ac50 &lt;__clzdi2+0x64&gt;
   100e8:       350000ef                jal     ra,10438 &lt;printf&gt;
   100ec:       01813083                ld      ra,24(sp)
   100f0:       00000513                li      a0,0
   100f4:       02010113                addi    sp,sp,32
   100f8:       00008067                ret
   100fc:       0002b537                lui     a0,0x2b
   10100:       c6850513                addi    a0,a0,-920 # 2ac68 &lt;__clzdi2+0x7c&gt;
   10104:       334000ef                jal     ra,10438 &lt;printf&gt;
   10108:       fe5ff06f                j       100ec &lt;main+0x3c&gt;
</pre>
<p>23 instructions for Ofast</p>
<br>
<img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task%202/Ofast_spike_odd.png",alt=Ofast debug>
<br><br>
</details>
</details>
<hr>   
                                              <!--End of Task 2-->
 <!-- Task 3 -->   
<details>
	<summary>
		<b>Task 3:</b> Identify instruction type of all the instructions of the Object dump with its exact 32 bits instruction code in the desired instruction type format.
	</summary><br>
<details>
	<p><summary>
		RISC-V Instruction Formats
	</summary></p>
<!-- Explaination -->
	
<h2>Instruction Types and Fields</h2>

<p> The RISC-V instructions are categorized into types based on their filed organization.Each type has specific fields like opcode,funct3,funct4,immediate values and register numbers. The types include:</p>

<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; R-Type:</b> Register Type <br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; I-Type:</b> Immediate Type <br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; S-Type:</b> Store Type <br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; B-Type:</b> Branch Type <br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; U-Type:</b> Upper Immediate Type <br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; J-Type:</b> Jump Type <br>

<!-- R-Type -->

<h3>RISCV R-Type Instructions</h3>

<p>R-type instructions are used for operations that involve only registers. These instructions typically perform arithmetic, logical, and shift operations.</p>

<b>Format:</b><br>

<pre>
+----------------------------------------------------------------------------------------------------------------------------------+
  funct7[31:25](7-bits) | rs2[24:20](5-bits) | rs1[19:15](5-bits) | funct3[14:12](3-bits) | rd[11:7](5-bits) | opcode[6:0](7-bits)
+----------------------------------------------------------------------------------------------------------------------------------+
</pre>

<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct7:</b> Further specifies the operation.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs2:</b> Second source register.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1:</b> First source register.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3:</b> Further specifies the operation.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd:</b> Destination register.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; opcode:</b> Specifies the operation.<br>

<!-- I-Type -->

<h3>RISCV I-Type Instructions</h3>

<p>I-Type instructions cover various operations, including immediate arithmetic, load operations, and certain control flow instructions.</p>

<b>Format:</b><br>

<pre>
+----------------------------------------------------------------------------------------------------------+
  imm[31:20](12-bits) | rs1[19:15](5-bits) | funct3[14:12](3-bits) | rd[11:7](5-bits) | opcode[6:0](7-bits)
+----------------------------------------------------------------------------------------------------------+
</pre>

<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; imm:</b> Immediate Value.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1:</b> First source register.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3:</b> Further specifies the operation.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd:</b> Destination register.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; opcode:</b> Specifies the operation.<br>

<!-- S-Type -->

<h3>RISCV S-Type Instructions</h3>

<p>S-type instructions are essential for accessing and manipulating data in memory.Used to store data from a register to memory.</p>

<b>Format:</b><br>

<pre>
+--------------------------------------------------------------------------------------------------------------------------------------------+
  imm[31:25](11:5)(7-bits) | rs2[24:20](5-bits) | rs1[19:15](5-bits) | funct3[14:12](3-bits) | imm[11:7](4:0)(5-bits) | opcode[6:0](7-bits)
+--------------------------------------------------------------------------------------------------------------------------------------------+
</pre>

<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; imm:</b> Immediate Value( split into imm[11:5] and imm[4:0]).<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs2:</b> Second source register.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1:</b> First source register.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3:</b> Further specifies the operation.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; opcode:</b> Specifies the operation.<br>

<!-- B-Type -->
      
<h3>RISCV B-Type Instructions</h3>

<p>B-type instructions are crucial for implementing control flow in programs, enabling conditional execution of code blocks.Used for conditional branches, which alter the program flow based on a comparison of register values.</p>

<b>Format:</b><br>

<pre>
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
  imm[31](12)(1-bit) | imm[30:25](10:5)(6-bits) | rs2[24:20](5-bits) | rs1[19:15](5-bits) | funct3[14:12](3-bits) | imm[11:8](4:1)(4-bits) | imm[7](11)(1-bit) | opcode[6:0](7-bits)
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
</pre>

<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; imm:</b> Immediate Value( split into imm[12], imm[10:5], imm[4:1] and imm[11]).<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs2:</b> Second source register.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1:</b> First source register.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3:</b> Further specifies the operation.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; opcode:</b> Specifies the operation.<br>

<!-- U-Type -->

<h3>RISCV U-Type Instructions</h3>

<p>U-Type instructions are used for operations like loading upper immediate (LUI) and adding upper immediate to PC (AUIPC).</p>

<b>Format:</b><br>

<pre>
+----------------------------------------------------------------------------------------------------------+
                  imm[31:12](20-bits)                |    rd[11:7](5-bits)      |     opcode[6:0](7-bits)
+----------------------------------------------------------------------------------------------------------+
</pre>

<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; imm:</b> Upper 20 bits of the immediate value.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd:</b> Destination register.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; opcode:</b> Specifies the operation.<br>

<!-- J-Type -->
      
<h3>RISCV J-Type Instructions</h3>

<p>J-type instructions in RISC-V are primarily used for unconditional jumps to specific target addresses within the program.They play a crucial role in controlling the flow of execution by transferring control to a different part of the code.</p>

<b>Format:</b><br>

<pre>
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
  imm[31](20)(1-bit) | imm[30:21](10:1)(10-bits) | imm[20](11)(1-bit) | imm[19:12](19:12)(8-bits) | rd[11:7](5-bits) | opcode[6:0](7-bits)
+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
</pre>

<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; imm:</b> Immediate Value( split into imm[20], imm[10:1], imm[11] and imm[19:12]).<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd:</b> Destination register.<br>
<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; opcode:</b> Specifies the operation.<br>
</details>
<!-- Machine Codes -->
<details>
	     <p><summary>
		     Machine Codes for Different Instructions
	     </summary></p>
<h3>Machine Codes:</h3>

<pre>0000000000010184 &ltmain&gt:
   10184:       fd010113                addi    sp,sp,-48
   10188:       02113423                sd      ra,40(sp)
   1018c:       02813023                sd      s0,32(sp)
   10190:       00913c23                sd      s1,24(sp)
   10194:       01213823                sd      s2,16(sp)
   10198:       01313423                sd      s3,8(sp)
   1019c:       00300993                li      s3,3
   101a0:       00000493                li      s1,0
   101a4:       27b00913                li      s2,635
   101a8:       0024941b                slliw   s0,s1,0x2
   101ac:       0094043b                addw    s0,s0,s1
   101b0:       0014141b                slliw   s0,s0,0x1
   101b4:       00a00593                li      a1,10
   101b8:       00090513                mv      a0,s2
   101bc:       130000ef                jal     ra,102ec &lt;__moddi3&gt;
   101c0:       008504bb                addw    s1,a0,s0
   101c4:       00a00593                li      a1,10
   101c8:       00090513                mv      a0,s2
   101cc:       09c000ef                jal     ra,10268 &lt;__divdi3&gt;
   101d0:       0005091b                sext.w  s2,a0
   101d4:       fff9899b                addiw   s3,s3,-1
   101d8:       fc0998e3                bnez    s3,101a8 &lt;main+0x24&gt;
   101dc:       27b00793                li      a5,635conver
   101e0:       02f48a63                beq     s1,a5,10214 &lt;main+0x90&gt;
   101e4:       27b00593                li      a1,635
   101e8:       00021537                lui     a0,0x21
   101ec:       20850513                addi    a0,a0,520 # 21208 &lt;__clzdi2+0x58&gt;
   101f0:       390000ef                jal     ra,10580 &lt;printf&gt;
   101f4:       00000513                li      a0,0
   101f8:       02813083                ld      ra,40(sp)
   101fc:       02013403                ld      s0,32(sp)
   10200:       01813483                ld      s1,24(sp)
   10204:       01013903                ld      s2,16(sp)
   10208:       00813983                ld      s3,8(sp)
   1020c:       03010113                addi    sp,sp,48
   10210:       00008067                ret
   10214:       27b00593                li      a1,635
   10218:       00021537                lui     a0,0x21
   1021c:       1f050513                addi    a0,a0,496 # 211f0 &lt;__clzdi2+0x40&gt;
   10220:       360000ef                jal     ra,10580 &lt;printf&gt;
   10224:       fd1ff06f                j       101f4 &lt;main+0x70&gt;
</pre>

<!-- 1 -->

<h3>1. Machine code for <code>addi sp, sp, -48</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>addi sp, sp, -48</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0010011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>-48 (12 bits,two's complement) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rs1): </b>sp (x2,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Destination Register(rd): </b>sp (x2,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>000 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(-48): </b><code>111111010000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(sp=x2): </b><code>00010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd(sp=x2): </b><code>00010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0010011</code> <br><br>
<pre><code>10184:       fd010113          addi  sp, sp, -48</code></pre>
	   
<table>
	<tr>
		<th>Immediate (12 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>rd (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>111111010000</td>
		<td>00010</td>
		<td>000</td>
		<td>00010</td>
		<td>0010011</td>
	</tr>
</table>

<!-- 2 -->

<h3>2. Machine code for <code>sd ra, 40(sp)</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>sd ra, 40(sp)</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0100011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>40 (12 bits split into imm[11:5] and imm[4:0]) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Base Register(rs1): </b>sp (x2,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rd): </b>ra (x1,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>011 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(40): </b><code>000000101000 </code>(Split into imm[11:5]=<code>0000001</code> and 		imm[4:0]=<code>01000 </code>)<br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(sp=x2): </b><code>00010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs2(ra=x1): </b><code>00001</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0100011</code> <br><br>
 <b>&nbsp;&nbsp;Binary Representation:</b><br><br>
 	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; imm[11:5] (7 bits): </b><code>0000001</code><br>
  	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs2 (5 bits): </b><code>00001</code><br>
   	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1 (5 bits): </b><code>00010</code><br>
    	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3 (3 bits): </b><code>011</code><br>
     	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; imm[4:0] (5 bits): </b><code>01000</code><br>
      	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; opcode (7 bits): </b><code>0100011</code><br><br>
<pre><code>10188:       02113423        sd   ra, 40(sp)</code></pre>
	   
<table>
	<tr>
		<th>Imm[11:5] (7 bits)</th>
		<th>rs2 (5 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>imm[4:0] (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>0000001</td>
		<td>00001</td>
		<td>00010</td>
		<td>011</td>
		<td>01000</td>
		<td>0100011</td>
	</tr>
</table>

<!-- 3 -->

<h3>3. Machine code for <code>sd s0, 32(sp)</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>sd s0, 32(sp)</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0100011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>32 (12 bits split into imm[11:5] and imm[4:0]) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Base Register(rs1): </b>sp (x2,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rd): </b>s0 (x8,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>011 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(32): </b><code>000000100000 </code>(Split into imm[11:5]=<code>0000001</code> and 		imm[4:0]=<code>00000</code>)<br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(sp=x2): </b><code>00010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs2(s0=x8): </b><code>01000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0100011</code> <br><br>
 <b>&nbsp;&nbsp;Binary Representation:</b><br><br>
 	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; imm[11:5] (7 bits): </b><code>0000001</code><br>
  	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs2 (5 bits): </b><code>01000</code><br>
   	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1 (5 bits): </b><code>00010</code><br>
    	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3 (3 bits): </b><code>011</code><br>
     	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; imm[4:0] (5 bits): </b><code>00000</code><br>
      	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; opcode (7 bits): </b><code>0100011</code><br><br>
<pre><code>1018c:       02813023           sd     s0, 32(sp)</code></pre>
	   
<table>
	<tr>
		<th>Imm[11:5] (7 bits)</th>
		<th>rs2 (5 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>imm[4:0] (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>0000001</td>
		<td>01000</td>
		<td>00010</td>
		<td>011</td>
		<td>00000</td>
		<td>0100011</td>
	</tr>
</table>

<!-- 4 -->

<h3>4. Machine code for <code>sd s3, 8(sp)</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>sd s3, 8(sp)</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0100011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>8 (12 bits split into imm[11:5] and imm[4:0]) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Base Register(rs1): </b>sp (x2,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rd): </b>s3 (x19,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>011 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(8): </b><code>000000001000 </code>(Split into imm[11:5]=<code>0000000</code> and 		imm[4:0]=<code>01000</code>)<br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(sp=x2): </b><code>00010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs2(s3=x19): </b><code>10011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0100011</code> <br><br>
 <b>&nbsp;&nbsp;Binary Representation:</b><br><br>
 	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; imm[11:5] (7 bits): </b><code>0000000</code><br>
  	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs2 (5 bits): </b><code>10011</code><br>
   	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1 (5 bits): </b><code>00010</code><br>
    	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3 (3 bits): </b><code>011</code><br>
     	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; imm[4:0] (5 bits): </b><code>01000</code><br>
      	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; opcode (7 bits): </b><code>0100011</code><br><br>
<pre><code>10198:       01313423           sd    s3, 8(sp)</code></pre>
	   
<table>
	<tr>
		<th>Imm[11:5] (7 bits)</th>
		<th>rs2 (5 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>imm[4:0] (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>0000000</td>
		<td>10011</td>
		<td>00010</td>
		<td>011</td>
		<td>01000</td>
		<td>0100011</td>
	</tr>
</table>

<!-- 5 -->

<h3>5. Machine code for <code>li s3, 3</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>li s3, 3</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0010011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>1 (12 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rs1): </b>zero (x0,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Destination Register(rd): </b>s3 (x19,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>000 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(3): </b><code>000000000011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(zero=x0): </b><code>00000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd(s3=x19): </b><code>10011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0010011</code> <br><br>
<pre><code>1019c:       00300993          li    s3, 3</code></pre>
	   
<table>
	<tr>
		<th>Immediate (12 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>rd (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>000000000011</td>
		<td>00000</td>
		<td>000</td>
		<td>10011</td>
		<td>0010011</td>
	</tr>
</table>

<!-- 6 -->

<h3>6. Machine code for <code>li a1, 635</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>li a1, 635</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0010011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>635 (12 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rs1): </b>zero (x0,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Destination Register(rd): </b>a1 (x11,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>000 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(1): </b><code>001001111011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(zero=x0): </b><code>00000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd(a1=x11): </b><code>01011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0010011</code> <br><br>
<pre><code>101e4:       27b00593             li    a1,635</code></pre>
	   
<table>
	<tr>
		<th>Immediate (12 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>rd (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>001001111011</td>
		<td>00000</td>
		<td>000</td>
		<td>01011</td>
		<td>0010011</td>
	</tr>
</table>

<!-- 7 -->

<h3>7. Machine code for <code>addi sp, sp, 48</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>addi sp, sp, 48</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0010011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>-48 (12 bits,two's complement) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rs1): </b>sp (x2,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Destination Register(rd): </b>sp (x2,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>000 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(48): </b><code>000000110000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(sp=x2): </b><code>00010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd(sp=x2): </b><code>00010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0010011</code> <br><br>
<pre><code>1020c:       03010113          addi  sp, sp, 48</code></pre>
	   
<table>
	<tr>
		<th>Immediate (12 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>rd (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>000000110000</td>
		<td>00010</td>
		<td>000</td>
		<td>00010</td>
		<td>0010011</td>
	</tr>
</table>

<!-- 8 -->

<h3>8. Machine code for <code>mv a0, s2</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>mv a0, s2</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0010011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>0 (12 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rs1): </b>s2 (x18,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Destination Register(rd): </b>a0 (x10,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>000 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(0): </b><code>000000000000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(s2=x18): </b><code>10010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd(a0=x10): </b><code>01010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0010011</code> <br><br>
<pre><code>101c8:       00090513            mv    a0, s2</code></pre>
	   
<table>
	<tr>
		<th>Immediate (12 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>rd (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>000000000000</td>
		<td>10010</td>
		<td>000</td>
		<td>01010</td>
		<td>0010011</td>
	</tr>
</table>

<!-- 9 -->

<h3>9. Machine code for <code>sext.w s2, a0</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>sext.w s2, a0</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0011011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>0 (12 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rs1): </b>a0 (x10,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Destination Register(rd): </b>s2 (x18,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>000 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(1): </b><code>000000000000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(a0=x10): </b><code>01010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd(s2=x18): </b><code>10010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0011011</code> <br><br>
<pre><code>101d0:       0005091b         sext.w  s2, a0 </code></pre>
	   
<table>
	<tr>
		<th>Immediate (12 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>rd (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>000000000000</td>
		<td>01010</td>
		<td>000</td>
		<td>10010</td>
		<td>0011011</td>
	</tr>
</table>

<!-- 10 -->

<h3>10. Machine code for <code>addiw s3, s3, -1</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>addiw s3, s3, -1</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0011011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>1 (12 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rs1): </b>s3 (x19,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Destination Register(rd): </b>s3 (x19,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>000 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(-1): </b><code>111111111111</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(s3=x19): </b><code>10011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd(s3=x19): </b><code>10011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0011011</code> <br><br>
<pre><code>101d4:       fff9899b          addiw   s3, s3, -1</code></pre>
	   
<table>
	<tr>
		<th>Immediate (12 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>rd (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>111111111111</td>
		<td>10011</td>
		<td>000</td>
		<td>10011</td>
		<td>0011011</td>
	</tr>
</table>

<!-- 11 -->

<h3>11. Machine code for <code>lui a0, 0x21</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>lui a0, 0x21</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0110111 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>0x21(33) (20 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Destination Register(rd): </b>a0 (x10,5 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(0x21): </b><code>00000000000000100001</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd(a0=x10): </b><code>01010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0110111</code> <br><br>
<pre><code>101e8:       00021537          lui  a0, 0x21</code></pre>
	   
<table>
	<tr>
		<th>Immediate (20 bits)</th>
		<th>rd (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>00000000000000100001</td>
		<td>01010</td>
		<td>0110111</td>
	</tr>
</table>

<!-- 12 -->

<h3>12. Machine code for <code>ld ra, 40(sp)</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>ld ra, 40(sp)</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0000011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>40 (12 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rs1): </b>sp (x2,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Destination Register(rd): </b>ra (x1,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>011 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(24): </b><code>000000101000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(sp=x2): </b><code>00010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd(ra=x1): </b><code>00001</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0000011</code> <br><br>
<pre><code>101f8:       02813083           ld   ra, 40(sp)</code></pre>
	   
<table>
	<tr>
		<th>Immediate (12 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>rd (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>000000101000</td>
		<td>00010</td>
		<td>011</td>
		<td>00001</td>
		<td>0000011</td>
	</tr>
</table>

<!-- 13 -->

<h3>13. Machine code for <code>slliw   s0,s1,0x2</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>slliw   s0,s1,0x2</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0011011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>0x2 (12 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rs1): </b>s1 (x9,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Destination Register(rd): </b>s0 (x8,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>001 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(2): </b><code>000000000010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(s1=x9): </b><code>10001</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd(s0=x8): </b><code>01000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0000011</code> <br><br>
<pre><code>101a8:       0024941b            slliw  s0, s1, 0x2</code></pre>
	   
<table>
	<tr>
		<th>Immediate (12 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>rd (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>000000000010</td>
		<td>01001</td>
		<td>001</td>
		<td>01000</td>
		<td>0011011</td>
	</tr>
</table>

<!-- 14 -->

<h3>14. Machine code for <code>addw s0, s0, s1</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>addw s0, s0, s1</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0111011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>8 (12 bits) <br>
 	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rs2): </b>s1 (x9,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rs1): </b>s0 (x8,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Destination Register(rd): </b>s0 (x8,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>000 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(0): </b><code>000000000000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs2(s1=x9): </b><code>01001</code> <br>
 	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(s0=x0): </b><code>01000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd(s0=x0): </b><code>01000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0111011</code> <br><br>
<pre><code>101ac:       0094043b          addw s0, s0, s1</code></pre>
	   
<table>
	<tr>
		<th>funct7 (7 bits)</th>
		<th>rs2 (5 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>rd (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>0000000</td>
		<td>01001</td>
		<td>01000</td>
		<td>000</td>
		<td>01000</td>
		<td>0111011</td>
	</tr>
</table>

<!-- 15 -->

<h3>15. Machine code for <code>ret</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>ret</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>1100111 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>0 (12 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rs1): </b>ra (x1,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Destination Register(rd): </b>zero (x0,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>000 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(1): </b><code>000000001011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(ra=x1): </b><code>00001</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd(zero=x0): </b><code>00000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>1100111</code> <br><br>
<pre><code>10210:       00008067       ret</code></pre>
	   
<table>
	<tr>
		<th>Immediate (12 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>rd (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>000000000000</td>
		<td>00001</td>
		<td>000</td>
		<td>00000</td>
		<td>1100111</td>
	</tr>
</table>
</details>
</details>
<hr>
<!--End of Task 3-->
<!-- Task 4 -->
<details><summary><b>Task 4: </b>By using RISC-V Core: Verilog netlist and Testbench, perform an experiment of Functional Simulation using GTKWave and Observe the waveforms.</summary>
    <h3>Steps:</h3>
    1. Using suitable commands install the iverilog and GTKWave in ubuntu<br>
    2. Compile the RISC-V Core: Verilog netlist and Testbench<br>
    3. Observe the waveform output in GTKWave window<br>
    <h4>Installing iverilog and GTKWave in Ubuntu:</h4>
    <pre><code>sudo apt install iverilog gtkwave</code></pre>
    <h3>Simulate and run the verilog code</h3>
    <pre><code>iverilog -o iiitb_rv32i iiitb_rv32i.v iiitb_rv32i_tb.v
    ./iiitb_rv32i
    gtkwave iiitb_rv32i.vcd</code></pre>
    <h4>GTKWave Window:</h4><br>
    <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/waveform.png" alt="GTKWave Window">
    <br><br>
    <h4>Hardcoded Instructions:</h4><br>
    <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/Instructions.png" alt="Hardcoded ISA">
    <br>
    <h3>Ouput Waveforms:</h3>
    <p>The output waveforms showing the instructions performed in a 5-stage pipelined architecture</p>
    <b><i>Instruction 1:</i></b><pre> ADD R6, R2, R1</pre>
        <p>This instruction Adds values of registers R2 and R1 and stores the result in register R6, In this case 1 + 2 = 3.</p>
        <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/add%20r6%2Cr1%2Cr2.png" alt="ADD R6, R2, R1">
    <br><br><b><i>Instruction 2:</i></b><pre> SUB R7, R1, R2</pre>
        <p>This instruction subtracts value of register R2 from R1 and stores the result in register R7, In this case 1 - 2 = -1.</p>
        <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/sub%20r7%2Cr1%2Cr2.png" alt="SUB R7, R1, R2">
    <br><br><b><i>Instruction 3:</i></b><pre> AND R8, R1, R3</pre>
        <p>This instruction executes bitwise "AND" between values of registers R1 and R3 and stores the result in register R8, In this case 01 & 11 = 01(1 in decimal).</p>
        <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/and%20r8%2Cr1%2Cr3.png" alt="AND R8, R1, R3">
    <br><br><b><i>Instruction 4:</i></b><pre> OR R9, R2, R5</pre>
        <p>This instruction executes bitwise "OR" between values of registers R2 and R5 and stores the result in register R9, In this case 010 | 101 = 111(7 in decimal).</p>
        <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/or%20r9%2Cr2%2Cr5.png" alt="OR R9, R2, R5">
    <br><br><b><i>Instruction 5:</i></b><pre> XOR R10, R1, R4</pre>
        <p>This instruction executes bitwise XOR between values of registers R1 and R4 and stores the result in register R10, In this case 001 ^ 100 = 101(5 in decimal).</p>
        <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/xor%20r10%2Cr1%2Cr4.png" alt="XOR R10, R1, R4">
    <br><br><b><i>Instruction 6:</i></b><pre> SLT R11, R2, R4</pre>
        <p>This instruction checks the values of registers R2 and R4 if value of R2 is less than value of R4, then register R11 is set to 1, In this case 2<4 so R11 is set to 1.</p>
        <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/slt%20r11%2Cr2%2Cr4.png" alt="SLT R11, R2, R4">
    <br><br><b><i>Instruction 7:</i></b><pre> ADDI R12, R4, 5</pre>
        <p>This instruction adds the immediate data 5 to the value in register R4 and stores the result in register R12, In this case 4 + 5 = 9.</p>
        <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/addi%20r12%2Cr4%2C5.(i7).png" alt="ADDI R12, R4, 5">
    <br><br><b><i>Instruction 8:</i></b><pre> SW R3, R1, 2</pre>
        <p>This instruction stores the register data @R1+2 into the memory, In this case 1 + 2 = 3.</p>
        <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/sw%20r3%2Cr1%2C2.png" alt="SW R3, R1, 2">
    <br><br><b><i>Instruction 9:</i></b><pre> LW R13, R1, 2</pre>
        <p>This instruction loads the register data @R1+2 into the register R13, In this case 1 + 2 = 3.</p>
        <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/lw%20r13%2Cr1%2C2.png" alt="LW R13, R1, 2">
    <br><br><b><i>Instruction 10:</i></b><pre> BEQ R0, R0, 15</pre>
        <p>This instruction Branches to 15 instructions ahead of current instruction if values of registers R0 equals R0, so Program Counter will be incremented by 15, In this case PC is 10 so new PC value will be 10+15=25.</p>
        <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/beq%20r0%2Cr0%2C15.png" alt="BEQ R0, R0, 15">
    <br><br><b><i>Instruction 11:</i></b><pre> ADD R14, R2 R2</pre>
        <p> This instruction Adds values of registers R2 and R2 and stores the result in register R14, In this case 2 + 2 = 4.</p>
        <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/add%20r14%2Cr2%2Cr2.png" alt="ADD R14, R2 R2">
    <br><br><b><i>Instruction 12:</i></b><pre> BNE R0, R1, 20</pre>
        <p>This instruction Branches to 20 instructions ahead of current instruction if values of registers R0 and R1 don't match , so Program Counter will be incremented by 20, In this case PC is 28 so new PC value will be 28+20=48.</p>
        <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/bne%20r0%2Cr1%2C20.png" alt="BNE R0, R1, 20">
    <br><br><b><i>Instruction 13:</i></b><pre> ADDI R12, R4, 5</pre>
        <p>This instruction adds the immediate data 5 to the value in register R4 and stores the result in register R12, In this case 4 + 5 = 9.</p>
        <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/addi%20r12%2Cr4%2C5.png" alt="ADDI R12, R4, 5">
    <br><br><b><i>Instruction 14:</i></b><pre> SLL R15, R1, R2</pre>
        <p>This instruction shifts the value of register R1 to left by 2, (001)&lt;&lt;2=(100)4.</p>
        <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/sll%20r15%2Cr1%2Cr2(2).png" alt="SLL R15, R1, R2">
    <br><br><b><i>Instruction 15:</i></b><pre> SRL R16, R4, R2</pre>
        <p>This instruction shifts the value of register R1 to right by 2, (100)&gt;&gt;2=(001)1.</p>
        <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task4/srl%20r16%2Cr14%2Cr2(2).png" alt="SRL R16, R4, R2">
    <br><br>
    </details>
    <!--End of Task 4-->
<hr>

<!--task 5-->
<details>
  <summary>
      <b>
        Task 5:
      </b>
      To implement any digital circuit using VSDSquadron Mini and check whether building and uploading of C program file on RISCV processor works.  
  </summary>
  <h2>
    Implement Binary to Grey code converter using VSDSquadronmini
  </h2>

  <h3>
    Overview
  </h3>

  <p>
This project involves the implementation of a binary-to-Gray code converter using the VSD Squadron Mini, a RISC-V-based SoC development kit. Gray code is a binary numeral system where two successive values differ by only one bit, making it useful in minimizing errors in digital systems. The implementation includes reading a binary input from GPIO pins, applying the Gray code conversion logic, and displaying the output using LEDs. This project demonstrates the practical application of digital encoding techniques and microcontroller-based signal processing, highlighting the efficiency of RISC-V for embedded system applications.
  </p>

  <h3>
   Components Required
  </h3>

  <ul>
    <li>
      VSD Squadron Mini
    </li>
    <li>
      Push buttons for clock
    </li>
    <li>
      8 LEDs for Output Binary and Grey code
    </li>
    <li>
      Bread Board
    </li>
    <li>
      Jumper wires
    </li>
    <li>
     VS Code for software Development
    </li>
    <li>
    PlatformIO multi framework professional IDE
    </li>
  </ul>
  <h3>
  Hardware Connections
  </h3>
  <ul>
    <li>
      <b>
        Input:
      </b>
      <p>
        One input connected to the GPIO Pins of VSDsquadron Mini via push button mounted on the breadboard.
      </p>
    </li>
    <li>
      <b>
        Output:
      </b>
      <p>
       Eight LEDs are connected to display the result of Binary and Grey code.
      </p>
    </li>
    <li>
      <p>
      The GPIO pins are configured according to the reference mannual ensuring the correct flow of signals between the components.
      </p>
    </li>
  </ul>
  <br>
  <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task%205/circuit.png">
  <br>

  <h3>
Block Diagram
  </h3>
  <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/Task%205/gray-to-binary-circuit-1.jpg">
  <br>
  <p>
The block diagram represents a 4-bit Binary to Gray Code Converter using XOR gates. It consists of:  
  </p>
  <ul>
<li>
<b>Inputs:</b> Four binary bits labeled  <b>b<sub>3</sub></b>, <b>b<sub>2</sub></b>,<b>b<sub>1</sub></b>, <b>b<sub>0</sub></b>.
</li>

<li>
<b>Logic Gates:</b> Three XOR gates are used to process the input bits and generate the corresponding Gray code.
</li>

<li>
<b>Outputs:</b> Four grey bits labeled  <b>g<sub>3</sub></b>, <b>g<sub>2</sub></b>,<b>g<sub>1</sub></b>, <b>g<sub>0</sub></b>.
</li>

<li>
The diagram visually shows the flow of data, where each XOR gate receives two inputs and produces one output, forming a sequential logic circuit.
</li>
  </ul>
  <h3>
    Working
  </h3>
  <p>
A Binary to Gray Code Converter is a combinational logic circuit that converts a binary number into its equivalent Gray code. Gray code is a special type of binary numeral system where two consecutive numbers differ by only one bit, reducing errors in digital systems like encoders and data transmission.
  </p>


  <p>
3 XOR gates to process the binary input:
  </p>
	  
<pre>
g3 = b3
g2 = b3 ^ b2
g1 = b2 ^ b1
g0 = b1 ^ b0
</pre>


<h3>Truth Table for Binary to Grey</h3>
<h3>Truth Table for Binary to Gray Conversion</h3>
<table>
<!--Row 1-->
	<tr>
		<th colspan="4" align="center">Binary</th><th colspan="4" align="center">Gray</th>
	</tr>
<!--Row 2-->
<tr> 
<!--B -->  <th>B<sub>3</sub></th> <th>B<sub>2</sub></th> <th>B<sub>1</sub></th> <th>B<sub>0</sub></th> 
<!--G -->  <th>G<sub>3</sub></th> <th>G<sub>2</sub></th> <th>G<sub>1</sub></th> <th>G<sub>0</sub></th>
</tr>	
<!--Row 3-->
<tr> 
<!--B -->  <td>0</td> <td>0</td> <td>0</td> <td>0</td> 
<!--G -->  <td>0</td> <td>0</td> <td>0</td> <td>0</td>
</tr>	
<!--Row 4-->
<tr> 
<!--B -->  <td>0</td> <td>0</td> <td>0</td> <td>1</td> 
<!--G -->  <td>0</td> <td>0</td> <td>0</td> <td>1</td>
</tr>
<!--Row 5-->
<tr> 
<!--B -->  <td>0</td> <td>0</td> <td>1</td> <td>0</td> 
<!--G -->  <td>0</td> <td>0</td> <td>1</td> <td>1</td>
</tr>
<!--Row 6-->
<tr> 
<!--B -->  <td>0</td> <td>0</td> <td>1</td> <td>1</td> 
<!--G -->  <td>0</td> <td>0</td> <td>1</td> <td>0</td>
</tr>
<!--Row 7-->
<tr> 
<!--B -->  <td>0</td> <td>1</td> <td>0</td> <td>0</td> 
<!--G -->  <td>0</td> <td>1</td> <td>1</td> <td>0</td>
</tr>
<!--Row 8-->
<tr> 
<!--B -->  <td>0</td> <td>1</td> <td>0</td> <td>1</td> 
<!--G -->  <td>0</td> <td>1</td> <td>1</td> <td>1</td>
</tr>
<!--Row 9-->
<tr> 
<!--B -->  <td>0</td> <td>1</td> <td>1</td> <td>0</td> 
<!--G -->  <td>0</td> <td>1</td> <td>0</td> <td>1</td>
</tr>
<!--Row 10-->
<tr> 
<!--B -->  <td>0</td> <td>1</td> <td>1</td> <td>1</td> 
<!--G -->  <td>0</td> <td>1</td> <td>0</td> <td>0</td>
</tr>
<!--Row 11-->
<tr> 
<!--B -->  <td>1</td> <td>0</td> <td>0</td> <td>0</td> 
<!--G -->  <td>1</td> <td>1</td> <td>0</td> <td>0</td>
</tr>
<!--Row 12-->
<tr> 
<!--B -->  <td>1</td> <td>0</td> <td>0</td> <td>1</td> 
<!--G -->  <td>1</td> <td>1</td> <td>0</td> <td>1</td>
</tr>
<!--Row 13-->
<tr> 
<!--B -->  <td>1</td> <td>0</td> <td>1</td> <td>0</td> 
<!--G -->  <td>1</td> <td>1</td> <td>1</td> <td>1</td>
</tr>
<!--Row 14-->
<tr> 
<!--B -->  <td>1</td> <td>0</td> <td>1</td> <td>1</td> 
<!--G -->  <td>1</td> <td>1</td> <td>1</td> <td>0</td>
</tr>
<!--Row 15-->
<tr> 
<!--B -->  <td>1</td> <td>1</td> <td>0</td> <td>0</td> 
<!--G -->  <td>1</td> <td>0</td> <td>1</td> <td>0</td>
</tr>
<!--Row 16-->
<tr> 
<!--B -->  <td>1</td> <td>1</td> <td>0</td> <td>1</td> 
<!--G -->  <td>1</td> <td>0</td> <td>1</td> <td>1</td>
</tr>
<!--Row 17-->
<tr> 
<!--B -->  <td>1</td> <td>1</td> <td>1</td> <td>0</td> 
<!--G -->  <td>1</td> <td>0</td> <td>0</td> <td>1</td>
</tr>
<!--Row 18-->
<tr> 
<!--B -->  <td>1</td> <td>1</td> <td>1</td> <td>1</td> 
<!--G -->  <td>1</td> <td>0</td> <td>0</td> <td>0</td>
</tr>
</table>

<h3>
  Code
</h3>
<pre>
#include&lt;stdio.h&gt;
#include&lt;debug.h&gt;
#include&lt;ch32v00x.h&gt;
#include&lt;math.h&gt;
#define N 8  // Define N as a macro
void GPIO_Config(void)
{
    GPIO_InitTypeDef GPIO_InitStructure = {0}; 
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD, ENABLE);
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOC, ENABLE);
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_4;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU; // Defined as Input Type.
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOC, &GPIO_InitStructure);
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_0 | GPIO_Pin_1 | GPIO_Pin_2 | GPIO_Pin_3 | GPIO_Pin_5 | GPIO_Pin_6 | GPIO_Pin_7;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOD, &GPIO_InitStructure);
    GPIO_Init(GPIOC, &GPIO_InitStructure);
}
int main()
{
    int lsfr[N] = {1, 0, 0, 0, 0, 0, 0, 0};  // Initialize all elements
    int lsfr_1[N];
    NVIC_PriorityGroupConfig(NVIC_PriorityGroup_1);
    SystemCoreClockUpdate();
    Delay_Init();
    GPIO_Config();
    while(1)
    {
        if (GPIO_ReadInputDataBit(GPIOC, GPIO_Pin_4) == 0)
    {
        i++%16;
        binary[3] = i & 1;
        binary[2] = (i>>1) & 1;
        binary[1] = (i>>2) & 1;
        binary[0] = (i>>3) & 1;

        binary[4] = binary[0];
        binary[5] = binary[0] ^ binary[1];
        binary[6] = binary[1] ^ binary[2];
        binary[7] = binary[2] ^ binary[3];

        GPIO_WriteBit(GPIOC, GPIO_Pin_3, (binary[7]) ? SET : RESET);
        GPIO_WriteBit(GPIOC, GPIO_Pin_2, (binary[6]) ? SET : RESET);
        GPIO_WriteBit(GPIOC, GPIO_Pin_1, (binary[5]) ? SET : RESET);
        GPIO_WriteBit(GPIOC, GPIO_Pin_0, (binary[4]) ? SET : RESET);
        
        GPIO_WriteBit(GPIOC, GPIO_Pin_6, (binary[3]) ? SET : RESET);
        GPIO_WriteBit(GPIOC, GPIO_Pin_7, (binary[2]) ? SET : RESET);
        GPIO_WriteBit(GPIOD, GPIO_Pin_2, (binary[1]) ? SET : RESET);
        GPIO_WriteBit(GPIOD, GPIO_Pin_3, (binary[0]) ? SET : RESET);
        Delay_Ms(500);

    }
    }

}
</pre>


</details>

<hr>
Binary to Grey Implementation_Video
<p>
  Higher Quality Video
</p>
<ul>
  <li>
<a href="https://youtu.be/u1Xu52OwNDE"
target="_blank">
 Youtube Link
</a>
</li>
</ul>
</body>
</html>
