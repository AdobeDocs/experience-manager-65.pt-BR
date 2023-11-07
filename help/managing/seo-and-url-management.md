---
title: Práticas recomendadas de gerenciamento de SEO e URL
description: Saiba mais sobre as práticas recomendadas da SEO e recomendações sobre uma implementação do AEM.
topic-tags: managing
content-type: reference
docset: aem65
exl-id: b138f6d1-0870-4071-b96e-4a759ad9a76e
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '3677'
ht-degree: 67%

---

# Práticas recomendadas de gerenciamento de SEO e URL{#seo-and-url-management-best-practices}

A SEO (Otimização do mecanismo de pesquisa) se tornou uma preocupação principal para muitos profissionais de marketing. Como resultado, as preocupações com a SEO devem ser abordadas em muitos projetos de AEM.

Este documento descreve primeiro alguns [Práticas recomendadas da SEO](#seo-best-practices) e recomendações sobre uma implementação do AEM. Em seguida, ele detalha algumas [etapas de implementação mais complexas](#aem-configurations) abordadas na primeira seção.

## Práticas recomendadas da SEO {#seo-best-practices}

Esta seção descreve algumas práticas recomendadas gerais da SEO.

### URLs {#urls}

Existem algumas práticas recomendadas aceitas para URLs.

No projeto do AEM, ao avaliar os URLs, pergunte-se o seguinte:

&quot;Se um usuário visse esse URL e nenhum conteúdo na página, ele poderia descrever essa página?&quot;

Se a resposta for sim, então é provável que o URL funcione bem em um mecanismo de pesquisa.

Estas são algumas dicas gerais sobre como criar os URLs para SEO:

* Use hífenshifens para separar palavras.

   * Nomeie páginas usando hífenshifens (-) como separadores.
   * Evite usar concatenadas, sublinhados e espaços.

* Evite a utilização de parâmetros de consulta sempre que possível. Quando necessário, limite-os a dois ou menos.

   * Use a estrutura de diretório para indicar a arquitetura de informações, quando disponível.
   * Se uma estrutura de diretório não for uma opção, use seletores Sling no URL em vez de strings de consulta. Além do valor de SEO fornecido, os seletores sling também permitem que as páginas sejam armazenadas em cache pelo Dispatcher.

* Quanto mais legível for um URL, melhor. Ter palavras-chave presentes no URL aumenta o valor.

   * Ao usar seletores em uma página, os seletores que fornecem valor semântico são preferenciais.
   * Se um humano não conseguir ler o URL, um mecanismo de pesquisa também não poderá.
   * Por exemplo:
     `mybrand.com/products/product-detail.product-category.product-name.html`
é preferível a `mybrand.com/products/product-detail.1234.html`

* Evite subdomínios sempre que possível, já que os mecanismos de pesquisa os tratam como entidades diferentes, fragmentando o valor SEO do site.

   * Em vez disso, use subcaminhos de primeiro nível. Por exemplo, em vez de `es.mybrand.com/home.html`, use `www.mybrand.com/es/home.html`.

   * Planeje sua hierarquia de conteúdo para corresponder à forma como o conteúdo é apresentado, de acordo com essa diretriz.

* A eficácia da palavra-chave em URLs diminui conforme o comprimento do URL e a posição da palavra-chave aumentam. Em outras palavras, menor é melhor.

   * Use técnicas e recursos de redução de URL fornecidos pelo AEM para remover partes desnecessárias do URL.
   * Por exemplo, `mybrand.com/en/myPage.html` é preferível a `mybrand.com/content/my-brand/en/myPage.html`.

* Use URLs canônicos.

   * Quando um URL puder ser distribuído a partir de caminhos diferentes ou com parâmetros ou seletores diferentes, certifique-se de usar uma tag `rel=canonical` na página.

   * Inclua URLs canônicos no código do modelo AEM.

* Corresponder URLs a títulos de página sempre que possível.

   * Os autores de conteúdo devem ser encorajados a seguir essa prática.

* Insensibilidade a maiúsculas e minúsculas em solicitações de URL.

   * Configure o Dispatcher para regravar todas as solicitações de entrada em letras minúsculas.
   * Treine autores de conteúdo para criar todas as páginas usando letras minúsculas.

* Certifique-se de que cada página seja distribuída somente de um protocolo.

   * Às vezes, os sites serão distribuídos pelo `http` até que um usuário chegue a uma página com, por exemplo, um formulário de check-out ou logon, no qual ele é alternado para `https`. Ao criar links a partir dessa página, se o usuário puder retornar ao `http` páginas e acessá-las por meio de `https`, o mecanismo de pesquisa as rastreia como duas páginas separadas.

   * Atualmente, o Google prefere páginas `https` às páginas `http`. Eles ajudam a facilitar a vida de todos para distribuir todo o site pelo `https`.

### Configuração de servidor {#server-configuration}

Em termos de configuração do servidor, você pode executar as seguintes etapas para garantir que somente o conteúdo correto esteja sendo rastreado:

* Use um arquivo `robots.txt` para bloquear o rastreamento de qualquer conteúdo que não deve ser indexado.

   * Bloquear **todos** os rastreamentos em ambientes de teste.

* Ao iniciar um novo site com URLs atualizados, implemente os redirecionamentos 301 para garantir que sua classificação de SEO existente não seja perdida.
* Inclua um favicon para o site.
* Para facilitar o rastreamento de conteúdo pelos mecanismos de pesquisa, implemente um mapa de site XML. Certifique-se de incluir um mapa de site móvel para sites móveis e/ou responsivos.

## Configurações do AEM {#aem-configurations}

Esta seção descreve as etapas de implementação para configurar o AEM de acordo com as seguintes recomendações de SEO.

### Uso de seletores Sling {#using-sling-selectors}

Anteriormente, o uso de parâmetros de consulta era a prática mais aceita ao criar um aplicativo web corporativo.

A tendência nos últimos anos tem sido remover parâmetros para tornar os URLs mais legíveis. Em muitas plataformas, esse processo de remoção envolve a implementação de redirecionamentos no servidor da Web ou na Rede de entrega de conteúdo (CDN), mas o Sling torna o processo simples. Os seletores Sling:

* Melhoram a legibilidade do URL.
* Permitem o armazenamento das páginas em cache no Dispatcher e melhoram a segurança.
* Permite abordar o conteúdo diretamente, em vez de utilizar um servlet genérico para recuperar o conteúdo. Ele concede os benefícios das ACLs que você aplica no repositório e filtros que você aplica no Dispatcher.

#### Usar seletores para servlets {#using-selectors-for-servlets}

O AEM nos fornece duas opções ao gravar servlets:

* Servlets **bin**
* Servlets **Sling**

Os exemplos a seguir ilustram como registrar servlets que seguem esses dois padrões e mostram o benefício de se utilizar servlets Sling.

#### Servlets bin (um nível abaixo) {#bin-servlets-one-level-down}

Os servlets **Bin** seguem o padrão para o qual muitos desenvolvedores são usados na programação J2EE. O servlet é registrado em um caminho específico que, no AEM, geralmente está sob `/bin`e você extrai os parâmetros de solicitação necessários da cadeia de caracteres de consulta.

A anotação SCR para este tipo de servlet seria algo como isto:

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

Em seguida, você extrai os parâmetros da cadeia de caracteres de consulta por meio do objeto `SlingHttpServletRequest` incluído no método `doGet`; por exemplo:

```
String myParam = req.getParameter("myParam");
```

O URL resultante usado seria semelhante a:

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

Há alguns pontos a considerar com esta abordagem:

* O próprio URL perde o valor SEO. Os usuários que acessam o site, incluindo mecanismos de pesquisa, não recebem nenhum valor semântico do URL, pois o URL representa um caminho programático e não a hierarquia de conteúdo.
* A presença de parâmetros de consulta no URL significa que o Dispatcher não pode armazenar a resposta em cache.
* Se quiser proteger esse servlet, implemente sua própria lógica de segurança personalizada no servlet.
* O Dispatcher deve ser configurado (com cuidado) para expor o `/bin/myApp/myServlet`. Apenas expor o `/bin` permitiria o acesso a determinados servlets que não deveriam ser abertos a visitantes do site.

#### Servlets sling (um nível abaixo) {#sling-servlets-one-level-down}

Os servlets **sling** permitem registrar o servlet da maneira oposta. Em vez de endereçar um servlet e especificar o conteúdo que gostaria que o servlet renderizasse com base nos parâmetros de consulta, você endereçaria o conteúdo desejado. E você especifica o servlet que deve renderizar o conteúdo com base nos seletores Sling.

A anotação SCR para este tipo de servlet seria algo como isto:

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json", methods="GET")
```

Nesse caso, o recurso que o URL endereça - uma instância do `myPageType` resource - é acessível automaticamente no servlet. Para acessá-lo, você chama o seguinte:

```
Resource myPage = req.getResource();
```

O URL resultante usado seria semelhante a:

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

Os benefícios dessa abordagem são:

* Você pode fazer o bake do valor SEO, obtido pela semântica presente na hierarquia do site e no nome da página.
* Como nenhum parâmetro de consulta está presente, o Dispatcher pode armazenar a resposta em cache. Além disso, as atualizações feitas na página endereçada invalidarão esse cache quando a página for ativada.
* Todas as ACLs aplicadas a `/content/my-brand/my-page` entrarão em vigor quando um usuário tentar acessar este servlet.
* O Dispatcher já está configurado para distribuir esse conteúdo por meio de uma função de distribuição de site. Nenhuma configuração adicional é necessária.

### Regravação de URL {#url-rewriting}

No AEM, todas as páginas da Web são armazenadas no `/content/my-brand/my-content`. Embora esse local seja útil da perspectiva do gerenciamento de dados de repositório, não é necessariamente a forma como você deseja que os clientes vejam o site. Além disso, pode entrar em conflito com a orientação da SEO de manter os URLs o mais curtos possível. Além disso, você pode estar distribuindo vários sites da mesma instância do AEM e de nomes de domínio diferentes.

Esta seção analisa as opções disponíveis no AEM para gerenciar esses URLs e apresentá-los aos usuários de maneira mais legível e fácil de usar para SEO.

#### URLs personalizadas {#vanity-urls}

Se um autor desejar que uma página seja acessível de um segundo local para fins promocionais, os URLs personalizados do AEM, definidos página por página, podem ser úteis. Para adicionar um URL personalizado de uma página, navegue até ele no console **Sites** e edite as propriedades da página. Na parte inferior da guia **Básico**, você verá uma seção na qual URLs personalizados podem ser adicionados. Lembre-se de que ter a página acessível por mais de um URL fragmentará o valor SEO da página. Portanto, uma tag de URL canônica deve ser adicionada à página para evitar esse problema.

#### Nomes de página localizados {#localized-page-names}

Talvez você queira exibir nomes de página localizados para usuários de conteúdo traduzido. Por exemplo:

* Em vez de um usuário de língua espanhola navegar até:
  `www.mydomain.com/es/home.html`

* Seria melhor que o URL fosse:
  `www.mydomain.com/es/casa.html`.

O desafio em traduzir o nome da página é que muitas das ferramentas de tradução disponíveis na plataforma do AEM dependem da correspondência dos nomes das páginas entre os locais para manter o conteúdo sincronizado.

A variável `sling:alias` a propriedade permite ter o Adobe bolo e comê-lo também. Você pode adicionar `sling:alias` como uma propriedade a qualquer recurso para permitir um nome de alias para o recurso. No exemplo anterior, você teria o seguinte:

* Uma página no JCR em:
  `…/es/home`

* Em seguida, adicione uma propriedade a ela:
  `sling:alias` = `casa`

Esse fluxo permite que as ferramentas de tradução do AEM, como o gerente de vários sites, continuem a manter uma relação entre:

* `/en/home`

* `/es/home`

Ao mesmo tempo, permitiria que os usuários finais interagissem com o nome da página em seus idiomas nativos.

>[!NOTE]
>
>A propriedade `sling:alias` pode ser definida usando a propriedade [Alias ao editar as Propriedades da página](/help/sites-authoring/editing-page-properties.md#advanced).

#### /etc/map {#etc-map}

Em uma instalação padrão do AEM:

* para a configuração do OSGi
  **Apache Sling Resource Resolver Factory**
( `org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* a propriedade
  **Localização do mapeamento** ( `resource.resolver.map.location`)

* toma como padrão `/etc/map`

As definições de mapeamento podem ser adicionadas neste local para mapear solicitações de entrada, regravar URLs em páginas no AEM ou em ambos.

Para criar um mapeamento, crie um nó `sling:Mapping` neste local por meio de `/http` ou `/https`. Com base nas propriedades `sling:match` e `sling:internalRedirect` definidas neste nó, o AEM redirecionará todo o tráfego do URL correspondente para o valor especificado na propriedade `internalRedirect`.

Embora essa abordagem seja documentada na documentação oficial do AEM e Sling, o suporte regular à expressão fornecido por essa implementação é limitado no escopo quando comparado às opções disponíveis usando o `SlingResourceResolver` diretamente. Além disso, a implementação de mapeamentos desta maneira pode levar a problemas com a invalidação do cache do Dispatcher.

Este é um exemplo de como esse problema ocorre:

1. Um usuário visita o site e solicita `https://www.mydomain.com/my-page.html`
1. O Dispatcher encaminha essa solicitação ao servidor de publicação.
1. Usando o `/etc/map`, o servidor de publicação resolve essa solicitação para `/content/my-brand/my-page` e renderiza a página.

1. O Dispatcher armazena a resposta em cache em `/my-page.html` e retorna a resposta ao usuário.
1. Um autor de conteúdo altera essa página e a ativa.
1. O agente de liberação do Dispatcher envia uma solicitação de invalidação para `/content/my-brand/my-page`**.** Como o Dispatcher não tem uma página em cache neste caminho, o conteúdo antigo permanece em cache e é obsoleto.

Há maneiras de configurar regras personalizadas de liberação do Dispatcher que mapearão o URL mais curto para o URL mais longo para fins de invalidação de cache.

No entanto, há também uma maneira mais simples de gerenciar esse problema:

1. **Regras SlingResourceResolver**

   Usando o console da Web (por exemplo, localhost:4502/system/console/configMgr), você pode configurar o Sling Resource Resolver:

   * **Apache Sling Resource Resolver Factory**
     `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`.

   O Adobe recomenda que você crie os mapeamentos necessários para encurtar URLs como expressões regulares e, em seguida, defina essas configurações em um nó OsgiConfig, `config.publish` que está incluído na sua build.

   Em vez de definir os mapeamentos no `/etc/map`, eles podem ser atribuídos diretamente à propriedade **Mapeamentos de URL** ( `resource.resolver.mapping`):

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   Neste exemplo simples, você está removendo `/content/my-brand/` do início de qualquer URL em que ele esteja presente.

   Ele converte um URL:

   * de `/content/my-brand/my-page.html`
   * para apenas `/my-page.html`

   Essa conversão está de acordo com a prática recomendada de manter os URLs o mais curtos possível.

1. **Mapeamento da saída de URL nas páginas**

   Depois de definir os mapeamentos no Apache Sling Resource Resolver, use esses mapeamentos em seus componentes para garantir que os URLs enviados nas páginas sejam curtos e organizados. Você pode fazer essa manutenção usando a função de mapa do `ResourceResolver`.

   Por exemplo, se estava implementando um componente de navegação personalizado que lista os filhos da página atual, pode usar o método de mapeamento da seguinte maneira:

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server mod_rewrite {#apache-http-server-mod-rewrite}

Até o momento, você implementou mapeamentos juntamente com a lógica nos componentes para usar esses mapeamentos ao enviar URLs para páginas.

A peça final do quebra-cabeça é lidar com estes URLs mais curtos quando eles chegam ao Dispatcher, que é onde o `mod_rewrite` entra em cena. O maior benefício de usar o `mod_rewrite` é que os URLs são mapeados de volta na sua forma longa *antes* de serem enviados ao módulo do Dispatcher. Esse fluxo significa que o Dispatcher solicita o URL longo do servidor de publicação e o armazena em cache de acordo. Portanto, todas as solicitações de liberação do Dispatcher que chegarem do servidor de publicação poderão invalidar esse conteúdo com êxito.

Para implementar essas regras, você pode adicionar elementos `RewriteRule` no host virtual na configuração do Apache HTTP Server. Se quiser expandir os URLs encurtados do exemplo anterior, você pode implementar uma regra que se pareça com esta:

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### Tags de URL canônicas {#canonical-url-tags}

As tags de URL canônicas são tags de link colocadas no cabeçalho de um documento HTML para esclarecer como os mecanismos de pesquisa devem tratar uma página enquanto indexam o conteúdo. A vantagem que oferecem é garantir que versões diferentes de uma página sejam indexadas como uma única versão, mesmo que o URL da página contenha diferenças.

Por exemplo, se um site oferecesse uma versão de uma página adaptada para impressoras, um mecanismo de pesquisa potencialmente indexaria essa página separadamente da versão normal da página. A tag canônica informará ao mecanismo de pesquisa que elas são a mesma página.

Exemplos:

* `https://www.mydomain.com/my-brand/my-page.html`
* `https://www.mydomain.com/my-brand/my-page.print.html`

Ambos aplicariam a seguinte tag ao cabeçalho da página:

```xml
<link rel="canonical" href="my-brand/my-page.html"/>
```

O `href` pode ser relativo ou absoluto. O código deve ser incluído na marcação da página para determinar o URL canônico da página e exibir essa tag.

### Configurar o Dispatcher para não diferenciar maiúsculas e minúsculas {#configuring-the-dispatcher-for-case-insensitivity}

A prática recomendada é distribuir todas as páginas usando letras minúsculas. No entanto, você não quer que um usuário tenha um 404 ao acessar o site usando letras maiúsculas no URL. Por esse motivo, a Adobe recomenda adicionar uma regra de regravação na configuração do Apache HTTP Server para mapear todos os URLs recebidos em minúsculas. Além disso, os autores de conteúdo devem ser orientados a criar suas páginas com nomes em minúsculas.

Para configurar o Apache para forçar todo o tráfego de entrada em letras minúsculas, adicione o seguinte à configuração `vhost`:

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

Além disso, adicione o seguinte à parte superior do arquivo `htaccess`:

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### Implementar o robots.txt para proteger ambientes de desenvolvimento {#implementing-robots-txt-to-protect-development-environments}

Os mecanismos de pesquisa *devem* verificar a presença de um arquivo `robots.txt` na raiz do site antes de rastrear o site. Embora os principais mecanismos de pesquisa, como Google, Yahoo ou Bing, respeitem esse arquivo, alguns mecanismos de pesquisa estrangeiros não respeitam.

A maneira mais simples de bloquear o acesso a todo o site é colocar um arquivo chamado `robots.txt` na raiz do site com o seguinte conteúdo:

```xml
User-agent: *
Disallow: /
```

Como alternativa, em um ambiente em tempo real, você pode optar por não permitir determinados caminhos que não deseja indexar.

A advertência ao colocar a variável `robots.txt` na raiz do site é que as solicitações de liberação do Dispatcher podem apagar este arquivo. Além disso, os mapeamentos de URL provavelmente colocam a raiz do site em um local diferente do `DOCROOT` conforme definido na configuração do Apache HTTP Server. Por isso, é comum colocar esse arquivo na instância do autor na raiz do site e replicá-lo na instância de publicação.

### Criar um mapa de site XML no AEM {#building-an-xml-sitemap-on-aem}

Os rastreadores usam mapas de site XML para entender melhor a estrutura dos sites. Embora não haja garantias de que a disponibilização de um mapa de site levará a melhores classificações de SEO, trata-se de uma prática recomendada conhecida. Você pode manter manualmente um arquivo XML no servidor da Web para usar como mapa do site. No entanto, a Adobe recomenda gerar o mapa de site de forma programática para garantir que, à medida que os autores criam conteúdo, o mapa de site reflita automaticamente suas alterações.

O AEM usa o [módulo Apache Sling Sitemap](https://github.com/apache/sling-org-apache-sling-sitemap) para gerar mapas de site XML, o que fornece uma grande variedade de opções para desenvolvedores e editores manterem um mapa de site XML atualizado.

>[!NOTE]
>
>Disponível como recurso do produto desde a versão 6.5.11.0 do Adobe Experience Manager.
> 
>Para versões mais antigas, você mesmo pode registrar um Sling Servlet para ouvir um `sitemap.xml` chame. Use o recurso fornecido por meio da API de servlet para procurar a página atual e seus descendentes para gerar uma `sitemap.xml` arquivo.

O módulo Apache Sling Sitemap distingue entre um mapa de site de nível superior e um mapa de site aninhado, ambos sendo gerados para qualquer recurso que tenha a propriedade `sling:sitemapRoot` definida como `true`. Em geral, os mapas de site são renderizados usando seletores no caminho do mapa de site de nível superior da árvore, recurso este que não possui outro ancestral raiz do mapa de site. Essa raiz do mapa de site de nível superior também expõe o índice do mapa de site, que normalmente é o que um proprietário de site configuraria no portal de configuração do mecanismo de pesquisa ou adicionaria ao `robots.txt` do site.

Por exemplo, considere um site que define uma raiz de mapa de site de nível superior em `my-page` e uma raiz de mapa de site aninhada em `my-page/news`, para gerar um mapa de site dedicado para páginas na subárvore de notícias. Os URLs relevantes resultantes seriam

* `https://www.mydomain.com/my-brand/my-page.sitemap-index.xml`
* `https://www.mydomain.com/my-brand/my-page.sitemap.xml`
* `https://www.mydomain.com/my-brand/my-page.sitemap.news-sitemap.html`

>[!NOTE]
>
>Os seletores `sitemap` e `sitemap-index` podem interferir em implementações personalizadas. Se não quiser usar o recurso do produto, configure seu próprio servlet que serve esses seletores com um `service.ranking` maior que 0.

Na configuração padrão, a caixa de diálogo Propriedades da página fornece uma opção para marcar uma página como uma raiz do mapa de site e, portanto, conforme descrito acima, gerar um mapa de site próprio e seus descendentes. Esse comportamento é implementado pelas implementações da interface `SitemapGenerator` e pode ser estendido adicionando implementações alternativas. No entanto, como a frequência na qual os mapas de site XML são regenerados depende dos fluxos de trabalho e cargas de trabalho de criação de conteúdo, o produto não envia nenhum `SitemapScheduler` configuração. Dessa forma, o recurso é efetivamente aceito.

Para habilitar o processo em segundo plano que gera os mapas de site XML, um `SitemapScheduler` precisa ser configurado. Para fazer isso, crie uma configuração OSGI para o PID `org.apache.sling.sitemap.impl.SitemapScheduler`. A expressão do scheduler `0 0 0 * * ?` pode ser usada como ponto de partida para regenerar todos os mapas de site XML uma vez por dia, à meia-noite.

![Apache Sling Sitemap - Scheduler](assets/sling-sitemap-scheduler.png)

O trabalho de geração de mapa de site pode ser executado em instâncias de nível do autor e de publicação. Normalmente, é recomendável executar a geração em instâncias do nível de publicação, já que URLs canônicos adequados podem ser gerados somente lá (devido às regras de Mapeamento de recursos do Sling que geralmente estão presentes apenas em instâncias do nível de publicação). No entanto, é possível conectar uma implementação personalizada do mecanismo de externalização usado para gerar os URLs canônicos. Isso é feito implementando o [SitemapLinkExternalizer](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/externalizer/SitemapLinkExternalizer.html) interface. Se uma implementação personalizada puder gerar os URLs canônicos de um mapa de site nas instâncias do nível do autor, a variável `SitemapScheduler` pode ser configurado para o modo de execução do autor. E a carga de trabalho de geração do mapa de site XML pode ser distribuída entre as instâncias do cluster de serviços do autor. Nesse cenário, deve-se ter cuidado ao manipular conteúdo que ainda não foi publicado, foi modificado ou está visível apenas para um grupo restrito de usuários.

O AEM Sites contém uma implementação padrão de um `SitemapGenerator` que atravessa uma árvore de páginas para gerar um mapa de site. Ela é pré-configurada para produzir apenas os URLs canônicos de um site e qualquer alternativa de idioma que estiver disponível. Ela também pode ser configurada para incluir a data da última modificação de uma página, se necessário. Para fazer isso, ative a variável _Adicionar última modificação_ opção do _Adobe AEM SEO - Gerador de mapas do site da árvore de páginas_ Configuração e selecione um _Última Origem Modificada_. Quando os mapas do site são gerados no nível de publicação, é recomendável usar a data `cq:lastModified`.

![Configuração do Adobe AEM SEO - Gerador de mapas do site da árvore de páginas](assets/sling-sitemap-pagetreegenerator.png)

Para limitar o conteúdo de um mapa do site, as seguintes interfaces de serviço podem ser implementadas quando necessário:

* a [SitemapPageFilter](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/sitemap/SitemapPageFilter.html) pode ser implementada para ocultar páginas de mapas de site XML criadas pelo gerador de mapas do site específico do AEM Sites
* a [SitemapProductFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapProductFilter.html) ou [SitemapCategoryFilter](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/sitemap/SitemapCategoryFilter.html) pode ser implementada para filtrar produtos ou categorias de mapas de site XML produzidos pelos geradores de mapas de site específicos das [Estruturas de integração de comércio](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/home.html?lang=pt-BR)

Se as implementações padrão não funcionarem em um caso de uso específico ou se os pontos de extensão não forem flexíveis o suficiente, implemente uma `SitemapGenerator` para assumir o controle total do conteúdo de um mapa de site gerado. O exemplo a seguir usa a lógica de implementação padrão para o AEM Sites. Ele usa [ResourceTreeSitemapGenerator](https://javadoc.io/doc/org.apache.sling/org.apache.sling.sitemap/latest/org/apache/sling/sitemap/spi/generator/ResourceTreeSitemapGenerator.html) como ponto de partida para percorrer uma árvore de páginas:

```
import java.util.Optional;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.sitemap.SitemapException;
import org.apache.sling.sitemap.builder.Sitemap;
import org.apache.sling.sitemap.builder.Url;
import org.apache.sling.sitemap.spi.common.SitemapLinkExternalizer;
import org.apache.sling.sitemap.spi.generator.ResourceTreeSitemapGenerator;
import org.apache.sling.sitemap.spi.generator.SitemapGenerator;
import org.jetbrains.annotations.NotNull;
import org.osgi.service.component.annotations.Component;
import org.osgi.service.component.annotations.Reference;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.aem.wcm.seo.sitemap.PageTreeSitemapGenerator;
import com.day.cq.wcm.api.Page;

@Component(
    service = SitemapGenerator.class,
    property = { "service.ranking:Integer=20" }
)
public class SitemapGeneratorImpl extends ResourceTreeSitemapGenerator {

    private static final Logger LOG = LoggerFactory.getLogger(SitemapGeneratorImpl.class);

    @Reference
    private SitemapLinkExternalizer externalizer;
    @Reference
    private PageTreeSitemapGenerator defaultGenerator;

    @Override
    protected void addResource(@NotNull String name, @NotNull Sitemap sitemap, Resource resource) throws SitemapException {
        Page page = resource.adaptTo(Page.class);
        if (page == null) {
            LOG.debug("Skipping resource at {}: not a page", resource.getPath());
            return;
        }
        String location = externalizer.externalize(resource);
        Url url = sitemap.addUrl(location + ".html");
        // add any additional content to the Url like lastmod, change frequency, etc
    }

    @Override
    protected final boolean shouldFollow(@NotNull Resource resource) {
        return super.shouldFollow(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldFollow).orElse(Boolean.TRUE);
    }

    private boolean shouldFollow(Page page) {
        // add additional conditions to stop traversing some pages
        return !defaultGenerator.isProtected(page);
    }

    @Override
    protected final boolean shouldInclude(@NotNull Resource resource) {
        return super.shouldInclude(resource)
            && Optional.ofNullable(resource.adaptTo(Page.class)).map(this::shouldInclude).orElse(Boolean.FALSE);
    }

    private boolean shouldInclude(Page page) {
        // add additional conditions to stop including some pages
        return defaultGenerator.isPublished(page)
            && !defaultGenerator.isNoIndex(page)
            && !defaultGenerator.isRedirect(page)
            && !defaultGenerator.isProtected(page);
    }
}
```

Além disso, a funcionalidade implementada para mapas de site XML também pode ser usada para casos de uso diferentes, por exemplo, para adicionar o link canônico ou o idioma alternativo ao cabeçalho de uma página. Consulte [SeoTags](https://javadoc.io/doc/com.adobe.cq.wcm/com.adobe.aem.wcm.seo/latest/com/adobe/aem/wcm/seo/SeoTags.html) para obter mais informações.

### Criar redirecionamentos 301 para URLs herdados {#creating-redirects-for-legacy-urls}

Ao iniciar um site com uma nova estrutura, é importante implementar e testar os redirecionamentos 301 no Apache HTTP Server por dois motivos:

* Os URLs herdados acumularam o valor SEO ao longo do tempo. Ao implementar um redirecionamento, o mecanismo de pesquisa pode aplicar esse valor ao novo URL.
* Os usuários do site podem ter criado marcadores nessas páginas. Ao implementar redirecionamentos, você pode direcionar o usuário para a página no novo site que melhor corresponde ao local em que ele estava tentando acessar no site antigo.

Verifique a seção de recursos adicionais a seguir para obter instruções sobre como implementar redirecionamentos 301 e uma ferramenta para testar se seus redirecionamentos estão funcionando conforme o esperado.

## Recursos adicionais {#additional-resources}

Para obter mais informações, consulte os seguintes recursos adicionais:

* [Mapeamento de recursos](/help/sites-deploying/resource-mapping.md)
* [https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url](https://moz.com/blog/seo-cheat-sheet-anatomy-of-a-url)
* [https://moz.com/blog/15-seo-best-practices-for-structuring-urls](https://moz.com/blog/15-seo-best-practices-for-structuring-urls)
* [https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/](https://mysiteauditor.com/blog/top-10-most-important-seo-tips-for-url-optimization/)
* [https://sling.apache.org/documentation/the-sling-engine/servlets.html](https://sling.apache.org/documentation/the-sling-engine/servlets.html)
* [https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
* [https://httpd.apache.org/docs/current/mod/mod_rewrite.html](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)
* [https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps](https://moz.com/blog/canonical-url-tag-the-most-important-advancement-in-seo-practices-since-sitemaps)
* [https://www.robotstxt.org/robotstxt.html](https://www.robotstxt.org/robotstxt.html)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)
