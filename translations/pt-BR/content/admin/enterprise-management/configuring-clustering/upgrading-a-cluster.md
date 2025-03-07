---
title: Atualizar o cluster
intro: 'Use o shell administrativo (SSH) para atualizar o cluster do {% data variables.product.prodname_ghe_server %} para a versão mais recente.'
redirect_from:
  - /enterprise/admin/clustering/upgrading-a-cluster
  - /enterprise/admin/enterprise-management/upgrading-a-cluster
  - /admin/enterprise-management/upgrading-a-cluster
versions:
  ghes: '*'
type: how_to
topics:
  - Clustering
  - Enterprise
  - Upgrades
ms.openlocfilehash: 040fe0d315f440c8d5489b04f808dbe1f6c67972
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2022
ms.locfileid: '145095947'
---
## Atualizar com hotpatch
{% data reusables.enterprise_installation.hotpatching-explanation %} O script de instalação do hotpatch instala o hotpatch em cada nó do cluster e reinicia os serviços na sequência adequada para evitar tempo de inatividade.

1. Faça backup de seus dados com [{% data variables.product.prodname_enterprise_backup_utilities %}](https://github.com/github/backup-utils#readme).
2. No shell administrativo de qualquer nó, use o comando `ghe-cluster-hotpatch` para instalar o hotpatch mais recente. Você pode informar uma URL para o hotpatch ou baixá-la manualmente e especificar um nome de arquivo local.
  ```shell
  $ ghe-cluster-hotpatch https://<em>HOTPATCH-URL/FILENAME</em>.hpkg
  ```

## Atualizar com pacote de atualização
Atualize para a versão mais recente do cluster do {% data variables.product.prodname_ghe_server %} usando um pacote de atualização. Por exemplo, você pode atualizar de `2.11` para `2.13`

### Preparar para a atualização

1. Veja em [Configuração de rede do cluster](/enterprise/admin/guides/clustering/cluster-network-configuration) a versão para a qual você está atualizando e atualize sua configuração conforme necessário.
2. Faça backup de seus dados com [{% data variables.product.prodname_enterprise_backup_utilities %}](https://github.com/github/backup-utils#readme).
3. Programe um período de manutenção para os usuários finais do cluster do {% data variables.product.prodname_ghe_server %}, já que ele ficará indisponível para uso regular durante a atualização. O modo de manutenção bloqueia o acesso de usuários e impede alterações de dados durante a atualização do cluster.
4. Na página de download do [ {% data variables.product.prodname_ghe_server %}](https://enterprise.github.com/download), copie a URL do arquivo *.pkg* de atualização para a área de transferência.
5. No shell administrativo de qualquer nó, use o comando `ghe-cluster-each` combinado com `curl` para baixar o pacote de versão para cada nó em uma única etapa. Como argumento, use a URL que você copiou na etapa anterior.
  ```shell
  $ ghe-cluster-each -- "cd /home/admin && curl -L -O  https://<em>PACKAGE-URL</em>.pkg"
  > ghe-app-node-1:   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
  > ghe-app-node-1:                                  Dload  Upload   Total   Spent    Left  Speed
  > 100  496M  100  496M    0     0  24.2M      0  0:00:20  0:00:20 --:--:-- 27.4M
  > ghe-data-node-2:   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
  > ghe-data-node-2:                                  Dload  Upload   Total   Spent    Left  Speed
  > 100  496M  100  496M    0     0  21.3M      0  0:00:23  0:00:23 --:--:-- 25.8M
  > ghe-data-node-1:   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
  > ghe-data-node-1:                                  Dload  Upload   Total   Spent    Left  Speed
  > 100  496M  100  496M    0     0  19.7M      0  0:00:25  0:00:25 --:--:-- 25.6M
  > ghe-app-node-2:   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
  > ghe-app-node-2:                                  Dload  Upload   Total   Spent    Left  Speed
  > 100  496M  100  496M    0     0  19.8M      0  0:00:25  0:00:25 --:--:-- 17.6M
  > ghe-data-node-3:   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
  > ghe-data-node-3:                                  Dload  Upload   Total   Spent    Left  Speed
  > 100  496M  100  496M    0     0  19.7M      0  0:00:25  0:00:25 --:--:-- 25.5M
  ```
6. Identifique o nó MySQL primário, que é definido como `mysql-master = <hostname>` em `cluster.conf`. Esse nó será atualizado por último.

### Atualizar os nós de cluster

1. Habilite o modo de manutenção de acordo com a janela agendada conectando-se ao shell administrativo de qualquer nó de cluster e executando `ghe-cluster-maintenance -s`.
2. **Com exceção do nó MySQL primário**, conecte-se ao shell administrativo de cada um dos nós do {% data variables.product.prodname_ghe_server %}.
Execute o comando `ghe-upgrade`, fornecendo o nome do arquivo de pacote que você baixou na Etapa 4 de [Preparação para atualizar](#preparing-to-upgrade):
  ```shell
  $ ghe-upgrade <em>PACKAGE-FILENAME</em>.pkg
  > *** verifying upgrade package signature...
  >  497MB 0:00:04 [ 117MB/s] [==========================================>] 100%            
  > gpg: Signature made Fri 19 Feb 2016 02:33:50 PM UTC using RSA key ID 0D65D57A
  > gpg: checking the trustdb
  > gpg: 3 marginal(s) needed, 1 complete(s) needed, PGP trust model
  > gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
  > gpg: Good signature from "GitHub Enterprise (Upgrade Package Key) > <enterprise@github.com>"
  ```
3. Assim que for concluído, o processo de atualização reinicializará o nó. Verifique se é possível usar `ping` em cada nó após a reinicialização.
4. Conecte-se ao shell administrativo do nó primário MySQL. Execute o comando `ghe-upgrade`, fornecendo o nome do arquivo de pacote que você baixou na Etapa 4 de [Preparação para atualizar](#preparing-to-upgrade):
  ```shell
  $ ghe-upgrade <em>PACKAGE-FILENAME</em>.pkg
  > *** verifying upgrade package signature...
  >  497MB 0:00:04 [ 117MB/s] [==========================================>] 100%            
  > gpg: Signature made Fri 19 Feb 2016 02:33:50 PM UTC using RSA key ID 0D65D57A
  > gpg: checking the trustdb
  > gpg: 3 marginal(s) needed, 1 complete(s) needed, PGP trust model
  > gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
  > gpg: Good signature from "GitHub Enterprise (Upgrade Package Key) > <enterprise@github.com>"
  ```
5. Assim que for concluído, o processo de atualização reinicializará o nó primário MySQL. Verifique se é possível usar `ping` em cada nó após a reinicialização.{% ifversion ghes %}
6. Conecte-se ao shell administrativo do nó MySQL primário e execute o comando `ghe-cluster-config-apply`.
7. Quando `ghe-cluster-config-apply` estiver concluído, verifique se os serviços estão em um estado íntegro executando `ghe-cluster-status`.{% endif %}
8. Saia do modo de manutenção do shell administrativo de qualquer nó executando `ghe-cluster-maintenance -u`.
