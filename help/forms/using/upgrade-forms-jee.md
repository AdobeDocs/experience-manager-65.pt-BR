---
title: Atualização para o AEM 6.5 Forms no JEE
description: Você pode executar uma atualização direta do AEM 6.1 Forms, AEM 6.2 Forms e LiveCycle ES4 SP1 para o AEM 6.3 Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin,User
exl-id: 722e75a0-bcb3-465e-bb74-ea94a3b99fd3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms Upgrade,AEM Forms on JEE
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
  - id: d49d6117-dd89-469c-a774-cc96b7eee433
    internal-label: Administration
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: b9cdd520-e7a7-4af9-a95f-296f28882b69
    internal-label: AEM Forms upgrade
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 1%
---
# Atualização para o AEM 6.5 Forms no JEE {#upgrade-to-aem-forms-jee}

O AEM 6.5.18.0 Forms no JEE fornece dois tipos de instaladores: instalador completo e instalador de patch.

**Instalador completo**: você pode usar o [AEM 6.5.18.0 no instalador completo do JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) para configurar novas instâncias do AEM Forms ou executar atualizações do AEM 6.5.x.x Forms no JEE para o AEM 6.5.18.0 Forms no JEE.

O **Instalador de patch**: [AEM 6.5.18.0 no instalador de patch JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) é para clientes que já usam as versões AEM 6.5.x.x. Você pode usar o instalador de patches para atualizar para a versão mais recente do AEM Forms.

A tabela a seguir mostra cenários de uso do instalador de patch e completo.

![Cenário do instalador completo e de patch](assets/full-and-patch-installer.png)

Execute o seguinte procedimento para usar o instalador completo para atualizar o AEM Forms 6.5.x.x existente no JEE para o AEM 6.5.18.0 Forms no JEE:

1. Baixe o instalador do AEM 6.5 Forms no JEE da [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html). Você precisa de um contrato válido de Manutenção e Suporte para usar o instalador.
1. Consulte [Lista de verificação de atualização e planejamento](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65) para saber mais sobre as verificações a serem executadas para garantir uma atualização bem-sucedida.
1. Consulte [Preparar para atualizar para o AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65) para aprender e executar as tarefas que garantem que a atualização seja executada corretamente com o mínimo de inatividade do servidor.
1. Dependendo do ambiente existente e do servidor de aplicativos, escolha um dos documentos a seguir e siga as instruções.

   * [Atualização do AEM 6.3 ou AEM 6.4 Forms para o AEM 6.5 Forms para JBoss](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65)
   * [Atualização do AEM 6.3 ou AEM 6.4 Forms para o AEM 6.5 Forms para WebSphere](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65)
   * [Atualização do AEM 6.3 ou AEM 6.4 Forms para o AEM 6.5 Forms para JBoss Turnkey](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65)
   * [Atualização do JBoss EAP da 7.4.10 para 7.4.23 para AEM Forms no JEE](/help/forms/using/upgrade-jboss-eap-from-7-4-10-to-7-4-23.md)
   * [Atualização do cluster JBoss EAP de 7.4.10 para 7.4.23 para AEM Forms no JEE](/help/forms/using/upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23.md)

A atualização direta do LiveCycle ES2, LiveCycle ES3, AEM 6.0 Forms, AEM 6.1 Forms, AEM 6.2 Forms para o AEM 6.5 Forms não está disponível. Você pode executar uma atualização intermediária para uma ou mais versões do LiveCycle ou do AEM Forms e, em seguida, atualizar para o AEM 6.5 Forms. Para obter a lista de versões intermediárias e as instruções de atualização correspondentes, consulte [Escolher um caminho de atualização](upgrade.md).

