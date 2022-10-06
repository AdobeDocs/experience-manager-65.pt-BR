---
title: Uso de assinaturas do Scribble em formulários HTML5
seo-title: Using Scribble Signature in HTML5 forms
description: Os formulários HTML5 são cada vez mais usados em dispositivos de toque, e um requisito comum é o suporte a assinaturas. Assinar documentos em dispositivos móveis está se tornando uma maneira aceita de assinar formulários em dispositivos móveis.
seo-description: HTML5 forms are increasingly used on touch devices, and one common requirement is to support signatures. Signing documents on mobile devices is becoming an accepted way of signing forms on mobile devices.
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
feature: Designer
exl-id: 2025182f-195b-40d0-aee7-67669f55b964
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# Uso de assinaturas do Scribble em formulários HTML5{#using-scribble-signature-in-html-forms}

Os formulários HTML5 são cada vez mais usados em dispositivos de toque, e um requisito comum é o suporte a assinaturas. O script (Escrever com uma caneta ou um dedo) está se tornando uma maneira aceita de assinar formulários em dispositivos móveis. Formulários HTML5 e Forms Designer agora ativam a opção de ter um campo de assinatura de rabisco no formulário. Quando o formulário é renderizado no navegador, é possível fazer logon nesses campos usando uma caneta, um mouse ou um toque.

## Como projetar um formulário usando o campo Assinatura do Scribble {#how-to-design-a-form-using-scribble-signature-field}

1. Abra um formulário no Forms Designer.
1. Arraste e solte o campo Signature Scribble na página.

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >Dimension do campo selecionado no Forms Designer são refletidas quando o campo é renderizado. No entanto, a dimensão da caixa de assinatura renderizada é calculada com base na proporção do aspecto do campo, e não na dimensão especificada no Forms Designer.

1. Configure o campo Signature Scribble .

   O campo Scribble de assinatura, por padrão, marca as informações de geolocalização como obrigatórias durante o processo de assinatura no iPad (e é opcional em outros dispositivos). Esse comportamento padrão pode ser substituído pela alteração do valor da variável `geoLocMandatoryOnIpad` propriedade. Essa propriedade é exposta como extras no Campo de rabisco de assinatura. As etapas para modificá-lo são:

   1. No formulário, selecione o campo Signature Scribble .
   1. Selecione o **Origem XML** guia .

      >[!NOTE]
      >
      >Para abrir a guia Origem XML, clique em **Exibir** > **Origem XML**.

   1. Localize a variável `<ui>` na `<field>` e modifique o código-fonte para parecer com o seguinte:

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. Selecione o **Visualização de projeto** guia . Na caixa de confirmação, clique em **Sim**.
   1. Salve o formulário.

1. Renderize o formulário em um navegador de dispositivo/desktop compatível.

## Interface com as assinaturas do Scribble {#interfacing-with-the-scribble-signatures}

### Assinatura {#signing}

Depois que um campo Scribble de assinatura é adicionado ao formulário e renderizado, clicar ou tocar no campo abre uma caixa de diálogo. O usuário pode assinar uma assinatura na área de desenho designada por um retângulo pontilhado, usando um mouse, dedo ou caneta.

![geolocalização](assets/geolocation.png)

**A.** Pincel **B.** Borracha **C.** Geolocalização **D.** Informações sobre geolocalização

### Marcação geográfica {#geo-tagging}

Clicar no ícone de geolocalização ao criar o rabisco faz com que as informações de localização geográfica e de hora sejam incorporadas ao campo.

>[!NOTE]
Na iPad, por padrão, a incorporação de informações de geolocalização é obrigatória.

No iPad, o ícone de geolocalização não é exibido por padrão, e as informações de geolocalização são automaticamente incorporadas quando você clica em **OK**.

Para iPads, essa configuração pode ser alterada modificando o valor de `geoLocManadatoryOnIpad` para `0`, nos parâmetros de inicialização do campo .

* Quando as informações de geolocalização são obrigatórias, o usuário é apresentado com uma área de desenho reduzida. O texto de geolocalização é adicionado quando o usuário clica em **OK** na área restante.
* Em outros casos, o usuário é apresentado com uma área de gaveta completa. Se o usuário optar por incorporar as informações de geolocalização, essa área será redimensionada para acomodar o texto da geolocalização.

### Limpar uma assinatura {#clearing-a-signature}

Ao usar esse recurso, o usuário pode clicar no botão **Borracha** para limpar o campo e começar de novo. Se as informações de localização geográfica foram adicionadas, elas também serão apagadas.

### Salvar uma assinatura {#saving-a-signature}

Clicar no **OK** ícone salva o rabisco como uma imagem no campo. A imagem e os valores podem ser enviados ao servidor para processamento adicional. Depois que um usuário clicar **OK**, o campo de rabisco está bloqueado. A assinatura não pode ser editada novamente usando o widget de rabisco.

Tocar ou clicar no campo Script abre a caixa de diálogo no modo somente leitura.

![3](assets/3.png)

### Seleção do tamanho da caneta {#selecting-pen-size}

Clique no botão **Pincéis** ícone para exibir uma lista de tamanhos de caneta disponíveis. Clique ou toque no tamanho da caneta para usar a caneta correspondente.

### Excluir assinaturas do formulário {#delete-signatures-from-the-form}

Para excluir as assinaturas do formulário:

* (Dispositivos móveis) Pressione por muito tempo o campo de assinatura e, na caixa de diálogo de confirmação, toque em **Sim**.
* (Desktop) Passe o mouse sobre o campo de assinatura, clique no botão **Cancelar** e, na caixa de diálogo de confirmação, clique em **Sim**.
