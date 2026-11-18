# PjBL — RA3 (Análise, Visualização e Machine Learning)

**Projeto:** demanda, cancelamentos e clientes de uma loja online do Reino Unido (base *Online Retail*, UCI).
**Disciplina:** Data Analytics (PUCPR) · **Entrega:** RA3

> Equipe: _PjBL 14 — João Guilherme Vargas e Mateus Natan Maoski_

## O que há neste repositório

| Caminho | Conteúdo |
|---|---|
| `RA3_Analise_Visualizacao_ML.ipynb` | Notebook com todo o RA3 (estatística descritiva → visualizações → amostragem e representatividade → machine learning → conclusões), com todas as células executadas |
| `RA3_Analise_Visualizacao_ML.html` | Export estático do notebook já executado, para conferência sem precisar rodar nada |
| `data/processed/online_retail_preparado.parquet` | **Conjunto preparado no RA1** (534.128 linhas × 14 colunas), ponto de partida do RA3 (mesmo arquivo usado no RA2) |
| `data/processed/metricas_ra1.json` | Números-chave do RA1, para referência |
| `data/raw/` | Não utilizado neste RA (o RA3 parte direto dos dados já preparados) |
| `requirements.txt` | Dependências, nas versões em que o notebook foi executado |

## Como reproduzir

1. `pip install -r requirements.txt` (ou crie um ambiente virtual: `python3 -m venv .venv && source .venv/bin/activate && pip install -r requirements.txt`).
2. Abra `RA3_Analise_Visualizacao_ML.ipynb` **na pasta raiz deste diretório** (`RA3/`) e use *Executar tudo*. O notebook lê `data/processed/online_retail_preparado.parquet`, incluído no repositório.
3. Execução completa verificada em ambiente Linux com Python 3.12.11 e as versões listadas em `requirements.txt` (menos de um minuto; 534 mil linhas, sem Spark).
4. Alternativa sem instalar nada: abra `RA3_Analise_Visualizacao_ML.html` em qualquer navegador.

## Conteúdo do RA3

O notebook está organizado em 5 seções, mapeadas diretamente à rubrica do RA3:

1. **Análise estatística descritiva** — tendência central (média/mediana), dispersão (amplitude, desvio-padrão, IQR) e distribuição (percentis, concentração) do valor das vendas, do ticket por fatura, da receita mensal e da proporção de cancelamento.
2. **Visualização e interpretação dos dados** — 6 gráficos: distribuição do valor das vendas (histograma + boxplot), receita líquida mensal, receita por país, mapa de calor de faturas por hora/dia da semana, proporção de cancelamento por mês e dispersão RFM dos clientes identificados. Cada um acompanhado de uma leitura de negócio.
3. **Amostragem e representatividade** — origem e abrangência da base (censo de um período, não uma amostra probabilística), adequação ao problema investigado e limitações/vieses conhecidos (concentração no Reino Unido, clientes não identificados, mês incompleto, outlier de quantidade extrema, ausência de custo/margem/canal).
4. **Machine Learning** — classificação binária (regressão logística) para prever se uma linha de pedido é um cancelamento, a partir de características disponíveis no momento do pedido (sem usar o sinal da quantidade, que definiria o alvo trivialmente). Inclui divisão treino/teste estratificada, padronização, comparação entre modelo padrão e balanceado, e avaliação com acurácia, precisão, recall, F1 e ROC-AUC.
5. **Conclusões** — síntese dos resultados estatísticos e visuais, interpretação do desempenho do modelo, limitações e relação com o problema definido no RA1.

## Fonte dos dados

Chen, D. *Online Retail* [Dataset]. UCI Machine Learning Repository, 2015. https://doi.org/10.24432/C5BW33 (licença CC BY 4.0).

## Lendo o conjunto preparado

```python
import pandas as pd
df = pd.read_parquet("data/processed/online_retail_preparado.parquet")
```

## Escopo (RA3)

O RA3 cobre análise estatística descritiva, visualização, uma discussão sobre amostragem/representatividade e uma aplicação de machine learning supervisionado, encerrando o fluxo de dados do projeto iniciado no RA1 (ingestão e preparação) e continuado no RA2 (processamento em streaming).
