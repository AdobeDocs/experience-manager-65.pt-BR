---
title: O Exportador de Página
description: Saiba como usar o Exportador de página do AEM.
translation-type: tm+mt
source-git-commit: 6aee1506b54a932bae8f2521fce4488de7d2a52a
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---


# O Exportador de Página{#the-page-exporter}

O AEM permite exportar uma página como uma página da Web completa, incluindo imagens `.js` e `.css` arquivos.

Depois de configurada, você solicita uma exportação de página do navegador, substituindo `html` por `export.zip` no URL. Isso gera um arquivo de arquivamento (zip), que contém a página renderizada no formato html, juntamente com os ativos referenciados. Todos os caminhos na página (por exemplo, caminhos para imagens) são reescritos para apontar para os arquivos incluídos no arquivo ou para os recursos no servidor. O arquivo de arquivamento (zip) pode ser baixado do seu navegador.

>[!NOTE]
>
>Dependendo do seu navegador e das configurações, o download será:
>* um arquivo de arquivamento (`<page-name>.export.zip`)
>* uma pasta (`<page-name>`); com eficácia, o arquivo de arquivamento já foi expandido


## Exportar uma página {#exporting-a-page}

As etapas a seguir descrevem como exportar uma página e presumem que existe um modelo de exportação para o site. Um modelo de exportação define a forma como uma página é exportada e é específica para seu site. Para criar um modelo de exportação, consulte a seção [Criando uma Configuração de Exportador de Página para seu Site](#creating-a-page-exporter-configuration-for-your-site) .

Para exportar uma página:

1. Navegue até a página desejada no console **Sites** .

1. Selecione a página e abra a caixa de diálogo **Propriedades** .

1. Select the **Advanced** tab.

1. Expanda o campo **Exportar** para selecionar um modelo de exportação.
Selecione o modelo necessário para o site e confirme com **OK**.

1. Selecione **Salvar e fechar** para fechar a caixa de diálogo de propriedades da página.

1. Solicite a exportação da página, substituindo o sufixo `html` por `export.zip` no URL.

   Por exemplo:
   * localhost:4502/content/we-retail/language-masters/en.html

   É acessado via:
   * localhost:4502/content/we-retail/language-masters/en.export.zip


1. Baixe o arquivo para o seu sistema de arquivos.

1. No sistema de arquivos, descompacte o arquivo, se necessário. Depois de expandida, haverá uma pasta com o mesmo nome da página selecionada. Esta pasta contém:

   * a subpasta `content`, que é a raiz de uma série de subpastas que refletem o caminho para a página no repositório

      * nesta estrutura, há o arquivo html para a página selecionada (`<page-name>.html`)
   * outros recursos (`.js` arquivos, `.css` arquivos, imagens etc.) estão localizados de acordo com as configurações no modelo de exportação


1. Abra o arquivo html da página (`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`) no navegador para verificar a renderização.

## Criando uma Configuração de Exportador de Página para seu Site {#creating-a-page-exporter-configuration-for-your-site}

O exportador de página é baseado na estrutura [de sincronização de](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)conteúdo. As configurações disponíveis na caixa de diálogo Propriedades **da** página são modelos de exportação que definem as dependências necessárias para uma página.

Quando uma exportação de página é acionada, o modelo de exportação é referenciado e o caminho da página e o caminho do design são aplicados dinamicamente. O arquivo zip é criado usando a funcionalidade padrão de Sincronização de conteúdo.

Uma instalação predefinida do AEM inclui um modelo predefinido em `/etc/contentsync/templates/default`.

* Este modelo é o modelo de fallback quando nenhum modelo de exportação é encontrado no repositório.

* O `default` modelo mostra como uma exportação de página pode ser configurada, de modo que possa servir como base para um novo modelo de exportação.

* Para visualização a estrutura de nó do modelo no seu navegador como formato JSON, solicite o seguinte URL:
   `http://localhost:4502/etc/contentsync/templates/default.json`

O método mais fácil para criar um novo modelo de exportador de página é:

* copiar o `default` modelo,

* atribuir um novo nome, apropriado ao seu site,

* faça as atualizações necessárias.

Para criar um modelo completamente novo:

1. No **CRXDE Lite**, crie um nó abaixo `/etc/contentsync/templates`:

   * `Name`: um nome adequado ao seu site; por exemplo, `<mysite>`. O nome aparece na caixa de diálogo de propriedades da página ao escolher o modelo de exportador de página.

   * `Type`: `nt:unstructured`

2. Abaixo do nó do modelo, chamado aqui `mysite`, crie uma estrutura de nó usando os nós de configuração descritos abaixo.

## Ativando um modelo de exportador de página para suas páginas {#activating-a-page-exporter-configuration-for-your-pages}

Depois que o modelo tiver sido configurado, é necessário disponibilizá-lo:

1. No CRXDE, navegue até a página desejada na `/content` ramificação. Pode ser uma página individual ou a página raiz de uma subárvore.

1. No `jcr:content` nó da página, crie a propriedade:
   * `Name`: `cq:exportTemplate`
   * `Type`: `String`
   * `Value`: caminho para o modelo; por exemplo: `/etc/contentsync/templates/mysite`

### Nós de configuração do exportador de páginas {#page-exporter-configuration-nodes}

O modelo consiste em uma estrutura de nó, pois usa a estrutura [de sincronização de](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/package-summary.html)conteúdo.  Cada nó tem uma `type` propriedade que define uma ação específica no processo de criação do arquivo zip.

<!-- For more details about the type property, refer to the Overview of configuration types section in the Content Sync framework page.
-->

Os nós a seguir podem ser usados para criar um modelo de exportação:

* `page`
O nó da página é usado para copiar o html da página para o arquivo zip. Tem as seguintes características:

   * É um nó obrigatório.
   * Está localizado abaixo `/etc/contentsync/templates/<mysite>`.
   * É definido com a propriedade `Name`definida como `page`.
   * O tipo de nó é `nt:unstructured`

   O `page` nó tem as seguintes propriedades:

   * Uma `type` propriedade definida com o valor `pages`.

   * Ela não tem uma `path` propriedade, pois o caminho da página atual é copiado dinamicamente para a configuração.

   <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
O nó regravar define como os links são regravados na página exportada. Os links regravados podem apontar para os arquivos incluídos no arquivo zip ou para os recursos no servidor.
   <!-- Please refer to the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
O nó de design é usado para copiar o design usado para a página exportada. Tem as seguintes características:

   * É opcional.
   * Está localizado abaixo `/etc/contentsync/templates/<mysite>`.
   * É definido com a propriedade `Name` definida como `design`.
   * O tipo de nó é `nt:unstructured`.

   O `design` nó tem as seguintes propriedades:

   * Uma `type` propriedade definida como o valor `copy`.

   * Ele não tem uma `path` propriedade, pois o caminho da página atual é copiado dinamicamente para a configuração.


* `generic`
Um nó genérico é usado para copiar recursos como clientlibs 
`.js` ou `.css` arquivos no arquivo zip. Tem as seguintes características:

   * É opcional.
   * Está localizado abaixo `/etc/contentsync/templates/<mysite>`.
   * Não tem um nome específico.
   * O tipo de nó é `nt:unstructured`.
   * Tem uma `type` propriedade e propriedades `type` relacionadas. <!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

   Por exemplo, o nó de configuração a seguir copia os `mysite.clientlibs.js` arquivos para o arquivo zip:

   ```xml
   "mysite.clientlibs.js": {
       "extension": "js",
       "type": "clientlib",
       "path": "/etc/designs/mysite/clientlibs",
       "jcr:primaryType": "nt:unstructured"
   }
   ```

**Implementação de uma configuração personalizada**

Configurações personalizadas também são possíveis.

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

Para atender a alguns requisitos específicos, talvez seja necessário implementar um manipulador [de atualizações](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/contentsync/handler/package-summary.html)personalizado.

<!-- To meet some specific requirements, you may need to implement a custom `type` property: to do so, refer to the Implementing a custom update handler section in the Content Sync page.
-->

## Exportar uma página de forma programática {#programmatically-exporting-a-page}

Para exportar uma página programaticamente, você pode usar o serviço OSGI [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) . Este serviço permite:

* Exportar uma página e gravar na resposta do servlet HTTP.
* Exporte uma página e salve o arquivo zip em um local específico.

O servlet vinculado ao `export` seletor e a `zip` extensão usa o serviço PageExporter.

## Resolução de Problemas{#troubleshooting}

Se houver um problema com o download do arquivo zip, você poderá excluir o `/var/contentsync` nó no repositório e enviar a solicitação de exportação novamente.
