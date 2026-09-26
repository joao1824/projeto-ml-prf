# Gravidade de acidentes nas rodovias federais de Santa Catarina

Projeto Final da disciplina de Machine Learning Clássico, Engenharia de Computação, UNISATC.

## Objetivo

Prever se um acidente registrado pela PRF em rodovia federal de Santa Catarina teve vítima fatal, a partir das condições em que ele aconteceu. É um problema de classificação binária, e foram comparados dois modelos: Regressão Logística e KNN.

## Dados

Dados abertos da Polícia Rodoviária Federal, arquivos de acidentes agrupados por ocorrência, de 2021 a 2025.

Fonte: https://www.gov.br/prf/pt-br/acesso-a-informacao/dados-abertos/dados-abertos-da-prf

Os cinco arquivos usados (`datatran2021.csv` a `datatran2025.csv`) estão na pasta `dados/`.

## Como rodar

1. Abrir o `Projeto_ML_PRF.ipynb` no Google Colab.
2. Enviar os cinco arquivos da pasta `dados/` para a área de arquivos do Colab (pasta `/content`).
3. Executar todas as células em Ambiente de execução > Executar tudo.

A parte do KNN demora alguns minutos.

Para rodar fora do Colab, instalar as bibliotecas do `requirements.txt` e trocar o caminho `/content/` no início do notebook pela pasta onde estão os CSVs. O código precisa do scikit-learn 1.2 ou mais novo.

## Estrutura

| Arquivo | Conteúdo |
|---|---|
| `Projeto_ML_PRF.ipynb` | Notebook com o pipeline completo |
| `dados/` | Arquivos CSV da PRF |
| `docs/` | Documento final em ABNT |
| `requirements.txt` | Bibliotecas usadas |


