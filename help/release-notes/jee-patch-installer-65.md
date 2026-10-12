---
title: Instalador de patch do AEM Forms JEE
description: Saiba como usar o Instalador de patch do AEM Forms JEE para corrigir problemas em componentes do AEM 6.5 Forms.
content-type: reference
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
hide: true
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ed762d86-a04b-452b-a08f-86359bb8ff27
    internal-label: Configuration and operations
subfeature_v2:
  - id: c21ccc2b-e0c8-4853-bf41-f12259ed93f8
    internal-label: Release information
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 19%
---
# Instalador de patch do AEM Forms JEE {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Contate o Suporte](https://experienceleague.adobe.com/pt-br?support-solution=General&support-tab=home#support) para obter mais informações ou obter o patch.

## Sobre o instalador de patch {#about-the-patch-installer}

O instalador de patch do AEM 6.5 Forms JEE inclui todos os problemas corrigidos de todos os componentes do AEM 6.5 Forms JEE disponíveis até o lançamento deste patch. Consulte as [Notas de Versão do Service Pack](release-notes.md) mais recentes para obter uma lista completa de problemas corrigidos.

## Pré-requisitos para instalar o patch {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Instalação e configuração do patch {#installing-and-configuring-the-patch}

1. Faça backup da pasta &lt;*AEM_forms_root*>/deploy. Isso é necessário caso você decida desinstalar a correção rápida.
1. Interrompa o servidor de aplicativos.
1. Extraia o arquivo do instalador de correção para o disco rígido.
1. No diretório nomeado de acordo com o seu sistema operacional:

   * **Windows**
     Navegue até o diretório apropriado na mídia ou pasta de instalação no disco rígido em que o instalador foi copiado e clique duas vezes no arquivo aemforms65_cfp_install.exe.

     * (Windows de 32 bits) `Windows\Disk1\InstData\VM`
     * (Windows 64-bit) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
     Navegue até o diretório apropriado e, em um prompt de comando, digite `./aem65_cfp_install.bin`.

     * (Linux®) `Linux/Disk1/InstData/NoVM`

   Isso inicia um assistente de instalação que o guiará durante a instalação.

1. No painel de Introdução, clique em **[!UICONTROL Próximo]**.
1. Na tela **Escolher Pasta de Instalação**, verifique se o local padrão exibido está correto para sua instalação existente ou clique em **[!UICONTROL Procurar]** para selecionar a pasta alternativa em que o AEM Forms está instalado e clique em **[!UICONTROL Avançar]**.
1. Leia as informações no Resumo de correção rápida e clique em **[!UICONTROL Próximo]**.
1. Leia as informações no Resumo de pré-instalação e clique em **[!UICONTROL Instalar]**.
1. Quando a instalação estiver concluída, clique em **[!UICONTROL Próximo]** para aplicar as atualizações de correção rápida aos arquivos instalados.

1. **[Somente para Windows]:** Faça o seguinte:
   * Desmarque a opção **Iniciar Gerenciador de Configurações** antes de clicar em **[!UICONTROL Concluído]**. Execute o **Configuration Manager** usando o arquivo **ConfigurationManager.bat** em `[aem-forms root]\configurationManager\bin`.

   * Ou desmarque a opção **Iniciar Gerenciador de Configurações** antes de clicar em **[!UICONTROL Concluído]**. Antes de executar o **Configuration Manager** usando o **ConfigurationManager.exe** ou o **ConfigurationManager_IPv6.exe**, navegue até o diretório *`<AEMForms_Install_Dir>\configurationManager\bin`* e substitua os arquivos **ConfigurationManager.lax** e **ConfigurationManager_IPV6.lax** mais recentes por [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) e [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax), Pesquise e substitua **axis-1.4.1.1.jar** com **axis-1.4.1.2.jar** nesses dois arquivos.

   >[!NOTE]
   >
   >Usar o arquivo **ConfigurationManager.bat** ajuda a evitar a atualização manual do nome de arquivos .lax.
   >

1. **[Somente para Unix]:**

   * A caixa de seleção **Iniciar Configuration Manager** está selecionada por padrão. Clique em **[!UICONTROL Concluído]** para executar o Gerenciador de Configurações instantaneamente ou para executar o **Gerenciador de Configurações** mais tarde, desmarque a opção **Iniciar Gerenciador de Configurações** antes de clicar em **[!UICONTROL Concluído]**. Você pode iniciar o **Configuration Manager** posteriormente usando o script apropriado no diretório `[AEM_forms_root]/configurationManager/bin`.

1. Dependendo do servidor de aplicativos, escolha um dos seguintes documentos e siga as instruções na seção *Configuração e implantação do AEM Forms*.

   * [Instalação e implantação do AEM Forms para JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_br)
   * [Instalação e implantação do AEM Forms para WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_br)

1. (Somente JBoss®) Após instalar o patch e configurar o servidor, exclua tmp e diretórios de trabalho do servidor de aplicativos JBoss®.

## Configurações pós-implantação {#post-deployment-configurations}

### Configurações de SAML {#saml-configurations}

Se você tiver a autenticação SAML configurada e estiver enfrentando problemas com grandes metadados IDP, faça o seguinte após instalar o patch:

1. Defina a seguinte propriedade do sistema no servidor de aplicativos:\
   `um.saml.enable.large.xml=true`
1. Reinicie o servidor.
1. Exclua os provedores de autenticação SAML existentes e adicione-os novamente para domínios existentes, conforme descrito nas configurações de SAML.

>[!NOTE]
>
> É recomendável usar o comando &#39;Ctrl + C&#39; para reiniciar o SDK. Reiniciar o AEM SDK usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

## Módulos afetados {#impacted-modules}

* Serviços de documento
* Segurança de documentos
* Foundation JEE

[Entrar em contato com o suporte](https://experienceleague.adobe.com/pt-br?support-solution=General&support-tab=home#support)
