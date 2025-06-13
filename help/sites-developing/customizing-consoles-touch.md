---
title: Personalização dos Consoles
description: O AEM fornece vários mecanismos para permitir personalizar os consoles da sua instância de criação
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 6e67f2b3-78b9-45f2-b496-61776b9fd9cc
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 0%

---

# Personalização dos Consoles {#customizing-the-consoles}

>[!CAUTION]
>
>Este documento descreve como personalizar consoles na interface moderna e habilitada para toque, e não se aplica à interface clássica.

O AEM fornece vários mecanismos para permitir que você personalize os consoles (e a [funcionalidade de criação de página](/help/sites-developing/customizing-page-authoring-touch.md)) da sua instância de criação.

* Clientlibs
As clientlibs permitem estender a implementação padrão para obter uma nova funcionalidade, além de reutilizar as funções, os objetos e os métodos padrão. Ao personalizar, você pode criar sua própria clientlib em `/apps.`. Por exemplo, ela pode conter o código necessário para seu componente personalizado.

* Sobreposições
As sobreposições são baseadas nas definições de nó e permitem sobrepor a funcionalidade padrão (em `/libs`) com sua própria funcionalidade personalizada (em `/apps`). Ao criar uma sobreposição, uma cópia 1:1 do original não é necessária, pois a fusão de recursos do sling permite a herança.

Eles podem ser usados de várias maneiras para estender os consoles do AEM. Uma pequena seleção é abordada abaixo (em um nível alto).

>[!NOTE]
>
>Para obter mais informações, consulte:
>
>* Usando e criando [clientlibs](/help/sites-developing/clientlibs.md).
>* Usando e criando [sobreposições](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>


>[!CAUTION]
>
>Você ***deve*** não alterar nada no caminho `/libs`.
>
>Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
>
>O método recomendado para configuração e outras alterações é:
>
>1. Recriar o item necessário (isto é, como ele existe em `/libs`) em `/apps`
>
>1. Fazer alterações em `/apps`
>

Por exemplo, o seguinte local dentro da estrutura `/libs` pode ser sobreposto:

* consoles (qualquer console com base nas páginas de interface do Granite); por exemplo:

   * `/libs/wcm/core/content`

>[!NOTE]
>
>Consulte o artigo da Base de Dados de Conhecimento, [Solução de problemas da interface para toque do AEM](https://experienceleague.adobe.com/pt-br/docs/experience-cloud-kcs/kbarticles/ka-16935), para obter mais dicas e ferramentas.

## Personalizando a View Default para uma Console {#customizing-the-default-view-for-a-console}

É possível personalizar a exibição padrão (coluna, cartão, lista) de um console:

1. Você pode reordenar as exibições sobrepondo a entrada necessária em:

   `/libs/wcm/core/content/sites/jcr:content/views`

   A primeira entrada será o padrão.

   Os nós disponíveis estão correlacionados com as opções de visualização disponíveis:

   * `column`
   * `card`
   * `list`

1. Por exemplo, em uma sobreposição para lista:

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   Defina a seguinte propriedade:

   * **Nome**: `sling:orderBefore`
   * **Tipo**: `String`
   * **Valor**: `column`

### Adicionar nova ação à barra de ferramentas {#add-new-action-to-the-toolbar}

1. Você pode criar seus próprios componentes e incluir as bibliotecas de clientes correspondentes para ações personalizadas. Por exemplo, uma ação **Promover para o Twitter** em:

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   Ele pode ser conectado a um item da barra de ferramentas no console:

   `/apps/<yourProject>/admin/ext/launches`

   Por exemplo, no modo de seleção:

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### Restringir uma ação da barra de ferramentas a um grupo específico {#restrict-a-toolbar-action-to-a-specific-group}

1. Você pode usar uma condição de renderização personalizada para sobrepor a ação padrão e impor condições específicas que devem ser atendidas antes de ser renderizada.

   Por exemplo, crie um componente para controlar as condições de renderização de acordo com o grupo:

   `/apps/myapp/components/renderconditions/group`

1. Para aplicá-los à ação Criar site no console Sites:

   `/libs/wcm/core/content/sites`

   Crie a sobreposição:

   `/apps/wcm/core/content/sites`

1. Em seguida, adicione a condição de renderização para a ação:

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   Usando propriedades neste nó, você pode definir o `groups` permitido para executar a ação específica; por exemplo, `administrators`

### Personalização de Colunas na Exibição de Lista {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>Este recurso é otimizado para colunas de campos de texto; para outros tipos de dados, é possível sobrepor `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` em `/apps`.

Para personalizar as colunas na exibição de lista:

1. Sobrepor a lista de colunas disponíveis.

   * No nó:

     ```
            /apps/wcm/core/content/common/availablecolumns
     ```

   * Adicione suas novas colunas ou remova as existentes.

   Consulte [Uso de sobreposições (e o Sling Resource Merger)](/help/sites-developing/overlays.md) para obter mais informações.

1. Opcionalmente:

   * Se quiser conectar dados adicionais, você precisará gravar um [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) com um

     Propriedade `pageInfoProviderType`.

   Por exemplo, consulte a classe/pacote anexado (do GitHub) abaixo.

1. Agora é possível selecionar a coluna no configurador de colunas da exibição em lista.

### Filtrar recursos {#filtering-resources}

Ao usar um console, um caso de uso comum é quando o usuário deve selecionar entre os recursos (por exemplo, páginas, componentes, ativos e assim por diante). Isso pode tomar a forma de uma lista, por exemplo, da qual o autor deve escolher um item.

Para manter a lista em um tamanho razoável e também relevante para o caso de uso, um filtro pode ser implementado no formato de um predicado personalizado. Consulte [Personalizando a criação de páginas - Recursos de filtragem](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) para obter detalhes.
