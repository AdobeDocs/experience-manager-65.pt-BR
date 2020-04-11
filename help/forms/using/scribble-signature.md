---
title: Uso da assinatura em script em formulários HTML5
seo-title: Uso da assinatura em script em formulários HTML5
description: Formulários HTML5 são cada vez mais usados em dispositivos de toque, e um requisito comum é o suporte a assinaturas. Assinar documentos em dispositivos móveis está se tornando uma forma aceita de assinar formulários em dispositivos móveis.
seo-description: Formulários HTML5 são cada vez mais usados em dispositivos de toque, e um requisito comum é o suporte a assinaturas. Assinar documentos em dispositivos móveis está se tornando uma forma aceita de assinar formulários em dispositivos móveis.
uuid: 163dd55a-971a-4dd4-93a7-a14e80184d9b
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
discoiquuid: ecd7f538-9c24-48e7-8450-596851e99cff
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Uso da assinatura em script em formulários HTML5{#using-scribble-signature-in-html-forms}

Os formulários HTML5 estão sendo cada vez mais usados em dispositivos de toque, e um requisito comum é o suporte a assinaturas. Escrever (Escrever com uma caneta ou um dedo) está se tornando uma maneira aceita de assinar formulários em dispositivos móveis. Formulários HTML5 e Forms Designer agora ativam a opção de ter um campo de assinatura em forma de script no formulário. Quando o formulário é renderizado no navegador, é possível fazer logon nesses campos usando um estilo, mouse ou toque.

## Como projetar um formulário usando o campo Assinatura de script {#how-to-design-a-form-using-scribble-signature-field}

1. Abra um formulário no Forms Designer.
1. Arraste e solte o campo Scribble de assinatura na página.

   ![designer_scribble](assets/designer_scribble.png)

   >[!NOTE]
   >
   >As dimensões do campo selecionado no Designer de Formulários são refletidas quando o campo é renderizado. No entanto, a dimensão da caixa de assinatura renderizada é calculada com base na proporção do campo, e não na dimensão especificada no Designer de Formulários.

1. Configure o campo Signature Scribble.

   O campo Scribble de assinatura, por padrão, marca as informações de geolocalização como obrigatórias durante o processo de assinatura no iPad (e é opcional em outros dispositivos). Esse comportamento padrão pode ser substituído pela alteração do valor da `geoLocMandatoryOnIpad` propriedade. Essa propriedade é exposta como extras no campo Scribble de assinatura. As etapas para modificá-la são:

   1. No formulário, selecione o campo Scribble de assinatura.
   1. Selecione a guia Origem **** XML.

      >[!NOTE]
      >
      >Para abrir a guia Origem XML, clique em **Visualização** > Fonte **** XML.

   1. Localize a `<ui>` tag na `<field>` tag e modifique o código-fonte para que se pareça com o seguinte:

      ```xml
      <extras name="x-scribble-add-on">
      <boolean name="geoLocMandatoryOnIpad">0</boolean>
      </extras>
      ```

   1. Selecione a guia **Visualização** de design. Na caixa de confirmação, clique em **Sim**.
   1. Salve o formulário.

1. Renderize o formulário em um navegador de dispositivo/área de trabalho compatível.

## Interface com as assinaturas Scribble {#interfacing-with-the-scribble-signatures}

### Signing {#signing}

Depois que um campo Scribble de assinatura for adicionado ao formulário e renderizado, clicar ou tocar no campo abrirá uma caixa de diálogo. O usuário pode escrever uma assinatura na área de desenho designada por um retângulo pontilhado, usando um mouse, dedo ou caneta.

![geolocalização](assets/geolocation.png)

**A.** Pincel **B.** Borracha **C.** Geolocation **D.** Informações sobre geolocalização

### Marcação geográfica {#geo-tagging}

Clicar no ícone de geolocalização ao criar o script faz com que as informações de localização geográfica e hora sejam incorporadas ao campo.

>[!NOTE]
No iPad, por padrão, a incorporação de informações de geolocalização é obrigatória.

No iPad, o ícone de geolocalização não é exibido por padrão, e as informações de geolocalização são incorporadas automaticamente quando você clica em **OK**.

Para iPads, essa configuração pode ser alterada modificando-se o valor do `geoLocManadatoryOnIpad` parâmetro para `0`, nos parâmetros de inicialização do campo.

* Quando a informação de geolocalização é obrigatória, o usuário recebe uma área de desenho reduzida. O texto de geolocalização é adicionado quando o usuário clica no ícone **OK** na área restante.
* Em outros casos, é apresentada ao usuário uma área de desenho completa. Se o usuário optar por incorporar informações de geolocalização, essa área será redimensionada para acomodar o texto da geolocalização.

### Limpando uma assinatura {#clearing-a-signature}

Ao usar esse recurso, um usuário pode clicar no ícone **Borracha** para limpar o campo e start sobre ele. Se as informações de geolocalização forem adicionadas, também serão limpas.

### Salvar uma assinatura {#saving-a-signature}

Clicar no ícone **OK** salva o script como uma imagem no campo. A imagem e os valores podem ser enviados ao servidor para processamento adicional. Depois que um usuário clicar em **OK**, o campo de script será bloqueado. A assinatura não pode ser editada novamente usando o widget de script.

Tocar ou clicar no campo Script abre a caixa de diálogo no modo somente leitura.

![3](assets/3.png)

### Seleção do tamanho da caneta {#selecting-pen-size}

Clique no ícone **Pincéis** para exibir uma lista de tamanhos de caneta disponíveis. Clique ou toque no tamanho da caneta para usar a caneta correspondente.

### Excluir assinaturas do formulário {#delete-signatures-from-the-form}

Para excluir as assinaturas do formulário:

* (Dispositivos móveis) Pressione por muito tempo o campo de assinatura e, na caixa de diálogo de confirmação, toque em **Sim**.
* (Desktop) Passe o mouse sobre o campo de assinatura, clique no ícone **Cancelar** e, na caixa de diálogo de confirmação, clique em **Sim**.
