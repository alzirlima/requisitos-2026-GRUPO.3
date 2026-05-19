# RELATÓRIO DE ELICITAÇÃO DE REQUISITOS: ENTREVISTA IN LOCO COM A COORDENAÇÃO
## Sistema GAC – Gestão de Ativos Circulantes (CCT/UNIFOR)

Este documento apresenta a consolidação e a análise técnica da entrevista de elicitação realizada com o principal *stakeholder* operacional do sistema, **Kildery (Coordenação de Apoio Técnico do CCT)**. A fim de capturar a real dimensão dos desafios diários, a entrevista foi conduzida no formato *in loco* **dentro de uma sala de aula ativa no Bloco J**, durante um momento de atendimento emergencial a um docente.

---

## 1. Metodologia de Elicitação e Contexto da Entrevista
A técnica adotada foi a **Entrevista de Contexto (Contextual Inquiry)** associada à **Análise de Protocolo Ativo**. Em vez de uma reunião formal em escritório, o analista acompanhou Kildery em sua rotina de campo pelos blocos do Centro de Ciências Tecnológicas (CCT) da UNIFOR.

A entrevista ocorreu especificamente em uma terça-feira, durante o intervalo crítico de troca de blocos (transição de turnos de aula), no momento exato em que Kildery solucionava uma falha técnica de projeção em uma sala de aula. Essa abordagem permitiu extrair as dores de governança, logística e segurança patrimonial diretamente do ambiente onde os problemas se manifestam.

---

## 2. Visão Unificada de Dores e Demandas (Perspectiva de Kildery)

Ao centralizar a visão operacional, Kildery mapeou os problemas sob três prismas que afetam diretamente o ecossistema do CCT, utilizando exemplos práticos observados na sala de aula durante a entrevista:

### 2.1. O Gargalo do Atendimento e a Fricção com o Corpo Docente
* **O Problema da Fila Física:** Olhando para os professores que aguardavam suporte, Kildery relatou: *"O maior gargalo hoje é o tempo. Na troca de blocos, dezenas de professores vêm ao balcão ao mesmo tempo. Assinar uma folha de papel física e rasurada gera uma fila que atrasa o início da aula em até 10 minutos. O professor fica estressado e nós ficamos sobrecarregados."*
* **A Falha de Identificação Jurídica:** Kildery apontou para o projetor conectado na mesa da sala de aula: *"Se esse professor precisar passar esse projetor para o colega que vai dar a próxima aula aqui, eles fazem isso informalmente de boca. No meu caderno físico, o primeiro professor continua como responsável. Se sumir um cabo HDMI ou o controle remoto no final do dia, eu não tenho como cobrar legalmente do verdadeiro culpado porque o registro em papel está defasado."*

### 2.2. O Desafio Logístico e Técnico da Equipe de Campo
* **A Conferência Visual Ineficiente na Devolução:** Segurando a bolsa do projetor, Kildery explicou o risco operacional: *"Quando o turno acaba, os professores devolvem os kits quase juntos. Minha equipe não consegue abrir bolsa por bolsa, ler um número de série minúsculo embaixo do projetor, contar se o cabo de energia, o cabo HDMI e o controle estão lá dentro, e testar se a lente está boa. A conferência é superficial por falta de tempo. Se um cabo voltar partido, só descobrimos na manhã seguinte quando outro professor vai usar."*
* **Discrepância de Localização:** *"Os projetores se movem como fantasmas pelo CCT. Professores trocam de sala por conveniência e levam o equipamento. Minha equipe passa horas correndo pelos blocos tentando adivinhar onde está o projetor de identificação X, porque o sistema manual não atualiza a posição geográfica do ativo em tempo real."*

### 2.3. O Controle Patrimonial e Gerencial (Nível de Coordenação)
* **O Custo Invisível do Desgaste de Lâmpadas:** Kildery detalhou a falta de manutenção preventiva: *"As lâmpadas dos projetores têm uma vida útil estrita medidada em horas. Como não há nenhum registro automatizado de quanto tempo cada aparelho ficou ligado, a lâmpada simplesmente queima no meio de uma aula importante. Isso interrompe a didática do CCT e me força a fazer uma manutenção corretiva de urgência, cujo custo de aquisição da peça é muito superior ao de uma substituição planejada."*
* **Inexistência de Indicadores de Ocupação:** *"Hoje eu não sei quais blocos demandam mais equipamentos, quais dias da semana são mais críticos ou quais aparelhos estão ociosos. Tomamos decisões de compra e alocação baseadas puramente em estimativas visuais, sem dados concretos."*

---

## 3. Requisitos de Automação Coletados na Sala de Aula

Diretamente da observação da dinâmica da sala de aula, Kildery consolidou as diretrizes para o desenvolvimento do Sistema GAC:

1. **Check-out e Identificação por QR Code:** Substituir a busca e digitação manual de séries por um escaneamento instantâneo do QR Code colado no ativo usando a câmera do celular.
2. **Autenticação Digital por E-mail Institucional:** Vincular o empréstimo ao e-mail do professor via integração síncrona com o Single Sign-On (SSO) da Dtec/UNIFOR, eliminando o papel.
3. **Mecanismo Sistêmico de Permutação:** Permitir que dois professores transfiram a responsabilidade do projetor entre si diretamente dentro da sala de aula através do aplicativo, exigindo o aceite digital do novo portador.
4. **Checklist de Vistoria com Registro Fotográfico:** Criar um fluxo obrigatório no aplicativo da equipe técnica para validar a presença de todos os itens do Kit (Projetor, Cabo de Força, Cabo HDMI, Controle e Bolsa), com capacidade de anexar fotos em caso de avarias.
5. **Rondas com Alertas de Discrepância:** Uma funcionalidade para que o técnico, ao passar pelas salas de aula, escaneie o QR Code e o sistema acuse imediatamente se aquele ativo deveria ou não estar naquela sala.
6. **Contador Cumulativo de Horas da Lâmpada:** O sistema deve cruzar o tempo logado de empréstimo e acumular no atributo do ativo, emitindo um alerta visual de cor âmbar no painel gerencial ao atingir 90% da vida útil prevista.

---

## 4. Matriz de Rastreabilidade Unificada

Esta matriz mapeia as dores diretas testemunhadas por Kildery durante a rotina na sala de aula e como o software irá solucioná-las:

| Contexto / Dor Observada por Kildery | Impacto no CCT | Solução Requisitada | Módulo de Destino (Arquitetura) |
| :--- | :--- | :--- | :--- |
| Lentidão e filas na troca de turno | Atraso no início das aulas | Autenticação via SSO com e-mail institucional | `🔒 Módulo de Segurança (SSO)` |
| Troca informal de aparelhos em sala | Insegurança jurídica e perda patrimonial | Fluxo de Permutação Direta síncrona via Mobile | `📝 Módulo de Empréstimos` |
| Verificação em massa ineficiente | Cabos e controles sumidos ou danificados | Checklist guiado obrigatório com fotos na devolução | `📝 Módulo Checklist Vistorias` |
| Aparelhos movidos sem registro | Desperdício de tempo da equipe técnica | Ronda de Auditoria com validação de sala física | `🕵️ Módulo Auditoria (Rondas)` |
| Queima inesperada de componentes | Manutenção corretiva cara e parada de aulas | Alerta preventivo baseado em horas de uso acumuladas | `📊 Motor Relatórios/Métricas` |
