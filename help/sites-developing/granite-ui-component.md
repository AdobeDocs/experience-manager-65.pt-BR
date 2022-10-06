---
title: Criação de um novo componente de campo da interface do usuário do Granite
seo-title: Creating a New Granite UI Field Component
description: A interface do usuário do Granite fornece vários componentes projetados para serem usados em formulários, chamados de campos
seo-description: Granite UI provides a range of components designed to be used in forms, called fields
uuid: cf26e057-4b0c-45f4-8975-2c658517f20e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 94b9eeee-aae3-4b28-9d6f-1be0e4acd982
exl-id: e4820330-2ee6-4eca-83fd-462aa0b83647
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# Criação de um novo componente de campo da interface do usuário do Granite{#creating-a-new-granite-ui-field-component}

A interface do usuário do Granite fornece uma variedade de componentes projetados para serem usados em formulários; são chamadas de *campos* no vocabulário da interface do usuário do Granite. Os componentes de formulário padrão do Granite estão disponíveis em:

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>Esses campos de formulário da interface de usuário do Granite são de especial interesse, pois são usados para [caixas de diálogo do componente](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Para obter detalhes completos sobre os campos, consulte o [Documentação da interface do usuário do Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

Use a estrutura da Fundação da interface do usuário do Granite para desenvolver e/ou estender os componentes do Granite. Isso tem dois elementos:

* lado do servidor:

   * uma coleção de componentes fundamentais

      * alicerce - modular, composível, em camadas, reutilizável
      * componentes - Componentes do Sling
   * ajuda para auxiliar no desenvolvimento de aplicativos


* lado do cliente:

   * uma coleção de clientlibs que fornece um vocabulário (ou seja, extensão da linguagem do HTML) para obter padrões de interação genéricos por meio de uma interface orientada por hipermídia

O componente genérico da interface do usuário do Granite `field` é composto por dois arquivos de interesse:

* `init.jsp`: trata o processamento genérico; rotular, descrever e fornecer o valor do formulário necessário ao renderizar o campo.
* `render.jsp`: é aqui que a renderização real do campo é executada e precisa ser substituída para o campo personalizado; está incluído por `init.jsp`.

Consulte a [Documentação da interface do usuário do Granite - Campo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) se desejar mais detalhes.

Para obter exemplos, consulte:

* `cqgems/customizingfield/components/colorpicker`

   * do [Amostra de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>Como esse mecanismo usa JSP, i18n e XSS não são fornecidos prontos para uso. Isso significa que você precisará internacionalizar e escapar de suas strings. O diretório a seguir contém os campos genéricos de uma instância padrão. Você pode usá-los como referência:
>
>`/libs/granite/ui/components/foundation/form` diretory

## Criação do script do lado do servidor para o componente {#creating-the-server-side-script-for-the-component}

Seu campo personalizado deve substituir apenas o `render.jsp` , onde você fornece a marcação para o seu componente. Você pode considerar o JSP (ou seja, o script de renderização) como um wrapper para sua marcação.

1. Crie um novo componente que use o `sling:resourceSuperType` propriedade a ser herdada de:

   `/libs/granite/ui/components/foundation/form/field`

1. Substitua o script:

   `render.jsp`

   Nesse script, você precisa gerar a marcação de hipermídia (ou seja, marcação enriquecida, contendo a disposição da hipermídia) para que o cliente saiba como interagir com o elemento gerado. Isso deve seguir o estilo de codificação da interface do usuário do Granite.

   Ao personalizar, o único contrato que você *must* fulfill é ler o valor do formulário (inicializado em `init.jsp`) da solicitação usando:

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   Para obter mais detalhes, consulte a implementação dos campos prontos para uso da interface do Granite; por exemplo, `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >No momento, o JSP é o método de script preferido, pois a transmissão de informações de um componente para outro (que é bastante frequente no contexto de formulário/campos) não é facilmente alcançada no HTL.

## Criar a biblioteca do cliente para o componente {#creating-the-client-library-for-the-component}

Para adicionar um comportamento específico do lado do cliente ao seu componente:

1. Criar uma clientlib da categoria `cq.authoring.dialog`.
1. Criar uma clientlib da categoria `cq.authoring.dialog` e defina `JS`/ `CSS` dentro dela.

   Defina as `JS`/ `CSS` dentro da clientlib.

   >[!NOTE]
   >
   >No momento, a interface do usuário do Granite não fornece ouvintes ou ganchos prontos para uso que você pode usar diretamente para adicionar o comportamento do JS. Portanto, para adicionar um comportamento JS adicional ao seu componente, é necessário implementar um gancho JS em uma classe personalizada que você atribui ao seu componente durante a geração da marcação.
