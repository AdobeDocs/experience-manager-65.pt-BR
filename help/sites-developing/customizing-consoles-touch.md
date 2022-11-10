---
title: Personalização dos consoles
seo-title: Customizing the Consoles
description: O AEM fornece vários mecanismos para permitir personalizar os consoles da sua instância de criação
seo-description: AEM provides various mechanisms to enable you to customize the consoles of your authoring instance
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
exl-id: 6e67f2b3-78b9-45f2-b496-61776b9fd9cc
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 1%

---

# Personalização dos consoles {#customizing-the-consoles}

>[!CAUTION]
>
>Este documento descreve como personalizar consoles na interface do usuário moderna e habilitada para toque e não se aplica à interface do usuário clássica.

O AEM fornece vários mecanismos para permitir que você personalize os consoles (e o [funcionalidade de criação de página](/help/sites-developing/customizing-page-authoring-touch.md)) da sua instância de criação.

* Clientlibs Clientlibs permite estender a implementação padrão para realizar novas funcionalidades, enquanto reutiliza as funções, objetos e métodos padrão. Ao personalizar, você pode criar sua própria clientlib em `/apps.` Por exemplo, ele pode conter o código necessário para o seu componente personalizado.

* As sobreposições são baseadas nas definições de nó e permitem que você sobreponha a funcionalidade padrão (em `/libs`) com sua própria funcionalidade personalizada (em `/apps`). Ao criar uma sobreposição, não é necessária uma cópia 1:1 do original, pois a fusão de recursos do sling permite a herança.

Elas podem ser usadas de várias maneiras para estender seus consoles de AEM. Uma pequena seleção é abordada abaixo (em um nível alto).

>[!NOTE]
>
>Para obter mais informações, consulte:
>
>* Uso e criação [clientlibs](/help/sites-developing/clientlibs.md).
>* Uso e criação [sobreposições](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>



>[!CAUTION]
>
>Você ***must*** não altere nada no `/libs` caminho.
>
>Isso ocorre porque o conteúdo da variável `/libs` O é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
>
>O método recomendado para configuração e outras alterações é:
>
>1. Recrie o item necessário (ou seja, como ele existe em `/libs`) `/apps`
>
>1. Faça quaisquer alterações no `/apps`

>


Por exemplo, a seguinte localização na variável `/libs` estrutura pode ser sobreposta:

* consoles (qualquer console baseado nas páginas da interface de usuário do Granite); por exemplo:

   * `/libs/wcm/core/content`

>[!NOTE]
>
>Consulte o artigo da Base de conhecimento , [Solução de problemas AEM TouchUI](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html), para obter mais dicas e ferramentas.

## Personalização da exibição padrão de um console {#customizing-the-default-view-for-a-console}

Você pode personalizar a exibição padrão (coluna, cartão, lista) de um console:

1. Você pode reordenar as exibições sobrepondo a entrada necessária de em:

   `/libs/wcm/core/content/sites/jcr:content/views`

   A primeira entrada será o padrão.

   Os nós disponíveis correlacionam-se às opções de exibição disponíveis:

   * `column`
   * `card`
   * `list`

1. Por exemplo, em uma sobreposição para a lista:

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   Defina a seguinte propriedade:

   * **Nome**: `sling:orderBefore`
   * **Tipo**: `String`
   * **Valor**: `column`

### Adicionar nova ação à barra de ferramentas {#add-new-action-to-the-toolbar}

1. Você pode criar seus próprios componentes e incluir as bibliotecas de clientes correspondentes para ações personalizadas. Por exemplo, um **Promover para Twitter** ação em:

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   Isso pode ser conectado a um item da barra de ferramentas no console:

   `/apps/<yourProject>/admin/ext/launches`

   Por exemplo, no modo de seleção:

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### Restringir uma ação da barra de ferramentas a um grupo específico {#restrict-a-toolbar-action-to-a-specific-group}

1. Você pode usar uma condição de renderização personalizada para sobrepor a ação padrão e impor condições específicas que devem ser cumpridas antes da renderização.

   Por exemplo, crie um componente para controlar as condições de renderização de acordo com o grupo:

   `/apps/myapp/components/renderconditions/group`

1. Para aplicá-los à ação Criar site no console Sites :

   `/libs/wcm/core/content/sites`

   Crie a sobreposição:

   `/apps/wcm/core/content/sites`

1. Em seguida, adicione a condição de renderização para a ação:

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   Usando as propriedades neste nó, é possível definir a variável `groups` Autorizados a executar a ação específica; por exemplo, `administrators`

### Personalização de colunas na exibição de lista {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>Esse recurso é otimizado para colunas de campos de texto; para outros tipos de dados, é possível sobrepor `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` em `/apps`.

Para personalizar as colunas na exibição de lista:

1. Sobreponha a lista de colunas disponíveis.

   * No nó :

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * Adicione as novas colunas ou remova as existentes.
   Consulte [Uso de sobreposições (e da Fusão de recursos do Sling)](/help/sites-developing/overlays.md) para obter mais informações.

1. Opcionalmente:

   * Se desejar plug-in de dados adicionais, é necessário gravar um [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) com um
      `pageInfoProviderType` propriedade.

   Por exemplo, consulte a classe/pacote anexado (do GitHub) abaixo.

1. Agora é possível selecionar a coluna no configurador de colunas da exibição em lista.

### Filtrar recursos {#filtering-resources}

Ao usar um console, um caso de uso comum é quando o usuário deve selecionar entre recursos (por exemplo, páginas, componentes, ativos etc.). Isso pode assumir a forma de uma lista, por exemplo, da qual o autor deve escolher um item.

Para manter a lista em um tamanho razoável e também relevante para o caso de uso, um filtro pode ser implementado na forma de um predicado personalizado. Consulte [este artigo](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) para obter detalhes.
