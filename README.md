# DCC 831 - TECC: Manutenção e Evolução de Software

## TP2: Avaliação do uso de LLMs em MES  
**Avaliação de desempenho de LLMs como juízes de códigos - Primeiras Percepções**  
**Caíque Bruno Fortunato - 2024700378**  
**Larisse Stefany Pires Amorim - 2024701072**

---

## Objetivo do Trabalho

Avaliar o desempenho de LLMs como juízes de código

---

## Base de Dados

Como base de dados, utilizamos a fornecida pelo **Code Review Open Platform (CROP)**. O CROP é um conjunto de dados de revisão de código aberto destinado a apoiar pesquisadores e profissionais de engenharia de software.

O CROP contém dados de duas comunidades de código aberto: **Eclipse** e **Couchbase**.

Para realização do trabalho, utilizamos a base de dados **java-client** fornecida pelo **Couchbase**, que é um arquivo CSV contendo 2635 links de revisões de código. Cada linha do arquivo representa uma única revisão de código, com as seguintes colunas:

- `id`
- `review_number`
- `revision_number`
- `author`
- `status`
- `change_id`
- `before_commit_id`
- `after_commit_id`

---

## Metodologia

- **Fonte:** Base `java-client` do projeto CROP (Couchbase).
- **Filtragem inicial:** Consideramos apenas revisões com status `MERGED` ou `ABANDONED`, totalizando **2622 revisões**.
- **Amostragem:** Seleção randômica de **300 revisões** para análise manual e automatizada.
- **Pré-processamento:**  
  Para cada revisão selecionada:
  - Extração do código original (antes da alteração) e do código modificado (após a alteração).

- **Avaliação com LLMs:**  
  Utilizaremos LLMs para julgar qual versão do código está mais adequada com base nos critérios:
  - Padrões de programação
  - Coesão
  - Manutenção

  As LLMs receberão dois trechos de código (antes e depois da revisão) e deverão escolher qual apresenta maior grau de compreensão e manutenibilidade.

---

## Modelos de Linguagem Utilizados

- **GPT-4o mini**
- **Gemma** (LLM Open Source)

*Versões específicas dos modelos ainda serão definidas.*

---

## Exemplos Preliminares de Prompts

> O prompt que utilizaremos nas LLMs para verificação será o seguinte:

Can you please rate whether the code 1 is better than the code 2 in terms of clarity, readability, and maintainability?
**I would like to know if:**
 • The code is easy to understand.
 • There are improvements in naming, structure, or style.
 • It is easy to maintain and extend.
 
 **Code 1:**
 `[code_1]`
 **Code 2:**
 `[code_2]`

---

## Avaliação Quantitativa

Após o julgamento das LLMs para as revisões disponíveis, faremos uma análise quantitativa, **comparando o resultado dado pelas LLMs com o resultado da coluna "status" da base de dados**.
Nosso objetivo é verificar se as revisões feitas pelas LLMs são parecidas com as revisões feitas por humanos, ou seja, o quanto ela se aproxima da avaliação humana ao julgar se um código pode ser aprovado ou não.

