---
title: Criando um novo componente de campo da interface do usuário do Granite
seo-title: Criando um novo componente de campo da interface do usuário do Granite
description: A interface do usuário Granite fornece uma variedade de componentes projetados para serem usados em formulários, chamados de campos
seo-description: A interface do usuário Granite fornece uma variedade de componentes projetados para serem usados em formulários, chamados de campos
uuid: cf26e057-4b0c-45f4-8975-2c658517f20e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 94b9eeee-aae3-4b28-9d6f-1be0e4acd982
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Criando um novo componente de campo da interface do usuário do Granite{#creating-a-new-granite-ui-field-component}

A interface do usuário Granite fornece uma variedade de componentes projetados para serem usados em formulários; estes são chamados *campos* no vocabulário da IU de Granite. Os componentes padrão do formulário Granite estão disponíveis em:

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>Esses campos de formulário da interface de usuário Granite são de especial interesse, pois são usados para caixas de diálogo [de](/help/sites-developing/developing-components.md)componentes.

>[!NOTE]
>
>Para obter detalhes completos sobre os campos, consulte a documentação [da interface do usuário do](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)Granite.

Use a estrutura da UI Foundation Granite para desenvolver e/ou estender componentes Granite. Isso tem dois elementos:

* servidor:

   * uma coleção de componentes básicos

      * alicerce - modular, composto, com camadas, reutilizável
      * componentes - Componentes Sling
   * ajuda ao desenvolvimento de aplicações


* lado do cliente:

   * uma coleção de clientlibs que fornece algum vocabulário (ou seja, extensão da linguagem HTML) para obter padrões de interação genéricos por meio de uma interface orientada por Hypermedia

O componente genérico da interface do usuário Granite `field` é composto de dois arquivos de interesse:

* `init.jsp`: trata do processamento genérico; rotulação, descrição e fornece o valor de formulário necessário ao renderizar o campo.
* `render.jsp`: é aqui que a renderização real do campo é executada e precisa ser substituída para seu campo personalizado; é incluído por `init.jsp`.

Consulte a documentação da interface do usuário [Granite - Campo](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) se desejar mais detalhes.

Para obter exemplos, consulte:

* `cqgems/customizingfield/components/colorpicker`

   * fornecido pela amostra [de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>Como esse mecanismo usa o JSP, o i18n e o XSS não são disponibilizados prontamente. Isso significa que você precisará internacionalizar e escapar de suas strings. O diretório a seguir contém os campos genéricos de uma instância padrão, você pode usá-los como referência:
>
>`/libs/granite/ui/components/foundation/form` diretório

## Criação do script do lado do servidor para o componente {#creating-the-server-side-script-for-the-component}

Seu campo personalizado deve substituir somente o `render.jsp` script, onde você fornece a marcação para o componente. Você pode considerar o JSP (ou seja, o script de renderização) como um invólucro para sua marcação.

1. Crie um novo componente que use a `sling:resourceSuperType` propriedade para herdar de:

   `/libs/granite/ui/components/foundation/form/field`

1. Substituir o script:

   `render.jsp`

   Neste script, é necessário gerar a marcação de hipermídia (isto é, marcação aprimorada, contendo a provisão de hipermídia) para que o cliente saiba como interagir com o elemento gerado. Isso deve seguir o estilo de codificação do lado do servidor da interface de usuário Granite.

   Ao personalizar, o único contrato que você *deve* cumprir é ler o valor do formulário (inicializado em `init.jsp`) da solicitação usando:

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   Para obter mais detalhes, consulte a implementação dos campos prontos para uso da interface do usuário Granite. por exemplo, `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >Atualmente, o JSP é o método de script preferido, já que a transmissão de informações de um componente para outro (bastante frequente no contexto de formulário/campos) não é facilmente alcançada no HTL.

## Criação da biblioteca do cliente para o componente {#creating-the-client-library-for-the-component}

Para adicionar um comportamento específico do cliente ao seu componente:

1. Crie uma clientlib de categoria `cq.authoring.dialog`.
1. Crie uma clientlib de categoria `cq.authoring.dialog` e defina sua `JS`/ `CSS` dentro dela.

   Defina seu `JS`/ `CSS` dentro da clientlib.

   >[!NOTE]
   >
   >No momento, a interface do usuário Granite não fornece ouvintes ou ganchos prontos para uso que você pode usar diretamente para adicionar o comportamento de JS. Portanto, para adicionar um comportamento adicional de JS ao seu componente, é necessário implementar um gancho JS em uma classe personalizada que você atribui ao seu componente durante a geração de marcação.

