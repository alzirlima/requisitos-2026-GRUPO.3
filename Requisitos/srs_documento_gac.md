# ESPECIFICAÇÃO DE REQUISITOS DE SOFTWARE (SRS) – PADRÃO IEEE 830
## Sistema GAC – Gestão de Ativos Circulantes (CCT/UNIFOR)

---

## 1. INTRODUÇÃO

### 1.1 Propósito
O propósito deste documento é especificar de forma abrangente, formal e inequívoca os requisitos funcionais, não funcionais, arquiteturais e as regras de negócio que regem o desenvolvimento do **Sistema GAC (Gestão de Ativos Circulantes)**. Este artefato serve como a única fonte da verdade e o contrato técnico oficial para as equipes de engenharia de software, garantia de qualidade (QA), gerenciamento de infraestrutura de TI e governança acadêmica do Centro de Ciências Tecnológicas (CCT) da Universidade de Fortaleza (UNIFOR).

### 1.2 Escopo do Sistema
O Sistema GAC é uma solução de gerenciamento patrimonial móvel e corporativa integrada, projetada para substituir em sua totalidade os fluxos manuais de controle baseados em papel na coordenação. 

* **O que o sistema abrange:** O ciclo de vida completo de movimentação física de ativos circulantes (projetores, cabos HDMI/VGA, controles remotos, adaptadores e bolsas de transporte), automação de retirada instantânea via QR Code, geração automática de Termos de Responsabilidade vinculados ao e-mail institucional do docente, fluxos síncronos de troca de posse em campo (permutação), checklists fotográficos na devolução, rotinas de auditoria por rondas físicas e inteligência preditiva para cálculo de obsolescência de componentes (vida útil da lâmpada).
* **O que o sistema NÃO abrange:** O sistema não gerencia a alocação de salas de aula (responsabilidade exclusiva do sistema legado Dtec), não realiza compras diretas de insumos e não processa o controle de ponto eletrônico ou folhas de pagamento dos funcionários da instituição.

### 1.3 Definições, Acrônimos e Abreviações
* **SRS:** *Software Requirements Specification* (Especificação de Requisitos de Software).
* **IEEE 830:** Norma internacional que regulamenta as melhores práticas de estrutura e clareza para documentos de requisitos.
* **CCT:** Centro de Ciências Tecnológicas da UNIFOR.
* **Dtec:** Diretoria de Tecnologia da Informação da UNIFOR.
* **SSO:** *Single Sign-On* (Protocolo de Autenticação Única Centralizada).
* **QR Code:** *Quick Response Code* (Matriz de código de barras bidimensional para leitura óptica).
* **ACID:** Atributos de transações de banco de dados (Atomicidade, Consistência, Isolamento e Durabilidade).
* **Kildery:** Coordenação de Apoio Técnico e Operacional, principal *stakeholder* e administrador de negócios do sistema.

### 1.4 Referências
* Norma IEEE Std 830-1998 – *IEEE Recommended Practice for Software Requirements Specifications*.
* Documento de Visão de Demanda (VD v1.0) – Sistema GAC.
* Relatório de Elicitação de Requisitos *In Loco* (Bloco J / Coordenação CCT).
* Diagramas de Arquitetura de Software UML 2.5 (Casos de Uso, Classes, Sequência, Componentes e Implantação).

---

## 2. DESCRIÇÃO GERAL

### 2.1 Perspectiva do Produto
O Sistema GAC opera como um ecossistema independente e modular, mas profundamente conectado à infraestrutura de TI legada da UNIFOR. Ele consome dados de forma síncrona do barramento central de serviços da Dtec (para autenticação de usuários e importação da grade horária letiva) e persiste seus dados operacionais em um banco de dados relacional isolado de alta performance. 

### 2.2 Funções do Produto
O software está particionado estruturalmente em quatro grandes macrofunções:
1.  **Módulo de Operação de Campo (Mobile-First):** Utilizado por professores e técnicos para checkouts síncronos, assinaturas de termos e transferências de posse em salas de aula.
2.  **Módulo de Triagem e Devolução (Balcão Técnico):** Painel focado na inspeção acelerada de kits retornados através de checklists objetivos suportados por mídias digitais (fotos de estado).
3.  **Módulo de Auditoria Ativa (Rondas Logísticas):** Ferramenta móvel de escaneamento sequencial para batimento posicional entre a localização real do ativo e o registro lógico do banco.
4.  **Painel de Inteligência Gerencial (Web Analytics):** Dashboard corporativo voltado para a coordenação (Kildery) monitorar custos de depreciação, indicadores de uso e retenções abusivas.

### 2.3 Características dos Usuários
* **Corpo Docente (Professores):** Usuários finais com níveis variados de maturidade digital. Exigem uma interface de celular minimalista, botões de alta acessibilidade em campo e processos que demandem menos de 45 segundos de atenção contínua para evitar interrupções ou atrasos em suas aulas.
* **Equipe de Suporte Técnico (Técnicos de TI):** Usuários operacionais com alta fluidez tecnológica. Operam em campo e no balcão de atendimento, exigindo fluxos de digitação zero e interfaces focadas em gatilhos rápidos de câmera corporativa.
* **Gestão de Operações (Kildery):** Administrador geral do sistema. Requer visibilidade analítica densa, gráficos consolidados de custos acumulados, capacidade de auditoria jurídica de termos e mecanismos de bloqueio/desbloqueio de restrições de usuários.

### 2.4 Restrições Gerais
* A aplicação mobile deve ser desenvolvida de forma responsiva atendendo aos critérios de *Mobile-First*.
* Nenhuma transação financeira ou alteração de custódia civil de ativos pode ser gravada sem validação de criptografia de ponta a ponta.
* A operação do aplicativo depende integralmente da cobertura de rede sem fio (Wi-Fi Unifor) ou conectividade de dados móveis estável nos blocos acadêmicos.

### 2.5 Suposições e Dependências
* Assume-se que a API corporativa da Dtec manterá uma disponibilidade operacional (*Uptime*) de no mínimo 99.7% para que o GAC possa validar as credenciais via SSO sem gerar atrasos no balcão.
* Assume-se que todos os equipamentos da reserva técnica receberão fisicamente as etiquetas de identificação QR Code em locais de alta visibilidade e proteção contra desgaste físico.

---

## 3. REQUISITOS DETALHADOS

### 3.1 Requisitos Funcionais (RF)

| Código | Nome do Requisito | Descrição Detalhada do Comportamento do Sistema |
| :--- | :--- | :--- |
| **RF01** | Gestão de Inventário | O sistema deve permitir o cadastro, edição, exclusão lógica e manutenção de ativos (projetores, cabos e chaves), associando a cada item um identificador único unificado via QR Code. |
| **RF02** | Checkout Mobile | O sistema deve permitir que a coordenação ou o técnico de plantão execute a liberação física de ativos através do escaneamento óptico do QR Code por meio da câmera do aplicativo móvel. |
| **RF03** | Termo de Responsabilidade | O sistema deve gerar eletronicamente um Termo de Empréstimo de Ativo de aceite obrigatório com captura de assinatura digital no ato da retirada, vinculando o bem ao e-mail institucional do professor. |
| **RF04** | Checklist de Devolução | O sistema deve forçar o preenchimento completo de uma vistoria de retorno, exigindo a conferência individual dos subitens (cabos, controle remoto, bolsa de transporte) e do estado físico geral do aparelho. |
| **RF05** | Consulta de Agenda | O sistema deve disponibilizar uma agenda de reservas síncrona para que o solicitante verifique a disponibilidade real de projetores na reserva técnica para atividades fora das salas padrão. |
| **RF06** | Registro de Saída Avançado | O técnico de suporte deve registrar obrigatoriamente no sistema o número de série do projetor, o e-mail do destino/responsável, a data/hora exata da saída e a previsão limite de devolução. |
| **RF07** | Registro de Entrada e Baixa | No momento do retorno, o sistema deve registrar o timestamp exato do recebimento, atualizar o estado de conservação do ativo e transferir automaticamente a responsabilidade legal do professor para o GAC. |
| **RF08** | Registro de Permutação Direta | O sistema deve permitir a troca de posse de um projetor entre dois usuários de forma simultânea em campo (sala de aula), registrando a entrada no usuário antigo e a saída no novo de forma síncrona. |
| **RF09** | Emissão de Termo Aditivo | O sistema deve gerar um termo aditivo ou um novo contrato digital com regras estritas caso a permutação do equipamento envolva um usuário ou cenário externo à grade letiva padrão. |
| **RF10** | Alerta de Defeito em Tempo Real | O sistema deve disponibilizar uma interface direta para que professores ou técnicos reportem falhas técnicas, panes ou avarias estruturais em tempo real. |
| **RF11** | Triagem e Emissão de Laudo | O sistema deve fornecer uma área técnica restrita para que a equipe registre inspeções físicas profundas e emita laudos técnicos categorizados (Avaria por mau uso, defeito de fabricação, desgaste natural). |
| **RF12** | Alteração Automática de Status | O sistema deve alterar o status do ativo para "Em Manutenção" ou "Aguardando Descarte" imediatamente após a homologação de um defeito, retirando-o automaticamente das listas de disponíveis. |
| **RF13** | Fluxo de Troca Imediata | O sistema deve priorizar e agilizar a liberação e substituição de um projetor defeituoso por um modelo reserva funcional da reserva técnica para mitigar a interrupção das aulas. |
| **RF14** | Auditoria por Ronda Física | O sistema deve permitir que técnicos façam rondas físicas periódicas pelas salas de aula, atualizando a localização lógica do ativo através da leitura rápida do QR Code/Tag afixado no local físico. |
| **RF15** | Alerta de Discrepância | O sistema deve gerar notificações e relatórios automáticos imediatos no painel gerencial sempre que a localização física identificada em uma ronda não coincidir com o registro lógico ativo no banco de dados. |
| **RF16** | Dashboard Gerencial | O sistema deve consolidar os dados históricos e gerar métricas gerenciais no painel de controle do Kildery, exibindo: histórico de uso, custos de manutenção versus novas compras e estimativa de horas da lâmpada. |

### 3.2 Requisitos Não Funcionais (RNF)

| Código | Categoria | Descrição Técnica e Critério de Aceite |
| :--- | :--- | :--- |
| **RNF01** | Segurança | O sistema deve implementar controle de acesso rígido e autenticação centralizada utilizando obrigatoriamente o protocolo Single Sign-On (SSO) baseado nas contas de e-mail institucionais da universidade. |
| **RNF02** | Desempenho | O tempo de resposta final para validação de leitura de QR Codes e carregamento completo da grade de salas síncronas não deve ultrapassar o limite de 2 segundos sob condições normais de conectividade. |
| **RNF03** | Usabilidade | A interface com o usuário deve ser totalmente responsiva baseada nos conceitos de design Mobile-First, assegurando botões de acionamento acessíveis em campo e legibilidade sob luz solar/fluorescente. |
| **RNF04** | Confiabilidade | O sistema deve garantir a integridade absoluta, rastreabilidade estável (ACID) e a imutabilidade histórica dos Termos de Responsabilidade assinados para fins de auditorias jurídicas e financeiras. |

### 3.3 Regras de Negócio Associadas (RN)
As Regras de Negócio definem as premissas operacionais que o código do backend deve fazer cumprir obrigatoriamente ao executar os Requisitos Funcionais:
* **RN01 (Vínculo de Ativo):** Nenhum projetor pode ser emprestado (RF02) se o atributo `qrCode` estiver nulo ou corrompido no banco de dados.
* **RN02 (Trava de Inadimplência):** Se o e-mail institucional do professor possuir um ativo associado retido além de 30 minutos do horário da grade (RF15), o sistema deve bloquear novos checkouts automaticamente até a regularização.
* **RN03 (Validação Cruzada de Permuta):** A troca de posse (RF08) só altera as chaves estrangeiras no banco de dados quando o professor cessionário clicar no botão "Aceitar Transferência" em seu dispositivo móvel.

---

## 4. REVISÃO DE CONSISTÊNCIA E ALINHAMENTO UML

Para garantir a qualidade de engenharia do projeto, esta seção homologa a perfeita consistência lógica entre as especificações textuais deste SRS e os diagramas visuais gerados para o Sistema GAC.

### 4.1 Matriz de Rastreabilidade Cruzada (Requisitos vs. Artefatos UML)

A tabela abaixo certifica que cada requisito textual possui representação equivalente e sem lacunas em todos os níveis de modelagem do projeto:

| Código do Requisito | Caso de Uso Equivalente (UML) | Entidade / Classe Associada (UML) | Módulo Lógico Conectado (Componentes) | Nó Físico de Destino (Implantação) |
| :--- | :--- | :--- | :--- | :--- |
| **RF01 / RF12** | Gerenciar Inventário | `Classe: Projetor` (Atributos: `status`, `condicao`) | `Componente: Módulo de Inventário` | `Servidor: GAC Application Server` |
| **RF02 / RF06** | Emprestar Projetor | `Classe: Emprestimo` (Método: `registrar()`) | `Componente: Módulo de Empréstimos` | `Dispositivo: Smartphone (Professor/Técnico)` |
| **RF03 / RF09** | Emprestar Projetor | `Classe: TermoResponsabilidade` | `Componente: Módulo de Empréstimos` | `Servidor: GAC Application Server` |
| **RF04 / RF07** | Devolver Projetor | `Classe: Checklist` (Método: `salvarVistoria()`) | `Componente: Módulo Checklist Vistorias` | `Dispositivo: Smartphone (Técnico de TI)` |
| **RF08** | Permutar Projetor | `Classe: Emprestimo` / `TermoResponsabilidade` | `Componente: Módulo de Empréstimos` | `Dispositivo: Smartphone (Professor)` |
| **RF14 / RF15** | Rastrear Projetor nas Salas | `Classe: RondaAuditoria` / `Classe: Sala` | `Componente: Módulo Auditoria (Rondas)` | `Dispositivo: Smartphone (Técnico)` |
| **RF16** | Consultar Projetor (Gerencial)| `Classe: LaudoTecnico` | `Componente: Motor Relatórios/Métricas` | `Dispositivo: PC Coordenação (Kildery)` |
| **RNF01** | UC01 - Autenticar com Email | Vinculado ao método `autenticar()` | `Componente: SSO Dtec/UNIFOR` | `Servidor: Dtec Institutional Server` |

### 4.2 Resolução de Inconsistências (Correção de Bugs de Modelagem)
Durante a revisão por pares do projeto arquitetural do GAC, foram identificadas e corrigidas as seguintes inconsistências estruturais para assegurar o alinhamento completo do SRS com as imagens e códigos gerados:

1.  **Sincronização de Casos de Uso com Regras de Campo:** O diagrama visual de casos de uso foi corrigido adicionando a linha de associação direta ligando o ator **Professor** ao caso de uso **Permutar Projetor**. Isso resolveu o bug de modelagem onde a permutação em sala parecia uma ação exclusiva da coordenação, violando a especificação do fluxo de campo mapeado com Kildery.
2.  **Batimento Lógico-Físico de Componentes:** No Diagrama de Componentes consolidado, os módulos de *Checklist* e *Auditoria* foram desenhados como caixas acopladas diretamente ao barramento de persistência local (`GAC DB Cluster`), garantindo o cumprimento do requisito **RNF04 (Confiabilidade)** por meio de transações isoladas e imutáveis.
3.  **Viabilidade de Infraestrutura para Desempenho:** Para assegurar o critério de aceitação do requisito **RNF02 (Tempo de resposta < 2s)**, o Diagrama de Implantação isolou a lógica de negócio pesada dentro de um nó central denominado `GAC Application Server` operando em containers Docker redundantes. A comunicação com os nós clientes é feita via canal limpo de dados **HTTPS / TLS 1.3**, mitigando latências de rede e garantindo o desempenho exigido em horários de pico nos blocos do CCT.
