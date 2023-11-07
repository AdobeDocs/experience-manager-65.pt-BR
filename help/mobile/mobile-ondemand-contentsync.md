---
title: Dispositivo móvel com sincronização de conteúdo
description: Siga esta página para saber mais sobre a Sincronização de conteúdo. As páginas criadas no Adobe Experience Manager (AEM) podem ser usadas como conteúdo do aplicativo, mesmo quando o dispositivo está offline. Além disso, como as páginas AEM são baseadas em padrões da Web, elas funcionam em várias plataformas, permitindo que você as incorpore em qualquer invólucro nativo. Essa estratégia reduz o esforço de desenvolvimento e permite atualizar facilmente o conteúdo do aplicativo.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: a6e59334-09e2-4bb8-b445-1868035da556
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2973'
ht-degree: 0%

---

# Dispositivo móvel com sincronização de conteúdo{#mobile-with-content-sync}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Use a Sincronização de conteúdo para empacotar o conteúdo para que ele possa ser usado em aplicativos móveis nativos. As páginas criadas no Adobe Experience Manager (AEM) podem ser usadas como conteúdo do aplicativo, mesmo quando o dispositivo está offline. Além disso, como as páginas AEM são baseadas em padrões da Web, elas funcionam em várias plataformas, permitindo que você as incorpore em qualquer invólucro nativo. Essa estratégia reduz o esforço de desenvolvimento e permite atualizar facilmente o conteúdo do aplicativo.

A estrutura de sincronização de conteúdo cria um arquivo que contém o conteúdo da Web. O conteúdo pode ser qualquer coisa, desde páginas simples, imagens e arquivos PDF ou aplicações Web inteiras. A API de sincronização de conteúdo fornece acesso ao arquivo morto de aplicativos móveis ou processos de criação para que o conteúdo possa ser recuperado e incluído no aplicativo.

A sequência de etapas a seguir ilustra um caso de uso típico da Sincronização de conteúdo:

1. O desenvolvedor do AEM cria uma configuração de Sincronização de conteúdo que especifica o conteúdo a ser incluído.
1. A estrutura de sincronização de conteúdo coleta e armazena o conteúdo em cache.
1. Em um dispositivo móvel, o aplicativo móvel é iniciado e solicita conteúdo do servidor, que é entregue em um arquivo ZIP.
1. O cliente descompacta o conteúdo do ZIP no sistema de arquivos local. A estrutura de pastas no arquivo ZIP simula os caminhos que um cliente (por exemplo, um navegador) normalmente solicitaria ao servidor.
1. O cliente abre o conteúdo em um navegador incorporado ou o usa de alguma outra maneira.
1. Posteriormente, o cliente solicitará o conteúdo atualizado do servidor. A estrutura de sincronização de conteúdo fornece atualizações incrementais para reduzir o tamanho e o tempo de download, que podem ser importantes para dispositivos móveis devido à largura de banda ou volumes de dados limitados.

## Desenvolvimento de manipuladores de sincronização de conteúdo {#developing-the-content-sync-handlers}

Algumas das diretrizes para desenvolver Manipuladores de sincronização de conteúdo são as seguintes:

* Os manipuladores devem implementar *com.day.cq.contentsync.handler.ContentUpdateHandler* (seja diretamente ou estendendo uma classe que o faz)
* Os manipuladores podem estender *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* O manipulador só deverá relatar true se atualizar o cache ContentSync. Falsamente relatar verdadeiro tem AEM criado uma atualização quando uma atualização não ocorreu de fato.
* O manipulador só deve atualizar o cache se o conteúdo for alterado. Não grave no cache se um branco não for necessário. Isso resulta na criação de uma atualização desnecessária.

>[!NOTE]
>
>Ativar *Log de depuração do ContentSync* por meio de configurações do logger OSGI no pacote *com.day.cq.contentsync*. Isso permite rastrear quais manipuladores foram executados e se eles atualizaram o cache e relataram a atualização do cache.

## Configurar o conteúdo de sincronização do conteúdo {#configuring-the-content-sync-content}

Crie uma configuração de Sincronização de conteúdo para especificar o conteúdo do arquivo ZIP que é entregue ao cliente. Você pode criar qualquer número de configurações de sincronização de conteúdo. Cada configuração tem um nome para fins de identificação.

Para criar uma configuração de sincronização de conteúdo, adicione um `cq:ContentSyncConfig` para o repositório, com o `sling:resourceType` propriedade definida como `contentsync/config`. A variável `cq:ContentSyncConfig` O nó pode estar localizado em qualquer lugar no repositório, no entanto, deve estar acessível aos usuários na instância de publicação do AEM. Portanto, você deve adicionar o nó abaixo `/content`.

Para especificar o conteúdo do arquivo ZIP de sincronização de conteúdo, adicione nós secundários ao nó cq:ContentSyncConfig. As seguintes propriedades de cada nó secundário identificam um item de conteúdo a ser incluído e como ele é processado ao adicioná-lo:

* `path`: o local do conteúdo.
* `type`: o nome do tipo de configuração a ser usado para processar o conteúdo. Vários tipos estão disponíveis e são descritos na seção *Tipos de configuração*.

Consulte *Exemplo de configuração de sincronização de conteúdo* para obter mais informações.

Depois de criar a configuração da Sincronização de conteúdo, ela aparece no console de Sincronização de conteúdo.

>[!NOTE]
>
>A estrutura de sincronização de conteúdo não verifica se as dependências de ativos e arquivos relacionados ao design estão incluídas nos pacotes de sincronização de conteúdo. Certifique-se de incluir todos os arquivos necessários no arquivo ZIP.

### Configuração do acesso a downloads de sincronização de conteúdo {#configuring-access-to-content-sync-downloads}

Especifique um usuário ou grupo que possa baixar da Sincronização de conteúdo. Você pode configurar o usuário ou grupo padrão que pode baixar de todos os caches da Sincronização de conteúdo, e pode substituir o padrão e configurar o acesso para uma configuração específica da Sincronização de conteúdo.

Quando o AEM é instalado, os membros do grupo do administrador podem baixar o da Sincronização de conteúdo por padrão.

#### Configuração do acesso padrão para downloads de sincronização de conteúdo {#setting-the-default-access-for-content-sync-downloads}

O serviço Gerenciador de sincronização de conteúdo do Day CQ controla o acesso à Sincronização de conteúdo. Configure esse serviço para especificar o usuário ou grupo que pode baixar da Sincronização de conteúdo por padrão.

Se você estiver [configuração do serviço usando o Console da Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), digite o nome do usuário ou grupo como o valor da propriedade Cache de Fallback Autorizável.

Se você estiver [configuração no repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository), use as seguintes informações sobre o serviço:

* PID: com.day.cq.contentsync.impl.ContentSyncManagerImpl
* Nome da propriedade: contentsync.fallback.authorizable

#### Substituição do acesso de download para um cache de sincronização de conteúdo {#overriding-download-access-for-a-content-sync-cache}

Para configurar o acesso de download para uma configuração específica da Sincronização de conteúdo, adicione a seguinte propriedade à `cq:ContentSyncConfig` nó:

* Nome: autorizável
* Tipo: String
* Valor: o nome do usuário ou grupo que pode baixar.

Por exemplo, seu aplicativo permite que os usuários instalem atualizações diretamente da Sincronização de conteúdo. Para permitir que todos os usuários baixem a atualização, defina o valor da propriedade autorizable como `everyone`.

Se a variável `cq:ContentSyncConfig` O nó não tem propriedade autorizable, o usuário ou grupo padrão configurado para a propriedade Autorizable de Cache de Fallback do serviço Gerenciador de Sincronização de Conteúdo do Day CQ determina quem pode baixar.

### Configurar o usuário para atualizar um cache de sincronização de conteúdo {#configuring-the-user-for-updating-a-content-sync-cache}

Quando um usuário executa uma atualização do cache da Sincronização de conteúdo, uma conta de usuário específica executa a ação em nome do usuário. O usuário anônimo atualiza todos os caches de sincronização de conteúdo por padrão.

Você pode substituir o usuário padrão e especificar um usuário ou grupo que atualize um cache de sincronização de conteúdo específico.

Para substituir o usuário padrão, especifique um usuário ou grupo que execute atualizações para uma configuração de Sincronização de conteúdo específica adicionando a seguinte propriedade ao nó cq:ContentSyncConfig:

* Nome: `updateuser`
* Tipo: `String`
* Valor: o nome do usuário ou grupo que pode executar as atualizações.

Se a variável `cq:ContentSyncConfig` o nó não tem `updateuser` propriedade, o padrão `anonymous` O usuário atualiza o cache.

### Tipos de configuração {#configuration-types}

O processamento pode variar desde a renderização de JSON simples até a renderização completa de páginas, incluindo seus ativos referenciados. Esta seção lista os tipos de configuração disponíveis e seus parâmetros específicos:

**copiar** - Copiar arquivos e pastas.

* **caminho** - Se o caminho apontar para um único arquivo, somente o arquivo será copiado. Se ele apontar para uma pasta (isso inclui nós de página), todos os arquivos e pastas abaixo serão copiados.

**conteúdo** Renderizar conteúdo usando padrão [Processamento de solicitação do Sling](/help/sites-developing/the-basics.md#sling-request-processing).

* **caminho** - Caminho para o recurso que deve ser gerado.
* **extensão** - Extensão que deve ser usada na solicitação. Exemplos comuns são *html* e *json*, mas qualquer outra extensão é possível.

* **seletor** - Seletores opcionais separados por ponto. Exemplos comuns são *toque* para renderizar versões móveis de uma página ou *infinito* para saída JSON.

**clientlib** - Criar um pacote de uma biblioteca de cliente JavaScript ou CSS.

* **caminho** - Caminho para a raiz da biblioteca do cliente.
* **extensão** - Tipo de biblioteca do cliente. Isso deve ser definido como *js* ou *css* neste momento.

**ativos**

Coletar representações originais de ativos.

* **caminho** - Caminho para uma pasta de ativos abaixo de /content/dam.

**imagem** - Colete uma imagem.

* **caminho** - Caminho para um recurso de imagem.

O tipo de imagem é usado para incluir o logotipo We Retail no arquivo zip.

**páginas** - Renderize páginas AEM e colete ativos referenciados.

* **caminho** - Caminho para uma página.
* **extensão** - Extensão que deve ser usada na solicitação. Para páginas, isso é quase sempre *html*, mas outros ainda são possíveis.

* **seletor** - Seletores opcionais separados por ponto. Exemplos comuns são *toque* para renderizar versões móveis de uma página.

* **profundo** - Propriedade booleana opcional que determina se as páginas secundárias também devem ser incluídas. O valor padrão é *verdadeiro.*

* **includeImages** - Propriedade booleana opcional que determina se as imagens devem ser incluídas. O valor padrão é *true*.

  Por padrão, somente componentes de imagem com um tipo de recurso de fundação/componentes/imagem são considerados para inclusão. Você pode adicionar mais tipos de recursos configurando o **Manipulador de atualização de páginas WCM CQ do dia** no console da Web.

**reescrever** - O nó rewrite define como os links são reescritos na página exportada. Os links regravados podem apontar para os arquivos incluídos no arquivo zip ou para os recursos no servidor.

A variável `rewrite` deve estar localizado abaixo de `page` nó.

A variável `rewrite` pode ter uma ou mais das seguintes propriedades:

* `clientlibs`: substitui caminhos clientlibs.

* `images`: substitui caminhos de imagens.
* `links`: substitui caminhos de links.

Cada propriedade pode ter um dos seguintes valores:

* `REWRITE_RELATIVE`: substitui o caminho por uma posição relativa para o arquivo de página .html no sistema de arquivos.

* `REWRITE_EXTERNAL`: reescreve o caminho apontando para o recurso no servidor, usando o AEM [Serviço externalizador](/help/sites-developing/externalizer.md).

O serviço AEM chamou **PathRewriterTransformerFactory** permite configurar os atributos html específicos que serão reescritos. O serviço pode ser configurado no console da Web e tem uma configuração para cada propriedade do `rewrite` nó: `clientlibs`, `images`, e `links`.

Este recurso foi adicionado no AEM 5.5.

### Exemplo de configuração de sincronização de conteúdo {#example-content-sync-configuration}

A listagem abaixo mostra um exemplo de configuração para a Sincronização de conteúdo.

```xml
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

**etc.designs.default e etc.designs.mobile** - As duas primeiras entradas da configuração são óbvias. Como você vai incluir várias páginas móveis, você precisa dos arquivos de design relacionados abaixo /etc/designs. E como não há necessidade de processamento adicional, a cópia é suficiente.

**events.plist** - Essa entrada é um pouco especial. Conforme mencionado na introdução, o aplicativo deve fornecer uma visualização de mapa com marcadores dos locais dos eventos. As informações de localização necessárias serão fornecidas como um arquivo separado no formato PLIST. Para que isso funcione, o componente Lista de eventos que é usado na página índice, tem um script chamado plist.jsp. Esse script é executado quando o recurso do componente é solicitado com o `.plist` extensão. Como de costume, o caminho dos componentes é fornecido na propriedade path e o tipo é definido como content, porque você deseja usar [Processamento de solicitação do Sling](/help/sites-developing/the-basics.md#sling-request-processing).

**events.touch.html** - Em seguida, vêm as páginas reais que são mostradas no aplicativo. A propriedade path é definida como a página raiz dos eventos. Todas as páginas de eventos abaixo dessa página também serão incluídas, pois o padrão da propriedade deep é true. As páginas são usadas como tipo de configuração, para que todas as imagens ou outros arquivos que possam ser referenciados de uma imagem ou componente de download em uma página sejam incluídos. Além disso, definir o seletor de toque nos fornece uma versão móvel das páginas. A configuração no pacote de recursos contém mais entradas desse tipo, mas elas são deixadas de fora para simplificar aqui.

**logotipo** - O tipo de configuração de logotipo não foi mencionado até o momento e não é nenhum dos tipos incorporados. No entanto, a estrutura de sincronização de conteúdo é extensível em algum grau, e este é um exemplo disso, que será abordado na próxima seção.

**manifesto** - Geralmente, é desejável ter algum tipo de metadados incluídos no arquivo zip, como a página inicial do conteúdo, por exemplo. No entanto, a codificação rígida dessas informações impede que você as altere facilmente posteriormente. A estrutura de Sincronização de Conteúdo é compatível com esse caso de uso ao procurar um nó de manifesto na configuração, que é identificado por nome e não requer um tipo de configuração. Todas as propriedades definidas nesse nó específico são adicionadas a um arquivo, que também é chamado de manifest e reside na raiz do arquivo zip.

No exemplo, a página da listagem de eventos deve ser a página inicial. Essas informações são fornecidas no **indexPage** propriedade e, portanto, podem ser facilmente alteradas a qualquer momento. Uma segunda propriedade define o caminho da variável *events.plist* arquivo. Como você verá mais tarde, o aplicativo cliente agora pode ler o manifesto e agir de acordo com ele.

Quando a configuração for definida, o conteúdo poderá ser baixado com um navegador ou qualquer outro cliente HTTP, ou se você estiver desenvolvendo para iOS, poderá usar a biblioteca dedicada do cliente WAppKitSync. O local de download é composto do caminho da configuração e do *.zip* extensão, por exemplo, ao trabalhar com uma instância local do AEM: *http://localhost:4502/content/weretail_go.zip*

### O Console de sincronização de conteúdo {#the-content-sync-console}

O console de Sincronização de conteúdo lista todas as configurações de Sincronização de conteúdo no repositório (todos os nós do tipo `cq:ContentSyncConfig`) e, para cada configuração, permite fazer o seguinte:

* Atualize o cache.
* Limpe o cache.
* Baixe um zip completo.
* Baixe um zip de comparação entre agora e uma data e hora específica.

Pode ser útil para desenvolvimento e solução de problemas.

O console pode ser acessado em:

`http://localhost:4502/libs/cq/contentsync/content/console.html`

Ela tem a seguinte aparência:

![chlimage_1-50](assets/chlimage_1-50.png)

### Extensão da estrutura de sincronização de conteúdo {#extending-the-content-sync-framework}

Embora o número de opções de configuração já seja extenso, ele pode não abranger todos os requisitos do seu caso de uso específico. Esta seção descreve os pontos de extensão da estrutura de sincronização de conteúdo e como criar tipos de configuração personalizados.

Para cada tipo de configuração, há uma variável *Manipulador de atualização de conteúdo*, que é uma fábrica de componentes OSGi registrada para esse tipo específico. Esses manipuladores coletam conteúdo, processam-no e adicionam-no a um cache mantido pela estrutura de sincronização de conteúdo. Implemente a seguinte interface ou classe base abstrata:

* `com.day.cq.contentsync.handler.ContentUpdateHandler` - Interface que todos os manipuladores de atualização devem implementar
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - Uma classe abstrata que simplifica a renderização de recursos usando Sling

Registre sua classe como fábrica de componentes OSGi e implante-a no contêiner OSGi em um pacote. Isso pode ser feito usando o [Plug-in Maven SCR](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/apache-felix-maven-scr-plugin-use.html) usando tags ou anotações JavaDoc. O exemplo a seguir mostra a versão do JavaDoc:

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

Observe que *fábrica* A definição contém a interface comum e o tipo personalizado separados por barra. Essa estratégia permite que a estrutura de sincronização de conteúdo localize e crie uma instância de sua classe personalizada, pois ela reconhece o tipo personalizado em uma entrada de configuração. A próxima seção fornece um exemplo concreto de um manipulador de atualização personalizado.

>[!CAUTION]
>
>Ao criar com base na classe base AbstractSlingResourceUpdateHandler, você deve adicionar a variável *herdar* definição. Caso contrário, o contêiner OSGi não definirá as referências necessárias declaradas na classe base.

### Implementação de um manipulador de atualização personalizado {#implementing-a-custom-update-handler}

Cada página móvel do We.Retail contém um logotipo no canto superior esquerdo que deve ser incluído no arquivo zip. No entanto, para otimização de cache, o AEM não faz referência à localização real do arquivo de imagem no repositório, o que nos impede de simplesmente usar o **copiar** tipo de configuração. O que você deve fazer, em vez disso, é prover o seu próprio **logotipo** tipo de configuração que disponibiliza a imagem no local solicitado pelo AEM. A listagem de código a seguir mostra a implementação completa do manipulador de atualização de logotipo:

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

A variável `LogoUpdateHandler` A classe implementa o `ContentUpdateHandler` da interface `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` , que aceita vários argumentos:

* A `ConfigEntry` instância que fornece acesso à entrada de configuração, para a qual este manipulador é chamado, e suas propriedades.
* A `lastUpdated` carimbo de data e hora indicando a última vez que a sincronização de conteúdo atualizou seu cache. O conteúdo que não foi modificado depois desse carimbo de data e hora não deve ser atualizado pelo manipulador.
* A `configCacheRoot` argumento que especifica o caminho raiz do cache. Todos os arquivos atualizados devem ser armazenados abaixo deste caminho para serem adicionados ao arquivo zip.
* Uma sessão administrativa que deve ser usada para todas as operações de repositório relacionadas ao cache.
* Uma sessão de usuário que pode ser usada para atualizar o conteúdo no contexto de um determinado usuário e, portanto, fornecer um tipo de conteúdo personalizado.

Para implementar o manipulador personalizado, primeiro crie uma instância da classe Image com base no recurso fornecido na entrada de configuração. Este é o mesmo procedimento que o componente de logotipo real em nossas páginas está executando. Ele garante que o caminho de destino da imagem seja o mesmo referenciado de uma página.

Em seguida, verifique se o recurso foi modificado desde a última atualização. As implementações personalizadas devem evitar atualizações desnecessárias do cache e retornar falso se nada for alterado. Se o recurso foi modificado, copie a imagem para o local de destino esperado relativo à raiz do cache. Por último, `true` é retornado para indicar à estrutura que o cache foi atualizado.

## Usar o conteúdo no cliente {#using-the-content-on-the-client}

Para usar o conteúdo em um aplicativo móvel fornecido pela Sincronização de conteúdo, você deve solicitar o conteúdo por meio de uma conexão HTTP ou HTTPS. Como resultado, o conteúdo recuperado (compactado em um arquivo ZIP) pode ser extraído e armazenado localmente no dispositivo móvel. O conteúdo não se refere apenas aos dados, mas também à lógica, ou seja, aos aplicativos Web completos; portanto, permite que o usuário móvel execute aplicativos Web recuperados e dados correspondentes mesmo sem conectividade de rede.

A sincronização de conteúdo fornece conteúdo de forma inteligente: somente as alterações de dados ocorridas desde a última sincronização bem-sucedida de dados são fornecidas, reduzindo o tempo necessário para a transferência de dados. Na primeira execução de um aplicativo, as alterações de dados são solicitadas desde 1° de janeiro de 1970, enquanto posteriormente somente os dados alterados desde a última sincronização bem-sucedida são solicitados. O AEM usa uma estrutura de comunicação do cliente para o iOS a fim de simplificar a comunicação e a transferência de dados, de modo que uma quantidade mínima de código nativo seja necessária para habilitar um aplicativo web baseado em iOS.

Todos os dados transferidos podem ser extraídos para a mesma estrutura de diretório. Não há etapas adicionais (por exemplo, verificações de dependência) necessárias ao extrair dados. Se houver iOS, todos os dados serão armazenados em uma subpasta na pasta Documents do aplicativo iOS.

Caminho de execução típico de um aplicativo AEM Mobile com base em iOS:

* O usuário inicia o aplicativo no dispositivo iOS.
* O aplicativo tenta se conectar ao back-end do AEM e solicita alterações nos dados desde a última execução.
* O servidor recupera os dados em questão e os compacta em um arquivo.
* Os dados são retornados ao dispositivo cliente, onde são extraídos para a pasta de documentos.
* O componente UIWebView é iniciado/atualizado.

Se uma conexão não puder ser estabelecida anteriormente, os dados baixados serão exibidos.

### Recursos adicionais {#additional-resources}

Para saber mais sobre as funções e responsabilidades de um Administrador e de um Autor, consulte os recursos abaixo:

* [Criação de conteúdo AEM para o AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
* [Administração de conteúdo para usar o AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
