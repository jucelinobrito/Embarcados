1. Considerando a biblioteca-padrão da linguagem C, responda:

(a) Quais são as funções (e seus protótipos) para abrir e fechar arquivos?

	FILE *(nome_do_ponteiro_para_o_arquivo);
	nome_do_ponteiro_para_o_arquivo = fopen("nome_do_arquivo.txt","r,w,rb,wb");
	fclose(nome_do_ponteiro_para_o_arquivo);
	
Exemplo:
	FILE *fp;
	fp = fopen("nome_do_arquivo.txt","w");
	fclose(fp);


(b) Quais são as funções (e seus protótipos) para escrever em arquivos?

	int putc (char ch, FILE *fp); 
	Exemplo: for (i=0;string[i];i++) 
		 putc(string[i], fp); 
		 putc('\n', fp); //Grava caracter por caracter -> Lembrar que \0 em ASCII = 0
	

	char fputs (char *str, FILE *fp); 
	Exemplo: putc(string,fp); //Grava um bloco de string completo em um arquivo.

	unsigned fwrite (void *buffer, int numero_de_bytes, int count, FILE *fp);
	Exemplo: fwrite(&pi, sizeof(float), 1, fp);

	int fprintf (FILE *stream, const char *format, ...);
	Exemplo: fprintf(fp,"Este e um arquivo chamado: \n%s\n",str);


(c) Quais são as funções (e seus protótipos) para ler arquivos?

	int getc (FILE *fp);
	Exemplo: while((c = getc(fp)) != EOF
		 printf("%c", c);

	char fgets (char *str, int tamanho, FILE *fp);
	Exemplo: char frase[80];
		 fgets(frase, 79, fp);

	unsigned fread (void *buffer, int numero_de_bytes, int count, FILE *fp);
	Exemplo: fread(&pilido, sizeof(float), 1, fp);

	int fscanf (FILE *stream, const char *format, ...);
	Exemplo: fscanf(fp,"%c",&c); 
	

(d) Quais são as funções (e seus protótipos) para reposicionar um ponteiro para arquivo?

	int fseek (FILE *stream, long int offset, int origin); -> reposiciona o ponteiro do arquivo
	
	void rewind (FILE *stream); -> volta o ponteiro do arquivo para o ínicio. 

	
(e) Quais bibliotecas devem ser incluídas no código para poder utilizar as funções acima?

	<stdlib.h> e <stdio.h>

2. O que é a norma POSIX?

	POSIX (um acrônimo para: Portable Operating System Interface, que pode ser traduzido como Interface Portável entre Sistemas Operacionais) é 		uma família de normas definidas pelo IEEE para a manutenção de compatibilidade entre sistemas operacionais, e designada formalmente por IEEE 		1003. POSIX define a interface de programação de aplicações (API), juntamente com shells de linha e comando e interfaces utilitárias, para 		compatibilidade de software com variantes de Unix e outros sistemas operacionais.

	Tem como objetivo garantir a portabilidade do código-fonte de um programa a partir de um sistema operacional que atenda as normas POSIX para 		outro sistema POSIX, desta forma as regras atuam como uma interface entre sistemas operacionais distintos, enfim, de modo coloquial "programar 		somente uma vez, com implementação em qualquer sistema operacional".

3. Considerando a norma POSIX, responda:

(a) Quais são as funções (e seus protótipos) para abrir e fechar arquivos?

	int fp;
	fp = open ("caminho ou nome do arquivo", flag de abertura);
	Exemplo:
	fp = open ("/tmp/teste.txt", O_WRONLY)
	Exemplos de flags de abertura:
	O_RDONLY - ABRIR SOMENTE PARA LEITURA
	O_WRONLY - ABRIR SOMENTE PARA ESCRITA
	O_RDWR - ABRIR PARA LEITURA E ESCRITA
	O_APPEND - ANEXAR AO FINAL DO ARQUIVO
	O_CREAT - CRIAR SE O ARQUIVO NÃO EXISTIR

	DEVEM SER COMBINADOS COM "OR":
	
	Exemplo: 
	int fd;
	fd = open("/tmp/teste.txt", O_RDWR | O_CREAT);

	Para fechar o arquivo:
	close(descritor do arquivo);
	Exemplo:
	close(fp);
		

(b) Quais são as funções (e seus protótipos) para escrever em arquivos?
	
	write("descritor de arquivo(integer)", endereço do buffer, numero 		de bytes a serem escritos);
	
	Exemplo:
	for(i=0; string[i]; i++)
		write(fp, &(string[i]), 1); // Grava a string, caractere a caractere	
	write(fp, "\n", 1);	

(c) Quais são as funções (e seus protótipos) para ler arquivos?

	read(descritor do arquivo(integer), endereço do buffer, numerdo de 		bytes a serem lidos);

	Exemplo:
	char c;
	while(read(fp, &c, 1) != 0)
		printf("%c", c);


(d) Quais são as funções (e seus protótipos) para reposicionar um ponteiro para arquivo?

	lseek(descritor do arquivo(integer), offset, seek_set,seek_cur, 	seek_end);

	Exemplo:
	O arquivo teste.txt contém o texto "Hello World"

	int fd;
	char c;
	fd = open("/tmp/teste.txt", O_RDONLY);
	lseek(fd, 6, SEEK_SET);
	read(fd, &c, 1);

	Será gravado o caracter "espaço" na variavel c	
	

(e) Quais bibliotecas devem ser incluídas no código para poder utilizar as funções acima?

	#include <stdio.h>	// Para a funcao printf()
	#include <fcntl.h>	// Para a funcao open()
	#include <unistd.h>	// Para a funcao close()
	#include <stdlib.h>	// Para a função exit()

