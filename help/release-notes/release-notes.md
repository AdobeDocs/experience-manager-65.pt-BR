---
title: Notas de versão para [!DNL Adobe Experience Manager] 6,5
description: '[!DNL Adobe Experience Manager]As notas o 6.5 que descrevem as informações da versão, novidades, como instalar e listas detalhadas de modificação.'
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: b3a3ba8f990d91e003ff862239094ee330b7429a
workflow-type: tm+mt
source-wordcount: '2630'
ht-degree: 6%

---

# [!DNL Adobe Experience Manager] 6.5 Notas de versão mais recentes do Service Pack {#aem-service-pack-release-notes}

## Informações da versão {#release-information}

| Produtos | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.12.0 |
| Tipo | Lançamento do Service Pack |
| Data | 24 de fevereiro de 2022 |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.12.0.zip) |

## O que está incluído em [!DNL Adobe Experience Manager] 6.5.12.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] A versão 6.5.12.0 inclui novos recursos, principais melhorias solicitadas pelo cliente e melhorias de desempenho, estabilidade e segurança, lançadas desde a disponibilização da versão 6.5 em abril de 2019. O service pack está instalado em [!DNL Adobe Experience Manager] 6.5.

Os principais recursos e aprimoramentos introduzidos no [!DNL Adobe Experience Manager] 6.5.12.0 são:

* Após configurar uma conexão entre implantações remotas do DAM e do Sites, os ativos no DAM remoto são disponibilizados na implantação do Sites. Agora é possível executar as operações de atualização, exclusão, renomeação e movimentação nos ativos ou pastas remotos do DAM. As atualizações, com algum atraso, estão disponíveis automaticamente na implantação do Sites (NPR-37816).

* Por padrão, implantações de push de uma fonte de live copy em várias cópias ativas agora são possíveis, sem exigir uma configuração de blueprint (CQ-4259951).
* O status das operações assíncronas em andamento agora é mostrado na interface do usuário para ajudar a impedir que os usuários acionem acidentalmente várias operações assíncronas no mesmo caminho (NPR-37611).
* O suporte para autenticação baseada em IMS é fornecido para APIs do Analytics 2.0 (CQ-4285474, NPR-37803, NPR-37701, NPR-37702, NPR-37703).
* Suporte a API para fragmento de experiência do tipo de oferta JSON (NPR-37796).
* A solicitação de oferta agora é fornecida para Exclusão de oferta (API de fragmento de experiência) no IMS (NPR-37668).
* O repositório integrado (Apache Jackrabbit Oak) ainda permanece em 1.22.9.

Esta é a lista de correções fornecidas em [!DNL Experience Manager] Versão 6.5.12.0.

### [!DNL Sites] {#sites-65120}

Os seguintes problemas foram corrigidos em [!DNL Sites]:

* O layout das Propriedades do fragmento de conteúdo é dividido quando as guias Básico e Avançado não têm margens à esquerda (SITES-4484).
* Opção para fechar o banner em fragmentos de conteúdo, referenciados em várias páginas do site, não está funcionando. Esse banner informa aos usuários que o fragmento de conteúdo é referenciado em uma ou mais páginas (SITES-4173).
* As caixas de seleção não estão alinhadas na caixa de diálogo Reverter herança (SITES-3514).
* A página de modelo em sites de varejo e wknd está quebrada, pois os componentes não são carregados e a opção de estrutura não está disponível, pois o servlet pageinfo.json está preso no LaunchManagerImpl.getLaunchStream (SITES-3489).
* A publicação do nó do usuário do ambiente Autor para publicação não está funcionando (NPR-38005).
* A tentativa de criar um fragmento de experiência usando um modelo editado não mostra as edições feitas nas propriedades da página inicial (NPR-37962).
* A operação de movimentação da página no Experience Manager é lenta (NPR-37961).
* A tradução do fragmento de experiência não atualiza referências a caminhos de cópia de idioma (NPR-37953).
* Os usuários sem permissões de replicação não podem excluir ou mover páginas, mesmo que as páginas não estejam ativadas (NPR-37936).
* Erros aleatórios org.apache.felix.metatype são observados no servidor (NPR-37935).
* As referências na interface de usuário de toque de administrador do Sites não estão exibindo os links de entrada corretamente (NPR-37934).
* O caminho de lançamento para adicionar novas páginas ou ativos não está disponível ao selecionar páginas em um trabalho de tradução (NPR-37912).
* As páginas de referência em um componente de lista adicionado nos fragmentos de experiência não são atualizadas para a página de destino ao promover a inicialização (NPR-37886).
* O ambiente do autor tem problemas com a interface do usuário, como o título da página do modo de Edição não é centralizado e o seletor de componentes permitidos no editor de políticas: a caixa de seleção de grupo ocupa toda a largura do contêiner, de modo que o rótulo é renderizado na próxima linha (NPR-37878).
* [Plataforma] O número da versão de xmlns:metatype no arquivo metatype.xml de commons-httpclient é &quot;http://www.osgi.org/xmlns/metatype/v1.0.0&quot; em vez de &quot;http://www.osgi.org/xmlns/metatype/v1.2.0&quot; (NPR-37865).
* Os erros são observados e as páginas não são movidas ao tentar uma página (NPR-37864).
* [Editor de Rich Text] A imagem não é renderizada na interface do usuário clássica ao adicionar a imagem como um item de lista no Editor de Rich Text (NPR-37835).
* Os autores podem aplicar tags que estão fora do caminho raiz configurado ao usar um campo de tag em uma caixa de diálogo (NPR-37834).
* Multifield não é renderizado corretamente no contêiner de layout e gera erro (NPR-37811).
* A tentativa de redimensionar o layout de componentes no editor de páginas não funciona no layout móvel (NPR-37805).
* A tradução do Fragmento de experiência não atualiza referências cíclicas para caminhos de cópia de idioma (NPR-37745).
* O uso do campo Rich Text cq-msm-lockable em propriedades da página não desativa o campo ao rolar a página e ele pode ser modificado pelos autores (NPR-37714).
* Ao ativar um fragmento de experiência, o editor envia muitas solicitações de ativação para o Dispatcher (NPR-37707).
* Na alteração da topologia, o trabalho do Sling para processamento de ativos é redefinido, resultando em trabalhos que estão em andamento no momento da alteração da topologia sendo ignorados (NPR-37706).
* As aspas, cruzamentos e traço não são exportadas para CSV quando os usuários dos URLs de ativos e sites de exportação do MacOS (NPR-37698) são exportados.
* O contêiner de layout SPA modelo de página não é capaz de registrar as classes CSS personalizadas definidas na Política de modelo ao executar reagem SPA páginas (NPR-37697).
* A imagem de plano de fundo não é visível quando o usuário seleciona o direcionamento em um fragmento de experiência que tem plano de fundo no contêiner (NPR-37662).
* O trabalho de tradução em um fragmento de experiência não está traduzindo todos os componentes nesse fragmento de experiência (NPR-37660).
* A tradução de fragmentos de experiência e da página que contém o fragmento de experiência não atualiza o caminho de inicialização no link do fragmento de experiência (NPR-37659).
* O widget Upload de arquivo não mostra o nome do arquivo, quando um arquivo é carregado e a caixa de diálogo é salva (NPR-37634).
* A ativação agendada (publicação) do ativo não é acionada no horário agendado se a pasta que contém esse ativo for movida (NPR-37621).
* [Plataforma] O painel do verificador de links externos não consegue renderizar resultados em [!DNL Adobe Experience Manager] WCM (NPR-37614).
* O editor de fragmento de conteúdo não funciona corretamente quando letras maiúsculas e minúsculas são usadas em nomes de tags ao editar tags no editor (NPR-37601).
* O editor de interface do usuário clássico não mostra a marcação como na exibição de comparação da interface do usuário de toque (NPR-37588).
* O erro 500 intermitente é registrado ao adicionar um fragmento de experiência aos trabalhos de tradução (NPR-37587).
* Os autores podem selecionar e usar a data do seletor de datas mesmo no seletor de datas desativado (NPR-37583).
* [Foundation] Os autores não podem inserir alguns valores decimais no tipo de recurso de campo de número em uma estrutura de diálogo de componente para a interface do usuário de toque (NPR-37059).
* Os caminhos na pasta libs são excluídos na instalação de service packs anteriores (NPR-36815).
* [Comércio] A desativação de uma pasta raiz não altera o status de desativação de produtos secundários em [!DNL Experience Manager Commerce] console; além disso, a contagem de pastas filhas de uma pasta raiz no momento da desativação é exibida incorretamente na interface do usuário (CQ-4338261).
* [Fluxo de trabalho de localização] O conteúdo para personalização de coluna e personalização de marca não está localizado na caixa de diálogo Controle de administração — ao selecionar o ícone sob o ícone de perfil em [!DNL Adobe Experience Manager] caixa de entrada (CQ-4334864).
* [Comunidades] O conteúdo dentro da tabela para membros do grupo não é clicável (CQ-4334404).
* [Oak] O processo de sincronização Cold-Standby não está funcionando e está registrando o erro (CQ-433868).
* [Interface do usuário do Platform Foundation] [!DNL Experience Manager] a página inicial será exibida novamente quando o usuário selecionar a variável [!DNL Adobe Experience Manager] ícone que já está sendo exibido na página inicial (CQ-4317409).

### [!DNL Assets] {#assets-65120}

<!--
The following accessibility enhancements are available in [!DNL Assets]:

* enhancement 1
-->

Os seguintes problemas foram corrigidos em [!DNL Assets]:

* Ao adicionar um ativo ou pasta (contendo `single quote` no nome) no Connected Assets, o caminho de referência falha e resulta como uma exceção (NPR-37712).
* Ao adicionar marca d&#39;água a um ativo, a marca d&#39;água é sempre exibida em preto, independentemente da cor definida pelo usuário (NPR-37720).
* Ao usar o Connected Assets, um usuário não administrador pode procurar um ativo mesmo quando os usuários não administradores são restritos a acessar o repositório DAM (NPR-37644).
* Ao atualizar metadados de ativos usando edição em massa, as alterações aplicadas aos campos suspensos não são salvas e redefinidas aos valores padrão (NPR-37345).
* A exclusão de uma pasta leva muito tempo, o que afeta o desempenho geral (NPR-37107).
* Ao aplicar regras no esquema de metadados, o usuário não pode visualizar o valor completo da lista suspensa `Field Value` e `Field Choices` se o valor for maior que a caixa de texto (CQ-4338074).
* Após a atualização para a versão 6.5.10.0, a página de propriedades do ativo reflete uma mensagem desnecessária de renderização de HTML (CQ-4336994).
* Classificar os ativos em `List View` não funciona efetivamente (CQ-4335298).
* Ao compartilhar ativos usando o link de compartilhamento, os ativos são baixados em pastas separadas (CQ-4335000).
* Ao verificar a [!DNL Experience Manager] `Inbox` , o `Share` e `Out of office` as guias refletem conteúdo não traduzido (CQ-4334858).

* As seguintes correções estão relacionadas aos metadados em cascata nas propriedades do ativo.
   * Uma lista suspensa obrigatória reflete várias mensagens de erro para cada seleção no campo de vários valores (NPR-37859).
   * Somente a última seleção do campo pai é salva para o campo não editável dependente (NPR-37858).
   * A lista suspensa dependente (campo de vários valores) reflete o valor padrão intermitentemente para a lista suspensa pai selecionada (NPR-37791).


### [!DNL Dynamic Media] {#dynamic-media-65120}

Os seguintes problemas foram corrigidos em [!DNL Dynamic Media]:

* Os ativos de uma pasta contendo `renditions` no nome da pasta não são sincronizados no `Dynamic Media` (CQ-4338428).
* Ao criar uma predefinição de imagem em `tiff` , a predefinição é criada, mas o formato muda para `jpeg` (CQ-4335985).
* Ao modificar o `Progressive JPEG Scan` no Editor de predefinições de imagens, o valor suspenso sempre é redefinido como `auto`(CQ-4335971).
* Os metadados de vídeo não estão visíveis para a variável `mxf` vídeos na página de propriedades do ativo (CQ-4335499).
* Ao reprocessar os ativos de vídeo, a publicação do AVS (Adaptive Video Set) e das representações de vídeo é cancelada no servidor de publicação (CQ-4335461).
* As miniaturas de PDF geradas são diferentes da primeira página do PDF real. Algumas partes da imagem estão ausentes na miniatura (CQ-4315554).
* A invalidação de CDN falha com uma resposta de URL incorreta se o `companyName` e `companyRoot` são diferentes (CQ-4339896).

### Fluxos de trabalhos {#workflows-65120}

* A rolagem não funcionará conforme o esperado se você aplicar o filtro aos itens da Caixa de entrada (CQ-433594).


### [!DNL Forms] {#forms-65120}


>[!NOTE]
>
>* O [!DNL Experience Manager Forms] lança os pacotes complementares uma semana após a data programada de lançamento do [!DNL Experience Manager] Service Pack.


<!--

**Adaptive Forms**

* Accessibility – When you set the `Wizard` layout for a panel in an adaptive form, the navigation buttons do not have Aria labels and role (NPR-37613).

* Validations on a date field in an adaptive form does not work, as expected (NPR-37556).

* When the label text for the Checkbox and Radio Button components is long, the text does not fit appropriately (NPR-37294).

* When you apply styling changes to the Thank You message of the AEM Forms Container component, the changes do not replicate in the source adaptive form (NPR-37284).

* Differences in the value of the `Switch` component on the user interface and in the backend (NPR-37268).

* When you use the keyboard keys to navigate to the `Submit` option and press the `Enter` key, you can submit the adaptive form multiple times (CQ-4333993).

* The Remove operation for the File Attachment component does not work, as expected (NPR-37376).

* When a label for a field exceeds 1000 characters in an adaptive form that translates to various languages, the dictionary fails to retrieve the translation of the label (CQ-4329290).

**Document Services**

* An error displays while using the Assembler service (NPR-37606):

  ```TXT
    500 Internal Server Error
  ```

* When the document attachments are passed to the Assembler service, the following exception displays (NPR-37582):

  ```TXT
    com.adobe.livecycle.assembler.client.ProcessingException: ⁪: Failed to execute the DDX
  ```

* Missing closing parenthesis from data after converting a PDF document to a PDF-A/1B PDF document (NPR-37608).

**HTML5 Forms**

* When you install AEM 6.5.10.0, the HTML preview for an XDP form does not work (NPR-37503, CQ-4331926).

* Text overlapping issues while migrating the PDF forms to HTML 5 forms in various languages (NPR-37173).

**Letters**

* When you submit a letter and reopen it in HTML view, the position of text document fragments does not remain the same (NPR-37307).

**Forms Workflow**

* In case of embedded container workflow, you get multiple workflow completion emails even after selecting the `Notify on Complete of Container Workflow` option (NPR-37280).

**Foundation JEE**

* After installing AEM 6.5 Forms Service Pack 9, the CRX repository URLs are no longer available (NPR-37592).

**Issues fixed in AEM Forms 6.5.11.1**

>[!NOTE]
>
>If you have not upgraded to AEM 6.5.11.0 Forms, install the AEM Forms 6.5.11.1 add-on package directly. If you have installed AEM 6.5.11.0 Forms, Adobe recommends to upgrade to AEM 6.5.11.1 Forms.

* Submit actions, Send Email and Invoke an AEM Workflow stop working after installing the Forms 6.5.11.0 add-on package.
* CreatePDF operation stops converting Microsoft Word documents to PDF documents after installing the Forms 6.5.11.0 add-on package.
* (JEE Only) Critical security vulnerabilities (CVE-2021-44228 and CVE-2021-45046) reported for Apache Log4j2.
* (JEE only) Assembler DSC in 6.5.11.0 patch contains incorrect metainfo like specification version and impl version.

-->


Para obter informações sobre atualizações de segurança, consulte [[!DNL Experience Manager] página de boletins de segurança](https://helpx.adobe.com/security/products/experience-manager.html).

## Instalar 6.5.12.0 {#install}

**Requisitos de configuração e mais informações**

* O Experience Manager 6.5.12.0 requer o Experience Manager 6.5. Consulte [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas.
* O download do service pack está disponível no Adobe [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html).
* Em uma implantação com MongoDB e várias instâncias, instale o Experience Manager 6.5.12.0 em uma das instâncias do autor usando o Gerenciador de pacotes.

>[!NOTE]
>
>O Adobe não recomenda remover ou desinstalar o [!DNL Adobe Experience Manager] Pacote 6.5.12.0.

### Instalar o service pack {#install-service-pack}

Para instalar o service pack em um [!DNL Adobe Experience Manager] Na instância 6.5, siga estas etapas:

1. Reinicie a instância antes da instalação se a instância estiver no modo de atualização (quando a instância foi atualizada de uma versão anterior). O Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar, faça um instantâneo ou um novo backup de sua [!DNL Experience Manager] instância.

1. Baixe o service pack de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.12.0.zip).

1. Abra Gerenciador de pacotes e clique em **[!UICONTROL Fazer upload de pacote]** para fazer upload do pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Armazenamento de dados do Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>A caixa de diálogo na interface do usuário do Gerenciador de Pacotes às vezes sai durante a instalação do service pack. O Adobe recomenda que você aguarde a estabilização dos registros de erros antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações foram bem-sucedidas. Normalmente, esse problema ocorre em [!DNL Safari] mas pode ocorrer intermitentemente em qualquer navegador.

**Instalação automática**

Há duas maneiras de instalar automaticamente [!DNL Experience Manager] 6.5.12.0 em uma instância de trabalho:

A. Coloque o pacote em `../crx-quickstart/install` quando o servidor estiver disponível online. O pacote é instalado automaticamente.

B. Use o [API HTTP do Gerenciador de pacotes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Adobe Experience Manager 6.5.12.0 não suporta a instalação do Bootstrap.

**Validar a instalação**

1. A página de informações do produto (`/system/console/productinfo`) exibe a sequência de caracteres da versão atualizada `Adobe Experience Manager (6.5.12.0)` under [!UICONTROL Produtos instalados].

1. Todos os pacotes OSGi são **[!UICONTROL ATIVO]** ou **[!UICONTROL FRAGMENTO]** no console OSGi (Use o console da Web: `/system/console/bundles`).

1. O pacote OSGi `org.apache.jackrabbit.oak-core` é versão 1.22.3 ou posterior (Use o Console da Web: `/system/console/bundles`).

Para conhecer as plataformas certificadas para funcionar com esta versão, consulte o [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

<!-- 

### Install Adobe Experience Manager Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Skip if you are not using Experience Manager Forms. Fixes in Experience Manager Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

1. Ensure that you have installed the Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 includes a new version of [AEM Forms Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). If you are using an older version of AEM Forms Compatibility Package and updating to Experience Manager 6.5.10.0, install the latest version of the package post installation of Forms Add-On Package.

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.

-->

### UberJar {#uber-jar}

O UberJar para Experience Manager 6.5.12.0 está disponível no [Repositório central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.12/).

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e incluir a seguinte dependência no POM do projeto:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.12</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>O UberJar e os outros artefatos relacionados estão disponíveis no Repositório Central Maven em vez do repositório Maven Adobe Public (`repo.adobe.com`). O arquivo UberJar principal é renomeado para `uber-jar-<version>.jar`. Portanto, não há `classifier`, com `apis` como o valor, para a variável `dependency` .

## Recursos obsoletos {#removed-deprecated-features}

Abaixo está uma lista de recursos e funcionalidades marcados como obsoletos [!DNL Experience Manager] 6.5.7.0. Os recursos são marcados como obsoletos inicialmente e posteriormente removidos em uma versão futura. Uma opção alternativa é fornecida.

Revise se você usa um recurso ou um recurso em uma implantação. Além disso, planeje alterar a implementação para usar uma opção alternativa.

| Área | Recurso | Substituição |
|---|---|---|
| Integrações | O **[!UICONTROL Aceitação dos serviços em nuvem AEM]** está obsoleta desde que o [!DNL Experience Manager] e [!DNL Adobe Target] A integração é atualizada no Experience Manager 6.5. A integração oferece suporte à API do Adobe Target Standard. A API usa autenticação via Adobe IMS e [!DNL Adobe I/O] e apoia o papel crescente do Adobe Launch como instrumento [!DNL Experience Manager] páginas para análise e personalização, o assistente de aceitação é funcionalmente irrelevante. | Configurar conexões do sistema, autenticação do Adobe IMS e [!DNL Adobe I/O] integrações por meio das respectivas [!DNL Experience Manager] serviços em nuvem. |
| Conectores | O Conector Adobe JCR para Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 está obsoleto para o Experience Manager 6.5. | N/A |

## Problemas conhecidos {#known-issues}

* Quando você instala o AEM 6.5 Service Pack 11 e tenta baixar o arquivo ZIP de status, o Experience Manager baixa um arquivo corrompido. Baixe e instale [Pacote de índice SEO do AEM Sites](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip) na instância AEM antes de baixar o arquivo ZIP para resolver o problema.

* As [!DNL Microsoft Windows Server 2019] não suporta [!DNL MySQL 5.7] e [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] não suporta instalações turnkey para [!DNL AEM Forms 6.5.10.0].

* Se estiver atualizando seu [!DNL Experience Manager] da versão 6.5 para 6.5.10.0, você pode visualizar `RRD4JReporter` exceções na `error.log` arquivo. Para resolver o problema, reinicie a instância.

* Se você instalar [!DNL Experience Manager] 6.5 Service Pack 10 ou service pack anterior no [!DNL Experience Manager] 6.5, a cópia em tempo de execução do modelo de fluxo de trabalho personalizado dos ativos (criado em `/var/workflow/models/dam`) é excluída.
Para recuperar a cópia de tempo de execução, o Adobe recomenda sincronizar a cópia de tempo de design do modelo de fluxo de trabalho personalizado com a cópia de tempo de execução usando a API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Os usuários podem renomear uma pasta em uma hierarquia em [!DNL Assets] e publicar uma pasta aninhada em [!DNL Brand Portal]. No entanto, o título da pasta não é atualizado em [!DNL Brand Portal] até que a pasta raiz seja republicada.

* Quando um usuário seleciona configurar um campo pela primeira vez em um formulário adaptável, a opção para salvar uma configuração não é exibida no Navegador de propriedades. Selecionar para configurar outro campo do formulário adaptável no mesmo editor resolve o problema.

* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação do Experience Manager 6.5.x.x:
   * &quot;Quando a integração do Adobe Target é configurada no Experience Manager usando a API do Target Standard (autenticação IMS), a exportação dos Fragmentos de experiência para o Target resulta na criação de tipos de ofertas incorretos. Em vez do tipo &quot;Fragmento de experiência&quot;/fonte &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/fonte &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * A validação do lado do servidor do Adaptive Form falha quando funções agregadas, como SUM, MAX e MIN são usadas (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de Banner de compra.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tempo limite aguardando a conclusão da alteração de reg não registrada.

* Ao tentar mover/excluir/publicar Fragmentos de conteúdo ou Sites/Páginas, há um problema quando as referências do Fragmento de conteúdo são buscadas, uma vez que a consulta em segundo plano falha; ou seja, a funcionalidade não funciona.
Para garantir a operação correta, é necessário adicionar as seguintes propriedades ao nó de definição de índice `/oak:index/damAssetLucene` (não é necessário reindexar) :

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## Pacotes de conteúdo e pacotes OSGi incluídos {#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos no [!DNL Experience Manager] 6.5.12.0:

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.12.0](assets/65120_bundles.txt)

* [Lista de pacotes de conteúdo incluídos na Experience Manager 6.5.12.0](assets/65120_packages.txt)

## Sites restritos {#restricted-sites}

Esses sites só estão disponíveis para clientes do . Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)
* Consulte [como entrar em contato com o Suporte ao cliente do Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR)
>* [Inscreva-se em Atualizações de produtos de prioridade da Adobe](https://www.adobe.com/subscription/priority-product-update.html)

