---
title: Gerenciando objetos LFS do Git em arquivos do seu repositório
shortTitle: 'Managing {% data variables.large_files.product_name_short %} objects in archives'
intro: 'Você pode escolher se os objetos {% data variables.large_files.product_name_long %} ({% data variables.large_files.product_name_short %}) estão incluídos nos arquivos de código-fonte, como arquivos ZIP e tarballs que {% data variables.product.product_name %} cria para seu repositório.'
permissions: 'People with admin permissions for a repository can manage whether {% data variables.large_files.product_name_short %} objects are included in archives of the repository.'
versions:
  fpt: '*'
  ghec: '*'
topics:
  - Repositories
redirect_from:
  - /github/administering-a-repository/managing-git-lfs-objects-in-archives-of-your-repository
  - /github/administering-a-repository/managing-repository-settings/managing-git-lfs-objects-in-archives-of-your-repository
ms.openlocfilehash: 64bad4c056a29ceffc465065c84a7424c870049f
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2022
ms.locfileid: '145127033'
---
## Sobre os objetos {% data variables.large_files.product_name_short %} nos arquivos

O {% data variables.product.product_name %} cria arquivos de código-fonte do seu repositório na forma de arquivos ZIP e tarballs. As pessoas podem baixar esses arquivos na página principal do seu repositório ou como ativos de versão. Por padrão, os objetos {% data variables.large_files.product_name_short %} não estão incluídos nesses arquivos, apenas os arquivos de ponteiro para esses objetos. Para melhorar a usabilidade dos arquivos no seu repositório, você pode optar por incluir os objetos do {% data variables.large_files.product_name_short %}. Para serem incluídos, os objetos {% data variables.large_files.product_name_short %} devem ser cobertos por regras de rastreamento em um arquivo *.gitattributes* com commit no repositório.

Sevocê optar por incluir os objetos {% data variables.large_files.product_name_short %}  nos arquivos de seu repositório, cada download desses arquivos contará para o uso de largura de banda de sua conta. Cada conta recebe {% data variables.large_files.initial_bandwidth_quota %} por mês de largura de banda gratuitamente, e você pode pagar pelo uso adicional. Para obter mais informações, confira "[Sobre o uso de armazenamento e largura de banda](/github/managing-large-files/about-storage-and-bandwidth-usage)" e "[Como gerenciar a cobrança do {% data variables.large_files.product_name_long %}](/billing/managing-billing-for-git-large-file-storage)".

Se você usar um servidor LFS externo (configurado no *.lfsconfig*), esses arquivos LFS não serão incluídos nos arquivos do repositório. O arquivo conterá apenas arquivos que têm commit para {% data variables.product.product_name %}.

## Gerenciando objetos {% data variables.large_files.product_name_short %} nos arquivos

{% data reusables.repositories.navigate-to-repo %} {% data reusables.repositories.sidebar-settings %}
3. Em "Arquivos", selecione ou desmarque **Incluir objetos do {% data variables.large_files.product_name_short %} nos arquivos**.
  ![Caixa de seleção usada para incluir os objetos do {% data variables.large_files.product_name_short %} nos arquivos](/assets/images/help/repository/include-git-lfs-objects-checkbox.png)
