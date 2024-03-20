---
title: Marca d'água personalizada na visualização de PDF da carta
description: Saiba como criar uma marca d'água personalizada na pré-visualização de PDF de correspondência.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 7d90fade-1ca4-41d8-bbf9-45490465784a
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Marca d&#39;água personalizada na visualização de PDF da carta{#custom-watermark-in-letter-pdf-preview}

## Visão geral {#overview}

Na interface Criar correspondência, os usuários do agente visualizam a correspondência na forma final na qual é enviada para pós-processamento, como para email ou impressão.

Para evitar o uso não autorizado desses dados, as organizações podem impor uma marca d&#39;água na PDF de visualização. A marca d&#39;água padrão é &quot;PRÉ-VISUALIZAÇÃO&quot;, que aparece no PDF.

Para ativar a marca d&#39;água no PDF de pré-visualização, selecione o **[!UICONTROL Aplicar marca d&#39;água]** Durante a opção de Visualização em **[!UICONTROL Configurações do gerenciamento de correspondência]** em https://&#39;[server]:[porta]&#39;/system/console/configMgr.

![default-watermark](assets/default-watermark.png)

Você pode usar as seguintes etapas para personalizar o texto e a aparência da marca d&#39;água:

## Personalizar a marca d&#39;água na visualização do PDF na interface de Criar correspondência {#customizewatermark-}

1. Ir para `https://'[server]:[port]'/[ContextPath]/crx/de` e faça logon como Administrador.
1. Na pasta de aplicativos, crie uma pasta chamada **[!UICONTROL previewwatermark]** com caminho/estrutura semelhante à pasta previewwatermark na pasta libs:

   1. Clique com o botão direito do mouse no **previewwatermark** no seguinte caminho e selecione **Sobrepor nó**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. Certifique-se de que a caixa de diálogo Sobrepor nó tenha os seguintes valores:

      **Caminho:** /libs/fd/cm/configFiles/previewwatermark

      **Local da sobreposição:** /apps/

      **Corresponder Tipos de Nó:** Marcado

      >[!NOTE]
      >
      >Não faça alterações na ramificação /libs. As alterações feitas podem ser perdidas, pois essa ramificação pode sofrer alterações sempre que você:
      >
      >    
      >    
      >    * Atualizar na sua instância
      >    * Aplicar um hot fix
      >    * Instalar um pacote de recursos
      >    
      >

   1. Clique em **OK** e clique em **Salvar tudo**. A variável **[!UICONTROL previewwatermark]** a pasta é criada no caminho especificado.

1. Copie e cole o arquivo ddx da pasta &quot;/libs/fd/cm/configFiles/previewwatermark&quot; para a pasta &quot;/apps/fd/cm/configFiles/previewwatermark&quot; e clique em **[!UICONTROL Salvar tudo]**.
1. Faça as alterações desejadas no arquivo ddx em /apps/fd/cm/configFiles/previewwatermark/.

   ```xml
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

   Para obter informações sobre como personalizar a aparência, o texto e o alinhamento da marca d&#39;água, consulte Adição e remoção de marcas d&#39;água e planos de fundo na [Serviço de Assembler e Referência DDX](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf) documento.

   >[!NOTE]
   >
   >No arquivo ddx, as referências ao resultado e à fonte devem permanecer inalteradas para output.pdf e input.pdf. O nome do arquivo ddx também não deve ser alterado.

1. Clique em **Salvar tudo**.
