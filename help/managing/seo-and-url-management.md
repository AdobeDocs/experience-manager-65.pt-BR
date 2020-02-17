---
title: Práticas recomendadas de gerenciamento de SEO e URL
seo-title: Práticas recomendadas de gerenciamento de SEO e URL
description: Saiba mais sobre as práticas recomendadas e recomendações de SEO para atingi-las em uma implementação do AEM.
seo-description: Saiba mais sobre as práticas recomendadas e recomendações de SEO para atingi-las em uma implementação do AEM.
uuid: 943e76c4-bd88-4b52-bb43-db375eb89d23
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing
content-type: reference
discoiquuid: 7c8f2cec-870b-41a8-8d98-70e29b495587
docset: aem65
translation-type: tm+mt
source-git-commit: c623724df8d849f4cc01f5dc134c775dc24dafc7

---


# Práticas recomendadas de gerenciamento de SEO e URL{#seo-and-url-management-best-practices}

A Otimização do Mecanismo de Pesquisa (SEO) se tornou uma preocupação chave para muitos comerciantes. Como resultado, as preocupações com o SEO precisam ser abordadas em muitos projetos do AEM.

Primeiro, este documento descreve algumas práticas [recomendadas de](#seo-best-practices) SEO e recomendações para realizá-las em uma implementação do AEM. Em seguida, este documento aprofunda algumas das etapas [de implementação mais](#aem-configurations) complexas abordadas na primeira seção.

## Práticas recomendadas do SEO {#seo-best-practices}

Esta seção descreve algumas práticas recomendadas gerais de SEO.

### URLs {#urls}

Há algumas práticas recomendadas geralmente aceitas quando se trata de URLs.

Em seu projeto do AEM, ao avaliar seus URLs, faça o seguinte:

&quot;Se um usuário visse esse URL e nenhum conteúdo na página, ele poderia descrever o que era essa página?&quot;

Se a resposta for sim, então é provável que o URL funcione bem para um mecanismo de pesquisa.

Estas são algumas dicas gerais sobre como criar seus URLs para SEO:

* Use hífens para separar palavras.

   * Nomear páginas usando hífens (-) como separadores.
   * Evite usar caixa de camelo, sublinhados e espaços.

* Evite o uso de parâmetros de consulta quando possível. Quando necessário, limite-os a dois ou menos.

   * Use a estrutura de diretório para indicar a arquitetura de informações, quando disponível.
   * Se uma estrutura de diretório não for uma opção, use seletores Sling no URL em vez de sequências de caracteres de consulta. Além do valor SEO que eles fornecem, os seletores de rolagem também tornarão as páginas acessíveis para o dispatcher.

* Quanto mais um URL legível por humanos, melhor; ter palavras-chave presentes no URL aumentará o valor.

   * Ao usar seletores em uma página, os seletores que fornecem valor semântico são preferenciais.
   * Se um humano não conseguir ler seu URL, um mecanismo de pesquisa também não poderá.
   * Por exemplo:
      `mybrand.com/products/product-detail.product-category.product-name.html`
é preferido a `mybrand.com/products/product-detail.1234.html`

* Evite subdomínios sempre que possível, já que os mecanismos de pesquisa os tratarão como entidades diferentes, fragmentando o valor SEO do site.

   * Em vez disso, use subcaminhos de primeiro nível. Por exemplo, em vez de `es.mybrand.com/home.html`, use `www.mybrand.com/es/home.html`.

   * Planeje sua hierarquia de conteúdo para corresponder à forma como o conteúdo será apresentado, de acordo com esta diretriz.

* A eficácia da palavra-chave em URLs diminui conforme a duração do URL e a posição da palavra-chave aumenta. Em outras palavras, menor é melhor.

   * Use técnicas e recursos de redução de URL fornecidos pelo AEM para remover partes desnecessárias do URL.
   * Por exemplo, `mybrand.com/en/myPage.html` é preferido a `mybrand.com/content/my-brand/en/myPage.html`.

* Use URLs canônicos.

   * Quando um URL puder ser servido a partir de caminhos diferentes ou com parâmetros ou seletores diferentes, certifique-se de usar uma `rel=canonical` tag na página.

   * Isso pode ser incluído no código do modelo AEM.

* Corresponder URLs a títulos de página sempre que possível.

   * Os autores de conteúdo devem ser encorajados a seguir essa prática.

* Insensibilidade a maiúsculas e minúsculas em solicitações de URL.

   * Configure o dispatcher para reescrever todas as solicitações de entrada como letras minúsculas.
   * Treinar autores de conteúdo para criar todas as páginas usando letras minúsculas.

* Certifique-se de que cada página seja servida somente de um protocolo.

   * Às vezes, os sites serão veiculados `http` até que um usuário chegue a uma página com, por exemplo, um formulário de check-out ou login, no qual ele muda para `https`. Ao criar links a partir dessa página, se o usuário puder retornar às `http` páginas e acessá-las por meio `https`, o mecanismo de pesquisa as rastreará como duas páginas separadas.

   * Atualmente, o Google prefere `https` páginas a `http` páginas. Por isso, muitas vezes torna a vida de todos mais fácil de servir todo o site `https`.

### Server configuration {#server-configuration}

Em termos de configuração do servidor, você pode executar as seguintes etapas para garantir que somente o conteúdo correto esteja sendo rastreado:

* Use um `robots.txt` arquivo para bloquear o rastreamento de qualquer conteúdo que não deve ser indexado.

   * Bloquear **todos** os rastreamentos em ambientes de teste.

* Ao iniciar um novo site com URLs atualizados, implemente os redirecionamentos 301 para garantir que sua classificação de SEO existente não seja perdida.
* Inclua um favicon para seu site.
* Implemente um mapa do site XML para facilitar o rastreamento do conteúdo pelos mecanismos de pesquisa. Certifique-se de incluir um mapa do site móvel para sites móveis e/ou responsivos.

## AEM Configurations {#aem-configurations}

Esta seção descreve as etapas de implementação necessárias para configurar o AEM para seguir essas recomendações de SEO.

### Uso dos seletores Sling {#using-sling-selectors}

Anteriormente, o uso de parâmetros de consulta era a prática geralmente aceita ao criar um aplicativo Web corporativo.

A tendência nos últimos anos tem sido removê-los em um esforço para tornar os URLs mais legíveis. Em várias plataformas, isso envolve a implementação de redirecionamentos no servidor da Web ou na Rede de entrega de conteúdo (CDN), mas o Sling torna isso simples. Seletores Sling:

* Melhore a legibilidade do URL.
* Permitem que você armazene suas páginas em cache no dispatcher e geralmente melhoram a segurança.
* Permita que você aborde o conteúdo diretamente, em vez de ter um servlet genérico que recupera o conteúdo. Isso concede os benefícios das ACLs que você aplica ao seu repositório e aos filtros que você aplica ao dispatcher.

#### Uso de seletores para servlets {#using-selectors-for-servlets}

O AEM nos fornece duas opções ao gravar servlets:

* **servlets bin**
* **Servlets Sling**

Os exemplos a seguir ilustram como registrar servlets que seguem ambos os padrões, bem como o benefício ganho com o uso de servlets Sling.

#### Servlets de compartimento (um nível para baixo) {#bin-servlets-one-level-down}

**Servlets Bin** seguem o padrão para o qual muitos desenvolvedores são usados na programação J2EE. O servlet é registrado em um caminho específico, que no caso do AEM normalmente está sob `/bin`, e você extrai os parâmetros de solicitação necessários da string de consulta.

A anotação SCR para este tipo de servlet seria algo como isto:

```
@SlingServlet(paths = "/bin/myApp/myServlet", extensions = "json", methods = "GET")
```

Em seguida, você extrai os parâmetros da string de consulta pelo `SlingHttpServletRequest` objeto incluído no `doGet` método; por exemplo:

```
String myParam = req.getParameter("myParam");
```

O URL resultante usado seria semelhante a:

`https://www.mydomain.com/bin/myApp/myServlet.json?myParam=myValue`

Há alguns pontos a considerar com esta abordagem:

* O próprio URL perde o valor SEO. Os usuários que acessam o site, incluindo mecanismos de pesquisa, não recebem nenhum valor semântico do URL, pois o URL representa um caminho programático e não a hierarquia de conteúdo.
* A presença de parâmetros de consulta no URL significa que o dispatcher não poderá armazenar a resposta em cache.
* Se quiser proteger este servlet, você precisa implementar sua própria lógica de segurança personalizada no servlet.
* O expedidor deve ser configurado (com cuidado) para expor `/bin/myApp/myServlet`. A exposição simples `/bin` permitiria o acesso a determinados servlets que não deveriam ser abertos aos visitantes do site.

#### Servlets Sling (um nível para baixo) {#sling-servlets-one-level-down}

**Os servlets Sling** permitem que você registre seu servlet da maneira oposta. Em vez de endereçar um servlet e especificar o conteúdo que você gostaria que o servlet renderizasse com base nos parâmetros de consulta, você endereçaria o conteúdo que deseja e especificaria o servlet que deve renderizar o conteúdo com base nos seletores Sling.

A anotação SCR para este tipo de servlet seria algo como isto:

```
@SlingServlet(resourceTypes = "myBrand/components/pages/myPageType", selectors = "myRenderer", extensions = "json”, methods=”GET”)
```

Nesse caso, o recurso que o URL endereça (uma instância do `myPageType` recurso) é acessível automaticamente no servlet. Para acessá-lo, você chama:

```
Resource myPage = req.getResource();
```

O URL resultante usado seria semelhante a:

`https://www.mydomain.com/content/my-brand/my-page.myRenderer.json`

Os benefícios desta abordagem são:

* Você pode fazer o backup do valor SEO, obtido pela semântica presente na hierarquia do site e no nome da página.
* Como nenhum parâmetro de consulta está presente, o dispatcher pode armazenar a resposta em cache. Além disso, quaisquer atualizações feitas na página endereçada invalidarão esse cache quando a página for ativada.
* Todas as ACLs aplicadas a `/content/my-brand/my-page` entrarão em vigor quando um usuário tentar acessar este servlet.
* O dispatcher já estará configurado para servir esse conteúdo como uma função de servir ao site. Nenhuma configuração adicional é necessária.

### regravação de URL {#url-rewriting}

No AEM, todas as suas páginas da Web são armazenadas em `/content/my-brand/my-content`. Embora isso possa ser útil na perspectiva do gerenciamento de dados do repositório, não é necessariamente a forma como você deseja que seus clientes vejam seu site e pode entrar em conflito com a orientação do SEO para manter os URLs o mais curtos possível. Além disso, você pode estar disponibilizando vários sites da mesma instância do AEM e de nomes de domínio diferentes.

Esta seção analisa as opções disponíveis no AEM para gerenciar esses URLs e apresentá-los aos usuários de maneira mais legível e fácil de usar para SEO.

#### URLs personalizadas {#vanity-urls}

Se um autor desejar que uma página seja acessível de um segundo local para fins promocionais, os URLs personalizados do AEM, definidos página por página, podem ser úteis. Para adicionar um URL personalizado para uma página, navegue até ele no console **Sites** e edite as propriedades da página. Na parte inferior da guia **Básico** , você verá uma seção na qual URLs personalizados podem ser adicionados. Lembre-se de que ter a página acessível por mais de um URL fragmentará o valor SEO da página, portanto, uma tag de URL canônica deve ser adicionada à página para evitar esse problema.

#### Nomes de página localizados {#localized-page-names}

Você pode exibir nomes de página localizados para usuários de conteúdo traduzido. Por exemplo:

* Em vez de ter um usuário de língua espanhola, navegue até:
   `www.mydomain.com/es/home.html`

* Seria melhor para o URL ser:
   `www.mydomain.com/es/casa.html`.

O desafio de localizar o nome da página é que muitas das ferramentas de localização disponíveis na plataforma AEM dependem de que os nomes das páginas correspondam às localidades para manter o conteúdo sincronizado.

A `sling:alias` propriedade permite que você coma nosso bolo também. `sling:alias` pode ser adicionada como uma propriedade a qualquer recurso para permitir um nome de alias para o recurso. No exemplo anterior, você teria:

* Uma página no JCR em:
   `…/es/home`

* Em seguida, adicione uma propriedade a ela:
   `sling:alias` = `casa`

Isso permitiria que as ferramentas de tradução do AEM, como o gerente de vários sites, continuassem a manter uma relação entre:

* `/en/home`

* `/es/home`

Ao mesmo tempo, permite que os usuários finais interajam com o nome da página em seus idiomas nativos.

>[!NOTE]
>
>A `sling:alias` propriedade pode ser definida usando a propriedade [Alias ao editar Propriedades](/help/sites-authoring/editing-page-properties.md#advanced)da página.

#### /etc/map {#etc-map}

Em uma instalação padrão do AEM:

* para a configuração do OSGi
   **Apache Sling Resource Resolver Fatory**( `org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl`)

* a propriedade
   **Localização** de mapeamento ( `resource.resolver.map.location`)

* defaults to `/etc/map`.

As definições de mapeamento podem ser adicionadas neste local para mapear solicitações de entrada, regravar URLs em páginas no AEM ou em ambos.

Para criar um novo mapeamento, crie um novo `sling:Mapping` nó neste local em `/http` ou `/https`. Com base nas `sling:match` e `sling:internalRedirect` propriedades definidas neste nó, o AEM redirecionará todo o tráfego do URL correspondente para o valor especificado na `internalRedirect` propriedade.

Embora essa seja a abordagem documentada na documentação oficial do AEM e Sling, o suporte à expressão regular fornecido por essa implementação é limitado no escopo quando comparado às opções que estão disponíveis usando o recurso `SlingResourceResolver` diretamente. Além disso, a implementação de mapeamentos dessa maneira pode levar a problemas com a invalidação do cache do dispatcher.

Este é um exemplo de como esse problema ocorre:

1. Um usuário visita seu site e solicita `https://www.mydomain.com/my-page.html`
1. O dispatcher encaminha essa solicitação para o servidor de publicação.
1. Usando `/etc/map`, o servidor de publicação resolve essa solicitação para `/content/my-brand/my-page` e renderiza a página.

1. O dispatcher armazena a resposta em cache `/my-page.html` e retorna a resposta ao usuário.
1. Um autor de conteúdo faz uma alteração nesta página e a ativa.
1. O agente de despachante envia uma solicitação de invalidação para `/content/my-brand/my-page`**.**Como o dispatcher não tem uma página em cache nesse caminho, o conteúdo antigo permanece em cache e será obsoleto.

Há maneiras de configurar regras de despachamento personalizadas que mapeiam o URL mais curto para o URL mais longo para fins de invalidação de cache.

No entanto, há também uma maneira mais simples de gerenciar isso:

1. **Regras SlingResourceResolver**

   Usando o console da Web (por exemplo, localhost:4502/system/console/configMgr), você pode configurar o Sling Resource Resolver:

   * **Apache Sling Resource Resolver Fatory**
      `(org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl)`.
   É recomendável que você crie os mapeamentos necessários para encurtar URLs como expressões regulares e, em seguida, defina essas configurações em um nó OsgiConfig, `config.publish`, incluído na sua compilação.

   Em vez de definir seus mapeamentos no, eles podem ser atribuídos diretamente à propriedade Mapeamentos `/etc/map`de **URL (** `resource.resolver.mapping`):

   ```xml
   resource.resolver.mapping="[/content/my-brand/(.*)</$1]"
   ```

   Neste exemplo simples, você está removendo `/content/my-brand/` do início de qualquer URL em que ele esteja presente.

   Isso converteria um URL:

   * from `/content/my-brand/my-page.html`
   * para just `/my-page.html`
   Isso está de acordo com a prática recomendada de manter os URLs o mais curtos possível.

1. **Mapeamento da saída de URL nas páginas**

   Depois de definir seus mapeamentos no Apache Sling Resource Resolver, é necessário usar esses mapeamentos em seus componentes para garantir que os URLs enviados em suas páginas sejam curtos e arrumados. Você pode fazer isso usando a função de mapa do `ResourceResolver`.

   Por exemplo, se você estava implementando um componente de navegação personalizado que lista os filhos da página atual, você pode usar o método de mapeamento como:

   ```
   for (Page child : children) {
     String childUrl = resourceResolver.map(request, child.getPath());
     //Output the childUrl on the page here
   }
   ```

#### Apache HTTP Server mod_rewrite {#apache-http-server-mod-rewrite}

Até agora, você implementou mapeamentos juntamente com a lógica em seus componentes para usar esses mapeamentos ao enviar URLs para nossas páginas.

A peça final do quebra-cabeça é lidar com esses URLs encurtados quando eles chegam ao despachante, que é onde `mod_rewrite` entram em cena. O maior benefício a ser usado `mod_rewrite` é que os URLs são mapeados de volta ao formulário longo *antes* de serem enviados ao módulo do dispatcher. Isso significa que o dispatcher solicitará o URL longo do servidor de publicação e o armazenará em cache de acordo. Portanto, todas as solicitações de despacho que chegarem do servidor de publicação poderão invalidar esse conteúdo com êxito.

Para implementar essas regras, você pode adicionar `RewriteRule` elementos sob seu host virtual na configuração do Apache HTTP Server. Se quiser expandir os URLs encurtados do exemplo anterior, você pode implementar uma regra que se pareça com esta:

```
<VirtualHost *:80>
  ServerName www.mydomain.com
  RewriteEngine on
  RewriteRule ^/(.*)$ /content/my-brand/$1 [PT,L]
  …
</VirtualHost>
```

### Tags de URL canônicas {#canonical-url-tags}

As tags canônicas de URL são tags de link colocadas no cabeçalho de um documento HTML para esclarecer como os mecanismos de pesquisa devem tratar uma página enquanto indexam o conteúdo. A vantagem que eles oferecem é garantir que (versões diferentes de) uma página seja indexada da mesma maneira, mesmo quando o URL da página possa conter diferenças.

Por exemplo, se um site oferecesse uma versão de uma página compatível com a impressora, um mecanismo de pesquisa potencialmente indexaria essa página separadamente da versão normal da página. A tag canônica informará ao mecanismo de pesquisa que eles são os mesmos.

Exemplos:

* https://www.mydomain.com/my-brand/my-page.html
* https://www.mydomain.com/my-brand/my-page.print.html

Ambos aplicariam a seguinte tag ao cabeçalho da página:

```xml
<link rel=”canonical” href=”my-brand/my-page.html”/>
```

O `href` pode ser relativo ou absoluto. O código deve ser incluído na marcação da página para determinar o URL canônico da página e exibir essa tag.

### Configurar o dispatcher para não sensibilidade a maiúsculas e minúsculas {#configuring-the-dispatcher-for-case-insensitivity}

A prática recomendada é servir todas as páginas usando letras minúsculas. No entanto, você não quer que um usuário receba um 404 quando ele acessar seu site usando letras maiúsculas em seu URL. Por isso, a Adobe recomenda que você adicione uma regra de regravação na configuração do Apache HTTP Server para mapear todos os URLs recebidos para minúsculas. Além disso, os autores de conteúdo devem ser treinados para criar suas páginas com nomes em minúsculas.

Para configurar o Apache para forçar todo o tráfego de entrada a minúsculas, adicione o seguinte à `vhost` configuração:

```xml
RewriteEngine On
RewriteMap lowercase int:tolower
```

Além disso, adicione o seguinte à parte superior do `htaccess` arquivo:

```xml
RewriteCond $1 [A-Z]
RewriteRule ^(.*)$ /${lowercase:$1} [R=301,L]
```

### Implementação do robots.txt para proteger os ambientes de desenvolvimento {#implementing-robots-txt-to-protect-development-environments}

Os mecanismos de pesquisa *devem* verificar a presença de um `robots.txt` arquivo na raiz do site antes de rastrear o site. Deve ser enfatizado aqui porque enquanto grandes mecanismos de busca como Google, Yahoo, ou Bing todos respeitam isso, alguns mecanismos de busca estrangeiros não.

A maneira mais simples de bloquear o acesso a todo o site é colocar um arquivo chamado `robots.txt` na raiz do site com o seguinte conteúdo:

```xml
User-agent: *
Disallow: /
```

Como alternativa, em um ambiente ativo, você pode optar por não permitir determinados caminhos que não deseja indexar.

O problema ao colocar o `robots.txt` arquivo na raiz do site é que as solicitações de despacho flush podem apagar esse arquivo e os mapeamentos de URL provavelmente colocarão a raiz do site em um local diferente do `DOCROOT` definido na configuração do Apache HTTP Server. Por isso, é comum colocar esse arquivo na instância do autor na raiz do site e replicá-lo na instância de publicação.

### Criar um mapa do site XML no AEM {#building-an-xml-sitemap-on-aem}

Os rastreadores usam mapas do site XML para entender melhor a estrutura dos sites. Embora não haja garantias de que a disponibilização de um mapa do site conduzirá a melhores classificações de SEO, trata-se de uma prática recomendada acordada. É possível manter manualmente um arquivo XML no servidor da Web para usar como mapa do site, mas é recomendável gerar o mapa do site de forma programática, o que garante que, à medida que os autores criarem novo conteúdo, o mapa do site reflita automaticamente suas alterações.

Para gerar programaticamente um mapa do site, registre uma escuta Sling Servlet para uma `sitemap.xml` chamada. O servlet pode então usar o recurso fornecido pela API de servlet para verificar a página atual e seus filhos, criando XML. O XML será armazenado em cache no dispatcher. Esse local deve ser referenciado na propriedade sitemap do `robots.txt` arquivo. Além disso, uma regra de liberação personalizada precisará ser implementada para certificar-se de limpar esse arquivo sempre que uma nova página for ativada.

>[!NOTE]
>
>Você pode registrar um Sling Servlet para ouvir o seletor `sitemap` com a extensão `xml`. Isso fará com que o servlet processe a solicitação sempre que um URL for solicitado e terminar em:
>    `/<path-to>/page.sitemap.xml`
Você pode obter o recurso solicitado da solicitação e gerar um mapa do site a partir desse ponto na árvore de conteúdo usando as APIs JCR.
O benefício para uma abordagem como esta é quando você tem vários sites sendo servidos da mesma instância. Uma solicitação para `/content/siteA.sitemap.xml` gerar um mapa do site por `siteA` enquanto uma solicitação para `/content/siteB.sitemap.xml` geraria um mapa do site para `siteB` sem a necessidade de escrever código adicional.

### Criação de redirecionamentos 301 para URLs herdados {#creating-redirects-for-legacy-urls}

Ao iniciar um site com uma nova estrutura, implementar e testar os redirecionamentos 301 no Apache HTTP Server é importante por dois motivos:

* Os URLs herdados acumularam o valor SEO ao longo do tempo. Ao implementar um redirecionamento, o mecanismo de pesquisa pode aplicar esse valor ao novo URL.
* Os usuários do site podem ter criado marcadores nessas páginas. Ao implementar redirecionamentos, você pode direcionar o usuário para a página no novo site que melhor corresponde ao local em que ele estava tentando acessar o site antigo.

Verifique a seção de recursos adicionais a seguir para obter instruções sobre como implementar redirecionamentos 301, bem como uma ferramenta para testar se os redirecionamentos estão funcionando como esperado.

## Additional Resources {#additional-resources}

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
* [https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/](https://www.internetmarketingninjas.com/blog/search-engine-optimization/301-redirects/)
* [https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/dispatcher/redirectTester)
* [https://adobe-consulting-services.github.io/](https://adobe-consulting-services.github.io/)

