---
title: Uso da Assinatura Escrita em formulários HTML5
description: Os formulários HTML5 são cada vez mais usados em dispositivos de toque, e um requisito comum é o suporte a assinaturas. Assinar documentos em dispositivos móveis está se tornando uma maneira aceita de assinar formulários em dispositivos móveis.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
docset: aem65
feature: Forms Designer,Designer
exl-id: 2025182f-195b-40d0-aee7-67669f55b964
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# Uso da Assinatura Escrita em formulários HTML5{#using-scribble-signature-in-html-forms}

Os formulários HTML5 são cada vez mais usados em dispositivos de toque, e um requisito comum é o suporte a assinaturas. Escrever (com uma caneta ou um dedo) está se tornando uma maneira aceita de assinar formulários em dispositivos móveis. Os formulários HTML5 e o Forms Designer agora permitem a opção de ter um campo de assinatura à mão no formulário. Quando o formulário é renderizado no navegador, é possível assinar esses campos usando uma caneta, um mouse ou um toque.

## Como criar um formulário usando o campo Assinatura Escrita {#how-to-design-a-form-using-scribble-signature-field}

1. Abra um formulário no Forms Designer.
1. Arraste e solte o campo Rabisco de assinatura na página.

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >Os Dimension do campo selecionado no Forms Designer são refletidos quando o campo é renderizado. No entanto, a dimensão da caixa de assinatura renderizada é calculada com base na proporção do campo, e não na dimensão especificada no Forms Designer.

1. Configure o campo Assinatura Escrita.

   O campo Assinatura fixa, por padrão, marca as informações de geolocalização como obrigatórias durante o processo de assinatura no iPad (e é opcional para outros dispositivos). Esse comportamento padrão pode ser substituído pela alteração do valor da propriedade `geoLocMandatoryOnIpad`. Essa propriedade é exposta como extras no Campo de rabisco de assinatura. As etapas para modificá-lo são:

   1. No formulário, selecione o campo Assinatura Escrita.
   1. Selecione a guia **XML Source**.

      >[!NOTE]
      >
      >Para abrir a guia XML Source, clique em **Exibir** > **XML Source**.

   1. Localize a marca `<ui>` na marca `<field>` e modifique o código-fonte para que seja semelhante ao seguinte:

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. Selecione a guia **Exibição de Design**. Na caixa de confirmação, clique em **Sim**.
   1. Salve o formulário.

1. Renderize o formulário em um navegador de dispositivo/desktop compatível.

## Interface com as assinaturas escritas {#interfacing-with-the-scribble-signatures}

### Assinatura {#signing}

Depois que um campo Rabiscar de assinatura é adicionado ao formulário e renderizado, clicar ou tocar no campo abre uma caixa de diálogo. O usuário pode rabiscar uma assinatura na área de desenho designada por um retângulo pontilhado, usando um mouse, dedo ou caneta.

![geolocalização](assets/geolocation.png)

**A.** Pincel **B.** Borracha **C.** Geolocalização **D.** Informações de geolocalização

### Marcação geográfica {#geo-tagging}

Clicar no ícone de localização geográfica ao criar o rabisco faz com que as informações de localização geográfica e hora sejam incorporadas ao campo.

>[!NOTE]
>
No iPad, por padrão, a incorporação de informações de geolocalização é obrigatória.

Na iPad, o ícone de geolocalização não é exibido por padrão, e as informações de geolocalização são inseridas automaticamente, quando você clica em **OK**.

Para iPads, esta configuração pode ser alterada modificando o valor do parâmetro `geoLocManadatoryOnIpad` para `0`, nos parâmetros init do campo.

* Quando as informações de geolocalização são obrigatórias, o usuário recebe uma área de desenho reduzida. O texto de geolocalização é adicionado quando o usuário clica no ícone **OK** na área restante.
* Em outros casos, o usuário é apresentado com uma área desenhável completa. Se o usuário optar por incorporar informações de geolocalização, essa área será redimensionada para acomodar o texto de geolocalização.

### Limpar uma assinatura {#clearing-a-signature}

Ao usar esse recurso, um usuário pode clicar no ícone **Borracha** para limpar o campo e começar novamente. Se as informações de geolocalização tiverem sido adicionadas, elas também serão apagadas.

### Como salvar uma assinatura {#saving-a-signature}

Clicar no ícone **OK** salva o rabisco como uma imagem no campo. A imagem e os valores podem ser enviados ao servidor para processamento adicional. Depois que um usuário clicar em **OK**, o campo de rabisco será bloqueado. A assinatura não pode ser editada novamente usando o widget de rabisco.

Tocar ou clicar no campo Rabiscar abre a caixa de diálogo no modo somente leitura.

![3](assets/3.png)

### Selecionar o tamanho da Caneta {#selecting-pen-size}

Clique no ícone **Pincéis** para exibir uma lista de tamanhos de caneta disponíveis. Clique no tamanho da caneta para usar a caneta correspondente.

### Excluir assinaturas do formulário {#delete-signatures-from-the-form}

Para excluir as assinaturas do formulário:

* (Dispositivos móveis) Pressione o campo de assinatura e, na caixa de diálogo de confirmação, selecione **Sim**.
* (Desktop) Passe o mouse sobre o campo de assinatura, clique no ícone **Cancelar** e, na caixa de diálogo de confirmação, clique em **Sim**.
