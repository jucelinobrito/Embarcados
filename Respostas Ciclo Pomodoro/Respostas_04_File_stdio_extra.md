1. Crie um código em C que escreve a sequência de Fibonacci em arquivo em formato binário. Comece a sequência com os valores 0 e 1, e grave suas primeiras 100 posições em arquivo.

#include<stdio.h>
#include<stdlib.h>

int main(int argc, char *argv[])
{
	FILE *fp;                                           //Declara ponteiro para o arquivo
	int k;	
	float i,j,aux;
	float fibo[100];
	if((fp = fopen("fibo.bin","wb")) == NULL)	    //rotina para abrir o arquivo fibo.bin para escrita em binário
	{
		printf("\nImpossivel abrir o arquivo!\n"); //se ocorrer um erro na abertura do arquivo retorna essa mensagem ao usuário e encerra
		exit(1);
	}
	
	i = 0;
	j = 1;
	
	fibo[0] = 0;
	fibo [1] = 1;
	
	for (k = 0; k < 100; k++)
	{
		aux = i + j;
		i = j;
		j = aux;
		fibo [k+2] = aux;
	}

	for(k = 0; k < 100; k++)
	{
		fprintf(fp,"%.f ",fibo[k]);
	}

	fclose(fp);
	
	return 0;

}


2. Crie um código em C que lê o arquivo da questão anterior e escreve os valores lidos da sequência de Fibonacci na tela.

#include<stdio.h>
#include<stdlib.h>

int main(int argc, char *argv[])
{
	FILE *fp;                                           //Declara ponteiro para o arquivo
	int k;	
	char c;
	if((fp = fopen("fibo.bin","rb")) == NULL)	    //rotina para abrir o arquivo fibo.bin para leitura
	{
		printf("\nImpossivel abrir o arquivo!\n"); //se ocorrer um erro na abertura do arquivo retorna essa mensagem ao usuário e encerra
		exit(1);
	}

	while((c = getc(fp)) != EOF)
		 printf("%c", c);
	
	fclose(fp);
	return 0;


}
