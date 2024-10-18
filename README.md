Praveen BV
212222100036

## Aim:
To implement the AES (Advanced Encryption Standard) encryption and decryption algorithm using a C programming language, demonstrating how to encrypt and decrypt a block of plaintext using a predefined AES key in 128-bit mode.

## Procedure:

1.	Introduction to AES:
    AES is a symmetric key encryption standard, meaning the same key is used for both encryption and decryption.
    It operates on fixed-size blocks of data (128-bit block size) and supports key sizes of 128, 192, or 256 bits.
    This implementation focuses on AES-128, which uses a 128-bit key and performs 10 rounds of encryption.
  	
3.	Steps for Encryption:
    Step 1: Define the key and plaintext.
        Select a 128-bit key (16 bytes) and a 128-bit block of plaintext data for encryption.
    Step 2: Initialize the key schedule.
        The AES key expansion algorithm generates round keys from the initial key. Each round key is used for one round of encryption.
    Step 3: Add the initial round key.
        XOR the first round key with the plaintext to initialize the encryption process.
    Step 4: Perform 9 rounds of AES transformations:
        SubBytes: Each byte in the block is replaced by its corresponding value from the S-box (Substitution Box).
        ShiftRows: The rows of the block are cyclically shifted by a certain number of bytes.
        MixColumns: The columns of the block are mixed to produce new values (except for the last round).
        AddRoundKey: The current round key is XORed with the block.
    Step 5: Final round (10th round):
        Perform SubBytes, ShiftRows, and AddRoundKey transformations (MixColumns is skipped in this round).
    Step 6: The resulting output is the encrypted ciphertext.
  	
5.	Steps for Decryption:
    Step 1: Initialize the key schedule with the same 128-bit key used for encryption.
    Step 2: Add the final round key to the ciphertext to begin the decryption process.
    Step 3: Perform the inverse AES transformations for 9 rounds:
        InvShiftRows: Perform the inverse row shifting.
        InvSubBytes: Replace each byte using the inverse S-box.
        InvMixColumns: Mix the columns in reverse order.
        AddRoundKey: XOR the block with the corresponding round key.
   Step 4: Final round (10th round):
        Perform InvShiftRows, InvSubBytes, and AddRoundKey (InvMixColumns is skipped).
    Step 5: The resulting output is the decrypted plaintext.
  	
7.	Key Components:
    AES Key Expansion: This step generates round keys from the initial AES key, using the AES key schedule process.
    SubBytes: Byte substitution using the S-box for non-linearity.
    ShiftRows: Cyclically shifts the rows to mix data across columns.
    MixColumns: Mixes the bytes within each column for diffusion.
    AddRoundKey: Adds (XORs) the round key with the state.
  	
9.	Implementation:
    Write a C program that implements these AES transformations.
    Use arrays to store the key, round keys, plaintext, and ciphertext.
    Ensure that both encryption and decryption functions are implemented.
  	
10.	Testing:
    Test the program by encrypting a known plaintext using the AES-128 key and then decrypting the resulting ciphertext back to the original plaintext.
    Print both the encrypted and decrypted values to verify correctness.

## Program:

```
#include <stdio.h>
#include <stdint.h>
#include <string.h>

// Define constants for AES (simplified version)
#define Nb 4            // Number of columns comprising the State (always 4 for AES)
#define Nk 4            // Number of 32-bit words comprising the key (Nk=4 for AES-128)
#define Nr 10           // Number of rounds for AES-128

// AES S-box
uint8_t sbox[256] = {
    // Fill in with the actual S-box values here (256 entries)
};

// Round constant for key expansion
uint8_t Rcon[11] = {
    // Fill in with round constant values
};

// AES key schedule and helper functions
void KeyExpansion(uint8_t *key, uint8_t *roundKeys) {
    // Implement key expansion
}

void AddRoundKey(uint8_t round, uint8_t *state, uint8_t *roundKey) {
    // XOR round key with state
}

void SubBytes(uint8_t *state) {
    // Substitution step using S-box
}

void ShiftRows(uint8_t *state) {
    // Row shifting
}

void MixColumns(uint8_t *state) {
    // Column mixing
}

void AES_encrypt(uint8_t *input, uint8_t *output, uint8_t *key) {
    uint8_t state[16];
    uint8_t roundKey[176];  // To hold all the round keys

    KeyExpansion(key, roundKey);

    memcpy(state, input, 16);

    // Initial round key addition
    AddRoundKey(0, state, roundKey);

    // Main rounds
    for (int round = 1; round < Nr; round++) {
        SubBytes(state);
        ShiftRows(state);
        MixColumns(state);
        AddRoundKey(round, state, roundKey);
    }

    // Final round
    SubBytes(state);
    ShiftRows(state);
    AddRoundKey(Nr, state, roundKey);

    // Copy encrypted data to output
    memcpy(output, state, 16);
}

// For decryption, you would need to implement the inverse steps like InvSubBytes, InvShiftRows, InvMixColumns

int main() {
    uint8_t key[16] = {0x2b, 0x7e, 0x15, 0x16, 0x28, 0xae, 0xd2, 0xa6,
                       0xab, 0xf7, 0x3c, 0xf2, 0x4b, 0x45, 0x77, 0x3c};  // AES-128 key

    uint8_t input[16] = {0x32, 0x43, 0xf6, 0xa8, 0x88, 0x5a, 0x30, 0x8d,
                         0x31, 0x31, 0x98, 0xa2, 0xe0, 0x37, 0x07, 0x34};  // Example input block

    uint8_t output[16];  // To hold the encrypted output

    AES_encrypt(input, output, key);

    printf("Encrypted data: ");
    for (int i = 0; i < 16; i++) {
        printf("%02x ", output[i]);
    }
    printf("\n");

    return 0;
}
```
## OUTPUT:
 ![image](https://github.com/user-attachments/assets/944e2167-4ee0-4c8b-b0a1-cf418f4f861f)

