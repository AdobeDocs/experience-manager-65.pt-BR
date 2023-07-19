---
title: Aplicativo de desktop AEM para AEM Forms
seo-title: AEM desktop app for AEM Forms
description: Aplicativo de desktop AEM para AEM Forms
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
role: Admin
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Aplicativo de desktop AEM para AEM Forms {#aem-desktop-app-for-aem-forms}

O aplicativo de desktop AEM permite mapear o repositório de ativos do Adobe Experience Manager (AEM) e os arquivos binários do AEM Forms para um diretório de rede no sistema. Você pode exibir os ativos sincronizados e os arquivos binários em um explorador de arquivos e usar vários aplicativos para editar os arquivos conforme desejado. Além de visualizar os arquivos, você também pode criar, fazer upload e excluir os arquivos binários. Você também pode abrir, editar e salvar arquivos diretamente do software. Por exemplo, você pode abrir e editar um arquivo XDP diretamente do Designer. As alterações feitas nos ativos localmente são refletidas no repositório do AEM Assets e na interface do usuário do AEM Forms.

Você pode baixar o aplicativo de uma instância AEM. Para obter informações detalhadas sobre como baixar o aplicativo, consulte [Notas de versão do aplicativo para desktop AEM](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html).

## ativos do AEM Forms compatíveis com o aplicativo de desktop AEM {#aem-forms-assets-supported-in-aem-desktop-app}

Você pode usar o aplicativo para sincronizar arquivos binários AEM Forms dos seguintes tipos: Modelos de formulário (.xdp), Formulário PDF (.pdf), Documento (.pdf), Imagens, Esquema XML (.xsd), Folhas de estilos (.xfs). O aplicativo lista todos os outros arquivos (arquivos não compatíveis) como arquivos de 0 byte. Listar arquivos não compatíveis como arquivos de 0 byte garante que o usuário esteja ciente da existência de outros ativos disponíveis no servidor do AEM Forms.

>[!NOTE]
>
>Um nome de arquivo só pode conter caracteres alfanuméricos, hífen ou sublinhado.

## Ativar o aplicativo de desktop AEM Forms para AEM {#enable-aem-forms-for-aem-desktop-app}

O aplicativo de desktop AEM usa o protocolo WebDAV no Microsoft Windows e o SMB1 no Mac OS X para se conectar a um servidor AEM Forms. Pronto para uso, o servidor do AEM Forms não é habilitado para sincronizar arquivos binários e outros ativos com um cliente WebDAV ou SMB. Execute as seguintes etapas para habilitar o aplicativo de desktop AEM Forms para AEM:

1. Faça logon no AEM Forms como administrador.
1. Na instância do autor, clique em ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Ferramentas]** ![martelo](assets/hammer.png) **[!UICONTROL > Implantação > Operações > Console da Web]**. O Console da Web é aberto em uma nova janela.
1. Na janela do console da Web, localize e abra o **[!UICONTROL Configuração de complemento do FormsManager]** opção.
1. Na caixa de diálogo Configuração de complemento do FormsManager, desmarque a **[!UICONTROL Sincronizar recursos de forma assíncrona]** e clique em **[!UICONTROL Salvar]**.
1. Reinicie o servidor do AEM Forms. Após a reinicialização, o servidor do AEM Forms é ativado para aceitar e compartilhar conteúdo com o aplicativo para desktop AEM.
1. Abra o aplicativo e conecte-se ao servidor do AEM Forms.

   Ao se conectar com êxito, o aplicativo preenche o `content/dam` e `content/dam/formsanddocuments` pastas. Além de mover arquivos das pastas acima para pastas locais e vice-versa, você pode usar o aplicativo para mover conteúdo entre pastas preenchidas automaticamente.
