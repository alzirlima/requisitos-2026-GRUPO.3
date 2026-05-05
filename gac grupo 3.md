# Visão da Demanda (VD)

## Histórico de Versões

| Data | Versão | Descrição | Autor |
| :--- | :--- | :--- | :--- |
| 2026 | 1.0 | Criação do documento de visão para o GAC | Francisco Alzir Lima Junior, João Gabriel de Holanda Montenegro, Lívia Maria Barreto Albuquerque, Rômulo Azevedo Montenegro Neto |

## 1. Objetivo

Definir a proposta de valor e o escopo do Sistema GAC (Gestão de Ativos Circulantes), detalhando as necessidades do Centro de Ciências Tecnológicas (CCT) no controle de aluguel de projetores e chaves.

## 2. Proposta de Valor

O sistema permitirá automatizar o ciclo de vida dos ativos através de uma plataforma digital, integrada com a matrícula do professor. Espera-se garantir agilidade na retirada, conformidade via termos de responsabilidade digitais e controle rigoroso de integridade através de identificação por QR Code e checklists técnicos.

## 3. Descrição da Demanda

O sistema apoiará o CCT na **organização da gestão de ativos:**

* cadastro e manutenção de ativos com identificação única (QR Code);
* checkout mobile para retirada de equipamentos;
* geração e aceite obrigatório de Termo de Responsabilidade digital;
* checklist obrigatório de devolução para conferência de cabos e estado físico;
* rastreamento da localização do equipamento baseado na grade de salas do professor;
* e consultas gerenciais com histórico de empréstimos e auditoria.

Todo o processo será digital, contando com autenticação via Single Sign-On institucional.

## 4. Partes Interessadas

| Nome | Papel | Responsabilidades |
| :--- | :--- | :--- |
| Professores | Usuário principal | Buscar agilidade na retirada e consulta de disponibilidade. |
| Atendentes CCT | Operadores do sistema | Realizar checklists automatizados e eliminar uso de papéis. |
| Coordenação CCT | Gestores | Acompanhar auditorias, histórico de uso e controle patrimonial. |
| Equipe de TI - DTEC | Suporte / Desenvolvimento | Garantir infraestrutura segura e integração via SSO e APIs institucionais. |

## 5. Personas

### 5.1. Professor

* **Descrição:** Docente do CCT que realiza o aluguel de projetores e chaves para dar aulas em diferentes salas.
* **Objetivo:** Conseguir agilidade na retirada do equipamento e poder assinar o termo de responsabilidade de forma rápida e digital pelo celular.

### 5.2. Atendente CCT

* **Descrição:** Operador responsável pelo balcão de atendimento e liberação dos equipamentos de reserva técnica.
* **Objetivo:** Realizar inspeções visuais (checklists) com facilidade na entrega/devolução e saber exatamente onde e com quem estão os equipamentos.

### 5.3. Coordenação CCT

* **Descrição:** Gestores responsáveis pela infraestrutura e ativos do centro tecnológico.
* **Objetivo:** Consultar o histórico de uso dos equipamentos para tomada de decisão (aquisição, descarte, custo de manutenção) e manter auditoria rigorosa.

### 5.4. Equipe de TI - DTEC

* **Descrição:** Profissionais de tecnologia da universidade.
* **Objetivo:** Disponibilizar autenticação segura (SSO) e garantir o tráfego correto das informações de matrícula e grade de horários dos professores.

## 6. Necessidades e Funcionalidades

### Necessidade 1: Gerenciar Empréstimos e Devoluções

#### F1.1 Checkout Mobile

* **Descrição:** Permite realizar a retirada de ativos através do escaneamento do código (QR Code) pelo app.
* **Incluída**
* **Atores:** Professor
* **Frequência:** Alta
* **Valor:** Alto

#### F1.2 Termo de Responsabilidade

* **Descrição:** Gera aceite digital de responsabilidade de forma obrigatória no ato da retirada do projetor.
* **Incluída**
* **Atores:** Professor
* **Frequência:** Alta
* **Valor:** Alto

#### F1.3 Checklist de Devolução

* **Descrição:** Força a conferência de cabos, acessórios e estado físico do projetor no momento do retorno.
* **Incluída**
* **Atores:** Atendente CCT
* **Frequência:** Alta
* **Valor:** Alto

---

### Necessidade 2: Gestão de Inventário e Reparos

#### F2.1 Gestão de Inventário

* **Descrição:** Cadastro e manutenção de ativos com identificação única via QR Code.
* **Incluída**
* **Atores:** Atendente CCT, Coordenação CCT
* **Frequência:** Média
* **Valor:** Alto

#### F2.2 Troca de Projetor com Defeito / Permutação

* **Descrição:** Permite substituir projetores que apresentem defeito, alterando seu status para "Em Manutenção" ou "Aguardando Descarte".
* **Incluída**
* **Atores:** Atendente CCT
* **Frequência:** Média
* **Valor:** Alto

---

### Necessidade 3: Rastreamento e Gerenciamento

#### F3.1 Rastrear Projetor nas Salas

* **Descrição:** Permite saber a localização dos equipamentos integrando o sistema com as salas da grade do professor no horário do aluguel.
* **Incluída**
* **Atores:** Atendente CCT, Coordenação CCT
* **Frequência:** Alta
* **Valor:** Alto

#### F3.2 Consultar Projetor (Gerencial)

* **Descrição:** Acesso a dados de histórico de empréstimos, estimativa de vida útil de lâmpadas e histórico de manutenções para auditoria.
* **Incluída**
* **Atores:** Coordenação CCT
* **Frequência:** Média
* **Valor:** Alto

---

### Necessidade 4: Regras e Bloqueios

#### F4.1 Bloqueio por Inadimplência

* **Descrição:** Professores com ativos em atraso são impedidos pelo sistema de realizar novos empréstimos.
* **Incluída**
* **Atores:** Sistema
* **Frequência:** Baixa
* **Valor:** Alto

---

## 7. Arquitetura da Demanda

### Descrição da Arquitetura

O sistema GAC será composto pelas seguintes interações e camadas de acordo com o Diagrama de Sequências:

#### 1. Frontend (Interface Mobile/Web)

* Interface otimizada para uso em campo, de forma responsiva.
* Telas para escaneamento de QR Code (Checkout Mobile), aceite digital de termos e exibição de salas do professor.

---

#### 2. Backend GAC

Responsável pela lógica de negócio e regras do sistema:

* Módulo de Cadastro e geração de QR Code.
* Verificação de regras (ex: bloqueio de inadimplência, status ativo/em manutenção).
* Registro de empréstimos e devoluções com checklists.
* Painel de Auditoria e Relatórios.

---

#### 3. Integrações

* **API DTEC (Sistema Unifor):** Autenticação via Single Sign-On (SSO) institucional e consulta à grade de salas associada à matrícula do professor.

## Checklist de Validação do Documento de Visão

- [X] O objetivo está claro e alinhado ao problema/necessidade?
- [X] A proposta de valor é mensurável e relevante?
- [X] Todas as partes interessadas estão listadas com papéis definidos?
- [X] Existem pelo menos duas personas descritas?
- [X] Todas as necessidades e funcionalidades estão relacionadas a atores?
- [X] Há indicação de valor e frequência para cada funcionalidade?
- [X] A arquitetura está ilustrada (mesmo que de forma simples)?
- [X] O documento está escrito em linguagem clara e objetiva?