---
title: Instalador de patch do AEM Forms JEE
description: AEM Forms JEE Patch Installer para corrigir problemas em componentes AEM 6.5 Forms.
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 20%

---

# Instalador de patch do AEM Forms JEE {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Entrar em contato com o suporte](https://www.adobe.com/account/sign-in.supportportal.html) para obter mais informações ou obter o patch.

## Sobre o instalador de patch {#about-the-patch-installer}

O instalador de patch do AEM 6.5 Forms JEE inclui todos os problemas corrigidos de todos os componentes do AEM 6.5 Forms JEE disponíveis até o lançamento deste patch. Veja a mais recente  [Notas de versão do Service Pack](release-notes.md) para obter uma lista completa de problemas corrigidos.

## Pré-requisitos para instalar o patch {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Instalação e configuração do patch {#installing-and-configuring-the-patch}

1. Faça backup do &lt;*AEM_forms_root*>/implantar pasta. Isso é necessário caso você decida desinstalar a correção rápida.
1. Interrompa o servidor de aplicativos.
1. Extraia o arquivo do instalador de correção para o disco rígido.
1. No diretório nomeado de acordo com o seu sistema operacional:

   * **Windows**
Navegue até o diretório apropriado na mídia ou pasta de instalação no disco rígido em que o instalador foi copiado e clique duas vezes no arquivo aemforms65_cfp_install.exe.

      * (Windows de 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows de 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux**
Navegue até o diretório apropriado e, em um prompt de comando, digite `./aem65_cfp_install.bin`.

      * (Linux) `Linux/Disk1/InstData/NoVM`

   Isso inicia um assistente de instalação que o guiará durante a instalação.

1. No painel de Introdução, clique em **[!UICONTROL Próximo]**.
1. No **Escolha a pasta de instalação** , verifique se o local padrão exibido está correto para sua instalação existente, ou clique em **[!UICONTROL Procurar]** para selecionar a pasta alternativa em que o AEM Forms está instalado e clique em **[!UICONTROL Próxima]**.
1. Leia as informações no Resumo de correção rápida e clique em **[!UICONTROL Próximo]**.
1. Leia as informações no Resumo de pré-instalação e clique em **[!UICONTROL Instalar]**.
1. Quando a instalação estiver concluída, clique em **[!UICONTROL Próximo]** para aplicar as atualizações de correção rápida aos arquivos instalados.

1. **[Somente para Windows]:** Execute uma das seguintes etapas:
   * Desmarque a opção **Iniciar o Gerenciador de Configurações** antes de clicar em **[!UICONTROL Concluído]**. Executar **Gerenciador de configurações** usando o **ConfigurationManager.bat** arquivo localizado em `[aem-forms root]\configurationManager\bin`.

   * Ou desmarque a opção **Iniciar o Gerenciador de Configurações** antes de clicar em **[!UICONTROL Concluído]**. Antes de executar **Gerenciador de configurações** usar **ConfigurationManager.exe** ou **ConfigurationManager_IPv6.exe**, navegue até *`<AEMForms_Install_Dir>\configurationManager\bin`* direcionar e substituir [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) e [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) arquivos.

   
   >[!NOTE]
   >
   >Usar **ConfigurationManager.bat** ajuda a evitar a atualização manual do nome de arquivos .lax.
   

1. **[Somente para Unix]:**

   * A variável **Iniciar o Gerenciador de Configurações** é marcada por padrão. Clique em **[!UICONTROL Concluído]** para executar o Gerenciador de configurações instantaneamente ou **Gerenciador de configurações** posteriormente, desmarque a opção **Iniciar o Gerenciador de Configurações** antes de clicar em **[!UICONTROL Concluído]**. Você pode começar **Gerenciador de configurações** posteriormente usando o script apropriado na `[AEM_forms_root]/configurationManager/bin` diretório.

1. Dependendo do servidor de aplicativos, escolha um dos seguintes documentos e siga as instruções na *Configuração e implantação de formulários AEM* seção.

   * [Instalação e implantação de formulários AEM para JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Instalação e implantação de formulários AEM para WebSphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (Somente JBoss) Após instalar o patch e configurar o servidor, exclua os diretórios de trabalho e tmp do servidor de aplicativos JBoss.

## Configurações pós-implantação {#post-deployment-configurations}

### Configurações de SAML {#saml-configurations}

Se você tiver configurado a autenticação SAML e estiver enfrentando problemas com grandes metadados IDP, faça o seguinte após instalar o patch:

1. Defina a seguinte propriedade do sistema no servidor de aplicativos:\
   `um.saml.enable.large.xml=true`
1. Reinicie o servidor.
1. Exclua os provedores de autenticação SAML existentes e adicione-os novamente para domínios existentes, conforme descrito nas configurações de SAML.

## Módulos afetados {#impacted-modules}

* Serviços de documento
* Segurança de documentos
* Foundation JEE

[Entrar em contato com o suporte](https://www.adobe.com/account/sign-in.supportportal.html)
