Questão 1.

#include<stdio.h>

int main(int argc, char **argv)
{
	printf("Ola Mundo!\n");
	return 0;

}

Questão 2.

#include<stdio.h>

int main(int argc, char **argv)
{
	char nome[15];
	printf("Qual o seu nome?\n");
	scanf("%s",nome);
	printf("Ola %s\n",nome);
	return 0;
}

Questão 3.

a) O resultado é apenas o primeiro nome digitado.
b) O resultado é o primeiro nome digitado precedido de uma aspa dupla
c) O programa roda direto e apresenta o nome digitado apos "echo", ou seja, não 
   é pedido para digitar o nome durante a execução do programa.

d) O resultado é apenas o primeiro nome digitado.
e) O resultado é o primeiro nome sem aspa alguma.
f) O resultado do programa é a primeira palavra digitada repetida devido ao comando echo

Questão 4.

#include<stdio.h>

int main(int argc, char **argv)
{
	if(argc < 2)
	{
		printf("Digite o seu nome logo após chamar o programa\n");
		printf("Por exemplo:\n");
		printf("$./ola_usuario2 Jucelino\n");		
		return -1;		
	}
	
		printf("Ola %s\n",argv[1]);	
		
	return 0;
}

Questão 5.

a) O resultado é apenas o primeiro nome digitado.
b) O resultado são todos os nomes digitados entre as aspas duplas.
c) O programa roda direto mas não recebe o argumento do comando echo, gerando um erro de não recebimento de argumento.

d) Ele não reconhece o argumento gerado através do pipe.
e) Da mesma forma como as duas questões anteriores.
f) O programa não reconhece o texto do arquivo "Ola.txt" como argumento de entrada.

Questão 6.

#include<stdio.h>

int main(int argc, char **argv)
{
	if(argc < 2)
	{
		printf("Digite o seu nome logo após chamar o programa\n");
		printf("Por exemplo:\n");
		printf("$./ola_usuario2 Jucelino\n");		
		return -1;		
	}
	
		printf("Ola %s\n",argv[1]);
		printf("Numero de entradas : %d\n", argc);	
		
	return 0;
}


Questão 7. 

#include <stdio.h>

int main(int argc, char **argv)
{
	int i = 1;	

	if(argc < 2)
	{
		printf("Digite o seu nome logo após chamar o programa\n");
		printf("Por exemplo:\n");
		printf("$./ola_usuario2 Jucelino\n");		
		return -1;		
	}
	
	printf("Ola ");
	
	do
	{
		printf("%s ", argv[i]);
		i++;

	} while (i < argc);
	
	printf("\n");
		
	return 0;
}

Questão 8. 

Parte 1: 

int Num_Caracs(char *string)
{
	int i = 0;
	char test;

	while ( test != '\0')
	{
		test = string[i];
		i++;
	}

	return i;
}

Parte 2:

int Num_Caracs(char *string);

Questão 9 e 10

Função:num_caracs.c

int Num_Caracs(char *string)
{
	int i = 0;
	char test ;

	do
	{
		test = string[i];
		++i;

	} while ( test != '\0');

	return (i-1);
}

Protótipo Função: num_caracs.h

int Num_Caracs(char *string);

Programa principal: ola_num_caracs1.c

#include <stdio.h>
#include <stdlib.h>
#include "num_caracs.h"

int main(int argc, char **argv)
{
	int i = 0;	

	if(argc < 2)
	{
		printf("Digite o seu nome logo após chamar o programa\n");
		printf("Por exemplo:\n");
		printf("$./ola_usuario2 Jucelino\n");		
		return -1;		
	}
	
	do
	{
		printf("Argumento:%s ", argv[i]);
		printf("/ Numero de caracteres: %d\n", Num_Caracs(argv[i]));
		i++;

	} while (i < argc);
	
	printf("\n");
		
	return 0;
}

Arquivo Makefile

num_caracs: ola_num_caracs1.o num_caracs.o 
	gcc $(flagso) -o ola_num_caracs1 ola_num_caracs1.o num_caracs.o
ola_num_caracs1.o: ola_num_caracs1.c num_caracs.h
	gcc $(flagso) -c ola_num_caracs1.c
num_caracs.o: num_caracs.c num_caracs.h
	gcc $(flagso) -c num_caracs.c
clean:
	rm -f *.o num_caracs

Questão 11 e 12.

#include <stdio.h>
#include <stdlib.h>
#include "num_caracs.h"

int main(int argc, char **argv)
{
	int i = 0;
	int j = 0;
	int tot = 0;

	if(argc < 2)
	{
		printf("Digite o seu nome logo após chamar o programa\n");
		printf("Por exemplo:\n");
		printf("$./ola_usuario2 Jucelino\n");		
		return -1;		
	}
	
	do
	{
		printf("%s ", argv[i]);
		j = Num_Caracs(argv[i]);
		tot = tot + j;
		i++;

		
	} while (i < argc);

	printf("\nNumero caracteres argumentos de entrada: %d", tot); 
	
	printf("\n");
		
	return 0;
}

Arquivo Makefile:

num_caracs: ola_num_caracs2.o num_caracs.o 
	gcc $(flagso) -o ola_num_caracs2 ola_num_caracs2.o num_caracs.o
ola_num_caracs2.o: ola_num_caracs2.c num_caracs.h
	gcc $(flagso) -c ola_num_caracs2.c
num_caracs.o: num_caracs.c num_caracs.h
	gcc $(flagso) -c num_caracs.c
clean:
	rm -f *.o num_caracs




