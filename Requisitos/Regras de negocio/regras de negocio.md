# Regras de negócio da solução (RN) - GAC (Gestão de Ativos do CCT)

## 1. Regras de negócio

### 1.1 Regra de negócio 01

* **Identificador:** RN01 - Sistema impede novos empréstimos para professores em atraso
* **Descrição:** Professores com ativos em atraso são impedidos de realizar novos empréstimos[cite: 146].

---

### 1.2 Regra de negócio 02

* **Identificador:** RN02 - Sistema bloqueia ativos com danos reportados

* **Descrição:** Ativos com danos reportados entram em status "bloqueado" até reparo técnico[cite: 148, 149].

---

## 2. Checklist de Validação da Regra de Negócio

Use este checklist antes de finalizar a regra.

### 2.1 Estrutura mínima

* [x] Identificador único e padronizado (ex.: RN1, RN1.1, RN2).
* [x] Nome da regra no formato sujeito + verbo + objeto.
* [x] Descrição clara, direta e sem ambiguidades.

### 2.2 Qualidade da regra

* [x] A regra descreve apenas uma decisão/comportamento principal.
* [x] Condições de aplicação (gatilho/contexto) estão explícitas.
* [x] Resultado esperado da regra está explícito.
* [x] A regra é verificável e testável.

### 2.3 Consistência e rastreabilidade

* [x] Não há conflito com outras regras já existentes.
* [x] A regra referencia origem (negócio, norma, lei ou decisão do cliente), quando aplicável.
* [x] A regra está alinhada com CDU, RNF e demais artefatos relacionados.

### 2.4 Prontidão

* [x] Conteúdo revisado por pares.
* [x] Regra pronta para uso em análise, desenvolvimento e testes.