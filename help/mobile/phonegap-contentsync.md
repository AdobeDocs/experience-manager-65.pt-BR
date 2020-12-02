---
title: Mobile com sincronização de conteúdo
seo-title: Mobile com sincronização de conteúdo
description: Siga esta página para saber mais sobre a Sincronização de conteúdo para Adobe PhoneGap Enterprise com AEM.
seo-description: Siga esta página para saber mais sobre a Sincronização de conteúdo para Adobe PhoneGap Enterprise com AEM.
uuid: c3a82171-e070-4e32-b1ef-26e65ae23d99
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 923fc031-1a06-4a9d-94da-a2a4e82c54ee
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '2989'
ht-degree: 0%

---


# Dispositivo móvel com sincronização de conteúdo{#mobile-with-content-sync}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Este documento faz parte do [Guia de introdução ao AEM Mobile](/help/mobile/getting-started-aem-mobile.md), um ponto de partida recomendado para referência ao AEM Mobile.

Use a Sincronização de conteúdo para disponibilizar conteúdo para que possa ser usado em aplicativos móveis nativos. As páginas criadas no AEM podem ser usadas como conteúdo do aplicativo, mesmo quando o dispositivo está offline. Além disso, como as páginas AEM são baseadas em padrões da Web, elas funcionam em várias plataformas, permitindo que você as incorpore em qualquer invólucro nativo. Essa estratégia reduz o esforço de desenvolvimento e permite que você atualize facilmente o conteúdo do aplicativo.

>[!NOTE]
>
>Os aplicativos PhoneGap que você cria usando AEM ferramentas já estão configurados para usar AEM páginas como conteúdo por meio da Sincronização de conteúdo.

A estrutura de Sincronização de conteúdo cria um arquivo de arquivamento que contém o conteúdo da Web. O conteúdo pode ser qualquer coisa de páginas simples, imagens e arquivos PDF, ou Aplicações web inteiras. A Content Sync API fornece acesso ao arquivo de arquivamento de aplicativos móveis ou processos de criação para que o conteúdo possa ser recuperado e incluído no aplicativo.

A seguinte sequência de etapas ilustra um caso de uso típico para a Sincronização de conteúdo:

1. O desenvolvedor AEM cria uma configuração de Sincronização de conteúdo que especifica o conteúdo a ser incluído.
1. A estrutura de Sincronização de conteúdo coleta e armazena em cache o conteúdo.
1. Em um dispositivo móvel, o aplicativo móvel é iniciado e solicita o conteúdo do servidor, que é fornecido em um arquivo ZIP.
1. O cliente descompacta o conteúdo ZIP no sistema de arquivos local. A estrutura de pastas no arquivo ZIP simula os caminhos que um cliente (por exemplo, um navegador) normalmente solicitaria do servidor.
1. O cliente abre o conteúdo em um navegador incorporado ou o usa de alguma outra forma.
1. Posteriormente, o cliente solicita conteúdo atualizado do servidor. A estrutura de sincronização de conteúdo fornece atualizações incrementais para reduzir o tamanho e o tempo de download, o que pode ser importante para dispositivos móveis devido à largura de banda limitada ou aos volumes de dados.

>[!NOTE]
>
>Para obter mais informações sobre as diretrizes para desenvolver manipuladores de Sincronização de conteúdo, consulte [Desenvolvendo manipuladores de sincronização de conteúdo](/help/mobile/contentsync-app-handlers.md).

## Configuração do conteúdo de sincronização {#configuring-the-content-sync-content}

Crie uma configuração de Sincronização de conteúdo para especificar o conteúdo do arquivo ZIP que é entregue ao cliente. É possível criar qualquer número de configurações de Sincronização de conteúdo. Cada configuração tem um nome para fins de identificação.

Para criar uma configuração de Sincronização de conteúdo, adicione um nó `cq:ContentSyncConfig` ao repositório, com a propriedade `sling:resourceType` definida como `contentsync/config`. O nó `cq:ContentSyncConfig` pode estar localizado em qualquer lugar no repositório, no entanto, o nó deve estar acessível aos usuários na instância de publicação AEM. Portanto, você deve adicionar o nó abaixo de `/content`.

Para especificar o conteúdo do arquivo ZIP de sincronização de conteúdo, adicione nós filhos ao nó cq:ContentSyncConfig. As seguintes propriedades de cada nó filho identificam um item de conteúdo a ser incluído e como ele é processado ao adicioná-lo:

* `path`: O local do conteúdo.
* `type`: O nome do tipo de configuração a ser usado para processar o conteúdo. Vários tipos estão disponíveis e são descritos em Tipos de configuração.

Consulte Exemplo de configuração de sincronização de conteúdo.

Depois de criar a configuração de Sincronização de conteúdo, ela será exibida no console Sincronização de conteúdo.

>[!NOTE]
>
>A estrutura de Sincronização de conteúdo não verifica se as dependências de ativos e arquivos relacionados ao design estão incluídos nos pacotes de Sincronização de conteúdo. Certifique-se de incluir todos os arquivos necessários no arquivo ZIP.

### Configurando o acesso a downloads de sincronização de conteúdo {#configuring-access-to-content-sync-downloads}

Especifique um usuário ou grupo que possa baixar a partir da Sincronização de conteúdo. Você pode configurar o usuário ou grupo padrão que pode baixar de todos os caches de Sincronização de conteúdo e pode substituir o padrão e configurar o acesso para uma configuração específica de Sincronização de conteúdo.

Quando o AEM é instalado, os membros do grupo de administradores podem fazer download do Content Sync por padrão.

### Configuração do acesso padrão para downloads de sincronização de conteúdo {#setting-the-default-access-for-content-sync-downloads}

O serviço Day CQ Content Sync Manager controla o acesso à Sincronização de conteúdo. Configure esse serviço para especificar o usuário ou grupo que pode ser baixado do Content Sync por padrão.

Se você estiver [configurando o serviço usando o Console da Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), digite o nome do usuário ou grupo como o valor da propriedade Autorizável do Cache de Fallback.

Se você estiver [configurando no repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository), use as seguintes informações sobre o serviço:

* PID: com.day.cq.contentsync.impl.ContentSyncManagerImpl
* Nome da propriedade: contentsync.fallback.autorizable

#### Substituição do acesso de download para um cache de sincronização de conteúdo {#overriding-download-access-for-a-content-sync-cache}

Para configurar o acesso de download para uma configuração específica de Sincronização de conteúdo, adicione a seguinte propriedade ao nó `cq:ContentSyncConfig`:

* Nome: autorizável
* Tipo: String
* Valor: O nome do usuário ou grupo que pode baixar.

Por exemplo, seu aplicativo permite que os usuários instalem atualizações diretamente da Sincronização de conteúdo. Para permitir que todos os usuários baixem a atualização, defina o valor da propriedade autorizável como `everyone`.

Se o nó `cq:ContentSyncConfig` não tiver uma propriedade autorizável, o usuário ou grupo padrão configurado para a propriedade Autorizável de Cache de Fallback do serviço Day CQ Content Sync Manager determinará quem pode fazer download.

### Configuração do usuário para atualização de um cache de sincronização de conteúdo {#configuring-the-user-for-updating-a-content-sync-cache}

Quando um usuário faz uma atualização do cache de Sincronização de conteúdo, uma conta de usuário específica executa a ação em nome do usuário. O usuário anônimo atualiza todos os caches de Sincronização de conteúdo por padrão.

Você pode substituir o usuário padrão e especificar um usuário ou grupo que atualize um cache de Sincronização de conteúdo específico.

Para substituir o usuário padrão, especifique um usuário ou grupo que execute atualizações para uma configuração específica de Sincronização de conteúdo adicionando a seguinte propriedade ao nó cq:ContentSyncConfig:

* Nome: updateuser
* Tipo: String
* Valor: O nome do usuário ou grupo que pode executar as atualizações.

Se o nó cq:ContentSyncConfig não tiver uma propriedade updateuser, o usuário anônimo padrão atualizará o cache.

### Tipos de configuração {#configuration-types}

O processamento pode variar desde a renderização de JSON simples até a renderização completa de páginas, incluindo seus ativos referenciados. Esta seção lista os tipos de configuração disponíveis e seus parâmetros específicos:

**** copiarBasta copiar arquivos e pastas.

* **path**  - Se o caminho apontar para um único arquivo, somente o arquivo será copiado. Se apontar para uma pasta (isso inclui nós de página), todos os arquivos e pastas abaixo serão copiados.

**conteúdoRenderize conteúdo usando o processamento de solicitação Sling padrão.** 

* **path**  - caminho para o recurso que deve ser enviado.
* **extension**  - Extensão que deve ser usada na solicitação. Exemplos comuns são *html* e *json*, mas qualquer outra extensão é possível.

* **seletor**  - Seletores opcionais separados por ponto. Exemplos comuns são *touch* para renderizar versões móveis de uma página ou *infinity* para saída JSON.

**clientlib** Empacote uma biblioteca de clientes Javascript ou CSS.

* **path**  - Caminho para a raiz da biblioteca do cliente.
* **extension**  - Tipo de biblioteca do cliente. Isso deve ser definido como *js* ou *css* no momento.

* **includeFolders** - Type é uma matriz de strings e permite que o usuário especifique pastas adicionais para digitalizar na biblioteca do cliente para buscar arquivos (como fontes personalizadas).

**ativos**

Coletar representações originais de ativos.

* **path**  - Caminho para uma pasta de ativos abaixo de /content/dam.
* **execuções**  - Tipo é uma matriz de sequências de caracteres que permite ao usuário especificar quais execuções usar em vez da imagem padrão. A lista a seguir resume algumas execuções prontas, mas você também pode usar qualquer representação criada pelo fluxo de trabalho:

   * *original*
   * *cq5dam.thumbnail.48.48.png*
   * *cq5dam.thumbnail.319.319.png*
   * *cq5dam.thumbnail.140.100.png*
   * *cq5dam.web.1280.1280.png*

**** imageColeta uma imagem.

* **path**  - Caminho para um recurso de imagem.

O tipo de imagem é usado para incluir o logotipo We.Retail no arquivo zip.

**** páginasRenderize AEM páginas e colete ativos referenciados.

* **path**  - Caminho para uma página.
* **extension**  - Extensão que deve ser usada na solicitação. Para páginas, isso é quase sempre *html*, mas outras ainda são possíveis.

* **seletor**  - Seletores opcionais separados por ponto. Exemplos comuns são *touch* para renderizar versões móveis de uma página.

* **deep**  - propriedade booleana opcional que determina se páginas secundárias também devem ser incluídas. O valor padrão é *true.*

* **includeImages**  - propriedade booleana opcional que determina se as imagens devem ser incluídas. O valor padrão é *true*.
Por padrão, somente os componentes de imagem com um tipo de recurso de fundação/componentes/imagem são considerados para inclusão. Você pode adicionar mais tipos de recursos configurando o **Day CQ WCM Pages Update Handler** no console da Web.

**** rewriteO nó rewrite define como os links são regravados na página exportada. Os links regravados podem apontar para os arquivos incluídos no arquivo zip ou para os recursos no servidor.

O nó `rewrite` precisa estar localizado abaixo do nó `page`.

O nó `rewrite` pode ter uma ou mais das seguintes propriedades:

* `clientlibs`: regrava caminhos clientlibs.

* `images`: regrava caminhos de imagens.
* `links`: regrava caminhos de links.

Cada propriedade pode ter um dos seguintes valores:

* `REWRITE_RELATIVE`: regrava o caminho com uma posição relativa ao arquivo .html da página no sistema de arquivos.

* `REWRITE_EXTERNAL`: regrava o caminho apontando para o recurso no servidor, usando o serviço [ AEM ](/help/sites-developing/externalizer.md)Externalizer.

O serviço AEM chamado **PathRewriterTransformerFactory** permite configurar os atributos html específicos que serão regravados. O serviço pode ser configurado no console da Web e tem uma configuração para cada propriedade do nó `rewrite`: `clientlibs`, `images` e `links`.

Este recurso foi adicionado no AEM 5.5.

### Exemplo de configuração de sincronização de conteúdo {#example-content-sync-configuration}

A lista abaixo mostra um exemplo de configuração para a Sincronização de conteúdo.

```java
+ weretail_go [cq:ContentSyncConfig]
  - sling:resourceType = "contentsync/config"

  + etc.designs.default [nt:unstructured]
    - path = "/etc/designs/default"
    - type = "copy"

  + etc.designs.mobile [nt:unstructured]
    - path = "/etc/designs/mobile"
    - type = "copy"

  + events.plist [nt:unstructured]
    - path = "/content/weretail_mobile/en/events/jcr:content/par/events"
    - type = "content"
    - extension = "plist"

  + events.touch.html [nt:unstructured]
    - path = "/content/weretail_mobile/en/events"
    - type = "pages"
    - extension = "html"
    - selector = "touch"

  + logo [nt:unstructured]
    - path = "/etc/designs/mobile/jcr:content/mobilecontentpage/logo"
    - type = "logo"

  + manifest [nt:unstructured]
    - indexPage = "/content/weretail_mobile/en/events.touch.html"
    - metadataPlist = "/content/weretail_mobile/en/events/_jcr_content/par/events.plist"

  + ...
```

**etc.designs.default e etc.designs.** mobileAs duas primeiras entradas da configuração devem ser bastante óbvias. Como vamos incluir várias páginas móveis, precisamos dos arquivos de design relacionados abaixo de /etc/designs. E como não há necessidade de processamento extra, basta copiar.

**eventos.** plistEsta entrada é um pouco especial. Conforme mencionado na introdução, o aplicativo deve fornecer uma visualização de mapa com marcadores dos locais dos eventos. Forneceremos as informações de localização necessárias como um arquivo separado no formato PLIST. Para que isso funcione, o componente de lista do evento usado na página de índice tem um script chamado plist.jsp. Esse script é executado quando o recurso do componente é solicitado com a extensão .plist. Como de costume, o caminho dos componentes é fornecido na propriedade path e o tipo é definido como conteúdo, pois queremos aproveitar o processamento de solicitação Sling.

**evento.touch.** htmlEm seguida, são mostradas as páginas reais que serão exibidas no aplicativo. A propriedade path é definida para a página raiz dos eventos. Todas as páginas de eventos abaixo dessa página também serão incluídas, pois o padrão da propriedade profunda é true. Usamos páginas como tipo de configuração, para que quaisquer imagens ou outros arquivos que possam ser referenciados a partir de uma imagem ou de um componente de download em uma página sejam incluídos. Além disso, definir o seletor de toque nos fornece uma versão móvel das páginas. A configuração no pacote de recursos contém mais entradas desse tipo, mas são deixadas de fora para simplificar aqui.

**** LogotipoO tipo de configuração do logotipo ainda não foi mencionado e não é nenhum dos tipos incorporados. No entanto, a estrutura de Sincronização de conteúdo é extensível até certo ponto e esse é um exemplo disso, que será abordado na próxima seção.

**** manifestGeralmente é desejável ter algum tipo de metadados incluídos no arquivo zip, como a página de start do seu conteúdo, por exemplo. No entanto, a codificação dessas informações impede que você as altere facilmente mais tarde. A estrutura de Sincronização de conteúdo oferece suporte a esse caso de uso, procurando um nó manifest na configuração, que é simplesmente identificado pelo nome e não requer um tipo de configuração. Cada propriedade definida nesse nó específico é adicionada a um arquivo, que também é chamado manifest e reside na raiz do arquivo zip.

No exemplo, a página de listagem do evento deve ser a página inicial. Essas informações são fornecidas na propriedade **indexPage** e podem ser facilmente alteradas a qualquer momento. Uma segunda propriedade define o caminho do arquivo *eventos.plist*. Como veremos mais tarde, o aplicativo cliente agora pode ler o manifesto e agir de acordo com ele.

Assim que a configuração for configurada, o conteúdo poderá ser baixado com um navegador ou qualquer outro cliente HTTP, ou se você estiver desenvolvendo para iOS, poderá usar a biblioteca de clientes dedicada WAppKitSync. O local de download é composto pelo caminho da configuração e pela extensão *.zip*, por exemplo, ao trabalhar com uma instância AEM local: *https://localhost:4502/content/weretail_go.zip*

### O console de sincronização de conteúdo {#the-content-sync-console}

O console Sincronização de conteúdo lista todas as configurações de Sincronização de conteúdo no repositório (todos os nós do tipo `cq:ContentSyncConfig`) e, para cada configuração, permite fazer o seguinte:

* Atualize o cache.
* Limpe o cache.
* Baixe um zip completo.
* Baixe um zip diff entre agora e uma data e hora específicas.

Pode ser útil para desenvolvimento e solução de problemas.

O console pode ser acessado em:

`https://localhost:4502/libs/cq/contentsync/content/console.html`

A sua aparência é a seguinte:

![chlimage_1](assets/chlimage_1.png)

### Extensão da estrutura de sincronização de conteúdo {#extending-the-content-sync-framework}

Embora o número de opções de configuração já seja bastante grande, ele pode não abranger todos os requisitos do caso de uso específico. Esta seção descreve os pontos de extensão da estrutura de sincronização de conteúdo e como criar tipos de configuração personalizados.

Para cada tipo de configuração, há um *Content Update Handler*, que é uma fábrica de componentes OSGi registrada para esse tipo específico. Esses manipuladores coletam conteúdo, processam e adicionam a um cache mantido pela estrutura de sincronização de conteúdo. Implemente a seguinte interface ou classe básica abstrata:

* `com.day.cq.contentsync.handler.ContentUpdateHandler` - Interface que todos os manipuladores de atualização precisam implementar
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - Uma classe abstrata que simplifica a renderização de recursos usando Sling

Registre sua classe como fábrica de componentes OSGi e implante-a no container OSGi em um pacote. Isso pode ser feito usando o plug-in [Maven SCR](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html) usando tags ou anotações do JavaDoc. O exemplo a seguir mostra a versão do JavaDoc:

```java
/*
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/customtype"
 */
public class CustomTypeUpdateHandler implements ContentUpdateHandler {
    // add your code here
}

/*
 * @scr.component metatype="no" inherit="true"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/othertype"
 */
public class OtherTypeUpdateHandler extends AbstractSlingResourceUpdateHandler {
    // add your code here
}
```

Observe que a definição *fatory* contém a interface comum e o tipo personalizado separado por barra. Essa estratégia permite que a estrutura de Sincronização de conteúdo localize e crie uma instância da sua classe personalizada, pois reconhece o tipo personalizado em uma entrada de configuração. A próxima seção fornece um exemplo concreto de um manipulador de atualização personalizado.

>[!CAUTION]
>
>Ao criar a classe base AbstractSlingResourceUpdateHandler, você deve adicionar a definição *herdar*. Caso contrário, o container OSGi não definirá as referências necessárias declaradas na classe base.

### Implementando um Manipulador de Atualização Personalizado {#implementing-a-custom-update-handler}

Cada página do We.Retail Mobile contém um logotipo no canto superior esquerdo que gostaríamos de incluir no arquivo zip, é claro. No entanto, para otimização de cache, AEM não faz referência ao local real do arquivo de imagem no repositório, o que nos impede de usar o tipo de configuração **copy**. Em vez disso, precisamos fornecer nosso próprio tipo de configuração **logo** que disponibilize a imagem no local solicitado pelo AEM. A listagem de código a seguir mostra a implementação completa do manipulador de atualizações de logotipo:

#### LogoUpdateHandler.java {#logoupdatehandler-java}

```java
package com.day.cq.wcm.apps.weretail.impl;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.day.cq.commons.jcr.JcrUtil;
import com.day.cq.contentsync.config.ConfigEntry;
import com.day.cq.contentsync.handler.ContentUpdateHandler;
import com.day.cq.wcm.foundation.Image;
import com.day.text.Text;

/**
 * The <code>LogoUpdateHandler</code> is used to update the content sync cache
 * with a page logo added using a logo component.
 *
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/logo"
 */
public class LogoUpdateHandler implements ContentUpdateHandler {

    private static final Logger log = LoggerFactory.getLogger(LogoUpdateHandler.class);

    /** @scr.reference policy="static" */
    protected JcrResourceResolverFactory resolverFactory;

    public boolean updateCacheEntry(ConfigEntry configEntry, Long lastUpdated, String configCacheRoot, Session admin, Session session) {
        ResourceResolver resolver = resolverFactory.getResourceResolver(admin);
        Resource resource = resolver.getResource(configEntry.getContentPath());

        Image img = new Image(resource);
        img.setItemName(Image.NN_FILE, "image");
        img.setItemName(Image.PN_REFERENCE, "imageReference");
        img.setSelector("img");

        try {
            if(img.getLastModified() == null || lastUpdated < img.getLastModified().getTime().getTime()) {
                String src = img.getSrc();
                String parentPath = configCacheRoot + Text.getRelativeParent(src, 1);

                Node parent = JcrUtil.createPath(parentPath, "sling:Folder", admin);
                Node image = resolver.getResource(resource.getPath() + "/image").adaptTo(Node.class);
                JcrUtil.copy(image, parent, Text.getName(src));

                admin.save();

                return true;
            }
        } catch (RepositoryException e) {
            log.error("Unexpected error while updating logo: ", e);
        }

        return false;
    }
}
```

A classe `LogoUpdateHandler` implementa o método `ContentUpdateHandler` da interface, que utiliza vários argumentos:`updateCacheEntry(ConfigEntry, Long, String, Session, Session)`

* Uma instância `ConfigEntry` que fornece acesso à entrada de configuração, para a qual esse manipulador é chamado, e suas propriedades.
* Um carimbo de data e hora `lastUpdated` que indica a última vez que a Sincronização de conteúdo atualizou seu cache. O conteúdo que não foi modificado após esse carimbo de data e hora não deve ser atualizado pelo manipulador.
* Um argumento `configCacheRoot` que especifica o caminho raiz do cache. Todos os arquivos atualizados devem ser armazenados abaixo desse caminho para serem adicionados ao arquivo zip.
* Uma sessão administrativa que deve ser usada para todas as operações de repositório relacionadas ao cache.
* Uma sessão de usuário que pode ser usada para atualizar o conteúdo no contexto de um determinado usuário e, portanto, fornecer um tipo de conteúdo personalizado.

Para implementar o manipulador personalizado, primeiro crie uma instância da classe Image com base no recurso fornecido na entrada de configuração. Este é basicamente o mesmo procedimento que o componente de logotipo real em nossas páginas está fazendo. Certifique-se de que o caminho do público alvo da imagem seja o mesmo referenciado a partir de uma página.

Em seguida, verifique se o recurso foi modificado desde a última atualização. As implementações personalizadas devem evitar atualizações desnecessárias do cache e retornar falso se nada mudar. Se o recurso foi modificado, copie a imagem para o local de público alvo esperado relativo à raiz do cache. Finalmente, `true` é retornado para indicar à estrutura que o cache foi atualizado.

## Usar o conteúdo no cliente {#using-the-content-on-the-client}

Para usar o conteúdo em um aplicativo móvel fornecido pela Sincronização de conteúdo, é necessário solicitar o conteúdo por meio de uma conexão HTTP ou HTTPS. Como resultado, o conteúdo recuperado (empacotado em um arquivo ZIP) pode ser extraído e armazenado localmente no dispositivo móvel. Observe que o conteúdo não se refere apenas aos dados, mas também à lógica, ou seja, aos aplicativos da Web completos; permitindo que o usuário móvel execute aplicativos da Web recuperados e dados correspondentes, mesmo sem conectividade de rede.

A Sincronização de conteúdo fornece conteúdo de forma inteligente: Somente as alterações de dados desde a última sincronização de dados bem-sucedida são entregues, reduzindo assim o tempo necessário para a transferência de dados. Na primeira execução de um aplicativo, são solicitadas alterações de dados desde 1 de janeiro de 1970, enquanto subsequentemente somente os dados que mudaram desde a última sincronização bem-sucedida são solicitados. AEM utiliza uma estrutura de comunicação do cliente para iOS para simplificar a comunicação e transferência de dados, de modo que uma quantidade mínima de código nativo seja necessária para habilitar um aplicativo da Web baseado no iOS.

Todos os dados transferidos podem ser extraídos na mesma estrutura de diretório, não há etapas adicionais (por exemplo, verificações de dependência) necessárias ao extrair dados. No caso do iOS, todos os dados são armazenados em uma subpasta dentro da pasta Documentos do aplicativo iOS.

Caminho típico de execução de um aplicativo AEM Mobile baseado em iOS:

* Aplicativo de start do usuário no dispositivo iOS.
* O aplicativo tenta se conectar AEM backend e solicita alterações de dados desde a última execução.
* O servidor recupera os dados em questão e os compacta em um arquivo.
* Os dados são retornados para o dispositivo cliente, onde são extraídos para a pasta documentos.
* Start/atualizações do componente UIWebView.

Se uma conexão não puder ser estabelecida, os dados baixados anteriormente serão exibidos.

### Aproximando-se {#getting-ahead}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Criação para Adobe PhoneGap Enterprise com AEM](/help/mobile/phonegap.md)
* [Administração de conteúdo para Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)

