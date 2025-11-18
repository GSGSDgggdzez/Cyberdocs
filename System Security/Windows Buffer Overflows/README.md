# Buffer Overflows Walkthrough - CyberMentor

- Anatomy of Memory:
	
	Memory structure

		> Kernel: also called "TOP" ==> 11111
		> Stack
		> Heap
		> Data
		> Text: also called "BOTTOM" ==> 00000


- Anatomy of Stack
	
	Stack structure
	
		> ESP(Extended Stack Pointer): also called "TOP"
		> Buffer Space
		> EBP (Extended Base Pointer): also called "BOTTOM"
		> EIP (Extended Instruction Pointer) / Return Address

	Explanation:
		
		The BUFFER SPACE executes from top to bottom.
		The goal of BOF is to fill the BUFFER SPACE with random characters ('A') and the EBP, EIP.
		To have a BOF attack we must fill the used BUFFER SPACE and write on the EBP and reach the EIP which is an address pointer (Next instruction | return address). What we can do is use this address to point to a direction we want. And this direction can be malicious code containing a reverse-shell.


- Buffer Overflows Walkthrough
	
	Steps to conduct a buffer overflow
	
		> Spiking
		> Fuzzing
		> Finding the Offset
		> Overwriting the EIP
		> Finding Bad Characters
		> Finding the Right Module
		> Generating Shellcode
		> Root!

	Explanation
		
		> Used to find a vulnerable part of a program
		> Once the vulnerability is found, we can use FUZZER to CRASH the program
		> If we crash it, we look for at what moment we can crash it correctly (OFFSET)
		> And we use this OFFSET to overwrite the EIP address the return pointer
		> Once we control the EIP, we must do some cleanup tasks:
			- find the bad characters (BAD CHARS)
			- find the right modules (RIGHT MOD)
		> Once the bad characters and modules are found, we can generate our reverse-shell by pointing EIP to a malicious shellcode.

Tools to be USED

	>  Kali Linux
	>  Windows 10
	>  Vulnserver (run on port 9999 by default)
	>  Immunity Debugger
