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
| Tema | Classificação de conteúdo que pode pertencer a uma ou mais coleções. |
| Grupo | Subdivisão opcional que pode pertencer a um ou mais temas. |
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

#### RF-AUT-001 — Criar conta com e-mail e senha

O sistema deverá permitir que uma pessoa crie uma conta utilizando e-mail e senha. Esse será o único método de autenticação do MVP.

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

O usuário deverá poder criar, visualizar, renomear, reorganizar, duplicar, arquivar, restaurar e excluir temas.

Um mesmo tema poderá pertencer a mais de uma coleção sem ser duplicado.

#### RF-ORG-003 — Gerenciar grupos

O usuário deverá poder criar, visualizar, renomear, reorganizar, duplicar, arquivar, restaurar e excluir grupos.

Um mesmo grupo poderá pertencer a mais de um tema sem ser duplicado.

#### RF-ORG-004 — Proteger conteúdos relacionados

Uma coleção, um tema ou um grupo não poderá provocar a exclusão automática de conteúdos que também pertençam a outros contextos.

Antes da exclusão, o sistema deverá informar claramente:

- Quais relações serão removidas.
- Quais temas, grupos ou cards continuarão existindo em outros contextos.
- Quais itens ficariam sem outro contexto.
- Quais itens seriam movidos para a área de excluídos.

Nenhum conteúdo compartilhado será excluído definitivamente sem uma decisão explícita do usuário.

#### RF-ORG-005 — Navegar pela hierarquia

O usuário deverá conseguir navegar pela estrutura conceitual `Coleção → Tema → Grupo → Card` e visualizar a quantidade de cards em cada nível.

Como temas, grupos e cards podem possuir vários pais, a interface deverá deixar claro quando um item exibido também pertence a outros contextos.

#### RF-ORG-006 — Duplicar estruturas

O usuário deverá poder duplicar temas e grupos para criar versões independentes destinadas a outro evento ou objetivo de estudo.

A duplicação deverá:

- Criar uma nova identidade para o item duplicado.
- Permitir alterações sem modificar o item original.
- Informar quais conteúdos internos serão apenas associados e quais também serão duplicados.
- Não copiar o histórico de aprendizagem para novos cards criados pela operação.

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

Se um card for selecionado por mais de uma fonte, deverá aparecer uma única vez no conjunto inicial da sessão. Novas aparições ocorrerão apenas como reforço depois de uma resposta incorreta.

#### RF-SEM-004 — Definir quantidade de cards

O usuário deverá poder escolher a quantidade de cards da sessão, respeitando a quantidade de cards selecionados individualmente, cuja inclusão é garantida.

#### RF-SEM-005 — Ordenar a sessão

O usuário deverá poder escolher entre a ordem recomendada pelo sistema e uma ordem aleatória.

#### RF-SEM-006 — Repetir cards respondidos incorretamente

Um card respondido incorretamente deverá reaparecer mais adiante na mesma sessão como reforço.

A repetição não poderá ocorrer imediatamente após o erro quando houver outros cards disponíveis.

#### RF-SEM-007 — Visualizar resumo antes de iniciar

Antes do início, o sistema deverá mostrar:

- Quantidade prevista de cards.
- Temas, grupos e eventos contemplados.
- Critérios utilizados para formar a sessão.
- Avisos relevantes sobre limitações da seleção.

Na sessão recomendada, o resumo também deverá apresentar a meta de duração configurada e a quantidade estimada de cards.

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

#### RF-SER-008 — Configurar duração das recomendações

O usuário deverá poder definir, nas configurações das recomendações, a duração desejada para sessões recomendadas.

O sistema deverá estimar quantos cards cabem nesse período usando o tempo médio de resposta de cada card. Quando não houver histórico suficiente, utilizará a média geral do usuário e, na ausência dela, uma estimativa inicial do sistema.

A duração será uma meta aproximada, pois o tempo real dependerá do comportamento do usuário durante a sessão.

No MVP, essa será a principal configuração oferecida ao usuário; os pesos internos do algoritmo não serão configuráveis.

### 6.6 Execução da sessão

#### RF-SES-001 — Apresentar pergunta

O sistema deverá apresentar inicialmente a pergunta sem revelar a resposta.

#### RF-SES-002 — Revelar resposta

O usuário deverá poder revelar a resposta quando considerar que concluiu sua tentativa mental.

#### RF-SES-003 — Registrar tempo de resposta

O sistema deverá registrar o tempo entre a apresentação da pergunta e a revelação da resposta.

O período utilizado para comparar a resposta e clicar em `Acertei` ou `Errei` não fará parte do tempo de resposta do card.

#### RF-SES-004 — Registrar autoavaliação

Após revelar a resposta, o usuário deverá marcar `Acertei` ou `Errei` antes de avançar.

#### RF-SES-005 — Salvar progresso continuamente

Cada resposta concluída deverá ser persistida sem depender da finalização de toda a sessão.

#### RF-SES-006 — Pausar e retomar

O usuário deverá poder pausar uma sessão e retomá-la posteriormente sem perder respostas já registradas.

O tempo em pausa não deverá ser contabilizado como tempo de resposta.

#### RF-SES-007 — Abandonar sessão

O usuário deverá poder encerrar uma sessão incompleta. Respostas já concluídas serão preservadas, e cards ainda não respondidos não gerarão registros de acerto ou erro.

Se a página for fechada durante um card ainda não avaliado, a tentativa incompleta e seu tempo não serão contabilizados. A sessão poderá ser retomada a partir desse card.

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

#### RF-SES-010 — Apresentar orientação antes da sessão

Antes de todas as sessões, o sistema deverá apresentar uma orientação breve contendo:

- Como revelar a resposta.
- Como marcar `Acertei` ou `Errei`.
- Como pausar, retomar ou encerrar a sessão.
- O momento em que o tempo de resposta é finalizado.
- O que é preservado ou descartado se a página for fechada.
- A regra de repetição de cards respondidos incorretamente.

No primeiro uso, a orientação poderá ser mais detalhada. Nas sessões posteriores, deverá permanecer acessível em uma versão resumida, sem impedir que o usuário prossiga imediatamente.

#### RF-SES-011 — Registrar primeira tentativa e reforços

Quando um card reaparecer após um erro na mesma sessão:

- A primeira resposta da sessão será utilizada para atualizar o estado, a taxa principal de acerto e o motor de recomendação.
- As respostas seguintes serão registradas como tentativas de reforço.
- Tentativas de reforço não transformarão o erro inicial em acerto nas métricas principais.
- O histórico poderá mostrar separadamente a evolução dentro da sessão.

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

O usuário deverá poder visualizar, editar e excluir eventos, inclusive depois da data definida.

O usuário poderá alterar nome, data, prioridade e conteúdos associados a qualquer momento.

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

#### RF-EVE-011 — Notificar término sem alterar o evento

Ao atingir ou ultrapassar a data de um evento, o sistema deverá:

- Notificar o usuário de que a data chegou.
- Manter o evento e seus relacionamentos.
- Permitir que o usuário altere a data, o nome, a prioridade e os conteúdos associados.
- Permitir que o usuário exclua o evento quando desejar.

O MVP não concluirá, arquivará nem excluirá automaticamente o evento.

#### RF-EVE-012 — Exibir calendário simplificado

O sistema deverá oferecer uma visualização simples do planejamento, contendo:

- Datas dos eventos.
- Próximas sessões recomendadas.
- Evento ou tema que receberá o foco planejado.
- Indicação visual de datas que foram recalculadas.

O calendário será informativo e acompanhará o planejamento recalculado; ele não criará obrigações nem bloqueará sessões fora das datas sugeridas.

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

No MVP, esses alertas existirão dentro da aplicação. E-mail, notificações do navegador e push ficarão para uma fase futura.

## 7. Regras de negócio consolidadas

### RB-001 — Propriedade dos dados

Todo conteúdo e histórico pertencem a um único usuário e não serão compartilhados no MVP.

### RB-002 — Identidade única do card

Associar um card a vários temas, grupos ou eventos não cria cópias nem históricos separados.

Temas e grupos também poderão possuir vários pais sem que isso, isoladamente, crie cópias.

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

Um card selecionado por várias fontes deverá ocupar uma única posição inicial. Caso a primeira resposta seja incorreta, ele reaparecerá posteriormente como reforço.

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

### RB-016 — Remoção de associação não é exclusão

Excluir um item de determinado contexto remove sua relação com aquele pai. Se o item possuir outros pais, ele continuará existindo e não poderá ser enviado para a área de excluídos sem autorização explícita.

### RB-017 — Duplicação cria independência

Um tema, grupo ou card duplicado terá identidade própria. Alterações realizadas na cópia não modificarão o original.

### RB-018 — Recuperação indefinida

Itens movidos para a área de excluídos permanecerão recuperáveis indefinidamente no MVP, exceto quando o usuário solicitar sua exclusão definitiva ou excluir a conta.

### RB-019 — Primeira tentativa da sessão

A primeira resposta de um card em uma sessão será a referência para estado, taxa principal de acerto e recomendação. Repetições na mesma sessão servirão como reforço e serão identificadas separadamente.

### RB-020 — Encerramento do tempo de resposta

O tempo de resposta termina quando o usuário revela a resposta.

### RB-021 — Permanência do evento

A chegada da data de um evento gera uma notificação, mas não altera nem remove automaticamente o evento.

## 8. Modelo inicial dos estados e recomendações

As regras desta seção serão os parâmetros iniciais do MVP. Elas deverão permanecer documentadas para o usuário e poderão ser calibradas depois de testes e dados reais, sem alterar a ordem conceitual dos fatores já aprovada.

### 8.1 Tentativa qualificadora

Para estados, taxa principal de acerto e prioridade, será considerada a primeira resposta de cada card em cada sessão.

Respostas adicionais ao mesmo card na sessão serão armazenadas como reforços, mas não substituirão o resultado da primeira tentativa.

O histórico recente será composto inicialmente pelas cinco últimas tentativas qualificadoras. Quando houver menos de cinco, serão utilizadas todas as disponíveis.

### 8.2 Transições iniciais dos estados

#### Novo

- Um card permanece `Novo` enquanto não possuir tentativa qualificadora.
- Depois da primeira tentativa, passa para `Em aprendizado`, independentemente do resultado.

#### Em aprendizado

- Permanece nesse estado após um erro.
- Avança para `Em consolidação` depois de dois acertos qualificadores consecutivos, em sessões distintas e com tempo de resposta aceitável.
- Um acerto lento é registrado como acerto, mas não completa a sequência necessária para avançar.

#### Em consolidação

- Avança para `Consolidado` depois de três acertos qualificadores consecutivos obtidos após entrar em consolidação, em sessões distintas e com tempo aceitável.
- Um erro faz o card voltar para `Em aprendizado`.
- Um acerto lento mantém o card em consolidação e interrompe a sequência de avanço.

#### Consolidado

- Permanece consolidado enquanto as revisões forem respondidas corretamente dentro do tempo aceitável.
- Entra em `Revisão pendente` quando alcançar a próxima data de revisão sem uma nova tentativa qualificadora.
- Um erro faz o card voltar para `Em consolidação`.
- Dois erros entre as três últimas tentativas qualificadoras fazem o card voltar para `Em aprendizado`.
- Dois acertos lentos entre as três últimas tentativas poderão fazê-lo voltar para `Em consolidação`.

#### Revisão pendente

- Um acerto em tempo aceitável retorna o card para `Consolidado` e amplia o próximo intervalo.
- Um acerto lento leva o card para `Em consolidação`.
- Um erro leva o card para `Em consolidação`; se também satisfizer a regra de dois erros entre as três últimas tentativas, irá para `Em aprendizado`.

### 8.3 Intervalos iniciais de revisão

| Situação | Próxima revisão inicial |
|---|---|
| Erro em qualquer estado | Repetição na sessão e nova recomendação no dia seguinte |
| Acerto que mantém o card `Em aprendizado` | 1 dia |
| Acerto que leva o card para `Em consolidação` | 3 dias |
| Acerto que mantém o card `Em consolidação` | 7 dias |
| Acerto que leva o card para `Consolidado` | 14 dias |
| Revisões corretas em `Consolidado` | Dobrar o intervalo anterior, até 90 dias |
| Acerto lento | Não ampliar o intervalo vigente |

Os intervalos determinam necessidade de revisão, mas eventos prioritários poderão antecipar a apresentação do card.

### 8.4 Classificação do tempo de resposta

O tempo será comparado com uma referência individual, evitando um limite universal para todos os cards e usuários.

- Com pelo menos três acertos qualificadores no card, a referência será a média dos tempos desses acertos.
- Sem histórico suficiente no card, será utilizada a média de acertos do usuário em seus outros cards.
- Sem histórico suficiente do usuário, será utilizada uma referência inicial de 30 segundos.
- Um tempo será inicialmente classificado como lento quando superar 150% da referência aplicável.

A referência utilizada para avaliar uma tentativa será calculada antes de incluir o tempo dessa própria tentativa.

### 8.5 Pontuação inicial do card

Cada card elegível receberá uma prioridade de `0` a `100`:

```text
Prioridade do card =
    45% pressão por erros
  + 25% pressão por lentidão
  + 20% necessidade de revisão
  + 10% incerteza por pouco histórico
```

#### Pressão por erros

- Considera as cinco últimas tentativas qualificadoras.
- Tentativas mais recentes recebem pesos `5`, `4`, `3`, `2` e `1`, da mais recente para a mais antiga.
- Um erro vale `1` e um acerto vale `0`.
- Sem histórico, o componente começa em `0,5`.

#### Pressão por lentidão

- Compara a média recente do card com a referência individual de tempo.
- Na referência ou abaixo dela, o componente vale `0`.
- Em 200% da referência ou acima, vale `1`.
- Valores intermediários crescem proporcionalmente.
- Sem histórico suficiente, o componente começa em `0,5`.

#### Necessidade de revisão

- Compara o tempo desde a última tentativa com o intervalo vigente do card.
- Ao atingir ou ultrapassar o intervalo, o componente vale `1`.
- Antes disso, cresce proporcionalmente de `0` a `1`.
- Para um card `Novo`, que ainda não possui intervalo, o componente começa em `0,5`.

#### Incerteza

- Começa em `1` para um card sem tentativas qualificadoras.
- Diminui a cada tentativa qualificadora.
- Chega a `0` depois de cinco tentativas.

Quando houver cards novos e cards com histórico na mesma sessão, a composição tentará reservar inicialmente até 10% para introdução de cards novos. Esse limite poderá ser ultrapassado quando o evento prioritário possuir principalmente cards novos ou quando não houver cards revisáveis suficientes.

### 8.6 Composição por duração

Para preencher a duração escolhida pelo usuário:

1. O sistema ordenará os candidatos pela prioridade calculada.
2. Para cada card, estimará o tempo pela média histórica de resposta acrescida inicialmente de 5 segundos para revelação, avaliação e avanço.
3. Sem histórico do card, utilizará a média geral do usuário.
4. Sem histórico do usuário, utilizará inicialmente 30 segundos por card, além da margem de interação.
5. Adicionará cards enquanto o tempo acumulado permanecer próximo da duração configurada.

O sistema deverá apresentar a quantidade estimada de cards e deixar claro que a duração real poderá variar.

### 8.7 Distribuição inicial entre eventos

A composição ocorrerá em duas etapas:

1. Distribuir o foco entre eventos e conteúdo geral.
2. Ordenar os cards de cada parte utilizando a pontuação definida na seção 8.5.

#### Quando existir um evento de alta prioridade

- Por padrão, ao menos 80% da duração recomendada será reservada para eventos de alta prioridade.
- Esse foco subirá para 90% quando faltar até 14 dias e menos de 70% dos cards relacionados estiverem consolidados.
- O foco poderá chegar a 100% quando faltar até 7 dias e menos de 70% estiver consolidado, ou quando o usuário solicitar foco exclusivo.
- A parcela restante será usada para manutenção de eventos médios, baixos e conteúdos sem evento.
- Em foco de 100%, conteúdos de prioridades inferiores poderão ser temporariamente ignorados.

#### Quando houver vários eventos de alta prioridade

A parcela de alta prioridade será dividida por um índice de necessidade:

```text
Necessidade do evento =
    40% proximidade da data
  + 35% conteúdo ainda não consolidado
  + 25% dificuldade observada
```

- A proximidade cresce linearmente de `0` a `1` durante os 90 dias anteriores ao evento e permanece em `1` na data.
- O conteúdo ainda não consolidado corresponde à proporção de cards relacionados que não estão em `Consolidado`.
- A dificuldade observada corresponde à média das pressões por erros e lentidão dos cards relacionados.

- Eventos em condições equivalentes receberão parcelas equivalentes.
- Se a duração permitir, todos os eventos de alta prioridade deverão receber ao menos um card.
- Cards associados a vários eventos serão apresentados uma vez e poderão satisfazer a parcela de todos eles.

#### Quando não houver evento de alta prioridade

Todos os cards serão ordenados pela prioridade base, com os seguintes multiplicadores iniciais:

| Associação | Multiplicador |
|---|---:|
| Evento de média prioridade | `1,20` |
| Evento de baixa prioridade | `1,05` |
| Sem evento ativo | `1,00` |

### 8.8 Transparência para o usuário

O produto deverá explicar em linguagem simples:

- Quais fatores formam a prioridade de um card.
- Que a primeira tentativa da sessão é a utilizada nas métricas principais.
- Por que um card está em determinado estado.
- Quando ocorrerá a próxima revisão estimada.
- Quanto da sessão está direcionado a cada evento.
- Quando um evento de alta prioridade estiver reduzindo ou suspendendo outras recomendações.

Os pesos e limites poderão aparecer em uma área de ajuda, enquanto a interface cotidiana utilizará explicações curtas e contextuais.

## 9. Requisitos não funcionais

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

Os fluxos frequentes deverão responder sem atrasos perceptíveis em condições normais. Como metas iniciais:

- Revelar resposta, avaliar card e avançar deverão apresentar reação visual em até 200 milissegundos.
- Navegações e carregamentos comuns deverão disponibilizar conteúdo utilizável em até 3 segundos.
- Salvamentos deverão confirmar o resultado em até 1 segundo, sempre que a conexão permitir.
- A geração de uma recomendação deverá concluir em até 3 segundos para o volume esperado no MVP.

Esses valores serão validados tecnicamente e monitorados durante o desenvolvimento.

### RNF-009 — Fórmulas matemáticas

Fórmulas deverão ser armazenadas e renderizadas de forma segura, legível e consistente em edição, visualização e sessão.

### RNF-010 — Compatibilidade

O MVP deverá oferecer suporte às duas versões estáveis mais recentes de:

- Google Chrome.
- Microsoft Edge.
- Mozilla Firefox.
- Safari.

Em dispositivos móveis, deverá funcionar nos navegadores principais baseados em Chrome e no Safari do iOS. Recursos essenciais não poderão depender de uma funcionalidade exclusiva de um único navegador.

### RNF-011 — Rastreabilidade

Registros relevantes deverão possuir data e hora suficientes para reconstruir sessões, respostas, mudanças de estado e versões de cards.

### RNF-012 — Fuso horário

Datas de eventos, sessões e recomendações deverão respeitar o fuso horário configurado ou identificado para o usuário.

## 10. Fora do escopo do MVP

- Nível de dificuldade informado manualmente.
- Observações e explicações complementares.
- Etiquetas.
- Importação por planilhas ou CSV.
- Configurações avançadas de duração e composição da sessão além da meta de tempo do MVP.
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
- Calendário analítico de atividade com mapa de intensidade e métricas históricas por dia.
- Conclusão, arquivamento ou exclusão automática de eventos após suas datas.
- Alertas por e-mail, navegador ou push.
- Login social. A integração com o Google será a primeira opção avaliada após a conclusão do MVP.

## 11. Decisões consolidadas e pendências residuais

### DP-001 — Método de autenticação

**Consolidada.** O MVP utilizará exclusivamente e-mail e senha. Ao término do MVP, a primeira evolução de autenticação a ser avaliada será o login social com Google.

### DP-002 — Estrutura de pais e duplicação

**Consolidada.** Temas, grupos e cards poderão pertencer a vários pais. Todos poderão ser duplicados para gerar versões independentes. O desenho da ação de duplicação deverá permitir que o usuário entenda quais descendentes serão associados e quais serão copiados.

### DP-003 — Exclusão de contêineres

**Consolidada.** Conteúdos existentes em outros contextos não serão excluídos automaticamente. O sistema mostrará o impacto e solicitará permissão explícita para qualquer exclusão adicional.

### DP-004 — Retenção da lixeira

**Consolidada.** Itens permanecerão recuperáveis indefinidamente no MVP, salvo exclusão definitiva solicitada pelo usuário ou exclusão da conta.

### DP-005 — Formato de fórmulas

**Adiada para o desenvolvimento.** Sintaxe, biblioteca e experiência de pré-visualização serão escolhidas junto à solução técnica do editor.

### DP-006 — Duração da sessão recomendada

**Consolidada.** O usuário definirá uma meta de tempo nas configurações limitadas de recomendação. O sistema estimará a quantidade de cards usando seus tempos médios de resposta.

### DP-007 — Medição do tempo de resposta

**Consolidada.** O cronômetro termina ao revelar a resposta. Todas as sessões começam com uma orientação sobre controles, persistência e contabilização do tempo.

### DP-008 — Repetição dentro da sessão

**Consolidada.** Um card respondido incorretamente reaparecerá na mesma sessão. Apenas a primeira resposta atualizará estado, taxa principal de acerto e prioridade; as demais serão tentativas de reforço.

### DP-009 — Transições dos estados

**Consolidada inicialmente.** As transições e os intervalos iniciais estão definidos nas seções 8.2 e 8.3 e poderão ser recalibrados após validação.

### DP-010 — Pesos da recomendação

**Consolidada inicialmente.** A pontuação inicial está definida na seção 8.5, com maior peso para erros, seguida de tempo de resposta, necessidade de revisão e incerteza.

### DP-011 — Distribuição entre eventos

**Consolidada inicialmente.** A distribuição está definida na seção 8.7. Eventos de alta prioridade recebem entre 80% e 100% do foco, conforme urgência e cobertura.

### DP-012 — Ciclo de vida do evento

**Consolidada para o MVP.** O sistema apenas notificará a chegada da data. O evento permanecerá editável e será gerenciado manualmente pelo usuário. Automatizações de conclusão e arquivamento irão para o backlog futuro.

### DP-013 — Canais de alerta

**Consolidada.** Alertas internos entram no MVP. E-mail, navegador e push ficam para uma fase futura.

### DP-014 — Metas de desempenho técnico

**Consolidada inicialmente.** Metas mensuráveis e suporte aos navegadores mais utilizados estão descritos nos requisitos `RNF-008` e `RNF-010`. A disponibilidade operacional será definida durante o planejamento técnico.

### DP-015 — Calendário

**Consolidada para o MVP.** Haverá um calendário simples para visualizar eventos e sessões recomendadas. O mapa analítico de atividade permanece como evolução futura.

## 12. Critérios gerais de conclusão do MVP

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
15. Configurar a duração desejada de uma sessão recomendada.
16. Repetir cards errados sem distorcer as métricas da primeira tentativa.
17. Consultar um calendário simples de eventos e sessões planejadas.
18. Receber alertas internos e uma orientação antes de iniciar cada sessão.

## 13. Próximo artefato após a aprovação

Depois da validação deste levantamento, os próximos documentos recomendados são:

1. Jornadas e fluxos do usuário.
2. Cenários de simulação e validação do motor de recomendação inicial.
3. Modelo conceitual de domínio e dados.
4. Arquitetura de informação e mapa de telas.
5. Backlog do MVP com histórias de usuário e critérios de aceitação executáveis.
