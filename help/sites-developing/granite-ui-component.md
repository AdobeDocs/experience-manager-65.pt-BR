---
title: Criação de um novo componente de campo da interface de usuário do Granite
description: A interface do usuário do Granite fornece vários componentes projetados para serem usados em formulários, chamados de campos
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e4820330-2ee6-4eca-83fd-462aa0b83647
source-git-commit: 26c0411d6cc16f4361cfa9e6b563eba0bfafab1e
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# Criação de um novo componente de campo da interface de usuário do Granite{#creating-a-new-granite-ui-field-component}

A interface do usuário do Granite fornece vários componentes projetados para serem usados em formulários; eles são chamados de *campos* no vocabulário da interface do usuário do Granite. Os componentes de formulário padrão do Granite estão disponíveis em:

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>Esses campos de formulário da interface do Granite são de especial interesse, pois são usados para [caixas de diálogo do componente](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Para obter detalhes completos sobre campos, consulte [Documentação da interface de usuário do Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

Use a estrutura do Granite UI Foundation para desenvolver e/ou estender componentes do Granite. Isso tem dois elementos:

* lado do servidor:

   * uma coleção de componentes de base

      * base - modular, componível, em camadas, reutilizável
      * componentes - componentes Sling

   * auxiliares para ajudar no desenvolvimento de aplicativos

* lado do cliente:

   * uma coleção de clientlibs fornecendo algum vocabulário (isto é, extensão da linguagem HTML) para alcançar padrões de interação genéricos através de uma interface de usuário orientada por Hypermedia.

O componente genérico da interface do Granite `field` O é composto por dois arquivos de interesse:

* `init.jsp`: lida com o processamento genérico, rotulagem, descrição e fornece o valor de formulário necessário ao renderizar o campo.
* `render.jsp`: é aqui que a renderização real do campo é executada e deve ser substituída para seu campo personalizado; é incluído por `init.jsp`.

Consulte [Documentação da interface do Granite - Campo](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) para obter detalhes.

Para obter exemplos, consulte:

* `cqgems/customizingfield/components/colorpicker`

   * fornecido pelo [Amostra de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>Como esse mecanismo usa JSP, i18n e XSS não são fornecidos prontos para uso. Isso significa que você deve internacionalizar e escapar seus Strings. O diretório a seguir contém os campos genéricos de uma instância padrão. Você pode usá-los como uma referência:
>
>`/libs/granite/ui/components/foundation/form` diretório

## Criação do script do lado do servidor para o componente {#creating-the-server-side-script-for-the-component}

Seu campo personalizado deve substituir apenas o `render.jsp` script, em que você fornece a marcação para o componente. Você pode considerar o JSP (ou seja, o script de renderização) como um invólucro para a marcação.

1. Crie um componente que use a variável `sling:resourceSuperType` propriedade da qual herdar:

   `/libs/granite/ui/components/foundation/form/field`

1. Substituir o script:

   `render.jsp`

   Nesse script, gere a marcação hypermedia (ou seja, marcação enriquecida, contendo o custo da hypermedia) para que o cliente saiba como interagir com o elemento gerado. Isso deve seguir o estilo de codificação do lado do servidor da interface do Granite.

   Ao personalizar, o único contrato que você *deve* fulfillment é ler o valor do formulário (inicializado em `init.jsp`) da solicitação usando:

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   Para obter mais detalhes, consulte a implementação dos campos de interface do usuário do Granite prontos para uso; por exemplo, `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >No momento, o JSP é o método de script preferido, pois transmitir informações de um componente para outro (o que é frequente no contexto de formulário/campos) não é facilmente obtido no HTL.

## Criação da biblioteca do cliente para o componente {#creating-the-client-library-for-the-component}

Para adicionar um comportamento específico do lado do cliente ao componente:

1. Criar uma clientlib da categoria `cq.authoring.dialog`.
1. Criar uma clientlib da categoria `cq.authoring.dialog` e defina seus `JS`/ `CSS` dentro dele.

   Defina o seu `JS`/ `CSS` dentro da clientlib.

   >[!NOTE]
   >
   >No momento, a interface do Granite não fornece ouvintes ou ganchos prontos para uso que você possa usar diretamente para adicionar o comportamento JS. Portanto, para adicionar mais comportamento JS ao componente, é necessário implementar um gancho JS em uma classe personalizada que você atribui ao componente durante a geração da marcação.
