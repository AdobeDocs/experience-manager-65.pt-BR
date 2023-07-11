---
title: Atualização para AEM 6.5 Forms no JEE
description: Você pode executar uma atualização direta do AEM 6.1 Forms, AEM 6.2 Forms e LiveCycle AEM ES4 SP1 para o 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 722e75a0-bcb3-465e-bb74-ea94a3b99fd3
source-git-commit: e9f64722ba7df0a7f43aaf1005161483e04142f5
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 1%

---

# Atualização para AEM 6.5 Forms no JEE {#upgrade-to-aem-forms-jee}

O AEM 6.5.12.0 Forms no JEE fornece dois tipos de instaladores: Instalador completo e Instalador de patch.

**Instalador completo**: Você pode usar o [Instalador completo do AEM 6.5.12.0 no JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) para configurar novas instâncias do AEM Forms ou executar atualizações do AEM 6.3 Forms no JEE, do AEM AEM 6.4 no JEE e atualização imediata do 6.5.x.x Forms AEM no JEE para o 6.5.12.0 Forms no JEE.

**Instalador de patch**: [AEM 6.5.12.0 no instalador de patch do JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) O é para clientes que já usam as versões AEM 6.5.x.x. Você pode usar o instalador de patches para atualizar para a versão mais recente do AEM Forms.

A tabela a seguir mostra cenários de uso do instalador de patch e completo.

![Cenário do instalador completo e de patch](assets/full-and-patch-installer.png)

Execute o seguinte procedimento para usar o instalador completo para atualizar o AEM 6.3 Forms existente no JEE ou o AEM 6.4 Forms AEM no JEE para o 6.5.12.0 Forms no JEE:

1. Baixe o instalador do AEM 6.5 Forms no JEE [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html). Você precisa de um contrato válido de Manutenção e Suporte para usar o instalador.
1. Consulte [Lista de verificação e planejamento de atualização](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65) para saber mais sobre as verificações a serem executadas para garantir uma atualização bem-sucedida.
1. Consulte [Preparação para atualizar para o AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65) para aprender e executar as tarefas que garantem que a atualização seja executada corretamente com o mínimo de inatividade do servidor.
1. Dependendo do ambiente existente e do servidor de aplicativos, escolha um dos documentos a seguir e siga as instruções.

   * [Atualização do AEM 6.3 ou AEM 6.4 Forms para o AEM 6.5 Forms para JBoss](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65)
   * [Atualização do AEM 6.3 ou AEM 6.4 Forms para o AEM 6.5 Forms para WebSphere](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65)
   * [Atualização do AEM 6.3 ou AEM 6.4 Forms para o AEM 6.5 Forms para JBoss Turnkey](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65)

A atualização direta do LiveCycle ES2, LiveCycle ES3, AEM 6.0 Forms, AEM 6.1 Forms, µ 6.2 Forms AEM Forms para o 6.5 AEM não está disponível. Você pode executar uma atualização intermediária para uma ou mais versões do LiveCycle ou AEM Forms e, em seguida, atualizar para o AEM 6.5 Forms. Para obter a lista de versões intermediárias e as instruções de atualização correspondentes, consulte [Escolha um caminho de atualização](upgrade.md).
