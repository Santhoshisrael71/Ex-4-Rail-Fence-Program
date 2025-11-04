# Ex-5 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

void encryptRailFence(char *message, int rails, char *encrypted) {
    int len = strlen(message);
    char rail[rails][len];
    int i, j;

    // Initialize rail matrix with '\n'
    for (i = 0; i < rails; i++)
        for (j = 0; j < len; j++)
            rail[i][j] = '\n';

    int row = 0, dir = 1;

    // Build the zig-zag pattern
    for (i = 0; i < len; i++) {
        rail[row][i] = message[i];
        if (row == 0)
            dir = 1;
        else if (row == rails - 1)
            dir = -1;
        row += dir;
    }

    // Read the matrix row-wise
    int k = 0;
    for (i = 0; i < rails; i++)
        for (j = 0; j < len; j++)
            if (rail[i][j] != '\n')
                encrypted[k++] = rail[i][j];

    encrypted[k] = '\0';
}

void decryptRailFence(char *cipher, int rails, char *decrypted) {
    int len = strlen(cipher);
    char rail[rails][len];
    int i, j;

    // Initialize rail matrix
    for (i = 0; i < rails; i++)
        for (j = 0; j < len; j++)
            rail[i][j] = '\n';

    int row = 0, dir = 1;

    // Mark the zig-zag path
    for (i = 0; i < len; i++) {
        rail[row][i] = '*';
        if (row == 0)
            dir = 1;
        else if (row == rails - 1)
            dir = -1;
        row += dir;
    }

    // Fill the marked positions with cipher text
    int index = 0;
    for (i = 0; i < rails; i++)
        for (j = 0; j < len; j++)
            if (rail[i][j] == '*' && index < len)
                rail[i][j] = cipher[index++];

    // Read the matrix in zig-zag pattern
    row = 0;
    dir = 1;
    index = 0;
    for (i = 0; i < len; i++) {
        decrypted[index++] = rail[row][i];
        if (row == 0)
            dir = 1;
        else if (row == rails - 1)
            dir = -1;
        row += dir;
    }

    decrypted[index] = '\0';
}

int main() {
    char message[100], encrypted[100], decrypted[100];
    int rails;

    printf("Enter a Secret Message: ");
    scanf("%[^\n]s", message);

    // Remove spaces and convert to uppercase
    char temp[100];
    int k = 0;
    for (int i = 0; message[i]; i++) {
        if (message[i] != ' ')
            temp[k++] = toupper(message[i]);
    }
    temp[k] = '\0';
    strcpy(message, temp);

    printf("Enter number of rails: ");
    scanf("%d", &rails);

    encryptRailFence(message, rails, encrypted);
    printf("\nEncrypted text: %s", encrypted);

    decryptRailFence(encrypted, rails, decrypted);
    printf("\nDecrypted text: %s\n", decrypted);

    return 0;
}

```
# OUTPUT
<img width="1611" height="857" alt="image" src="https://github.com/user-attachments/assets/ed888539-b3b0-4085-8ff6-4531bfd43615" />

# RESULT
The given code is Executed Successfully
