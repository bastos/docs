---
title: Gerenciar um domínio personalizado do seu site do GitHub Pages
intro: 'É possível definir ou atualizar determinados registros DNS e as configurações de repositório para apontar o domínio padrão do seu site do {% data variables.product.prodname_pages %} para um domínio personalizado.'
redirect_from:
  - /articles/quick-start-setting-up-a-custom-domain
  - /articles/setting-up-an-apex-domain
  - /articles/setting-up-a-www-subdomain
  - /articles/setting-up-a-custom-domain
  - /articles/setting-up-an-apex-domain-and-www-subdomain
  - /articles/adding-a-cname-file-to-your-repository
  - /articles/setting-up-your-pages-site-repository
  - /articles/managing-a-custom-domain-for-your-github-pages-site
  - /github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site
product: '{% data reusables.gated-features.pages %}'
versions:
  fpt: '*'
  ghec: '*'
topics:
  - Pages
shortTitle: Manage a custom domain
ms.openlocfilehash: ad96d0be88614e8294e29de74fd7112cfed1bc46
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2022
ms.locfileid: '147710320'
---
Pessoas com permissões de administrador para um repositório podem configurar um domínio personalizado de um site do {% data variables.product.prodname_pages %}.

## Sobre a configuração de domínio personalizado

Lembre-se de adicionar o domínio personalizado ao seu site do {% data variables.product.prodname_pages %} antes de configurar o domínio personalizado com o provedor DNS. Se você configurar o domínio personalizado com o provedor DNS sem adicioná-lo ao {% data variables.product.product_name %}, outra pessoa conseguirá hospedar um site em um dos seus subdomínios.

{% windows %}

O comando `dig`, que pode ser usado para verificar a configuração correta dos registros DNS, não está incluído no Windows. Para verificar se os registros DNS estão configurados corretamente, instale o [BIND](https://www.isc.org/bind/).

{% endwindows %}

{% note %}

**Observação:** as alterações de DNS podem levar até 24 horas para serem propagadas.

{% endnote %}

## Configurando um subdomínio

Para configurar um subdomínio `www` ou personalizado, como `www.example.com` ou `blog.example.com`, você precisa adicionar seu domínio às configurações do repositório. Em seguida, configure um registro CNAME com seu provedor DNS.

{% data reusables.pages.navigate-site-repo %} {% data reusables.repositories.sidebar-settings %} {% data reusables.pages.sidebar-pages %}
4. Em "Domínio personalizado", digite seu domínio personalizado e clique em **Salvar**. Se você estiver publicando seu site de um branch, isso criará um commit que adiciona um arquivo `CNAME` à raiz do branch de origem. Se você estiver publicando seu site com um fluxo de trabalho de {% data variables.product.prodname_actions %}, nenhum arquivo `CNAME` será criado. Para obter mais informações sobre a sua fonte de publicação, confira "[Como configurar uma fonte de publicação para o seu site do GitHub Pages](/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)."
  ![Botão Salvar domínio personalizado](/assets/images/help/pages/save-custom-subdomain.png)
5. Navegue até o provedor DNS e crie um registro `CNAME` que aponte o subdomínio para o domínio padrão do seu site. Por exemplo, se você quiser usar o subdomínio `www.example.com` para seu site de usuário, crie um registro `CNAME` que aponte `www.example.com` para `<user>.github.io`. Caso deseje usar o subdomínio `another.example.com` para seu site de organização, crie um registro `CNAME` que aponte `another.example.com` para `<organization>.github.io`. O registro `CNAME` deve sempre apontar para `<user>.github.io` ou `<organization>.github.io`, excluindo o nome do repositório. {% data reusables.pages.contact-dns-provider %} {% data reusables.pages.default-domain-information %}

{% indented_data_reference reusables.pages.wildcard-dns-warning spaces=3 %} {% data reusables.command_line.open_the_multi_os_terminal %}
6. Para confirmar se o registro DNS foi configurado corretamente, use o comando `dig`, substituindo _WWW.EXAMPLE.COM_ pelo subdomínio.
```shell
    $ dig <em>WWW.EXAMPLE.COM</em> +nostats +nocomments +nocmd
    > ;<em>WWW.EXAMPLE.COM.</em>                     IN      A
    > <em>WWW.EXAMPLE.COM.</em>              3592    IN      CNAME   <em>YOUR-USERNAME</em>.github.io.
    > <em>YOUR-USERNAME</em>.github.io.      43192   IN      CNAME   <em> GITHUB-PAGES-SERVER </em>.
    > <em> GITHUB-PAGES-SERVER </em>.         22      IN      A       192.0.2.1
```
{% data reusables.pages.build-locally-download-cname %} {% data reusables.pages.enforce-https-custom-domain %}

## Configurando um domínio apex

Para configurar um domínio apex, como `example.com`, você precisa configurar um domínio personalizado nas configurações do seu repositório e pelo menos um registro `ALIAS`, `ANAME` ou `A` com seu provedor DNS.

{% data reusables.pages.www-and-apex-domain-recommendation %} Para obter mais informações, confira "[Como configurar um subdomínio](#configuring-a-subdomain)".

{% data reusables.pages.navigate-site-repo %} {% data reusables.repositories.sidebar-settings %} {% data reusables.pages.sidebar-pages %}
4. Em "Domínio personalizado", digite seu domínio personalizado e clique em **Salvar**. Se você estiver publicando seu site de um branch, isso criará um commit que adiciona um arquivo `CNAME` à raiz do branch de origem. Se você estiver publicando seu site com um fluxo de trabalho de {% data variables.product.prodname_actions %}, nenhum arquivo `CNAME` será criado. Para obter mais informações sobre a sua fonte de publicação, confira "[Como configurar uma fonte de publicação para o seu site do GitHub Pages](/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)."
  ![Botão Salvar domínio personalizado](/assets/images/help/pages/save-custom-apex-domain.png)
5. Navegue até o provedor DNS e crie um registro `ALIAS`, `ANAME` ou `A`. Crie também registros `AAAA` para suporte ao IPv6. {% data reusables.pages.contact-dns-provider %}
    - Para criar um registro `ALIAS` ou um registro `ANAME`, aponte seu domínio apex para o domínio padrão do seu site. {% data reusables.pages.default-domain-information %}
    - Para criar registros `A`, aponte seu domínio apex para os endereços IP do {% data variables.product.prodname_pages %}.
      ```shell
      185.199.108.153
      185.199.109.153
      185.199.110.153
      185.199.111.153
      ```
    - Para criar registros `AAAA`, aponte seu domínio apex para os endereços IP do {% data variables.product.prodname_pages %}.
      ```shell
      2606:50c0:8000::153
      2606:50c0:8001::153
      2606:50c0:8002::153
      2606:50c0:8003::153
      ```

{% indented_data_reference reusables.pages.wildcard-dns-warning spaces=3 %} {% data reusables.command_line.open_the_multi_os_terminal %}
6. Para confirmar se o registro DNS foi configurado corretamente, use o comando `dig`, substituindo _EXAMPLE.COM_ pelo domínio apex. Confirme que os resultados correspondem aos endereços IP do {% data variables.product.prodname_pages %} acima.
   - Para registros `A`.
    ```shell
    $ dig <em>EXAMPLE.COM</em> +noall +answer -t A
    > <em>EXAMPLE.COM</em>     3600    IN A     185.199.108.153
    > <em>EXAMPLE.COM</em>     3600    IN A     185.199.109.153
    > <em>EXAMPLE.COM</em>     3600    IN A     185.199.110.153
    > <em>EXAMPLE.COM</em>     3600    IN A     185.199.111.153
    ```
   - Para registros `AAAA`.
    ```shell
    $ dig <em>EXAMPLE.COM</em> +noall +answer -t AAAA
    > <em>EXAMPLE.COM</em>     3600    IN AAAA     2606:50c0:8000::153
    > <em>EXAMPLE.COM</em>     3600    IN AAAA     2606:50c0:8001::153
    > <em>EXAMPLE.COM</em>     3600    IN AAAA     2606:50c0:8002::153
    > <em>EXAMPLE.COM</em>     3600    IN AAAA     2606:50c0:8003::153
    ```
{% data reusables.pages.build-locally-download-cname %} {% data reusables.pages.enforce-https-custom-domain %}

## Como configurar um domínio apex e a variante de subdomínio `www`

Quando você usar um domínio apex, recomendamos que você configure seu site do {% data variables.product.prodname_pages %} para hospedar o conteúdo no domínio apex e na variante de subdomínio `www`.

Para configurar um subdomínio `www` ao lado do domínio apex, primeiro, você precisa configurar um domínio apex criando um registro `ALIAS`, `ANAME` ou `A` com o provedor DNS. Para obter mais informações, confira "[Como configurar um domínio apex](#configuring-an-apex-domain)".

Depois de configurar o domínio apex, você deverá configurar um registro CNAME com seu provedor DNS.

1. Navegue até o provedor DNS e crie um registro `CNAME` que aponte `www.example.com` para o domínio padrão do seu site: `<user>.github.io` ou `<organization>.github.io`. Não inclua o nome do repositório. {% data reusables.pages.contact-dns-provider %} {% data reusables.pages.default-domain-information %}
2. Para confirmar se o registro DNS foi configurado corretamente, use o comando `dig`, substituindo _WWW.EXAMPLE.COM_ pela variante de subdomínio `www`.
```shell
    $ dig <em>WWW.EXAMPLE.COM</em> +nostats +nocomments +nocmd
    > ;<em>WWW.EXAMPLE.COM.</em>                     IN      A
    > <em>WWW.EXAMPLE.COM.</em>              3592    IN      CNAME   <em>YOUR-USERNAME</em>.github.io.
    > <em>YOUR-USERNAME</em>.github.io.      43192   IN      CNAME   <em> GITHUB-PAGES-SERVER </em>.
    > <em> GITHUB-PAGES-SERVER </em>.         22      IN      A       192.0.2.1
```
## Remover um domínio personalizado

{% data reusables.pages.navigate-site-repo %} {% data reusables.repositories.sidebar-settings %} {% data reusables.pages.sidebar-pages %}
4. Em "Domínio personalizado", clique em **Remover**.
  ![Botão Salvar domínio personalizado](/assets/images/help/pages/remove-custom-domain.png)

## Protegendo seu domínio personalizado

{% data reusables.pages.secure-your-domain %} Para obter mais informações, confira "[Como verificar seu domínio personalizado do {% data variables.product.prodname_pages %}](/pages/configuring-a-custom-domain-for-your-github-pages-site/verifying-your-custom-domain-for-github-pages)".

## Leitura adicional

- "[Solução de problemas de domínios personalizados e do {% data variables.product.prodname_pages %}](/articles/troubleshooting-custom-domains-and-github-pages)"
