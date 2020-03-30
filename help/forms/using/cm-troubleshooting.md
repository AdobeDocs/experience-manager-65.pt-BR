---
title: '"Gestão de correspondência: Solução de problemas"'
seo-title: Solução de problemas do Gerenciamento de correspondência
description: Solução de problemas do Gerenciamento de correspondência
seo-description: Solução de problemas do Gerenciamento de correspondência
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Gerenciamento de correspondência: Solução de problemas {#correspondence-management-troubleshooting}

## Erros ao salvar uma carta {#errors-when-saving-a-letter}

### Problema {#issue}

Um dos seguintes erros era exibido ao salvar uma carta:

* O vínculo de dados não está presente para o módulo de texto
* Forneça a informação de propriedade necessária para o seguinte

### Motivo {#reason}

Esses erros podem ocorrer devido a um dos seguintes:

* Um dicionário de dados está vinculado à letra, mas não está presente no servidor.
* Um dicionário de dados está vinculado à letra, mas tem um sublinhado (_) em seu nome.

### Solução {#workaround}

Certifique-se de que o dicionário de dados que você está usando na carta esteja presente no servidor e não tenha um sublinhado (_) em seu nome.

## Erro ao visualizar uma carta {#error-when-previewing-a-letter}

### Problema {#issue-1}

Ao visualizar uma carta, o erro &quot;Erro na carta de carregamento: &quot;Não foi possível importar o ativo da entrada XML&quot; é exibido mesmo quando um ativo de texto não publicado anteriormente na carta é publicado.

### Solução {#workaround-1}

Redefina o cache de letras na instância de publicação usando as etapas a seguir e tente exibir novamente a carta:

1. Vá para **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** e faça logon como Administrador.
1. Selecione Configurações **de gerenciamento de** correspondência.
1. Em Configurações **de gerenciamento de** correspondência, desative **Ativar cache de carta** e clique **em Salvar.**
1. Ative **Ativar Cache** Carta e clique em **Salvar**.
1. Tente novamente visualizar a carta.

