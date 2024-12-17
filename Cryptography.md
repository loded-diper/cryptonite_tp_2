# C3

  

**Flag:**  `picoCTF{adlibs}`

How you approached the challenge:

- So basically the encoding is done by finding the index of each character of the flag in `lookup1` string and is encoded as the `(current - previous)%40`th index in `lookup2` string.
- To decode this we have the outputted string which is
```
DLSeGAGDgBNJDQJDCFSFnRBIDjgHoDFCFtHDgJpiHtGDmMAQFnRBJKkBAsTMrsPSDDnEFCFtIbEDtDCIbFCFtHTJDKerFldbFObFCFtLBFkBAAAPFnRBJGEkerFlcPgKkImHnIlATJDKbTbFOkdNnsgbnJRMFnRBNAFkBAAAbrcbTKAkOgFpOgFpOpkBAAAAAAAiClFGIPFnRBaKliCgClFGtIBAAAAAAAOgGEkImHnIl
```  
- We'll take each character if this string and try to find the `cur` variable (which originally made the string) and out decoded message will be simply `lookup1[cur]`.
- This is the code which can decode the `out`
```python
lookup1 = "\n \"#()*+/1:=[]abcdefghijklmnopqrstuvwxyz"
lookup2 = "ABCDEFGHIJKLMNOPQRSTabcdefghijklmnopqrst"
out="DLSeGAGDgBNJDQJDCFSFnRBIDjgHoDFCFtHDgJpiHtGDmMAQFnRBJKkBAsTMrsPSDDnEFCFtIbEDtDCIbFCFtHTJDKerFldbFObFCFtLBFkBAAAPFnRBJGEkerFlcPgKkImHnIlATJDKbTbFOkdNnsgbnJRMFnRBNAFkBAAAbrcbTKAkOgFpOgFpOpkBAAAAAAAiClFGIPFnRBaKliCgClFGtIBAAAAAAAOgGEkImHnIl"
dec = ""
prev =0
for _ in out:
    cur=(prev+lookup2.index(_))%40
    dec += lookup1[cur]
    prev = cur
print(dec)
```
- We first find the cur variable which was used to encode it and the `cur`th index in `lookup1` string is out character of the original string.
- The original string came out to be 
```python
#asciiorder
#fortychars
#selfinput
#pythontwo

chars = ""
from fileinput import input
for line in input():
    chars += line
b = 1 / 1

for i in range(len(chars)):
    if i == b * b * b:
        print chars[i] #prints
        b += 1 / 1
```
- here the comments suggest that the code is in Python 2.0 and we have to give self input to the program to find the flag, after a while i figured out that the self input is this code itself, on running this code with input the code itself on python 2 we got the flag.
![final image](https://github.com/loded-diper/cryptonite_tp_2/blob/main/Images/C3.png)

What you learned through solving this challenge:
1. Cryptography
  
Other incorrect methods you tried:
- Tried to input `lookup1`, `lookup2` and other string as an input to the second step.   
References
- https://www.reddit.com/r/learnpython/comments/gjthg6/print_vs_sysstdoutwrite_in_python_2x_vs_python_3x/

# miniRSA

**Flag:**  `picoCTF{n33d_a_lArg3r_e_d0cd6eae}`

How you approached the challenge:

- We are given a standard RSA encryption except the fact that the value of `e` is very small `e=3`, which makes it possible for us to decrypt it.
- To begin we know that in a RSA encryption the algorithm is `C=pow(M,e)%N` , where M is the number to be encrypted, e is the public exponent, N is the product of two very large prime numbers & C is the encrypted text.
- So C is the remainder obtained on dividing `M^e` by `N`, so we can re-write it as, `M^e = N*i + c`, where i is the quotient in the division.
- So if we can find `i` we can decrypt it, & because `M^e` is not a whole lot bigger than `C` due to the fact `e` is small, it will be easy to find `i`.
- So i wrote a code which runs until i find a value of `i` which satisfies the equation `M=(N*i+c)^(1/3)`
```python
import gmpy2
n=29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e=6000
c=2205316413931134031074603746928247799030155221252519872650080519263755075355825243327515211479747536697517688468095325517209911688684309894900992899707504087647575997847717180766377832435022794675332132906451858990782325436498952049751141
i=0
while (True):
    find=n*i+c
    flag,perfect_root=gmpy2.iroot(find,e)
    if perfect_root:
        break
    i+=1
# Convert the integer to bytes
flag=flag.to_bytes((flag.bit_length()+8)// 8)
ascii_flag=''
for _ in flag:
    ascii_flag+=chr(_)
print(ascii_flag)
```
-After we got the flag as integer, i converted it to byte array using the `to_bytes()` method and then converted the whole byte array to ascii text and printed it which fetched me the flag.

What you learned through solving this challenge:
1. Use of gmpy2 library, as calculating roots in the normal way was giving overflowerror, because python can't handle very large float numbers & this library calculates the nearest integer cube root.
2. Converting long integer to byte arrays
3. Converting byte arrays to text
4. Use & working of RSA algorithm
  
Other incorrect methods you tried:
- Tried to calculate integer with `flag=(n*i+c)^(1/3), which gave overflowerror
- Tried to convert the byte array to long without adding 7 in the specified bit length. 

References

 - https://www.youtube.com/watch?v=rlJTMUBXhKE&t=337s&pp=ygUNcnNhIGFsZ29yaXRobQ%3D%3D
 - https://stackoverflow.com/questions/15390807/integer-square-root-in-python
 - https://www.geeksforgeeks.org/how-to-convert-int-to-bytes-in-python/

# Custom Encryption

**Flag:**  `picoCTF{custom_d2cr0pt6d_49fbee5b}`

How you approached the challenge:

```python
if __name__ == "__main__":
    message = sys.argv[1]
    test(message, "trudeau")
```
- Starting from this , we know that the `message` which is the flag is taken from the command line using `sys.argv[1]` and the second text `trudeau` will be used to encrypt this in someway are sent to the function `test`
```python
def test(plain_text, text_key):
    p = 97
    g = 31
    if not is_prime(p) and not is_prime(g):
        print("Enter prime numbers")
        return
    a = randint(p-10, p)
    b = randint(g-10, g)
    print(f"a = {a}") #90
    print(f"b = {b}") #26
    u = generator(g, a, p) #64
    v = generator(g, b, p) #9
    key = generator(v, a, p) #22
    b_key = generator(u, b, p) #22
    shared_key = None
    if key == b_key:
        shared_key = key #22
    else:
        print("Invalid key")
        return
    semi_cipher = dynamic_xor_encrypt(plain_text, text_key)
    cipher = encrypt(semi_cipher, shared_key)
    print(f'cipher is: {cipher}')

```
- In this function we can see two variables p & q initialized above & then they are used to calculate the values a & b, which are given in the output & I've also commented their values respectively. Using these values of u, v, key & b_key are calculated using a function `generator` which does same encryption as done in `RSA` but the modulus is very small, equal to `p` which is `97` , so at last the value of `shared_key` which will be used for further encryption comes out to be `22`.
- Then the `flag` and the text `trudeau` are sent to a function `dynamic_xor_encrypt` to get the `semi-cipher`.

```python
def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)	#7
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text
```
- XOR takes place here with a character from `trudeau` which is decided by `i % key_length` & a letter from the flag `back to start` which is then returned & used as `semi-cipher`

```python
def encrypt(plaintext, key):
    cipher = []
    for char in plaintext:
        cipher.append(((ord(char) * key*311)))
    return cipher
```
- For the final encryption, the `semi-cipher` & the `shared-key=22` is sent to this function, where each character of the semi-cipher is multiplied by `key*311` to create a list which is shown in the output to us.

- So i created an algorithm which divides each element from the list by `key*311` (where key is 22), to get the ascii value of `semi-cipher` & hence create the semi-cipher.
- Then i retrace the steps, which is basically performing one more XOR using the characters of the obtained `semi-cipher` with the text `trudeau` using the same characters as used for encryptions which is decided by `i % key_length`, then i finally print the obtained flag in reverse as it was encrypted in reverse.
```python
c=[61578, 109472, 437888, 6842, 0, 20526, 129998, 526834, 478940, 287364, 0, 567886, 143682, 34210, 465256, 0, 150524, 588412, 6842, 424204, 164208, 184734, 41052, 41052, 116314, 41052, 177892, 348942, 218944, 335258, 177892, 47894, 82104, 116314]
semi_cipher=''
key=22
for i in c:
    semi_cipher+=chr(int(i/(key*311)))
text_key="trudeau"
deciphered_text=''
key_length = len(text_key)
for i, char in enumerate(semi_cipher[::1]):
        key_char = text_key[i % key_length]
        unencrypted_char = chr(ord(char) ^ ord(key_char))
        deciphered_text += unencrypted_char
print(deciphered_text[::-1])
```
This is how i found the flag


What you learned through solving this challenge:
1. Cryptography
2. Use of function `enumerate()`
  
Other incorrect methods you tried:
- None

 
References
- https://www.geeksforgeeks.org/enumerate-in-python/