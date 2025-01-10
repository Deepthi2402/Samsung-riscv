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
    <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/task%201/cprog_ex1.jpg"  alt=C code>
    <br><br>
    <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/task%201/cprog_output.jpg"      alt=commands for c compilation>
    <br><br>
    <b>2. Object Dump and O1, Ofast Output</b>
    <br><br>
    <pre><code>
    cat summ.c
    riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o summ.o summ.c
    ls -ltr summ.o
    </code></pre>
    <br>
    <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/task%201/cmd_risc.jpg"    alt=Commands >
    <br><br>
    <pre><code>riscv64-unknown-elf-objdump -d summ.o |less</code></pre>
    <br>
    <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/task%201/obj_dump.jpg" alt=Object dump>
      <br>
      <br>
      <b>For O1: The number of instructions were 15</b><br><br>
    <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/task%201/o1_ass.jpg" alt=O1 output>
    <br><br>
    <pre><code>riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o summ.o summ.c</code></pre>
    <br>
      <b>For Ofast: the number of instructions were 12</b>
      <br><br>
    <img src="https://github.com/Deepthi2402/Samsung-riscv/blob/main/task%201/fast_ass.jpg"  alt=Ofast output>
    <br><br>
    </details>
<hr>
<!--End of Task 1-->
