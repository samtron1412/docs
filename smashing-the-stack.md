[TOC]

# Shellcode
We can *modify the return address* and the flow of execution, what program do we want to execute? In most case we'll simply want the program *spawn a shell*. How can we place arbitrary instruction into its address space? The answer is to place the code with are trying to execute in the buffer we are overflowing, and overwrite the return address so it points back into the buffer.
