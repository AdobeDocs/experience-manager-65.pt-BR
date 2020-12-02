---
title: Configuração para aplicativos AEM
seo-title: Configuração para aplicativos AEM
description: Saiba como configurar AEM aplicativos.
seo-description: Saiba como configurar AEM aplicativos.
uuid: ab9acd93-da7f-4bb7-8d26-224044899068
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 34f24837-f5e2-41f0-a359-fdb695e1b8f2
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Configuração para aplicativos AEM{#configuring-for-aem-apps}

Os aplicativos Adobe Experience Manager fornecem a capacidade de atualizar o conteúdo do seu aplicativo pelo ar (OTA). O conteúdo atualizado é armazenado na instância de publicação. Para permitir que o aplicativo em seu dispositivo se conecte à instância de publicação e verifique se há atualizações, a instância de publicação precisa ser configurada para permitir um cabeçalho de quem indicou vazio.

## Configuração do cabeçalho de Quem indicou vazio {#configuring-empty-referrer-header}

Para configurar o serviço de filtro de quem indicou:

* Abra o console do Apache Felix (**Configurações**) em:
* https://&lt;servidor>:&lt;número_porta>/system/console/configMgr
* Faça logon como administrador.
* No menu **Configurações**, selecione: *Filtro de Quem indicou Sling do Apache*
* Marque o campo Permitir vazio para permitir cabeçalhos de quem indicou vazios/ausentes.
* Clique em **Salvar** para salvar as alterações.

![chlimage_1-58](assets/chlimage_1-58a.png)

Consulte [Configurações de OSGI](/help/sites-deploying/osgi-configuration-settings.md) e [Lista de verificação de segurança - Problemas com a falsificação de solicitação entre sites](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) para obter mais detalhes.
