# Exercícios para prova 2
- Temas:
	- Grafos e algoritmos: DFS, BFS, Dijkstra, Kosaraju, Karger
	- Algoritmos gulosos: Frog hopping, Activity Selection, Prim, Kruskal
	- Programação dinâmica: Bellman Ford, Floyd Warshall, Longest Common Subsequence, Knapsack, Maximal Independent Set

## Grafos e algoritmos
### Problema 1
O quadrado de um grafo $G = (V, E)$ é o grafo $G^2 = (V, E^2)$ tal que $(u,v ) \in E^2$ se existe um caminho de no máximo 2 arestas de $u$ para $v$ em $G$. Apresente um algoritmo eficiente para calcular $G^2$ a partir da lista adjacências de $G$. Analise o tempo computacional.

### Problema 2
Existem dois tipos de lutadores, os "molengas" e os "durões". Entre cada par de lutadores, pode existir uma rivalidade ou não. Suponha que nós temos uma lista de $n$ lutadores e uma lista de $r$ rivalidades. Apresente um algoritmo $O(n + r)$ se é possível separar os lutadores em dois grupos (molegas e durões) de tal forma que só existe rivalidade entre grupos diferentes (molenga vs durão). Se for possível dividir em dois grupos, o seu algoritmo deve apresentar a divisão.

### Problema 3
Suponha que temos um grafo em que as arestas tem pesos com valores naturais dentro do intervalo $[1, |V|]$. Quão eficiente o algoritmo Kruskal consegue obter a *minimum spanning tree* com essas arestas? E se os pesos estiverem dentro do intervalo $[1, W], W \in \mathbb{N}$?

### Problema 4
Suponha que nós temos a *minimum spanning tree* computada do grafo $G$. Adicionamos um novo vértice a $G$ e algoumas arestas (saindo do novo vértice). Apresente um algoritmo para atualizar a *minimum spanning tree* e apresente seu tempo computacional.

## Algoritmos gulosos
### Problema 5
Suponha que nós temos $n$ aulas (que possuem um horário de íncio e de término), e que precisamos alocar essas atividades em salas. Queremos alocar todas as atividades para alguma sala, mas queremos usar o mínimo possível de salas (sem fazer com que duas aulas ocorram na mesma sala no mesmo horário). Apresente um algoritmo guloso que encontra o alocamento ótimo.

### Problema 6
Nós temos uma lista de $n$ números reais $\{x_1, \dots, x_n\}$. Apresente um algoritmo guloso que encontrará o menor número de intervalos de tamanho unitário $[a_i, b_i], b_i - a_i = 1$, tal que todo ponto está dentro de um intervalo.

## Programação dinâmica

### Problema 7
Com uma lista de números $L$, encontre a maior sequência de números em ordem crescente (por exemplo, na lista $[1, 2, -4, 0.4, 0.5, 1, 10, 0]$,  desejamos encontrar $[0.4, 0.5, 1, 10]$). Apresente um algoritmo $O(n^2)$ (utilizando programação dinâmica).

## Problema 8
Considere o problema de imprimir um texto justificado em uma página com uma fonte *monospace* (todos os caracteres tem a mesma largura). Nós temos $n$ palavras que serão impressas, cada uma com $(l_i)|_i = 1^n$ caracteres.  Observe que se uma linha contém as palavras de $i$ até $j$, então o espaço usado nessa linha é $j - i + \sum_{k= i}^j l_k$. Considerando que em uma linha cabe no máximo $M$ caracteres, então o espaço sobrando na linha é $M - j + i - \sum_{k= i}^j l_k$.  Apresente um algoritmo que encontra o posicionamento ótimo de palavras em cada linha, de modo a minimizar o cubo do espaço sobrando em cada linha  $(M - j + i - \sum_{k= i}^j l_k)^3$.