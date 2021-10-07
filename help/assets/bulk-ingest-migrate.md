---
title: Instale o feature pack 18912 para migração de ativos em massa
description: O Feature Pack 18912 permite assimilar ativos em massa por FTP ou migrar ativos do Dynamic Media Classic para o Dynamic Media no Adobe Experience Manager. Este pacote de recursos opcional está disponível no suporte ao Adobe.
uuid: 45c2f5f8-4368-4d7b-a43e-fe96cfb272fd
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 5d5eebe4-46c9-4028-9354-c5f27944fcdc
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
source-git-commit: b2faf81983216bef9151548d90ae86f1c26a9f91
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Instale o feature pack 18912 para migração de ativos em massa{#installing-feature-pack-for-bulk-asset-migration}

A instalação do pacote de recursos 18912 é *opcional*.

O Feature Pack 18912 permite assimilar ativos em massa diretamente no modo Dynamic Media - Scene7 no Adobe Experience Manager por meio de FTP. Também permite migrar ativos do Dynamic Media Classic para o modo Dynamic Media - Scene7 no Experience Manager. O pacote de recursos está disponível em [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>É possível usar o pacote de recursos para migrar ativos em massa por conta própria do Dynamic Media Classic para o Dynamic Media - modo Scene7 no Experience Manager. Também é possível migrar ativos em massa usando o recurso FTP no Dynamic Media Classic. No entanto, o Adobe *not* recomenda que você use qualquer um desses métodos devido à complexidade envolvida.
>
>Dessa forma, esse pacote de recursos de migração é compatível *somente* como parte de um projeto de migração quando feito por meio de [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Antes de instalar o feature pack, crie um usuário de serviço e forneça essas informações para o suporte ao Adobe.

Consulte também [Configurar Dynamic Media - Modo Scene7](/help/assets/config-dms7.md).

**Para instalar o feature pack 18912 para a migração de ativos em massa:**

1. Na instância do Experience Manager, navegue até **[!UICONTROL Ferramenta]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]** e selecione **[!UICONTROL Criar Usuário]**. Este usuário de serviço deve ter permissões *read/write* para `/content/dam.`
1. Nos campos **[!UICONTROL ID]** e **[!UICONTROL Senha]**, digite um nome de usuário e uma senha; por exemplo, **Usuário FTP**. Esse nome aparece na linha do tempo como o usuário que criou o ativo. Quando um ativo é carregado a partir do FTP, um ativo é considerado criado quando é carregado no servidor FTP e é enviado para o Experience Manager.
1. Entre em contato com o [Adobe Customer Support for Experience Manager](https://experienceleague.adobe.com/?support-solution=General#support) para solicitar acesso ao feature pack 18912 para download. Você pode precisar das seguintes informações quando entrar em contato com o suporte:

   * Endereço IP do servidor para a instância do Autor, incluindo o número da porta (por padrão, o número da porta é 4502.)
   * Nome de usuário e senha do serviço Experience Manager da etapa anterior.

1. O Suporte ao cliente do Adobe para Experience Manager fornece as credenciais do FTP e o acesso ao feature pack 18912.
1. Quando receber o feature pack 18912, instale-o.

   Consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md) para obter mais informações sobre como usar a Distribuição de software e os pacotes no Experience Manager.
