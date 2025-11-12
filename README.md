# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:
```
#include <stdio.h>
#include <math.h>

// Function to compute modular exponentiation: (base^exp) % mod
long long modExp(long long base, long long exp, long long mod) {
    long long result = 1;
    base = base % mod;  // Ensure base < mod
    while (exp > 0) {
        if (exp % 2 == 1) {  // If exponent is odd
            result = (result * base) % mod;
        }
        base = (base * base) % mod;
        exp = exp / 2;
    }
    return result;
}

int main() {
    long long p, g;
    long long privateKeyA, publicKeyA;
    long long message, k;
    long long c1, c2, decryptedMessage;

    printf("***** ElGamal Encryption/Decryption *****\n\n");

    // Step 1: Input a large prime p and generator g
    printf("Enter a large prime number (p): ");
    scanf("%lld", &p);

    printf("Enter a generator (g): ");
    scanf("%lld", &g);

    // Step 2: Alice inputs her private key
    printf("Enter Alice's private key: ");
    scanf("%lld", &privateKeyA);

    // Step 3: Compute Alice's public key
    publicKeyA = modExp(g, privateKeyA, p);
    printf("Alice's public key: %lld\n", publicKeyA);

    // Step 4: Bob inputs the message to encrypt and selects random k
    printf("Enter the message to encrypt (as a number < p): ");
    scanf("%lld", &message);

    printf("Enter a random number k: ");
    scanf("%lld", &k);

    // Step 5: Compute ciphertext
    c1 = modExp(g, k, p);                    // c1 = g^k mod p
    c2 = (message * modExp(publicKeyA, k, p)) % p;  // c2 = m * (publicKeyA^k) mod p

    printf("Encrypted message (c1, c2): (%lld, %lld)\n", c1, c2);

    // Step 6: Alice decrypts the message
    decryptedMessage = (c2 * modExp(c1, p - 1 - privateKeyA, p)) % p;

    printf("Decrypted message: %lld\n", decryptedMessage);

    return 0;
}
```

## Output:
<img width="1919" height="1145" alt="image" src="https://github.com/user-attachments/assets/24e410d3-cf1a-42a6-a924-639c5a028e61" />

<img width="1893" height="909" alt="image" src="https://github.com/user-attachments/assets/c7b39cb3-73cc-438a-b575-50e4906bde7e" />


## Result:
The program is executed successfully.
