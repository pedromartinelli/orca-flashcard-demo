# Planejamento conceitual — Plataforma de estudos com flashcards

> Status: checkpoint para validação ponto a ponto.

As decisões abaixo consolidam o escopo inicial do produto e as alterações realizadas durante a primeira rodada de validação.

## 1. Priorização de eventos em uma sessão manual

Em uma sessão planejada manualmente, o evento deve funcionar como uma fonte de cards, não como uma priorização abstrata.

O usuário poderá montar a sessão escolhendo:

- Cards específicos.
- Temas ou grupos.
- Um ou mais eventos.
- Uma combinação dessas opções.

Ao selecionar um evento, os temas e cards associados a ele entram no conjunto da sessão. Cards repetidos entre temas, eventos ou seleções individuais aparecem apenas uma vez.

Regras recomendadas:

1. Cards selecionados individualmente têm inclusão garantida.
2. Cards provenientes de temas e eventos formam o restante da seleção.
3. Se a quantidade disponível for maior que a quantidade desejada, o algoritmo escolhe os demais cards conforme desempenho, tempo de resposta e necessidade de revisão.
4. A prioridade do evento influencia a seleção dos cards vinculados a ele.
5. Se todos os cards couberem na sessão, a prioridade apenas influencia a ordem de apresentação.

Dessa forma, a opção anteriormente descrita como “priorizar cards de determinado evento” será renomeada para:

> **Incluir evento na sessão**

Na sessão recomendada, não será necessário selecionar o evento manualmente. Eventos ativos influenciarão automaticamente a recomendação de acordo com:

- Prioridade configurada.
- Proximidade da data.
- Desempenho nos temas relacionados.
- Quantidade de conteúdo ainda não estudado.

## 2. Planejamento de disponibilidade

O plano de estudos não dependerá obrigatoriamente de o usuário informar dias ou horários disponíveis.

Existirão dois comportamentos:

### Funcionamento padrão

O sistema estará sempre pronto para gerar uma sessão recomendada quando o usuário entrar. Ele calculará o melhor conteúdo para aquele momento considerando o histórico e os eventos.

### Planejamento opcional

Se desejar, o usuário poderá informar:

- Dias em que pretende estudar.
- Tempo disponível em cada dia.
- Dias em que não estará disponível.

Essas informações apenas refinam o planejamento, sem limitar o acesso às sessões.

O sistema também poderá recomendar datas:

- “Recomendamos uma sessão até quarta-feira.”
- “Para manter o ritmo deste evento, faça três sessões nesta semana.”
- “Este tema deveria ser revisado antes da próxima semana.”

Se o usuário não estudar no dia recomendado, o plano será recalculado automaticamente. Não haverá sessões “perdidas” nem bloqueios por descumprimento do planejamento.

## 3. Explicação da recomendação

A justificativa não será exibida durante a apresentação de cada card, evitando distrações.

Ela poderá ser consultada em uma listagem de recomendações antes ou depois da sessão:

| Card ou tema | Motivo da recomendação |
|---|---|
| Princípio da legalidade | Erros recentes |
| Controle de constitucionalidade | Tempo de resposta elevado |
| Direitos fundamentais | Revisão pendente |
| Crase | Associado a uma prova próxima |
| Regência verbal | Poucas revisões realizadas |

Também poderá existir uma visualização dessas informações na gestão dos cards, sem interferir no fluxo do estudo.

## 4. Calendário de atividade

A ideia é apresentar um calendário semelhante a um mapa de atividade:

```text
Setembro
Seg  ░ ░ ▓ ░ ░
Ter  ░ ▒ ▓ ░ ▒
Qua  ▓ ▓ ░ ░ ▒
Qui  ░ ▒ ▒ ▓ ░
Sex  ░ ░ ▓ ▓ ░
```

Cada dia recebe uma intensidade de cor baseada na atividade. O usuário poderá escolher qual indicador visualizar:

- Tempo estudado.
- Quantidade de cards.
- Quantidade de sessões.
- Taxa de acerto.

Ao selecionar um dia, poderá visualizar:

- Sessões realizadas.
- Cards estudados.
- Temas revisados.
- Tempo de estudo.
- Taxa de acerto.
- Tempo médio de resposta.

Exemplo:

> **14 de setembro**
>
> 2 sessões · 47 cards · 32 minutos · 81% de acertos

O principal objetivo é mostrar consistência, lacunas e padrões de estudo. Esse calendário não representa sozinho o domínio do conteúdo; ele complementa as métricas de evolução.

A recomendação é incluí-lo no produto, mas não necessariamente no primeiro lançamento do MVP. O painel inicial pode começar com gráficos simples e receber o calendário posteriormente.

## 5. Estados de aprendizagem atualizados

A terminologia fica:

```text
Novo
  ↓
Em aprendizado
  ↓
Em consolidação
  ↓
Consolidado
  ↓
Revisão pendente
```

“Revisão pendente” substituirá integralmente “atrasado para revisão”.

Um card consolidado entra em revisão pendente quando passa tempo suficiente sem aparecer. Após uma nova resposta:

- Se houver acerto consistente, retorna para consolidado.
- Se houver erro, poderá retornar para em consolidação ou em aprendizado.
- Se houver acerto muito lento, poderá permanecer em revisão pendente ou voltar para em consolidação.

## 6. Ordem de prioridade do algoritmo

A lógica terá como sinais principais:

1. Taxa de acerto, com maior peso para resultados recentes.
2. Tempo de resposta.
3. Tempo desde a última revisão.
4. Prioridade e proximidade dos eventos.
5. Quantidade de evidências existentes sobre o card.

O tempo desde a última revisão continuará funcionando como uma proteção contra esquecimento. Mesmo um card com excelente taxa de acerto voltará a aparecer quando permanecer muito tempo sem revisão.

A prioridade dos eventos definirá a distribuição de foco das recomendações até a data de cada evento.

Quando existir um evento de alta prioridade:

- A maior parte das recomendações deverá se concentrar nos temas e cards associados a ele.
- Eventos de baixa e média prioridade receberão recomendações esporádicas de manutenção.
- Dependendo da proximidade e das necessidades do evento prioritário, eventos de menor prioridade poderão deixar de aparecer temporariamente.
- O sistema deverá informar claramente esse efeito ao usuário ao configurar a prioridade e ao apresentar o planejamento recomendado.

Uma sessão dedicada exclusivamente a um evento deverá apresentar uma indicação como:

> **Sessão focada no evento “Prova de Cálculo”, definido com prioridade alta.**

Quando houver mais de um evento de alta prioridade, o foco das recomendações será dividido entre eles. Essa divisão poderá considerar a proximidade das datas, a quantidade de conteúdo restante e o desempenho do usuário, garantindo que todos os eventos de alta prioridade sejam contemplados.

Em períodos com várias provas próximas, o sistema deverá recomendar prioridades semelhantes para elas. O usuário ainda poderá atribuir prioridade superior a apenas uma ou duas caso queira concentrar deliberadamente seus estudos, sendo avisado de que os demais eventos poderão receber pouca ou nenhuma recomendação até a conclusão dos eventos prioritários.

## 7. Cards associados a vários temas

Um card poderá pertencer a vários temas sem ser duplicado.

Exemplo:

```text
Card: “Quais são os princípios da Administração Pública?”

Temas:
- Direito Administrativo
- Princípios Constitucionais
- Revisão para Concurso X
```

O histórico continuará sendo único. Uma resposta ao card atualizará sua evolução em todos os temas aos quais ele estiver associado.

Se o mesmo card entrar em uma sessão por dois temas diferentes, ele será apresentado apenas uma vez.

## 8. Conteúdo dos cards na versão inicial

Inicialmente, o card terá:

- Pergunta.
- Resposta.
- Estado atual de aprendizagem, como `Novo`, `Em aprendizado`, `Em consolidação`, `Consolidado` ou `Revisão pendente`.
- Uma ou mais associações com coleções, temas ou grupos.
- Dados automáticos de desempenho.
- Histórico de revisões.
- Eventos relacionados.

Pergunta e resposta aceitarão texto editável com formatação básica para:

- Parágrafos.
- Listas.
- Alternativas.
- Destaques.
- Quebras de linha.
- Fórmulas matemáticas, tanto em linha quanto em blocos destacados.

Imagens, áudios e outros tipos de mídia ficam para futuras versões.

## 9. Alterações substanciais em um card

A recomendação é adotar versionamento conceitual e separar o histórico de estudo do progresso atual.

Ao editar a pergunta ou a resposta, o sistema perguntará:

> **Esta alteração muda o conteúdo estudado?**

O usuário escolherá entre:

- **Apenas correção:** mantém o progresso atual.
- **Novo conteúdo:** reinicia o progresso de aprendizagem.

Exemplos:

| Alteração | Comportamento recomendado |
|---|---|
| Correção ortográfica | Manter progresso |
| Melhorar formatação | Manter progresso |
| Adicionar um exemplo sem mudar a resposta | Manter progresso |
| Mudar a resposta correta | Reiniciar progresso |
| Substituir a pergunta por outra | Reiniciar progresso |
| Alterar significativamente o nível de abrangência | Reiniciar progresso |

Quando o progresso for reiniciado:

- O histórico antigo não será apagado.
- A versão anterior continuará registrada.
- As métricas antigas poderão ser consultadas.
- O algoritmo passará a considerar principalmente as respostas realizadas após a nova versão.
- O card retornará ao estado `Novo` ou `Em aprendizado`.

Isso preserva os dados históricos sem permitir que o desempenho em uma pergunta antiga distorça a recomendação da nova pergunta.

> **Nova ideia:** em uma versão futura, o sistema poderá identificar automaticamente alterações significativas e recomendar a reinicialização, mas a decisão final continuará pertencendo ao usuário.

## 10. Funcionalidades transferidas para evoluções futuras

A lista consolidada passa a incluir:

- Nível de dificuldade informado manualmente.
- Observações e explicações complementares.
- Etiquetas.
- Importação por planilhas ou CSV.
- Duração desejada para uma sessão.
- Marcos intermediários para eventos.
- Resposta digitada.
- Comparação da resposta por inteligência artificial.
- Imagens e áudio.
- Cards de múltipla escolha interativos.
- Cards com lacunas.
- Compartilhamento de coleções.
- Coleções públicas.
- Estudo colaborativo.
- Gamificação avançada.
- Aplicativo móvel com funcionamento offline.
- Integrações com calendários.
- Geração assistida de cards.
- Detecção automática de alterações substanciais.
- Algoritmo configurável pelo usuário.

## 11. Escopo consolidado do produto inicial

O produto inicial será uma aplicação web responsiva para dispositivos móveis, com:

- Autenticação e recuperação de conta.
- Coleções, temas e grupos.
- Cards pertencentes a vários temas.
- Conteúdo inicialmente textual, com suporte à formatação de fórmulas matemáticas.
- Exibição do estado atual de aprendizagem em cada card.
- Arquivamento e exclusão.
- Sessões manuais e recomendadas.
- Inclusão de eventos em sessões manuais.
- Autoavaliação com acerto ou erro.
- Registro do tempo de resposta.
- Pausa e retomada de sessões.
- Histórico permanente.
- Métricas por card, tema, grupo e evento.
- Estados de aprendizagem.
- Eventos com data e prioridade.
- Planejamento regressivo flexível.
- Recomendações de datas para novas sessões.
- Justificativas das recomendações fora da apresentação do card.
- Motor adaptativo baseado principalmente em acertos, erros e tempo de resposta.
- Proteção contra esquecimento por meio do estado `Revisão pendente`.
- Versionamento conceitual dos cards quando o conteúdo for alterado.

A solução possui uma separação clara: o MVP cobre o ciclo essencial de criação, estudo, recomendação e acompanhamento; recursos que aumentam a complexidade editorial ou dependem de inteligência artificial ficam reservados para evoluções posteriores.
