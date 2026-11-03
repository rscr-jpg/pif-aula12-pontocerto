# Respostas da dupla — Atividade PontoCerto

## Dupla

| Papel | Nome completo | Usuário do GitHub |
|---|---|---|
| Integrante 1 (dono do fork) | Rubens Sousa | rscr-jpg |
| Integrante 2 (colaborador) | João Paulo do Nascimento | JP2311 |

## Explicação da solução

`calculaPontos` recebe a regra e o valor da compra, então a mesma função serve para
qualquer campanha. As fábricas recebem apenas o fator ou o bônus e devolvem uma
nova regra pronta para ser usada. Assim, não é necessário escrever uma função quase
igual para cada multiplicador ou para cada valor de bônus.

## Desafio 2

As regras são curtas e usadas apenas uma vez no teste da promoção. A lambda deixa a
regra no próprio lugar em que ela é aplicada, sem criar um nome que não será
reutilizado.

## Desafio 3

`campanhaMultiplicadora 5` devolve outra função, que recebe os pontos e os multiplica
por 5; não devolve um número. O comando `:t campanhaMultiplicadora 5` mostra
`Int -> Int`, confirmando que o resultado é uma função de pontos para pontos.

## Desafio 4

**a)** As operações não são equivalentes: multiplicar antes do bônus soma 200 depois
da multiplicação, enquanto aplicar o bônus antes faz com que esses 200 também sejam
multiplicados por 5.

**b)** A ordem deve ser `acumula blackFriday aniversarioCliente valor`, pois a
multiplicação acontece primeiro e o bônus é acrescentado apenas no final.

## Desafio 5 — revisão de código

| Erro | Função | O que estava errado | Como o GHC avisou (resumo da mensagem) | Como corrigimos |
|---|---|---|---|---|
| 1 | `aplicaRegraDuasVezes` | A assinatura dizia que `regra` era `Int`, mas ela é chamada como função. | O GHC indicou que um `Int` não podia ser aplicado como função. | Alteramos o primeiro tipo para `(Int -> Int)`. |
| 2 | `fimDeSemana` | A lambda usava `=>`, que não é a seta de Haskell. | O GHC apontou erro de análise perto de `=>`. | Trocamos por `->`. |
| 3 | `natal` | A fábrica `campanhaBonus` foi atribuída sem informar o bônus. | O GHC mostrou que o tipo esperado era `Int -> Int`, mas restava um argumento `Int`. | Aplicamos a fábrica com `300`. |
| 4 | `promocaoAtual` | A função foi aplicada a `100`, produzindo um número em vez de uma regra. | O GHC mostrou que era esperado `Int -> Int`, mas a expressão tinha tipo `Int`. | Atribuímos a própria função `pontosEmDobro`. |

## Desafio 6 — Haskell × C

Em Haskell, o tipo da regra é escrito como `(Int -> Int)` e as funções são valores de
primeira classe diretamente. Em C, a regra precisa ser declarada explicitamente como
ponteiro para função, `int (*regra)(int)`, e a chamada usa essa sintaxe de ponteiro.

## Evidência de execução

Saída do `main` de `fidelidade.hs`:

```text
--- Desafio 1 ---
120
240
170
240
--- Desafio 2 ---
80
160
130
240
170
--- Desafio 3 ---
750
350
100
55
--- Desafio 4 ---
950
1750
280
```

Saída do `main` de `revisao.hs` (depois de corrigido):

```text
40
100
400
200
```

Saída de `pontocerto.c`:

```text
160
130
250
300
```

