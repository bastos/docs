---
title: コミットメッセージの変更
redirect_from:
  - /articles/can-i-delete-a-commit-message
  - /articles/changing-a-commit-message
  - /github/committing-changes-to-your-project/changing-a-commit-message
  - /github/committing-changes-to-your-project/creating-and-editing-commits/changing-a-commit-message
intro: 'コミットメッセージに不明確、不正確、または機密情報が含まれている場合、ローカルでメッセージを修正して、{% data variables.product.product_name %}に新しいメッセージで新しいコミットをプッシュできます。 また、コミットメッセージを変更して、不足している情報を追加することも可能です。'
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
ms.openlocfilehash: fa4966da0fe443e6635b43fc9b3b11108d57cf6e
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2022
ms.locfileid: '145132571'
---
## 直近のコミットメッセージの書き換え

`git commit --amend` コマンドで、直近のコミット メッセージを変更できます。

Git では、コミットメッセージのテキストはコミットの一部として扱われます。 コミットメッセージを変更すると、コミット ID (コミットの SHA1 チェックサム) も変更されます。 実質的には、古いコミットに代わる新しいコミットを作成することになります。

## オンラインにプッシュされていないコミット

コミットがローカル リポジトリにのみ存在し、{% data variables.product.product_location %} にプッシュされていない場合、`git commit --amend` コマンドでコミット メッセージを修正できます。

1. コマンドラインで、修正したいコミットのあるリポジトリに移動します。
2. 「`git commit --amend`」と入力して **Enter** キーを押します。
3. テキストエディタでコミットメッセージを編集し、コミットを保存します。
    - コミットにトレーラーを追加することで、共作者を追加できます。 詳細については、「[複数の作者を持つコミットを作成する](/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/creating-a-commit-with-multiple-authors)」を参照してください。
{% ifversion fpt or ghec %}
    - コミットにトレーラーを追加することで、Organization の代理でコミットを作成できます。 詳細については、「[Organization の代理でコミットを作成する](/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/creating-a-commit-on-behalf-of-an-organization)」を参照してください。{% endif %}

次回のプッシュ時に、{% data variables.product.product_location %}に新たなコミットとメッセージが表示されます。

{% tip %}

Git で使うデフォルトのテキスト エディタは、`core.editor` の設定で変更できます。 詳しい情報については、Git のマニュアルにある「[基本クライアント設定](https://git-scm.com/book/en/Customizing-Git-Git-Configuration#_basic_client_configuration)」を参照してください。

{% endtip %}

## 古いまたは複数のコミットメッセージの修正

すでにコミットを {% data variables.product.product_location %}にプッシュしている場合、修正済みのメッセージでコミットをフォースプッシュする必要があります。

{% warning %}

リポジトリの履歴が変更されるため、フォースプッシュは推奨されません。 フォースプッシュを行った場合、リポジトリをすでにクローンした人はローカルの履歴を手動で修正する必要があります。 詳しい情報については、Git のマニュアルにある「[上流リベースからのリカバリ](https://git-scm.com/docs/git-rebase#_recovering_from_upstream_rebase)」を参照してください。

{% endwarning %}

**直近でプッシュされたコミットのメッセージを変更する**

1. [上記の手順](/articles/changing-a-commit-message#commit-has-not-been-pushed-online)に従って、コミット メッセージを修正します。
2. `push --force-with-lease` コマンドにより、古いコミットをフォース プッシュで上書きします。
  ```shell
  $ git push --force-with-lease origin <em>example-branch</em>
  ```

**古いまたは複数のコミット メッセージを変更する**

複数のコミットまたは古いコミットの、メッセージを修正する必要がある場合は、インタラクティブなリベースを利用した後にフォースプッシュして、コミットの履歴を変更できます。

1. コマンドラインで、修正したいコミットのあるリポジトリに移動します。
2. `git rebase -i HEAD~n` コマンドで、デフォルトのテキスト エディタに直近 `n` コミットの一覧を表示できます。

    ```shell
    # Displays a list of the last 3 commits on the current branch
    $ git rebase -i HEAD~3
    ```
    リストは、以下のようになります。

    ```shell
    pick e499d89 Delete CNAME
    pick 0c39034 Better README
    pick f7fde4a Change the commit message but push the same commit.

    # Rebase 9fdb3bd..f7fde4a onto 9fdb3bd
    #
    # Commands:
    # p, pick = use commit
    # r, reword = use commit, but edit the commit message
    # e, edit = use commit, but stop for amending
    # s, squash = use commit, but meld into previous commit
    # f, fixup = like "squash", but discard this commit's log message
    # x, exec = run command (the rest of the line) using shell
    #
    # These lines can be re-ordered; they are executed from top to bottom.
    #
    # If you remove a line here THAT COMMIT WILL BE LOST.
    #
    # However, if you remove everything, the rebase will be aborted.
    #
    # Note that empty commits are commented out
    ```
3. 各コミット メッセージを変更する前に、`pick` を `reword` に置換してください。
  ```shell
  pick e499d89 Delete CNAME
  reword 0c39034 Better README
  reword f7fde4a Change the commit message but push the same commit.
  ```
4. コミット一覧のファイルを保存して閉じます。
5. 生成された各コミットコミットファイルに、新しいコミットメッセージを入力し、ファイルを保存して閉じます。
6. 変更を GitHub にプッシュする準備ができたら、push --force コマンドを使用して、古いコミットを強制的にプッシュします。
```shell
$ git push --force origin <em>example-branch</em>
```

インタラクティブ リベースに関する詳しい情報については、Git のマニュアルにある「[インタラクティブ モード](https://git-scm.com/docs/git-rebase#_interactive_mode)」を参照してください。

{% tip %}

この方法でも、コミットメッセージを修正すると、ID が新しい新たなコミットメッセージが作成されます。 ただしこの方法では、修正したコミットに続く各コミットも新しい ID を取得します。各コミットには、親の ID が含まれているためです。

{% endtip %}

{% warning %}

修正したコミットをフォースプッシュしても元のコミットは {% data variables.product.product_name %}から削除されない場合がありますので、元のコミットメッセージに機密情報が含まれている場合は注意してください。 古いコミットは、以降のクローンには含まれませんが、{% data variables.product.product_name %}にキャッシュされ、コミット ID でアクセスできます。 リモートリポジトリから古いコミットメッセージをパージするには、古いコミット ID を添えて {% data variables.contact.contact_support %}にお問い合わせください。

{% endwarning %}

## 参考資料

* 「[コミットに署名する](/articles/signing-commits)」
