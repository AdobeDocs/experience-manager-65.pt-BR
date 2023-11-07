---
title: Manipuladores de aplicativos prontos para uso
seo-title: Out of the Box App Handlers
description: Siga esta página para saber mais sobre os manipuladores prontos para uso do Adobe PhoneGap Enterprise com AEM.
seo-description: Follow this page to learn about the out-of-the-box handlers for Adobe PhoneGap Enterprise with AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 0%

---

# Manipuladores de aplicativos prontos para uso{#out-of-the-box-app-handlers}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Consulte as diretrizes a seguir para desenvolver Manipuladores de sincronização de conteúdo:

* Os manipuladores devem implementar *com.day.cq.contentsync.handler.ContentUpdateHandler* (seja diretamente ou estendendo uma classe que o faz)
* Os manipuladores podem estender *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* O manipulador só deverá relatar true se tiver atualizado o cache do ContentSync. Falsamente relatar verdadeiro permitirá que o AEM crie uma atualização.
* O manipulador só deve atualizar o cache se o conteúdo for realmente alterado. Não grave no cache se um branco não for necessário e evite uma criação de atualização desnecessária.

## Manipuladores prontos para uso {#out-of-the-box-handlers}

O seguinte lista os manipuladores de aplicativo prontos para uso:

**mobileapppages** Renderiza páginas do aplicativo.

* ***type - String*** - mobileapppages
* ***path - String*** - caminho para uma página
* ***extension - String*** - Extensão que deve ser usada na solicitação. Para páginas, isso é quase sempre *html*, mas outros ainda são possíveis.

* ***seletor - String*** - Seletores opcionais separados por ponto. Exemplos comuns são *toque* para renderizar versões móveis de uma página.

* ***deep - Booleano*** - Propriedade booleana opcional que determina se as páginas secundárias também devem ser incluídas. O valor padrão é *verdadeiro.*

* ***includeImages - Booleano*** - Propriedade booleana opcional que determina se as imagens devem ser incluídas. O valor padrão é *true*.

   * Por padrão, somente componentes de imagem com um tipo de recurso de fundação/componentes/imagem são considerados para inclusão.

* ***includeVídeos - Booleano*** - A propriedade booleana opcional determina se os vídeos devem ser incluídos. O valor padrão é *true*.

* ***includeModifiedPagesOnly - Booleano*** - Se for falso ou omitido, renderiza todas as páginas e verifica as atualizações na renderização. Se verdadeiro, baseia o diffs nas alterações em uma página lastModified.
* ***+ regravação (nó)***
  ***- relativeParentPath - String*** - o caminho no qual gravar todos os outros caminhos relativos.

>[!NOTE]
>
>O tipo de recurso dos componentes de imagem e vídeo afetados por esse manipulador é definido pela configuração das propriedades do *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Serviço OSGi MobilePagesUpdateHandler*.

**mobilepageassets** Coleta ativos da página de aplicativos.

**mobilecontentlisting** Lista o conteúdo do zip ContentSync. Isso é usado pelo js do lado do cliente no dispositivo para fazer a cópia inicial do arquivo necessária para aplicativos AEM.

Esse manipulador deve ser adicionado a qualquer configuração AEM Apps ContentSync.

* ***type - String - mobilecontentlisting***
* ***caminho*** - Cadeia de caracteres - mantenha vazio, deve estar presente para ser visto como um manipulador válido, mas o caminho é inferido como o cache ContentSync atual. Esse valor é ignorado.
* ***targetRootDirectory* -**String - o prefixo a ser adicionado aos caminhos como uma raiz de destino para a atualização de conteúdo para este manipulador.
* ***order - Long* -**Ordem para ContentSync executar este manipulador. Esse número deve ser definido como maior do que todos os outros manipuladores, como 100. Ela deve ser executada após os manipuladores de conteúdo tradicionais.

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

* ***tipo - String - mobilecontentpackageslisting***
* ***caminho **-**String*** - Caminho para um shell de aplicativo (nó com pge-type=app-instance).
* ***targetRootDirectory - cadeia de caracteres*** - o prefixo a ser adicionado aos caminhos como uma raiz de destino para a atualização de conteúdo para este manipulador.
* ***order - Long* -**Ordenar que o ContentSync execute este manipulador. Esse número deve ser definido como maior do que todos os outros manipuladores, como 100. Ela deve ser executada após os manipuladores de conteúdo tradicionais.

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

**widgetconfig** Inclui um config.xml atualizado que mescla todas as edições feitas por meio do Centro de comando com um config.xml fornecido. Se esse manipulador não for incluído, os detalhes do aplicativo alterados por meio da interface de Administração não serão incluídos no cache.

Esse manipulador deve ser usado em uma configuração ContentSync do shell do aplicativo AEM (nó com pge-type=[app-instance]).

* ***type - String* - **widgetconfig
* ***caminho **-**String*** - Caminho para qualquer nó filho do shell do aplicativo (nó com pge-type=[app-instance]).
* ***targetRootDirectory - cadeia de caracteres*** - o prefixo a ser adicionado aos caminhos como uma raiz de destino para a atualização de conteúdo para este manipulador.
* ***targetIconDirectory - String*** - o diretório onde colocar os ícones do aplicativo

**mobileADBMobileConfigJSON** Inclua o arquivo ADBMobileConfig.JSON se o serviço de nuvem AMS tiver sido configurado.

Isso é usado no momento da compilação para configurar o plug-in AMS para suporte analítico.

O manipulador deve ser usado na configuração ContentSync do shell do aplicativo AEM (nó com pge-type=app-instance)

* ***type - String*** - mobileADBMobileConfigJSON
* ***path - String*** - Caminho para um shell de aplicativo (nó com pge-type=app-instance ou um RT que estende /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - cadeia de caracteres*** - o prefixo a ser adicionado aos caminhos como uma raiz de destino para a atualização de conteúdo para este manipulador

**notificationsconfig** Extrai configurações de notificações necessárias no dispositivo. As propriedades são extraídas da respectiva configuração do serviço de nuvem do serviço de push associada ao aplicativo.

As propriedades não AEM no nó jcr:content do serviço de nuvem são extraídas e adicionadas à **page-notifications-config.json** Arquivo JSON para inclusão na raiz www do conteúdo do aplicativo.

As propriedades AEM são aquelas com espaçamento de nome &quot;cq&quot;, &quot;sling&quot; ou &quot;jcr&quot;. Outras propriedades podem ser excluídas usando a propriedade &quot;excludeProperties&quot; no nó de configuração de sincronização de conteúdo.

* ***type - String*** - notificationsconfig
* ***excludeProperties - String[]*** - propriedades a serem excluídas

**contentsyncconfigcontent** Coleta conteúdo de uma configuração ContentSync existente.

* ***type - String*** - contentsyncconfigcontent
* ***path - String*** - Caminho para um de:

   * outra configuração ContentSync
   * para um Pacote de conteúdo (usará a propriedade phonegap-exportTemplate para localizar a configuração ContentSync)
   * para um recurso móvel (app-content&#39;s serão encontrados nesse recurso e, se esses pacotes de conteúdo tiverem uma propriedade page-includeInBuild que for verdadeira, o phonegap-exportTemplate será usado para encontrar sua configuração ContentSync)

* ***autoCreateFirstUpdateBeforeImport - Booleano*** - se verdadeiro, cria um atributo inicial **atualizar** na configuração do target antes da importação se ainda não existir uma vez

* ***autoFillBeforeImport - Booleano*** - se verdadeiro, atualiza/preenche a configuração do target antes de importar
* ***configSuffix - Cadeia de caracteres*** - uma sequência de caracteres a ser anexada ao caminho indicado na propriedade &quot;phonegap-exportTemplate&quot; do conteúdo do aplicativo. Isso pode ser usado para distinguir modelos de exportação diferentes. Por exemplo, essa propriedade pode ser definida como **&quot;-dev&quot;** para indicar que *&quot;/../../../appconfig-dev&quot;* deve ser utilizada (em vez de *&quot;/../../../appconfig&quot;*).

**app-assets** Inclui todos os ativos associados a uma instância do aplicativo. Esse manipulador incluirá todos os ativos encontrados no caminho especificado, juntamente com os ativos referenciados pela propriedade appAssetPath de uma instância do aplicativo.

* ***type - String*** - app-assets

* ***caminho **-**String*** - caminho para um local em uma instância do aplicativo onde os ativos do aplicativo são armazenados

**mobileapproffers** Um novo manipulador de sincronização de conteúdo foi introduzido para o caso de uso de Personalização, para renderizar o conteúdo direcionado. O manipulador &quot;mobileapproffers&quot; sabe como renderizar as ofertas de público-alvo associadas que foram criadas pelo autor de conteúdo. O manipulador mobileapproffers estende o manipulador de atualização de páginas abstratas, portanto, muitas das propriedades são semelhantes. Os detalhes do manipulador mobileapproffers têm as seguintes propriedades.

O manipulador mobileappsoffers estende o manipulador mobileappspages e adiciona as seguintes propriedades:

* ***locationRoot - String*** - especifique o local do aplicativo móvel
* ***includePageTypes - Cadeia de caracteres*** - padrões para oferecer suporte a cq/personalization/components/teaserpage e cq/personalization/components/offerproxy
* ***seletor - String*** - deve ser ajustado para tandt
* ***path - String***- o caminho para a marca da campanha

**mobileappconfig** O manipulador de sincronização de conteúdo mobileappconfig fornece uma maneira de inserir dados JSON no MobileAppsConfig.json. Para registrar uma classe de provedor, os desenvolvedores adicionarão sua classe MobileAppsInfoProvider à lista de provedores. O manipulador iterará sobre a lista de MobileAppsInfoProviders e permitirá que o provedor insira dados no arquivo json resultante. As listas de propriedades que este manipulador aceita são:

* ***caminho **-**String*** - o caminho para um nó de instância de aplicativo com pge-type=app-instance ou um RT que estende /libs/mobileapps/core/components/instance
* ***providers - String*** `[]` - a lista de MobileAppsInfoProviders totalmente qualificados
* ***targetRootDirectory - cadeia de caracteres*** - o diretório no qual gravar o arquivo MobileAppsConfig.json.
* **fileName - String** - nome opcional do arquivo no qual gravar o JSON, o padrão é MobileAppsConfig.json

É possível ter vários manipuladores mobileappconfig configurados, cada um com um conjunto exclusivo de provedores gravando em arquivos JSON diferentes.

### Teste de manipuladores de sincronização de conteúdo {#testing-content-sync-handlers}

**Etapas para verificar a integridade** Limpar cache

* Limpar cache
* Executar o manipulador (cache atualizado)
* Execute o manipulador novamente (o cache não deve ser atualizado)

**Etapas para depuração**

* Executar sua configuração
* Exportar sua configuração ou revisão no dispositivo
* Se a renderização falhar, verifique se está ausente *estilos/ativos/bibliotecas* ou verifique se há caminhos inválidos para *estilos/ativos/bibliotecas*

**Logs** Habilitar o log de depuração do ContentSync por meio das configurações do agente OSGI no pacote `com.day.cq.contentsync` Isso permitirá rastrear quais manipuladores foram executados e se eles atualizaram o cache e relataram a atualização do cache.

## Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Criação para Adobe PhoneGap Enterprise com AEM](/help/mobile/phonegap.md)
* [Administração de conteúdo para o Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Para começar a usar o desenvolvimento de aplicativos do AEM Mobile, clique em [aqui](/help/mobile/getting-started-aem-mobile.md).
