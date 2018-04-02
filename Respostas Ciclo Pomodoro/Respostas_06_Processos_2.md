1. Crie um código em C para gerar três processos-filho usando o `fork()`.

#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

int main(int argc, char **argv())
{
	if (fork() != 0 ) //criou primeiro processo filho
	{	
		if (fork() != 0) //processo filho criou processo neto
		{
			if (fork() != 0) //processo neto criou processo bisneto
			{
				sleep(5);
			}
			else
				sleep(1);
		}
		else
			sleep(1);
	}
	else
		sleep(1);

	return 0;
}

2. Crie um código em C que recebe o nome de diversos comandos pelos argumentos de entrada (`argc` e `*argv[]`), e executa cada um sequencialmente usando `system()`. Por exemplo, considerando que o código criado recebeu o nome de 'serial_system', e que ele foi executado na pasta '/Sistemas_Embarcados/Code/06_Processos', que contem diversos arquivos:

```bash
$ ./serial_system pwd echo ls echo cal
$ ~/Sistemas_Embarcados/Code/06_Processos
$
$ Ex1.c    Ex2b.c   Ex4.c   Ex6.c
$ Ex2a.c   Ex3.c    Ex5.c   serial_system
$
$     Março 2017
$ Do Se Te Qu Qu Se Sá
$           1  2  3  4
$  5  6  7  8  9 10 11
$ 12 13 14 15 16 17 18
$ 19 20 21 22 23 24 25
$ 26 27 28 29 30 31
```

#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
	int i;
	int a;

	if(argc < 2)
	{
		printf("\nDigite  os comandos logo após a chamada do programa\n");
		exit(1);
	}
	for(i = 1; i <= argc; i++)
	{
		a = system(argv[i]);
	}

	return 0;
}


3. Crie um código em C que recebe o nome de diversos comandos pelos argumentos de entrada (`argc` e `*argv[]`), e executa cada um usando `fork()` e `exec()`.

#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

int main (int argc, char **argv)
{
	int i;
	char * args[] = {" ", NULL};
	if (argc < 2)
	{
		printf("Digite os comandos logo apos a chamada do programa\n");
		exit(1);
	}

	for (i = 1; i < argc; i++)
		if (fork() != 0) 
		{
			args[0] = argv[i];
			execvp(args[0], args);
			printf("Erro\n");
		}

	return 0;

}

4. Crie um código em C que gera três processos-filho usando o `fork()`, e que cada processo-filho chama a seguinte função uma vez:

```C
int v_global = 0; // Variavel global para este exemplo
void Incrementa_Variavel_Global(pid_t id_atual)
{
	v_global++;
	printf("ID do processo que executou esta funcao = %d\n", id_atual);
	printf("v_global = %d\n", v_global);
}
```

(Repare que a função `Incrementa_Variavel_Global()` recebe como entrada o ID do processo que a chamou.) Responda: a variável global `v_global` foi compartilhada por todos os processos-filho, ou cada processo enxergou um valor diferente para esta variável?

#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int v_global = 0; // Variavel global para este exemplo
void Incrementa_Variavel_Global(pid_t id_atual)
{
	v_global++;
	printf("ID do processo que executou esta funcao = %d\n", id_atual);
	printf("v_global = %d\n", v_global);
}

int main(void)
{
	if (fork() == 0) {
	/* Filho 01 */
	Incrementa_Variavel_Global(getpid());
		if (fork() == 0) {
		/* Filho 02 */
		Incrementa_Variavel_Global(getpid());
			if (fork() == 0) {
			/* Filho 03 */
			Incrementa_Variavel_Global(getpid());
			}
		}
	}

	wait(NULL);
	return 0;
}

A variável global foi compartilhada por todos os processos filhos

5. Repita a questão anterior, mas desta vez faça com que o processo-pai também chame a função `Incrementa_Variavel_Global()`. Responda: a variável global `v_global` foi compartilhada por todos os processos-filho e o processo-pai, ou cada processo enxergou um valor diferente para esta variável?

#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int v_global = 0; // Variavel global para este exemplo
void Incrementa_Variavel_Global(pid_t id_atual)
{
	v_global++;
	printf("ID do processo que executou esta funcao = %d\n", id_atual);
	printf("v_global = %d\n", v_global);
}

int main(void)
{
	printf("Processo pai: \n");
	Incrementa_Variavel_Global(getpid());
	printf("\n");	

	if (fork() == 0) {
	/* Filho 01 */
	Incrementa_Variavel_Global(getpid());
		if (fork() == 0) {
		/* Filho 02 */
		Incrementa_Variavel_Global(getpid());
			if (fork() == 0) {
			/* Filho 03 */
			Incrementa_Variavel_Global(getpid());
			}
		}
	}

	wait(NULL);
	return 0;
}

A variável global foi compartilhada por todos.
