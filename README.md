# Detecção de Páginas Web de Phishing Baseada em Perceptron Multicamadas (MLP)

Este repositório contém a implementação de um modelo de Rede Neural Artificial do tipo Perceptron Multicamadas (MLP) para a classificação e detecção de websites de phishing.

---

## Visão Geral do Projeto

O phishing representa uma das principais vulnerabilidades na segurança da informação. Este trabalho aplica aprendizado profundo (Deep Learning) sobre características estruturais de páginas web e URLs para diferenciar endereços legítimos de páginas maliciosas.

* **Modelo Base:** Perceptron Multicamadas (MLP).
* **Framework:** TensorFlow / Keras.
* **Explicabilidade:** SHAP (*KernelExplainer*).

---

## Conjunto de Dados (Dataset)

A pesquisa utiliza o dataset público **Phishing Websites Dataset** (UCI ID: 327):

* **Total de Amostras:** 11 055 páginas.
* **Distribuição:** 6 157 páginas legítimas e 4 898 páginas de *phishing*.
* **Atributos:** 30 características extraídas (ex.: presença de certificado SSL/TLS, IP no domínio, encurtadores de URL, idade do domínio, entre outros).
* **Divisão dos Dados:** 80% para treino e 20% para teste ($N = 2 211$) com amostragem estratificada.

---

## Arquitetura do Modelo

A rede neural foi estruturada em camadas densas com mecanismos de regularização para garantir boa capacidade de generalização:

1. **Camada de Entrada:** 30 atributos.
2. **1ª Camada Oculta:** 64 neurónios com função de ativação `ReLU`, acompanhada de Batch Normalization e Dropout ($20\%$).
3. **2ª Camada Oculta:** 32 neurónios com ativação `ReLU`.
4. **Camada de Saída:** 1 neurónio com ativação `Sigmoide` para classificação binária.

### Configurações de Treino:
* **Função de Perda:** Entropia Cruzada Binária (Binary Cross-Entropy).
* **Otimizador:** Adam ($\text{Learning Rate} = 0,001$).
* **Total de Parâmetros Treináveis:** 4 097 parâmetros.
* **Callbacks:** *Early Stopping* e *ReduceLROnPlateau*.

---

## Resultados Obtidos

O desempenho do modelo avaliado no conjunto de teste revelou as seguintes métricas gerais:

* **Acurácia de Validação:** 97,15%
* **Perda (Loss) de Validação:** 0,0851

### Matriz de Confusão Numérica:
* **Verdadeiros Negativos (Legítimos identificados corretamente):** 1 213
* **Falsos Positivos (Legítimos classificados como phishing):** 18
* **Falsos Negativos (Phishing classificados como legítimos):** 45
* **Verdadeiros Positivos (Phishing identificados corretamente):** 935

---

## Explicabilidade com SHAP

Para prover transparência ao modelo e interpretar como cada atributo influencia a decisão da rede neural, utiliza-se a biblioteca SHAP (KernelExplainer).A análise calcula o impacto de todas as 30 características do conjunto de dados, destacando no gráfico as 20 mais influentes para a decisão do modelo.
