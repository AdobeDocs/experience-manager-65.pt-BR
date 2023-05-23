---
title: Sobreposições
seo-title: Overlays
description: O AEM usa o princípio de sobreposições para permitir estender e personalizar os consoles e outras funcionalidades
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

O AEM (e, antes disso, o CQ) há muito tempo usa o princípio de sobreposições para permitir estender e personalizar o [consoles](/help/sites-developing/customizing-consoles-touch.md) e outras funcionalidades (por exemplo, [criação de página](/help/sites-developing/customizing-page-authoring-touch.md)).

Sobreposição é um termo que pode ser usado em muitos contextos. Nesse contexto (estender AEM), uma sobreposição significa usar a funcionalidade predefinida e impor suas próprias definições sobre ela (para personalizar a funcionalidade padrão).

Em uma instância padrão, a funcionalidade predefinida é mantida em `/libs` e é prática recomendada definir sua sobreposição (personalizações) no `/apps` filial. O AEM usa um caminho de pesquisa para encontrar um recurso, pesquisando primeiro o `/apps` e depois a variável `/libs` ramificação (a [o caminho de pesquisa pode ser configurado](#configuring-the-search-paths)). Esse mecanismo significa que sua sobreposição (e as personalizações definidas lá) terão prioridade.

Desde o AEM 6.0, foram feitas alterações no modo como as sobreposições são implementadas e usadas:

* AEM 6.0 em diante - para [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)Sobreposições relacionadas ao (ou seja, a interface habilitada para toque)

   * Método

      * Reconstrua o apropriado `/libs` estrutura em `/apps`.

         Isso não exige uma cópia 1:1, a [Fusão de recursos do Sling](/help/sites-developing/sling-resource-merger.md) é usado para cruzar as definições originais necessárias. O Sling Resource Merger fornece serviços para acessar e mesclar recursos por meio de mecanismos de diferenciação.

      * Faça as alterações em `/apps`.
   * Vantagens

      * Mais robusta às mudanças no `/libs`.
      * Apenas redefina o que é realmente necessário.


* Sobreposições não-Granite e sobreposições anteriores ao AEM 6.0

   * Método

      * Copiar o conteúdo de `/libs` para `/apps`

         É necessário copiar toda a sub-ramificação, incluindo as propriedades.

      * Faça as alterações em `/apps`.
   * Desvantagens

      * Embora suas alterações não sejam perdidas quando algo for alterado em `/libs`, talvez seja necessário recriar determinadas alterações que ocorrem na sobreposição em `/apps`.


>[!CAUTION]
>
>A variável [Fusão de recursos do Sling](/help/sites-developing/sling-resource-merger.md) e os métodos relacionados só podem ser usados com [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Isso significa que a criação de uma sobreposição com uma estrutura de esqueleto só é apropriada para a interface de usuário padrão habilitada para toque.
>
>As sobreposições para outras áreas (incluindo a interface clássica) envolvem a cópia do nó apropriado e de toda a subestrutura e, em seguida, fazem as alterações necessárias.

As sobreposições são o método recomendado para muitas alterações, como [configuração dos seus consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) ou [criar a categoria de seleção no navegador de ativos no painel lateral](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (usado ao criar páginas). Elas são necessárias como:

* Você ***não deve* fazer alterações no `/libs` ramificação **As alterações feitas podem ser perdidas, pois essa ramificação pode sofrer alterações sempre que você:

   * atualizar na sua instância
   * aplicar um hotfix
   * instalar um pacote de recursos

* Eles concentram as alterações em um local, facilitando o rastreamento, a migração, o backup e/ou a depuração das alterações, conforme necessário.

## Configurar os caminhos de pesquisa {#configuring-the-search-paths}

Para sobreposições, o recurso entregue é uma agregação dos recursos e propriedades recuperados, dependendo dos caminhos de pesquisa que podem ser definidos:

* O recurso **Caminho de pesquisa do resolvedor** conforme definido na [Configuração OSGi](/help/sites-deploying/configuring-osgi.md) para o **Fábrica do Apache Sling Resource Resolver**.

   * A ordem de cima para baixo dos caminhos de pesquisa indica suas respectivas prioridades.
   * Em uma instalação padrão, os padrões primários são `/apps`, `/libs` - para que o conteúdo de `/apps` tem uma prioridade mais alta do que a de `/libs` (ou seja, *sobreposições* it).

* Dois usuários de serviço precisam de acesso JCR:READ ao local em que os scripts são armazenados. Esses usuários são: components-search-service (usado pelo com.day.cq.wcm.coto access/cache components) e sling-scripting (usado por org.apache.sling.servlets.resolver para localizar servlets).
* A configuração a seguir também deve ser configurada de acordo com o local onde você coloca os scripts (neste exemplo, em /etc, /libs ou /apps).

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* Finalmente, o Resolvedor de Servlet também deve ser configurado (neste exemplo, para adicionar /etc também)

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## Exemplo de uso {#example-of-usage}

Alguns exemplos são abordados quando:

* [Personalização dos Consoles](/help/sites-developing/customizing-consoles-touch.md)
* [Personalização da criação de página](/help/sites-developing/customizing-page-authoring-touch.md)
