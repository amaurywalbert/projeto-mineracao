# Mineração de Dados Aplicada à Predição da Energia de Docking de Peptídeos Antimicrobianos

Projeto desenvolvido na disciplina **Mineração de Dados** do Programa de Pós-Graduação em Ciência da Computação (PPGCO/UFU).

O trabalho apresenta um pipeline completo de mineração de dados para construção e avaliação de modelos de Aprendizado de Máquina capazes de predizer a energia de docking de peptídeos antimicrobianos presentes na base **SAGAPEP**, utilizando diferentes descritores bioinformáticos e técnicas de redução de dimensionalidade.

---

## Objetivos

O projeto possui como objetivo principal comparar diferentes representações de sequências de aminoácidos e investigar seu impacto na capacidade preditiva de algoritmos de regressão para estimativa da energia de docking.

Especificamente são realizados:

- análise exploratória dos dados;
- extração de diferentes descritores proteicos;
- redução de dimensionalidade utilizando PCA;
- treinamento de diversos algoritmos de regressão;
- otimização de hiperparâmetros;
- comparação estatística entre descritores e modelos.

---

# Estrutura do Projeto

```
projeto-mineracao/
│
├── data/
│   ├── raw/
│   │   └── sagapep.csv
│   │
│   └── processed/
│       ├── aac_features.csv
│       ├── aal_features.csv
│       ├── cksnap_features.csv
│       ├── cksaagp_features.csv
│       ├── pca_aac.pkl
│       ├── pca_aal.pkl
│       ├── pca_cksnap.pkl
│       └── pca_cksaagp.pkl
│
├── notebooks/
│   ├── 01_Dataset_EDA.ipynb
│   ├── 02_AAC.ipynb
│   ├── 03_AAL.ipynb
│   ├── 04_CKSNAP.ipynb
│   ├── 05_CKSAAGP.ipynb
│   ├── 05.1_Comparacao_descritores.ipynb
│   ├── 06_Treinamento.ipynb
│   └── 06.1_Ajustes_hiperparametros.ipynb
│
├── results/
│   ├── model_results.csv
│   ├── model_results_hiper.csv
│   ├── model_ranking.csv
│   └── model_ranking_hiper.csv
│
└── docs/
    ├── Artigo.docx
    └── Artigo.pdf
```

---

# Fluxo Metodológico

O projeto segue as principais etapas de um processo de mineração de dados:

1. Análise exploratória da base SAGAPEP.
2. Pré-processamento das sequências.
3. Extração dos descritores bioinformáticos.
4. Redução de dimensionalidade utilizando PCA.
5. Construção dos conjuntos de treinamento.
6. Treinamento de múltiplos algoritmos de regressão.
7. Ajuste de hiperparâmetros.
8. Comparação dos modelos.
9. Geração do ranking final.

---

# Descrição dos Notebooks

## 01_Dataset_EDA.ipynb

Realiza a análise exploratória da base SAGAPEP, investigando:

- distribuição das variáveis;
- estatísticas descritivas;
- valores ausentes;
- distribuição da variável alvo;
- preparação inicial dos dados.

---

## 02_AAC.ipynb

Implementa o descritor **AAC (Amino Acid Composition)**.

Cada sequência é representada pela frequência relativa de ocorrência dos 20 aminoácidos.

Ao final são produzidos:

- matriz de atributos;
- aplicação do PCA;
- armazenamento do dataset processado.

---

## 03_AAL.ipynb

Implementa o descritor **AAL (Amino Acid Local)**.

Além da composição global, procura representar informações relacionadas à posição dos aminoácidos na sequência.

---

## 04_CKSNAP.ipynb

Implementa o descritor **CKSNAP (Composition of K-Spaced Amino Acid Pairs)**.

Esse método considera pares de aminoácidos separados por diferentes distâncias (k-spaced), capturando relações locais entre resíduos.

---

## 05_CKSAAGP.ipynb

Implementa o descritor **CKSAAGP (Composition of K-Spaced Amino Acid Group Pairs)**.

Nesse caso os aminoácidos são agrupados segundo propriedades físico-químicas, reduzindo a dimensionalidade e preservando relações biológicas importantes.

---

## 05.1_Comparacao_descritores.ipynb

Compara os diferentes descritores gerados:

- número de atributos;
- comportamento após PCA;
- impacto na representação dos dados.

---

## 06_Treinamento.ipynb

Notebook responsável pela etapa principal de modelagem.

São treinados diversos algoritmos de regressão utilizando exatamente o mesmo protocolo experimental.

Características:

- Validação Cruzada 10-Fold;
- Pipeline do Scikit-Learn;
- Padronização automática quando necessária;
- Avaliação utilizando múltiplas métricas;
- Comparação direta entre descritores.

Entre os algoritmos avaliados encontram-se:

- Random Forest
- Support Vector Regression (SVR)
- KNN Regressor
- MLP Regressor
- Bayesian Ridge

---

## 06.1_Ajustes_hiperparametros.ipynb

Realiza a otimização dos hiperparâmetros dos modelos visando maximizar o desempenho preditivo.

Ao final é produzido um novo ranking contendo os modelos ajustados.

---

# Dados

O projeto utiliza a base:

**SAGAPEP**

A base contém sequências de peptídeos antimicrobianos juntamente com o valor da melhor energia de docking utilizada como variável alvo da regressão.

---

# Resultados

Os principais resultados são armazenados em:

```
results/
```

incluindo:

- desempenho individual dos modelos;
- ranking dos algoritmos;
- comparação entre descritores;
- comparação após otimização dos hiperparâmetros.

---

# Tecnologias Utilizadas

- Python 3
- Pandas
- NumPy
- Scikit-Learn
- Matplotlib
- Seaborn
- Jupyter Notebook

---

# Como Executar

Clone o repositório:

```bash
git clone https://github.com/amaurywalbert/projeto-mineracao.git
```

Acesse a pasta:

```bash
cd projeto-mineracao
```

Instale as dependências:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn notebook
```

Inicie o Jupyter:

```bash
jupyter notebook
```

Execute os notebooks na seguinte ordem:

```
01_Dataset_EDA

02_AAC

03_AAL

04_CKSNAP

05_CKSAAGP

05.1_Comparacao_descritores

06_Treinamento

06.1_Ajustes_hiperparametros
```

---


# Organização dos Experimentos

Todos os modelos são avaliados utilizando exatamente o mesmo protocolo experimental:

- Validação Cruzada 10-Fold;
- mesma variável alvo;
- mesmas métricas de avaliação;
- comparação direta entre descritores;
- posterior otimização de hiperparâmetros.

Essa estratégia garante uma comparação justa entre diferentes representações das sequências biológicas.

---

# Produto Final

O projeto resulta em:

- Diferentes conjuntos de atributos bioinformáticos;
- Modelos de regressão treinados;
- Comparação entre descritores;
- Ranking dos algoritmos;
- [Artigo científico descrevendo toda a metodologia.](./docs/Artigo.pdf)

---

# Autor

**Amaury Walbert**


Doutorando em Ciência da Computação — Universidade Federal de Uberlândia (UFU)

Disciplina: Mineração de Dados — PPGCO/UFU

Orientação: Prof. Dr. Leandro Nogueira Couto