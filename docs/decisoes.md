# Previsões, evidências e decisões

Preencha antes e depois da execução. Explique com suas palavras; resultados de testes sozinhos não respondem às perguntas.

## Etapa 01 — reconhecer e cadastrar (até 300 palavras)

| Situação | Minha previsão antes de executar | Evidência observada e explicação |
|---|---|---|
| Duas instâncias com LT-101: identidade e igualdade | preencher | preencher |
| Inserir 12% e depois 99% com a mesma tag | preencher | preencher |
| Buscar outra instância da mesma tag | preencher | preencher |
| Buscar chave ausente e consultar leitura zero | preencher | preencher |

1. De onde vêm os dois `second` do C++? Por que o `map` precisa de ordem e o `dict` precisa de hash e igualdade?
2. Qual comportamento mudaria se cada tentativa sobrescrevesse o cadastro? Em que requisito essa alternativa seria adequada?
3. Por que um conjunto de tags não substitui o catálogo de medições? Hashes diferentes para objetos iguais seriam aceitáveis?

## Etapa 02 — remover, consultar e pensar na memória (até 350 palavras)

| Situação                                              | Minha previsão                                                                                                                             | Evidência C++ e Python                                                                                          |
| ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------- |
| Remover chave existente duas vezes                    | A primeira remoção deve retornar `true` e diminuir a quantidade de cadastros. A segunda deve retornar `false`, pois a chave já não existe. | Os testes confirmaram esse comportamento em C++ e Python.                                                       |
| Consultar 0, 2 e 100 últimas leituras de [12, 12, 15] | Para 0, espero uma coleção vazia. Para 2, espero `[12, 15]`. Para 100, espero todas as leituras `[12, 12, 15]`.                            | Os testes confirmaram os três casos nas duas linguagens, mantendo a ordem de chegada e preservando o histórico. |
| Limpar a coleção devolvida e consultar novamente      | A coleção retornada deve ser independente, portanto alterá-la não deve modificar o histórico original.                                     | Os testes confirmaram que o histórico permanece intacto após modificar a coleção retornada.                     |
| Remover cadastro e consultar histórico independente   | A remoção do cadastro não deve apagar as leituras já registradas no histórico.                                                             | Os testes confirmaram que o histórico continua disponível após a remoção do cadastro.                           |

### 1. Algoritmo de `ultimas`

O algoritmo verifica primeiro o caso de limite zero. Nesse caso, retorna uma coleção vazia sem alterar o histórico. Se o limite for menor que a quantidade de leituras, calcula a posição inicial como quantidade menos limite e copia as leituras dessa posição até o final. Se o limite for maior ou igual à quantidade existente, retorna todas as leituras.

Em C++, o limite usa `size_t`, portanto não existe limite negativo. Em Python, foi necessário rejeitar explicitamente valores negativos com `ValueError`.

### 2. Memória do histórico

A consulta não limita a memória do histórico. Ela apenas seleciona as últimas leituras para exibição. Para mostrar somente os últimos dez valores, a consulta seria suficiente. Seria necessário descartar dados antigos somente se o requisito fosse manter no máximo dez leituras. Nesse caso, as informações descartadas não poderiam mais ser consultadas.

### 3. Posse e referências

Em Python, se o chamador ainda possui uma referência para uma medição, remover a entrada do catálogo não destrói necessariamente essa medição. Em C++, um ponteiro para uma entrada que foi removida deixa de ser válido e não pode ser usado com segurança depois da remoção.

### 4. Alternativa rejeitada

Uma alternativa rejeitada seria eliminar repetições. Isso violaria o requisito de preservar cada ocorrência do histórico, pois duas leituras iguais podem representar momentos diferentes. Essa alternativa poderia ser útil em um sistema que precisasse armazenar somente valores distintos.

## Evidências da entrega

* **Comando local:** `make test ETAPA=02`
* **Resultado:** `OK C++ etapa 02`, `OK Python etapa 02` e `OK etapa 02 cumulativa (C++ e Python)`.
* **Commit testado:** `d61ca27` — `remove cadastros e consulta ultimas leituras sem perder historico`
* **URL da execução de Actions desse commit:** preencher com o link da execução no GitHub.
* **Diagnóstico de falha encontrado e correção:** os testes inicialmente indicaram falhas em `inserir`, `buscar`, `remover` e `ultimas`. As implementações foram corrigidas para impedir duplicatas, consultar sem criar entradas, remover corretamente os cadastros e retornar as últimas leituras sem alterar o histórico.
* **Limite observado dos testes:** os testes verificam o comportamento esperado das implementações, mas a explicação das decisões de projeto, como identidade, igualdade, estabilidade da chave e gerenciamento de referências, exige análise do código e do contrato.


## Evidências da entrega

## Evidências da entrega

* **Comando local, resultado e commit testado:** `make test ETAPA=02` — resultado: `OK C++ etapa 02`, `OK Python etapa 02` e `OK etapa 02 cumulativa (C++ e Python)`. Commit: `d61ca27` — `remove cadastros e consulta ultimas leituras sem perder historico`.
* **URL da execução de Actions desse commit:** preencher com o link da execução no GitHub.
* **Um diagnóstico de falha encontrado e como o corrigiu:** os testes inicialmente indicaram falhas nas operações de cadastro e consulta. Foram corrigidos `inserir`, `buscar`, `remover` e `ultimas`, mantendo as regras de não duplicar cadastros, consultar sem criar entradas, remover corretamente e preservar o histórico.
* **Limite observado dos testes: o que ainda exige inspeção/explicação?** Os testes verificam os comportamentos esperados, mas algumas decisões de projeto precisam ser explicadas, como identidade e igualdade, estabilidade da chave, independência do histórico e validade de referências após uma remoção.

