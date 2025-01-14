---
title: Renomear um arquivo
intro: 'Você pode renomear qualquer arquivo no repositório diretamente em {% data variables.product.product_name %} ou usando a linha de comando.'
redirect_from:
  - /articles/renaming-a-file
  - /github/managing-files-in-a-repository/renaming-a-file
  - /articles/renaming-a-file-using-the-command-line
  - /github/managing-files-in-a-repository/renaming-a-file-using-the-command-line
  - /github/managing-files-in-a-repository/managing-files-on-github/renaming-a-file
  - /github/managing-files-in-a-repository/managing-files-using-the-command-line/renaming-a-file-using-the-command-line
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
topics:
  - Repositories
ms.openlocfilehash: 826c9c45ee8cace0d3e81c78fc010ac4c76f9ab1
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2022
ms.locfileid: '145126972'
---
## Renomeando um arquivo em {% data variables.product.product_name %}

A renomeação de um arquivo também oferece a oportunidade de [mover o arquivo para um novo local](/articles/moving-a-file-to-a-new-location)

{% tip %}

**Dicas**:

- Se você tentar renomear um arquivo em um repositório ao qual não tem acesso, criaremos um fork do projeto para sua conta pessoal e ajudaremos você a enviar [uma solicitação de pull](/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) para o repositório original depois que você fizer commit da alteração.
- Os nomes de arquivos criados por meio da interface da Web só podem conter caracteres alfanuméricos e hifens (`-`). Para usar outros caracteres, crie e faça commit dos arquivos localmente, depois faça push deles para o repositório.
- Alguns arquivos, como imagens, exigem que a renomeação seja feita usando a linha de comando. Para obter mais informações, confira "[Como renomear um arquivo usando a linha de comando](/articles/renaming-a-file-using-the-command-line)".

{% endtip %}

1. No repositório, navegue até o arquivo que deseja renomear.
2. No canto superior direito da exibição de arquivo, clique em {% octicon "pencil" aria-label="The edit icon" %} para abrir o editor de arquivos.
![Ícone Editar arquivo](/assets/images/help/repository/edit-file-icon.png)
3. No campo de nome do arquivo, insira o nome de arquivo que deseja atribuir. Você também pode atualizar o conteúdo do arquivo ao mesmo tempo.
![Edição de um nome de arquivo](/assets/images/help/repository/changing-file-name.png) {% data reusables.files.write_commit_message %} {% data reusables.files.choose_commit_branch %} {% data reusables.files.propose_file_change %}

## Renomear um arquivo usando a linha de comando 

Você pode usar a linha de comando para renomear qualquer arquivo do repositório.

Muitos arquivos podem ser [renomeados diretamente no {% data variables.product.product_name %}](/articles/renaming-a-file), mas alguns arquivos, como imagens, exigem que você os renomeie na linha de comando.

{% data reusables.command_line.manipulating_file_prereqs %}

{% data reusables.command_line.open_the_multi_os_terminal %} {% data reusables.command_line.switching_directories_procedural %}
3. Renomeie o arquivo especificando o nome antigo e o novo nome que deseja atribuir ao arquivo. Isso fará o stage da alteração para commit.
  ```shell
  $ git mv <em>old_filename</em> <em>new_filename</em>
  ```
4. Use `git status` para verificar os nomes de arquivos antigos e novos.
  ```shell
  $ git status
  > # On branch <em>your-branch</em>
  > # Changes to be committed:
  > #   (use "git reset HEAD <file>..." to unstage)
  > #
  > #     renamed: <em>old_filename</em> -> <em>new_filename</em>
  > #
  ```
{% data reusables.git.commit-file %}
  ```shell
  $ git commit -m "Rename file"
  # Commits the tracked changes and prepares them to be pushed to a remote repository.
  # {% data reusables.git.reset-head-to-previous-commit-codeblock %}
  ```
{% data reusables.git.git-push %}

