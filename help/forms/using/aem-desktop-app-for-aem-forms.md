---
title: Aplicativo de desktop AEM para AEM Forms
seo-title: Aplicativo de desktop AEM para AEM Forms
description: 'null'
seo-description: 'null'
uuid: 99e0f2fb-8623-45bb-8e2e-5c5d6f482366
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
discoiquuid: c30332b6-e012-442d-8e84-28832c116c7b
noindex: true
translation-type: tm+mt
source-git-commit: 3460909eb77cc078b728d1af4becd47cc4377b73

---


# Aplicativo de desktop AEM para AEM Forms {#aem-desktop-app-for-aem-forms}

O aplicativo de desktop AEM permite que você mapeie o repositório do Adobe Experience Manager (AEM) Assets e os arquivos binários do AEM Forms para um diretório de rede no seu sistema. Você pode exibir os ativos sincronizados e os arquivos binários em um explorador de arquivos e usar vários aplicativos para editar os arquivos conforme desejado. Além de exibir os arquivos, você também pode criar, carregar e excluir os arquivos binários. Você também pode abrir, editar e salvar arquivos diretamente do software. Por exemplo, você pode abrir e editar diretamente um arquivo XDP do Designer. As alterações feitas nos ativos localmente são refletidas no repositório do AEM Assets e na interface do usuário do AEM Forms.

Você pode baixar o aplicativo de uma instância do AEM. Para obter informações detalhadas sobre como baixar o aplicativo, consulte Notas [de versão do aplicativo para desktop do](https://helpx.adobe.com/experience-manager/desktop-app/release-notes.html)AEM.

## Ativos do AEM Forms com suporte no aplicativo de desktop do AEM {#aem-forms-assets-supported-in-aem-desktop-app}

Você pode usar o aplicativo para sincronizar arquivos binários do AEM Forms do seguinte tipo Modelos de formulário (.xdp), Formulário PDF (.pdf), Documento (.pdf), Imagens, Esquema XML (.xsd), folhas de estilos (.xfs). O aplicativo lista todos os outros arquivos (arquivos sem suporte) como arquivos de 0 byte. A listagem de arquivos não suportados como arquivos de 0 bytes garante que o usuário esteja ciente da existência de outros ativos disponíveis no servidor do AEM Forms.

>[!NOTE]
>
>Um nome de arquivo só pode conter caracteres alfanuméricos, hífen ou sublinhado.

## Ativar o AEM Forms para aplicativo de desktop AEM {#enable-aem-forms-for-aem-desktop-app}

O aplicativo de desktop AEM usa o protocolo WebDAV no Microsoft Windows e SMB1 no Mac OS X para se conectar a um servidor de formulários AEM. O servidor AEM Forms não está habilitado para sincronizar arquivos binários e outros ativos com um cliente WebDAV ou SMB. Execute as seguintes etapas para ativar os formulários AEM para o aplicativo de desktop AEM:

1. Faça logon no AEM Forms como administrador.
1. Na instância do autor, clique em ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager > Ferramentas]** ![martelo](assets/hammer.png) **[!UICONTROL > Implantação > Operações > Console]** da Web. O Console da Web é aberto em uma nova janela.
1. Na janela Console da Web, localize e abra a opção Configuração **[!UICONTROL do complemento]** FormsManager.
1. Na caixa de diálogo Configuração do complemento do FormsManager, desmarque a caixa de seleção Recursos **[!UICONTROL de sincronização]** assíncrona e clique em **[!UICONTROL Salvar]**.
1. Reinicie o servidor do AEM Forms. Após a reinicialização, o servidor do AEM Forms é habilitado a aceitar e compartilhar conteúdo com aplicativos de desktop do AEM.
1. Abra o aplicativo e conecte-se ao servidor do AEM Forms.

   Na conexão bem-sucedida, o aplicativo preenche as pastas `content/dam` e `content/dam/formsanddocuments` . Juntamente com a movimentação de arquivos de pastas acima para pastas locais e vice-versa, você pode usar o aplicativo para mover o conteúdo entre pastas preenchidas automaticamente.

