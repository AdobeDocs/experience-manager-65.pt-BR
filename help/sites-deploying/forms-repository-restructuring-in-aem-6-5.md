---
title: Reestruturação do repositório Forms no AEM 6.5
description: Saiba como fazer as alterações necessárias para migrar para a nova estrutura do repositório no AEM 6.5 para Forms.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: d555422e-dc97-4d45-9525-4299d22315e2
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 5%

---

# Reestruturação do repositório Forms no AEM 6.5{#forms-repository-restructuring-in-aem}

Conforme descrito na página pai [Reestruturação do repositório no AEM 6.5](/help/sites-deploying/repository-restructuring.md), os clientes que estão atualizando para o AEM 6.5 devem usar esta página para avaliar o esforço de trabalho associado às alterações no repositório que afetam a Solução da AEM Forms. Algumas alterações exigem esforço de trabalho durante o processo de atualização do AEM 6.5, enquanto outras podem ser adiadas até uma atualização futura.

**Com Atualização 6.5**

* [Diversos](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**Antes de atualização futura**

* [Configuração de Cloud Service de eco](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [Configurações de Cloud Service de Recaptcha](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [Configurações de Cloud Service do TypeKit](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [Diversos](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## Com atualização para 6.5 {#with-upgrade}

### Diversos {#misc}

| **Local anterior** | `/etc/clientlibs/fd/fp` |
|---|---|
| **Novo local** | `/libs/fd/fp/components` |
| **Orientação sobre reestruturação** | Qualquer referência explícita no código personalizado ao local herdado deve ser atualizada para o Novo local. |
| **Notas** | Essas bibliotecas de clientes não devem ser editadas ou estendidas. |

| **Local anterior** | `/etc/clientlibs/fd/rte` |
|---|---|
| **Novo local** | `/libs/fd/rte` |
| **Orientação sobre reestruturação** | Para os recursos nas bibliotecas do cliente que podem ser referenciados por caminhos absolutos, você deve usar caminhos mais recentes nos novos ativos. |
| **Notas** | N/A |

| **Local anterior** | `/etc/clientlibs/fd/af` |
|---|---|
| **Novo local** | `/libs/fd/af/authoring/clientlibs` |
| **Orientação sobre reestruturação** | Para os recursos nas bibliotecas do cliente que podem ser referenciados por caminhos absolutos, você deve usar caminhos mais recentes nos novos ativos. |
| **Notas** | N/A |

| **Local anterior** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **Novo local** | `/libs/fd/xfaforms/clientlibs/` |
| **Orientação sobre reestruturação** | Para os recursos nas bibliotecas do cliente que podem ser referenciados por caminhos absolutos, você deve usar caminhos mais recentes nos novos ativos. |
| **Notas** | N/A |

| **Local anterior** | `/etc/clientlibs/fd/af` |
|---|---|
| **Novo local** | `/libs/fd/af/runtime/clientlibs` |
| **Orientação sobre reestruturação** | Para os recursos nas bibliotecas do cliente que podem ser referenciados por caminhos absolutos, você deve usar caminhos mais recentes nos novos ativos. |
| **Notas** | N/A |

| **Local anterior** | `/etc/clientlibs/fd/af` |
|---|---|
| **Novo local** | `/libs/fd/af/runtime/clientlibs` |
| **Orientação sobre reestruturação** | Para os recursos nas bibliotecas do cliente que podem ser referenciados por caminhos absolutos, você deve usar caminhos mais recentes nos novos ativos. |
| **Notas** | N/A |

| **Local anterior** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **Novo local** | `/libs/fd/expeditor/clientlibs` |
| **Orientação sobre reestruturação** | Para os recursos nas bibliotecas do cliente que podem ser referenciados por caminhos absolutos, você deve usar caminhos mais recentes nos novos ativos. |
| **Notas** | N/A |

| **Local anterior** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **Novo local** | `/libs/fd/fmaddon` |
| **Orientação sobre reestruturação** | A alteração dessas clientlibs nunca foi recomendada ou suportada. Se tiverem sido feitas modificações nessas clientlibs, elas deverão ser revertidas para usar o código fornecido pelo AEM. |
| **Notas** | N/A |

| **Local anterior** | `/etc/aep` |
|---|---|
| **Novo local** | `/var/fd/content/annotations` |
| **Orientação sobre reestruturação** | A alteração dessas clientlibs nunca foi recomendada ou suportada. Se tiverem sido feitas modificações nessas clientlibs, elas deverão ser revertidas para usar o código fornecido pelo AEM. |
| **Notas** | N/A |

## Antes de uma atualização futura {#prior-to-upgrade}

### Configuração de Cloud Service de eco {#echosign-cloud-service-configuration}

| **Local anterior** | `/etc/cloudservices/echosign` |
|---|---|
| **Novo local** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **Orientação sobre reestruturação** | O utilitário [Migração de Conteúdo Lenta](/help/sites-deploying/lazy-content-migration.md) será acionado a partir da interface de Migração do Forms. |
| **Notas** | N/A |

### Configurações de Cloud Service de Recaptcha {#recaptcha-cloud-service-configurations}

| **Local anterior** | `/etc/cloudservices/recaptcha` |
|---|---|
| **Novo local** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **Orientação sobre reestruturação** | O utilitário [Migração de Conteúdo Lenta](/help/sites-deploying/lazy-content-migration.md) será acionado a partir da interface de Migração do Forms. |
| **Notas** | N/A |

### Configurações de Cloud Service do TypeKit {#typekit-cloud-service-configurations}

| **Local anterior** | `/etc/cloudservices/typekit` |
|---|---|
| **Novo local** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **Orientação sobre reestruturação** | O utilitário [Migração de Conteúdo Lenta](/help/sites-deploying/lazy-content-migration.md) será acionado a partir da interface de Migração do Forms. |
| **Notas** | N/A |

### Diversos {#misc-1}

| **Local anterior** | `/etc/cloudservices/fdm` |
|---|---|
| **Novo local** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **Orientação sobre reestruturação** | O utilitário [Migração de Conteúdo Lenta](/help/sites-deploying/lazy-content-migration.md) será acionado a partir da interface de Migração do Forms. |
| **Notas** | N/A |

| **Local anterior** | `/etc/designs/fd/fp` |
|---|---|
| **Novo local** | `/libs/fd/fp` |
| **Orientação sobre reestruturação** | Atualize todas as referências aos modelos /etc para apontar para seus equivalentes `/libs`. |
| **Notas** | N/A |
