---
title: Desative o UAC para a configuração PDFG aplicável ao JEE e OSGI
description: Etapas para desativar o UAC para configuração PDFG
exl-id: 785b7bb4-7158-45ea-a1e5-eebf3dc3ebc3
source-git-commit: 2e9b9c40f54aa54a946e4320341ed4a760c56fd1
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 3%

---

# Não é possível converter o arquivo do Word ou Excel para o PDF no Windows Server {#unable-to-convert-word-excel-files-PDF}

## Problema {#issue}

Quando o usuário tenta converter arquivos do Word ou do Excel para o PDF no Microsoft Windows Server, o seguinte erro é encontrado como:

*Mensagem de erro do conversor principal: ALC-PDG-015-003-O sistema não pode abrir o arquivo de entrada. Envie seu arquivo novamente ou entre em contato com o administrador do sistema.*


## Solução {#solution}

Execute as seguintes etapas para resolver o problema:
1. Para acessar o Utilitário de configuração do sistema, acesse **[!UICONTROL Iniciar > Executar]** e então insira **[!UICONTROL MSCONFIG]**.
1. Clique no botão **[!UICONTROL Ferramentas]** e role para baixo e selecione **[!UICONTROL Alterar configurações de UAC]**. Clique em **[!UICONTROL Launch]** para executar o comando em uma nova janela.
1. Ajuste o controle deslizante para o nível Nunca notificar . Quando terminar, feche a janela de comando e feche a janela Configuração do sistema.
1. Verifique se a configuração do Registro para UAC está definida como 0 (zero). Execute as seguintes etapas para verificar:

   1. A Microsoft® recomenda fazer backup do registro antes de modificá-lo. Para obter etapas detalhadas, consulte [Como fazer backup e restaurar o registro no Windows](https://support.microsoft.com/en-us/help/322756).
   1. Abra o editor de Registro do Microsoft® Windows. Para abrir o editor do registro, vá para Iniciar > Executar, digite regedit e clique em OK.
   1. Vá até `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Verifique se o valor de EnableLUA está definido como 0 (zero).
   1. Garanta o valor de **EnableLUA** é definido como 0 (zero). Se o valor não for 0, altere o valor para 0. Feche o editor de Registro.

1. Reinicie o computador.

## Aplica-se a {#appliesto}

Essa solução se aplica ao seguinte:
* AEM Forms no servidor JEE
* AEM Forms no servidor OSGi
