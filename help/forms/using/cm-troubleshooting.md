---
title: 'Gerenciamento de correspondência: solução de problemas'
description: Saiba como lidar com erros que surgem durante o processo de salvar uma correspondência em um ambiente do AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 1%
---
# Gerenciamento de correspondência: solução de problemas {#correspondence-management-troubleshooting}

## Erros ao salvar uma carta {#errors-when-saving-a-letter}

### Problema {#issue}

Um dos seguintes erros é exibido ao salvar uma correspondência:

* Vinculação de dados ausente para o módulo de texto
* Forneça as informações de propriedade necessárias para o seguinte

### Motivo {#reason}

Esses erros podem ocorrer devido a um dos seguintes motivos:

* Um dicionário de dados está associado à carta, mas não está presente no servidor.
* Um dicionário de dados é vinculado à letra, mas tem um sublinhado (_) em seu nome.

### Solução alternativa {#workaround}

Certifique-se de que o dicionário de dados que você está usando na correspondência esteja presente no servidor e não tenha um sublinhado (_) em seu nome.

## Erro ao visualizar uma correspondência {#error-when-previewing-a-letter}

### Problema {#issue-1}

Ao visualizar uma correspondência, o erro &quot;Erro ao carregar a correspondência: não foi possível importar o ativo da entrada XML&quot; aparece mesmo quando um ativo de texto não publicado anteriormente na correspondência é publicado.

### Solução alternativa {#workaround-1}

Redefina o cache de cartas na instância de publicação usando as seguintes etapas e tente exibir a carta novamente:

1. Vá para **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** e faça logon como Administrador.
1. Selecione **Configurações de gerenciamento de correspondência**.
1. Em **Configurações de Gerenciamento de Correspondências**, desabilite **Habilitar Cache de Carta** e clique em **Salvar.**
1. Marque **Habilitar Cache de Carta** e clique em **Salvar**.
1. Tente novamente visualizar a carta.
