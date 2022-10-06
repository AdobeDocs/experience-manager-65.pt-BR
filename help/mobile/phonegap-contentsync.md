---
title: Móvel com sincronização de conteúdo
seo-title: Mobile with Content Sync
description: Siga esta página para saber mais sobre a Sincronização de conteúdo para Adobe PhoneGap Enterprise com o AEM.
seo-description: Follow this page to learn about Content Sync for Adobe PhoneGap Enterprise with AEM.
uuid: c3a82171-e070-4e32-b1ef-26e65ae23d99
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 923fc031-1a06-4a9d-94da-a2a4e82c54ee
docset: aem65
exl-id: 2cadd9c5-4335-48d0-8d1c-941fca717409
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2971'
ht-degree: 0%

---

# Móvel com sincronização de conteúdo{#mobile-with-content-sync}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Este documento faz parte do [Introdução ao AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guia, um ponto de partida recomendado para referência do AEM Mobile.

Use a Sincronização de conteúdo para empacotar o conteúdo para que ele possa ser usado em aplicativos móveis nativos. As páginas criadas no AEM podem ser usadas como conteúdo do aplicativo, mesmo quando o dispositivo está offline. Além disso, como AEM páginas são baseadas em padrões da Web, elas funcionam em várias plataformas, permitindo que você as incorpore a qualquer wrapper nativo. Essa estratégia reduz o esforço de desenvolvimento e permite atualizar facilmente o conteúdo do aplicativo.

>[!NOTE]
>
>Os aplicativos PhoneGap criados com AEM ferramentas já estão configurados para usar AEM páginas como conteúdo via Sincronização de conteúdo.

A estrutura de Sincronização de conteúdo cria um arquivo de arquivamento que contém o conteúdo da Web. O conteúdo pode ser qualquer coisa a partir de páginas simples, imagens e arquivos de PDF, ou de aplicações web inteiras. A API de Sincronização de conteúdo fornece acesso ao arquivo de arquivamento de aplicativos móveis ou processos de criação para que o conteúdo possa ser recuperado e incluído no aplicativo.

A sequência de etapas a seguir ilustra um caso de uso típico da Sincronização de conteúdo:

1. O desenvolvedor do AEM cria uma configuração de Sincronização de conteúdo que especifica o conteúdo a ser incluído.
1. A estrutura de Sincronização de conteúdo coleta e armazena em cache o conteúdo.
1. Em um dispositivo móvel, o aplicativo móvel é iniciado e solicita conteúdo do servidor, que é fornecido em um arquivo ZIP.
1. O cliente descompacta o conteúdo ZIP no sistema de arquivos local. A estrutura de pastas no arquivo ZIP simula os caminhos que um cliente (por exemplo, um navegador) normalmente solicitaria do servidor.
1. O cliente abre o conteúdo em um navegador incorporado ou o usa de alguma outra maneira.
1. Posteriormente, o cliente solicita o conteúdo atualizado do servidor. A estrutura de Sincronização de conteúdo fornece atualizações incrementais para reduzir o tamanho e o tempo de download, o que pode ser importante para os dispositivos móveis devido à largura de banda limitada ou aos volumes de dados.

>[!NOTE]
>
>Para obter mais informações sobre as diretrizes para o desenvolvimento de manipuladores de Sincronização de conteúdo, consulte manipuladores de aplicativos prontos para uso, consulte [Desenvolvimento de manipuladores de sincronização de conteúdo](/help/mobile/contentsync-app-handlers.md).

## Configurar o conteúdo da sincronização de conteúdo {#configuring-the-content-sync-content}

Crie uma configuração de Sincronização de conteúdo para especificar o conteúdo do arquivo ZIP que é entregue ao cliente. É possível criar qualquer número de configurações de Sincronização de conteúdo. Cada configuração tem um nome para fins de identificação.

Para criar uma configuração de Sincronização de conteúdo, adicione uma `cq:ContentSyncConfig` para o repositório, com o `sling:resourceType` propriedade definida como `contentsync/config`. O `cq:ContentSyncConfig` pode ser localizado em qualquer lugar no repositório, no entanto, o nó deve estar acessível aos usuários na instância de publicação do AEM. Portanto, você deve adicionar o nó abaixo `/content`.

Para especificar o conteúdo do arquivo ZIP da Sincronização de Conteúdo, adicione nós filhos ao nó cq:ContentSyncConfig . As seguintes propriedades de cada nó filho identificam um item de conteúdo a ser incluído e como ele é processado ao adicioná-lo:

* `path`: O local do conteúdo.
* `type`: O nome do tipo de configuração a ser usado para processar o conteúdo. Vários tipos estão disponíveis e são descritos em Tipos de configuração.

Consulte Exemplo de configuração de sincronização de conteúdo.

Após criar a configuração da Sincronização de conteúdo, ela aparecerá no console Sincronização de conteúdo.

>[!NOTE]
>
>A estrutura de Sincronização de conteúdo não verifica se as dependências de ativos e arquivos relacionados ao design estão incluídas nos pacotes de Sincronização de conteúdo. Certifique-se de incluir todos os arquivos necessários no arquivo ZIP.

### Configuração do acesso aos downloads da sincronização de conteúdo {#configuring-access-to-content-sync-downloads}

Especifique um usuário ou grupo que possa ser baixado da Sincronização de conteúdo. É possível configurar o usuário ou grupo padrão que pode ser baixado de todos os caches de Sincronização de conteúdo, bem como substituir o padrão e configurar o acesso para uma configuração específica de Sincronização de conteúdo.

Quando o AEM é instalado, os membros do grupo de administradores podem fazer download do Content Sync por padrão.

### Configuração do acesso padrão para downloads de sincronização de conteúdo {#setting-the-default-access-for-content-sync-downloads}

O serviço Day CQ Content Sync Manager controla o acesso à Sincronização de conteúdo. Configure esse serviço para especificar o usuário ou grupo que pode ser baixado da Sincronização de conteúdo por padrão.

Se você [configuração do serviço usando o Console da Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), digite o nome do usuário ou grupo como o valor da propriedade Autorizável de Cache de Fallback.

Se você [configuração no repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository), use as seguintes informações sobre o serviço:

* PID: com.day.cq.contentsync.impl.ContentSyncManagerImpl
* Nome da propriedade: contentsync.fallback.authorizable

#### Substituição do acesso a download para um cache de sincronização de conteúdo {#overriding-download-access-for-a-content-sync-cache}

Para configurar o acesso de download para uma configuração específica do Content Sync, adicione a seguinte propriedade ao `cq:ContentSyncConfig` nó:

* Nome: autorizável
* Tipo: String
* Valor: O nome do usuário ou grupo que pode baixar.

Por exemplo, seu aplicativo permite que os usuários instalem atualizações diretamente da Sincronização de conteúdo. Para permitir que todos os usuários baixem a atualização, você define o valor da propriedade autorizável como `everyone`.

Se a variável `cq:ContentSyncConfig` não tem propriedade autorizável, o usuário ou grupo padrão configurado para a propriedade Autorizável de Cache de Fallback do serviço Day CQ Content Sync Manager determina quem pode baixar.

### Configuração do usuário para atualizar um cache de sincronização de conteúdo {#configuring-the-user-for-updating-a-content-sync-cache}

Quando um usuário executa uma atualização do cache do Content Sync, uma conta de usuário específica executa a ação em nome do usuário. O usuário anônimo atualiza todos os caches de Sincronização de Conteúdo por padrão.

Você pode substituir o usuário padrão e especificar um usuário ou grupo que atualize um cache de Sincronização de conteúdo específico.

Para substituir o usuário padrão, especifique um usuário ou grupo que execute atualizações para uma configuração de Sincronização de conteúdo específica, adicionando a seguinte propriedade ao nó cq:ContentSyncConfig :

* Nome: updateuser
* Tipo: String
* Valor: O nome do usuário ou grupo que pode executar as atualizações.

Se o nó cq:ContentSyncConfig não tiver uma propriedade updateuser, o usuário anônimo padrão atualizará o cache.

### Tipos de configuração {#configuration-types}

O processamento pode variar desde a renderização de JSON simples até a renderização completa de páginas, incluindo seus ativos referenciados. Esta seção lista os tipos de configuração disponíveis e seus parâmetros específicos:

**copiar** Basta copiar arquivos e pastas.

* **caminho** - Se o caminho apontar para um único arquivo, somente o arquivo será copiado. Se ele apontar para uma pasta (isso inclui nós de página), todos os arquivos e pastas abaixo serão copiados.

**conteúdo** Renderize o conteúdo usando o processamento de solicitação Sling padrão.

* **caminho** - Caminho para o recurso que deve ser de saída.
* **extensão** - Extensão que deve ser usada na solicitação. Exemplos comuns são *html* e *json*, mas qualquer outra extensão é possível.

* **seletor** - Seletores opcionais separados por ponto. Exemplos comuns são *toque* para renderização de versões móveis de uma página ou *infinito* para saída JSON.

**clientlib** Compacte uma biblioteca do cliente Javascript ou CSS.

* **caminho** - Caminho para a raiz da biblioteca do cliente.
* **extensão** - Tipo de biblioteca do cliente. Isso deve ser definido como *js* ou *css* no momento.

* **includeFolders** - Tipo é uma matriz de sequências de caracteres e permite que o usuário especifique pastas adicionais para digitalização na biblioteca do cliente para buscar arquivos (como fontes personalizadas).

**ativos**

Coletar representações originais de ativos.

* **caminho** - Caminho para uma pasta de ativos abaixo de /content/dam.
* **representações** - Tipo é uma matriz de sequências de caracteres que permite ao usuário especificar quais representações usar em vez da imagem padrão. A lista a seguir resume algumas representações prontas, mas você também pode usar qualquer representação criada pelo fluxo de trabalho:

   * *original*
   * *cq5dam.thumbnail.48.48.png*
   * *cq5dam.thumbnail.319.319.png*
   * *cq5dam.thumbnail.140.100.png*
   * *cq5dam.web.1280.1280.png*

**imagem** Colete uma imagem.

* **caminho** - Caminho para um recurso de imagem.

O tipo de imagem é usado para incluir o logotipo We.Retail no arquivo zip.

**páginas** Renderize AEM páginas e colete ativos referenciados.

* **caminho** - Caminho para uma página.
* **extensão** - Extensão que deve ser usada na solicitação. Para páginas, isso é quase sempre *html*, mas outros ainda são possíveis.

* **seletor** - Seletores opcionais separados por ponto. Exemplos comuns são *toque* para renderização de versões móveis de uma página.

* **profundo** - Propriedade booleana opcional que determina se páginas filhas também devem ser incluídas. O valor padrão é *verdadeiro.*

* **includeImages** - Propriedade booleana opcional que determina se imagens devem ser incluídas. O valor padrão é *true*.
Por padrão, somente os componentes de imagem com um tipo de recurso de foundation/components/image são considerados para inclusão. Você pode adicionar mais tipos de recursos configurando a variável **Manipulador de atualização das páginas do Day CQ WCM** no console da Web.

**reescrever** O nó rewrite define como os links são regravados na página exportada. Os links reescritos podem apontar para os arquivos incluídos no arquivo zip ou para os recursos no servidor.

O `rewrite` O nó precisa estar localizado abaixo do `page` nó .

O `rewrite` pode ter uma ou mais das seguintes propriedades:

* `clientlibs`: regrava caminhos clientlibs.

* `images`: regrava caminhos de imagens.
* `links`: regrava caminhos de links.

Cada propriedade pode ter um dos seguintes valores:

* `REWRITE_RELATIVE`: regrava o caminho com uma posição relativa ao arquivo .html da página no sistema de arquivos.

* `REWRITE_EXTERNAL`: reescreve o caminho apontando para o recurso no servidor, usando o AEM [Serviço Externalizador](/help/sites-developing/externalizer.md).

O serviço de AEM chamado **PathRewriterTransformerFactory** permite configurar os atributos html específicos que serão regravados. O serviço pode ser configurado no console da Web e tem uma configuração para cada propriedade do `rewrite` nó: `clientlibs`, `images` e `links`.

Esse recurso foi adicionado no AEM 5.5.

### Exemplo de configuração de sincronização de conteúdo {#example-content-sync-configuration}

A listagem abaixo mostra um exemplo de configuração para a Sincronização de conteúdo.

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

**etc.designs.default e etc.designs.mobile** As duas primeiras entradas da configuração devem ser bastante óbvias. Como vamos incluir várias páginas móveis, precisamos dos arquivos de design relacionados abaixo de /etc/designs. E como não há necessidade de processamento extra, a cópia é suficiente.

**events.plist** Esta entrada é um pouco especial. Como mencionado na introdução, o aplicativo deve fornecer uma exibição de mapa com marcadores da localização dos eventos. Vamos fornecer as informações de localização necessárias como um arquivo separado no formato PLIST. Para que isso funcione, o componente de lista de eventos usado na página de índice tem um script chamado plist.jsp. Esse script é executado quando o recurso do componente é solicitado com a extensão .plist . Como de costume, o caminho dos componentes é fornecido na propriedade path e o tipo é definido como conteúdo, pois queremos aproveitar o processamento de solicitação do Sling.

**events.touch.html** Em seguida, vem as páginas reais que serão exibidas no aplicativo. A propriedade path é definida como a página raiz dos eventos. Todas as páginas de evento abaixo dessa página também serão incluídas, pois o padrão da propriedade profunda é true. Usamos páginas como tipo de configuração, de modo que qualquer imagem ou outro arquivo que possa ser referenciado a partir de uma imagem ou componente de download em uma página será incluído. Além disso, definir o seletor de toque oferece uma versão móvel das páginas. A configuração no pacote de recursos contém mais entradas desse tipo, mas elas são deixadas de fora para simplicidade aqui.

**logotipo** O tipo de configuração do logotipo não foi mencionado até agora e não é nenhum dos tipos incorporados. No entanto, a estrutura de Sincronização de conteúdo é extensível até certo ponto e esse é um exemplo disso, que será abordado na próxima seção.

**manifest** Geralmente, é desejável ter algum tipo de metadados incluídos no arquivo zip, como a página inicial do conteúdo, por exemplo. No entanto, codificar essas informações de maneira rígida evita que você as altere facilmente mais tarde. A estrutura de Sincronização de conteúdo oferece suporte a esse caso de uso, procurando um nó de manifesto na configuração, que é simplesmente identificado pelo nome e não requer um tipo de configuração. Cada propriedade definida nesse nó específico é adicionada a um arquivo, que também é chamado de manifesto e reside na raiz do arquivo zip.

No exemplo, a página de listagem de eventos deve ser a página inicial. Essas informações são fornecidas no **indexPage** e pode ser facilmente alterada a qualquer momento. Uma segunda propriedade define o caminho da variável *events.plist* arquivo. Como veremos mais tarde, o aplicativo cliente agora pode ler o manifesto e agir de acordo com ele.

Assim que a configuração for configurada, o conteúdo poderá ser baixado com um navegador ou qualquer outro cliente HTTP, ou se você estiver desenvolvendo para o iOS, poderá usar a biblioteca do cliente WAppKitSync dedicada. O local de download é composto pelo caminho da configuração e pela variável *.zip* , por exemplo, ao trabalhar com uma instância de AEM local: *https://localhost:4502/content/weretail_go.zip*

### O Console de sincronização de conteúdo {#the-content-sync-console}

O console Sincronização de conteúdo lista todas as configurações da Sincronização de conteúdo no repositório (todos os nós do tipo `cq:ContentSyncConfig`) e para cada configuração, você pode fazer o seguinte:

* Atualize o cache.
* Limpe o cache.
* Baixe um zip completo.
* Baixe um zip de comparação entre agora e uma data e hora específicas.

Ele pode ser útil para desenvolvimento e solução de problemas.

O console pode ser acessado em:

`https://localhost:4502/libs/cq/contentsync/content/console.html`

Tem a seguinte aparência:

![chlimage_1](assets/chlimage_1.png)

### Extensão da estrutura de Sincronização de conteúdo {#extending-the-content-sync-framework}

Embora o número de opções de configuração já seja bastante grande, ele pode não abranger todos os requisitos do caso de uso específico. Esta seção descreve os pontos de extensão da estrutura de Sincronização de conteúdo e como criar tipos de configuração personalizados.

Para cada tipo de configuração, há uma *Manipulador de atualização de conteúdo*, que é uma fábrica de componentes OSGi registrada para esse tipo específico. Esses manipuladores coletam conteúdo, processam e adicionam a um cache mantido pela estrutura de Sincronização de conteúdo. Implemente a seguinte interface ou classe base abstrata:

* `com.day.cq.contentsync.handler.ContentUpdateHandler` - Interface de que todos os manipuladores de atualização precisam implementar
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - Uma classe abstrata que simplifica a renderização de recursos usando o Sling

Registre sua classe como fábrica de componentes OSGi e implante-a no contêiner OSGi em um pacote. Isso pode ser feito usando o [Plug-in SCR Maven](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html) usando tags ou anotações do JavaDoc. O exemplo a seguir mostra a versão do JavaDoc:

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

Observe que a variável *fábrica* A definição contém a interface comum e o tipo personalizado separado por barra. Essa estratégia permite que a estrutura Sincronização de conteúdo encontre e crie uma instância da sua classe personalizada, pois reconhece o tipo personalizado em uma entrada de configuração. A próxima seção fornece um exemplo concreto de um manipulador de atualização personalizado.

>[!CAUTION]
>
>Ao construir sobre a classe base AbstractSlingResourceUpdateHandler , você deve adicionar o *herdar* definição. Caso contrário, o contêiner OSGi não definirá as referências necessárias que são declaradas na classe base.

### Implementar um manipulador de atualização personalizado {#implementing-a-custom-update-handler}

Cada página do We.Retail Mobile contém um logotipo no canto superior esquerdo que gostaríamos de incluir no arquivo zip, é claro. No entanto, para otimização de cache, AEM não faz referência ao local real do arquivo de imagem no repositório, o que nos impede de usar simplesmente o **copiar** tipo de configuração. Em vez disso, o que temos de fazer é proporcionar o nosso próprio **logotipo** tipo de configuração que disponibiliza a imagem no local solicitado pelo AEM. A listagem de código a seguir mostra a implementação completa do manipulador de atualização de logotipo:

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

O `LogoUpdateHandler` classe implementa `ContentUpdateHandler` da interface `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` , que utiliza vários argumentos:

* A `ConfigEntry` instância que fornece acesso à entrada de configuração, para a qual esse manipulador é chamado, e suas propriedades.
* A `lastUpdated` carimbo de data e hora que indica a última vez que a Sincronização de conteúdo atualizou seu cache. O conteúdo que não foi modificado após esse carimbo de data e hora não deve ser atualizado pelo manipulador.
* A `configCacheRoot` argumento que especifica o caminho raiz do cache. Todos os arquivos atualizados devem ser armazenados abaixo desse caminho para serem adicionados ao arquivo zip.
* Uma sessão administrativa que deve ser usada para todas as operações de repositório relacionadas ao cache.
* Uma sessão de usuário que pode ser usada para atualizar o conteúdo no contexto de um determinado usuário e, portanto, fornecer um tipo de conteúdo personalizado.

Para implementar o manipulador personalizado, primeiro crie uma instância da classe Image com base no recurso fornecido na entrada de configuração. Esse é basicamente o mesmo procedimento que o componente de logotipo real em nossas páginas está fazendo. Certifique-se de que o caminho de destino da imagem seja o mesmo referenciado de uma página.

Em seguida, verifique se o recurso foi modificado desde a última atualização. As implementações personalizadas devem evitar atualizações desnecessárias do cache e retornar false se nada for alterado. Se o recurso tiver sido modificado, copie a imagem para o local de destino esperado em relação à raiz do cache. Por último, `true` é retornado para indicar à estrutura que o cache foi atualizado.

## Uso do conteúdo no cliente {#using-the-content-on-the-client}

Para usar conteúdo em um aplicativo móvel fornecido pela Sincronização de conteúdo, é necessário solicitar conteúdo por meio de uma conexão HTTP ou HTTPS. Como resultado, o conteúdo recuperado (empacotado em um arquivo ZIP) pode ser extraído e armazenado localmente no dispositivo móvel. Observe que o conteúdo não se refere apenas aos dados, mas também à lógica, ou seja, aos aplicativos Web completos; dessa forma, o usuário móvel pode executar aplicativos da Web recuperados e dados correspondentes mesmo sem conectividade de rede.

A Sincronização de conteúdo fornece conteúdo de forma inteligente: Somente as alterações de dados desde a última sincronização de dados bem-sucedida são entregues, reduzindo o tempo necessário para a transferência de dados. Na primeira execução de um aplicativo, são necessárias alterações nos dados desde 1 de Janeiro de 1970, sendo posteriormente solicitados apenas os dados que foram alterados desde a última sincronização bem-sucedida. O AEM usa uma estrutura de comunicação de cliente para o iOS para simplificar a comunicação e a transferência de dados, de modo que uma quantidade mínima de código nativo é necessária para habilitar um aplicativo Web baseado em iOS.

Todos os dados transferidos podem ser extraídos na mesma estrutura de diretório, não há etapas adicionais (por exemplo, verificações de dependência) necessárias ao extrair dados. No caso do iOS, todos os dados são armazenados em uma subpasta dentro da pasta Documents do aplicativo do iOS.

Caminho de execução típico de um aplicativo AEM Mobile baseado em iOS:

* O usuário inicia o aplicativo no dispositivo iOS.
* O aplicativo tenta se conectar AEM backend e solicita alterações de dados desde a última execução.
* O servidor recupera os dados em questão e os compacta em um arquivo.
* Os dados são retornados ao dispositivo cliente, onde são extraídos na pasta de documentos.
* O componente UIWebView inicia/atualiza.

Se uma conexão não puder ser estabelecida, os dados baixados anteriormente serão exibidos.

### Avançar {#getting-ahead}

Para saber mais sobre as funções e responsabilidades de um Administrador e Desenvolvedor, consulte os recursos abaixo:

* [Criação para Adobe PhoneGap Enterprise com AEM](/help/mobile/phonegap.md)
* [Administração de conteúdo para Adobe PhoneGap Enterprise com AEM](/help/mobile/administer-phonegap.md)
