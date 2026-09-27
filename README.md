# Gravidade de acidentes nas rodovias federais de Santa Catarina

Projeto da disciplina de Machine Learning, Engenharia de Computação, UNISATC.

Bruno Pagani Rampinelli · João Henrique Camilo Fogaça · Vinícius dos Santos Nascimento

## Objetivo

Prever se um acidente registrado pela PRF em rodovia federal de Santa Catarina teve vítima fatal, a partir das condições em que ele aconteceu. É um problema de classificação binária, e foram comparados dois modelos: Regressão Logística e KNN.

Só 4,2% dos acidentes são fatais, então o trabalho gira em torno de tratar esse desbalanceamento.

## Dados

Dados abertos da Polícia Rodoviária Federal, arquivos de acidentes agrupados por ocorrência, de 2021 a 2025.

Fonte: https://www.gov.br/prf/pt-br/acesso-a-informacao/dados-abertos/dados-abertos-da-prf

Os cinco arquivos usados (`datatran2021.csv` a `datatran2025.csv`) estão na pasta `dados/`. São 39.849 acidentes de Santa Catarina depois do filtro.

Treino: 2021 a 2024. Teste: o ano de 2025 inteiro, usado uma única vez.

## Como rodar

**No Google Colab**

1. Abrir o `Projeto_ML_PRF.ipynb`.
2. Enviar os cinco arquivos da pasta `dados/` para a área de arquivos do Colab.
3. Executar em Ambiente de execução > Executar tudo.

**Localmente**

1. Clonar o repositório e instalar as bibliotecas: `pip install -r requirements.txt`
2. Abrir o notebook e executar todas as células.

Não é preciso mudar caminho nenhum: a primeira célula usa a pasta `dados/` quando ela existe ao lado do notebook e o `/content` quando está no Colab.

A célula que compara as técnicas de balanceamento leva cerca de sete minutos, porque testa quatro combinações de modelo e técnica com validação cruzada.

## Estrutura

| Arquivo | Conteúdo |
|---|---|
| `Projeto_ML_PRF.ipynb` | Notebook com o pipeline completo |
| `dados/` | Arquivos CSV da PRF |
| `docs/` | Documento final em ABNT |
| `requirements.txt` | Bibliotecas usadas |

## Resultado no conjunto de teste (2025)

| Modelo | Revocação | F1 | ROC-AUC |
|---|---|---|---|
| Regressão Logística | 0,722 | 0,252 | 0,853 |
| KNN com subamostragem | 0,650 | 0,244 | 0,810 |

O modelo escolhido foi a Regressão Logística, que encontrou 270 dos 374 acidentes fatais de 2025. Os fatores de maior peso foram atropelamento de pedestre e colisão frontal.

## Tratamento do desbalanceamento

Três frentes, todas aplicadas apenas ao treino:

- **Peso de classe** (`class_weight='balanced'`) na Regressão Logística.
- **Subamostragem aleatória**, que descarta acidentes não graves até as classes empatarem. É a técnica usada no Modelo B.
- **SMOTE**, que cria acidentes fatais sintéticos. Testado para comparação.

As duas técnicas de reamostragem ficam dentro do pipeline, então rodam só nas partes de treino de cada divisão da validação cruzada. O conjunto de teste nunca é reamostrado.

## Trabalhos de referência

O tratamento do desbalanceamento foi baseado em:

- MAFORT, E. V.; KAPPEL, M. A. A. Técnicas de aprendizado de máquina para predição de gravidade de acidentes em rodovias do estado do Rio de Janeiro. REIC, v. 23, n. 1, 2025.
- GABARDO, A. M. P. et al. Highway to... determining fatal outcomes in traffic accidents based on police reports. BRACIS, 2025.
- SOUSA, G. I. L. de; RODRIGUES, M. C. de O.; ROSA, A. G. F. Aprendizado de máquina na análise de sinistros de trânsito: um estudo na zona urbana de Teresina - PI. Scientia Generalis, v. 7, n. 1, 2026.
- FIORENTINI, N.; LOSA, M. Handling imbalanced data in road crash severity prediction by machine learning algorithms. Infrastructures, v. 5, n. 7, 2020.
