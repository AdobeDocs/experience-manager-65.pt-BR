---
title: Sobreposições
description: O Adobe Experience Manager usa o princípio de sobreposições para permitir que você estenda e personalize os consoles e outras funcionalidades.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# Sobreposições{#overlays}

O Adobe Experience Manager (AEM) — e, antes disso, o CQ — há muito tempo usa o princípio de sobreposições para permitir que você estenda e personalize os [consoles](/help/sites-developing/customizing-consoles-touch.md) e outras funcionalidades (por exemplo, [criação de página](/help/sites-developing/customizing-page-authoring-touch.md)).

Sobreposição é um termo usado em muitos contextos. Nesse contexto (extensão do AEM), uma sobreposição significa usar a funcionalidade predefinida e impor suas próprias definições sobre ela (para personalizar a funcionalidade padrão).

Em uma instância padrão, a funcionalidade predefinida é mantida em `/libs` e é prática recomendada definir sua sobreposição (personalizações) na ramificação `/apps`. O AEM usa um caminho de pesquisa para localizar um recurso, pesquisando primeiro a ramificação `/apps` e depois a ramificação `/libs` (o [caminho de pesquisa pode ser configurado](#configuring-the-search-paths)). Esse mecanismo significa que sua sobreposição (e as personalizações definidas lá) tem prioridade.

Desde o AEM 6.0, foram feitas alterações no modo como as sobreposições são implementadas e usadas:

* AEM 6.0 e posterior - para sobreposições relacionadas ao [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) (ou seja, a interface habilitada para toque)

   * Método

      * Reconstruir a estrutura `/libs` apropriada em `/apps`.

        Isso não requer uma cópia 1:1. O [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) é usado para fazer referência cruzada das definições originais necessárias. O Sling Resource Merger fornece serviços para acessar e mesclar recursos com mecanismos de diferenciação.

      * Em `/apps`, faça as alterações.

   * Vantagens

      * Mais robusto para alterações em `/libs`.
      * Apenas redefina o que é necessário.

* Sobreposições não-Granite e sobreposições antes do AEM 6.0

   * Método

      * Copiar o conteúdo de `/libs` para `/apps`

        Copie a subramificação inteira, incluindo as propriedades.

      * Em `/apps`, faça as alterações.

   * Desvantagens

      * Embora as alterações não sejam perdidas quando algo for alterado em `/libs`, talvez seja necessário recriar determinadas alterações que ocorrem na sobreposição em `/apps`.

>[!CAUTION]
>
>O [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) e os métodos relacionados só podem ser usados com o [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Isso significa que a criação de uma sobreposição com uma estrutura de esqueleto só é apropriada para a interface de usuário padrão habilitada para toque.
>
>As sobreposições para outras áreas (incluindo a interface clássica) envolvem a cópia do nó apropriado e de toda a subestrutura e, em seguida, fazem as alterações necessárias.

Sobreposições são o método recomendado para muitas alterações, como [configurar seus consoles](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) ou [criar a categoria de seleção para o navegador de ativos no painel lateral](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (usado ao criar páginas). Elas são necessárias como:

* ***Não* fazer alterações na `/libs` ramificação **As alterações feitas podem ser perdidas, pois essa ramificação pode sofrer alterações sempre que você:

   * atualizar na sua instância
   * aplicar um hotfix
   * instalar um pacote de recursos

* Eles concentram as alterações em um local, facilitando o rastreamento, a migração, o backup ou a depuração de alterações, conforme necessário.

## Configurar os caminhos de pesquisa {#configuring-the-search-paths}

Para sobreposições, o recurso entregue é uma agregação dos recursos e propriedades recuperados, dependendo dos caminhos de pesquisa que podem ser definidos:

* O recurso **Caminho de Pesquisa do Resolvedor** conforme definido na [configuração OSGi](/help/sites-deploying/configuring-osgi.md) para a **Fábrica do Resolvedor de Recursos Apache Sling**.

   * A ordem de cima para baixo dos caminhos de pesquisa indica suas respectivas prioridades.
   * Em uma instalação padrão, os padrões primários são `/apps`, `/libs` - portanto, o conteúdo de `/apps` tem uma prioridade mais alta do que a de `/libs` (isto é, ele *sobreposições*).

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
