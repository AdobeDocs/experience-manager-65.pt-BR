---
title: Uso de assinaturas do Scribble em formulários HTML5
seo-title: Uso de assinaturas do Scribble em formulários HTML5
description: Os formulários HTML5 são cada vez mais usados em dispositivos de toque e um requisito comum é o suporte a assinaturas. Assinar documentos em dispositivos móveis está se tornando uma maneira aceita de assinar formulários em dispositivos móveis.
seo-description: Os formulários HTML5 são cada vez mais usados em dispositivos de toque e um requisito comum é o suporte a assinaturas. Assinar documentos em dispositivos móveis está se tornando uma maneira aceita de assinar formulários em dispositivos móveis.
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
feature: Designer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---


# Uso de assinaturas do Scribble em formulários HTML5{#using-scribble-signature-in-html-forms}

Formulários HTML5 são cada vez mais usados em dispositivos de toque e um requisito comum é o suporte a assinaturas. O script (Escrever com uma caneta ou um dedo) está se tornando uma maneira aceita de assinar formulários em dispositivos móveis. Formulários HTML5 e Forms Designer agora permitem a opção de ter um campo de assinatura de rabisco no formulário. Quando o formulário é renderizado no navegador, é possível fazer logon nesses campos usando uma caneta, um mouse ou um toque.

## Como projetar um formulário usando o campo de assinatura do Scribble {#how-to-design-a-form-using-scribble-signature-field}

1. Abra um formulário no Forms Designer.
1. Arraste e solte o campo Signature Scribble na página.

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >Dimension do campo selecionado no Forms Designer são refletidas quando o campo é renderizado. No entanto, a dimensão da caixa de assinatura renderizada é calculada com base na proporção do aspecto do campo, e não na dimensão especificada no Forms Designer.

1. Configure o campo Signature Scribble .

   O campo Signature Scribble , por padrão, marca as informações de geolocalização como obrigatórias durante o processo de assinatura no iPad (e é opcional em outros dispositivos). Esse comportamento padrão pode ser substituído pela alteração do valor da propriedade `geoLocMandatoryOnIpad`. Essa propriedade é exposta como extras no Campo de rabisco de assinatura. As etapas para modificá-lo são:

   1. No formulário, selecione o campo Signature Scribble .
   1. Selecione a guia **Origem XML**.

      >[!NOTE]
      >
      >Para abrir a guia Origem XML, clique em **Ver** > **Origem XML**.

   1. Localize a tag `<ui>` na tag `<field>` e modifique o código-fonte para que pareça o seguinte:

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. Selecione a guia **Visualização de projeto**. Na caixa de confirmação, clique em **Yes**.
   1. Salve o formulário.

1. Renderize o formulário em um navegador de dispositivo/desktop compatível.

## Interface com as assinaturas do Scribble {#interfacing-with-the-scribble-signatures}

### Assinando {#signing}

Depois que um campo Scribble de assinatura é adicionado ao formulário e renderizado, clicar ou tocar no campo abre uma caixa de diálogo. O usuário pode assinar uma assinatura na área de desenho designada por um retângulo pontilhado, usando um mouse, dedo ou caneta.

![geolocalização](assets/geolocation.png)

**A.** Pincel  **B.** Borracha  **C.** Geolocation  **D.** Informações de geolocalização

### Marcação geográfica {#geo-tagging}

Clicar no ícone de geolocalização ao criar o rabisco faz com que as informações de localização geográfica e de hora sejam incorporadas ao campo.

>[!NOTE]
No iPad, por padrão, a incorporação de informações de geolocalização é obrigatória.

No iPad, o ícone de geolocalização não é mostrado por padrão, e as informações de geolocalização são automaticamente incorporadas, quando você clica em **OK**.

Para iPads, essa configuração pode ser alterada modificando o valor do parâmetro `geoLocManadatoryOnIpad` para `0`, nos parâmetros de inicialização do campo.

* Quando as informações de geolocalização são obrigatórias, o usuário é apresentado com uma área de desenho reduzida. O texto de geolocalização é adicionado quando o usuário clica no ícone **OK** na área restante.
* Em outros casos, o usuário é apresentado com uma área de gaveta completa. Se o usuário optar por incorporar as informações de geolocalização, essa área será redimensionada para acomodar o texto da geolocalização.

### Limpar uma assinatura {#clearing-a-signature}

Ao usar esse recurso, um usuário pode clicar no ícone **Borracha** para limpar o campo e começar de novo. Se as informações de localização geográfica foram adicionadas, elas também serão apagadas.

### Salvar uma assinatura {#saving-a-signature}

Clicar no ícone **OK** salva o rabisco como uma imagem no campo. A imagem e os valores podem ser enviados ao servidor para processamento adicional. Depois que um usuário clicar em **OK**, o campo de rabisco é bloqueado. A assinatura não pode ser editada novamente usando o widget de rabisco.

Tocar ou clicar no campo Script abre a caixa de diálogo no modo somente leitura.

![3](assets/3.png)

### Selecionar o tamanho da caneta {#selecting-pen-size}

Clique no ícone **Pincéis** para exibir uma lista de tamanhos de caneta disponíveis. Clique ou toque no tamanho da caneta para usar a caneta correspondente.

### Excluir assinaturas do formulário {#delete-signatures-from-the-form}

Para excluir as assinaturas do formulário:

* (Dispositivos móveis) Pressione por muito tempo o campo de assinatura e, na caixa de diálogo de confirmação, toque em **Yes**.
* (Desktop) Passe o mouse sobre o campo de assinatura, clique no ícone **Cancelar** e, na caixa de diálogo de confirmação, clique em **Sim**.
