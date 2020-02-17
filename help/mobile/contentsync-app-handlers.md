---
title: Manipuladores de aplicativos prontos para uso
seo-title: Manipuladores de aplicativos prontos para uso
description: Siga esta página para saber mais sobre os manipuladores prontos para uso do Adobe PhoneGap Enterprise com AEM.
seo-description: Siga esta página para saber mais sobre os manipuladores prontos para uso do Adobe PhoneGap Enterprise com AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Manipuladores de aplicativos prontos para uso{#out-of-the-box-app-handlers}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

Consulte as diretrizes a seguir para desenvolver Content Sync Handlers:

* Os manipuladores devem implementar *com.day.cq.contentsync.handler.ContentUpdateHandler* (diretamente ou estendendo uma classe que o faça)
* Os manipuladores podem estender *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* O manipulador só deve relatar true se tiver atualizado o cache do ContentSync. O relatório falso de true permitirá que o AEM crie uma atualização.
* O manipulador só deve atualizar o cache se o conteúdo realmente tiver sido alterado. Não grave no cache se um branco não for necessário e evite uma criação desnecessária de atualização.

## Manipuladores fora da caixa {#out-of-the-box-handlers}

A seguir estão listados os manipuladores de aplicativos prontos para uso:

**mobileapppages** Renderiza páginas de aplicativo.

* ***type - String*** - mobileapppages
* ***path - String*** - caminho para uma página
* ***extension - String*** - Extensão que deve ser usada na solicitação. Para páginas, isso é quase sempre *html*, mas outras ainda são possíveis.

* ***seletor - String*** - Seletores opcionais separados por ponto. Exemplos comuns são o *toque* para renderizar versões móveis de uma página.

* ***deep - Booliano*** - propriedade booleana opcional que determina se páginas secundárias também devem ser incluídas. The default value is *true.*

* ***includeImages - Boolean*** - propriedade booleana opcional que determina se as imagens devem ser incluídas. The default value is *true*.

   * Por padrão, somente os componentes de imagem com um tipo de recurso de fundação/componentes/imagem são considerados para inclusão.

* ***includeVideos - Booliano*** - A propriedade booleana opcional determina se os vídeos devem ser incluídos. The default value is *true*.

* ***includeModifiedPagesOnly - Boolean*** - Se falso ou omitido renderiza todas as páginas e verifica as atualizações na renderização. Se verdadeiro, a base se diferencia nas alterações em uma página lastModified.
* ***+ rewrite (nó)***
   ***- relativeParentPath - String*** - o caminho para gravar todos os outros caminhos relativos a.

>[!NOTE]
>
>O tipo de recurso dos componentes de imagem e vídeo afetados por esse manipulador é definido pela configuração das propriedades do *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Serviço* MobilePagesUpdateHandler OSGi.

**mobilepageassets** coleta ativos da página do aplicativo.

**mobilecontentlist** Lista o conteúdo do zip ContentSync. Isso é usado pelo lado do cliente js no dispositivo para fazer a cópia de arquivo inicial necessária para aplicativos AEM.

Esse manipulador deve ser adicionado a qualquer configuração ContentSync dos aplicativos AEM.

* ***type - String - mobilecontentlisted***
* ***path*** - String - manter vazio, deve estar presente para ser visto como um manipulador válido, mas o caminho é inferido como o cache ContentSync atual. Esse valor é ignorado.
* ***targetRootDirectory *-**String - o prefixo a ser adicionado aos caminhos como uma raiz de destino para a atualização de conteúdo deste manipulador.
* ***pedido - Longo *-**pedido para que o ContentSync execute este manipulador. Esse número deve ser definido como maior que todos os outros manipuladores, como 100. Ela deve ser executada após manipuladores de conteúdo tradicionais.

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

**mobilecontentpackageslist** Lista o pacote de conteúdo AEM em um determinado aplicativo, bem como o serverURL para o qual fazer solicitações de atualização. Isso é usado nas js do lado do cliente no dispositivo para solicitar atualizações de conteúdo

O manipulador deve ser usado na configuração ContentSync do AEM App Shell (nó com pge-type=app-instance)

* ***type - String - mobilecontentpackageslist***
* ***path **-**String*** - Caminho para um shell de aplicativo (nó com pge-type=app-instance).
* ***targetRootDirectory - String*** - o prefixo a ser adicionado aos caminhos como uma raiz de destino para a atualização de conteúdo deste manipulador.
* ***order - Long *- Order for ContentSync (Longo **pedido para que o ContentSync execute este manipulador). Esse número deve ser definido como maior que todos os outros manipuladores, como 100. Ela deve ser executada após manipuladores de conteúdo tradicionais.

>[!NOTE]
>
>O seguinte bloco de código não é uma implementação exata e deve ser usado como exemplo de referência:

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

**widgetconfig** Inclui um config.xml atualizado que mescla todas as edições feitas através do Centro de comando com um config.xml fornecido. Se esse manipulador não estiver incluído, nenhum detalhe de aplicativo que seja alterado pela interface de Administração não será incluído no cache.

Esse manipulador deve ser usado em uma configuração ContentSync da AEM App Shell (nó com pge-type=[app-instance]).

* ***type - String* - **widgetconfig
* ***path **-**String*** - Caminho para qualquer nó filho do shell do aplicativo (nó com pge-type=[app-instance]).
* ***targetRootDirectory - String*** - o prefixo a ser adicionado aos caminhos como uma raiz de destino para a atualização de conteúdo deste manipulador.
* ***targetIconDirectory - String*** - o diretório para colocar os ícones do aplicativo

**mobileADBMobileConfigJSON** Inclua o arquivo ADBMobileConfig.JSON se o serviço de nuvem AMS tiver sido configurado.

Isso é usado em tempo de compilação para configurar o plug-in AMS para suporte analítico.

O manipulador deve ser usado na configuração ContentSync do AEM App Shell (nó com pge-type=app-instance)

* ***type - String*** - mobileADBMobileConfigJSON
* ***path - String*** - Caminho para um shell de aplicativo (nó com pge-type=app-instance ou um RT que estende /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - String*** - o prefixo a ser adicionado aos caminhos como uma raiz de destino para a atualização de conteúdo deste manipulador

**notificationsconfig** Extrai configurações de notificações necessárias no dispositivo. As propriedades são extraídas da respectiva configuração do serviço de nuvem do serviço de push associado ao aplicativo.

As propriedades que não são AEM no nó jcr:content do serviço de nuvem são extraídas e adicionadas ao arquivo JSON do serviço de **página-notifications-config.json** para inclusão na raiz www do conteúdo do aplicativo.

As propriedades do AEM são aquelas que têm o nome espaçado com &quot;cq&quot;, &quot;sling&quot; ou &quot;jcr&quot;. Outras propriedades podem ser excluídas usando a propriedade &quot;excludeProperties&quot; no nó de configuração de sincronização de conteúdo.

* ***type - String*** - notifications - config
* ***excludeProperties - String[]*** - propriedades a serem excluídas

**contentsyncconfigcontent** coleta conteúdo de uma configuração ContentSync existente.

* ***type - String*** - contentsyncconfigcontent
* ***path - String*** - Caminho para um de:

   * outra configuração do ContentSync
   * para um Pacote de conteúdo (usará sua propriedade phonegap-exportTemplate para localizar sua configuração ContentSync)
   * para um recurso móvel (o app-content&#39;s será encontrado nesse recurso e, se esses pacotes de conteúdo tiverem uma propriedade pge-includeInBuild que for verdadeira, o phonegap-exportTemplate será usado para encontrar sua configuração ContentSync)

* ***autoCreateFirstUpdateBeforeImport - Boolean*** - se verdadeiro, crie uma **atualização** inicial na configuração de destino antes de importar se já não existir uma vez

* ***autoFillBeforeImport - Boolean*** - se verdadeiro, atualize/preencha a configuração de destino antes de importar
* ***configSuffix - String*** - uma string a ser anexada ao caminho indicado na propriedade &quot;phonegap-exportTemplate&quot; de app-content. Isso pode ser usado para distinguir diferentes modelos de exportação. Por exemplo, essa propriedade pode ser definida como **&quot;-dev&quot;** para indicar que *&quot;/.../.../appconfig-dev&quot;* deve ser usado (em oposição a *&quot;/.../.../appconfig&quot;*).

**app-assets** Inclui todos os ativos associados a uma instância do aplicativo. Esse manipulador incluirá todos os ativos encontrados no caminho especificado junto com quaisquer ativos referenciados pela propriedade appAssetPath de uma instância do aplicativo.

* ***type - String*** - app-assets

* ***path **-**String*** - caminho para um local em uma instância do aplicativo onde os ativos do aplicativo são armazenados

**mobileappoffers** Um novo manipulador de sincronização de conteúdo foi introduzido para o caso de uso Personalização para renderizar o conteúdo direcionado. O manipulador &#39;mobileappoffers&#39; sabe como renderizar as ofertas de destino associadas que foram criadas pelo autor do conteúdo. O manipulador mobileappoffers estende o manipulador de atualização de páginas abstratas, portanto, muitas das propriedades são semelhantes. Os detalhes do manipulador mobileappoffers têm as seguintes propriedades.

O manipulador mobileappsoffers estende o manipulador mobileappspages e adiciona as seguintes propriedades:

* ***locationRoot - String*** - especifique o local do aplicativo móvel
* ***includePageTypes - String*** - padrões para suporte a cq/personalization/components/teaserpage e cq/personalization/components/offerproxy
* ***seletor - String*** - deve ser definido como tandor
* ***path - String***- o caminho para a marca da campanha

**mobileappconfig** O manipulador de sincronização de conteúdo mobileappconfig fornece uma maneira de inserir dados JSON no MobileAppsConfig.json. Para registrar uma classe de provedor, os desenvolvedores adicionarão sua classe MobileAppsInfoProvider à lista de provedores. O manipulador repetirá a lista de MobileAppsInfoProviders e permitirá que o provedor injete dados no arquivo json resultante. A lista de propriedades suportadas por este manipulador é:

* ***path **-**String*** - o caminho para um nó de instância de aplicativo com pge-type=app-instance ou um RT que estende /libs/mobileapps/core/components/instance
* ***provedores - String*** `[]` - a lista de MobileAppsInfoProviders totalmente qualificados
* ***targetRootDirectory - String*** - o diretório no qual gravar o arquivo MobileAppsConfig.json.
* **fileName - String** - nome opcional do arquivo para gravar o JSON, o padrão é MobileAppsConfig.json

É possível ter vários manipuladores mobileappconfig configurados cada um com um conjunto exclusivo de provedores gravando em arquivos JSON diferentes.

### Testando manipuladores de sincronização de conteúdo {#testing-content-sync-handlers}

**Etapas para verificar a integridade** do cache limpo

* Limpar cache
* Executar seu manipulador (cache atualizado)
* Execute seu manipulador novamente (o cache não deve ser atualizado)

**Etapas para depuração**

* Executar sua configuração
* Exportar sua configuração ou revisão no dispositivo
* Se a renderização falhar, verifique se há *estilos/ativos/libs* ausentes ou se há caminhos ruins para *estilos/ativos/libs*

**Registrando** Ativar log de Depuração de ConteúdoSync por meio das configurações de log do OSGI no pacote `com.day.cq.contentsync` Isso permitirá rastrear quais manipuladores executaram e se eles atualizaram o cache e relataram a atualização do cache.

## Additional Resources {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Criação para Adobe PhoneGap Enterprise com AEM](/help/mobile/phonegap.md)
* [Administração de conteúdo para Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Para começar a desenvolver aplicativos do AEM Mobile, clique [aqui](/help/mobile/getting-started-aem-mobile.md).

