---
title: Instalar o pacote de recursos 18912 para migração de ativos em massa
description: O Feature Pack 18912 permite assimilar ativos em massa por meio do FTP ou migrar ativos do Dynamic Media Classic para o Dynamic Media no Adobe Experience Manager. Este pacote de recursos opcional está disponível no suporte para Adobe.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Instalar o pacote de recursos 18912 para migração de ativos em massa{#installing-feature-pack-for-bulk-asset-migration}

A instalação do pacote de recursos 18912 é *opcional*.

O Feature Pack 18912 permite assimilar ativos em massa diretamente no modo Dynamic Media - Scene7 no Adobe Experience Manager por meio do FTP. Ela também permite migrar ativos do Dynamic Media Classic para o modo Dynamic Media - Scene7 no Experience Manager. O pacote de recursos está disponível no [Adobe Professional Services](https://business.adobe.com/br/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>É possível usar o pacote de recursos para migrar ativos em massa por conta própria do Dynamic Media Classic para o modo Dynamic Media - Scene7 no Experience Manager. Também é possível migrar ativos em massa usando o recurso de FTP na Dynamic Media Classic. No entanto, o Adobe *não* recomenda o uso de qualquer um desses métodos devido à complexidade envolvida.
>
>Sendo assim, este pacote de recursos de migração tem *suporte apenas* como parte de um projeto de migração quando concluído por meio do [Adobe Professional Services](https://business.adobe.com/br/customers/consulting-services/main.html).

Antes de instalar o pacote de recursos, crie um usuário de serviço e forneça essas informações ao suporte do Adobe.

Consulte também [Configurar Dynamic Media - Modo Scene7](/help/assets/config-dms7.md).

**Para instalar o pacote de recursos 18912 para migração de ativos em massa:**

1. Na sua instância do Experience Manager, navegue até **[!UICONTROL Ferramenta]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]** e selecione **[!UICONTROL Criar Usuário]**. Este usuário do serviço deve ter *permissões de leitura/gravação* para `/content/dam.`
1. Nos campos **[!UICONTROL ID]** e **[!UICONTROL Senha]**, digite um nome de usuário e senha; por exemplo, **Usuário FTP**. Esse nome aparece na linha do tempo como o usuário que criou o ativo. Quando um ativo é carregado do FTP, um ativo é considerado criado quando é carregado no servidor FTP e é enviado para o Experience Manager.
1. Entre em contato com o Suporte ao Cliente do [Adobe para obter o Experience Manager](https://experienceleague.adobe.com/pt-br?support-solution=General#support) e solicitar acesso ao pacote de recursos 18912 para download. Talvez você precise das seguintes informações ao entrar em contato com o suporte:

   * Endereço IP do servidor para a instância do autor, incluindo o número da porta (por padrão, o número da porta é 4502).
   * Nome de usuário e senha do serviço Experience Manager da etapa anterior.

1. O Suporte ao cliente do Adobe para Experience Manager fornece as credenciais de FTP e acesso ao pacote de recursos 18912.
1. Ao receber o pacote de recursos 18912, instale-o.

   Consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md) para obter mais informações sobre como usar a Distribuição de software e pacotes no Experience Manager.
