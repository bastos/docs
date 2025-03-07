---
title: Personalizando um fluxo de trabalho para triagem de suas notificações
intro: 'Para criar um fluxo de trabalho ideal para a triagem de suas notificações, você pode adaptar e personalizar esses fluxos de trabalho de exemplo.'
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
topics:
  - Notifications
redirect_from:
  - /github/managing-subscriptions-and-notifications-on-github/customizing-a-workflow-for-triaging-your-notifications
  - /github/managing-subscriptions-and-notifications-on-github/viewing-and-triaging-notifications/customizing-a-workflow-for-triaging-your-notifications
shortTitle: Triage your notifications
ms.openlocfilehash: 9e5771dff52408a1b6967a3792eb36eefebefd72
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2022
ms.locfileid: '145094780'
---
## Iniciando sua triagem de caixa de entrada

Antes de começar a fazer a triagem de sua caixa de entrada, considere se você prefere primeiro encontrar e responder às atualizações mais importantes ou limpar sua caixa de entrada de atualizações sem importância que são fáceis de remover ou fazer triagem.

Você pode decidir usar uma combinação de ambas as abordagens em vários momentos, dependendo do volume de notificações que você tenha.

Para ver um exemplo de fluxo de trabalho de localização e resposta às notificações mais importantes, confira "[Verificando suas prioridades de notificação mais altas](#checking-your-highest-notification-priorities)".

Para ver um exemplo de fluxo de trabalho de remoção de notificações que são fáceis de remover ou fazer triagem, confira "[Limpar suas notificações menos importantes](#clearing-your-least-important-notifications)".

## Verificando suas maiores prioridades de notificação

Escolha qual tipo de notificações são mais urgentes para revisar e escolha um horário para revisá-las. Você pode considerar a pergunta "Quem estou bloqueando?"

Por exemplo, você pode decidir verificar suas notificações nesta ordem pela manhã em sua agenda diária de planejamento:
  - Pull requests onde sua revisão é solicitada. (filtrar por `reason:review-requested`)
  - Eventos em que seu nome de usuário é @mentioned, também chamados de menção direta. (filtrar por `reason:mention`)
  - Eventos em que uma equipe da qual você é membro é @mentioned, também chamados de menções de equipe. (filtrar por `reason:team-mention`)
  - Falhas de fluxo de trabalho do CI para um repositório específico. (filtre por `reason:ci-activity` e `repo:owner/repo-name` e confirme se você habilitou notificações de atividade de CI para falhas de fluxo de trabalho em suas configurações de notificação)

  {% tip %}

  **Dica:** para revisar rapidamente suas prioridades mais altas, configure filtros personalizados em ordem da prioridade de revisão. Para obter mais informações, confira "[Como gerenciar notificações na sua caixa de entrada](/github/managing-subscriptions-and-notifications-on-github/managing-notifications-from-your-inbox#customizing-your-inbox-with-custom-filters)".

  {% endtip %}

## Seguindo as atualizações de notificação em andamento

Para acompanhar as notificações, você pode considerar a pergunta: "O que foi que eu bloqueei e que fez eu não estar mais bloqueado?" Escolha suas prioridades de notificação de acompanhamento.

Por exemplo, você pode decidir acompanhar nesta ordem:
  - Problemas e pull requests atribuídos a você. Imediatamente feche quaisquer problemas ou pull requests que você possa e adicione atualizações. Conforme necessário, salve as notificações para revisar mais tarde.
  - Revise as notificações na caixa de entrada salva, especialmente atualizações não lidas. Se o thread não for mais relevante, desmarque {% octicon "bookmark" aria-label="The bookmark icon" %} para remover a notificação da caixa de entrada salva e não salvá-lo.

## Gerenciando notificações de baixa prioridade

Após fazer a triagem das notificações de prioridade mais alta, revise as notificações restantes, como notificações de participação. Considere estas perguntas:
  - Você pode cancelar a inscrição desta notificação? Esta notificação está concluída e pronta para ser marcada como **Concluída**?
  {% tip %}

  **Dica:** ao cancelar a inscrição de uma notificação, você não receberá novas atualizações, a menos que comece a participar do thread ou seja @mentioned ou que uma equipe da qual esteja participando seja @mentioned. Quando você marca uma notificação como **Concluída**, a notificação é removida da exibição da caixa de entrada principal e pode ser exibida com a consulta `is:read`. Para obter mais informações, confira "[Como gerenciar notificações na sua caixa de entrada](/github/managing-subscriptions-and-notifications-on-github/managing-notifications-from-your-inbox#triaging-options)".

  {% endtip %}
  - Você gostaria de receber atualizações futuras quando este problema ou a pull request forem fechados ou reabertos, ou quando uma pull request for mesclada? Para obter mais informações sobre essas opções, confira "[Como fazer a triagem de uma só notificação](/github/managing-subscriptions-and-notifications-on-github/triaging-a-single-notification#customizing-when-to-receive-future-updates-for-an-issue-or-pull-request)".
  - Gostaria de evitar receber notificações como esta no futuro? Em caso afirmativo, considere cancelar a assinatura. Para obter mais informações, confira "[Como gerenciar assinaturas para a atividade no GitHub](/github/managing-subscriptions-and-notifications-on-github/managing-subscriptions-for-activity-on-github)".

## Limpando suas notificações menos importantes

Escolha qual tipo de notificações são mais rápidas e mais fáceis para você fazer triagem e remover da sua caixa de entrada, idealmente, fazendo várias notificações de uma só vez.

Por exemplo, você pode decidir limpar as notificações nesta ordem:
  - Notificações participantes das quais você pode cancelar a inscrição.
  - Atualizações de repositório que não são relevantes para manter ou acompanhar.

Para obter mais informações sobre como gerenciar várias notificações em sua caixa de entrada ao mesmo tempo, confira "[Gerenciando notificações em sua caixa de entrada](/github/managing-subscriptions-and-notifications-on-github/managing-notifications-from-your-inbox#triaging-multiple-notifications-at-the-same-time)".

Você também pode considerar alterar suas configurações de notificação ou cancelar a assinatura dessas atualizações, se possível. Para obter mais informações, confira "[Configurando notificações](/github/managing-subscriptions-and-notifications-on-github/configuring-notifications)" ou "[Gerenciando assinaturas de atividades no GitHub](/github/managing-subscriptions-and-notifications-on-github/managing-subscriptions-for-activity-on-github)".
