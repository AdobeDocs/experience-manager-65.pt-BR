---
title: AEM aplicativo de desktop para AEM Forms
seo-title: AEM desktop app for AEM Forms
description: AEM aplicativo de desktop para AEM Forms
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
role: Admin
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# AEM aplicativo de desktop para AEM Forms {#aem-desktop-app-for-aem-forms}

AEM aplicativo de desktop permite mapear o repositório do Adobe Experience Manager (AEM) Assets e os arquivos binários do AEM Forms para um diretório de rede no seu sistema. Você pode exibir os ativos sincronizados e os arquivos binários em um gerenciador de arquivos e usar vários aplicativos para editar os arquivos, conforme desejado. Além de visualizar os arquivos, você também pode criar, carregar e excluir os arquivos binários. Também é possível abrir, editar e salvar arquivos diretamente do software. Por exemplo, é possível abrir e editar diretamente um arquivo XDP no Designer. As alterações feitas nos ativos localmente são refletidas no repositório do AEM Assets e na interface do usuário do AEM Forms.

Você pode baixar o aplicativo de uma instância do AEM. Para obter informações detalhadas sobre como baixar o aplicativo, consulte [Notas de versão do aplicativo de desktop do AEM](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html).

## Ativos da AEM Forms compatíveis com AEM aplicativo de desktop {#aem-forms-assets-supported-in-aem-desktop-app}

Você pode usar o aplicativo para sincronizar arquivos binários do AEM Forms dos seguintes tipos de Modelos de formulário (.xdp), Formulário PDF (.pdf), Documento (.pdf), Imagens, Esquema XML (.xsd), folhas de estilos (.xfs). O aplicativo lista todos os outros arquivos (arquivos não compatíveis) como arquivos de 0 bytes. Listar arquivos não suportados como arquivos de 0 bytes garante que o usuário esteja ciente da existência de outros ativos disponíveis no servidor do AEM Forms.

>[!NOTE]
>
>Um nome de arquivo só pode conter caracteres alfanuméricos, hífen ou sublinhado.

## Ativar o AEM Forms para AEM aplicativo de desktop {#enable-aem-forms-for-aem-desktop-app}

AEM aplicativo de desktop usa o protocolo WebDAV no Microsoft Windows e SMB1 no Mac OS X para se conectar a um servidor AEM Forms. Pronto para uso, o servidor AEM Forms não é habilitado para sincronizar arquivos binários e outros ativos com um cliente WebDAV ou SMB. Execute as seguintes etapas para ativar o AEM Forms para AEM aplicativo de desktop:

1. Faça logon no AEM Forms como administrador.
1. Na instância do autor, clique em ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Ferramentas]** ![martelo](assets/hammer.png) **[!UICONTROL > Implantação > Operações > Console da Web]**. O Console da Web é aberto em uma nova janela.
1. Na janela do console da Web, localize e abra o **[!UICONTROL Configuração do complemento FormsManager]** opção.
1. Na caixa de diálogo Configuração do complemento FormsManager , desmarque a opção **[!UICONTROL Sincronizar recursos de forma assíncrona]** e clique em **[!UICONTROL Salvar]**.
1. Reinicie o servidor do AEM Forms. Após a reinicialização, o servidor do AEM Forms é habilitado para aceitar e compartilhar conteúdo com AEM aplicativo de desktop.
1. Abra o aplicativo e conecte-se ao servidor do AEM Forms.

   Ao se conectar com êxito, o aplicativo preenche a variável `content/dam` e `content/dam/formsanddocuments` pastas. Juntamente com a movimentação de arquivos das pastas acima para pastas locais e vice-versa, é possível usar o aplicativo para mover o conteúdo entre pastas preenchidas automaticamente.
