---
title: Criar um formulário adaptável usando um conjunto de formulários adaptáveis
description: Com o AEM Forms, reúna formulários adaptáveis para criar um único formulário adaptável grande e entender seus recursos.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 4254c2cb-66cc-4a46-b447-bc5e32def7a0
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Criar um formulário adaptável usando um conjunto de formulários adaptáveis{#create-an-adaptive-form-using-a-set-of-adaptive-forms}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

## Visão geral {#overview}

Em um fluxo de trabalho, como um aplicativo para abrir uma conta bancária, os usuários preenchem vários formulários. Em vez de pedir que eles preencham um conjunto de formulários, você pode empilhá-los e criar um formulário grande (formulário pai). Ao adicionar um formulário adaptável ao formulário maior, ele é adicionado como um painel (formulário filho). Você adiciona um conjunto de formulários secundários para criar um formulário principal. Você pode mostrar ou ocultar painéis com base na entrada do usuário. Os botões do formulário pai, como enviar e redefinir, substituem os botões do formulário filho. Para adicionar um formulário adaptável no formulário pai, você pode arrastar e soltar o formulário adaptável do navegador de ativos (como fragmentos de formulário adaptáveis).

Os recursos disponíveis são:

* Criação independente
* Mostrar/ocultar formulários apropriados
* Carregamento lento

Recursos como criação independente e carregamento lento fornecem melhorias de desempenho em relação ao uso de componentes individuais para criar o formulário pai.

>[!NOTE]
>
>Não é possível usar formulários/fragmentos adaptáveis baseados em XFA como formulários secundários ou principais.

## Nos bastidores {#behind-the-scenes}

Você pode adicionar formulários e fragmentos adaptáveis baseados em XSD no formulário principal. A estrutura do formulário pai é igual a [qualquer formulário adaptável](../../forms/using/prepopulate-adaptive-form-fields.md). Quando você adiciona um formulário adaptável como um formulário filho, ele é adicionado como um painel no formulário pai. Os dados de um formulário filho associado são armazenados na `data`raiz da seção `afBoundData` do esquema XML do formulário pai.

Por exemplo, seus clientes preenchem um formulário de inscrição. Os dois primeiros campos do formulário são nome e identidade. Seu XML é:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
        </data>
    </afBoundData>
</afData>
```

Você adiciona outro formulário no aplicativo que permite que os clientes preencham o endereço comercial. A raiz de esquema do formulário filho é `officeAddress`. Aplicar `bindref` `/application/officeAddress` ou `/officeAddress`. Se `bindref` não for fornecido, o formulário filho será adicionado como a subárvore `officeAddress`. Consulte o XML do formulário abaixo:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
        </data>
    </afBoundData>
</afData>
```

Se você inserir outro formulário que permita que seus clientes forneçam o endereço residencial, aplique `bindref` `/application/houseAddress or /houseAddress.`O XML se parece com:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <officeAddress>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </officeAddress>
            <houseAddress>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </houseAddress>
        </data>
    </afBoundData>
</afData>
```

Se você quiser manter o mesmo nome de subraiz da raiz do esquema ( `Address` neste exemplo), use bindrefs indexados.

Por exemplo, aplique bindrefs `/application/address[1]` ou `/address[1]` e `/application/address[2]` ou `/address[2]`. O XML do formulário é:

```xml
<afData>
    <afUnboundData>
        <data />
    </afUnboundData>
    <afBoundData>
        <data xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
            <applicantName>Sarah Rose</applicantName>
            <applicantId>1234</applicantId>
            <address>
                <addressLine>1, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
            <address>
                <addressLine>2, Geometrixx City</addressLine>
                <zip>11111</zip>
            </address>
        </data>
    </afBoundData>
</afData>
```

É possível alterar a subárvore padrão do formulário/fragmento adaptável usando a propriedade `bindRef`. A propriedade `bindRef` permite especificar o caminho que aponta para um local na estrutura de árvore do esquema XML.

Se o formulário filho não estiver vinculado, seus dados serão armazenados na `data`raiz da seção `afUnboundData` do esquema XML do formulário pai.

É possível adicionar um formulário adaptável como formulário filho várias vezes. Verifique se `bindRef` foi modificado corretamente para que cada instância usada do formulário adaptável aponte para uma subraiz diferente na raiz de dados.

>[!NOTE]
>
>Se diferentes formulários/fragmentos forem mapeados para a mesma subraiz, os dados serão substituídos.

## Adicionar um formulário adaptável como um formulário filho usando o navegador de ativos {#adding-an-adaptive-form-as-a-child-form-using-asset-browser}

Execute as seguintes etapas para adicionar um formulário adaptável como um formulário filho usando o navegador de ativos.

1. Abra o formulário principal no modo de edição.
1. Na barra lateral, clique em **Assets** ![assets-browser](assets/assets-browser.png). Em Assets, selecione **Formulário adaptável** no menu suspenso.
   [![Selecionar formulário adaptável em Assets](assets/asset.png)](assets/asset-1.png)

1. Arraste e solte o formulário adaptável que deseja adicionar como um formulário filho.
   [![Arraste e solte o formulário adaptável no site](assets/drag-drop.png)](assets/drag-drop-1.png)O formulário adaptável solto é adicionado como um formulário filho.
