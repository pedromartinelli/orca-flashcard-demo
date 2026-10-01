# Levantamento de requisitos do produto — Plataforma de estudos com flashcards

> Status: rascunho para validação ponto a ponto.
>
> Documento de origem: `PLANEJAMENTO_CONCEITUAL.md`.
>
> Escopo: produto web responsivo, com foco no MVP.

## 1. Objetivo do produto

Oferecer uma plataforma de aprendizagem adaptativa baseada em flashcards que permita ao usuário organizar conteúdos, realizar sessões de estudo, acompanhar sua evolução e receber recomendações orientadas por desempenho, tempo de resposta, necessidade de revisão e eventos futuros.

O produto deverá ajudar o usuário a decidir o que estudar e quando revisar, sem retirar sua liberdade de planejar sessões manualmente.

## 2. Objetivos do MVP

- Permitir que o usuário crie e organize seu próprio conteúdo de estudo.
- Oferecer sessões manuais e recomendadas.
- Registrar acertos, erros e tempo de resposta.
- Adaptar recomendações ao desempenho recente do usuário.
- Evitar o esquecimento de conteúdos já consolidados.
- Permitir a preparação orientada para provas, concursos e outros eventos.
- Apresentar histórico e métricas por card, tema, grupo e evento.
- Explicar as recomendações sem interferir no momento de resposta do card.

## 3. Escopo e premissas

- O produto inicial será uma aplicação web responsiva para dispositivos móveis.
- Cada conta possuirá dados de estudo privados e independentes.
- A avaliação inicial será feita pelo próprio usuário, por meio de `Acertei` ou `Errei`.
- A resposta será mental; não haverá campo de resposta nem correção por inteligência artificial no MVP.
- Perguntas e respostas aceitarão texto formatado e fórmulas matemáticas.
- Um card poderá pertencer a vários temas sem ser duplicado.
- O histórico não expirará automaticamente enquanto a conta estiver ativa.
- Regras numéricas do motor de recomendação serão especificadas em documento próprio após a validação destes requisitos.

## 4. Glossário

| Termo | Definição |
|---|---|
| Coleção | Contêiner de mais alto nível usado para organizar um objetivo ou conjunto de estudos. |
| Tema | Classificação de conteúdo dentro de uma coleção. Um card pode pertencer a vários temas. |
| Grupo | Subdivisão opcional de um tema. |
| Card | Unidade de estudo composta inicialmente por pergunta e resposta. |
| Estado de aprendizagem | Situação atual do card: `Novo`, `Em aprendizado`, `Em consolidação`, `Consolidado` ou `Revisão pendente`. |
| Evento | Objetivo com data definida, como prova, concurso, certificação ou apresentação. |
| Sessão | Conjunto de cards estudados em uma mesma execução. |
| Sessão manual | Sessão cujo escopo é escolhido pelo usuário. |
| Sessão recomendada | Sessão composta automaticamente pelo sistema. |
| Registro de estudo | Resultado de uma interação com um card, incluindo avaliação e tempo de resposta. |
| Revisão pendente | Estado de um card que precisa reaparecer para reduzir o risco de esquecimento. |

## 5. Atores

### 5.1 Usuário não autenticado

Pode criar uma conta, autenticar-se e recuperar o acesso à conta.

### 5.2 Usuário autenticado

Pode gerenciar seu conteúdo, eventos, sessões, preferências, histórico e conta.

## 6. Requisitos funcionais

### 6.1 Autenticação e conta

#### RF-AUT-001 — Criar conta

O sistema deverá permitir que uma pessoa crie uma conta utilizando as credenciais suportadas pelo MVP.

Critérios de aceitação:

- O sistema valida os campos obrigatórios.
- Não permite duas contas com o mesmo identificador de acesso.
- Informa de forma compreensível quando o cadastro não puder ser concluído.
- Após o cadastro bem-sucedido, o usuário poderá acessar sua conta.

#### RF-AUT-002 — Autenticar-se

O sistema deverá permitir que o usuário entre utilizando credenciais válidas.

Critérios de aceitação:

- Credenciais válidas concedem acesso aos dados do usuário.
- Credenciais inválidas não concedem acesso.
- O erro não deverá revelar informações sensíveis sobre a conta.

#### RF-AUT-003 — Encerrar sessão

O sistema deverá permitir que o usuário encerre sua sessão autenticada.

#### RF-AUT-004 — Recuperar acesso

O sistema deverá oferecer um processo de recuperação de acesso à conta.

#### RF-AUT-005 — Gerenciar perfil e preferências

O usuário deverá poder consultar e alterar os dados e as preferências disponibilizados pelo MVP.

#### RF-AUT-006 — Excluir conta

O usuário deverá poder solicitar a exclusão de sua conta e de seus dados, mediante confirmação explícita.

#### RF-AUT-007 — Isolar dados por usuário

O usuário deverá acessar exclusivamente suas próprias coleções, cards, sessões, eventos e métricas.

### 6.2 Organização do conteúdo

#### RF-ORG-001 — Gerenciar coleções

O usuário deverá poder criar, visualizar, renomear, arquivar, restaurar e excluir coleções.

#### RF-ORG-002 — Gerenciar temas

O usuário deverá poder criar, visualizar, renomear, reorganizar, arquivar, restaurar e excluir temas.

#### RF-ORG-003 — Gerenciar grupos

O usuário deverá poder criar, visualizar, renomear, reorganizar, arquivar, restaurar e excluir grupos dentro de temas.

#### RF-ORG-004 — Proteger conteúdos relacionados

Uma coleção, um tema ou um grupo não poderá ser excluído de maneira definitiva sem que o sistema informe o impacto sobre os cards e o histórico relacionados.

#### RF-ORG-005 — Navegar pela hierarquia

O usuário deverá conseguir navegar pela estrutura `Coleção → Tema → Grupo → Card` e visualizar a quantidade de cards em cada nível.

### 6.3 Gestão de cards

#### RF-CAR-001 — Criar card

O usuário deverá poder criar um card informando:

- Pergunta.
- Resposta.
- Ao menos uma associação organizacional válida.
- Temas, grupos ou eventos relacionados, quando aplicável.

Ao ser criado, o card deverá receber o estado `Novo`.

#### RF-CAR-002 — Formatar conteúdo

Pergunta e resposta deverão aceitar:

- Parágrafos.
- Listas.
- Alternativas.
- Destaques.
- Quebras de linha.
- Fórmulas matemáticas em linha e em blocos destacados.

#### RF-CAR-003 — Visualizar card

A visualização de um card deverá apresentar, no mínimo:

- Pergunta e resposta.
- Estado atual de aprendizagem.
- Coleções, temas e grupos relacionados.
- Eventos relacionados.
- Resumo de desempenho, quando houver histórico.
- Data da última revisão, quando houver.

#### RF-CAR-004 — Editar card

O usuário deverá poder alterar o conteúdo e as associações de um card.

Ao alterar pergunta ou resposta, o sistema deverá perguntar se a mudança representa:

- Apenas uma correção, preservando o progresso atual; ou
- Um novo conteúdo, reiniciando o progresso de aprendizagem.

#### RF-CAR-005 — Versionar alteração substancial

Quando o usuário indicar que a edição representa novo conteúdo, o sistema deverá:

- Preservar o histórico anterior.
- Preservar a versão anterior para consulta.
- Iniciar uma nova etapa de aprendizagem.
- Desconsiderar o desempenho antigo no cálculo principal da nova versão.
- Definir o estado da nova versão como `Novo` ou `Em aprendizado`, conforme a regra que vier a ser estabelecida.

#### RF-CAR-006 — Associar card a vários temas

O usuário deverá poder associar o mesmo card a mais de um tema sem criar cópias.

Critérios de aceitação:

- O card possui um único histórico.
- Uma resposta atualiza as métricas de todos os temas associados.
- O card aparece apenas uma vez quando vários critérios da mesma sessão o selecionarem.

#### RF-CAR-007 — Duplicar card

O usuário deverá poder criar um novo card a partir de uma cópia, sem copiar o histórico de aprendizagem do card original.

#### RF-CAR-008 — Arquivar e restaurar card

O usuário deverá poder arquivar um card e restaurá-lo posteriormente.

Critérios de aceitação:

- O arquivamento preserva o histórico.
- Um card arquivado não participa de novas recomendações.
- A restauração recupera o card e seu histórico.

#### RF-CAR-009 — Excluir e recuperar card

O usuário deverá poder mover um card para uma área de itens excluídos, restaurá-lo e solicitar sua exclusão definitiva.

#### RF-CAR-010 — Pesquisar e filtrar cards

O usuário deverá poder pesquisar e filtrar cards, ao menos por:

- Texto da pergunta ou resposta.
- Coleção.
- Tema.
- Grupo.
- Evento.
- Estado de aprendizagem.
- Situação ativa ou arquivada.

#### RF-CAR-011 — Realizar ações em lote

O usuário deverá poder selecionar vários cards para alterar suas associações, arquivá-los, restaurá-los ou excluí-los.

### 6.4 Sessão manual

#### RF-SEM-001 — Planejar sessão manual

O usuário deverá poder montar uma sessão escolhendo uma ou mais fontes:

- Cards específicos.
- Temas.
- Grupos.
- Eventos.

#### RF-SEM-002 — Incluir evento na sessão

Ao escolher `Incluir evento na sessão`, os cards relacionados ao evento deverão entrar no conjunto de candidatos.

#### RF-SEM-003 — Eliminar duplicidades

Se um card for selecionado por mais de uma fonte, deverá aparecer uma única vez no conjunto da sessão, salvo quando o usuário habilitar repetição.

#### RF-SEM-004 — Definir quantidade de cards

O usuário deverá poder escolher a quantidade de cards da sessão, respeitando a quantidade de cards selecionados individualmente, cuja inclusão é garantida.

#### RF-SEM-005 — Ordenar a sessão

O usuário deverá poder escolher entre a ordem recomendada pelo sistema e uma ordem aleatória.

#### RF-SEM-006 — Configurar repetição

O usuário deverá poder definir se cards poderão se repetir durante a mesma sessão.

#### RF-SEM-007 — Visualizar resumo antes de iniciar

Antes do início, o sistema deverá mostrar:

- Quantidade prevista de cards.
- Temas, grupos e eventos contemplados.
- Critérios utilizados para formar a sessão.
- Avisos relevantes sobre limitações da seleção.

A duração estimada não fará parte do MVP.

### 6.5 Sessão recomendada

#### RF-SER-001 — Gerar sessão recomendada

O sistema deverá gerar uma sessão recomendada sempre que houver cards ativos elegíveis.

#### RF-SER-002 — Considerar desempenho

A recomendação deverá considerar, nesta ordem conceitual:

1. Taxa de acerto, com maior peso para resultados recentes.
2. Tempo de resposta relativo ao próprio usuário e ao histórico do card.
3. Tempo desde a última revisão.
4. Prioridade e proximidade dos eventos.
5. Quantidade de evidências existentes sobre o card.

#### RF-SER-003 — Tratar cards novos

Cards sem histórico deverão ser introduzidos gradualmente e receber prioridade suficiente para iniciar sua aprendizagem.

#### RF-SER-004 — Proteger contra esquecimento

Cards com bom desempenho deverão voltar a ser recomendados quando passarem tempo suficiente sem revisão.

#### RF-SER-005 — Evitar concentração excessiva

O sistema deverá evitar, quando possível:

- Repetir imediatamente o mesmo card.
- Concentrar toda a sessão em um único tema sem justificativa.
- Preencher toda a sessão apenas com cards de dificuldade elevada.

Essa regra poderá ser sobreposta pelo foco explícito de um evento de alta prioridade.

#### RF-SER-006 — Explicar recomendações

O sistema deverá disponibilizar, antes ou depois da sessão e na gestão dos cards, os motivos das recomendações.

Exemplos:

- Erros recentes.
- Tempo de resposta elevado.
- Revisão pendente.
- Poucas revisões realizadas.
- Associação com evento prioritário.

As explicações não deverão interromper nem disputar atenção com a apresentação da pergunta durante a sessão.

#### RF-SER-007 — Informar foco da sessão

Quando a sessão estiver dedicada a um evento, o sistema deverá informar claramente o foco e a prioridade correspondente.

Exemplo:

> **Sessão focada no evento “Prova de Cálculo”, definido com prioridade alta.**

### 6.6 Execução da sessão

#### RF-SES-001 — Apresentar pergunta

O sistema deverá apresentar inicialmente a pergunta sem revelar a resposta.

#### RF-SES-002 — Revelar resposta

O usuário deverá poder revelar a resposta quando considerar que concluiu sua tentativa mental.

#### RF-SES-003 — Registrar tempo de resposta

O sistema deverá registrar o tempo utilizado pelo usuário para responder mentalmente ao card.

#### RF-SES-004 — Registrar autoavaliação

Após revelar a resposta, o usuário deverá marcar `Acertei` ou `Errei` antes de avançar.

#### RF-SES-005 — Salvar progresso continuamente

Cada resposta concluída deverá ser persistida sem depender da finalização de toda a sessão.

#### RF-SES-006 — Pausar e retomar

O usuário deverá poder pausar uma sessão e retomá-la posteriormente sem perder respostas já registradas.

O tempo em pausa não deverá ser contabilizado como tempo de resposta.

#### RF-SES-007 — Abandonar sessão

O usuário deverá poder encerrar uma sessão incompleta. Respostas já concluídas serão preservadas, e cards ainda não respondidos não gerarão registros de acerto ou erro.

#### RF-SES-008 — Concluir sessão

Uma sessão será considerada concluída quando todos os cards previstos forem respondidos ou quando uma condição de encerramento definida pelo produto for atingida.

#### RF-SES-009 — Exibir resultado

Ao final, o sistema deverá mostrar:

- Quantidade de cards respondidos.
- Quantidade e taxa de acertos e erros.
- Tempo de estudo.
- Tempo médio de resposta.
- Temas e eventos contemplados.
- Cards que precisam de maior atenção.

### 6.7 Estados de aprendizagem

#### RF-EAP-001 — Manter estado por card

Cada card deverá possuir exatamente um estado atual de aprendizagem para o usuário proprietário.

Estados permitidos:

```text
Novo
Em aprendizado
Em consolidação
Consolidado
Revisão pendente
```

#### RF-EAP-002 — Atualizar estado automaticamente

O sistema deverá atualizar o estado após respostas e após a passagem de tempo relevante para revisão.

#### RF-EAP-003 — Priorizar resultados recentes

As transições deverão considerar o desempenho recente com peso superior ao histórico antigo.

#### RF-EAP-004 — Reagir a erros e lentidão

- Um erro poderá levar o card a uma etapa anterior.
- Um acerto consistente poderá avançar o card.
- Um acerto muito lento poderá impedir o avanço ou fazer o card voltar para consolidação.

#### RF-EAP-005 — Tornar estado visível

O estado atual deverá ser visível na listagem, nos filtros e nos detalhes do card.

### 6.8 Eventos e planejamento

#### RF-EVE-001 — Criar evento

O usuário deverá poder criar um evento informando:

- Nome.
- Tipo.
- Data.
- Descrição opcional.
- Prioridade baixa, média ou alta.
- Temas, grupos e cards relacionados.

#### RF-EVE-002 — Gerenciar evento

O usuário deverá poder visualizar, editar, concluir, cancelar e excluir eventos.

#### RF-EVE-003 — Associar conteúdos

Um evento deverá aceitar vários temas, grupos e cards. Um mesmo conteúdo poderá participar de vários eventos.

#### RF-EVE-004 — Calcular progresso

O sistema deverá apresentar, por evento:

- Dias restantes.
- Conteúdo estudado e ainda não estudado.
- Distribuição dos estados de aprendizagem.
- Taxa de acerto e tempo médio de resposta.
- Temas com maior necessidade de atenção.

#### RF-EVE-005 — Planejar regressivamente

O sistema deverá utilizar a data do evento para sugerir ritmo e frequência de estudo até sua realização.

#### RF-EVE-006 — Aceitar disponibilidade opcional

O usuário poderá informar, sem obrigatoriedade:

- Dias em que pretende estudar.
- Tempo disponível por dia.
- Dias indisponíveis.

A ausência dessas informações não impedirá a geração de sessões recomendadas.

#### RF-EVE-007 — Recomendar próximas sessões

O sistema deverá recomendar quando uma nova sessão deveria ocorrer e recalcular o plano caso o usuário não siga a recomendação.

Não haverá bloqueio, punição nem sessão perdida por descumprimento do planejamento.

#### RF-EVE-008 — Concentrar recomendações em prioridade alta

Quando houver um evento de alta prioridade:

- A maior parte das recomendações deverá se concentrar nele.
- Eventos de baixa ou média prioridade poderão receber apenas manutenção esporádica.
- Eventos de menor prioridade poderão ser temporariamente omitidos até a conclusão do evento prioritário.

#### RF-EVE-009 — Dividir foco entre eventos de alta prioridade

Quando houver vários eventos de alta prioridade, o sistema deverá contemplar todos e distribuir o foco considerando:

- Proximidade das datas.
- Quantidade de conteúdo restante.
- Desempenho do usuário.

#### RF-EVE-010 — Comunicar impacto da prioridade

Ao definir prioridade alta, o sistema deverá avisar que eventos de menor prioridade poderão receber pouca ou nenhuma recomendação temporariamente.

Em períodos com várias provas próximas, o sistema deverá sugerir prioridades semelhantes, preservando a decisão final do usuário.

### 6.9 Histórico e métricas

#### RF-MET-001 — Exibir visão geral

O sistema deverá apresentar:

- Total de sessões.
- Tempo total de estudo.
- Quantidade de cards estudados.
- Taxa geral de acerto.
- Tempo médio de resposta.
- Frequência de estudo.
- Evolução ao longo do tempo.

#### RF-MET-002 — Exibir métricas por organização

O usuário deverá poder consultar métricas por coleção, tema e grupo:

- Taxa de acerto.
- Tempo médio de resposta.
- Quantidade de cards por estado.
- Evolução no período.
- Última revisão.

#### RF-MET-003 — Exibir histórico do card

O detalhe do card deverá apresentar:

- Histórico cronológico de respostas.
- Acertos e erros.
- Tempo de cada tentativa.
- Intervalos entre revisões.
- Versões do conteúdo.
- Evolução de estado.
- Motivos atuais de recomendação.
- Eventos relacionados.

#### RF-MET-004 — Exibir métricas por evento

O sistema deverá apresentar:

- Cobertura do conteúdo.
- Evolução até a data.
- Temas de maior risco.
- Ritmo atual em comparação ao recomendado.
- Conteúdos ainda não estudados.

#### RF-MET-005 — Filtrar métricas por período

O usuário deverá poder limitar a análise a períodos relevantes, sem perder a possibilidade de consultar o histórico completo.

#### RF-MET-006 — Preservar histórico

O histórico deverá ser preservado durante a vida da conta, inclusive quando cards forem arquivados ou receberem uma nova versão.

### 6.10 Alertas e recomendações

#### RF-ALR-001 — Exibir alertas internos

O sistema deverá poder alertar o usuário sobre situações relevantes, como:

- Cards em revisão pendente.
- Queda de desempenho em um tema.
- Evento próximo com conteúdo insuficientemente estudado.
- Necessidade de realizar uma nova sessão.

#### RF-ALR-002 — Configurar alertas

O usuário deverá poder ativar ou desativar categorias de alerta para evitar notificações indesejadas.

No MVP, esses alertas poderão existir apenas dentro da aplicação; canais externos dependerão de decisão posterior.

## 7. Regras de negócio consolidadas

### RB-001 — Propriedade dos dados

Todo conteúdo e histórico pertencem a um único usuário e não serão compartilhados no MVP.

### RB-002 — Identidade única do card

Associar um card a vários temas, grupos ou eventos não cria cópias nem históricos separados.

### RB-003 — Estado inicial

Todo card novo começa no estado `Novo`.

### RB-004 — Autoavaliação obrigatória

Uma tentativa somente será considerada respondida depois que o usuário marcar `Acertei` ou `Errei`.

### RB-005 — Histórico imutável de respostas

Uma edição de card não alterará retroativamente os registros das sessões anteriores.

### RB-006 — Arquivamento não é exclusão

O arquivamento retira o item das recomendações e preserva conteúdo e histórico.

### RB-007 — Seleção individual garantida

Cards escolhidos individualmente para uma sessão manual têm precedência sobre cards provenientes de temas, grupos ou eventos.

### RB-008 — Deduplicação da sessão

Um card selecionado por várias fontes deverá ocupar uma única posição, exceto quando a repetição estiver explicitamente habilitada.

### RB-009 — Prioridade recente

Resultados recentes terão maior influência que resultados antigos na recomendação e no estado de aprendizagem.

### RB-010 — Proteção contra esquecimento

Nenhum card ativo e consolidado deixará de ser revisado indefinidamente.

### RB-011 — Tempo relativo

O tempo de resposta será interpretado em relação ao usuário e ao histórico do card, e não por um limite absoluto universal.

### RB-012 — Eventos de alta prioridade

Um evento de alta prioridade pode reduzir ou suspender temporariamente recomendações de eventos com prioridades inferiores.

### RB-013 — Transparência da recomendação

O sistema deverá registrar e disponibilizar os principais motivos que levaram um card ou evento a ser recomendado.

### RB-014 — Planejamento flexível

Disponibilidade e datas sugeridas orientam o planejamento, mas não restringem o acesso a sessões.

### RB-015 — Histórico permanente condicionado à conta

Não haverá expiração automática do histórico durante a vida da conta. A exclusão da conta seguirá o processo de remoção de dados aplicável.

## 8. Requisitos não funcionais

### RNF-001 — Responsividade

A aplicação deverá funcionar em navegadores de desktop e dispositivos móveis, adaptando navegação, editor e sessão de estudo ao tamanho da tela.

### RNF-002 — Usabilidade durante o estudo

A tela de estudo deverá minimizar distrações e manter pergunta, revelação da resposta e autoavaliação como ações centrais.

### RNF-003 — Acessibilidade

Os fluxos principais deverão ser utilizáveis por teclado, possuir foco visível, semântica adequada e contraste suficiente.

### RNF-004 — Segurança

Credenciais e sessões deverão ser protegidas por práticas atuais de segurança, e toda autorização deverá validar a propriedade do recurso acessado.

### RNF-005 — Privacidade

O tratamento de dados pessoais deverá ser transparente e compatível com a legislação aplicável, incluindo mecanismos de consulta e exclusão.

### RNF-006 — Persistência

Uma resposta concluída não deverá ser perdida por atualização da página, interrupção da sessão ou falha posterior em outro card.

### RNF-007 — Integridade histórica

Edições, arquivamentos e novas versões não poderão corromper ou reescrever registros históricos já concluídos.

### RNF-008 — Desempenho percebido

Os fluxos frequentes, especialmente revelar resposta, avaliar card e avançar, deverão responder sem atrasos perceptíveis em condições normais.

### RNF-009 — Fórmulas matemáticas

Fórmulas deverão ser armazenadas e renderizadas de forma segura, legível e consistente em edição, visualização e sessão.

### RNF-010 — Compatibilidade

O MVP deverá oferecer suporte às versões modernas dos principais navegadores definidos antes da implementação.

### RNF-011 — Rastreabilidade

Registros relevantes deverão possuir data e hora suficientes para reconstruir sessões, respostas, mudanças de estado e versões de cards.

### RNF-012 — Fuso horário

Datas de eventos, sessões e recomendações deverão respeitar o fuso horário configurado ou identificado para o usuário.

## 9. Fora do escopo do MVP

- Nível de dificuldade informado manualmente.
- Observações e explicações complementares.
- Etiquetas.
- Importação por planilhas ou CSV.
- Planejamento por duração desejada da sessão.
- Marcos intermediários para eventos.
- Resposta digitada.
- Comparação de resposta por inteligência artificial.
- Imagens e áudio nos cards.
- Cards interativos de múltipla escolha.
- Cards com lacunas.
- Compartilhamento de coleções.
- Coleções públicas.
- Estudo colaborativo.
- Gamificação avançada.
- Aplicativo móvel nativo ou funcionamento offline.
- Integração com calendários externos.
- Geração assistida de cards.
- Detecção automática de alterações substanciais.
- Configuração manual dos pesos do algoritmo.
- Calendário visual de atividade, caso não caiba no primeiro lançamento.

## 10. Decisões pendentes para validação

Os itens abaixo não impedem o levantamento inicial, mas precisam ser definidos antes da implementação de seus respectivos módulos.

### DP-001 — Método de autenticação

Definir se o MVP utilizará e-mail e senha, login social ou ambos.

### DP-002 — Estrutura exata de grupos

Definir se um grupo pertence obrigatoriamente a um único tema e se um card pode estar em vários grupos simultaneamente.

### DP-003 — Exclusão de contêineres

Definir o comportamento dos cards quando coleção, tema ou grupo for excluído: impedir exclusão, mover cards ou solicitar decisão ao usuário.

### DP-004 — Retenção da lixeira

Definir se itens excluídos permanecerão recuperáveis indefinidamente ou por um período determinado.

### DP-005 — Formato de fórmulas

Definir como o usuário escreverá fórmulas no editor, incluindo sintaxe e pré-visualização.

### DP-006 — Quantidade padrão da sessão

Definir quantidade inicial, limites mínimos e máximos e comportamento quando a seleção individual superar o limite escolhido.

### DP-007 — Medição do tempo de resposta

Definir se o cronômetro termina ao revelar a resposta ou ao registrar `Acertei` ou `Errei`.

### DP-008 — Repetição dentro da sessão

Definir o comportamento padrão da repetição e se um erro poderá fazer o card reaparecer na mesma sessão.

### DP-009 — Transições dos estados

Definir critérios e limites para avançar, regredir ou colocar um card em `Revisão pendente`.

### DP-010 — Pesos da recomendação

Definir os pesos iniciais de acerto, tempo de resposta, tempo sem revisão, eventos e quantidade de evidências.

### DP-011 — Distribuição entre eventos

Definir percentuais ou limites para eventos de alta, média e baixa prioridade e para vários eventos de alta prioridade simultâneos.

### DP-012 — Ciclo de vida do evento

Definir o que acontece automaticamente na data do evento e como eventos concluídos, vencidos ou cancelados afetam métricas e recomendações.

### DP-013 — Canais de alerta

Confirmar se alertas internos entram no MVP e deixar e-mail, navegador ou push para uma fase futura.

### DP-014 — Metas de desempenho técnico

Definir tempos de resposta, disponibilidade e navegadores suportados antes do planejamento técnico.

### DP-015 — Calendário de atividade

Confirmar se o calendário visual fará parte do MVP ou da primeira evolução após seu lançamento.

## 11. Critérios gerais de conclusão do MVP

O MVP estará funcionalmente completo quando um usuário puder:

1. Criar e acessar sua conta.
2. Organizar coleções, temas, grupos e cards.
3. Criar cards textuais com fórmulas e associá-los a vários temas.
4. Realizar uma sessão manual completa.
5. Realizar uma sessão recomendada e entender seu foco.
6. Revelar respostas e registrar acertos, erros e tempo de resposta.
7. Pausar e retomar uma sessão sem perder progresso.
8. Acompanhar o estado de aprendizagem de cada card.
9. Criar eventos e influenciar recomendações por prioridade.
10. Consultar histórico e métricas por card, organização e evento.
11. Arquivar e restaurar conteúdo sem perder histórico.
12. Editar um card preservando ou reiniciando conscientemente seu progresso.
13. Receber recomendações mesmo sem informar disponibilidade de estudo.
14. Utilizar os fluxos principais em desktop e dispositivo móvel.

## 12. Próximo artefato após a aprovação

Depois da validação deste levantamento, os próximos documentos recomendados são:

1. Jornadas e fluxos do usuário.
2. Especificação detalhada das regras do motor de recomendação.
3. Modelo conceitual de domínio e dados.
4. Arquitetura de informação e mapa de telas.
5. Backlog do MVP com histórias de usuário e critérios de aceitação executáveis.
