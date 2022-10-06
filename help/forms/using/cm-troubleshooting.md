---
title: "Gerenciamento de correspondência: Solução de problemas"
seo-title: Correspondence Management Troubleshooting
description: Solução de problemas do gerenciamento de correspondência
seo-description: Correspondence Management Troubleshooting
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 6%

---

# Gerenciamento de correspondência: Solução de problemas {#correspondence-management-troubleshooting}

## Erros ao salvar uma carta {#errors-when-saving-a-letter}

### Problema {#issue}

Um dos seguintes erros é exibido ao salvar uma carta:

* O vínculo de dados não está presente para o módulo de texto
* Forneça a informação de propriedade necessária para o seguinte

### Motivo {#reason}

Esses erros podem ocorrer devido a um dos seguintes:

* Um dicionário de dados está vinculado à carta, mas não está presente no servidor.
* Um dicionário de dados é vinculado à letra, mas tem um sublinhado (_) em seu nome.

### Solução alternativa {#workaround}

Certifique-se de que o dicionário de dados que você está usando na carta esteja presente no servidor e não tenha um sublinhado (_) em seu nome.

## Erro ao visualizar uma carta {#error-when-previewing-a-letter}

### Problema {#issue-1}

Ao visualizar uma carta, o erro &quot;Erro na carta de carregamento: Não foi possível importar o ativo da entrada XML&quot; é exibido mesmo quando um ativo de texto não publicado anteriormente na carta é publicado.

### Solução alternativa {#workaround-1}

Redefina o cache de letras na instância de publicação usando as seguintes etapas e tente visualizar novamente a carta:

1. Ir para **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** e faça logon como Administrador.
1. Selecionar **Configurações de gerenciamento de correspondência**.
1. Em **Configurações de gerenciamento de correspondência**, desativar **Ativar Cache de Carta** e, em seguida, clique em **Salvar.**
1. Habilitar **Ativar Cache de Carta** e, em seguida, clique em **Salvar**.
1. Tente novamente visualizar a carta.
