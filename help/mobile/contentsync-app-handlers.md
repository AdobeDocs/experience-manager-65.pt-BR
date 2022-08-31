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
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1409'
ht-degree: 0%

---

# Manipuladores de aplicativos prontos para uso{#out-of-the-box-app-handlers}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Consulte as diretrizes a seguir para desenvolver Manipuladores de sincronização de conteúdo:

* Os manipuladores devem implementar *com.day.cq.contentsync.handler.ContentUpdateHandler* (diretamente ou estendendo uma classe que o faça)
* Os manipuladores podem estender *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* O manipulador só deve relatar true se tiver atualizado o cache do ContentSync. O relatório falso de true permitirá AEM criar uma atualização.
* O manipulador só deve atualizar o cache se o conteúdo tiver sido realmente alterado. Não grave no cache se um branco não for necessário e evite uma criação de atualização desnecessária.

## Manipuladores prontos para uso {#out-of-the-box-handlers}

A seguir estão listados os manipuladores de aplicativos prontos para uso:

**mobileapppages** Renderiza páginas do aplicativo.

* ***type - String*** - mobileapppages
* ***path - String*** - caminho para uma página
* ***extensão - String*** - Extensão que deve ser usada na solicitação. Para páginas, isso é quase sempre *html*, mas outros ainda são possíveis.

* ***seletor - String*** - Seletores opcionais separados por ponto. Exemplos comuns são *toque* para renderização de versões móveis de uma página.

* ***deep - Booleano*** - Propriedade booleana opcional que determina se páginas filhas também devem ser incluídas. O valor padrão é *verdadeiro.*

* ***includeImages - Booleano*** - Propriedade booleana opcional que determina se imagens devem ser incluídas. O valor padrão é *true*.

   * Por padrão, somente os componentes de imagem com um tipo de recurso de foundation/components/image são considerados para inclusão.

* ***includeVideos - Booleano*** - A propriedade booleana opcional determina se os vídeos devem ser incluídos. O valor padrão é *true*.

* ***includeModifiedPagesOnly - Booleano*** - Se falso ou omitido, renderize todas as páginas e verifique as atualizações na renderização. Se true, baseie os diffs nas alterações em uma página lastModified.
* ***+ rewrite (node)***
   ***- relativeParentPath - String*** - o caminho para gravar todos os outros caminhos em relação a.

>[!NOTE]
>
>O tipo de recurso dos componentes de imagem e vídeo afetados por esse manipulador é definido pela configuração das propriedades do *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Serviço OSGi MobilePagesUpdateHandler*.

**mobilepageassets** Coleta ativos da página do aplicativo.

**mobilecontentlisting** Lista o conteúdo do zip ContentSync. Isso é usado pelo js do lado do cliente no dispositivo para fazer a cópia de arquivo inicial necessária para AEM aplicativos.

Esse manipulador deve ser adicionado a qualquer Configuração de ContentSync do aplicativo AEM.

* ***type - String - mobilecontentlisting***
* ***caminho*** - String - mantenha empty, deve estar presente para ser visto como um manipulador válido, mas o caminho é inferido como o cache ContentSync atual. Esse valor é ignorado.
* ***targetRootDirectory* -**String - o prefixo a ser adicionado aos caminhos como uma raiz de destino para a atualização de conteúdo para este manipulador.
* ***order - Long* -**Solicite que o ContentSync execute esse manipulador. Esse número deve ser definido como maior do que todos os outros manipuladores, como 100. Ela deve ser executada após manipuladores de conteúdo tradicionais.

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

**mobilecontentpackageslisting** Lista o pacote de conteúdo AEM em um determinado aplicativo, bem como o serverURL para fazer solicitações de atualização. Ele é usado no lado do cliente js no dispositivo para solicitar atualizações de conteúdo

O manipulador deve ser usado AEM App Shell ContentSync Config (nó com page-type=app-instance)

* ***type - String - mobilecontentpackageslisting***
* ***caminho **-**String*** - Caminho para um shell de aplicativo (nó com page-type=app-instance).
* ***targetRootDirectory : cadeia de caracteres*** - o prefixo para adicionar a caminhos como uma raiz de destino para atualização de conteúdo para este manipulador.
* ***order - Long* -**Ordenar que o ContentSync execute esse manipulador. Esse número deve ser definido como maior do que todos os outros manipuladores, como 100. Ela deve ser executada após manipuladores de conteúdo tradicionais.

>[!NOTE]
>
>O bloco de código a seguir não é uma implementação exata e deve ser usado como um exemplo de referência:

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

**widgetconfig** Inclui um config.xml atualizado que mescla todas as edições feitas através do Centro de comando com um config.xml fornecido. Se esse manipulador não estiver incluído, os detalhes do aplicativo alterados pela interface de Administração não serão incluídos no cache.

Esse manipulador deve ser usado em uma configuração AEM App Shell ContentSync (nó com page-type=[app-instance]).

* ***type - String* - **widgetconfig
* ***caminho **-**String*** - Caminho para qualquer nó filho do app shell (nó com page-type=[app-instance]).
* ***targetRootDirectory : cadeia de caracteres*** - o prefixo para adicionar a caminhos como uma raiz de destino para atualização de conteúdo para este manipulador.
* ***targetIconDirectory : String*** - o diretório para colocar os ícones do aplicativo

**mobileADBMobileConfigJSON** Inclua o arquivo ADBMobileConfig.JSON se o serviço de nuvem AMS tiver sido configurado.

Isso é usado em tempo de compilação para configurar o plug-in AMS para suporte analítico.

O manipulador deve ser usado AEM App Shell ContentSync Config (nó com page-type=app-instance)

* ***type - String*** - mobileADBMobileConfigJSON
* ***path - String*** - Caminho para um shell de aplicativo (nó com page-type=app-instance ou um RT que estende /libs/mobileapps/core/components/instance)
* ***targetRootDirectory : cadeia de caracteres*** - o prefixo a ser adicionado aos caminhos como uma raiz de destino para a atualização de conteúdo deste manipulador

**notificationsconfig** Extrai as configurações de notificações necessárias no dispositivo. As propriedades são extraídas da respectiva configuração do serviço de nuvem do serviço de push associada ao aplicativo.

As propriedades não AEM no nó jcr:content do serviço de nuvem são extraídas e adicionadas ao **pge-notifications-config.json** Arquivo JSON para inclusão na raiz www do conteúdo do aplicativo.

AEM propriedades são aquelas que têm espaçamento entre nomes com &quot;cq&quot;, &quot;sling&quot; ou &quot;jcr&quot;. Outras propriedades podem ser excluídas usando a propriedade &quot;excludeProperties&quot; no nó de configuração de sincronização de conteúdo.

* ***type - String*** - notificationsconfig
* ***excludeProperties - String[]*** - propriedades a excluir

**contentsyncconfigcontent** Coleta conteúdo de uma configuração ContentSync existente.

* ***type - String*** - contentsyncconfigcontent
* ***path - String*** - Caminho para um dos seguintes:

   * outra configuração do ContentSync
   * para um Pacote de conteúdo (usará sua propriedade phonegap-exportTemplate para localizar sua configuração ContentSync )
   * para um recurso móvel (o app-content&#39;s será encontrado sob esse recurso e, se esses pacotes de conteúdo tiverem uma propriedade page-includeInBuild que é verdadeira, phonegap-exportTemplate será usado para encontrar sua configuração ContentSync)

* ***autoCreateFirstUpdateBeforeImport - Boolean*** - se verdadeiro, crie um **atualizar** na configuração do target antes da importação, se já não existir uma vez

* ***autoFillBeforeImport - Boolean*** - se verdadeiro, atualize/preencha a configuração de destino antes de importar
* ***configSuffix - String*** - uma string a ser anexada ao caminho indicado na propriedade &quot;phonegap-exportTemplate&quot; do conteúdo do aplicativo. Isso pode ser usado para distinguir diferentes modelos de exportação. Por exemplo, essa propriedade pode ser definida como **&quot;-dev&quot;** para indicar que *&quot;/../../../appconfig-dev&quot;* deve ser usada (em vez de *&quot;/../../../appconfig&quot;*).

**app-assets** Inclui todos os ativos associados a uma instância de aplicativo. Esse manipulador incluirá todos os ativos encontrados no caminho especificado, juntamente com quaisquer ativos referenciados pela propriedade appAssetPath de uma instância do aplicativo.

* ***type - String*** - app-assets

* ***caminho **-**String*** - caminho para um local em uma instância do aplicativo em que os ativos do aplicativo são armazenados

**mobileappoffers** Um novo manipulador de sincronização de conteúdo foi introduzido no caso de uso de Personalização para renderizar o conteúdo direcionado. O manipulador &quot;mobileappoffers&quot; sabe como renderizar as ofertas de destino associadas que foram criadas pelo autor de conteúdo. O manipulador mobileappoffers estende o manipulador de atualização de páginas abstrato, portanto, muitas das propriedades são semelhantes. Os detalhes do manipulador mobileappoffers têm as seguintes propriedades.

O manipulador mobileappsoffers expande o manipulador de mobileappspages e adiciona as seguintes propriedades:

* ***locationRoot - String*** - especificar a localização do aplicativo móvel
* ***includePageTypes - String*** - padrões de suporte para cq/personalization/components/teaserpage e cq/personalization/components/offerproxy
* ***seletor - String*** - deve ser definido como tandt
* ***path - String***- o caminho para a marca da campanha

**mobileappconfig** O manipulador de sincronização de conteúdo mobileappconfig fornece uma maneira de inserir dados JSON no MobileAppsConfig.json. Para registrar um desenvolvedor de classe de provedor, adicione sua classe MobileAppsInfoProvider à lista de provedores. O manipulador fará uma iteração sobre a lista de MobileAppsInfoProviders e permitirá que o provedor injete dados no arquivo json resultante. A lista de propriedades suportadas por esse manipulador é:

* ***caminho **-**String*** - o caminho para um nó de instância de aplicativo com page-type=app-instance ou um RT que estende /libs/mobileapps/core/components/instance
* ***provider - String*** `[]` - a lista de MobileAppsInfoProviders totalmente qualificados
* ***targetRootDirectory : cadeia de caracteres*** - o diretório onde gravar o arquivo MobileAppsConfig.json.
* **fileName - String** - nome opcional do arquivo para gravar o JSON, padrão para MobileAppsConfig.json

É possível ter vários manipuladores mobileappconfig configurados cada um com um conjunto exclusivo de provedores gravando em arquivos JSON diferentes.

### Teste dos manipuladores de sincronização de conteúdo {#testing-content-sync-handlers}

**Etapas para verificar a integridade** Limpar cache

* Limpar cache
* Execute seu manipulador (cache atualizado)
* Execute seu manipulador novamente (o cache não deve ser atualizado)

**Etapas para depuração**

* Executar sua configuração
* Exportar sua configuração ou revisão no dispositivo
* Se a renderização falhar, verifique se está faltando *estilos/ativos/libs* ou verifique se há caminhos ruins para *estilos/ativos/libs*

**Registro** Ativar o registro do ContentSync Debug por meio das configurações do logger OSGI no pacote `com.day.cq.contentsync` Isso permitirá rastrear quais manipuladores foram executados e se eles atualizaram o cache e relataram a atualização do cache.

## Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Criação para Adobe PhoneGap Enterprise com AEM](/help/mobile/phonegap.md)
* [Administração de conteúdo para Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Para começar a usar o desenvolvimento de aplicativos AEM Mobile, clique em [here](/help/mobile/getting-started-aem-mobile.md).
