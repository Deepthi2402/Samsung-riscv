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
   </body></html>
