---
title: Instalando o feature pack 18912 para a migração de ativos em massa
description: O Feature Pack 18912 permite assimilar ativos em massa por FTP ou migrar ativos do Dynamic Media Classic para o Dynamic Media no AEM. Este pacote de recursos opcional está disponível no suporte ao Adobe.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Asset Management
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Instalando o pacote de recursos 18912 para migração de ativos em massa{#installing-feature-pack-for-bulk-asset-migration}

A instalação do pacote de recursos 18912 é *opcional*.

O Feature Pack 18912 permite assimilar ativos em massa diretamente no modo Dynamic Media - Scene7 no AEM por meio de FTP ou migrar ativos do Dynamic Media Classic para o modo Dynamic Media - Scene7 no AEM. O pacote de recursos está disponível em [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

>[!NOTE]
>
>Embora seja possível usar o pacote de recursos para migrar ativos em massa por conta própria do Dynamic Media Classic para o Dynamic Media - Scene7 no modo AEM ou migrar ativos em massa usando o recurso FTP no Dynamic Media Classic, o Adobe *não* recomenda esse método devido à complexidade envolvida.
>
>Dessa forma, os pacotes de recursos de migração, como este, são *compatíveis somente* como parte de um projeto de migração quando feitos por meio de [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html).

Antes de instalar o feature pack, primeiro crie um usuário de serviço e forneça essas informações para o suporte do Adobe.

Consulte também [Configuração do Dynamic Media - Modo Scene7](/help/assets/config-dms7.md).

**Para instalar o feature pack 18912 para migração de ativos em massa**

1. Na instância de AEM, navegue até **[!UICONTROL Ferramentas > Segurança > Usuários]** e selecione **[!UICONTROL Criar usuário]**. Este usuário de serviço deve ter permissões *read/write* para `/content/dam.`
1. Nos campos **[!UICONTROL ID]** e **[!UICONTROL Senha]**, digite um nome de usuário e uma senha; por exemplo, **Usuário FTP**. Esse nome aparece na linha do tempo como o usuário que criou o ativo. Quando um ativo é carregado a partir do FTP, um ativo é considerado criado quando é carregado no servidor FTP e é enviado ao AEM.
1. Entre em contato com o [Adobe Enterprise Customer Care for Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support) para solicitar acesso ao feature pack 18912 para download. Você pode precisar das seguintes informações quando entrar em contato com o suporte:

   * Endereço IP do servidor para a instância do Autor, incluindo o número da porta (por padrão, o número da porta é 4502.)
   * AEM nome de usuário do serviço e senha da etapa anterior.

1. O Atendimento ao cliente da Adobe Enterprise para AEM fornece as credenciais do FTP e o acesso ao feature pack 18912.
1. Quando receber o feature pack 18912, instale-o.

   Consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md) para obter mais informações sobre como usar a Distribuição de software e pacotes no AEM.
