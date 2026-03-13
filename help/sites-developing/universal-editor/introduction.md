---
title: O Editor universal
description: Saiba mais sobre a flexibilidade do Universal Editor e como ele pode ajudar a potencializar suas experiências headless usando o AEM 6.5.
feature: Developing
role: Developer
exl-id: 7bdf1fcc-02b9-40bc-8605-e6508a84d249
source-git-commit: 28e44586c6a8596037a44fa10d21b3fdcdea1606
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 1%

---


# O Editor universal {#universal-editor}

Saiba mais sobre a flexibilidade do Universal Editor e como ele pode ajudar a potencializar suas experiências headless usando o AEM 6.5.

## Visão geral {#overview}

O Universal Editor é um editor visual versátil que faz parte do Adobe Experience Manager Sites. Ele permite que os autores façam a edição &quot;o que você vê é o que você obtém&quot; (WYSIWYG) de qualquer experiência headless.

* Os autores se beneficiam da flexibilidade do Universal Editor, pois ele oferece suporte à mesma edição visual consistente para todas as formas de conteúdo headless do AEM.
* Os desenvolvedores se beneficiam da versatilidade do Universal Editor, pois ele também suporta a verdadeira dissociação da implementação. Ele permite que os desenvolvedores utilizem praticamente qualquer estrutura ou arquitetura de sua escolha, sem impor restrições de SDK ou tecnologia.

Consulte a [documentação do AEM as a Cloud Service sobre o Universal Editor](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) para obter mais detalhes.

## Arquitetura {#architecture}

O Editor universal é um serviço que trabalha em conjunto com o AEM para criar conteúdo em headless.

* O Editor Universal está hospedado em `https://experience.adobe.com/#/aem/editor/canvas` e pode editar páginas renderizadas pelo AEM 6.5.
* A página do AEM é lida pelo Editor universal por meio do dispatcher da instância do autor do AEM.
* O Universal Editor Service, que é executado no mesmo host que a Dispatcher, grava as alterações de volta na instância de autor do AEM.

![Fluxo de autor usando o Editor Universal](assets/author-flow.png)

## Requisitos {#requirements}

O Editor Universal é compatível com:

* AEM 6.5
   * Há suporte para hospedagem local e AMS*.
* [AEM 6.5 LTS](https://experienceleague.adobe.com/en/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * Há suporte para hospedagem local e AMS*.
* [AEM as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction)

Este documento se concentra no suporte do AEM 6.5 ao Universal Editor. Para usar o Editor universal com o AEM 6.5, será necessário:

* AEM 6.5 with service pack 23 or higher
   * Service packs 21 and 22 are also supported with [a feature pack.](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-6.5.21-universal-editor-1.0.0.zip).
* Dispatcher properly configured

>[!NOTE]
>
>*Se você usa o Adobe Managed Services (AMS), entre em contato com o engenheiro de sucesso do cliente (CSE) se desejar usar o Universal Editor.

## Configurar {#setup}

Para testar o Editor universal, será necessário:

1. [Configurar um Serviço do Editor Universal local.](#set-up-ue)
1. [Ajuste o dispatcher para permitir o Universal Editor Service.](#update-dispatcher)

Após concluir a instalação, você pode [instrumentar seus aplicativos para usar o Editor Universal.](#instrumentation)

### Configure Services {#configure-services}

The Universal Editor leverages several packages for which additional configuration is needed.

#### Set the SameSite Attribute for the `login-token` cookie. {#samesite-attribute}

1. Abra o Gerenciador de configurações.
   * `http://<host>:<port>/system/console/configMgr`
1. Localize o **Manipulador de autenticação de token do Adobe Granite** na lista e clique em **Alterar os valores de configuração**.
1. Na caixa de diálogo, altere o atributo **SameSite do cookie de token de logon** (`token.samesite.cookie.attr`) para `Partitioned`.
1. Clique em **Salvar**.

#### Remova a opção X-Frame de cabeçalhos `SAMEORIGIN`. {#sameorigin}

1. Abra o Gerenciador de configurações.
   * `http://<host>:<port>/system/console/configMgr`
1. Locate **Apache Sling Main Servlet** in the list and click **Edit the configuration values**.
1. Exclua o valor `X-Frame-Options=SAMEORIGIN` do atributo (**)** Cabeçalhos de resposta adicionais`sling.additional.response.headers` se ele existir.
1. Clique em **Salvar**.

#### Configure o Manipulador de autenticação de parâmetro de consulta do Adobe Granite. {#query-parameter}

1. Abra o Gerenciador de configurações.
   * `http://<host>:<port>/system/console/configMgr`
1. Localize o **Manipulador de Autenticação de Parâmetro de Consulta do Adobe Granite** na lista e clique em **Editar os valores de configuração**.
1. No campo **Caminho** (`path`), adicione `/` para habilitar.
   * Um valor vazio desativa o manipulador de autenticação.
1. Clique em **Salvar**.

#### Define for which content paths or `sling:resourceTypes` the Universal Editor shall be opened. {#paths}

1. Abra o Gerenciador de configurações.
   * `http://<host>:<port>/system/console/configMgr`
1. Locate **Universal Editor URL Service** in the list and click **Edit the configuration values**.
1. Defina para quais caminhos de conteúdo ou `sling:resourceTypes` o Editor Universal deve ser aberto.
   * In the **Universal Editor Opening Mapping** field, provide the paths for which the Universal Editor is opened.
   * In the **Sling:resourceTypes which shall be opened by Universal Editor** field, provide a list of resources which are opened directly by the Universal Editor.
1. Clique em **Salvar**.
1. Check your [externalizer configuration](/help/sites-developing/externalizer.md) and ensure at a minimum you have the local, author, and publish environments set as in the following example.

   ```text
   "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
   "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
   "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]"
   ```

Once those configuration steps are complete, AEM will open the Universal Editor for pages in the following order.

1. O AEM verificará os mapeamentos em `Universal Editor Opening Mapping` e se o conteúdo estiver em qualquer caminho definido nele, o Editor Universal será aberto para ele.
1. Para conteúdo não nos caminhos definidos em `Universal Editor Opening Mapping`, o AEM verifica se o `resourceType` do conteúdo corresponde aos definidos em **Sling:resourceTypes que devem ser abertos pelo Universal Editor** e se o conteúdo corresponde a um desses tipos, o Universal Editor será aberto para ele em `${author}${path}.html`.
1. Caso contrário, o AEM abrirá o Editor de páginas.

As variáveis a seguir estão disponíveis para definir seus mapeamentos em `Universal Editor Opening Mapping`.

* `path`: Caminho de conteúdo do recurso a ser aberto
* `localhost`: Entrada do externalizador para `localhost` sem esquema, ex.: `localhost:4502`
* `author`: Entrada externalizadora para autor sem esquema, ex.: `localhost:4502`
* `publish`: Entrada do externalizador para publicação sem esquema, ex.: `localhost:4503`
* `preview`: Entrada do externalizador para visualização sem esquema, ex.: `localhost:4504`
* `env`: `prod`, `stage`, `dev` com base nos modos de execução do Sling definidos
* `token`: Token de consulta necessário para `QueryTokenAuthenticationHandler`

Exemplo de mapeamentos:

* Abrir todas as páginas em `/content/foo` no Autor do AEM:
   * `/content/foo:${author}${path}.html?login-token=${token}`
   * Isto resulta na abertura de `https://localhost:4502/content/foo/x.html?login-token=<token>`
* Abrir todas as páginas em `/content/bar` em um servidor NextJS remoto, fornecendo todas as variáveis como informações
   * `/content/bar:nextjs.server${path}?env=${env}&author=https://${author}&publish=https://${publish}&login-token=${token}`
   * Isto resulta na abertura de `https://nextjs.server/content/bar/x?env=prod&author=https://localhost:4502&publish=https://localhost:4503&login-token=<token>`

### Configurar o Serviço do Editor Universal {#set-up-ue}

Com o AEM atualizado e configurado, você pode configurar um Serviço local do Universal Editor para desenvolvimento e teste locais.

1. Instale o Node.js versão >=20.
1. Baixe e descompacte o Serviço Universal Editor mais recente da [Distribuição de Software](https://experienceleague.adobe.com/pt-br/docs/experience-cloud/software-distribution/home)
1. Configure o Universal Editor Service por meio de variáveis de ambiente ou arquivo `.env`.
   * [Consulte a documentação do AEM as a Cloud Service Universal Editor para obter detalhes.](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service)
   * Observe que talvez seja necessário usar a opção `UES_MAPPING` se for necessária a regravação interna do IP.
1. Executar `universal-editor-service.cjs`

### Update the Dispatcher {#update-dispatcher}

With AEM configured and a local Universal Editor service running, you will need to allow a reverse proxy for the new service [in the dispatcher.](https://experienceleague.adobe.com/pt-br/docs/experience-manager-dispatcher/using/dispatcher)

1. Adjust the vhost file of author instance to include a reverse proxy.

   ```html
   <IfModule mod_proxy.c>
    ProxyPass "/universal-editor" "http://localhost:8080"
    ProxyPassReverse "/universal-editor" "http://localhost:8080"
   </IfModule>
   ```

   >[!NOTE]
   >
   >8080 is the default port. Se você alterou isto usando o parâmetro `UES_PORT` em [seu arquivo `.env`,](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/local-dev#setting-up-service) ajuste o valor da porta aqui de acordo.

1. Reinicie o Apache.

## Instrumentar o aplicativo {#instrumentation}

Com o AEM atualizado e um Serviço do editor universal local em execução, você pode começar a editar conteúdo headless usando o editor universal.

No entanto, seu aplicativo deve ser instrumentado para aproveitar o Editor universal. Isso envolve a inclusão de metatags para instruir o editor sobre como e onde persistir o conteúdo. Os detalhes desta instrumentação estão disponíveis na [documentação do Universal Editor para AEM as a Cloud Service.](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/getting-started#instrument-page)

Observe que, ao seguir a documentação do Universal Editor com AEM as a Cloud Service, as seguintes alterações se aplicam ao usá-lo com o AEM 6.5.

* O protocolo na meta tag deve ser `aem65` em vez de `aem`.

  ```html
  <meta name="urn:adobe:aue:system:aemconnection" content={`aem65:${getAuthorHost()}`}/>
  ```

* O ponto de extremidade do Serviço do Editor Universal deve ser anunciado por meio de uma meta tag.

  ```html
  <meta name="urn:adobe:aue:config:service" content={`${getAuthorHost()}/universal-editor`}/>
  ```

* Na seção `plugins` da definição de componentes, deve ser usado `aem65` em vez de `aem`.

>[!TIP]
>
>Para obter um guia abrangente de introdução do Universal Editor para desenvolvedores, consulte o documento [Visão geral do Universal Editor para desenvolvedores do AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/developer-overview) na documentação do AEM as a Cloud Service, tendo em mente as alterações necessárias para o suporte ao AEM 6.5, conforme mencionado nesta seção.

## Diferenças entre o AEM 6.5 e o AEM as a Cloud Service {#differences}

O Editor universal no AEM 6.5 funciona amplamente da mesma forma que no AEM as a Cloud Service, incluindo a interface do usuário e grande parte da configuração. Há, no entanto, diferenças que devem ser observadas.

* O Universal Editor no 6.5 é compatível apenas com o caso de uso headless.
* Setup of the Universal Editor varies slightly for 6.5 ([as described](#setup) in the current document).
* The Universal Editor in 6.5 uses a different asset picker and a different Content Fragment picker than AEM as a Cloud Service.
