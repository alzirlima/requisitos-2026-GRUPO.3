# ESPECIFICAÇÃO DE CASOS DE USO – SISTEMA GAC
## Centro de Ciências Tecnológicas (CCT/UNIFOR)

Este documento apresenta a especificação formal dos Casos de Uso do Sistema GAC (Gestão de Ativos Circulantes), estruturada estritamente de acordo com o padrão normativo de engenharia de software e totalmente alinhada ao Diagrama de Casos de Uso visual da solução.

---

## 1. Caso de Uso: UC01 - Autenticar com Email (Professor)

1. **Nome do Caso de Uso**
   Autenticar com Email (Professor)

2. **Determine o objetivo do caso de uso**
   Permitir que o Professor ou a Coordenação realize o acesso seguro à plataforma utilizando suas credenciais institucionais vinculadas ao e-mail corporativo.

3. **Classifique o caso de uso**
   Concreto.

4. **Descreva os atores**
   * **Professor:** Primário. Realiza a inserção do e-mail institucional e senha para acessar as funcionalidades mobile.
   * **Coordenação (Kildery):** Primário. Realiza o login na interface administrativa web para gerenciar o inventário.
   * **Sistema Dtec (Unifor):** Secundário. Solução externa que recebe as credenciais e valida o estado ativo do usuário na base corporativa.

5. **Descreva as pré-condições**
   O usuário deve possuir uma conta de e-mail institucional ativa e homologada pela Dtec.

6. **Descreva o fluxo principal**
   * **P1.** O caso de uso é iniciado quando o Professor ou a Coordenação (Kildery) acessa a aplicação e seleciona a opção de login.
   * **P2.** O sistema apresenta o formulário de login solicitando o e-mail institucional e a senha.
   * **P3.** O usuário preenche os campos com suas credenciais e seleciona a opção Entrar. **[E1]**
   * **P4.** O sistema envia os dados informados para validação síncrona junto ao Sistema Dtec (Unifor).
   * **P5.** O sistema recebe a confirmação positiva de autenticação e os dados de perfil do usuário. **[E2]**
   * **P6.** O sistema concede o acesso e direciona o usuário para a tela inicial de seu respectivo perfil.
   * **P7.** Encerrar caso de uso.

7. **Descreva os fluxos alternativos**
   Não se aplicam.

8. **Descreva os fluxos de exceção**
   * **E1. Campos obrigatórios não preenchidos**
       * E1.1 No passo P3, o sistema:
           * E1.1.1 Identifica que um ou mais campos obrigatórios estão em branco.
           * E1.1.2 Apresenta a mensagem **MSG_ERR_01** ("Preenchimento obrigatório").
           * E1.1.3 O sistema retorna ao passo P2.
   * **E2. Credenciais inválidas ou incorretas**
       * E2.1 No passo P5, o sistema:
           * E2.1.1 Recebe do Sistema Dtec (Unifor) o retorno de falha de autenticação.
           * E2.1.2 Apresenta a mensagem **MSG_ERR_02** ("E-mail ou senha incorretos").
           * E2.1.3 O sistema retorna ao passo P2.

9. **Descreva as pós-condições**
   O usuário é autenticado com sucesso e uma sessão segura é estabelecida no dispositivo.

10. **Descreva os requisitos não funcionais**
    * **RNF01 (Segurança):** A autenticação deve ser realizada de forma centralizada utilizando o protocolo Single Sign-On (SSO).

11. **Indica os pontos de extensão**
    Não se aplicam.

12. **Indica a frequência de utilização do caso de uso**
    Alta. Ocorre sempre que uma nova sessão expira ou quando o usuário abre o aplicativo pela primeira vez no dia.

---

## 2. Caso de Uso: Emprestar Projetor (com QR Code)

1. **Nome do Caso de Uso**
   Emprestar Projetor (com QR Code)

2. **Determine o objetivo do caso de uso**
   Permitir a retirada física e a vinculação de custódia de um projetor da reserva técnica ao e-mail institucional de um Professor.

3. **Classifique o caso de uso**
   Concreto.

4. **Descreva os atores**
   * **Professor:** Primário. Solicita a retirada do ativo e efetua a leitura do código em campo.
   * **Coordenação (Kildery):** Primário. Valida a entrega e supervisiona o processo de retirada no balcão da reserva técnica.

5. **Descreva as pré-condições**
   O projetor físico deve possuir uma etiqueta de identificação com QR Code cadastrada no sistema.

6. **Descreva o fluxo principal**
   * **P1.** O Professor ou a Coordenação (Kildery) inicia o caso de uso selecionando a opção Realizar Empréstimo.
   * **P2.** O sistema inclui obrigatoriamente o caso de uso "UC01 - Autenticar com Email (Professor)".
   * **P3.** O sistema aciona a câmera do dispositivo móvel e solicita a leitura do código do ativo.
   * **P4.** O usuário realiza o escaneamento do QR Code fixado na carcaça do projetor.
   * **P5.** O sistema valida o identificador do ativo no inventário de disponíveis. **[E1]**
   * **P6.** O sistema inclui o caso de uso "Consultar Grade" para recuperar as salas de aula associadas ao e-mail do Professor.
   * **P7.** O sistema apresenta o Termo de Responsabilidade Digital preenchido com os dados do kit e o cronograma de salas do dia.
   * **P8.** O Professor revisa os dados exibidos e realiza a Assinatura Digital do termo na tela do aplicativo. **[A1]**
   * **P9.** O sistema armazena o documento assinado, altera o status do projetor para "Emprestado" e exibe a confirmação **MSG_SUC_01** ("Empréstimo autorizado com sucesso").
   * **P10.** Encerrar caso de uso.

7. **Descreva os fluxos alternativos**
   * **A1. Cancelamento do empréstimo pelo solicitante**
       * A1.1 No passo P8, o Professor opta por não assinar o termo e seleciona a opção Cancelar.
       * A1.2 O sistema invalida a operação de checkout e apresenta a mensagem **MSG_INF_01** ("Operação cancelada pelo usuário").
       * A1.3 Encerrar caso de uso.

8. **Descreva os fluxos de exceção**
   * **E1. Equipamento indisponível para empréstimo**
       * E1.1 No passo P5, o sistema:
           * E1.1.1 Identifica que o ativo lido possui o status "Em Manutenção" ou "Aguardando Descarte".
           * E1.1.2 Apresenta a mensagem **MSG_ERR_03** ("Ativo indisponível para empréstimo no momento").
           * E1.1.3 O sistema retorna ao passo P3.

9. **Descreva as pós-condições**
   A responsabilidade de guarda do projetor é transferida para o e-mail do professor e o ativo fica indisponível para novas reservas.

10. **Descreva os requisitos não funcionais**
    * **RNF02 (Desempenho):** O tempo para validação do código e carregamento do termo não deve ultrapassar 2 segundos.
    * **RNF04 (Confiabilidade):** Garantia de integridade e imutabilidade do histórico do Termo de Responsabilidade assinado.

11. **Indica os pontos de extensão**
    Não se aplicam.

12. **Indica a frequência de utilização do caso de uso**
    Alta. Apresenta picos intensos nos 15 minutos anteriores ao início de cada bloco de aulas do CCT.

---

## 3. Caso de Uso: Devolver Projetor (com Checklist)

1. **Nome do Caso de Uso**
   Devolver Projetor (com Checklist)

2. **Determine o objetivo do caso de uso**
   Registrar a devolução física do equipamento na reserva técnica e avaliar o estado dos componentes que integram o kit antes de dar a baixa de responsabilidade.

3. **Classifique o caso de uso**
   Concreto.

4. **Descreva os atores**
   * **Coordenação (Kildery):** Primário. Inspeciona fisicamente o kit, preenche os dados cadastrais da devolução e encerra a custódia.

5. **Descreva as pré-condições**
   O projetor devolvido deve constar previamente com o status lógico de "Emprestado" associado a um usuário no banco de dados.

6. **Descreva o fluxo principal**
   * **P1.** O caso de uso inicia quando a Coordenação (Kildery) seleciona a opção Registrar Devolução.
   * **P2.** O sistema solicita o escaneamento do QR Code do equipamento que está retornando.
   * **P3.** A Coordenação (Kildery) realiza a leitura do QR Code fixado na bolsa ou carcaça do projetor.
   * **P4.** O sistema localiza o registro do empréstimo correspondente e exibe na tela o formulário de Checklist de Devolução.
   * **P5.** A Coordenação (Kildery) confere a presença e a integridade de todos os acessórios (cabos, controle e bolsa) e marca as opções em conformidade. **[E1]**
   * **P6.** A Coordenação (Kildery) seleciona a opção Finalizar Devolução.
   * **P7.** O sistema atualiza o status do ativo para "Disponível", encerra o vínculo legal com o e-mail do professor e exibe a mensagem **MSG_SUC_02** ("Devolução concluída com sucesso").
   * **P8.** Encerrar caso de uso.

7. **Descreva os fluxos alternativos**
   Não se aplicam.

8. **Descreva os fluxos de exceção**
   * **E1. Avaria identificada ou acessórios faltantes no kit**
       * E1.1 No passo P5, a Coordenação (Kildery) identifica que o kit está incompleto ou danificado e marca a irregularidade.
       * E1.2 O sistema abre um campo obrigatório para justificativa em texto e aciona a câmera para captura de registro fotográfico do dano.
       * E1.3 O sistema encerra o empréstimo, altera o status do projetor para "Em Manutenção" e gera uma pendência administrativa vinculada ao e-mail do professor portador.
       * E1.4 O sistema apresenta a mensagem **MSG_ALERTA_01** ("Devolução registrada com restrições técnicas") e segue para o passo P8.

9. **Descreva as pós-condições**
   A custódia legal do professor é encerrada e o status físico real do patrimônio é atualizado de forma auditável.

10. **Descreva os requisitos não funcionais**
    * **RNF03 (Usabilidade):** Interface simplificada com campos de seleção rápida para agilizar a triagem no balcão de atendimento.

11. **Indica os pontos de extensão**
    Não se aplicam.

12. **Indica a frequência de utilização do caso de uso**
    Alta. Concentrada maciçamente nos horários de término das aulas e fechamento dos turnos acadêmicos.

---

## 4. Caso de Uso: Permutar Projetor

1. **Nome do Caso de Uso**
   Permutar Projetor

2. **Determine o objetivo do caso de uso**
   Permitir a transferência direta de posse e responsabilidade legal de um projetor entre dois professores em campo, sem a necessidade de retorno físico à coordenação.

3. **Classifique o caso de uso**
   Concreto.

4. **Descreva os atores**
   * **Professor:** Primário. O docente portador atual (cedente) e o novo docente (cessionário) interagem de forma ativa para realizar a transferência.
   * **Coordenação (Kildery):** Primário. Ator que monitora passivamente a movimentação gerencial por meio do dashboard.

5. **Descreva as pré-condições**
   O professor cedente deve possuir um empréstimo ativo e regularizado em seu nome para o equipamento selecionado.

6. **Descreva o fluxo principal**
   * **P1.** O Professor portador do ativo seleciona a opção Transferir Equipamento em Sala no aplicativo móvel.
   * **P2.** O sistema solicita o identificador de e-mail institucional do novo responsável.
   * **P3.** O Professor digita o e-mail institucional do professor que receberá o kit de ativos.
   * **P4.** O sistema valida a conta e envia uma notificação síncrona com o Termo Aditivo para o dispositivo móvel do professor destino. **[E1]**
   * **P5.** O novo Professor abre a notificação em seu aplicativo móvel e seleciona a opção Aceitar Transferência. **[A1]**
   * **P6.** O sistema encerra o empréstimo do professor antigo e abre um novo registro de custódia vinculado ao e-mail institucional do novo portador.
   * **P7.** O sistema envia a confirmação de sucesso **MSG_SUC_03** ("Permutação homologada com sucesso") para ambos os docentes.
   * **P8.** Encerrar caso de uso.

7. **Descreva os fluxos alternativos**
   * **A1. Rejeição da transferência pelo destinatário**
       * A1.1 No passo P5, o novo Professor opta por não receber o ativo e seleciona a opção Recusar.
       * A1.2 O sistema cancela o processo e envia um alerta para o professor cedente com a mensagem **MSG_ALERTA_02** ("Transferência recusada pelo destinatário").
       * A1.3 A responsabilidade legal e civil do projetor permanece sob a custódia inalterada do professor original.
       * A1.4 Encerrar caso de uso.

8. **Descreva os fluxos de exceção**
   * **E1. Destinatário inválido ou bloqueado por inadimplência**
       * E1.1 No passo P4, o sistema identifica que o e-mail inserido está incorreto ou bloqueado por pendências pendentes na coordenação.
       * E1.2 O sistema apresenta para o emissor a mensagem de erro **MSG_ERR_04** ("O destinatário informado está inelegível para transferência").
       * E1.3 O sistema retorna ao passo P2.

9. **Descreva as pós-condições**
   A custódia do bem patrimonial é alterada e atualizada no histórico posicional do inventário sem passar pela coordenação física.

10. **Descreva os requisitos não funcionais**
    * **RNF02 (Desempenho):** O processamento da transferência mútua das chaves de banco de dados deve ocorrer em menos de 2 segundos.

11. **Indica os pontos de extensão**
    Não se aplicam.

12. **Indica a frequência de utilização do caso de uso**
    Moderada. Ocorre tipicamente durante as transições de professores que lecionam matérias distintas de forma sequencial na mesma sala física.

---

## 5. Caso de Uso: Trocar Projetor com Defeito

1. **Nome do Caso de Uso**
   Trocar Projetor com Defeito

2. **Determine o objetivo do caso de uso**
   Agilizar a substituição imediata de um equipamento que apresentou mau funcionamento por um modelo reserva funcional da reserva técnica, minimizando a interrupção das atividades didáticas.

3. **Classifique o caso de uso**
   Concreto.

4. **Descreva os atores**
   * **Professor:** Primário. Comunica a falha técnica em tempo real através de seu dispositivo móvel.
   * **Coordenação (Kildery):** Primário. Recebe o alerta técnico, separa um equipamento reserva, realiza a triagem e homologa a substituição.

5. **Descreva as pré-condições**
   O professor solicitante deve estar com um empréstimo ativo associado ao projetor que apresentou a falha.

6. **Descreva o fluxo principal**
   * **P1.** O Professor acessa os detalhes do empréstimo ativo no app móvel e seleciona a opção Notificar Defeito.
   * **P2.** O sistema solicita a descrição sumária do problema e a confirmação do envio.
   * **P3.** O Professor preenche as informações e seleciona a opção Enviar Alerta.
   * **P4.** O sistema altera automaticamente o status do projetor danificado para "Em Manutenção" e emite um chamado prioritário na tela de gerenciamento da Coordenação (Kildery).
   * **P5.** A Coordenação (Kildery) separa um novo projetor funcional da reserva técnica e seleciona a opção Iniciar Substituição de Emergência no painel.
   * **P6.** O sistema aciona o fluxo de checkout e solicita a leitura do QR Code do novo equipamento.
   * **P7.** A Coordenação (Kildery) escaneia o QR Code do novo projetor de reserva.
   * **P8.** O sistema encerra o empréstimo do ativo com defeito sem penalidades e abre um novo empréstimo para o novo ativo sob o e-mail do professor.
   * **P9.** O sistema exibe para a coordenação a mensagem **MSG_SUC_05** ("Substituição concluída. Novo ativo vinculado").
   * **P10.** Encerrar caso de uso.

7. **Descreva os fluxos alternativos**
   Não se aplicam.

8. **Descreva os fluxos de exceção**
   Não se aplicam.

9. **Descreva as pós-condições**
   O equipamento defeituoso é bloqueado para manutenção técnica e o professor recebe um novo equipamento regularizado para dar continuidade à aula.

10. **Descreva os requisitos não funcionais**
    * **RNF03 (Usabilidade):** Interface simplificada com botões grandes de alerta de pane para agilizar o acionamento em sala de aula.

11. **Indica os pontos de extensão**
    Não se aplicam.

12. **Indica a frequência de utilização do caso de uso**
    Baixa. Ocorre de forma eventual e corretiva mediante falhas físicas de hardware ou queima de lâmpadas.

---

## 6. Caso de Uso: Consultar Projetor (Gerencial)

1. **Nome do Caso de Uso**
   Consultar Projetor (Gerencial)

2. **Determine o objetivo do caso de uso**
   Disponibilizar à gestão da coordenação um painel de controle contendo dados analíticos consolidados sobre o inventário, histórico de uso, custos e vida útil dos equipamentos.

3. **Classifique o caso de uso**
   Concreto.

4. **Descreva os atores**
   * **Coordenação (Kildery):** Primário. Acessa a interface administrativa para visualizar métricas, emitir relatórios e tomar decisões de compra/manutenção.
   * **Sistema Dtec (Unifor):** Secundário. Cede dados consolidados históricos para cruzamento e geração de relatórios de auditoria.

5. **Descreva as pré-condições**
   O usuário da Coordenação (Kildery) deve possuir privilégios administrativos ativos associados ao seu login de e-mail corporativo.

6. **Descreva o fluxo principal**
   * **P1.** A Coordenação (Kildery) seleciona a opção Dashboard Gerencial na plataforma web do sistema.
   * **P2.** O sistema carrega os dados históricos em tempo real do banco de dados relacional.
   * **P3.** O sistema apresenta gráficos consolidados exibindo taxas de ocupação, custos acumulados de manutenção e estimativa de horas de uso das lâmpadas.
   * **P4.** A Coordenação (Kildery) aplica filtros por Bloco Acadêmico e seleciona a opção Exportar Relatório de Retenções.
   * **P5.** O sistema processa o arquivo consolidado e disponibiliza o download do documento em formato digital auditável.
   * **P6.** Encerrar caso de uso.

7. **Descreva os fluxos alternativos**
   Não se aplicam.

8. **Descreva os fluxos de exceção**
   Não se aplicam.

9. **Descreva as pós-condições**
   Os relatórios operacionais e métricas gerenciais são gerados e disponibilizados sem alterações no estado dos ativos do inventário.

10. **Descreva os requisitos não funcionais**
    Não se aplicam.

11. **Indica os pontos de extensão**
    Não se aplicam.

12. **Indica a frequência de utilização do caso de uso**
    Baixa a moderada. Utilizado rotineiramente para fechamentos de relatórios mensais ou planejamentos semestrais de infraestrutura de ativos do CCT.

---

## 7. Caso de Uso: Rastrear Projetor nas Salas

1. **Nome do Caso de Uso**
   Rastrear Projetor nas Salas

2. **Determine o objetivo do caso de uso**
   Permitir o monitoramento contínuo da localização física real dos projetores distribuídos nos blocos didáticos do CCT através de rondas periódicas de auditoria.

3. **Classifique o caso de uso**
   Concreto.

4. **Descreva os atores**
   * **Coordenação (Kildery):** Primário. Agente técnico que executa as vistorias físicas de mapeamento geográfico das salas de aula em campo.

5. **Descreva as pré-condições**
   As salas de aula físicas auditadas devem conter etiquetas identificadoras com QR Code ativos e legíveis fixadas nas mesas ou paredes.

6. **Descreva o fluxo principal**
   * **P1.** A Coordenação (Kildery) inicia o processo no app móvel selecionando a opção Iniciar Ronda de Auditoria.
   * **P2.** O sistema solicita o escaneamento do QR Code identificador da sala física.
   * **P3.** O usuário realiza a leitura do QR Code fixado na estrutura interna da sala de aula.
   * **P4.** O sistema valida o código da sala e solicita o escaneamento do QR Code do projetor em funcionamento no local.
   * **P5.** O usuário realiza o escaneamento do QR Code presente na carcaça do projetor alocado.
   * **P6.** O sistema efetua o cruzamento síncrono dos dados lidos com a grade ativa de empréstimos do banco de dados. **[E1]**
   * **P7.** O sistema valida a perfeita conformidade de localização do ativo e grava o log de auditoria bem-sucedido no histórico do patrimônio.
   * **P8.** O sistema apresenta a mensagem **MSG_SUC_04** ("Auditoria de ambiente concluída com sucesso").
   * **P9.** Encerrar caso de uso.

7. **Descreva os fluxos alternativos**
   Não se aplicam.

8. **Descreva os fluxos de exceção**
   * **E1. Discrepância posicional do ativo identificada**
       * E1.1 No passo P6, o sistema detecta que o projetor escaneado deveria estar alocado em outro bloco ou sob empréstimo de um professor lotado em outra sala.
       * E1.1.1 O sistema gera automaticamente um Alerta de Inconsistência no painel administrativo central.
       * E1.1.2 O sistema atualiza emergencialmente a posição lógica do ativo no banco de dados para a localização real encontrada em campo para resguardar a rastreabilidade do patrimônio.
       * E1.1.3 O sistema apresenta o aviso **MSG_ALERTA_03** ("Discrepância de localização registrada e reportada") e segue para o passo P9.

9. **Descreva as pós-condições**
   A localização lógica atual do patrimônio é sincronizada de forma idêntica à realidade física constatada nas salas de aula durante a auditoria.

10. **Descreva os requisitos não funcionais**
    * **RNF03 (Usabilidade):** O aplicativo móvel deve operar com fluxo fluido em modo Mobile-First para agilizar a leitura consecutiva de códigos em campo.

11. **Indica os pontos de extensão**
    Não se aplicam.

12. **Indica a frequência de utilização do caso de uso**
    Semanal ou quinzenal. Executado de forma amostral e rotineira pela coordenação para coibir perdas operacionais de periféricos e permutações informais.
