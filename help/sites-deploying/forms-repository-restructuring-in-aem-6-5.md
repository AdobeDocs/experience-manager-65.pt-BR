---
title: Reestruturação do repositório Forms no AEM 6.5
seo-title: Forms Repository Restructuring in AEM 6.5
description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura do repositório no AEM 6.5 para Forms.
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.5 for Forms.
uuid: e60830d4-23ca-4be9-941a-ee4abe4786a6
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 1ce9a622-5968-407f-a74b-d325a2bff669
feature: Upgrading
exl-id: d555422e-dc97-4d45-9525-4299d22315e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 7%

---

# Reestruturação do repositório Forms no AEM 6.5{#forms-repository-restructuring-in-aem}

Conforme descrito no pai [Reestruturação do repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md) , os clientes que estiverem atualizando para o AEM 6.5 devem usar esta página para avaliar o esforço de trabalho associado às alterações no repositório que afetam a solução da AEM Forms. Algumas alterações exigem esforço de trabalho durante o processo de atualização do AEM 6.5, enquanto outras podem ser adiadas até uma atualização futura.

**Com atualização para 6.5**

* [Diversos](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**Antes de uma atualização futura**

* [Configuração de Cloud Service de eco](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [Configurações de Cloud Service de Recaptcha](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Configurações de Cloud Service do TypeKit](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [Diversos](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## Com atualização para 6.5 {#with-upgrade}

### Diversos {#misc}

| **Local anterior** | `/etc/clientlibs/fd/fp` |
|---|---|
| **Novos locais** | `/libs/fd/fp/components` |
| **Orientações em matéria de reestruturação** | Qualquer referência explícita no código personalizado ao local herdado deve ser atualizada para o Novo local. |
| **Notas** | Essas bibliotecas de clientes não devem ser modificadas ou estendidas. |

| **Local anterior** | `/etc/clientlibs/fd/rte` |
|---|---|
| **Novos locais** | `/libs/fd/rte` |
| **Orientações em matéria de reestruturação** | Para os recursos nas bibliotecas do cliente que podem ser referenciados por caminhos absolutos, é necessário usar caminhos mais recentes nos novos ativos. |
| **Notas** | N/A |

| **Local anterior** | `/etc/clientlibs/fd/af` |
|---|---|
| **Novos locais** | `/libs/fd/af/authoring/clientlibs` |
| **Orientações em matéria de reestruturação** | Para os recursos nas bibliotecas do cliente que podem ser referenciados por caminhos absolutos, é necessário usar caminhos mais recentes nos novos ativos. |
| **Notas** | N/A |

| **Local anterior** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **Novos locais** | `/libs/fd/xfaforms/clientlibs/` |
| **Orientações em matéria de reestruturação** | Para os recursos nas bibliotecas do cliente que podem ser referenciados por caminhos absolutos, é necessário usar caminhos mais recentes nos novos ativos. |
| **Notas** | N/A |

| **Local anterior** | `/etc/clientlibs/fd/af` |
|---|---|
| **Novos locais** | `/libs/fd/af/runtime/clientlibs` |
| **Orientações em matéria de reestruturação** | Para os recursos nas bibliotecas do cliente que podem ser referenciados por caminhos absolutos, é necessário usar caminhos mais recentes nos novos ativos. |
| **Notas** | N/A |

| **Local anterior** | `/etc/clientlibs/fd/af` |
|---|---|
| **Novos locais** | `/libs/fd/af/runtime/clientlibs` |
| **Orientações em matéria de reestruturação** | Para os recursos nas bibliotecas do cliente que podem ser referenciados por caminhos absolutos, é necessário usar caminhos mais recentes nos novos ativos. |
| **Notas** | N/A |

| **Local anterior** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **Novos locais** | `/libs/fd/expeditor/clientlibs` |
| **Orientações em matéria de reestruturação** | Para os recursos nas bibliotecas do cliente que podem ser referenciados por caminhos absolutos, é necessário usar caminhos mais recentes nos novos ativos. |
| **Notas** | N/A |

| **Local anterior** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **Novos locais** | `/libs/fd/fmaddon` |
| **Orientações em matéria de reestruturação** | A alteração dessas clientlibs nunca foi recomendada ou suportada. Se tiverem sido feitas modificações nessas clientlibs, elas deverão ser revertidas para usar o código fornecido pelo AEM. |
| **Notas** | N/A |

| **Local anterior** | `/etc/aep` |
|---|---|
| **Novos locais** | `/var/fd/content/annotations` |
| **Orientações em matéria de reestruturação** | A alteração dessas clientlibs nunca foi recomendada ou suportada. Se tiverem sido feitas modificações nessas clientlibs, elas deverão ser revertidas para usar o código fornecido pelo AEM. |
| **Notas** | N/A |

## Antes de uma atualização futura {#prior-to-upgrade}

### Configuração de Cloud Service de eco {#echosign-cloud-service-configuration}

| **Local anterior** | `/etc/cloudservices/echosign` |
|---|---|
| **Novos locais** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **Orientações em matéria de reestruturação** | A variável [Migração de conteúdo lento](/help/sites-deploying/lazy-content-migration.md) que será acionado na interface de migração do Forms. |
| **Notas** | N/A |

### Configurações de Cloud Service de Recaptcha {#recaptcha-cloud-service-configurations}

| **Local anterior** | `/etc/cloudservices/recaptcha` |
|---|---|
| **Novos locais** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **Orientações em matéria de reestruturação** | A variável [Migração de conteúdo lento](/help/sites-deploying/lazy-content-migration.md) que será acionado na interface de migração do Forms. |
| **Notas** | N/A |

### Configurações de Cloud Service do TypeKit {#typekit-cloud-service-configurations}

| **Local anterior** | `/etc/cloudservices/typekit` |
|---|---|
| **Novos locais** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **Orientações em matéria de reestruturação** | A variável [Migração de conteúdo lento](/help/sites-deploying/lazy-content-migration.md) que será acionado na interface de migração do Forms. |
| **Notas** | N/A |

### Diversos {#misc-1}

| **Local anterior** | `/etc/cloudservices/fdm` |
|---|---|
| **Novos locais** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **Orientações em matéria de reestruturação** | A variável [Migração de conteúdo lento](/help/sites-deploying/lazy-content-migration.md) que será acionado na interface de migração do Forms. |
| **Notas** | N/A |

| **Local anterior** | `/etc/designs/fd/fp` |
|---|---|
| **Novos locais** | `/libs/fd/fp` |
| **Orientações em matéria de reestruturação** | Quaisquer referências aos modelos /etc devem ser atualizadas para apontar para seus `/libs` seus homólogos. |
| **Notas** | N/A |
