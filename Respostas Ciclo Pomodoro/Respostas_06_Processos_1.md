1. Como se utiliza o comando `ps` para:

(a) Mostrar todos os processos rodando na máquina?

	$ ps -e 
        $ ps -ef
        $ ps -eF
        $ ps -ely


(b) Mostrar os processos de um usuário?

	$ ps -U "usuario"

(c) Ordenar todos os processos de acordo com o uso da CPU?

	$ ps -ef --sort pcpu

(d) Mostrar a quanto tempo cada processo está rodando?

	$ ps -ef --sort utime

2. De onde vem o nome `fork()`?

	"Fork" vem do inglês e significa "bifurcação"

3. Quais são as vantagens e desvantagens em utilizar:

(a) `system()`?

	Permite executar um comando dentro de um programa, criando um sub-processo.
	O uso do system() não é recomendado na maioria dos casos. É simples, mas dá
	brechas a falhas de execução pois depende muito do sistema.

(b) `fork()` e `exec()`?

	No Unix não há meio para que um processo crie outro somente mandando executá-lo diretamente.
	Não há função que crie e execute um novo processo em um único passo.
	Para isso utiliza-se a função fork() que cria uma cópia do processo atual e em seguida a função exec() que substitui o conteúdo do novo processo por um novo programa.
	fork() -> uma duplicata do processo é criada - processo filho
	Em seguida, tanto o processo pai quanto o processo filho continuam a executar normalmente a partir do fork().
	O processo filho tem um novo PID que pode ser verificado com o getpid(). Entretanto, a função fork() retorna valores distintos. O valor do retorno no processo pai é o PID do processo filho, ou seja, retorna um novo PID, já o valor do retorno do processo filho é zero.	
	

4. É possível utilizar o `exec()` sem executar o `fork()` antes?

	É possível, mas o processo original seria substituido pelo novo processo.  Pois a família de funções exec() substitui a imagem do processo atual por uma imagem de um novo processo.
	Quando um programa chama a função exec(), o processo cessa imediatamente a execução do programa corrente e passa a executar um novo programa do inicio.
	Como a função exec() substitui o programa em execução por outro, ela não retorna valor algum, exceto quando um erro ocorre.

5. Quais são as características básicas das seguintes funções:

	Existem seis primitivas na família, as quais podem ser divididas 		em dois grupos: os execl(), para o qual o número de argumentos do 		programa lançado é conhecido; e os execv(), para o qual esse 		número é desconhecido. Em outras palavras, estes grupos de 		primitivas se diferenciam pelo número de parâmetros passados.

	O parâmetro inicial destas funções é o caminho do arquivo a ser 	executado.

	As funções execv e execvp fornecem um vetor de ponteiros para 		strings não-nulas que representam a lista de argumentos para o 		programa executado.

	Para ambos os casos, assume-se, por convenção, que o primeiro 		argumento vai apontar para o arquivo associado ao nome do programa 		sendo executado. A lista de argumento deve ser terminada pelo 		ponteiro NULL.

	A função execle também especifica o ambiente do processo executado 		após o ponteiro NULL da lista de parâmetros ou o ponteiro para o 		vetor argv com um parâmetro adicional. Este parâmetro adicional é 		um vetor de ponteiros para strings não-nulas que deve também ser 		finalizado por um ponteiro NULL. As outras funções consideram o 	ambiente para o novo processo como sendo igual ao do processo 		atualmente em execução.

	L: lista de argumentos [execl(), execle() e execlp()]. Os 		argumentos que serão recebidos em argv são listados um a um como 		parâmetros da função em forma de string.

	V: vetor de argumentos [execv(), execve() e execvp()]. Os 		argumentos que serão recebidos em argv são passados em um vetor do 		tipo char* que já contém todas as strings previamente carregadas.

	E: variáveis de ambiente [execle() e execve()]. O último parâmetro 		destas funções é um vetor para strings (char *) que será recebido 		pelo novo programa no argumento envp contendo variáveis de 		ambiente pertinentes para sua execução. Para as versões sem a 		letra “e“, o ambiente é adquirido a partir de uma variável externa 		(extern char **environ) já declarada na biblioteca unistd.h.

	P: utilização da variável de ambiente PATH [execlp() e execvp()]. 		Esta função irá buscar a nova imagem do processo nos diretórios 	contidos na variável PATH. Para as versões sem a letra “p“, deverá 		ser passada uma string contendo o caminho completo para o arquivo executável.

