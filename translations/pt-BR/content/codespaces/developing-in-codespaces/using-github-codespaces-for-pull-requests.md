---
title: Como usar o GitHub Codespaces em solicitações de pull
shortTitle: Pull requests
intro: 'Você pode usar {% data variables.product.prodname_github_codespaces %} no seu fluxo de trabalho de desenvolvimento para criar e revisar solicitações de pull, além de abordar comentários de revisão.'
product: '{% data reusables.gated-features.codespaces %}'
versions:
  fpt: '*'
  ghec: '*'
type: how_to
topics:
  - Codespaces
  - Visual Studio Code
  - Developer
redirect_from:
  - /codespaces/developing-in-codespaces/using-codespaces-for-pull-requests
ms.openlocfilehash: d4ac4d4b8003600c95293f3939f547cd73639884
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2022
ms.locfileid: '147111384'
---
## Sobre as solicitações de pull do {% data variables.product.prodname_github_codespaces %}

{% data variables.product.prodname_github_codespaces %} fornece a você muitas das funcionalidades que você pode precisar para trabalhar com solicitações de pull:

- [Criar uma solicitação de pull](/codespaces/developing-in-codespaces/using-source-control-in-your-codespace#raising-a-pull-request) – Usando os comandos do terminal e do Git ou a exibição de Controle do Código-Fonte, você pode criar solicitações de pull da mesma forma que faria no {% data variables.product.prodname_dotcom_the_website %}. Se o repositório usar um modelo de pull request, você poderá usá-lo na visualização de controle de origem.
- [Abrir uma solicitação de pull](#opening-a-pull-request-in-codespaces) – Você pode abrir uma solicitação de pull existente em um codespace, desde que tenha acesso de codespace no branch que está sendo mesclado.
- [Revisar uma solicitação de pull](#reviewing-a-pull-request-in-codespaces) – Depois de abrir uma solicitação de pull em um codespace, use a exibição "Solicitação de Pull do GitHub" para adicionar comentários de revisão e aprovar solicitações de pull. Use também o {% data variables.product.prodname_codespaces %} para [ver comentários de revisão](#view-comments-from-a-review-in-codespaces).

## Abrir um pull request em {% data variables.product.prodname_codespaces %}

{% data reusables.repositories.sidebar-pr %}

2. Na lista de pull requests, clique no pull request que deseja abrir em {% data variables.product.prodname_codespaces %}.
3. No lado direito da tela, clique em **{% octicon "code" aria-label="The code icon" %} Código**. 
4. Na guia {% data variables.product.prodname_codespaces %}, clique em **Criar codespace no BRANCH**.
  ![Opção usada para abrir uma PR em um codespace](/assets/images/help/codespaces/open-with-codespaces-pr.png)

## Revendo um pull request em {% data variables.product.prodname_codespaces %}

{% data reusables.codespaces.review-pr %}

Para obter mais informações sobre como revisar uma solicitação de pull, confira "[Como revisar as alterações propostas em uma solicitação de pull](/github/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/reviewing-proposed-changes-in-a-pull-request)".

## Visualizar de uma revisão em {% data variables.product.prodname_codespaces %}

Depois de receber comentários sobre uma solicitação de pull, você pode [abri-la em um codespace](#opening-a-pull-request-in-codespaces) para ver os [comentários de revisão](#reviewing-a-pull-request-in-codespaces). A partir de lá você pode responder a comentários, adicionar reações ou ignorar a revisão. 

  ![Opção para abrir RP em um codespace](/assets/images/help/codespaces/incorporating-codespaces.png)
