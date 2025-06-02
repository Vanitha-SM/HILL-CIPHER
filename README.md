# HILL CIPHER
HILL CIPHER
EX. NO: 3 AIM:
 

IMPLEMENTATION OF HILL CIPHER
 
## To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM:
```
def mod_inverse(a, m):
    a %= m
    for x in range(1, m):
        if (a * x) % m == 1:
            return x
    return -1

def determinant(matrix):
    return (matrix[0][0]*matrix[1][1] - matrix[0][1]*matrix[1][0]) % 26

def inverse_matrix(matrix):
    det = determinant(matrix)
    det_inv = mod_inverse(det, 26)
    if det_inv == -1:
        raise ValueError("Matrix is not invertible")

    inv = [
        [ matrix[1][1] * det_inv % 26, -matrix[0][1] * det_inv % 26],
        [-matrix[1][0] * det_inv % 26,  matrix[0][0] * det_inv % 26]
    ]
    
    # Make sure all values are positive mod 26
    for i in range(2):
        for j in range(2):
            inv[i][j] = inv[i][j] % 26
    return inv

def multiply(matrix, vector):
    result = [0, 0]
    for i in range(2):
        result[i] = sum(matrix[i][j] * vector[j] for j in range(2)) % 26
    return result

def hill_cipher(text, matrix, encrypt=True):
    text = text.upper().replace(" ", "").replace("J", "I")
    if len(text) % 2 != 0:
        text += 'X'  # padding

    if not encrypt:
        matrix = inverse_matrix(matrix)

    output = ""
    for i in range(0, len(text), 2):
        block = [ord(text[i]) - ord('A'), ord(text[i+1]) - ord('A')]
        result = multiply(matrix, block)
        output += ''.join(chr(r + ord('A')) for r in result)
    
    return output

# --- Main Section ---
key_matrix = [[3, 3], [2, 5]]
message = "DHANALAKSHMI"

encrypted = hill_cipher(message, key_matrix, encrypt=True)
decrypted = hill_cipher(encrypted, key_matrix, encrypt=False)

print("Original  :", message)
print("Encrypted :", encrypted)
print("Decrypted :", decrypted)


```

## OUTPUT:
![image](https://github.com/user-attachments/assets/52d3c9c5-53de-422f-bb44-83103e109ddb)


## RESULT:
The program is executed successfully


