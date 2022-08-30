---
title: Instalador de patches do AEM Forms JEE
description: Instalador de patches do AEM Forms JEE
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 20%

---

# Instalador de patches do AEM Forms JEE {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Entre em contato com o suporte](https://www.adobe.com/account/sign-in.supportportal.html) para mais informações ou para obter o sistema.

## Sobre o instalador de patches {#about-the-patch-installer}

O instalador de patches do Forms JEE AEM 6.5 inclui todos os problemas corrigidos de todos os componentes do Forms JEE AEM 6.5 disponíveis até o lançamento deste patch. Veja o mais recente  [Notas de versão do Service Pack](release-notes.md) para obter uma lista completa de problemas corrigidos.

## Pré-requisitos para instalar o patch {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Instalação e configuração do patch {#installing-and-configuring-the-patch}

1. Faça um backup do &lt;*AEM_forms_root*>/implantar pasta. Isso é necessário caso você decida desinstalar a correção rápida.
1. Interrompa o servidor de aplicativos.
1. Extraia o arquivo do instalador de correção para o disco rígido.
1. No diretório nomeado de acordo com o seu sistema operacional:

   * **Windows**
Navegue até o diretório apropriado na mídia de instalação ou pasta do disco rígido em que você copiou o instalador e clique duas vezes no arquivo aemforms65_cfp_install.exe .

      * (Windows de 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows de 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux**
Navegue até o diretório apropriado e, a partir de um prompt de comando, digite 
`./aem65_cfp_install.bin`.

      * (Linux) `Linux/Disk1/InstData/NoVM`

   Isso inicia um assistente de instalação que o guiará durante a instalação.

1. No painel de Introdução, clique em **[!UICONTROL Próximo]**.
1. No **Escolha a pasta Instalar** verifique se o local padrão exibido está correto para a instalação existente ou clique em **[!UICONTROL Procurar]** para selecionar a pasta alternativa onde AEM formulários está instalado e clique em **[!UICONTROL Próximo]**.
1. Leia as informações no Resumo de correção rápida e clique em **[!UICONTROL Próximo]**.
1. Leia as informações no Resumo de pré-instalação e clique em **[!UICONTROL Instalar]**.
1. Quando a instalação estiver concluída, clique em **[!UICONTROL Próximo]** para aplicar as atualizações de correção rápida aos arquivos instalados.

1. **[Somente para Windows]:** Execute uma das seguintes etapas:
   * Desmarque a opção **Iniciar o Configuration Manager** antes de clicar **[!UICONTROL Concluído]**. Executar **Gerenciador de configuração** usando o **ConfigurationManager.bat** arquivo localizado em `[aem-forms root]\configurationManager\bin`.

   * Ou desmarque a opção **Iniciar o Configuration Manager** antes de clicar **[!UICONTROL Concluído]**. Antes de executar **Gerenciador de configuração** usar **ConfigurationManager.exe** ou **ConfigurationManager_IPv6.exe**, navegue até *`<AEMForms_Install_Dir>\configurationManager\bin`* direcionar e substituir [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) e [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) arquivos.
   >[!NOTE]
   >Usando **ConfigurationManager.bat** ajuda a evitar a atualização manual do nome dos arquivos .lax.

1. **[Somente para baseado em Unix]:**

   * O **Iniciar o Configuration Manager** é selecionada por padrão. Clique em **[!UICONTROL Concluído]** para executar o Configuration Manager instantaneamente ou para executar **Gerenciador de configuração** depois, desmarque a opção **Iniciar o Configuration Manager** antes de clicar **[!UICONTROL Concluído]**. Você pode começar **Gerenciador de configuração** mais tarde, usando o script apropriado na `[AEM_forms_root]/configurationManager/bin` diretório.

1. Dependendo do servidor de aplicativos, escolha um dos seguintes documentos e siga as instruções em *Configuração e implantação de formulários AEM* seção.

   * [Instalação e implantação de formulários AEM para JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Instalar e implantar formulários de AEM para o WebSphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (Somente JBoss) Após instalar o patch e configurar o servidor, exclua o tmp e os diretórios de trabalho do servidor de aplicativos JBoss.

## Configurações pós-implantação {#post-deployment-configurations}

### Configurações de SAML {#saml-configurations}

Se tiver a autenticação SAML configurada e enfrentado problemas com metadados IDP grandes, faça o seguinte após instalar o patch:

1. Defina a seguinte propriedade do sistema no servidor de aplicativos:\
   `um.saml.enable.large.xml=true`
1. Reinicie o servidor.
1. Exclua os provedores de autenticação SAML existentes e adicione-os novamente aos domínios existentes, conforme descrito nas configurações de SAML.

## Módulos afetados {#impacted-modules}

* Serviços de documento
* Segurança de documentos
* Foundation JEE

[Entre em contato com o suporte](https://www.adobe.com/account/sign-in.supportportal.html)
