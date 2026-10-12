---
title: Desabilitar UAC para Configuração PDFG aplicável a JEE e OSGI
description: Saiba mais sobre como desabilitar a Configuração UAC para PDFG para corrigir a conversão do Word em PDF.
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 4%
---
# Não é possível converter o arquivo do Word ou Excel em PDF no Windows Server {#unable-to-convert-word-excel-files-PDF}

## Problema {#issue}

Quando o usuário tenta converter arquivos do Word ou Excel para o PDF no Microsoft® Windows Server, o seguinte erro é encontrado como:

*Mensagem de erro do conversor primário:*
*ALC-PDG-015-003-O sistema não pode abrir o arquivo de entrada. Envie seu arquivo novamente ou contate o administrador do sistema.*


## Solução {#solution}

Faça o seguinte:

1. Para acessar o Utilitário de Configuração do Sistema, vá para **[!UICONTROL Iniciar > Executar]** e digite **[!UICONTROL MSCONFIG]**.
1. Clique na guia **[!UICONTROL Ferramentas]**, role para baixo e selecione **[!UICONTROL Alterar Configurações de UAC]**. Clique em **[!UICONTROL Iniciar]** para executar o comando em uma nova janela.
1. Ajuste o controle deslizante para o nível Nunca notificar. Quando terminar, feche a janela de comando e a janela Configuração do sistema.
1. Verifique se a configuração do Registro para UAC está definida como 0 (zero). Execute as seguintes etapas para verificar:

   1. A Microsoft® recomenda fazer backup do registro antes de modificá-lo. Para obter etapas detalhadas, consulte [Como fazer backup e restaurar o Registro no Windows](https://support.microsoft.com/en-us/help/322756).
   1. Abra o editor de Registro do Microsoft® Windows. Para abrir o editor de registro, vá para Iniciar > Executar, digite regedit e clique em OK.
   1. Vá até `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Verifique se o valor de EnableLUA está definido como 0 (zero).
   1. Verifique se o valor de **EnableLUA** está definido como 0 (zero). Se o valor não for 0, altere o valor para 0. Feche o editor de Registro.

1. Reinicie o computador.

## Aplica-se a {#appliesto}

Essa solução se aplica ao AEM Forms no servidor JEE e ao AEM Forms no servidor OSGi.
