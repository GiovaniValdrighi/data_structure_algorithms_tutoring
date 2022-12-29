# Lista de exercícios para prova 1

## Questão 1
Utilizando o método da substituição, mostre que:
- A solução de $T(n) = T(n - 1) + n$ é $O(n^2)$.
- A solução de $T(n) = T(\lceil n/2 \rceil) + 1$ é $O(\log n)$

## Solução 1
Para o primeiro item fazemos as substituições:
$$T(n) =  T(n-1) + n = T(n -2) + 2n = \dots = T(n - (n)) + n\cdot n$$
$$T(n) = T(0) + n^2 = n^2 $$

Para o segundo item:
$$T(n) = T(\lceil n/2 \rceil) + 1 = T(\lceil (\lceil n/2 \rceil))/2\rceil) + 2 = \cdots $$
Isto é, recursivamente vamos dividindo por 2 e pegando o "teto". Suponha sem perda de generalidade que $n$ é potência de 2, $n = 2^k$, (podemos remover todos os "tetos"):

$$T(n) = T(n/2) + 1 = T (n/4) + 2 = T(n/2^k) + k = T(1) + k $$
Temos que $k$ é $O(log n)$.


## Questão 2
Tem-se que a solução de $T(n) = 2T(\lfloor n/2\rfloor) + n$ é $O(n \log n)$. Mostre que essa recorrência também é $\Omega (n \log n)$ e conclua que ela é $\Theta (n \log n)$.

## Solução 2

Temos:

$$T(n) = 2T(\lfloor n/2 \rfloor ) + n$$
Assuma que exista $c$ tal que $T(\lfloor n/2 \rfloor) \geq c \lfloor n/2 \rfloor \log \left ( \lfloor n/2 \rfloor \right )$, subtituimos:

$$T(n) = 2T(\lfloor n/2 \rfloor ) + n \geq 2 \left(  c \lfloor n/2 \rfloor \log \left (\lfloor n/2 \rfloor \right ) \right ) + n = $$
$$ = 2  \lfloor n/2 \rfloor c  \log \left (\lfloor n/2 \rfloor \right ) + n \geq c (n - 1) \log ((n- 1)/2) + n =$$
Note a transformação que fizemos de $\lfloor n/2 \rfloor$ para $(n - 1)$ para a desigualdade valer.
$$ = c (n-1) (\log (n - 1)  + 1) + n = $$
$$ = c(n - 1)\log (n -1) + c(n - 1) + n  = $$
Note que o primeiro termo é suficiente para dizermos que $O(n\log n)$ pois podemos desconsiderar as constantes e os termos de grau menor.

## Questão 3
Use o método de recursão em árvore para encontrar uma intuição sobre a solução de $T(n) = 2T(n -1) + 1$ e depois use o método da substituição para provar sua resposta.

## Solução 3

Primeiro, vemos que a "entrada" vai diminuindo de 1 em 1, isto é, de $n$ para $n-1$, logo, para chegar a $T(0)$ teremos $n$ níveis. Depois, em cada nível dobramos o número de problemas e cada um tem o peso $1$, logo, teremos algo assim:

$$T(n) = (1 + 2 + 2^2 + \cdots + 2^n)$$
Cada parcela é o total de custo de um nível, e temos um total de $n$ níveis.

$$T(n) = 2^{n+1} - 1$$
Vamos provar com o método da substituição, supomos que $T(n -1) \leq 2^n - 1$:

$$T(n) = 2T(n - 1) + 1 \leq 2 (2^n - 1) + 1 = 2^{n+1} - 1$$
Exatamente como esperávamos.


## Questão 4

Um professor tem $n$ chips que são supostamente idênticos e são capazes de testar uns aos outros. O aparelho de testes é capaz de testar dois chips ao mesmo tempo. Quando o teste é realizado, cada chip diz se o outro é "bom" ou "ruim". Um chip bom sempre responde corretamente se o outro chip é bom ou ruim, mas um chip ruim nem sempre responde corretamente. Existem quatro situações possíveis:


| Chip A diz | Chip B diz | Conclusão |
| ---------- | ---------- | ------------ |
| B é bom | A é bom | Ambos são bons ou ambos são ruims |
| B é bom | A é ruim | Pelo menos um é ruim |
| B é ruim | A é bom | Pelo menos um é ruim |
| B é ruim | A é ruim | Pelo menos um é ruim |

a) Mostre que se mais de $n/2$ chips são ruins, o professor não é capaz de encontrar o chips bons usando qualquer estratégia (baseada nas comparações de dois chips). Assuma que os chips ruins podem se "esforçar" para enganar.

b) Considere o problema de encontrar um chip bom entre $n$ chips, assumindo que mais de $n/2$ chips são bons. Mostre que $\lfloor n/2 \rfloor$ testes são suficientes para reduzir o problema a um de metade do tamanho.

c) Mostre que chips bons podem ser identificados com $\Theta (n)$ testes, assumindo que mais de $n/2$ chips são bons. Apresente a resolva a recorrência que define o número de testes necessários.

## Solução 4

a) Suponhamos que separamos os chips em pares e realizamos o teste com cada um deles.  No pior dos casos teremos um chip ruim em cada par, e no pior dos casos, o chip ruim sempre vai dizer que o ruim é bom e que o bom é ruim, sem informação para reduzir o problema.

b) Temos mais chips bons do que chips ruins. A ideia para resolver esse problema será gerar problemas "menores" que mantém essa propriedade, até restar com 2 chips ou 1 chip (assim encontraremos um bom). Fazemos:

- Separamos os chips em pares e deixamos um restando caso necessário.
- Executamos os testes. Em cada teste:
	- Se pelo menos um chip diz que o outro é ruim, jogamos fora os dois chips.
	- Se os dois chips dizem que o outro é bom, jogamos um dos dois fora.
- Repetimos isso recursivamente com os chips que restam.

Note que quando jogamos os dois chips fora, estamos jogando ou 2 ruins ou 1 ruim e 1 bom, isso não faz com que haja mais chips ruins do que bons nos restantes.

Nos outros pares, ou os dois são bons ou os dois são ruins, ao jogarmos um chip de cada, reduzimos os números de chips bons e ruins pela metade, sem inverter a proporção.

Chegaremos a uma situação com $2$ ou $1$ chip:

- Se tivermos $2$ chips, realizamos o teste. Se ambos disserem que o outro chip é bom, então temos que ambos os chips são bons. Se um diz que o outro é ruim, é porque ainda existe um ruim entre esse par, e o chip que reservamos no começo é bom.
- Se tivermos $1$ chip, ele é bom.

c) Para encontrar todos os chips bons, encontramos um chip bom usando o algoritmo acima e depois testamos todos os outros chips (que vai ter custo $n$). O algoritmo acima possui a seguinte recursão:

$$T(n) = T(\lfloor n/2 \rfloor) + \lfloor n/2 \rfloor$$
Podemos resolver com o teorema master $T(n) = \Theta (n)$, logo, o algoritmo total $T(n)  = \Theta (n)$.

## Questão 5
Suponha que as partições em todos os níveis em um quicksort são na proporção $1 - \alpha$ para $\alpha$ com $0 < \alpha \leq 1/2$ uma constante. Mostre que a profundidade mínima de uma folha na árvore de recursão é aproximadamente $- \log n / log \alpha$ e a profundidade máxima é aproximadamente $- \log n / \log (1 - \alpha)$.

## Solução 5

Temos que $\alpha \leq 1 - \alpha$, e o menor "caminho" sempre será na partição de proporção $\alpha$. Na primeira partição, obtemos um vetor de tamanho $n \alpha$, na segunda, temos $n \alpha^2$, e isso vai recursivamente até obtivermos $n\alpha^k = 1$, em que o quick-sort para a subdivisão e resolve o caso base. $k$ é o total de níveis que será necessário "descer" na árvore de recursão, logo podemos isolar:

$$n\alpha^k = 1 \implies k \log \alpha = - \log n \implies k = \dfrac{- \log n}{\log \alpha}$$
Para o pior "caso" possível (maior profundidade), é nas recursivas partições de tamanho $(1 - \alpha)$, pois iremos levar mais iterações para tal que $n (1 - \alpha)^k = 1$. Isolando da mesma forma temos:

$$k = \dfrac{-\log n}{\log (1 - \alpha)}$$

## Questão 6
Você tem uma tabela de hash de tamanho $m$ na qual você insere $n$ chaves usando encadeamento" (separate chaining). As chaves são inteiros selecionados do conjunto $U = \{1, 2, \dots , nm\}$.

a) Prove que, não importa quão engenhosamente você projete sua função hash, deve existir um subconjunto $S$ de $U$ de tamanho pelo menos $n$ tal que cada chave em $S$ mapeie para a mesma localização na tabela de hash.

b) O que o item anterior implica sobre o tempo de execução do pior caso necessário para inserir $n$ chaves extraídas de $U$ em sua tabela de hash?

## Solução 6

a) Ao distribuirmos as $nm$ keys ao longo das $m$ entradas da tabela hash, temos que ao menos uma das entradas deve conter ao menos $n$ keys. Ao tomar qualquer entrada da tabela de tal modo, alcançamos que o subset de keys $S$ que mapeia para a mesma entrada da tabela de hash, tem tamanho pelo menos $n$.

b) No pior caso, teríamos a inserção de todos os $n$ levados a uma mesma posição da hash, criando uma lista de tamanho $n$. Como vamos chamar uma inserção $n$ vezes, e na \textit{linked-list}, a inserção é $O(n)$, o tempo para inserir os $n$ nós será $O(n^2)$.


