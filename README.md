## RSA Encryption Algorithm

## Aim:

The aim of the RSA Encryption Algorithm is to securely transmit information over an insecure network by using a public key for encryption and a private key for decryption. RSA, one of the first public-key cryptosystems, is widely used for secure data transmission, digital signatures, and secure key exchanges.

## Algorithm

 Step 1: Choose two distinct large prime numbers ppp and qqq.

 Step 2: Compute n=p×qn = p \times qn=p×q. nnn will be used as part of the public and private keys.

 Step 3: Calculate ϕ(n)=(p−1)×(q−1)\phi(n) = (p-1) \times (q-1)ϕ(n)=(p−1)×(q−1), where ϕ\phiϕ is Euler's Totient function.

 Step 4: Choose an integer eee such that 1<e<ϕ(n)1 < e < \phi(n)1<e<ϕ(n) and gcd⁡(e,ϕ(n))=1\gcd(e, \phi(n)) = 1gcd(e,ϕ(n))=1. eee is the public exponent.

 Step 5: Compute ddd as the modular multiplicative inverse of emod ϕ(n)e \mod \phi(n)emodϕ(n), such that e×d≡1mod ϕ(n)e \times d \equiv 1 \mod \phi(n)e×d≡1modϕ(n). ddd is the private exponent.

 Step 6: The public key is (e,n)(e, n)(e,n), and the private key is (d,n)(d, n)(d,n).

## Encryption

 Step 1: To encrypt a message MMM, convert it into an integer mmm, where m<nm < nm<n.

 Step 2: Compute the ciphertext C=memod nC = m^e \mod nC=memodn.

 Step 3: The encrypted message is CCC.

## Decryption:

 Step 1: To decrypt the ciphertext CCC, use the private key ddd.

 Step 2: Compute m=Cdmod nm = C^d \mod nm=Cdmodn, which gives the original message mmm.

 Step 3: Convert mmm back to the original message MMM.

## PROGRAM:

#include <stdio.h>
#include <math.h>
long long gcd(long long a, long long b) {
while (b != 0) {
long long temp = b;
b = a % b;
a = temp;
}
return a;
}
long long modInverse(long long a, long long m) {
a = a % m;
for (long long x = 1; x < m; x++) {
if ((a * x) % m == 1) {
return x;
}
}
return 1;
}
long long power(long long base, long long exp, long long mod) {
long long result = 1;
base = base % mod;
while (exp > 0) {
if (exp % 2 == 1) {
result = (result * base) % mod;
}
exp = exp >> 1;
base = (base * base) % mod;
}
return result;
}
int isPrime(long long n) {
if (n <= 1) return 0;
for (long long i = 2; i <= sqrt(n); i++) {
if (n % i == 0) return 0;
}
return 1;
}
int main() {
long long p, q, n, phi, e, d, message, encryptedMessage, decryptedMessage;
// Choose two prime numbers
printf("Enter prime number p: ");
scanf("%lld", &p);
while (!isPrime(p)) {
printf("p is not a prime number. Enter a prime number: ");
scanf("%lld", &p);
}
printf("Enter prime number q: ");
scanf("%lld", &q);
while (!isPrime(q)) {
printf("q is not a prime number. Enter a prime number: ");
scanf("%lld", &q);
}
// Calculate n = p * q
n = p * q;
// Calculate phi(n) = (p-1)*(q-1)
phi = (p - 1) * (q - 1);
// Choose e such that 1 < e < phi(n) and gcd(e, phi(n)) = 1
printf("Enter public key exponent e (1 < e < %lld and gcd(e, %lld) = 1): ", phi, phi);
scanf("%lld", &e);
while (gcd(e, phi) != 1) {
printf("Invalid e. Enter a valid public key exponent: ");
scanf("%lld", &e);
}
// Calculate the private key d such that (d * e) % phi = 1
d = modInverse(e, phi);
// Enter the message
printf("Enter the message to encrypt (as an integer): ");
scanf("%lld", &message);
// Encrypt the message
encryptedMessage = power(message, e, n);
printf("Encrypted message: %lld\n", encryptedMessage);
// Decrypt the message
decryptedMessage = power(encryptedMessage, d, n);
printf("Decrypted message: %lld\n", decryptedMessage);
return 0;
}

## OUTPUT:
![Crypto-9 1](https://github.com/user-attachments/assets/1147b2a3-a3f3-402c-ab78-7339e0bc184e)

## RESULT:
Thus the program to execute RSA Algorithm is executed successfully.
