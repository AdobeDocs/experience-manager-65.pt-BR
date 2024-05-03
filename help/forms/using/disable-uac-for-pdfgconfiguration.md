---
title: Desabilitar UAC para Configuração PDFG aplicável a JEE e OSGI
description: Saiba mais sobre as etapas para desativar a configuração de UAC para PDFG a fim de corrigir a conversão do Word em PDF.
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---

# Não é possível converter arquivo do Word ou Excel em PDF no Windows Server {#unable-to-convert-word-excel-files-PDF}

## Problema {#issue}

Quando o usuário tenta converter arquivos do Word ou Excel para o PDF no Microsoft® Windows Server, o seguinte erro é encontrado como:

*Mensagem de erro do conversor primário:*
*ALC-PDG-015-003-O sistema não pode abrir o arquivo de entrada. Envie seu arquivo novamente ou contate o administrador do sistema.*


## Solução {#solution}

Faça o seguinte:

1. Para acessar o Utilitário de configuração do sistema, vá para **[!UICONTROL Iniciar > Executar]** e insira **[!UICONTROL MSCONFIG]**.
1. Clique em **[!UICONTROL Ferramentas]** e role para baixo e selecione **[!UICONTROL Alterar Configurações de UAC]**. Clique em **[!UICONTROL Launch]** para executar o comando em uma nova janela.
1. Ajuste o controle deslizante para o nível Nunca notificar. Quando terminar, feche a janela de comando e a janela Configuração do sistema.
1. Verifique se a configuração do Registro para UAC está definida como 0 (zero). Execute as seguintes etapas para verificar:

   1. A Microsoft® recomenda fazer backup do registro antes de modificá-lo. Para obter etapas detalhadas, consulte [Como fazer backup e restaurar o registro no Windows](https://support.microsoft.com/en-us/help/322756).
   1. Abra o editor de Registro do Microsoft® Windows. Para abrir o editor de registro, vá para Iniciar > Executar, digite regedit e clique em OK.
   1. Navegue até `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Verifique se o valor de EnableLUA está definido como 0 (zero).
   1. Garantir valor de **EnableLUA** é definido como 0 (zero). Se o valor não for 0, altere o valor para 0. Feche o editor de Registro.

1. Reinicie o computador.

## Aplica-se a {#appliesto}

Essa solução se aplica ao AEM Forms no servidor JEE e ao AEM Forms no servidor OSGi.
