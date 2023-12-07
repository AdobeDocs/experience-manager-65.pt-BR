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
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Instalar o pacote de recursos 18912 para migração de ativos em massa{#installing-feature-pack-for-bulk-asset-migration}

A instalação do pacote de recursos 18912 é *opcional*.

O Feature Pack 18912 permite assimilar ativos em massa diretamente no modo Dynamic Media - Scene7 no Adobe Experience Manager por meio do FTP. Ela também permite migrar ativos do Dynamic Media Classic para o modo Dynamic Media - Scene7 no Experience Manager. O pacote de recursos está disponível em [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

>[!IMPORTANT]
>
>É possível usar o pacote de recursos para migrar ativos em massa por conta própria do Dynamic Media Classic para o modo Dynamic Media - Scene7 no Experience Manager. Também é possível migrar ativos em massa usando o recurso de FTP na Dynamic Media Classic. No entanto, o Adobe *não* recomendamos que você use qualquer um desses métodos devido à complexidade envolvida.
>
>Sendo assim, este pacote de recursos de migração é *somente* compatível como parte de um projeto de migração quando concluído por meio de [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Antes de instalar o pacote de recursos, crie um usuário de serviço e forneça essas informações ao suporte do Adobe.

Consulte também [Configurar o modo Dynamic Media - Scene7](/help/assets/config-dms7.md).

**Para instalar o pacote de recursos 18912 para migração de ativos em massa:**

1. Na instância do Experience Manager, navegue até **[!UICONTROL Ferramenta]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]** e selecione **[!UICONTROL Criar usuário]**. Este usuário do serviço deve ter *leitura/gravação* permissões para `/content/dam.`
1. No **[!UICONTROL ID]** e **[!UICONTROL Senha]** insira um nome de usuário e senha; por exemplo, **Usuário FTP**. Esse nome aparece na linha do tempo como o usuário que criou o ativo. Quando um ativo é carregado do FTP, um ativo é considerado criado quando é carregado no servidor FTP e é enviado para o Experience Manager.
1. Contato [Suporte ao cliente Adobe para Experience Manager](https://experienceleague.adobe.com/?support-solution=General&amp;lang=pt-BR#support) para solicitar acesso ao pacote de recursos 18912 para download. Talvez você precise das seguintes informações ao entrar em contato com o suporte:

   * Endereço IP do servidor para a instância do autor, incluindo o número da porta (por padrão, o número da porta é 4502).
   * Nome de usuário e senha do serviço Experience Manager da etapa anterior.

1. O Suporte ao cliente do Adobe para Experience Manager fornece as credenciais de FTP e acesso ao pacote de recursos 18912.
1. Ao receber o pacote de recursos 18912, instale-o.

   Consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md) para obter mais informações sobre o uso de Distribuição de software e pacotes no Experience Manager.
