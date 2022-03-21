# chall_01_pwn_writeup

Welcome to the UD Secure Software Design aka x86Exploit course challenge one. Course contents avalible at https://sec.prof.ninja/.

  Course Author: Professor Andy Novocin
  
# chall_01

We begin by performing some recon on the binary. We run 'file a.out' and 'checksec a.out'

Observe the following:
  1. file command output states it's **dynamically** linked and **64bit**
  2. checksec reports there is no stack canary, meaning we are free to smash the stack with a buffer overflow.

Next, we open the file using radare2. Entering the command 'r2 -Ad a.out', observe main:

We see there is a win function, but it's not called at any point during the program exection. 

We open pwntools, start the process and observe with radare2 in debug mode. Grab the win address and smash the stack to change the ret address. 

![image](https://user-images.githubusercontent.com/79220528/159311833-56b4e4a0-ecc5-4d63-961a-2293c9031ebd.png)
