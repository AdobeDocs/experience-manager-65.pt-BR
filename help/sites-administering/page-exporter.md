---
title: O Exportador de Página
seo-title: O Exportador de Página
description: Saiba como usar o Exportador de página do AEM.
seo-description: Saiba como usar o Exportador de página do AEM.
uuid: 2ca2b8f1-c723-4e6b-8c3d-f5886cd0d3f1
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6ab07b5b-ee37-4029-95da-be2031779107
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# O Exportador de Página{#the-page-exporter}

O AEM permite exportar uma página como uma página da Web completa, incluindo imagens, arquivos .js e .css.

Depois que a exportação for configurada, basta solicitar uma página no navegador, substituindo-a `html` por `export.zip` no URL e você obterá um download de arquivo zip contendo a página renderizada no formato html e os ativos referenciados. Todos os caminhos na página, por exemplo, caminhos para imagens, são reescritos para apontar para os arquivos incluídos no arquivo zip ou para os recursos no servidor.

## Exportar uma página {#exporting-a-page}

As etapas a seguir descrevem como exportar uma página e presumem que existe um modelo de configuração de exportação para o site. Um modelo de configuração define a forma como uma página é exportada e é específica para seu site. Para criar um modelo de configuração, consulte a seção [Criando uma Configuração de Exportador de Página para seu Site](#creating-a-page-exporter-configuration-for-your-site) .

Para exportar uma página:

1. No seu navegador, abra a página. Por exemplo:
1. `http://localhost:4502/content/geometrixx/en/products/triangle.html`
1. Abra a caixa de diálogo de propriedades da página, selecione a guia **Avançado** e expanda o conjunto de campos **Exportar** .

1. Clique no ícone de lente de aumento e selecione um modelo de configuração. Selecione o modelo **geometrixx** , pois é o padrão para o site Geometrixx. Clique em **OK**.

1. Clique em **OK** para fechar a caixa de diálogo de propriedades da página.
1. Solicite a página substituindo `html` por `export.zip` no URL.

1. Baixe o `<page-name>.export.zip` arquivo no seu sistema de arquivos.

1. No sistema de arquivos, descompacte o arquivo:

   * o arquivo html da página ( `<page-name>.html`) está disponível abaixo `<unzip-dir>/<page-path>`
   * outros recursos (arquivos .js, arquivos .css, imagens, etc.) estão localizados de acordo com as configurações no modelo de exportação. Neste exemplo, alguns recursos estão abaixo `<unzip-dir>/etc`, alguns abaixo `<unzip-dir>/<page-path>`.

1. Abra o arquivo html da página ( `<unzip-dir>/<page-path>.html`) no navegador para verificar a renderização.

## Criando uma Configuração de Exportador de Página para seu Site {#creating-a-page-exporter-configuration-for-your-site}

O exportador de página é baseado na estrutura de Sincronização de conteúdo. As configurações disponíveis na caixa de diálogo de propriedades da página são modelos de configuração. Eles definem todas as dependências necessárias para uma página. Quando uma exportação de página é acionada, o modelo de configuração é usado e o caminho da página e o caminho do design são aplicados dinamicamente à configuração. O arquivo zip é criado usando a funcionalidade padrão de Sincronização de conteúdo.

O AEM incorpora alguns modelos, incluindo:

* Um padrão em `/etc/contentsync/templates/default`. Este modelo:

   * É o modelo de fallback quando nenhum modelo de configuração é encontrado no repositório.
   * Pode servir como base para um novo modelo de configuração.

* Uma que é dedicada ao site **Geometrixx** , em `/etc/contentsync/templates/geometrixx`. Este modelo pode ser usado como exemplo para criar um novo.

Para criar um modelo de configuração de exportador de página:

1. No **CRXDE Lite**, crie um nó abaixo `/etc/contentsync/templates`:

   * Nome:por exemplo `mysite`. O nome aparece na caixa de diálogo de propriedades da página ao escolher o modelo de exportador de página.
   * Tipo: `nt:unstructured`

1. Abaixo do nó do modelo, chamado aqui `mysite`, crie uma estrutura de nó usando os nós de configuração descritos abaixo.

### Nós de configuração do exportador de páginas {#page-exporter-configuration-nodes}

O modelo de configuração consiste em uma estrutura de nó. Cada nó tem uma `type` propriedade que define uma ação específica no processo de criação do arquivo zip. Para obter mais detalhes sobre a propriedade type, consulte a seção Visão geral dos tipos de configuração na página da estrutura de Sincronização de conteúdo.

Os nós a seguir podem ser usados para criar um modelo de configuração de exportação:

**nó** de página O nó de página é usado para copiar a página html para o arquivo zip. Tem as seguintes características:

* É um nó obrigatório.
* Está localizado abaixo `/etc/contentsync/templates/<sitename>`.
* Seu nome é `page`.
* Seu tipo de nó é `nt:unstructured`

O `page` nó tem as seguintes propriedades:

* Uma `type` propriedade definida com o valor `pages`.

* Ela não tem uma `path` propriedade, pois o caminho da página atual é copiado dinamicamente para a configuração.

* As outras propriedades são descritas na seção Visão geral dos tipos de configuração da estrutura de sincronização de conteúdo.

**nó** de regravação O nó de regravação define como os links são regravados na página exportada. Os links regravados podem apontar para os arquivos incluídos no arquivo zip ou para os recursos no servidor.

Consulte a página Sincronização de conteúdo para obter uma descrição completa do `rewrite` nó.

**nó** de design O nó de design é usado para copiar o design usado para a página exportada. Tem as seguintes características:

* É opcional.
* Está localizado abaixo `/etc/contentsync/templates/<sitename>`.
* Seu nome é `design`.
* Seu tipo de nó é `nt:unstructured`.

O `design` nó tem as seguintes propriedades:

* Uma `type` propriedade definida como o valor `copy`.

* Ela não tem uma `path` propriedade, pois o caminho da página atual é copiado dinamicamente para a configuração.

**nó** genérico Um nó genérico é usado para copiar recursos como arquivos clientlibs .js ou .css para o arquivo zip. Tem as seguintes características:

* É opcional.
* Está localizado abaixo `/etc/contentsync/templates/<sitename>`.
* Não tem um nome específico.
* Seu tipo de nó é `nt:unstructured`.
* Tem uma `type` propriedade e quaisquer propriedades `type` relacionadas, conforme definido na seção Visão geral dos tipos de configuração da estrutura de Sincronização de conteúdo.

Por exemplo, o nó de configuração a seguir copia os arquivos geometrixx clientlibs .js para o arquivo zip:

```xml
"geometrixx.clientlibs.js": {
    "extension": "js",
    "type": "clientlib",
    "path": "/etc/designs/geometrixx/clientlibs",
    "jcr:primaryType": "nt:unstructured"
}
```

O modelo de configuração de exportação de página do **Geometrixx** mostra como uma exportação de página pode ser configurada. Para exibir a estrutura de nó do modelo no seu navegador como formato json, solicite o seguinte URL:

`http://localhost:4502/etc/contentsync/templates/geometrixx.-1.json`

**Implementação de uma configuração personalizada**

Como você pode ter notado na estrutura do nó, o modelo de configuração de exportação de página do **Geometrixx** tem um `logo` nó com uma `type` propriedade definida como `image`. Este é um tipo de configuração especial que foi criado para copiar o logotipo da imagem para o arquivo zip. Para atender a alguns requisitos específicos, talvez seja necessário implementar uma `type` propriedade personalizada: para fazer isso, consulte a seção Implementação de um manipulador de atualização personalizado na página Sincronização de conteúdo.

## Exportar uma página de forma programática {#programmatically-exporting-a-page}

Para exportar uma página programaticamente, você pode usar o serviço OSGI [PageExporter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) . Este serviço permite:

* Exportar uma página e gravar na resposta do servlet HTTP.
* Exporte uma página e salve o arquivo zip em um local específico.

O servlet vinculado ao `export` seletor e a `zip` extensão usa o serviço PageExporter.

## Resolução de Problemas{#troubleshooting}

Se houver um problema com o download do arquivo zip, você poderá excluir o `/var/contentsync` nó no repositório e enviar a solicitação de exportação novamente.

