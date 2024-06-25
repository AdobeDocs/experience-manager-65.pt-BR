---
title: Este artigo inclui a instrução para desinstalar o pacote complementar do Forms usando o Gerenciador de pacotes do CRX.
description: Saiba mais sobre as etapas para desinstalar o pacote complementar do Forms usando o Gerenciador de pacotes do CRX.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: 2755e414ea23ebc1472e9c08d832eca93f28311b
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---


# Desinstalar pacote complementar do AEM Forms da instância AEM

Este artigo descreve as etapas necessárias para desinstalar corretamente o pacote complementar do AEM Forms de uma instância do SDK da AEM Forms. Siga estas etapas para garantir a remoção do pacote complementar do Forms, evitando possíveis problemas com seu ambiente AEM.

## Pré-requisito

Certifique-se de fazer backup para evitar qualquer perda de dados.

## Para desinstalar o pacote complementar do AEM Forms

Para desinstalar o pacote complementar do AEM Forms, execute as seguintes etapas:

1. **Desinstale o pacote complementar do AEM Forms:**
   1. Navegue até a `http://[host]:[port]/crx/de/index.jsp`.
   1. Localize e desinstale o `AEM Forms add-on package`.

   ![Desinstalar pacote](/help/forms/using/assets/uninstall-aem-forms-package.png)

1. **Exclua a pasta nativa do CRXDE:**
   1. Navegue até a `http://[host]:[port]/crx/de/index.jsp`.
   1. Ir para `/libs/fd/native/install` e excluir `native` pasta no CRXDE.

      ![Excluir nó nativo do CRX/de](/help/forms/using/assets/native-install-folder-crxde.png)
   1. Salve as alterações.

1. **Pare o SDK do AEM Forms:**
   1. Pare a instância do SDK do AEM Forms usando o comando &quot;Ctrl + C&quot;.

1. **Verifique as pastas de base e instalação na pasta crx-quickstart**
   1. Navegue até `..author\crx-quickstart` na instância do SDK do AEM Forms.
   1. Pesquisar pastas chamadas `bedrock` e `install`.
Se encontrados, verifique se foram excluídos da `crx-quickstart` na instância do SDK do AEM Forms.

   >[!NOTE]
   >
   > A variável `bedrock` A pasta é criada novamente automaticamente ao reiniciar a instância do SDK do AEM Forms.

1. **Reinicie a instância do AEM:**
   1. Quando todas as etapas anteriores forem concluídas, [reinicie a instância do SDK do AEM Forms](/help/forms/using/restart-aem-sdk.md).




