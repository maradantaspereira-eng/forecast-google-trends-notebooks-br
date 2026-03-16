# Previsão de Séries Temporais com Modelos Clássicos e ML — Google Trends Brasil (2021–2026)

Pipeline de forecasting aplicado a dados do Google Trends (Brasil, 2021–2026). Modelos: ETS, ARIMA, Prophet, NNETAR, Gradient Boosting. Validação out-of-sample com RMSE, MAPE e MASE.

## Sobre o Projeto

Este projeto compara seis modelos de previsão aplicados a dados mensais do Google Trends para o termo "MacBook Air" no Brasil. O objetivo é avaliar o desempenho de modelos clássicos, GAM e de machine learning em uma série temporal curta (51 observações no treino, 12 no teste).

## Modelos Implementados

| Categoria | Modelo | Descrição |
|-----------|--------|-----------|
| Baseline | SNAIVE | Sazonal ingênuo, replica os valores do período sazonal anterior |
| Baseline | TSLM | Regressão linear com tendência + dummies mensais via OLS |
| Estatístico | ETS | Holt-Winters aditivo (erro, tendência, sazonalidade) |
| Estatístico | ARIMA | Seleção automática de ordem via AIC (pmdarima) |
| GAM | Prophet | Modelo aditivo com sazonalidade anual e estimação bayesiana |
| ML | NNETAR | MLP (10,5) com lags selecionados por AIC do ARIMA |
| ML | Gradient Boosting | Regressão quantílica (τ = 0.05, 0.5, 0.95) para intervalos de predição |
| Combinação | Ensemble | Média aritmética de ETS, ARIMA, Prophet, NNETAR e TSLM |

## Resultados

| Modelo | RMSE | MAPE | MASE |
|--------|------|------|------|
| NNETAR | 4,87 | 5,90% | 0,64 |
| Ensemble | 8,42 | 11,50% | 1,23 |
| ARIMA | 9,20 | 12,43% | 1,34 |
| TSLM | 8,90 | 12,87% | 1,36 |
| ETS | 9,70 | 14,46% | 1,51 |
| Prophet | 10,84 | 15,86% | 1,68 |
| ML_Central | 15,05 | 20,76% | 2,23 |
| SNAIVE | 14,23 | 23,69% | 2,42 |

O NNETAR liderou em todas as métricas. MASE de 0,64 indica que o erro do modelo é 36% menor que o do baseline sazonal ingênuo.

## Estrutura do Projeto

```
forecast-google-trends-notebooks-br/
├── data/
│   └── time_series_BR_20201231-2100_20260314-1255.csv
├── series_temporais_google_trends.ipynb
├── README.md
├── .gitignore
└── LICENSE
```

## Dependências

- Python 3.10+
- pandas
- numpy
- matplotlib
- seaborn
- statsmodels
- pmdarima
- prophet
- scikit-learn

Instalação:

```bash
pip install pandas numpy matplotlib seaborn statsmodels pmdarima prophet scikit-learn
```

## Como Executar

1. Clone o repositório:
```bash
git clone https://github.com/maradantaspereira-eng/forecast-google-trends-notebooks-br.git
```

2. Instale as dependências:
```bash
pip install pandas numpy matplotlib seaborn statsmodels pmdarima prophet scikit-learn
```

3. Abra o notebook no VSCode ou Jupyter:
```bash
jupyter notebook series_temporais_google_trends.ipynb
```

O CSV já está na pasta `data/`. O notebook roda direto sem configuração adicional.

## Licença

MIT
