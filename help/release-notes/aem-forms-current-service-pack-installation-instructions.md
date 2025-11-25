---
title: Instruções de instalação de patch do AEM Forms para o AEM Forms
description: Instruções de instalação do pacote de serviços da AEM Forms para ambientes OSGi e JEE
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '1722'
ht-degree: 6%

---

# Instruções de instalação do AEM 6.5 Forms Service Pack {#aem-form-patch-installation-instructions}

## Informações da versão

| Produto | Adobe Experience Manager 6.5 Forms |
|---|---|
| Versão | 6.5.23.0 |
| Tipo | Versão do pacote de serviços |
| Data | 6 de junho de 2025 |
| URL de download | [Últimas versões do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR) |

>[!NOTE]
>
>Consulte as [Notas de versão do AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=pt-BR) mais recentes para obter uma lista completa de problemas corrigidos.

## O que está incluído no Experience Manager Forms 6.5

O Adobe Experience Manager (AEM) Forms Service Pack inclui recursos novos e atualizados, como importantes melhorias solicitadas por clientes, desempenho, estabilidade e segurança. Service packs de lançamento do AEM Forms em intervalos regulares para fornecer os recursos e as melhorias mais recentes. Dependendo do seu conjunto de tecnologias, escolha um dos seguintes caminhos para baixar e instalar o service pack em seu ambiente:

* [Baixe e instale o Service Pack em um Formulário do AEM no ambiente JEE](#download-and-install-for-jee-service-pack)
* [Baixar e instalar o Service Pack em um Formulário do AEM em um ambiente OSGi](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> * A Adobe lança um instalador completo a cada sexto service pack. O AEM 6.5 Forms Service Pack 18 (6.5.18.0) é o instalador completo mais recente do JEE. O instalador completo oferece suporte a novas plataformas, enquanto o instalador regular de pacotes de serviços inclui novos recursos, correção de erros e melhorias gerais. Se você estiver executando uma nova instalação ou planejando usar o software mais recente para o AEM 6.5 Forms no ambiente JEE, a Adobe recomenda usar o instalador completo do AEM 6.5.18.0 Forms no JEE lançado em 31 de agosto de 2023, em vez do instalador do AEM 6.5 Forms lançado em 08 de abril de 2019 ou do AEM 6.5.12.0 Forms Installer lançado em 03 de março de 2022. Depois de usar o instalador completo, instale o pacote de serviços mais recente.
> * O recurso do AEM Forms, como o Adaptive Forms, disponível no [AEM 6.5 QuickStart](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=pt-BR), destina-se apenas a fins de exploração e avaliação. Para uso em produção, é essencial obter uma licença válida para o AEM Forms.

<!--

## Prerequisites {#prerequisites}

From AEM Service Pack 6.5.19.0 and onwards, XMLFM (XML output) will be available in 64-bit only, therefore you require the latest [Microsoft Visual C++ Redistributable (2015-2022) 64-bit](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) to be installed on Windows Server prior to JEE or OSGi installation.

>[!NOTE]
> This prerequisite is required in addition to the already existing Microsoft Visual C++ Redistributable 32-bit.

-->

## Baixar e instalar o Service Pack em um formulário do AEM no ambiente JEE {#download-and-install-for-jee-service-pack}

<!--
![JEE Installation](/help/forms/using/assets/jeeinstallation.png) -->

+++&#x200B;1. Fazer backup do ambiente existente

1. Faça backup do [Repositório CRX, Esquema de Banco de Dados e GDS (Armazenamento Global de Documentos)](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html?lang=pt-BR).
1. Faça backup da pasta &lt;*AEM_forms_root*>/deploy.

>[!NOTE]
>
> Antes de executar o instalador do pacote de serviços da AEM, verifique se você tem privilégios de acesso de gravação no diretório de instalação do AEM.

+++

+++&#x200B;2. Baixar o software necessário

* [AEM Forms no JEE Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR)

* [Servlet de fragmento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=pt-BR)
* [Pacote complementar do Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR)


+++

+++&#x200B;3. Instalar pacotes redistribuíveis do Microsoft Visual C++

* Baixe e instale a versão [64 bits dos pacotes redistribuíveis do Microsoft Visual C++ para Visual Studio 2015, 2017, 2019 e 2022](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) no computador em que o AEM 6.5 Forms está instalado.

>[!NOTE]
>
> Instale o Redistribuível, mesmo que uma versão anterior esteja instalada, para garantir a disponibilidade da versão mais recente.

+++

+++&#x200B;4. Instale o AEM Forms no service pack JEE:

1. Interrompa o servidor de aplicativos.
1. Extraia o **arquivo do instalador do AEM Forms no JEE Service Pack** para o disco rígido:

   * **Janelas**
Navegue até o diretório apropriado na mídia ou pasta de instalação no disco rígido em que você copiou     instalador e clique duas vezes no arquivo `aemforms65_cfp_install.exe`.

      * (Windows de 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows 64-bit) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
Navegue até o diretório apropriado, em um shell e digite `./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Isso inicia um assistente de instalação que o guiará durante a instalação.

1. No painel de Introdução, clique em **[!UICONTROL Próximo]**.
1. Na tela **Escolher Pasta de Instalação**, verifique se o local padrão exibido está correto para sua instalação existente ou clique em **[!UICONTROL Procurar]** para selecionar a pasta alternativa em que o AEM Forms está instalado e clique em **[!UICONTROL Avançar]**.
1. Leia as informações de resumo do Service Pack e clique em **[!UICONTROL Avançar]**.
1. Leia as informações no Resumo de pré-instalação e clique em **[!UICONTROL Instalar]**.
1. Quando a instalação estiver concluída, clique em **[!UICONTROL Próximo]** para aplicar as atualizações de correção rápida aos arquivos instalados.
1. **[Somente para Windows]:** Execute uma das seguintes etapas:

   * Desmarque a opção **Iniciar Gerenciador de Configurações** antes de clicar em **[!UICONTROL Concluído]**. Execute o **Configuration Manager** usando o arquivo **ConfigurationManager.bat** em `[aem-forms root]\configurationManager\bin`.

   * Ou desmarque a opção **Iniciar Gerenciador de Configurações** antes de clicar em **[!UICONTROL Concluído]**. Antes de executar o **Configuration Manager** usando o **ConfigurationManager.exe** ou o **ConfigurationManager_IPv6.exe**, navegue até o diretório *`<AEMForms_Install_Dir>\configurationManager\bin`* e substitua os arquivos **ConfigurationManager.lax** e **ConfigurationManager_IPV6.lax** mais recentes por [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) e [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax), Pesquise e substitua **axis-1.4.1.1.jar** com **axis-1.4.1.2.jar** nesses dois arquivos.

     >[!NOTE]
     >
     >* Atualizar ou substituir o arquivo **ConfigurationManager.bat** ajuda a evitar a atualização manual dos arquivos .lax.

1. **[Somente para Unix]:** A caixa de seleção **Iniciar Gerenciador de Configurações** está marcada por padrão. Clique em **[!UICONTROL Concluído]** para executar o Gerenciador de Configurações instantaneamente ou para executar o **Gerenciador de Configurações** mais tarde, desmarque a opção **Iniciar Gerenciador de Configurações** antes de clicar em **[!UICONTROL Concluído]**. Você pode iniciar o **Configuration Manager** posteriormente usando o script apropriado no diretório `[AEM_forms_root]/configurationManager/bin`.

1. Dependendo do servidor de aplicativos, escolha um dos seguintes documentos e siga as instruções na seção *Configuração e implantação do AEM Forms*.

   * [Instalando e implantando formulários AEM para JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_br)
   * [Instalando e implantando formulários AEM para WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_br)
   * [Instalando e Implantando o AEM Forms para WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65_br)
   * [Instalando e implantando formulários AEM para JBoss® Cluster](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [Instalando e implantando o AEM Forms para WebSphere® Cluster](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [Instalando e Implantando o AEM Forms para o Cluster WebLogic](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
>* Após instalar o AEM Forms no service pack JEE, é necessário remover o pacote complementar do Forms da pasta `crx-repository\install` antes de reiniciar o appserver. Baixe o pacote complementar mais recente do Forms no [Portal de Distribuição de Software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR).
>* É recomendável usar o comando &#39;Ctrl + C&#39; para reiniciar o SDK. Reiniciar o AEM SDK usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.
>* Para [Hotfix para Redução de vulnerabilidades do Spring Framework para AEM Forms no JEE](/help/release-notes/aem-forms-hotfix.md), ao implantar em um ambiente de cluster, é essencial garantir que os localizadores sejam iniciados usando o JDK 17.

+++

+++&#x200B;5. Instale o fragmento de servlet se não estiver instalado (**Etapa obrigatória**)

<!-- >[!NOTE] > > * If you are upgrading from **AEM Service Pack 6.5.15.0**, the installation of the **servlet fragment** is not required. For versions **AEM Service Pack 6.5.14.0** or earlier, it is **mandatory to install** the servlet fragment. -->

Para baixar e instalar o fragmento de servlet:

1. Se você não tiver baixado o fragmento, baixe-o da [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

2. Inicie o servidor de aplicativos, aguarde os logs estabilizarem e verifique o estado do pacote.

3. Abra os Pacotes de console da Web. A URL padrão é `http://[Server]:[Port]/system/console/bundles`.

4. Clique em Instalar/Atualizar. Escolha o fragmento baixado, `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. Clique em **Instalar** ou **Atualizar**. Aguarde o servidor de aplicativos estabilizar

5. Interrompa o servidor de aplicativos.

+++

+++&#x200B;6. Instalar o AEM Service Pack

1. Reinicie a instância antes da instalação se ela estiver no modo de atualização (quando a instância tiver sido atualizada de uma versão anterior). A Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.
1. Antes de instalar, faça um instantâneo ou um novo backup da instância do [!DNL Experience Manager].
1. Baixe o pacote de serviços de [Distribuição de Software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Abra o Gerenciador de Pacotes e selecione **[!UICONTROL Carregar Pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).
1. Selecione o pacote e depois selecione **[!UICONTROL Instalar]**.

**Instalação automática**

Há dois métodos diferentes que você pode usar para instalar automaticamente o [!DNL ExperienceManager] service pack.<!--       UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote na pasta `../crx-quickstart/install` quando o servidor estiver disponível online.
O pacote é      instalado automaticamente.

* Use a [API HTTP do Gerenciador de Pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

  >[!NOTE]
  >
  >O service pack do Experience Manager não é compatível com a instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

  **Validar a instalação**

  Para conhecer as plataformas certificadas para trabalhar com esta versão, consulte os [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

   1. A página de informações do produto (`/system/console/productinfo`) exibe a cadeia de caracteres da versão atualizada `Adobe Experience Manager (spversion)` em [!UICONTROL Produtos Instalados].<!-- UPDATE FOR EACH NEW RELEASE -->
   1. Todos os pacotes OSGi estão **[!UICONTROL ATIVOS]** ou **[!UICONTROL FRAGMENTOS]** no Console OSGi (Use a Web     Console: `/system/console/bundles`).
   1. O pacote OSGi `org.apache.jackrabbit.oak-core` é versão 1.22.14 ou posterior (Use WebConsole: `/system/console/bundles`).

+++

+++&#x200B;7. Instalar o pacote complementar do AEM Experience Manager Forms

1. Verifique se você instalou o service pack [!DNL Experience Manager].
1. Baixe o pacote complementar do Forms correspondente listado em [Versões do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR) para seu sistema operacional.
1. Instale o pacote complementar do Forms conforme descrito em [Instalando pacotes complementares do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR).
1. Se você usa letras no Experience Manager 6.5 Forms, instale o [pacote mais recente de Compatibilidade do AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR).

+++

## Baixar e instalar o Service Pack em um formulário do AEM em um ambiente OSGi {#download-and-install-for-osgi-service-pack}


<!-- ![OSGi Installation Steps](/help/forms/using/assets/osgiinstallation.png)
-->

+++&#x200B;1. Fazer backup do ambiente existente

1. Faça backup do [Esquema de Banco de Dados e Repositório do CRX](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html?lang=pt-BR).

>[!NOTE]
>
> Se você instalar o AEM Forms service pack para banco de dados relacional, é obrigatório fazer backup de DB_schema.

+++

+++&#x200B;2. Baixar o software necessário

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=pt-BR)
* [Pacote complementar do Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR)

+++

+++ &#x200B;3. Instalar pacotes redistribuíveis do Microsoft Visual C++

* Baixe e instale a versão [64 bits dos pacotes redistribuíveis do Microsoft Visual C++ para Visual Studio 2015, 2017, 2019 e 2022](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) no computador em que o AEM 6.5 Forms está instalado.

>[!NOTE]
>
>
> Instale o Redistribuível, mesmo que uma versão anterior esteja instalada, para garantir a disponibilidade da versão mais recente.

+++

+++&#x200B;4. Instalar o AEM Service Pack

1. Reinicie a instância antes da instalação se ela estiver no modo de atualização (quando a instância tiver sido atualizada de uma versão anterior). A Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.
1. Antes de instalar, faça um instantâneo ou um novo backup da instância do [!DNL Experience Manager].
1. Baixe o pacote de serviços de [Distribuição de Software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Abra o Gerenciador de Pacotes e selecione **[!UICONTROL Carregar Pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).
1. Selecione o pacote e depois selecione **[!UICONTROL Instalar]**.

**Instalação automática**

Há dois métodos diferentes que você pode usar para instalar automaticamente o [!DNL Experience Manager] service pack.<!--  UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote na pasta `../crx-quickstart/install` quando o servidor estiver disponível online. O pacote é      instalado automaticamente.
* Use a [API HTTP do Gerenciador de Pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

  >[!NOTE]
  >
  >O service pack do Experience Manager não é compatível com a instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

  **Validar a instalação**

  Para conhecer as plataformas certificadas para trabalhar com esta versão, consulte os [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

   1. A página de informações do produto (`/system/console/productinfo`) exibe a cadeia de caracteres da versão atualizada `Adobe Experience Manager (spversion)` em [!UICONTROL Produtos Instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

   1. Todos os pacotes OSGi estão **[!UICONTROL ATIVOS]** ou **[!UICONTROL FRAGMENTOS]** no Console OSGi (Use o Console da Web: `/system/console/bundles`).

      1. O pacote OSGi `org.apache.jackrabbit.oak-core` é versão 1.22.14 ou posterior (Use o Console da Web: `/system/console/bundles`).

+++

+++&#x200B;5. Instalar o pacote complementar do Adobe Experience Manager Forms (AEM)

1. Verifique se você instalou o service pack [!DNL Experience Manager].
1. Baixe o pacote complementar do Forms correspondente listado em [Versões do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR) para seu sistema operacional.
1. Instale o pacote complementar do Forms conforme descrito em [Instalando pacotes complementares do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR).
1. Se você usa letras no Experience Manager 6.5 Forms, instale o [pacote mais recente de Compatibilidade do AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR).

+++

## Resolução de problemas

* Se a **Caixa de diálogo na interface do usuário do Gerenciador de Pacotes** sair durante a instalação do service pack, aguarde a estabilização dos logs de erros antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações serão bem-sucedidas. Normalmente, esse problema ocorre no navegador Safari, mas pode ocorrer intermitentemente em qualquer navegador.

* Verifique os registros do monitor (error.log) após a conclusão da instalação para verificar se há atividade. Aguarde alguns minutos até que não haja atividade nos logs. Reinicie a instância do AEM.

* Caso você receba um **erro de serviço indisponível** após instalar o AEM Forms 6.5.15.0 ou o service pack posterior, [instale o fragmento e o pacote do servlet](/help/forms/using/aem-service-pack-installation-solution.md) para corrigir o erro.
