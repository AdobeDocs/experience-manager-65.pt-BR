---
title: Instalação do pacote de recursos 18912 para migração de ativos em massa
description: O pacote de recursos 18912 permite que você ingira ativos em massa por meio de FTP ou migre ativos do Dynamic Media Classic para Dynamic Media no AEM. Este pacote opcional de recursos está disponível no suporte da Adobe.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Instalação do pacote de recursos 18912 para migração de ativos em massa{#installing-feature-pack-for-bulk-asset-migration}

A instalação do pacote de recursos 18912 é *opcional*.

O pacote de recursos 18912 permite que você ingira ativos em massa diretamente no Dynamic Media - modo Scene7 no AEM por meio de FTP ou migre ativos do Dynamic Media Classic para Dynamic Media - modo Scene7 no AEM. O pacote de recursos está disponível no [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

>[!NOTE]
>
>Embora seja possível usar o pacote de recursos para migrar ativos em massa por conta própria do modo Dynamic Media Classic para Dynamic Media - Scene 7 no AEM ou migrar ativos em massa usando o recurso FTP no Dynamic Media Classic, a Adobe *não* recomenda esse método devido à complexidade envolvida.
>
>Dessa forma, os pacotes de recursos de migração, como este, *só* são suportados como parte de um projeto de migração quando realizados por meio dos [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

Antes de instalar o pacote de recursos, você deve primeiro criar um usuário de serviço e fornecer essas informações ao suporte da Adobe.

Consulte também [Configuração do Dynamic Media - Modo](/help/assets/config-dms7.md)Scene7.

**Para instalar o pacote de recursos 18912 para migração de ativos em massa**

1. Em sua instância do AEM, navegue até **[!UICONTROL Ferramentas > Segurança > Usuários]** e selecione **[!UICONTROL Criar usuário]**. Este usuário do serviço deve ter permissões de *leitura/gravação* para `/content/dam.`
1. Nos campos **[!UICONTROL ID]** e **[!UICONTROL senha]** , digite um nome de usuário e uma senha; por exemplo, Usuário **** FTP. Esse nome aparece na linha do tempo como o usuário que criou o ativo. Quando um ativo é carregado do FTP, um ativo é considerado criado quando é carregado no servidor FTP e enviado para o AEM.
1. Entre em contato com o suporte [Adobe Enterprise para o Experience Manager](https://helpx.adobe.com/contact/enterprise-support.ec.html) para solicitar acesso ao pacote de recursos 18912 para download. Você pode precisar das seguintes informações ao entrar em contato com o suporte:

   * Endereço IP do servidor para a instância do autor, incluindo o número da porta (por padrão, o número da porta é 4502).
   * Nome de usuário e senha do serviço AEM da etapa anterior.

1. O suporte empresarial da Adobe para o AEM fornece as credenciais FTP e o acesso ao pacote de recursos 18912.
1. Quando receber o pacote de recursos 18912, instale-o.

   Consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md) para obter mais informações sobre como usar o Compartilhamento de pacotes e pacotes no AEM.

