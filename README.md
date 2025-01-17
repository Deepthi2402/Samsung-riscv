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
<b>&nbsp;&nbsp;Instruction: </b><code>sd s1, 8(sp)</code>  <br><br>
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
<pre><code>10198:       01313423           sd    s1, 8(sp)</code></pre>
	   
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

<h3>7. Machine code for <code>li s1, 11</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>li s1, 11</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0010011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>11 (12 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rs1): </b>zero (x0,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Destination Register(rd): </b>s1 (x9,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>000 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(1): </b><code>000000001011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(zero=x0): </b><code>00000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd(s1=x9): </b><code>01001</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0010011</code> <br><br>
<pre><code>1019c:       00b00493            li     s1, 11</code></pre>
	   
<table>
	<tr>
		<th>Immediate (12 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>rd (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>000000001011</td>
		<td>00000</td>
		<td>000</td>
		<td>01001</td>
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
<b>&nbsp;&nbsp;Instruction: </b><code>sext.w a1, a0</code>  <br><br>
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
<pre><code>10218:       00021537          lui  a0, 0x21</code></pre>
	   
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

<h3>13. Machine code for <code>ld s0, 16(sp)</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>ld s0, 16(sp)</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0000011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>16 (12 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rs1): </b>sp (x2,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Destination Register(rd): </b>s0 (x8,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>011 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(16): </b><code>000000010000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(sp=x2): </b><code>00010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd(s0=x8): </b><code>01000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0000011</code> <br><br>
<pre><code>101d0:       01013403          ld   s0, 16(sp)</code></pre>
	   
<table>
	<tr>
		<th>Immediate (12 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>rd (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>000000010000</td>
		<td>00010</td>
		<td>011</td>
		<td>01000</td>
		<td>0000011</td>
	</tr>
</table>

<!-- 14 -->

<h3>14. Machine code for <code>ld s1, 8(sp)</code></h3>
<b>&nbsp;&nbsp;Instruction: </b><code>ld s1, 8(sp)</code>  <br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b>0000011 (7 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate: </b>8 (12 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Source Register(rs1): </b>sp (x2,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Destination Register(rd): </b>s1 (x9,5 bits) <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Function(funct3): </b>011 (3 bits) <br><br>
<b>&nbsp;&nbsp;Breakdown:</b><br><br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Immediate(8): </b><code>000000001000</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rs1(sp=x2): </b><code>00010</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; funct3: </b><code>011</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; rd(s1=x9): </b><code>01001</code> <br>
	<b>&nbsp;&nbsp;&nbsp;&nbsp;&#183; Opcode: </b><code>0000011</code> <br><br>
<pre><code>101d4:       00813483          ld   s1, 8(sp)</code></pre>
	   
<table>
	<tr>
		<th>Immediate (12 bits)</th>
		<th>rs1 (5 bits)</th>
		<th>funct3 (3 bits)</th>
		<th>rd (5 bits)</th>
		<th>Opcode (7 bits)</th>
	</tr>
	<tr>
		<td>000000001000</td>
		<td>00010</td>
		<td>011</td>
		<td>01001</td>
		<td>0000011</td>
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

</body>
</html>
