---
title: Instruções de instalação de patches do AEM Forms para AEM Forms
description: Instruções de instalação do service pack do AEM Forms para o ambiente OSGi e JEE
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: c4584e34b5b12f29dc995bd5483bcbad476a82ef
workflow-type: tm+mt
source-wordcount: '1767'
ht-degree: 9%

---

# AEM 6.5 Instruções de instalação do Forms Service Pack {#aem-form-patch-installation-instructions}

## Informações da versão

| Produto | Adobe Experience Manager 6.5 Forms |
|---|---|
| Versão | 6.5.15.0 |
| Tipo | Versão do Service Pack |
| Data | 01 de dezembro de 2023 |
| URL de download | [Versões mais recentes da AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) |

>[!NOTE]
>
>Veja o mais recente [Notas de versão do AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=pt-BR) para obter uma lista completa de problemas corrigidos.

## O que está incluído no Experience Manager Forms 6.5

O Adobe Experience Manager (AEM) Forms service pack inclui recursos novos e atualizados, como aprimoramentos principais solicitados pelo cliente, desempenho, estabilidade e aprimoramentos de segurança. Pacotes do serviço de versão do AEM Forms em um intervalo regular para fornecer os recursos e as melhorias mais recentes. Dependendo da pilha, escolha um dos seguintes caminhos para baixar e instalar o service pack no seu ambiente:

* [Baixe e instale o Service Pack em um formulário AEM no ambiente JEE](#download-and-install-for-jee-service-pack)
* [Baixe e instale o Service Pack em um formulário AEM no ambiente OSGi](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> O Adobe lança um instalador completo após cada 6º service pack. AEM 6.5 Forms Service Pack 12 (6.5.12.0) no JEE é o último instalador completo. O instalador completo oferece suporte para novas plataformas, enquanto o instalador regular do service pack inclui apenas correções de erros e melhorias gerais. Se você estiver executando uma nova instalação ou planejando usar o software mais recente para o seu AEM 6.5 Forms no ambiente JEE, o Adobe recomenda usar o AEM 6.5.12.0 Forms no instalador completo JEE lançado em 3 de março de 2022, em vez do instalador AEM 6.5 Forms lançado em 8 de abril de 2019. Depois de usar o instalador completo, instale o service pack mais recente.

## Baixe e instale o Service Pack em um formulário AEM no ambiente JEE {#download-and-install-for-jee-service-pack}

![Instalação JEE](/help/forms/using/assets/jeeinstallation.png)

+++1. Faça backup do seu ambiente existente:

1. Faça backup do seu [Repositório CRX, esquema de banco de dados e GDS (armazenamento global de documentos)](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).
1. Faça o backup do &lt;*AEM_forms_root*>/implantar pasta. É necessário se você decidir desinstalar o service pack.

>[!NOTE]
>
> Antes de executar o instalador AEM service pack, verifique se você tem privilégios de acesso de gravação AEM diretório de instalação.

+++

+++2.Baixe o software necessário:

* [AEM Forms no Service Pack do JEE 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM 6.5.15.0 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=pt-BR)
* [Pacote complementar do Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [Servlet de fragmento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

+++

+++3. Instale o AEM Forms no service pack JEE:

1. Interrompa o servidor de aplicativos.
1. Extraia o **Arquivo do instalador do AEM Forms no JEE 6.5.15.0 Service Pack** ao disco rígido:

   * **Windows**
Navegue até o diretório apropriado na mídia ou pasta de instalação do disco rígido onde você copiou o instalador e clique duas vezes no 
`aemforms65_cfp_install.exe` arquivo.

      * (Windows de 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows de 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux®**
Navegue até o diretório apropriado e a partir de um shell e digite 
`./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Isso inicia um assistente de instalação que o guiará durante a instalação.

1. No painel de Introdução, clique em **[!UICONTROL Próximo]**.
1. No **Escolha a pasta Instalar** verifique se o local padrão exibido está correto para a instalação existente ou clique em **[!UICONTROL Procurar]** para selecionar a pasta alternativa onde AEM formulários está instalado e clique em **[!UICONTROL Próximo]**.
1. Leia as informações de resumo do Service Pack e clique em **[!UICONTROL Próximo]**.
1. Leia as informações no Resumo de pré-instalação e clique em **[!UICONTROL Instalar]**.
1. Quando a instalação estiver concluída, clique em **[!UICONTROL Próximo]** para aplicar as atualizações de correção rápida aos arquivos instalados.
1. **[Somente para Windows]:** Execute uma das seguintes etapas:

   * Desmarque a opção **Iniciar o Configuration Manager** antes de clicar **[!UICONTROL Concluído]**. Executar **Gerenciador de configuração** usando o **ConfigurationManager.bat** arquivo localizado em `[aem-forms root]\configurationManager\bin`.

   * Ou desmarque a opção **Iniciar o Configuration Manager** antes de clicar **[!UICONTROL Concluído]**. Antes de executar **Gerenciador de configuração** usar **ConfigurationManager.exe** ou **ConfigurationManager_IPv6.exe**, navegue até *`<AEMForms_Install_Dir>\configurationManager\bin`* direcionar e substituir [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) e [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) arquivos.

      >[!NOTE]
      >
      >* Atualização ou substituição do **ConfigurationManager.bat** ajuda a evitar a atualização manual do nome dos arquivos .lax.


1. **[Somente para baseado em Unix]:** O **Iniciar o Configuration Manager** é selecionada por padrão. Clique em **[!UICONTROL Concluído]** para executar o Configuration Manager instantaneamente ou para executar **Gerenciador de configuração** depois, desmarque a opção **Iniciar o Configuration Manager** antes de clicar **[!UICONTROL Concluído]**. Você pode começar **Gerenciador de configuração** mais tarde, usando o script apropriado na `[AEM_forms_root]/configurationManager/bin` diretório.

1. Dependendo do servidor de aplicativos, escolha um dos seguintes documentos e siga as instruções em *Configuração e implantação de formulários AEM* seção.

   * [Instalação e implantação de formulários AEM para JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Instalar e implantar formulários de AEM para o WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65)
   * [Instalação e implantação do AEM Forms para WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65)
   * [Instalação e implantação de formulários AEM para Cluster JBoss®](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [Instalar e implantar formulários de AEM para o WebSphere® Cluster](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [Instalar e implantar o AEM Forms para o cluster do WebLogic](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
> Depois de instalar o AEM Forms no service pack JEE, é necessário remover o pacote complementar do Forms de `crx-repository\install` pasta antes de reiniciar o appserver. Baixe o pacote complementar mais recente do Forms no [Portal de distribuição de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

+++4. Instalar o fragmento de servlet

>[!NOTE]
>
> É obrigatório instalar o **fragmento de servlet** para todos os servidores de aplicativos, exceto aqueles que estão sendo executados em **JBoss® EAP 7.4.0**.


Para baixar e instalar o fragmento de servlet:

1. Se você não tiver baixado o fragmento, baixe-o de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

1. Inicie o servidor de aplicativos, aguarde os logs para estabilizar e verificar o estado do pacote.

1. Abra Pacotes do Console da Web. O URL padrão é `http://[Server]:[Port]/system/console/bundles`.

1. Clique em Instalar/atualizar. Escolha o fragmento baixado, `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. Clique em **Instalar** ou **Atualizar**. Aguarde a estabilização do servidor de aplicativos

1. Pare o servidor de aplicativos.

+++

+++5. Instale o AEM Service Pack

1. Reinicie a instância antes da instalação se a instância estiver no modo de atualização (quando a instância foi atualizada de uma versão anterior). O Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.
1. Antes de instalar, faça um instantâneo ou um novo backup de sua [!DNL Experience Manager] instância.
1. Baixe o service pack de [Distribuição de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Abra o Gerenciador de Pacotes e selecione **[!UICONTROL Fazer upload do pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).
1. Selecione o pacote e selecione **[!UICONTROL Instalar]**.
1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Armazenamento de dados do Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

**Instalação automática**

Há dois métodos diferentes que podem ser usados para instalar automaticamente [!DNL ExperienceManager] 6.5.15.0<!--       UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote em `../crx-quickstart/install` quando o servidor estiver disponível online.
O pacote é instalado automaticamente.

* Use o [API HTTP do Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR). Use  `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

   >[!NOTE]
   >
   >O Experience Manager 6.5.15.0 não suporta a instalação do Bootstrap. <!-- UPDATE FOR EACHNEW RELEASE -->

**Validar a instalação**

Para conhecer as plataformas certificadas para funcionar com esta versão, consulte o [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a sequência de caracteres da versão atualizada `Adobe Experience      Manager (6.5.15.0)` under [!UICONTROL Produtos instalados].<!-- UPDATE FOR EACH NEW RELEASE -->
1. Todos os pacotes OSGi são **[!UICONTROL ATIVO]** ou **[!UICONTROL FRAGMENTO]** no console OSGi (Use o console da Web: `/system/console/bundles`).
1. O pacote OSGi `org.apache.jackrabbit.oak-core` é versão 1.22.13 ou posterior (Use o WebConsole: `/system/console/     bundles`).

+++

+++6. Instalar AEM pacote do complemento Experience Manager Forms

1. Verifique se você instalou o [!DNL Experience Manager] service pack.
1. Baixe o pacote complementar do Forms correspondente listado em [Versões do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) para seu sistema operacional.
1. Instale o pacote complementar do Forms conforme descrito em [Instalação de pacotes complementares do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. Se você usar letras no Experience Manager 6.5 Forms, instale o [Pacote de compatibilidade AEMFD mais recente](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## Baixe e instale o Service Pack em um formulário AEM no ambiente OSGi {#download-and-install-for-osgi-service-pack}

![Etapas de instalação do OSGi](/help/forms/using/assets/osgiinstallation.png)


+++1. Faça backup do seu ambiente existente:

1. Faça backup do seu [Repositório CRX e esquema de banco de dados](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).

>[!NOTE]
>
> Se você instalar o service pack do AEM Forms para o banco de dados relacional, é obrigatório fazer backup do DB_schema.

+++

+++2.Baixe o software necessário:

* [AEM 6.5.15.0 Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=pt-BR)
* [Pacote complementar do Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)

+++

+++3. Instale o AEM Service Pack

1. Reinicie a instância antes da instalação se a instância estiver no modo de atualização (quando a instância foi atualizada de uma versão anterior). O Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.
1. Antes de instalar, faça um instantâneo ou um novo backup de sua [!DNL Experience Manager] instância.
1. Baixe o service pack de [Distribuição de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Abra o Gerenciador de Pacotes e selecione **[!UICONTROL Fazer upload do pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).
1. Selecione o pacote e selecione **[!UICONTROL Instalar]**.
1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Armazenamento de dados do Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

**Instalação automática**

Há dois métodos diferentes que podem ser usados para instalar automaticamente [!DNL Experience Manager] 6.5.15.0<!--       UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote em `../crx-quickstart/install` quando o servidor estiver disponível online. O pacote é instalado automaticamente.
* Use o [API HTTP do Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

   >[!NOTE]
   >
   >O Experience Manager 6.5.15.0 não suporta a instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar a instalação**

Para conhecer as plataformas certificadas para funcionar com esta versão, consulte o [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a sequência de caracteres da versão atualizada `Adobe Experience      Manager (6.5.15.0)` under [!UICONTROL Produtos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos os pacotes OSGi são **[!UICONTROL ATIVO]** ou **[!UICONTROL FRAGMENTO]** no console OSGi (Use o console da Web: `/system/console/bundles`).

   1. O pacote OSGi `org.apache.jackrabbit.oak-core` é versão 1.22.13 ou posterior (Use o Console da Web: `/system/console/bundles`).

+++

+++4. Instalar AEM pacote do complemento Experience Manager Forms

1. Verifique se você instalou o [!DNL Experience Manager] service pack.
1. Baixe o pacote complementar do Forms correspondente listado em [Versões do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) para seu sistema operacional.
1. Instale o pacote complementar do Forms conforme descrito em [Instalação de pacotes complementares do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
1. Se você usar letras no Experience Manager 6.5 Forms, instale o [Pacote de compatibilidade AEMFD mais recente](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

+++

## Resolução de problemas

* If **Caixa de diálogo na interface do usuário do Gerenciador de pacotes** sai durante a instalação do service pack, aguarde a estabilização dos registros de erros antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações foram bem-sucedidas. Normalmente, esse problema ocorre no navegador Safari, mas pode ocorrer intermitentemente em qualquer navegador.

* Verifique os registros do monitor (error.log) assim que a instalação for concluída para qualquer atividade. Aguarde alguns minutos até que não haja nenhuma atividade nos logs. Reinicie a instância de AEM.

* Caso tenha um **erro de serviço indisponível** após instalar o service pack do AEM Forms 6.5.15.0, [instale o fragmento e o pacote do servlet](/help/forms/using/aem-service-pack-installation-solution.md) para corrigir o erro.
