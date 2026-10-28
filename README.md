# Simulador de investimentos em FIIs

Planilha educativa criada do zero para o desafio da DIO. O arquivo usa apenas exemplos fictícios e demonstra fórmulas e recursos do Excel; não é recomendação de investimento.

## Arquivos

- `simulador_fii.xlsx` — simulador e tabela de apoio com fórmulas, lista suspensa e gráficos editáveis.
- `prints/perfil-conservador.png` e `prints/perfil-agressivo.png` — prévias da planilha com os dois perfis para comparar a alocação.

## Como usar

Abra a aba **Simulador** e altere as células amarelas:

| Campo | Exemplo inicial | O que controla |
|---|---:|---|
| Salário mensal | R$ 4.000 | Base para a sugestão de aporte de 30% |
| Aporte informado | R$ 2.000 | Aporte mensal usado nas projeções e na alocação |
| Prazo | 20 anos | Horizonte da projeção principal |
| Retorno total mensal | 0,80% | Hipótese usada para projetar o patrimônio |
| Yield de dividendos mensal | 0,60% | Hipótese usada para estimar os dividendos mensais |
| Perfil de investidor | Conservador | Escolha Conservador, Moderado ou Agressivo na lista |

O simulador apresenta as cinco respostas do desafio, compara o aporte informado com a sugestão de 30% do salário, mostra projeções de 2, 5, 10, 20 e 30 anos e divide o aporte entre seis categorias de FII. O gráfico de rosca acompanha o perfil selecionado; o gráfico de linha mostra a projeção de patrimônio.

## Fórmulas demonstradas

O patrimônio futuro usa a função **VF** do Excel (armazenada como `FV`):

```excel
=VF(B9; B8*12; -B7; 0; 0)
```

Na pasta, os nomes `aporte` e `taxa_mensal` continuam definidos para os campos editáveis B7 e B9. A fórmula atual usa as referências diretas equivalentes. Para praticar a versão com nomes, substitua B9 por `taxa_mensal` e B7 por `aporte`. Os depósitos são considerados no fim de cada mês (`tipo = 0`). Nos cenários, taxa e aporte usam referências absolutas, enquanto o prazo acompanha a linha.

A estimativa mensal de dividendos é calculada à parte:

```excel
=J14 * B10
```

O retorno total e o yield são hipóteses diferentes. A planilha não soma os dividendos novamente ao retorno total, o que evita dupla contagem nessa simulação simplificada. O modelo não calcula reinvestimento de dividendos.

Na aba **Apoio**, cada linha combina Perfil e Tipo de FII numa chave, como `Moderado-Papel`. A aba principal usa `PROCV` (a função interna pode aparecer como `VLOOKUP`, conforme o idioma do Excel) para buscar o percentual dessa chave. A coluna de conferência verifica que cada perfil totalize 100%.

## Como editar as premissas de alocação

Na aba **Apoio**, edite os percentuais fictícios na coluna D. Mantenha seis categorias para cada perfil e confira se os totais nas colunas F:G permanecem em 100%. A tabela deve conter uma linha única para cada combinação de perfil e categoria, pois a chave composta usada pelo PROCV precisa ser única.

## Capturas de tela para o repositório

As imagens nesta pasta são prévias renderizadas da própria planilha. No Excel, você pode reproduzir a comparação selecionando **Conservador** e depois **Agressivo**, mantendo as demais entradas iguais.

![Perfil conservador](prints/perfil-conservador.png)

![Perfil agressivo](prints/perfil-agressivo.png)

Com os percentuais iniciais, o perfil Conservador concentra 40% em Papel e 40% em Tijolo; o perfil Agressivo distribui 20% em Papel, 20% em Tijolo, 20% em Desenvolvimento e o restante entre as outras categorias. Todos os percentuais são ilustrativos e não representam recomendação ou perfil adequado para uma pessoa.

## Limitações importantes

Os resultados são hipóteses matemáticas, não previsões nem garantias. A planilha supõe taxa mensal constante e aportes mensais regulares. Não inclui inflação, impostos, taxas, oscilações de preço, vacância, mudanças nas distribuições ou reinvestimento de dividendos. Dividendos de FIIs podem variar ou deixar de ser pagos; o patrimônio também pode cair.

## Entrega

Antes de publicar, abra o arquivo no Excel para conferir a lista suspensa, os gráficos e o recálculo das fórmulas no seu ambiente.

