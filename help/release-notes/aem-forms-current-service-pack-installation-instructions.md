---
title: Instruções de instalação de patch do AEM Forms para o AEM Forms
description: Instruções de instalação do pacote de serviços do AEM Forms para ambientes OSGi e JEE
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: b15581701aaff72db2fc0030b0062d2f12150d8f
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 9%

---

# Instruções de instalação do AEM 6.5 Forms Service Pack {#aem-form-patch-installation-instructions}

## Informações da versão

| Produto | Adobe Experience Manager 6.5 Forms |
|---|---|
| Versão | 6.5.16.0 |
| Tipo | Versão do Service Pack |
| Data | 2 de março de 2023 |
| URL de download | [Versões mais recentes do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) |

>[!NOTE]
>
>Veja a mais recente [Notas de versão do AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=pt-BR) para obter uma lista completa de problemas corrigidos.

## O que está incluído no Experience Manager Forms 6.5

O Adobe Experience Manager (AEM) Forms Service Pack inclui recursos novos e atualizados, como aprimoramentos solicitados por clientes importantes, desempenho, estabilidade e melhorias de segurança. Service packs de lançamento do AEM Forms em intervalos regulares para fornecer os recursos e as melhorias mais recentes. Dependendo da pilha, escolha um dos seguintes caminhos para baixar e instalar o service pack em seu ambiente:

* [Baixar e instalar o Service Pack em um formulário AEM no ambiente JEE](#download-and-install-for-jee-service-pack)
* [Baixar e instalar o Service Pack em um formulário AEM em um ambiente OSGi](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> O Adobe lança um instalador completo a cada 6º service pack. O AEM 6.5 Forms Service Pack 12 (6.5.12.0) no JEE foi o último instalador completo. O instalador completo oferece suporte para novas plataformas, enquanto o instalador regular de pacotes de serviços inclui novos recursos, correções de erros e melhorias gerais. Se você estiver executando uma nova instalação ou planejando usar o software mais recente para o seu Forms AEM 6.5 no ambiente JEE, o Adobe AEM recomenda usar o instalador completo do 6.5.12.0 Forms AEM no JEE, lançado em 03 de março de 2022, em vez do instalador do Forms 6.5, lançado em 08 de abril de 2019. Depois de usar o instalador completo, instale o pacote de serviços mais recente.

## Baixar e instalar o Service Pack em um formulário AEM no ambiente JEE {#download-and-install-for-jee-service-pack}

![Instalação do JEE](/help/forms/using/assets/jeeinstallation.png)

+++1. Faça backup do ambiente existente:

1. Faça backup do seu [Repositório CRX, esquema de banco de dados e GDS (Global Document Storage, armazenamento global de documentos)](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).
1. Faça backup do &lt;*AEM_forms_root*>/implantar pasta.

>[!NOTE]
>
> Antes de executar o instalador do pacote de serviços AEM, verifique se você tem privilégios de acesso de gravação no diretório de instalação do AEM.

+++

+++2.Faça o download do software necessário:

* [AEM Forms no Service Pack do JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=pt-BR)
* [Pacote complementar do Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [Servlet de fragmento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

+++

+++3. Instalar o AEM Forms no service pack JEE:

1. Interrompa o servidor de aplicativos.
1. Extraia o **Arquivo do instalador do AEM Forms no JEE Service Pack** no disco rígido:

   * **Windows**
Navegue até o diretório apropriado na mídia ou pasta de instalação no disco rígido em que você copiou o instalador e clique duas vezes no 
`aemforms65_cfp_install.exe` arquivo.

      * (Windows de 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows de 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux®**
Navegue até o diretório apropriado e, em um shell e digite 
`./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Isso inicia um assistente de instalação que o guiará durante a instalação.

1. No painel de Introdução, clique em **[!UICONTROL Próximo]**.
1. No **Escolha a pasta de instalação** , verifique se o local padrão exibido está correto para sua instalação existente, ou clique em **[!UICONTROL Procurar]** para selecionar a pasta alternativa em que o AEM Forms está instalado e clique em **[!UICONTROL Próxima]**.
1. Leia as informações de resumo do Service Pack e clique em **[!UICONTROL Próxima]**.
1. Leia as informações no Resumo de pré-instalação e clique em **[!UICONTROL Instalar]**.
1. Quando a instalação estiver concluída, clique em **[!UICONTROL Próximo]** para aplicar as atualizações de correção rápida aos arquivos instalados.
1. **[Somente para Windows]:** Execute uma das seguintes etapas:

   * Desmarque a opção **Iniciar o Gerenciador de Configurações** antes de clicar em **[!UICONTROL Concluído]**. Executar **Gerenciador de configurações** usando o **ConfigurationManager.bat** arquivo localizado em `[aem-forms root]\configurationManager\bin`.

   * Ou desmarque a opção **Iniciar o Gerenciador de Configurações** antes de clicar em **[!UICONTROL Concluído]**. Antes de executar **Gerenciador de configurações** usar **ConfigurationManager.exe** ou **ConfigurationManager_IPv6.exe**, navegue até *`<AEMForms_Install_Dir>\configurationManager\bin`* direcionar e substituir [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) e [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) arquivos.

      >[!NOTE]
      >
      >* Atualizar ou substituir o **ConfigurationManager.bat** ajuda a evitar a atualização manual dos arquivos .lax.


1. **[Somente para Unix]:** A variável **Iniciar o Gerenciador de Configurações** é marcada por padrão. Clique em **[!UICONTROL Concluído]** para executar o Gerenciador de configurações instantaneamente ou **Gerenciador de configurações** posteriormente, desmarque a opção **Iniciar o Gerenciador de Configurações** antes de clicar em **[!UICONTROL Concluído]**. Você pode começar **Gerenciador de configurações** posteriormente usando o script apropriado na `[AEM_forms_root]/configurationManager/bin` diretório.

1. Dependendo do servidor de aplicativos, escolha um dos seguintes documentos e siga as instruções na *Configuração e implantação de formulários AEM* seção.

   * [Instalação e implantação de formulários AEM para JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Instalação e implantação de formulários AEM para WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)
   * [Instalação e implantação do AEM Forms para WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65)
   * [Instalação e implantação de formulários AEM para JBoss® Cluster](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [Instalação e implantação de formulários AEM para WebSphere® Cluster](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [Instalação e implantação do AEM Forms para WebLogic Cluster](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
> Depois de instalar o AEM Forms no service pack JEE, é necessário remover o pacote complementar do Forms de `crx-repository\install` antes de reiniciar o appserver. Baixe o pacote complementar mais recente do Forms na [Portal de distribuição de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

+++4. Instalar o fragmento do servlet

>[!NOTE]
>
> * No caso, você está atualizando do **AEM Service Pack 6.5.15.0**, não é necessário instalar o **fragmento de servlet**. Se estiver atualizando de uma versão anterior à **AEM Service Pack 6.5.15.0**, é obrigatório instalar o **fragmento de servlet**.
> * É obrigatório instalar o **fragmento de servlet** para todos os servidores de aplicativos, exceto os executados em **JBoss® EAP 7.4.0**.



Para baixar e instalar o fragmento de servlet:

1. Se você não tiver baixado o fragmento, baixe-o de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

1. Inicie o servidor de aplicativos, aguarde os logs estabilizarem e verifique o estado do pacote.

1. Abra os Pacotes de console da Web. O URL padrão é `http://[Server]:[Port]/system/console/bundles`.

1. Clique em Instalar/Atualizar. Escolha o fragmento baixado, `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. Clique em **Instalar** ou **Atualizar**. Aguarde o servidor de aplicativos estabilizar

1. Interrompa o servidor de aplicativos.

+++

+++5. Instale o AEM Service Pack

1. Reinicie a instância antes da instalação se ela estiver no modo de atualização (quando a instância tiver sido atualizada de uma versão anterior). O Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.
1. Antes de instalar o, faça um instantâneo ou um novo backup de seu [!DNL Experience Manager] instância.
1. Baixe o pacote de serviços de [Distribuição de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Abra o Gerenciador de pacotes e selecione **[!UICONTROL Fazer upload do pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).
1. Selecione o pacote e **[!UICONTROL Instalar]**.

**Instalação automática**

Há dois métodos diferentes que você pode usar para instalar automaticamente o [!DNL ExperienceManager] pacote de serviços.<!--       UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote em `../crx-quickstart/install` pasta quando o servidor estiver disponível online.
O pacote é instalado automaticamente.

* Use o [API HTTP do Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR). Uso  `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

   >[!NOTE]
   >
   >o service pack do Experience Manager não suporta a instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar a instalação**

Para conhecer as plataformas certificadas para trabalhar com esta versão, consulte a [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a string da versão atualizada `Adobe Experience Manager (spversion)` em [!UICONTROL Produtos instalados].<!-- UPDATE FOR EACH NEW RELEASE -->
1. Todos os pacotes OSGi são **[!UICONTROL ATIVO]** ou **[!UICONTROL FRAGMENTO]** no console OSGi (Use o console da Web: `/system/console/bundles`).
1. O pacote OSGi `org.apache.jackrabbit.oak-core` é versão 1.22.14 ou posterior (Use o WebConsole: `/system/console/     bundles`).

+++

+++6. Instalar o pacote complementar do AEM Experience Manager Forms

1. Verifique se você instalou o [!DNL Experience Manager] pacote de serviços.
1. Baixe o pacote complementar do Forms correspondente listado em [Versões do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) para seu sistema operacional.
1. Instale o pacote complementar do Forms conforme descrito em [Instalação de pacotes complementares do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. Se você usa letras no Experience Manager 6.5 Forms, instale o [pacote de compatibilidade do AEMFD mais recente](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## Baixar e instalar o Service Pack em um formulário AEM em um ambiente OSGi {#download-and-install-for-osgi-service-pack}

![Etapas de instalação do OSGi](/help/forms/using/assets/osgiinstallation.png)


+++1. Faça backup do ambiente existente:

1. Faça backup do seu [Esquema de banco de dados e repositório CRX](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).

>[!NOTE]
>
> Se você instalar o AEM Forms service pack para banco de dados relacional, é obrigatório fazer backup de DB_schema.

+++

+++2.Faça o download do software necessário:

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=pt-BR)
* [Pacote complementar do Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)

+++

+++3. Instale o AEM Service Pack

1. Reinicie a instância antes da instalação se ela estiver no modo de atualização (quando a instância tiver sido atualizada de uma versão anterior). O Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.
1. Antes de instalar o, faça um instantâneo ou um novo backup de seu [!DNL Experience Manager] instância.
1. Baixe o pacote de serviços de [Distribuição de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Abra o Gerenciador de pacotes e selecione **[!UICONTROL Fazer upload do pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).
1. Selecione o pacote e **[!UICONTROL Instalar]**.

**Instalação automática**

Há dois métodos diferentes que você pode usar para instalar automaticamente o [!DNL Experience Manager] pacote de serviços.<!--  UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote em `../crx-quickstart/install` pasta quando o servidor estiver disponível online. O pacote é instalado automaticamente.
* Use o [API HTTP do Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR). Uso `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

   >[!NOTE]
   >
   >o service pack do Experience Manager não suporta a instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar a instalação**

Para conhecer as plataformas certificadas para trabalhar com esta versão, consulte a [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a string da versão atualizada `Adobe Experience Manager (spversion)` em [!UICONTROL Produtos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos os pacotes OSGi são **[!UICONTROL ATIVO]** ou **[!UICONTROL FRAGMENTO]** no console OSGi (Use o console da Web: `/system/console/bundles`).

   1. O pacote OSGi `org.apache.jackrabbit.oak-core` O é versão 1.22.14 ou posterior (Use o Console da Web: `/system/console/bundles`).

+++

+++4. Instalar o pacote complementar do AEM Experience Manager Forms

1. Verifique se você instalou o [!DNL Experience Manager] pacote de serviços.
1. Baixe o pacote complementar do Forms correspondente listado em [Versões do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) para seu sistema operacional.
1. Instale o pacote complementar do Forms conforme descrito em [Instalação de pacotes complementares do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. Se você usa letras no Experience Manager 6.5 Forms, instale o [pacote de compatibilidade do AEMFD mais recente](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## Resolução de problemas

* Se **Caixa de diálogo na interface do usuário do Gerenciador de pacotes** sai durante a instalação do service pack, aguarde a estabilização dos logs de erro antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações serão bem-sucedidas. Normalmente, esse problema ocorre no navegador Safari, mas pode ocorrer intermitentemente em qualquer navegador.

* Verifique os registros do monitor (error.log) após a conclusão da instalação para verificar se há atividade. Aguarde alguns minutos até que não haja atividade nos logs. Reinicie a instância do AEM.

* Caso você obtenha uma **erro de serviço indisponível** após instalar o pacote de serviços AEM Forms 6.5.15.0, [instalar o fragmento e o pacote do servlet](/help/forms/using/aem-service-pack-installation-solution.md) para corrigir o erro.
