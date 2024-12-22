# vault-door-3

**Flag:**  `picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_c79a21}`

How you approached the challenge:
- We are given the java source code with in which we have to do some operations to a following string
```
        for (i=0; i<8; i++) {
            buffer[i] = password.charAt(i);
        }
        for (; i<16; i++) {
            buffer[i] = password.charAt(23-i);
        }
        for (; i<32; i+=2) {
            buffer[i] = password.charAt(46-i);
        }
        for (i=31; i>=17; i-=2) {
            buffer[i] = password.charAt(i);
        }
        String s = new String(buffer);
        return s.equals("jU5t_a_sna_3lpm12g94c_u_4_m7ra41");
``` 
- for 1st 7 characters we need not do anything `jU5t_a_s`
- for next 8 to 15 indices we need to print the character at `(23-i)th` index which leads to `1mpl3_an`
- for next 16,18,20,22...30 indices we need to print the characters at `(46-i)th` index which leads to `4gr4m_4_u_c79a21`
- next operation is useless as no change occurs to the odd indices from `17 to 31`
- final string which is the flag is `jU5t_a_s1mpl3_an4gr4m_4_u_c79a21`
  
Other incorrect methods you tried:
- Tried rearranging the string manually

# GDB baby step 1

**Flag:**  `picoCTF{549698}`

How you approached the challenge:
- In this question we had to use the gdb debugger on the file `debugger0_a` and then used `disassemble main` (because it was told that we need to gather info on main function) to convert the machine code to assembly code, where i found what was needed
```bash
(gdb) disassemble main
Dump of assembler code for function main:
   0x0000000000001129 <+0>:     endbr64
   0x000000000000112d <+4>:     push   %rbp
   0x000000000000112e <+5>:     mov    %rsp,%rbp
   0x0000000000001131 <+8>:     mov    %edi,-0x4(%rbp)
   0x0000000000001134 <+11>:    mov    %rsi,-0x10(%rbp)
   0x0000000000001138 <+15>:    mov    $0x86342,%eax
   0x000000000000113d <+20>:    pop    %rbp
   0x000000000000113e <+21>:    ret
End of assembler dump.
```
Here the contents of the `eax` register are given as `$0x86342` which ono converting to decimal gives `549698`, hence we got the flag.
  
Other incorrect methods you tried:
- Using GDB and commands like `disassemble` to convert the machine code to assembly code
- basic knowledge about registers , EAX, AX etc..
- syntax of assembly code, `mov $0x86342,%eax` means moving the the content `$0x86342` to `eax`

