#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define CIPHER_SIZE 52
typedef struct
{
	char originalCharacter;
	char cipherCharacter;
} Cipher;
void ReadCipherFile(Cipher* cipherArray)
{
	FILE* fp;
	int i = 0;
	fp = fopen("cipher.txt", "r");
	while (!feof(fp))
	{
		//Read the original character
		cipherArray[i].originalCharacter = fgetc(fp);
		//Read the cipher character
		cipherArray[i].cipherCharacter = fgetc(fp);
		//Read the newline character
		fgetc(fp);
		i++;
	}
}
//Function Input: character to subsitute and cipher array
//Function output: Subsituted character if part of cipher array
//Description: Given a character and the cipher array, return the substitution if it exists
char CipherSub(char in, const Cipher* cipherArray)
{
	int i;
	for(i =0 ; i< CIPHER_SIZE; i++)
	//linear search from 0 to CIPHER_SIZE
	{
		if (in == cipherArray[i].originalCharacter)
		{
			return cipherArray[i].cipherCharacter;
		}
	}
	return -1;
}
//Function Input: String to cipher and cipher array
//Function Output: Ciphered string (passed by reference)
//Description: Given a string input, create an output string that is all  substituted character
//For example: A string input of "abc123." would have an output string of "zyx123."
void ProcessCipher(char* input, char* output, const Cipher* cipherArray)
{
	int i = 0;
	char give;
// Go through from the first character to the string length of input 
	for(i; i<strlen(input); i++)
	{
		give = CipherSub(input[i], cipherArray);

		//TODO: Call CipherSub() and see what it returns
		if (CipherSub(input[i], cipherArray) == -1)
		{
			output[i] = input[i];

		}
		else
		{
			output[i] = give;
		}
	}
	output[i] = '\0';
}
//Function Input: File pointers for input, output and cipher array
//Function Output: None
//Description: Go through the input file and process string by string.  Take every 
//de-ciphered string and output it to the output file
void ProcessFiles(FILE* fIn, FILE* fOut, const Cipher* cipherArray)
{
	char bufferIn[10000];
	char bufferOut[10000];
	char* input;
	char output[100]="";
	while (!feof(fIn))
	{
		input = fgets(bufferIn, 10000, fIn);
		ProcessCipher(input, &output[0], cipherArray);
		fputs(output, fOut);
	}
}
void main()
{
	Cipher cipherArray[CIPHER_SIZE];
	FILE* fIn = 0;
	FILE* fOut = 0;
	char fileNameIn[1000];
	char fileNameOut[1000];
	ReadCipherFile(cipherArray);

	printf("Enter the file to input: ");
	gets(fileNameIn);
	printf("Enter the file to output: ");
	gets(fileNameOut);
	fIn = fopen("EncryptedText.txt", "r");
	fOut = fopen("Result.txt", "w");

	ProcessFiles(fIn, fOut, cipherArray);
	fclose(fIn);
	fclose(fOut);
}

