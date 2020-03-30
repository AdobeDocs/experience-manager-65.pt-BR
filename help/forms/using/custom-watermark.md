---
title: Marca d'água personalizada na pré-visualização PDF carta
seo-title: Marca d'água personalizada na pré-visualização PDF carta
description: Saiba como criar uma marca d'água personalizada na pré-visualização PDF carta.
seo-description: Saiba como criar uma marca d'água personalizada na pré-visualização PDF carta.
uuid: 5adfede3-9b38-4a12-bf14-6d80cfb0a05a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: adc7ec13-0675-4071-9c4c-e238202d9d85
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Marca d&#39;água personalizada na pré-visualização PDF carta{#custom-watermark-in-letter-pdf-preview}

## Visão geral {#overview}

Na interface do usuário Criar correspondência, os usuários agentes pré-visualizações a correspondência na forma final em que é enviada para o processamento de postagens, como para e-mail ou impressão.

Para impedir o uso não autorizado desses dados, as organizações podem impor uma marca d&#39;água no PDF da pré-visualização. A marca d&#39;água padrão é &quot;PRÉ-VISUALIZAÇÃO&quot;, que aparece no PDF.

Para ativar a marca d&#39;água no PDF da pré-visualização, selecione a opção **[!UICONTROL Aplicar marca d&#39;água]** durante a Pré-visualização em Configurações **[!UICONTROL de gerenciamento de]** correspondência em https://&#39;[server]:[port]&#39;/system/console/configMgr.

![marca d&#39;água padrão](assets/default-watermark.png)

Você pode usar as seguintes etapas para personalizar o texto e a aparência da marca d&#39;água:

## Personalizar a marca d&#39;água na pré-visualização PDF na interface Criar correspondência {#customizewatermark-}

1. Vá para `https://'[server]:[port]'/[ContextPath]/crx/de` e faça logon como Administrador.
1. Na pasta apps, crie uma pasta chamada **[!UICONTROL pré-marca d&#39;água]** com caminho/estrutura semelhante à pasta de marca d&#39;água da visualização na pasta libs:

   1. Clique com o botão direito do mouse na pasta de marca d&#39;água **da** visualização no seguinte caminho e selecione **Sobrepor nó**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. Certifique-se de que a caixa de diálogo Sobrepor nó tenha os seguintes valores:

      **Caminho:** /libs/fd/cm/configFiles/previewwatermark

      **Localização da sobreposição:** /apps/

      **Corresponder tipos de nós:** Verificado

      >[!NOTE]
      >
      >Não faça alterações na ramificação /libs. Quaisquer alterações feitas podem ser perdidas, pois essa ramificação está sujeita a alterações sempre que você:
      >
      >    
      >    
      >    * Atualizar na sua instância
      >    * Aplicar uma correção
      >    * Instalar um pacote de recursos


   1. Clique em **OK** e em **Salvar tudo**. A pasta de marca d&#39;água **[!UICONTROL da]** visualização é criada no caminho especificado.



1. Copie e cole o arquivo dx da pasta &quot;/libs/fd/cm/configFiles/previewwatermark&quot; para a pasta &quot;/apps/fd/cm/configFiles/previewwatermark&quot; e clique em **[!UICONTROL Salvar tudo]**.
1. Faça as alterações desejadas no arquivo ddx em /apps/fd/cm/configFiles/previewwatermark/.

   ```
   <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
    <PDF result="output.pdf">
     <PDF source="input.pdf"/>
           <Watermark opacity="15%" rotation="45">
            <StyledText>
                     <p font-family="Georgia" font-size="70pt" color="black" font-weight="bold">
                         PREVIEW
                    </p>
            </StyledText>
           </Watermark>
    </PDF>
   </DDX>
   ```

   Para obter informações sobre como personalizar a aparência da marca d&#39;água, o texto e o alinhamento, consulte Adicionar e remover marcas d&#39;água e planos de fundo no [Assembler Service e no documento de referência](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) DDX.

   >[!NOTE]
   >
   >No arquivo ddx, as referências ao resultado e à fonte devem permanecer inalteradas para output.pdf e input.pdf. O nome do arquivo ddx também não deve ser alterado.

1. Clique em **Salvar tudo**.

