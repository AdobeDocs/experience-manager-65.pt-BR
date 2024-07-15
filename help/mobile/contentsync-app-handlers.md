---
title: Manipuladores de aplicativos prontos para uso
description: Siga esta página para saber mais sobre os manipuladores prontos para uso do Adobe PhoneGap Enterprise com AEM.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1408'
ht-degree: 0%

---

# Manipuladores de aplicativos prontos para uso{#out-of-the-box-app-handlers}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Consulte as diretrizes a seguir para desenvolver Manipuladores de sincronização de conteúdo:

* Os manipuladores devem implementar *com.day.cq.contentsync.handler.ContentUpdateHandler* (diretamente ou estendendo uma classe que o faça)
* Os manipuladores podem estender *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* O manipulador só deverá relatar true se tiver atualizado o cache do ContentSync. Falsamente relatar verdadeiro permitirá que o AEM crie uma atualização.
* O manipulador só deve atualizar o cache se o conteúdo for realmente alterado. Não grave no cache se um branco não for necessário e evite uma criação de atualização desnecessária.

## Manipuladores prontos para uso {#out-of-the-box-handlers}

O seguinte lista os manipuladores de aplicativo prontos para uso:

**mobileapppages** Renderiza páginas de aplicativo.

* ***tipo - Cadeia de caracteres*** - mobileapppages
* ***caminho - Cadeia de caracteres*** - caminho para uma página
* ***extensão - Cadeia de caracteres*** - Extensão que deve ser usada na solicitação. Para páginas, isso é quase sempre *html*, mas outras ainda são possíveis.

* ***seletor - Cadeia de caracteres*** - Seletores opcionais separados por ponto. Exemplos comuns são *touch* para renderizar versões móveis de uma página.

* ***profundo - Booleano*** - Propriedade booleana opcional que determina se as páginas secundárias também devem ser incluídas. O valor padrão é *true.*

* ***includeImages - Booleano*** - Propriedade booleana opcional determinando se as imagens devem ser incluídas. O valor padrão é *true*.

   * Por padrão, somente componentes de imagem com um tipo de recurso de fundação/componentes/imagem são considerados para inclusão.

* ***includeVideos - Booleano*** - A propriedade booleana opcional determina se os vídeos devem ser incluídos. O valor padrão é *true*.

* ***includeModifiedPagesOnly - Booleano*** - Se for falso ou omitido, renderize todas as páginas e verifique as atualizações na renderização. Se verdadeiro, baseia o diffs nas alterações em uma página lastModified.
* ***+ regravação (nó)***
  ***- relativeParentPath - String*** - o caminho para gravar todos os outros caminhos relativos a.

>[!NOTE]
>
>O tipo de recurso dos componentes de imagem e vídeo afetados por este manipulador é definido pela configuração das propriedades do *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Serviço OSGi MobilePagesUpdateHandler*.

**mobilepageassets** Coleta ativos da página de aplicativos.

**mobilecontentlisting** Lista o conteúdo do zip ContentSync. Isso é usado pelo js do lado do cliente no dispositivo para fazer a cópia inicial do arquivo necessária para aplicativos AEM.

Esse manipulador deve ser adicionado a qualquer configuração AEM Apps ContentSync.

* ***tipo - Cadeia de caracteres - mobilecontentlisting***
* ***caminho*** - Cadeia de caracteres - manter vazio, deve estar presente para ser visto como um manipulador válido, mas o caminho é inferido como o cache ContentSync atual. Esse valor é ignorado.
* ***targetRootDirectory* -**Cadeia de caracteres - o prefixo a ser adicionado a caminhos como uma raiz de destino para atualização de conteúdo para este manipulador.
* ***pedir - Longo* -**Ordenar que o ContentSync execute este manipulador. Esse número deve ser definido como maior do que todos os outros manipuladores, como 100. Ela deve ser executada após os manipuladores de conteúdo tradicionais.

```xml
{
  "files": [
    "config.xml",
    "res/screens/ios/screen-ipad-portrait-2x.png",
    "res/screens/ios/screen-ipad-landscape.png",
    "res/screens/ios/screen-iphone-portrait-2x.png",
    "res/screens/ios/screen-iphone-landscape.png",
    "res/screens/ios/screen-iphone-portrait.png",
    "apps/weretail-app/components/splash-page/clientlibs.css",
    ...
    "pge-content-packages.json"
  ],
  "count": 382,
  "lastModified": 1422902754733
}
```

**mobilecontentpackageslisting** Lista o pacote de conteúdo AEM em um determinado aplicativo e o serverURL para o qual fazer solicitações de atualização. Isso é usado no js do lado do cliente no dispositivo para solicitar atualizações de conteúdo

O manipulador deve ser usado na configuração ContentSync do shell do aplicativo AEM (nó com pge-type=app-instance)

* ***tipo - Cadeia de caracteres - mobilecontentpackageslisting***
* ***caminho **-**Cadeia de caracteres*** - Caminho para um shell de aplicativo (nó com pge-type=app-instance).
* ***targetRootDirectory - String*** - o prefixo a ser adicionado aos caminhos como uma raiz de destino para atualização de conteúdo para este manipulador.
* ***pedir - Longo* -**Ordenar que o ContentSync execute este manipulador. Esse número deve ser definido como maior do que todos os outros manipuladores, como 100. Ela deve ser executada após os manipuladores de conteúdo tradicionais.

>[!NOTE]
>
>O bloco de código a seguir não é uma implementação exata e deve ser usado como exemplo de referência:

```xml
{
  "content": [
    {
      "name": "en",
      "title": "We Retail Mobile App - English",
      "type": "CONTENT",
      "path": "/content/phonegap/weretail-outdoors/en",
      "updatePath": "/content/phonegap/weretail/en/jcr:content/pge-app/app-config"
    },
    {
      "name": "shell",
      "title": "We Retail Mobile App",
      "type": "INSTANCE",
      "path": "/content/phonegap/weretail-outdoors/shell",
      "updatePath": "/content/phonegap/weretail/shell/jcr:content/pge-app/app-config"
    }
  ],
  "serverURL": "http://localhost:4503/"
}
```

**widgetconfig** Inclui um config.xml atualizado que mescla todas as edições feitas pelo Centro de Comandos com um config.xml fornecido. Se esse manipulador não for incluído, os detalhes do aplicativo alterados por meio da interface de Administração não serão incluídos no cache.

Este manipulador deve ser usado em uma configuração ContentSync do Shell do aplicativo AEM (nó com pge-type=[app-instance]).

* ***tipo - Cadeia de caracteres* - **widgetconfig
* ***caminho **-**Cadeia de caracteres*** - Caminho para qualquer nó filho do shell do aplicativo (nó com pge-type=[app-instance]).
* ***targetRootDirectory - String*** - o prefixo a ser adicionado aos caminhos como uma raiz de destino para atualização de conteúdo para este manipulador.
* ***targetIconDirectory - Cadeia de caracteres*** - o diretório no qual colocar os ícones do aplicativo

**mobileADBMobileConfigJSON** Inclua o arquivo ADBMobileConfig.JSON se o serviço de nuvem AMS tiver sido configurado.

Isso é usado no momento da compilação para configurar o plug-in AMS para suporte analítico.

O manipulador deve ser usado na configuração ContentSync do shell do aplicativo AEM (nó com pge-type=app-instance)

* ***tipo - Cadeia de caracteres*** - mobileADBMobileConfigJSON
* ***caminho - Cadeia de caracteres*** - Caminho para um shell de aplicativo (nó com pge-type=app-instance ou um RT que estende /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - Cadeia de caracteres*** - o prefixo a ser adicionado aos caminhos como uma raiz de destino para atualização de conteúdo para este manipulador

**notificationsconfig** Extrai configurações de notificações necessárias no dispositivo. As propriedades são extraídas da respectiva configuração do serviço de nuvem do serviço de push associada ao aplicativo.

As propriedades que não são do AEM no nó jcr:content do serviço em nuvem são extraídas e adicionadas ao arquivo JSON **pge-notifications-config.json** para inclusão na raiz www do conteúdo do aplicativo.

As propriedades AEM são aquelas com espaçamento de nome &quot;cq&quot;, &quot;sling&quot; ou &quot;jcr&quot;. Outras propriedades podem ser excluídas usando a propriedade &quot;excludeProperties&quot; no nó de configuração de sincronização de conteúdo.

* ***tipo - Cadeia de caracteres*** - notificationsconfig
* ***excludeProperties - String[]*** - propriedades a serem excluídas

**contentsyncconfigcontent** Coleta conteúdo de uma configuração ContentSync existente.

* ***tipo - Cadeia de caracteres*** - contentsyncconfigcontent
* ***caminho - Cadeia de caracteres*** - Caminho para um de:

   * outra configuração ContentSync
   * para um Pacote de conteúdo (usará a propriedade phonegap-exportTemplate para localizar a configuração ContentSync)
   * para um recurso móvel (app-content&#39;s serão encontrados nesse recurso e, se esses pacotes de conteúdo tiverem uma propriedade page-includeInBuild que for verdadeira, o phonegap-exportTemplate será usado para encontrar sua configuração ContentSync)

* ***autoCreateFirstUpdateBeforeImport - Booleano*** - se verdadeiro, crie uma **atualização** inicial na configuração de destino antes de importar, se uma vez ainda não existir

* ***autoFillBeforeImport - Booleano*** - se verdadeiro, atualize/preencha a configuração de destino antes de importar
* ***configSuffix - Cadeia de caracteres*** - uma cadeia de caracteres a ser anexada ao caminho indicado na propriedade &quot;phonegap-exportTemplate&quot; do conteúdo do aplicativo. Isso pode ser usado para distinguir modelos de exportação diferentes. Por exemplo, essa propriedade pode ser definida como **&quot;-dev&quot;** para indicar que *&quot;/../../../appconfig-dev&quot;* deve ser usado (em vez de *&quot;/../../../appconfig&quot;*).

**app-assets** Inclui todos os ativos associados a uma instância do aplicativo. Esse manipulador incluirá todos os ativos encontrados no caminho especificado, juntamente com os ativos referenciados pela propriedade appAssetPath de uma instância do aplicativo.

* ***tipo - Cadeia de caracteres*** - app-assets

* ***caminho **-**Cadeia de caracteres*** - caminho para um local em uma instância do aplicativo onde os ativos do aplicativo são armazenados

**mobileapproffers** Um novo manipulador de sincronização de conteúdo foi introduzido para o caso de uso do Personalization para renderizar o conteúdo direcionado. O manipulador &quot;mobileapproffers&quot; sabe como renderizar as ofertas de público-alvo associadas que foram criadas pelo autor de conteúdo. O manipulador mobileapproffers estende o manipulador de atualização de páginas abstratas, portanto, muitas das propriedades são semelhantes. Os detalhes do manipulador mobileapproffers têm as seguintes propriedades.

O manipulador mobileappsoffers estende o manipulador mobileappspages e adiciona as seguintes propriedades:

* ***locationRoot - String*** - especifique o local do aplicativo móvel
* ***includePageTypes - String*** - o padrão é oferecer suporte a cq/personalization/components/teaserpage e cq/personalization/components/offerproxy
* ***seletor - Cadeia de caracteres*** - deve ser definido como pendente
* ***caminho - Cadeia de caracteres***- o caminho para a marca da campanha

**mobileappconfig** O manipulador de sincronização de conteúdo mobileappconfig fornece uma maneira de injetar dados JSON no MobileAppsConfig.json. Para registrar uma classe de provedor, os desenvolvedores adicionarão sua classe MobileAppsInfoProvider à lista de provedores. O manipulador iterará sobre a lista de MobileAppsInfoProviders e permitirá que o provedor insira dados no arquivo json resultante. As listas de propriedades que este manipulador aceita são:

* ***caminho **-**Cadeia de caracteres*** - o caminho para um nó de instância de aplicativo com pge-type=app-instance ou um RT que estende /libs/mobileapps/core/components/instance
* ***provedores - Cadeia de caracteres*** `[]` - a lista de MobileAppsInfoProviders totalmente qualificados
* ***targetRootDirectory - Cadeia de caracteres*** - o diretório no qual gravar o arquivo MobileAppsConfig.json.
* **fileName - String** - nome opcional do arquivo no qual gravar o JSON; o padrão é MobileAppsConfig.json

É possível ter vários manipuladores mobileappconfig configurados, cada um com um conjunto exclusivo de provedores gravando em arquivos JSON diferentes.

### Teste de manipuladores de sincronização de conteúdo {#testing-content-sync-handlers}

**Etapas para Verificar Integridade** Limpar cache

* Limpar o cache
* Executar o manipulador (cache atualizado)
* Execute o manipulador novamente (o cache não deve ser atualizado)

**Etapas para depuração**

* Executar sua configuração
* Exportar sua configuração ou revisão no dispositivo
* Se a renderização falhar, verifique se há *estilos/ativos/bibliotecas* ausentes ou verifique se há caminhos inválidos para *estilos/ativos/bibliotecas*

**Logs** Habilite o log de depuração ContentSync por meio das configurações do agente OSGI no pacote `com.day.cq.contentsync`. Isso permitirá que você acompanhe quais manipuladores foram executados e se eles atualizaram o cache e relataram a atualização do cache.

## Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Criação para Adobe PhoneGap Enterprise com AEM](/help/mobile/phonegap.md)
* [Administração de conteúdo para o Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Para começar a usar o desenvolvimento de aplicativos do AEM Mobile, clique [aqui](/help/mobile/getting-started-aem-mobile.md).
