# EX.-NO-1-C-IMPLEMENTATION-OF-HILL-CIPHER

## AIM:
To write a C program to implement the hill cipher substitution techniques.

## ALGORITHM:

STEP-1: Read the plain text and key from the user.

STEP-2: Split the plain text into groups of length three.

STEP-3: Arrange the keyword in a 3*3 matrix.

STEP-4: Multiply the two matrices to obtain the cipher text of length three.

STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM: 
    #include <stdio.h>
    #include <string.h>
    #include <ctype.h>
    void prepareKeyMatrix(char key[], int keyMatrix[3][3]);
    void prepareText(char text[]);
    void multiplyMatrices(int keyMatrix[3][3], int textVector[3], int cipherMatrix[3]);
    void encryptGroup(char keyMatrix[3][3], char text[], char cipher[], int startIdx);
    void encryptText(char text[], char key[], char cipher[]);

    int main() {
    char text[100], key[10], cipher[100];
    printf("Enter the plain text: ");
    gets(text);
    printf("Enter the key (9 characters): ");
    gets(key);
    encryptText(text, key, cipher);
    printf("Cipher text: %s\n", cipher);

    return 0;
    }
    void prepareKeyMatrix(char key[], int keyMatrix[3][3]) {
    int i, j, k = 0;
    for(i = 0; i < 3; i++) {
        for(j = 0; j < 3; j++) {
            keyMatrix[i][j] = (toupper(key[k]) - 'A') % 26;
            k++;
        }
    }
    }

    void prepareText(char text[]) {
    int i, j = 0;
    char prepared[100];
    
    for(i = 0; i < strlen(text); i++) {
        if (isalpha(text[i])) {
            prepared[j++] = toupper(text[i]);
        }
    }
    while (j % 3 != 0) {
        prepared[j++] = 'X';
    }
    prepared[j] = '\0';
    strcpy(text, prepared);
    }

    void multiplyMatrices(int keyMatrix[3][3], int textVector[3], int cipherMatrix[3]) {
    int i, j;
    for(i = 0; i < 3; i++) {
        cipherMatrix[i] = 0;
        for(j = 0; j < 3; j++) {
            cipherMatrix[i] += keyMatrix[i][j] * textVector[j];
        }
        cipherMatrix[i] = cipherMatrix[i] % 26;
    }
    }

    void encryptGroup(char keyMatrix[3][3], char text[], char cipher[], int startIdx) {
    int i;
    int textVector[3], cipherMatrix[3];

    for(i = 0; i < 3; i++) {
        textVector[i] = text[startIdx + i] - 'A';
    }

    multiplyMatrices(keyMatrix, textVector, cipherMatrix);

    for(i = 0; i < 3; i++) {
        cipher[startIdx + i] = cipherMatrix[i] + 'A';
    }
    }

    void encryptText(char text[], char key[], char cipher[]) {
    int keyMatrix[3][3], i;

    prepareText(text);
    prepareKeyMatrix(key, keyMatrix);

    for(i = 0; i < strlen(text); i += 3) {
        encryptGroup(keyMatrix, text, cipher, i);
    }
    cipher[i] = '\0';
}

## OUTPUT:
Enter the plain text: good luck

Enter the key (9 characters): qwertyuio

Cipher text: SCMGMMGWA
## RESULT:
  Thus the hill cipher substitution technique had been implemented successfully.
