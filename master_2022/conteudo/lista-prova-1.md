# Lista de exercícios para prova 1

## Questão 1
Utilizando o método da substituição, mostre que:
- A solução de $T(n) = T(n - 1) + n$ é $O(n^2)$.
- A solução de $T(n) = T(\lceil n/2 \rceil) + 1$ é $O(\log n)$.

## Questão 2
Tem-se que a solução de $T(n) = 2T(\lfloor n/2\rfloor) + n$ é $O(n \log n)$. Mostre que essa recorrência também é $\Omega (n \log n)$ e conclua que ela é $\Theta (n \log n)$.

## Questão 3
Use o método de recursão em árvore para encontrar uma intuição sobre a solução de $T(n) = 2T(n -1) + 1$ e depois use o método da substituição para provar sua resposta.

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

## Questão 5
Suponha que as partições em todos os níveis em um quicksort são na proporção $1 - \alpha$ para $\alpha$ com $0 < \alpha \leq 1/2$ uma constante. Mostre que a profundidade mínima de uma folha na árvore de recursão é aproximadamente $- \log n / log \alpha$ e a profundidade máxima é aproximadamente $- \log n / \log (1 - \alpha)$.

## Questão 6
Você tem uma tabela de hash de tamanho $m$ na qual você insere $n$ chaves usando encadeamento" (separate chaining). As chaves são inteiros selecionados do conjunto $U = \{1, 2, \dots , nm\}$.

a) Prove que, não importa quão engenhosamente você projete sua função hash, deve existir um subconjunto $S$ de $U$ de tamanho pelo menos $n$ tal que cada chave em $S$ mapeie para a mesma localização na tabela de hash.

b) O que o item anterior implica sobre o tempo de execução do pior caso necessário para inserir $n$ chaves extraídas de $U$ em sua tabela de hash?


