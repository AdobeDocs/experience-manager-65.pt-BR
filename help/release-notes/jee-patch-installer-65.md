---
title: Instalador de patch AEM Forms JEE
description: 'null'
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
translation-type: tm+mt
source-git-commit: c1af919d4c0fd984249e1a7009274c63b8ce9adb
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---


# Instalador de patch AEM Forms JEE {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Entre em contato com o suporte](https://www.adobe.com/account/sign-in.supportportal.html) para obter mais informações ou obter o patch.

## Sobre o instalador de patch {#about-the-patch-installer}

O instalador de patch Forms JEE 6.5 AEM inclui todos os problemas corrigidos para todos os componentes do Forms JEE 6.5 disponíveis até o lançamento deste patch. Consulte as Notas [de versão mais recentes do](sp-release-notes.md) Service Pack para obter uma lista completa de problemas corrigidos.

## Pré-requisitos para instalar o patch {#prerequisites-to-installing-the-patch}

* Forms AEM 6.5

## Instalação e configuração do patch {#installing-and-configuring-the-patch}

1. Faça backup da pasta &lt;*AEM_forms_root*>/deployel. É necessário se você decidir desinstalar a correção rápida.
1. Pare o servidor de aplicativos.
1. Extraia o arquivo de arquivamento do instalador de patch para o disco rígido.
1. No diretório nomeado de acordo com o sistema operacional que você está usando:

   * **Windows** Navegue até o diretório apropriado na mídia de instalação ou pasta no disco rígido onde você copiou o instalador e clique com o duplo no arquivo aemforms65_cfp_install.exe.

      * (Windows de 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows de 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux** Navegue até o diretório apropriado e, em um prompt de comando, digite 
`./aem65_cfp_install.bin`.

      * (Linux) `Linux/Disk1/InstData/NoVM`

   Isso inicia um assistente de instalação que o guia pela instalação.

1. No painel Introdução, clique em **[!UICONTROL Avançar]**.
1. Na tela Escolher pasta de instalação, verifique se o local padrão exibido está correto para a instalação existente ou clique em **[!UICONTROL Procurar]** para selecionar a pasta alternativa onde AEM formulários estão instalados e clique em **[!UICONTROL Avançar]**.
1. Leia as informações de Resumo do patch de correção rápida e clique em **[!UICONTROL Avançar]**.
1. Leia as informações do Resumo da pré-instalação e clique em **[!UICONTROL Instalar]**.
1. Quando a instalação estiver concluída, clique em **[!UICONTROL Avançar]** para aplicar as atualizações de correção rápida aos arquivos instalados.

1. Desmarque a opção Gerenciador de configuração do Start antes de clicar em Concluído. Antes de executar o gerenciador de configuração usando **ConfigurationManager.exe** ou **ConfigurationManager_IPv6.exe**, navegue até o diretório *&lt;AEMForms_Install_Dir>\configurationManager\bin* e atualize **axis.jar** para **axis-1.4.1.1.jar** nos seguintes arquivos:

   * ConfigurationManager.lax
   * ConfigurationManager_IPv6.lax

1. A caixa de seleção Gerenciador de configuração do Start é selecionada por padrão. Clique em **[!UICONTROL Concluído]** para executar o Configuration Manager.

1. Para executar o Configuration Manager mais tarde, desmarque a opção Start Configuration Manager antes de clicar em Concluído. Você pode start o Configuration Manager posteriormente usando o script apropriado no `[AEM_forms_root]/configurationManager/bin` diretório.

1. Dependendo do servidor de aplicativos, escolha um dos documentos a seguir e siga as instruções na seção *Configuração e implantação AEM formulários* .

   * [Instalação e implantação de formulários AEM para JBoss](http://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Instalação e implantação de formulários AEM para o WebSphere](http://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (Somente JBoss) Após instalar o patch e configurar o servidor, exclua o tmp e os diretórios de trabalho do servidor de aplicativos JBoss.

## Configurações pós-implantação {#post-deployment-configurations}

### Configurações SAML {#saml-configurations}

Se você tiver configurado a autenticação SAML e enfrentar problemas com metadados IDP grandes, faça o seguinte após instalar o patch:

1. Defina a seguinte propriedade do sistema no servidor de aplicativos:\
   `um.saml.enable.large.xml=true`
1. Reinicie o servidor.
1. Exclua os provedores de autenticação SAML existentes e adicione-os novamente para domínios existentes, conforme descrito nas configurações SAML.

## Módulos afetados {#impacted-modules}

* Serviços de documentação
* Segurança de documentos
* Foundation JEE

[Entre em contato com o suporte](https://www.adobe.com/account/sign-in.supportportal.html)
