Para todas as questões, utilize as funções da norma POSIX (`open()`, `close()`, `write()`, `read()` e `lseek()`). Compile os códigos com o gcc e execute-os via terminal.

1. Crie um código em C para escrever "Ola mundo!" em um arquivo chamado 'ola_mundo.txt'.

#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>	// Para a funcao open()
#include <unistd.h>	// Para a funcao close()

int main( int argc, char **argv)
{
	int fp,i;
	//char string[100] = "Ola Mundo !\n";
	fp = open("ola_mundo.txt", O_RDWR | O_CREAT, S_IRWXU); //S_IRWXU para dar permissões de leitura e escrita ao arquivo criado
	if(fp==-1)
	{
		printf("Erro na abertura do arquivo.\n");
		exit(-1);
	}
	
	//for(i = 0; string[i] ; i++)
	//	write(fp, &(string[i]), 1); //grava caracter a caracter, sendo que cada caracter possui 1 byte
	
	write(fp, "Ola Mundo cruel!\n", 17);	
	close(fp);
	return 0;
}

2. Crie um código em C que pergunta ao usuário seu nome e sua idade, e escreve este conteúdo em um arquivo com o seu nome e extensão '.txt'. Por exemplo, considerando que o código criado recebeu o nome de 'ola_usuario_1':

```bash
$ ./ola_usuario_1
$ Digite o seu nome: Eu
$ Digite a sua idade: 30
$ cat Eu.txt
$ Nome: Eu
$ Idade: 30 anos

#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>	// Para a funcao open()
#include <unistd.h>	// Para a funcao close()

int main(int argc, char **argv)
{
	char nome[100];
	int idade,i;
	int fp;
	printf("Digite seu nome:\n");
	gets(nome);
	printf("Digite sua idade:\n");
	scanf("%d",&idade);
	
	fp = open(nome, O_RDWR | O_CREAT, S_IRWXU);
	if(fp == -1)
	{
		printf("Impossivel abrir arquivo!\n");
		exit(-1);
	}
	write(fp, "Nome: ", 6);
	for(i = 0; nome [i]; i++)
		write(fp, &(nome[i]), 1);
	write(fp, "\n", 1);

	write(fp,"Idade: ", 7);
	write(fp, &idade, sizeof(int));
	write(fp, " anos\n", 6);
	
	close(fp);
	return 0;	
	

}


3. Crie um código em C que recebe o nome do usuário e e sua idade como argumentos de entrada (usando as variáveis `argc` e `*argv[]`), e escreve este conteúdo em um arquivo com o seu nome e extensão '.txt'. Por exemplo, considerando que o código criado recebeu o nome de 'ola_usuario_2':

```bash
$ ./ola_usuario_2 Eu 30
$ cat Eu.txt
$ Nome: Eu
$ Idade: 30 anos

#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>	// Para a funcao open()
#include <unistd.h>	// Para a funcao close()


int main(int argc, char **argv)
{
	int fp;	
	int i;

	if (argc < 2) 
	{
		printf("Argumento Invalido!\n");
		printf("Escreva como o código a seguir\n");
		printf("$./out Nome Idade\n");
		printf("Exemplo: \n");
		printf("$./out Jucelino 24\n");
		exit(1);
	}
	
	fp = open(argv[1], O_RDWR | O_CREAT, S_IRWXU);
	if(fp == -1)
	{
		printf("Erro na abertura do arquivo\n");
		exit(2);
	}

	write(fp, "Nome: ", 6);
	for(i = 0; argv[1][i]; i++)
		write(fp, &(argv[1][i]), 1);
	write(fp, "\n", 1);

	write(fp,"Idade: ", 7);
	for(i = 0; argv[2][i]; i++)
		write(fp, &(argv[2][i]), 1);
	write(fp, " anos\n", 6);
	
	close(fp);
	
	return 0;
}


4. Crie uma função que retorna o tamanho de um arquivo, usando o seguinte protótipo: `int tam_arq_texto(char *nome_arquivo);` Salve esta função em um arquivo separado chamado 'bib_arqs.c'. Salve o protótipo em um arquivo chamado 'bib_arqs.h'. Compile 'bib_arqs.c' para gerar o objeto 'bib_arqs.o'.

Função para tamanho do arquivo

#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>	// Para a funcao open()
#include <unistd.h>	// Para a funcao close()

int tam_arq_texto(char *nome_arquivo)
{
	int fp;
	int tam = 0;
	char aux;

	fp = open(nome_arquivo, O_RDONLY);
	if(fp == -1)
	{
		printf("Não foi possível ler o arquivo!\n");
		printf("Digite o nome do arquivo logo apos chamar o programa!\n");
		printf("Exemplo:\n");
		printf("$ ./cat_falsificado ola.txt\n");
		exit(1);
	}
	
	while(read(fp, &aux, 1) != 0)
		tam++;	
	
	close(fp);	

	return tam;
}


5. Crie uma função que lê o conteúdo de um arquivo-texto e o guarda em uma string, usando o seguinte protótipo: `void le_arq_texto(char *nome_arquivo, char *conteúdo);` Repare que o conteúdo do arquivo é armazenado no vetor `conteudo[]`. Ou seja, ele é passado por referência. Salve esta função no mesmo arquivo da questão 4, chamado 'bib_arqs.c'. Salve o protótipo no arquivo 'bib_arqs.h'. Compile 'bib_arqs.c' novamente para gerar o objeto 'bib_arqs.o'.

void le_arq_texto(char *nome_arquivo, char *conteudo,int tam)
{
	int fp;
	char aux;
	int i = 0;
	
	fp = open(nome_arquivo, O_RDONLY);
	if(fp == 0)
	{
		printf("Não foi possível ler o arquivo!\n");
		exit(1);
	}	
	while(read(fp, &aux, 1) != 0)
	{
		conteudo[i] = aux;
		i++;
	}
	
	close(fp);

}


6. Crie um código em C que copia a funcionalidade básica do comando `cat`: escrever o conteúdo de um arquivo-texto no terminal. Reaproveite as funções já criadas nas questões anteriores. Por exemplo, considerando que o código criado recebeu o nome de 'cat_falsificado':

```bash
$ echo Ola mundo cruel! Ola universo ingrato! > ola.txt
$ ./cat_falsificado ola.txt
$ Ola mundo cruel! Ola universo ingrato!

#include <stdio.h>
#include <stdlib.h>
#include "bib_arq.h"


int main(int argc, char **argv)
{
	int fp;
	int tam;

	tam = tam_arq_texto(argv[1]);

	char conteudo[tam];	
	
	le_arq_texto(argv[1],conteudo,tam); //cat falsificado
	printf("%s\n",conteudo);
	
		
	return 0;
}

7. Crie um código em C que conta a ocorrência de uma palavra-chave em um arquivo-texto, e escreve o resultado no terminal. Reaproveite as funções já criadas nas questões anteriores. Por exemplo, considerando que o código criado recebeu o nome de 'busca_e_conta':

```bash
$ echo Ola mundo cruel! Ola universo ingrato! > ola.txt
$ ./busca_e_conta Ola ola.txt
$ 'Ola' ocorre 2 vezes no arquivo 'ola.txt'.
```
