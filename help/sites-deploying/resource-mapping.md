---
title: Mapeamento de recursos
seo-title: Mapeamento de recursos
description: Saiba como definir redirecionamentos, URLs personalizados e hosts virtuais para o AEM usando o mapeamento de recursos.
seo-description: Saiba como definir redirecionamentos, URLs personalizados e hosts virtuais para o AEM usando o mapeamento de recursos.
uuid: 2ca2d0e4-6f90-4ecc-82db-26991f08c66f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 3582a4d8-a47b-467a-9e25-cb45f969ec93
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Mapeamento de recursos{#resource-mapping}

O mapeamento de recursos é usado para definir redirecionamentos, URLs personalizados e hosts virtuais para o AEM.

Por exemplo, você pode usar esses mapeamentos para:

* Prefixe todas as solicitações com `/content` o prefixo para que a estrutura interna fique oculta dos visitantes do site.
* Defina um redirecionamento para que todas as solicitações da `/content/en/gateway` página do site sejam redirecionadas para `https://gbiv.com/`.

Um mapeamento HTTP possível prefixa todas as solicitações `localhost:4503` com `/content`. Um mapeamento como esse pode ser usado para ocultar a estrutura interna dos visitantes ao site, conforme permite:

`localhost:4503/content/we-retail/en/products.html`

a ser acessado usando:

`localhost:4503/we-retail/en/products.html`

como o mapeamento adicionará automaticamente o prefixo `/content` ao `/we-retail/en/products.html`.

>[!CAUTION]
>
>URLs personalizados não suportam padrões regex.

>[!NOTE]
>
>Consulte a documentação Sling e [Mapeamentos para Resolução](https://sling.apache.org/site/resources.html) de recursos e [Recursos](https://sling.apache.org/site/mappings-for-resource-resolution.html) para obter mais informações.

## Exibindo Definições de Mapeamento {#viewing-mapping-definitions}

Os mapeamentos de duas listas que o Resolvedor de recursos do JCR avalia (de cima para baixo) para localizar uma correspondência.

Essas listas podem ser visualizadas (junto com as informações de configuração) na opção **JCR ResourceResolver** do console Felix; por exemplo, `https://<*host*>:<*port*>/system/console/jcrresolver`:

* ConfiguraçãoMostra a configuração atual (conforme definido para o [Apache Sling Resource Resolver](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver)).

* Teste de configuraçãoIsso permite inserir um URL ou caminho de recurso. Clique em **Resolver** ou em **Mapa** para confirmar como o sistema transformará a entrada.

* **Entradas** do mapa do resolvedorA lista de entradas usadas pelos métodos ResourceResolver.resolve para mapear URLs para Recursos.

* **Mapeamento de entradas** do mapaA lista de entradas usadas pelos métodos ResourceResolver.map para mapear Caminhos de recursos para URLs.

As duas listas mostram várias entradas, incluindo aquelas definidas como padrões pelos aplicativos. Muitas vezes, o objetivo é simplificar os URLs para o usuário.

As listas emparelham um **Padrão**, uma expressão regular correspondente à solicitação, com uma **Substituição** que define o redirecionamento a ser imposto.

Por exemplo, a variável

**Padrão**`^[^/]+/[^/]+/welcome$`

acionará:

**Substituição** `/libs/cq/core/content/welcome.html`.

para redirecionar uma solicitação:

`https://localhost:4503/welcome` ``

para:

`https://localhost:4503/libs/cq/core/content/welcome.html`

Novas definições de mapeamento são criadas no repositório.

>[!NOTE]
>
>Há muitos recursos disponíveis que ajudam a explicar como definir expressões regulares. por exemplo, [https://www.regular-expressions.info/](https://www.regular-expressions.info/).

### Criar definições de mapeamento no AEM {#creating-mapping-definitions-in-aem}

Em uma instalação padrão do AEM, você pode encontrar a pasta:

`/etc/map/http`

Essa é a estrutura usada ao definir mapeamentos para o protocolo HTTP. Outras pastas ( `sling:Folder`) podem ser criadas em `/etc/map` qualquer outro protocolo que você deseja mapear.

#### Configurar um redirecionamento interno para /content {#configuring-an-internal-redirect-to-content}

Para criar o mapeamento que prefixa qualquer solicitação para https://localhost:4503/ com `/content`:

1. Usando o CRXDE, navegue até `/etc/map/http`.

1. Criar um novo nó:

   * **Tipo** `sling:Mapping`Esse tipo de nó é destinado a esses mapeamentos, embora seu uso não seja obrigatório.

   * **Nome** `localhost_any`

1. Clique em **Salvar tudo**.
1. **Adicione** as seguintes propriedades a este nó:

   * **Nome** `sling:match`

      * **Tipo** `String`

      * **Valor**`localhost.4503/`
   * **Nome** `sling:internalRedirect`

      * **Tipo** `String`

      * **Valor**`/content/`


1. Clique em **Salvar tudo**.

Isso lidará com uma solicitação como:
`localhost:4503/geometrixx/en/products.html`como se:
`localhost:4503/content/geometrixx/en/products.html`tinham sido solicitados.

>[!NOTE]
>
>Consulte [Recursos](https://sling.apache.org/site/mappings-for-resource-resolution.html) na Documentação do Sling para obter mais informações sobre as propriedades de sling disponíveis e como elas podem ser configuradas.

>[!NOTE]
>
>É possível usar `/etc/map.publish` para manter as configurações do ambiente de publicação. Eles devem ser replicados e o novo local ( `/etc/map.publish`) configurado para o Local **de** mapeamento do Resolvedor [de recursos do](/help/sites-deploying/osgi-configuration-settings.md#apacheslingresourceresolver) Apache Sling do ambiente de publicação.

