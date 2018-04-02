Questão 1.

#include <stdio.h>
#include <stdlib.h>

int main( int argc, char **argv)
{
	FILE *fp;
	char string[100] = "Ola Mundo !\n";
	if((fp = fopen("ola_mundo.txt","w")) == NULL)
	{
		printf("\nImpossivel abrir o arquivo!\n");
		exit(1);
	}

	fputs(string,fp);
	fclose(fp);
	return 0;
}

Questão 2.

#include <stdio.h>
#include <stdlib.h>

int main(int argc, char **argv)
{
	char nome[100];
	int idade;
	FILE *fp;
	printf("Digite seu nome:\n");
	gets(nome);
	printf("Digite sua idade:\n");
	scanf("%d",&idade);
	
	if((fp = fopen(nome,"w")) == NULL)
	{
		printf("Impossivel abrir arquivo!\n");
		exit(1);
	}
	fprintf(fp,"Nome: %s\n",nome);
	fprintf(fp,"Idade: %d\n",idade);
	fclose(fp);
	return 0;	
	

}

Questão 3.

#include <stdio.h>
#include <stdlib.h>

int main(int argc, char **argv)
{
	FILE *fp;	
	if (argc < 2) 
	{
		printf("Argumento Invalido!\n");
		printf("Escreva como o código a seguir\n");
		printf("$./ola_usuario2 Nome Idade\n");
		printf("Exemplo: \n");
		printf("$./ola_usuario2 Jucelino 24\n");
		exit(1);
	}
	
	if((fp = fopen(argv[1],"w")) == NULL)
	{
		printf("Erro na abertura do arquivo\n");
		exit(2);
	}
	fprintf(fp,"%s\n",argv[1]);
	fprintf(fp,"%s\n",argv[2]);
	fclose(fp);
	
	return 0;
}

Questão 4. 

#include <stdio.h>
#include <stdlib.h>

int tam_arq_texto(char *nome_arquivo)
{
	FILE *fp;
	int tam = 0;
	char aux;

	if((fp = fopen(nome_arquivo,"r")) == NULL)
	{
		printf("Não foi possível ler o arquivo!\n");
		printf("Digite o nome do arquivo logo apos chamar o programa!\n");
		printf("Exemplo:\n");
		printf("$ ./cat_falsificado ola.txt\n");
		exit(1);
	}
	
	while(!feof(fp))
	{
		aux = getc(fp);
		tam++;	
	}
	
	fclose(fp);	
	tam = tam;	

	return tam;
}

Questão 5.

void le_arq_texto(char *nome_arquivo, char *conteudo,int tam)
{
	FILE *fp;
	int i;
	
	if((fp = fopen(nome_arquivo,"r")) == NULL)
	{
		printf("Não foi possível ler o arquivo!\n");
		exit(1);
	}	
	
	fgets(conteudo, (tam-1), fp);
	
	fclose(fp);

}

Questão 6.

#include <stdio.h>
#include <stdlib.h>
#include "bib_arqs.h"


int main(int argc, char **argv)
{
	FILE *fp;
	int tam;

	tam = tam_arq_texto(argv[1]);

	char conteudo[tam];	
	
	le_arq_texto(argv[1],conteudo,tam); //cat falsificado
	printf("%s\n",conteudo);
	
		
	return 0;
}

Questão 7.

