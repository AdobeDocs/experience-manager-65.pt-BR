---
title: Sobreposições
seo-title: Sobreposições
description: AEM usa o princípio de sobreposições para permitir que você estenda e personalize os consoles e outras funcionalidades
seo-description: AEM usa o princípio de sobreposições para permitir que você estenda e personalize os consoles e outras funcionalidades
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---


# Overlays{#overlays}

AEM (e antes disso, o CQ) há muito tempo usa o princípio de sobreposições para permitir que você estenda e personalize os [consoles](/help/sites-developing/customizing-consoles-touch.md) e outras funcionalidades (por exemplo, [criação de página](/help/sites-developing/customizing-page-authoring-touch.md)).

A sobreposição é um termo que pode ser usado em muitos contextos. Neste contexto (estender AEM) uma sobreposição significa usar a funcionalidade predefinida e impor suas próprias definições sobre isso (para personalizar a funcionalidade padrão).

Em uma instância padrão, a funcionalidade predefinida é mantida em `/libs` e é recomendável definir sua sobreposição (personalizações) na ramificação `/apps`. AEM usa um caminho de pesquisa para localizar um recurso, pesquisando primeiro a ramificação `/apps` e depois a ramificação `/libs` (o caminho de pesquisa [pode ser configurado](#configuring-the-search-paths)). Esse mecanismo significa que sua sobreposição (e as personalizações definidas ali) terão prioridade.

Desde o AEM 6.0, foram feitas alterações no modo como as sobreposições são implementadas e usadas:

* AEM 6.0 em diante - para sobreposições relacionadas a [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) (isto é, a interface habilitada para toque)

   * Método

      * Reconstrua a estrutura `/libs` apropriada em `/apps`.

         Isso não requer uma cópia 1:1, o [Sling Resource Fusion](/help/sites-developing/sling-resource-merger.md) é usado para fazer referência cruzada às definições originais necessárias. A fusão Sling Resource presta serviços de acesso e fusão de recursos através de mecanismos de diferenciação (diferenciação).

      * Faça quaisquer alterações em `/apps`.
   * Vantagens

      * Mais robusto às alterações em `/libs`.
      * Apenas redefina o que é realmente necessário.


* Sobreposições e sobreposições não granitas anteriores ao AEM 6.0

   * Método

      * Copie o conteúdo de `/libs` para `/apps`

         É necessário copiar a subramificação inteira, incluindo as propriedades.

      * Faça quaisquer alterações em `/apps`.
   * Desvantagens

      * Embora suas alterações não sejam perdidas quando algo mudar em `/libs`, talvez seja necessário recriar determinadas alterações que ocorrem na sobreposição em `/apps`.


>[!CAUTION]
>
>O [Sling Resource Fusion](/help/sites-developing/sling-resource-merger.md) e os métodos relacionados só podem ser utilizados com [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Isso significa que a criação de uma sobreposição com uma estrutura de esqueleto é apropriada apenas para a interface de usuário padrão habilitada para toque.
>
>As sobreposições para outras áreas (incluindo a interface clássica) envolvem a cópia do nó e da subestrutura inteira apropriados e, em seguida, as alterações necessárias.

As sobreposições são o método recomendado para muitas alterações, como [configurar seus consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) ou [criar sua categoria de seleção para o navegador de ativos no painel lateral](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (usado durante a criação de páginas). São exigidos como:

* Você ***não deve* fazer alterações na `/libs` ramificação **Quaisquer alterações feitas podem ser perdidas, pois essa ramificação está sujeita a alterações sempre que você:

   * atualização em sua instância
   * aplicar uma correção
   * instalar um pacote de recursos

* Eles concentram suas alterações em um local; tornando mais fácil para você rastrear, migrar, fazer backup e/ou depurar as alterações conforme necessário.

## Configuração dos caminhos de pesquisa {#configuring-the-search-paths}

Para sobreposições, o recurso fornecido é uma agregação dos recursos e propriedades recuperados, dependendo dos caminhos de pesquisa que podem ser definidos:

* O recurso **Resolver Search Path**, conforme definido em [Configuração OSGi](/help/sites-deploying/configuring-osgi.md) para a **Apache Sling Resource Resolver Fatory**.

   * A ordem de cima para baixo dos caminhos de pesquisa indica suas respectivas prioridades.
   * Em uma instalação padrão, os padrões primários são `/apps`, `/libs` - portanto, o conteúdo de `/apps` tem uma prioridade mais alta do que o de `/libs` (isto é, *sobreposições*).

* Dois usuários do serviço precisam de acesso JCR:READ ao local onde os scripts estão armazenados. Esses usuários são: components-search-service (usado pelos componentes com.day.cq.wcm.coreto access/cache) e sling-scripting (usado por org.apache.sling.servlets.resolver para localizar servlets).
* A configuração a seguir também deve ser configurada de acordo com o local onde você coloca seus scripts (neste exemplo, em /etc, /libs ou /apps).

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* Finalmente, o Servlet Resolver também deve ser configurado (neste exemplo, para adicionar /etc também)

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## Exemplo de uso {#example-of-usage}

Alguns exemplos são abordados quando:

* [Personalização dos consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Personalização da criação de página](/help/sites-developing/customizing-page-authoring-touch.md)

