---
title: Configuração para aplicativos AEM
seo-title: Configuring for AEM Apps
description: Saiba como configurar AEM aplicativos.
seo-description: Learn how to configure AEM Apps.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Configuração para aplicativos AEM{#configuring-for-aem-apps}

Os aplicativos Adobe Experience Manager oferecem a capacidade de atualizar o conteúdo do aplicativo ao ar (OTA). O conteúdo atualizado é armazenado na instância de publicação. Para permitir que o aplicativo em seu dispositivo se conecte à instância de publicação e verifique se há atualizações, a instância de publicação precisa ser configurada para permitir um cabeçalho de referenciador vazio.

## Configuração do Cabeçalho do Referenciador Vazio {#configuring-empty-referrer-header}

Para configurar o serviço de filtro do referenciador:

* Abra o console do Apache Felix (**Configurações**) em:
* https://&lt;server>:&lt;port_number>/system/console/configMgr
* Faça logon como administrador.
* No **Configurações** selecione: *Filtro de referenciador do Apache Sling*
* Marque o campo Permitir vazio para permitir cabeçalhos de referenciador vazios/ausentes.
* Clique em **Salvar** para salvar as alterações.

![chlimage_1-58](assets/chlimage_1-58a.png)

Consulte a [Configurações de OSGI](/help/sites-deploying/osgi-configuration-settings.md) e [Lista de verificação de segurança - Problemas com a falsificação de solicitação entre sites](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) para obter mais detalhes.
