# Diamond Price Prediction

> Um projeto de Machine Learning para precificação automática de diamantes com alta precisão, utilizando Random Forest Regressor.

![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat-square)
![Lib](https://img.shields.io/badge/Scikit--Learn-Random%20Forest-orange?style=flat-square)
![Status](https://img.shields.io/badge/Status-Concluído-green?style=flat-square)

## Sobre o Projeto

A precificação de joias preciosas, especialmente diamantes, é uma tarefa complexa que depende de múltiplas variáveis físicas e subjetivas (os "4 Cs": Carat, Cut, Color, Clarity). Avaliações manuais são demoradas e sujeitas a viés humano.

Este projeto visa resolver esse problema criando um modelo preditivo capaz de estimar o preço de um diamante com base em suas características, auxiliando joalherias e avaliadores a terem um preço de referência rápido e preciso.

## O Dataset

Foram utilizados dados contendo **53.940 registros** de diamantes.
As principais colunas são:
* **Price:** Preço em dólares (Alvo).
* **Carat:** Peso do diamante.
* **Cut:** Qualidade do corte (Fair, Good, Very Good, Premium, Ideal).
* **Color:** Cor do diamante (de J a D).
* **Clarity:** Medida de clareza (de I1 a IF).
* **Dimensões:** x, y, z, depth, table.

## Engenharia de Atributos & Estratégia

Para garantir que o modelo entendesse a hierarquia de qualidade dos diamantes, optei por **não utilizar OneHotEncoding** nas variáveis categóricas. Em vez disso, apliquei **Mapeamento Ordinal**:

* O modelo "entende" que um corte `Ideal` (5) é matematicamente superior a um corte `Fair` (1).
* Isso preservou a ordem de grandeza e melhorou a performance da árvore de decisão.

```python
# Exemplo da estratégia utilizada
mapa_corte = {'Fair': 1, 'Good': 2, 'Very Good': 3, 'Premium': 4, 'Ideal': 5}
df['cut'] = df['cut'].map(mapa_corte)
