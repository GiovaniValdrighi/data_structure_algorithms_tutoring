# Exercícios para prova 2 soluções
- Temas:
	- Grafos e algoritmos: DFS, BFS, Dijkstra, Kosaraju, Karger
	- Algoritmos gulosos: Frog hopping, Activity Selection, Prim, Kruskal
	- Programação dinâmica: Bellman Ford, Floyd Warshall, Longest Common Subsequence, Knapsack, Maximal Independent Set

## Grafos e algoritmos
### Problema 1
O quadrado de um grafo $G = (V, E)$ é o grafo $G^2 = (V, E^2)$ tal que $(u,v ) \in E^2$ se existe um caminho de no máximo 2 arestas de $u$ para $v$ em $G$. Apresente um algoritmo eficiente para calcular $G^2$ a partir da lista adjacências de $G$. Analise o tempo computacional.

### Solução 1
Se estivessemos tratando com uma matriz de adjacência, poderíamos fazer o quadrado da matriz ($A^2$), que teríamos todos as ligações de tamanho 2, depois precisariamos adicionar as ligações de caminho 1.

Com a lista de adjacência $L$, criamos uma cópia $L'$. Essa cópia contém todos os caminhos de tamanho $1$, agora precisamos adicionar os caminhos de tamanho $2$. Para cada vértice $u$, temos a sua lista de conexões. Para cada $v$ nessa lista de conexões, iteramos sobre a sua lista de conexões. Adicionamos todos os $w \in L[v]$ na lista $L'[u]$. Caso exista algum $w$ que é conectado a $u$, iremos adicionar elementos repetidos, então depois é necessário remover as arestas repetidas.

Dessa forma, para cada conexão $(u, v)$, precisaremos iterar sobre os vértices, logo o tempo computacional é $O(|E||V|)$.

### Problema 2
Existem dois tipos de lutadores, os "molengas" e os "durões". Entre cada par de lutadores, pode existir uma rivalidade ou não. Suponha que nós temos uma lista de $n$ lutadores e uma lista de $r$ rivalidades. Apresente um algoritmo $O(n + r)$ se é possível separar os lutadores em dois grupos (molegas e durões) de tal forma que só existe rivalidade entre grupos diferentes (molenga vs durão). Se for possível dividir em dois grupos, o seu algoritmo deve apresentar a divisão.

### Solução 2
Esse problema é uma ilustração do problema de coloração de um grafo com duas cores. Temos um grafo em que cada lutador é um vértices, e temos as arestas que são as rivalidades. Queremos pintar os lutadores das cores "molenga"/"durão" de tal forma que uma ligação só exista entre lutadores de cores diferentes.

O algoritmo para resolver esse problema usa breadth-first-search. Para cada componente conexa do grafo, escolhemos um vértice e executamos a breadth-first-search, os nós vão receber valores de acordo com o seu nível. Colorimos os níveis pares de "molenga" e os níveis impares de "durõe". Depois, precisamos verificar se a propriedade está valendo, iteramos sobre as arestas, e para cada par $(u, v)$, verificamos se as cores são diferentes.

O algoritmo de encontrar componentes conexas é $O(n + r)$, a breadth-first-search é também é $O(n +r )$  e a última etapa de verificação é $O(r)$, logo esse algoritmo é $O(n + r)$.

### Problema 3
Suponha que temos um grafo em que as arestas tem pesos com valores naturais dentro do intervalo $[1, |V|]$. Quão eficiente o algoritmo Kruskal consegue obter a *minimum spanning tree* com essas arestas? E se os pesos estiverem dentro do intervalo $[1, W], W \in \mathbb{N}$?

### Solução 3
O algoritmo de Kruskal cria um grafo vazio, e vai adicionando as arestas de menor peso até que encontre a *minimum spanning tree*. Dessa forma, precisamos da lista de arestas ordenada de acordo com os pesos, e nesse caso, como sabemos o valor máximo dos pesos (em ambos os casos $|V|$ ou $W$), podemos ordernar as arestas utilizando o *counting sort* ou o *radix sort* em tempo $O(|E|)$.  Dessa forma, o tempo total será $O(|E|)$.

### Problema 4
Suponha que nós temos a *minimum spanning tree* computada do grafo $G$. Adicionamos um novo vértice a $G$ e algoumas arestas (saindo do novo vértice). Apresente um algoritmo para atualizar a *minimum spanning tree* e apresente seu tempo computacional.

### Solução 4
Ao adicionarmos um novo nó $v$ que possui $k$ arestas, para obtermos de volta a *minimum spanning tree*, precisamos remover $k-1$ arestas, possui o vértice $v$ deve ter apenas $1$ ligação com o resto da estrutura. Iteramos pelas $k$ novas arestas adicionadas a partir da de menor peso, adicionamos a aresta na *minimum spanning tree*, e aplicamos DFS no nó adicionado para encontrar um ciclo. Após encontrar o primeiro ciclo, removemos a aresta de maior peso desse ciclo. Repetimos esse processo até não existir mais ciclos. Ao adicionamors $k$ arestas iremos criar $k-1$ ciclos, logo no final só adicionamos uma nova aresta a *minimum spanning tree*.

Esse algoritmo roda o DFS $k$ vezes, e em cada vez será $O(|V|)$.

## Algoritmos gulosos
### Problema 5
Suponha que nós temos $n$ aulas (que possuem um horário de íncio e de término), e que precisamos alocar essas atividades em salas. Queremos alocar todas as atividades para alguma sala, mas queremos usar o mínimo possível de salas (sem fazer com que duas aulas ocorram na mesma sala no mesmo horário). Apresente um algoritmo guloso que encontra o alocamento ótimo.

### Solução 5
Para fazer isso, criamos dois conjuntos, $L$ e $O$, que iremos atualizar iterativamente. Em dada iteração, $O$ será o conjunto de salas que estão ocupadas no atual momento e $L$ será o conjunto de salas livres que já foram ocupadas em algum momento.

Vamos iterando na lista $\{t_1, \dots, t_n\}$ de tempos de início de cada aula. Em cada iteração de tempo $t_i$, verificamos todas as salas da lista $O$, se alguma delas estã com uma aula que terminou antes de $t_i$, caso exista, adicionamos essa sala na lista $L$. Depois disso, veríficamos na lista $L$ se tem alguma sala vazia, caso tenha, adicionamos a atual aula nessa sala. Caso contrário, pegamos uma nova sala que nunca foi usada e colocamos essa aula. Em ambos os casos, a sala vai para a lista $O$.

Essa solução funciona pois caso exista um dado momento com $m$ aulas simultâneas, vamos utilizar $m$ salas, e em todos os outros momentos, iremos utilizar menos de $m$ aulas, na realidade, iremos sempre utilizar o mínimo necessário possível de salas.

### Problema 6
Nós temos uma lista de $n$ números reais $\{x_1, \dots, x_n\}$. Apresente um algoritmo guloso que encontrará o menor número de intervalos de tamanho unitário $[a_i, b_i], b_i - a_i = 1$, tal que todo ponto está dentro de um intervalo.

### Solução 6
Imagine que temos as soluções, considere o intervalo mais a "esquerda", o intervalo que possui o menor $a_i$. O valor menor valor $x$ deve estar dentro desse intervalo (caso ele não esteja, não tem nenhum outro valor no intervalo, então o intervalo seria "inútil" e não faria parte da solução ótima). Não faz sentido que $a_i < \min x$, pois esse "espaço" de intervalo mais a esquerda de $\min x$ não seria utilizado para cobrir nenhum outro valor, então se colocarmos $a_i = \min x$, existe maiores chances de outros valores $x$ estarem dentro de $[a_i, b_i]$. Logo, definimos um intervalo que começa com $\min x$, removemos todos os $x$ dentro desse intervalo da nossa lista de números, e repetimos o problema agora com uma lista de números reduzidas. Fazemos isso até que cubramos todos os valores.

## Programação dinâmica

### Problema 7
Com uma lista de números $L$, encontre a maior sequência de números em ordem crescente (por exemplo, na lista $[1, 2, -4, 0.4, 0.5, 1, 10, 0]$,  desejamos encontrar $[0.4, 0.5, 1, 10]$). Apresente um algoritmo $O(n^2)$ (utilizando programação dinâmica).

### Solução 7
Para fazer isso, podemos utilizar do algoritmo de encontrar a maior sequência comum em strings. Primeiro criamos uma cópia ordenada de $L$, vamos chamar de $L'$. Depois aplicamos o algoritmo LCS em $L$ e $L'$. A maior sequência encontrada será ordenada, pois ela pertence a $L'$ e ela também fara parte da lista original $L$. Esse algoritmo ordenada e depois aplica LCS, logo ele é $O(n^2)$.

### Problema 8
Considere o problema de imprimir um texto justificado em uma página com uma fonte *monospace* (todos os caracteres tem a mesma largura). Nós temos $n$ palavras que serão impressas, cada uma com $(l_i)|_i = 1^n$ caracteres.  Observe que se uma linha contém as palavras de $i$ até $j$, então o espaço usado nessa linha é $j - i + \sum_{k= i}^j l_k$. Considerando que em uma linha cabe no máximo $M$ caracteres, então o espaço sobrando na linha é $M - j + i - \sum_{k= i}^j l_k$.  Apresente um algoritmo que encontra o posicionamento ótimo de palavras em cada linha, de modo a minimizar o cubo do espaço sobrando em cada linha  $(M - j + i - \sum_{k= i}^j l_k)^3$.

### Solução 8
Precisamos primeiro encontrar a estrutura de sub-problemas. Note que se soubermos que a solução ótima possui $k$ palavras na primeira linha, então vamos lidar com o mesmo problema, só que dessa vez com as palavras de $l_k$ até $l_n$. Vamos criar duas tabelas, $C[k]$ vai armazenar o custo de escrever as palavras de $l_k$ até $l_n$. A solução estará em $C[1]$. $P[k]$ contém o índice da palavra que vai estar na última posição da primeira linha quando consideramos as letras de $l_k$ até $l_n$. $P$ vai ser usado para reconstruirmos a solução, por exemplo, $P[1]$ vai nos dizer qual é a palavra que vai estar no final da primeira linha (aí saberemos todas as palavras dessa linha).

Algoritmo:
```
C = array tamanho n
P = array tamanho n

para k de n até 1:
	se $\sum_{i =k}^n l_i + n - k < M$
		$C[k] = 0$ 
	$cost = \infty$
	para j de 1 até n - k
		$subset\_cost = \sum_{m = 1}^j l_{k+j} + j - 1$
		se ($subset\_cost < M$) e ($(M - subset\_cost)^3 + C[k + j + 1] < cost$):
			$cost = (M - subset\_cost)^3  + C[k + j + 1]$
			$P[k] = k + j$
	$C[k] = cost$
```

Nós vamos resolvendo o problema adicionando as "últimas palavras", esse é o loop que vai de $k = n$ até $k = 1$. Depois internamente, primeiro verificamos se as palavras de $k$ até $n$ cabem em uma única linha (a soma dos caracteres é menor do que $M$). Depois, vamos aumentando as palavras de uma uma, de $k$ até $n$, isto é, consideramos o intervalo $k, k+1$, depois $k, k+2$, etc. Para cada um desses, verificamos se essas palavras cabem em uma única linha, e se elas couberem, verificamos se o custo de adicionar elas em uma única linha mais o custo de resolver as demais (de $k+j + 1$ até $n$) é menor do que o custo anterior. Caso seja, atualizamos o custo e a matriz $P$.
