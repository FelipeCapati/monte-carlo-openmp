# Análise da Integral Numérica de Monte Carlo #

### Abstract ###

###### This project aims to introduce the Monte Carlo mathematical method, the integral calculation using the same and one of the High Performance Computing (HPC) techniques aimed at Symmetric Multiprocessing (SMP), along with a validation methodology that analyzes the time of processing required for calculating the integral applied in a prototyped model using Python with pythran.  ######

Keywords — Monte Carlo Integration, Monte Carlo Analysis, Python, pythran, OpenMP, HPC, SMP.

## I.	 INTRODUÇÃO ##
Este projeto tem como objetivo introduzir o método matemático de Monte Carlo, o cálculo da 
integral utilizando o mesmo e uma das técnicas de High Performance Computing (HPC) voltada a 
Symmetric Multiprocessing (SMP), juntamente com uma metodologia de validação que analisa o 
tempo de processamento necessário para o cálculo da integral aplicada em um modelo prototipado 
utilizando Python com pythran. 

## II.	FUNDAMENTAÇÃO TEÓRICA ##

### A.	Monte Carlo ###
O algoritmo de Monte Carlo é um método numérico utilizado para solucionar problemas 
matemáticos de difícil solução em uma gama diversa de áreas do conhecimento indo de 
física atômica a métodos financeiros, probabilísticos e cálculo de integral numérica. 
Em contrapartida a robustez do algoritmo, tem-se seu custo computacional lento 
[O(N-1/2)] [1].

### B.	Integral de Monte Carlo ###
De acordo com [1], temos que a integral de uma função pode ser expressa como a média da 
função expectativa / avaliação em local aleatório. Simplificando o sistema e considerando 
uma integral unidimensional, temos:

![Alt text](images/func_01.png?)

Seja x uma variável uniformemente distribuída em um intervalo unitário.

![Alt text](images/func_02.png?)

A equação da quadratura de Monte Carlo é baseada na probabilidade de uma variável distribuída 
uniformemente coincidir com a área sob o gráfico ou não, na qual para uma distribuição normal 
de N variáveis em um array {xn} podemos explicitar como: 

![Alt text](images/func_03.png?)

Na qual para um número de interações infinitas, temos:

![Alt text](images/func_04.png?)

Com base na equação (4) podemos inferir que para um número infinito de interações a integral de 
Monte Carlo converge. Na qual temos a função de erro e erro médio quadrático (RMSE), respectivamente:

![Alt text](images/func_05_e_06.png?)

Aplicando o Central Limit Theorem (CLT) [2] citado em [1] na qual descreve o tamanho e as propriedades 
estatísticas dos erros de integração de Monte Carlo, pode-se escrever o erro como:

![Alt text](images/func_07.png?)

Similar ao cálculo da integral unidimensional, é possível fazer o cálculo da integral de volume partindo 
do mesmo princípio, com distinções que terá mais limites de integração (x, y, z) e que o ponto tem que 
estar contido dentro do espaço determinado pela função, na qual podemos simplificar como:

![Alt text](images/func_08.png?)

### C.	OpenMP ###
O OpenMP é uma padrão criado para desenvolvimento de aplicações que necessitam de multiprocessamento 
(processamento paralelo) para solução de problemas matemáticos desenvolvidos em C, C++ ou Fortran.<br>
Esse padrão foi desenvolvido pelo OpenMP Architecture Review Board (ARB) [3] na metade da década de 90 
para unificar diversas arquiteturas SMP (Symmetric Multiprocessing).<br>
O OpenMP não é uma linguagem de programação [3], ele é uma notação que pode ser adicionada a um programa 
sequencial no Fortran, C ou C++ para descrever como os trabalhos devem ser compartilhados entre os threads 
que serão executados em diferentes processadores ou núcleos. Fortemente utilizado devida a especialidade 
em programação paralela estruturada de forma muito simples com a capacidade de ser executada em plataformas 
distintas.<br>
Hoje existe a possibilidade de usar OpenMP utilizando outras linguagens de programação, tais como Java [4] 
e Python [5]. Neste projeto será utilizado Python juntamente com pythran. 

## III.	METODOLOGIA ##

Foi utilizado o Python (Jupyter), juntamente com o pythran e uma máquina física com 4 núcleos e 8 processadores 
lógicos para prototipar o modelo, na qual a função que calcula a integral utiliza de um gerador aleatório 
responsável por gerar N pontos distribuídos uniformemente sobre os limites de integração. A seguir tem-se um 
pseudocódigo da modelagem. 

![Alt text](images/pseudo_codigo.png?)

Para exemplificação da integral de Monte Carlo, foi calculada a integral (9), na qual (9) é uma integral de 
volume definida de um toroide e seus resultados serão discutidos melhor em IV. 

![Alt text](images/func_09.png?)

## IV. RESULTADOS ##

Baseando-se na metodologia proposta em III foram gerados os gráficos a seguir que dizem respeito ao cálculo 
da integral, ao tempo de processamento necessário dada uma quantidade N de iterações e ao ganho de relativo 
ao tempo de processamento quando utiliza-se OpenMP: 

![Alt text](images/graph_01.png?)

O gráfico 3D a seguir diz respeitos a figura formada pelos pontos utilizados para o cálculo da integral de 
Monte Carlo para a função (9): 

![Alt text](images/graph_02.png?)

Utilizando uma função do Python chamada de timeit é possível medir e mensurar aproximadamente o tempo de 
processamento gasto para executar a função e qual a relação do loop com o tempo gasto. Foi criada uma função 
utilizando o OpenMP e outra sem utilizar, na qual, obteve-se as seguintes equações de tempo em ms, na qual n 
representa o número de loops que a função executará:

![Alt text](images/func_10.png?)

## V. CONCLUSÃO ##

Dado os resultados vistos em IV podemos inferir que o Método de Integração de Monte Carlo é funcional, converge 
ao valor real de (9) com cerca 30.000 iterações (podendo variar em função da função analisada) e que o tempo de 
processamento tem um comportamento crescente proporcional a N tanto para o cálculo da integral utilizando OpenMP, 
quanto para integral sem o OpenMP.<br>
O OpenMP proporcionou um aumento significativo para o tempo de processamento (12x) quando utiliza-se 4 núcles e 8 
processadores lógicos, sendo que é possível escalar esse valor em função do hardware utilizado. 

## VI. AGRADECIMENTOS ##

Agradecimentos especiais a CAPES e ao Centro Universitário FEI por financiar o mestrado que está em curso; 
ao professor Reinaldo Bianchi por proporcionar visões sobre o mundo acadêmico e orientar trabalhos científicos 
com o objetivo de lapidar os conhecimentos abordados em sala; aos meus pais e a minha família que sempre me 
apoiaram em meio a dificuldades.

## VII. REFERÊNCIAS ##

[1] R. E. Caflisch, “Monte Carlo and quasi-Monte Carlo methods” Mathematics Department, UCLA, Los Angeles, CA, USA, 1998.<br> 
[2] W. Fellen, An Introduction to Probability Theory and its Application, vol. 1. Wiley, 1971.<br>
[3] B. Chapman, R. V. D. Pass, Using OpenMP: portable shared memory parallel programming, Editora Cambridge, Mass. 2008<br> 
[4] P. Belohlavek, J. A. Steinhauser, OMP4J, http://www.omp4j.org/, acessado em 15/09/2019<br>
[5] S. Guelton, et al, Pythran, https://pythran.readthedocs.io/en/latest/ acessado em 15/09/2019<br>
[6] S. S. Paille, Pythran Tutorial, https://serge-sans-paille.github.io/pythran-stories/pythran-tutorial.html
 
## VIII. APÊNDICE ##

### A. Comandos para instalar o Pythran ###
```
pip install pythran
```
Mais detalhes pode-se consultar o link do Paille https://serge-sans-paille.github.io/pythran-stories/pythran-tutorial.html
na qual tem-se um projeto que foi utilizado como base para o desenvolvimento desse.