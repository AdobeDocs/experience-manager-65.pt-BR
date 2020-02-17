---
title: Sobreposições
seo-title: Sobreposições
description: O AEM usa o princípio de sobreposições para permitir que você estenda e personalize os consoles e outras funcionalidades
seo-description: O AEM usa o princípio de sobreposições para permitir que você estenda e personalize os consoles e outras funcionalidades
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Sobreposições{#overlays}

O AEM (e antes disso, o CQ) há muito tempo usa o princípio de sobreposições para permitir estender e personalizar os [consoles](/help/sites-developing/customizing-consoles-touch.md) e outras funcionalidades (por exemplo, criação [de](/help/sites-developing/customizing-page-authoring-touch.md)página).

Sobreposição é um termo que pode ser usado em muitos contextos. Neste contexto (estender o AEM), uma sobreposição significa usar a funcionalidade predefinida e impor suas próprias definições sobre isso (para personalizar a funcionalidade padrão).

Em uma instância padrão, a funcionalidade predefinida é mantida em `/libs` e é recomendável definir sua sobreposição (personalizações) na `/apps` ramificação. O AEM usa um caminho de pesquisa para localizar um recurso, pesquisando primeiro a `/apps` ramificação e, em seguida, a `/libs` ramificação (o caminho [de pesquisa pode ser configurado](#configuring-the-search-paths)). Esse mecanismo significa que sua sobreposição (e as personalizações definidas ali) terão prioridade.

Desde o AEM 6.0, alterações foram feitas em como as sobreposições são implementadas e usadas:

* A partir do AEM 6.0 - para sobreposições relacionadas ao [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)(ou seja, a interface habilitada para toque)

   * Método

      * Reconstrua a `/libs` estrutura apropriada em `/apps`.

         Isso não requer uma cópia 1:1, a Fusão [de recursos de](/help/sites-developing/sling-resource-merger.md) Sling é usada para fazer referência cruzada às definições originais necessárias. A fusão Sling Resource presta serviços de acesso e fusão de recursos através de mecanismos de diferenciação (diferenciação).

      * Faça quaisquer alterações em `/apps`.
   * Vantagens

      * Mais robusto para as alterações apresentadas em `/libs`.
      * Apenas redefina o que é realmente necessário.


* Sobreposições não granitas e sobreposições anteriores ao AEM 6.0

   * Método

      * Copiar o conteúdo de `/libs` para `/apps`

         É necessário copiar a subramificação inteira, incluindo as propriedades.

      * Faça quaisquer alterações em `/apps`.
   * Desvantagens

      * Embora suas alterações não sejam perdidas quando algo mudar em `/libs`, talvez seja necessário recriar determinadas alterações que ocorrem na sobreposição em `/apps`.


>[!CAUTION]
>
>A Fusão [de Recursos de](/help/sites-developing/sling-resource-merger.md) Sling e os métodos relacionados só podem ser utilizados com [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Isso significa que a criação de uma sobreposição com uma estrutura de esqueleto é apropriada apenas para a interface de usuário padrão habilitada para toque.
>
>As sobreposições para outras áreas (incluindo a interface clássica) envolvem a cópia do nó e da subestrutura inteira apropriados e, em seguida, as alterações necessárias.

As sobreposições são o método recomendado para muitas alterações, como [configurar seus consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) ou [criar sua categoria de seleção para o navegador de ativos no painel](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) lateral (usado ao criar páginas). São exigidos como:

* Você não ****deve fazer alterações na`/libs`ramificação **Qualquer alteração feita pode ser perdida, pois essa ramificação está sujeita a alterações sempre que você:

   * atualização em sua instância
   * aplicar uma correção
   * instalar um pacote de recursos

* Eles concentram suas alterações em um local; tornando mais fácil para você rastrear, migrar, fazer backup e/ou depurar as alterações conforme necessário.

## Configuração dos caminhos de pesquisa {#configuring-the-search-paths}

Para sobreposições, o recurso fornecido é um agregado dos recursos e propriedades recuperados, dependendo dos caminhos de pesquisa que podem ser definidos:

* O Caminho **de pesquisa do** Resolvedor de recursos, conforme definido na configuração [do](/help/sites-deploying/configuring-osgi.md) OSGi para a Fábrica **do Resolvedor de Recursos do Sling do** Apache.

   * A ordem de cima para baixo dos caminhos de pesquisa indica suas respectivas prioridades.
   * Em uma instalação padrão, os padrões principais são `/apps`, `/libs` - portanto, o conteúdo de `/apps` tem uma prioridade mais alta do que o de `/libs` (isto é, ele *sobrepõe* -o).

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

