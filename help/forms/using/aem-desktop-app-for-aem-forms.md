---
title: aplicativo de desktop Adobe Experience Manager (AEM) para AEM Forms
description: aplicativo de desktop Adobe Experience Manager (AEM) para AEM Forms
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
noindex: true
role: Admin
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# aplicativo de desktop Adobe Experience Manager (AEM) para AEM Forms {#aem-desktop-app-for-aem-forms}

O aplicativo de desktop AEM permite mapear o repositório de ativos do Adobe Experience Manager (AEM) e os arquivos binários do AEM Forms para um diretório de rede no sistema. Você pode exibir os ativos sincronizados e os arquivos binários em um explorador de arquivos e usar vários aplicativos para editar os arquivos conforme desejado. Além de visualizar os arquivos, você também pode criar, fazer upload e excluir os arquivos binários. Você também pode abrir, editar e salvar arquivos diretamente do software. Por exemplo, você pode abrir e editar um arquivo XDP diretamente do Designer. As alterações feitas nos ativos localmente são refletidas no repositório do AEM Assets e na interface do usuário do AEM Forms.

Você pode baixar o aplicativo de uma instância AEM. Para obter informações detalhadas sobre como baixar o aplicativo, consulte [Notas de versão do aplicativo para desktop AEM](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=en).

## ativos do AEM Forms compatíveis com o aplicativo de desktop AEM {#aem-forms-assets-supported-in-aem-desktop-app}

Você pode usar o aplicativo para sincronizar arquivos binários AEM Forms dos seguintes tipos: Modelos de formulário (.xdp), Formulário PDF (.pdf), Documento (.pdf), Imagens, Esquema XML (.xsd), Folhas de estilos (.xfs). O aplicativo lista todos os outros arquivos (arquivos não compatíveis) como arquivos de 0 byte. Listar arquivos não compatíveis como arquivos de 0 byte garante que o usuário esteja ciente da existência de outros ativos disponíveis no servidor do AEM Forms.

>[!NOTE]
>
>Um nome de arquivo só pode conter caracteres alfanuméricos, hífen ou sublinhado.

## Ativar o aplicativo de desktop AEM Forms para AEM {#enable-aem-forms-for-aem-desktop-app}

O aplicativo de desktop AEM usa o protocolo WebDAV no Microsoft® Windows e SMB1 no macOS X para se conectar a um servidor AEM Forms. Pronto para uso, o AEM Forms Server não é habilitado para sincronizar arquivos binários e outros ativos com um cliente WebDAV ou SMB. Execute as seguintes etapas para habilitar o aplicativo de desktop AEM Forms para AEM:

1. Faça logon no AEM Forms como administrador.
1. Na instância do autor, clique em ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Ferramentas]** ![martelo](assets/hammer.png) **[!UICONTROL > Implantação > Operações > Console da Web]**. O Console da Web é aberto em uma nova janela.
1. Na janela do Console da Web, localize e abra o **[!UICONTROL Configuração de complemento do FormsManager]** opção.
1. Na caixa de diálogo Configuração de complemento do FormsManager, desmarque a **[!UICONTROL Sincronizar recursos de forma assíncrona]** e clique em **[!UICONTROL Salvar]**.
1. Reinicie o servidor do AEM Forms. Após a reinicialização, o AEM Forms Server é ativado para aceitar e compartilhar conteúdo com o aplicativo de desktop AEM.
1. Abra o aplicativo e conecte-se ao AEM Forms Server.

   >[!NOTE]
   >
   > É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

   Ao se conectar com êxito, o aplicativo preenche o `content/dam` e `content/dam/formsanddocuments` pastas. Além de mover arquivos das pastas acima para pastas locais e vice-versa, você pode usar o aplicativo para mover conteúdo entre pastas preenchidas automaticamente.
