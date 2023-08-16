---
title: O exportador da página
description: Saiba como usar o Exportador de página AEM.
exl-id: 15d08758-cf75-43c0-9818-98a579d64183
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 0%

---

# O exportador da página{#the-page-exporter}

O AEM permite exportar uma página como uma página da Web completa, incluindo imagens, `.js` e `.css` arquivos.

Depois de configurado, você solicita uma exportação de página do seu navegador, substituindo `html` com `export.zip` no URL. Isso gera um arquivo (zip) contendo a página renderizada em formato html, junto com os ativos referenciados. Todos os caminhos na página (por exemplo, caminhos para imagens) são regravados para apontar para os arquivos incluídos no arquivamento ou para os recursos no servidor. O arquivo compactado (zip) pode ser baixado do navegador.

>[!NOTE]
>
>Dependendo do navegador e das configurações, o download será:
>* um arquivo morto (`<page-name>.export.zip`)
>* uma pasta (`<page-name>`); efetivamente o arquivo já expandido

## Exportar uma página {#exporting-a-page}

As etapas a seguir descrevem como exportar uma página e supor que exista um modelo de exportação para o site. Um modelo de exportação define como uma página é exportada e é específico do site. Para criar um template de exportação, consulte a [Criação de uma configuração do Exportador de página para seu site](#creating-a-page-exporter-configuration-for-your-site) seção.

Para exportar uma página:

1. Navegue até a página desejada na **Sites** console.

1. Selecione a página e abra o **Propriedades** diálogo.

1. Selecione o **Avançado** guia.

1. Expanda a **Exportar** para selecionar um modelo de exportação.
Selecione o modelo necessário para o site e confirme com **OK**.

1. Selecionar **Salvar e fechar** para fechar a caixa de diálogo de propriedades da página.

1. Solicitar a página para exportação, substituindo o sufixo `html` com `export.zip` no URL.

   Por exemplo:
   * localhost:4502/content/we-retail/language-masters/en.html

   É acessado via:
   * localhost:4502/content/we-retail/language-masters/en.export.zip

1. Baixe o arquivo morto no sistema de arquivos.

1. Em seu sistema de arquivos, descompacte o arquivo, se necessário. Depois de expandida, haverá uma pasta com o mesmo nome da página selecionada. Esta pasta contém:

   * a subpasta `content`, que é a raiz de uma série de subpastas que refletem o caminho para a página no repositório

      * dentro dessa estrutura há o arquivo html para a página selecionada (`<page-name>.html`)

   * outros recursos (`.js` arquivos, `.css` arquivos, imagens etc.) estão localizados de acordo com as configurações no modelo de exportação

1. Abra o arquivo html da página (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) no navegador para verificar a renderização.

## Criação de uma configuração do Exportador de página para seu site {#creating-a-page-exporter-configuration-for-your-site}

O exportador da página baseia-se na [Estrutura de sincronização de conteúdo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html). As configurações disponíveis na variável **Propriedades da página** são modelos de exportação que definem as dependências necessárias para uma página.

Quando uma exportação de página é acionada, o modelo de exportação é referenciado e o caminho da página e do design são aplicados dinamicamente. O arquivo zip é então criado usando a funcionalidade padrão Sincronização de conteúdo.

Uma instalação pronta para uso do AEM inclui um modelo padrão em `/etc/contentsync/templates/default`.

* Esse é o modelo de fallback quando nenhum modelo de exportação é encontrado no repositório.

* A variável `default` O modelo mostra como uma exportação de página pode ser configurada, para que o possa servir como base para um novo modelo de exportação.

* Para exibir a estrutura de nó do modelo em seu navegador como formato JSON, solicite o seguinte URL:
  `http://localhost:4502/etc/contentsync/templates/default.json`

O método mais fácil para criar um modelo de exportador de página é:

* copie o `default` modelo,

* atribuir um novo nome, apropriado ao seu site,

* em seguida, faça as atualizações necessárias.

Para criar um template completamente novo:

1. Entrada **CRXDE Lite**, crie um nó abaixo `/etc/contentsync/templates`:

   * `Name`: um nome apropriado ao seu site; por exemplo, `<mysite>`. O nome aparece na caixa de diálogo de propriedades da página ao escolher o modelo do exportador da página.

   * `Type`: `nt:unstructured`

2. Abaixo do nó do modelo, chamado aqui `mysite`, crie uma estrutura de nó usando os nós de configuração descritos abaixo.

## Ativar um modelo do exportador da página para suas páginas {#activating-a-page-exporter-configuration-for-your-pages}

Após configurar o template, é necessário disponibilizá-lo:

1. No CRXDE, navegue até a página desejada no `/content` filial. Pode ser uma página individual ou a página raiz de uma subárvore.

1. No `jcr:content` da página cria a propriedade:
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: caminho para o modelo; por exemplo: `/etc/contentsync/templates/mysite`

### Nós de configuração do exportador da página {#page-exporter-configuration-nodes}

O modelo consiste em uma estrutura de nó, pois usa o [Estrutura de sincronização de conteúdo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html).  Cada nó tem um `type` propriedade que define uma ação específica no processo de criação do arquivo zip.

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

Os seguintes nós podem ser usados para criar um template de exportação:

* `page`
O nó da página é usado para copiar o html da página para o arquivo zip. Ele tem as seguintes características:

   * É um nó obrigatório.
   * Está localizado abaixo de `/etc/contentsync/templates/<mysite>`.
   * É definido com a propriedade `Name`definir como `page`.
   * O tipo de nó é `nt:unstructured`

  A variável `page` possui as seguintes propriedades:

   * A `type` propriedade definida com o valor `pages`.

   * Ele não tem um `path` como o caminho da página atual é copiada dinamicamente para a configuração.
  <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
O nó rewrite define como os links são reescritos na página exportada. Os links regravados podem apontar para os arquivos incluídos no arquivo zip ou para os recursos no servidor.
  <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
O nó de design é usado para copiar o design usado para a página exportada. Ele tem as seguintes características:

   * É opcional.
   * Está localizado abaixo de `/etc/contentsync/templates/<mysite>`.
   * É definido com a propriedade `Name` definir como `design`.
   * O tipo de nó é `nt:unstructured`.

  A variável `design` possui as seguintes propriedades:

   * A `type` propriedade definida com o valor `copy`.

   * Ele não tem um `path` propriedade, pois o caminho da página atual é copiado dinamicamente para a configuração.

* `generic`
Um nó genérico é usado para copiar recursos como clientlibs `.js` ou `.css` para o arquivo zip. Ele tem as seguintes características:

   * É opcional.
   * Está localizado abaixo de `/etc/contentsync/templates/<mysite>`.
   * Não tem um nome específico.
   * O tipo de nó é `nt:unstructured`.
   * Tem um `type` propriedade e `type` propriedades relacionadas. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

  Por exemplo, o nó de configuração a seguir copia a variável `mysite.clientlibs.js` para o arquivo zip:

  ```xml
  "mysite.clientlibs.js": {
      "extension": "js",
      "type": "clientlib",
      "path": "/etc/designs/mysite/clientlibs",
      "jcr:primaryType": "nt:unstructured"
  }
  ```

**Implementar uma configuração personalizada**

Configurações personalizadas também são possíveis.

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

Para atender a alguns requisitos específicos, pode ser necessário implementar uma [manipulador de atualização personalizado](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html).

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## Exportar programaticamente uma página {#programmatically-exporting-a-page}

Para exportar uma página de forma programática, você pode usar o [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) Serviço OSGI. Esse serviço permite:

* Exportar uma página e gravar na resposta do servlet HTTP.
* Exporte uma página e salve o arquivo zip em um local específico.

O servlet vinculado ao `export` seletor e o `zip` A extensão do usa o serviço PageExporter.

## Resolução de problemas {#troubleshooting}

Se você tiver um problema com o download do arquivo zip, poderá excluir o `/var/contentsync` no repositório e envie a solicitação de exportação novamente.
