# Previsão do valor de aluguel com regressão linear

Modelos de regressão linear simples e múltipla que estimam o valor do aluguel de um imóvel a partir das suas características: metragem, valor do condomínio e número de quartos, banheiros, suítes e vagas.

Projeto desenvolvido como exercício prático do módulo 18 (Regressão Linear) do curso Profissão Cientista de Dados. O trabalho segue as etapas do CRISP-DM: entendimento e preparação dos dados, modelagem e avaliação.

## Contexto

Quem procura um apartamento para alugar normalmente sabe o tamanho do imóvel, o valor do condomínio e quantos quartos, banheiros e vagas ele tem. A ideia é usar essas informações para estimar o aluguel esperado e saber se o imóvel cabe no orçamento antes mesmo de visitá-lo.

## Base de dados

`ALUGUEL_MOD12.csv`: 7.203 imóveis e 7 variáveis numéricas.

| Variável | Descrição |
|---|---|
| Valor_Aluguel | Valor do aluguel (variável alvo) |
| Valor_Condominio | Valor do condomínio |
| Metragem | Área do imóvel em m² |
| N_Quartos | Número de quartos |
| N_banheiros | Número de banheiros |
| N_Suites | Número de suítes |
| N_Vagas | Número de vagas de garagem |

## Etapas

1. **Diagnóstico:** verificação dos tipos de dados e dos valores faltantes (a base não tem nulos).
2. **Limpeza:** remoção de 598 linhas duplicadas e de 30 registros incoerentes, com mais suítes do que banheiros.
3. **Outliers:** IQR com limite de 3× (outliers extremos) no aluguel e na metragem, o que removeu 7% das linhas. O limite tradicional de 1,5× descartaria cerca de 16% da base, incluindo imóveis de alto padrão que existem de verdade.
4. **Análise exploratória:** gráficos bivariados e matriz de correlação. A metragem é a variável mais correlacionada com o aluguel (0,65).
5. **Modelagem:** divisão de 80% para treino e 20% para teste, regressão linear simples (só a metragem) e regressão linear múltipla (todas as variáveis).
6. **Avaliação:** comparação do R² de treino e de teste para identificar overfitting ou underfitting.

## Resultados

| Modelo | R² treino | R² teste |
|---|---|---|
| Regressão linear simples (Metragem) | 0,414 | 0,435 |
| Regressão linear múltipla (6 variáveis) | 0,519 | 0,508 |

- Equação do modelo simples: **Valor_Aluguel = 26,41 × Metragem + 359,39**. Cada m² a mais soma cerca de R$ 26 ao aluguel.
- A regressão múltipla teve o melhor desempenho, e nenhum dos dois modelos mostra overfitting, porque o R² de treino e o de teste ficaram próximos.
- Cerca de metade da variação do aluguel continua sem explicação. A principal informação que falta na base é a localização do imóvel, e incluí-la seria o próximo passo para melhorar o modelo.

![Reta de regressão: metragem x valor do aluguel](imagens/reta_regressao.png)

## Como executar

```bash
pip install -r requirements.txt
jupyter notebook
```

Abra o notebook `previsao_aluguel_regressao_linear.ipynb` com o arquivo `ALUGUEL_MOD12.csv` na mesma pasta. O notebook também roda no Google Colab: basta enviar o CSV para a sessão antes de executar.

## Tecnologias

Python, pandas, matplotlib, seaborn e scikit-learn.
