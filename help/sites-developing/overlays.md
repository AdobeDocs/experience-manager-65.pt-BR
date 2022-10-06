---
title: Sobreposições
seo-title: Overlays
description: AEM usa o princípio de sobreposições para permitir estender e personalizar os consoles e outras funcionalidades
seo-description: AEM uses the principle of overlays to allow you to extend and customize the consoles and other functionality
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# Sobreposições{#overlays}

AEM (e antes disso, o CQ) utiliza há muito o princípio de sobreposições para permitir estender e personalizar o [consoles](/help/sites-developing/customizing-consoles-touch.md) e outras funcionalidades (por exemplo, [criação de página](/help/sites-developing/customizing-page-authoring-touch.md)).

Sobreposição é um termo que pode ser usado em muitos contextos. Neste contexto (extensão de AEM), uma sobreposição significa usar a funcionalidade predefinida e impor suas próprias definições sobre isso (para personalizar a funcionalidade padrão).

Em uma instância padrão, a funcionalidade predefinida é mantida em `/libs` e é prática recomendada definir sua sobreposição (personalizações) no `/apps` ramificação. AEM usa um caminho de pesquisa para localizar um recurso, pesquisando primeiro o `/apps` e depois a `/libs` ramificação (a [o caminho de pesquisa pode ser configurado](#configuring-the-search-paths)). Esse mecanismo significa que sua sobreposição (e as personalizações definidas lá) terá prioridade.

Desde o AEM 6.0, alterações foram feitas no modo como as sobreposições são implementadas e usadas:

* AEM 6.0 em diante - para [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)Sobreposições relacionadas (ou seja, a interface habilitada para toque)

   * Método

      * Reconstrua o `/libs` estrutura `/apps`.

         Isso não requer uma cópia 1:1, a variável [Fusão de Recursos Sling](/help/sites-developing/sling-resource-merger.md) é usada para fazer referência cruzada às definições originais necessárias. O Sling Resource Merger fornece serviços para o acesso e a fusão de recursos através de mecanismos de diferenciação (diferenciação).

      * Faça quaisquer alterações em `/apps`.
   * Vantagens

      * Mais robusto para alterações em `/libs`.
      * Apenas redefina o que é realmente necessário.


* Sobreposições e sobreposições não granulares anteriores ao AEM 6.0

   * Método

      * Copie o conteúdo de `/libs` para `/apps`

         Você precisa copiar a sub-ramificação inteira, incluindo propriedades.

      * Faça quaisquer alterações em `/apps`.
   * Desvantagens

      * Embora suas alterações não sejam perdidas quando algo for alterado em `/libs`, talvez seja necessário recriar determinadas alterações que ocorrem na sobreposição em `/apps`.


>[!CAUTION]
>
>O [Fusão de Recursos Sling](/help/sites-developing/sling-resource-merger.md) e os métodos relacionados só podem ser usados com [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Isso significa que a criação de uma sobreposição com uma estrutura de esqueleto é adequada apenas para a interface de usuário padrão habilitada para toque.
>
>As sobreposições para outras áreas (incluindo a interface clássica) envolvem a cópia do nó apropriado e de toda a subestrutura, e em seguida a realização das alterações necessárias.

As sobreposições são o método recomendado para muitas alterações, como [configurar seus consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) ou [criação da categoria de seleção no navegador de ativos no painel lateral](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (usado durante a criação de páginas). São exigidas como:

* Você ***não deve* faça alterações no `/libs` ramificação **As alterações feitas podem ser perdidas, pois essa ramificação pode ser alterada sempre que você:

   * atualizar em sua instância
   * aplicar um hotfix
   * instalar um pacote de recursos

* Eles concentram suas alterações em um local; tornando mais fácil para você rastrear, migrar, fazer backup e/ou depurar as alterações, conforme necessário.

## Configuração dos caminhos de pesquisa {#configuring-the-search-paths}

Para sobreposições, o recurso entregue é um agregado dos recursos e propriedades recuperados, dependendo dos caminhos de pesquisa que podem ser definidos:

* O recurso **Caminho de Pesquisa do Resolvedor** conforme definido no [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para **Fábrica do Resolvedor de Recursos do Apache Sling**.

   * A ordem de cima para baixo dos caminhos de pesquisa indica suas respectivas prioridades.
   * Em uma instalação padrão, os padrões principais são `/apps`, `/libs` - o conteúdo `/apps` tem uma prioridade mais elevada do que a `/libs` (isto é, *sobreposições* a).

* Dois usuários de serviço precisam de acesso JCR:READ ao local onde os scripts são armazenados. Esses usuários são: components-search-service (usado pelos componentes com.day.cq.wcm.coreto access/cache) e sling-scripting (usado por org.apache.sling.servlets.resolver para encontrar servlets).
* A configuração a seguir também deve ser configurada de acordo com a localização dos scripts (neste exemplo, em /etc, /libs ou /apps).

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
