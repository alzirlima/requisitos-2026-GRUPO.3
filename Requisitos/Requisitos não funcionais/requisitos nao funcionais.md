# Especificação de Requisitos Não Funcionais

> **Especificação — Sistema GAC (Gestão de Ativos do CCT)**
>
>  Este documento registra os requisitos não funcionais do sistema GAC, definindo os padrões de qualidade, segurança e integração necessários para o controle de ativos circulantes (projetores e chaves) do Centro de Ciências Tecnológicas[cite: 87, 95].

## Histórico de Versões

| Data | Versão | Descrição | Autor |
| :--- | :--- | :--- | :--- |
| 2026 | 1.0 |  Criação inicial do documento de requisitos não funcionais para o GAC [cite: 88, 92] |  Francisco Alzir, João Gabriel, Lívia Maria, Rômulo Azevedo [cite: 90] |

## 1. Requisitos de Produto

### 1.1. Eficiência de Desempenho

#### 1.1.1. Comportamento temporal
 O tempo de resposta para validação de QR Codes e carregamento da grade de salas síncronas não deve ultrapassar 2 segundos sob condições normais de rede[cite: 144].

#### 1.1.2. Capacidade
 O sistema deve suportar acessos simultâneos de professores e atendentes do CCT sem lentidão, especialmente durante os intervalos e horários de pico nas trocas de turmas para evitar filas no balcão[cite: 96, 105].

#### 1.1.3. Uso de recursos
 O sistema deve operar de forma estável na infraestrutura da universidade, interagindo eficientemente com as APIs já existentes do sistema Unifor (DTEC)[cite: 171, 173].

### 1.2. Flexibilidade (portabilidade)

#### 1.2.1. Escalabilidade
 O sistema deve permitir o cadastro ilimitado de novos ativos (projetores, cabos, chaves), acompanhando o crescimento do inventário do CCT[cite: 114].

#### 1.2.2. Adaptabilidade
 A interface do usuário deve ser totalmente responsiva (Mobile-First), garantindo legibilidade e funcionamento fluido tanto em desktops quanto em smartphones e tablets utilizados em campo[cite: 101, 144].

#### 1.2.3. Instalabilidade
A solução deve ser facilmente acessível via navegador ou aplicativo móvel, não exigindo configurações complexas nos dispositivos pessoais dos professores.

### 1.3. Confiabilidade

#### 1.3.1. Disponibilidade
 O sistema deve manter alta disponibilidade durante todo o período letivo, garantindo que o fluxo de aulas não sofra atrasos por indisponibilidade da plataforma de empréstimos[cite: 96, 103].

#### 1.3.2. Tolerância a falhas
 O sistema deve prever tratamento de erros caso haja perda momentânea de conexão no momento do checkout mobile ou preenchimento do checklist de devolução[cite: 115, 117].

#### 1.3.3. Recuperabilidade
 Deve haver rotinas de backup que protejam os registros de movimentações e laudos técnicos contra perda de dados em caso de falhas[cite: 128].

### 1.4. Segurança

#### 1.4.1. Confidencialidade
 Dados de uso, métricas gerenciais e históricos de manutenções só devem ser acessados pelos perfis de Coordenação CCT e técnicos autorizados[cite: 105, 135].

#### 1.4.2. Integridade
 O sistema deve garantir a integridade e a imutabilidade dos históricos de Termos de Responsabilidade assinados para fins de auditorias jurídicas e financeiras[cite: 144].

#### 1.4.3. Autenticidade (autenticação)
 O sistema deve implementar controle de acesso e autenticação centralizada utilizando o protocolo Single Sign-On (SSO) institucional da universidade[cite: 144].

#### 1.4.4. Resistência
A comunicação entre o aplicativo móvel e a API do DTEC deve ser protegida para impedir o acesso indevido às grades de salas e dados dos docentes.

### 1.5. Privacidade

#### 1.5.1. Licitude
 O uso do e-mail do professor e de sua grade de salas baseia-se na necessidade de gerenciar a responsabilidade sobre equipamentos da universidade[cite: 100, 102].

#### 1.5.2. Finalidade
 Os dados extraídos do sistema DTEC devem ser usados exclusivamente para validar o empréstimo, preencher o termo digital e rastrear o ativo na sala de aula correta[cite: 101, 102, 103].

#### 1.5.3. Necessidade
 O sistema captura apenas as informações vitais para a transação: identificação do professor (e-mail institucional), ativo vinculado e salas associadas àquele horário[cite: 101, 102].

### 1.6. Capacidade de Interação (UX + usabilidade + acessibilidade)

#### 1.6.1. Facilidade de aprendizado
 A aplicação deve oferecer uma interface simples para reserva, minimizando o tempo necessário para o usuário entender como escanear o equipamento e confirmar o termo[cite: 109].

#### 1.6.2. Operabilidade
 A interface deve conter botões acessíveis em campo, adequados para o toque (touchscreen) no contexto ágil de retirada e devolução no balcão[cite: 144].

#### 1.6.3. Proteção contra erros do usuário
 O sistema deve forçar o preenchimento completo do checklist de devolução, não permitindo o encerramento do processo sem a conferência de todos os itens exigidos (cabos, controle, bolsa)[cite: 117].

### 1.7. Manutenibilidade

#### 1.7.1. Modularidade
 O sistema deve ser dividido em módulos claros: Autenticação, Gestão de Inventário, Empréstimo/Devolução e Painel Gerencial[cite: 151, 154].

#### 1.7.2. Analisabilidade
 Geração de alertas e relatórios de discrepância sempre que a leitura física de um ativo durante a ronda não coincidir com o banco de dados[cite: 134].

### 1.8. Compatibilidade

#### 1.8.1. Interoperabilidade
 A plataforma deve se integrar nativamente via API ao Sistema Unifor (DTEC) para retornar os dados de autenticação e a grade de horários[cite: 171, 173, 229].

### 1.9. Segurança Operacional (safety)

#### 1.9.1. Restrição operacional
 Professores inadimplentes (com ativos em atraso) devem ser bloqueados e impedidos pelo sistema de realizar novos empréstimos[cite: 146].

#### 1.9.2. Identificação de riscos
 Ativos com danos reportados devem ter seu status alterado automaticamente para "Em Manutenção" ou "Aguardando Descarte", bloqueando a máquina para novos aluguéis até o reparo técnico[cite: 130, 148, 149].

### 1.10. Adequação funcional

#### 1.10.1. Completude funcional
 O sistema deve contemplar todo o ciclo de vida do ativo: cadastro via QR Code, empréstimo, devolução, permutas, registros de defeitos, rondas físicas e dashboards gerenciais[cite: 114, 116, 123, 131, 133, 135].

## 2. Requisitos Externos

### 2.1. Regulatório
 A plataforma deve atender aos padrões de auditoria da Coordenação CCT, fornecendo relatórios transparentes de custos de manutenção versus aquisição e histórico de quem utilizou o equipamento por último[cite: 105, 109, 138].

## 3. Requisitos Organizacionais

### 3.1. Operacionais
 O sistema terá níveis distintos de permissão para seus atores: Professores (para retirada), Atendentes CCT (para operações de checklist) e Coordenação (para auditoria gerencial)[cite: 105].

### 3.2. Desenvolvimento
 O projeto terá seu repositório mantido no Github (`https://github.com/alzirlima/requisitos-2026-GRUPO.3`) para controle de versionamento pela equipe[cite: 91].
