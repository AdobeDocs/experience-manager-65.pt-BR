---
title: Notas de versão do [!DNL Adobe Experience Manager] 6.5
description: Encontre informações sobre versões, novidades, instruções de instalação e uma lista de alterações detalhada para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
source-git-commit: 676472125cf472d42b792fae87dffe263e499014
workflow-type: tm+mt
source-wordcount: '2605'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] Notas de versão do Service Pack 6.5 mais recente {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=WRAZ43&nav=MTVfezk2OTJDQTNFLUI4QTQtNDY2RS05NEVCLUQ5QjcyNEVENkJDNn0 -->

## Informações da versão {#release-information}

| Produto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.16.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versão do Service Pack |
| Data | Quinta-feira, 23 de fevereiro de 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]be/packages/cq650/servicepack/aem-service-pkg-6.5.16.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## O que está incluído em [!DNL Experience Manager] 6.5.16.0 {#what-is-included-in-aem-6516}

[!DNL Experience Manager] O 6.5.16.0 inclui novos recursos, importantes melhorias solicitadas por clientes, correções de erros e melhorias de desempenho, estabilidade e segurança, lançadas desde a disponibilização inicial do 6.5 em abril de 2019. [Instalar este pacote de serviços](#install) em [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Uma melhoria importante no Dynamic Media é a seguinte:

Novo protocolo DASH (Dynamic Adaptive Streaming over HTTP) com suporte lançado para transmissão adaptável de taxa de bits na entrega de vídeo do Dynamic Media (com CMAF [Formato de aplicativo de mídia comum] ativado).

* A transmissão adaptável (DASH/HLS) garante uma melhor experiência de visualização do usuário final para vídeos.
* DASH é o protocolo padrão internacional para transmissão de vídeo adaptável e é amplamente adotado no setor.
* Disponível agora na América do Norte (a ser ativado por meio de tíquete de suporte), em breve na Ásia-Pacífico e Europa-Oriente Médio-África.

Consulte [Habilitar DASH na sua conta](/help/assets/video.md#enable-dash).

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6516}

* Ativos conectados: ao ativar as opções de Recorte inteligente para imagens no DAM remoto, fazer upload de imagens em uma pasta e sincronizar a pasta com os sites locais, a pasta não é aberta na implantação local do Sites. (NPR-39912)
* Ao classificar uma coleção por nome, a exibição em lista não está funcionando corretamente (ASSETS-19401)
* Quando um arquivo de mídia grande (JPEG) é carregado para Coleções, o Experience Manager para de responder. (ASSETS-19387)
* No painel da árvore de conteúdo, o nome do ativo exibido está incorreto, pois o local do ativo não é renderizado adequadamente. (ASSETS-18870)
* Ao compartilhar uma coleção usando um link, os dados no URL não correspondem entre o embaralhamento da exibição de cartão e a exibição de lista. (ASSETS-18758)
* Quando você executa uma omnisearch usando um filtro no tipo de pasta, os resultados da pesquisa são inconsistentes. (ASSETS-18227)
* A variável `dam:size` A propriedade não é atualizada após o write-back XMP, o que resulta no retorno de informações incorretas da `/platform/path/to/asset.jpg;resource=metadata` API. (ASSETS-17631)
* Resolvedor de recursos não fechado em todas as instâncias de Experience Manager. (ASSETS-16904)
* Não é possível criar uma versão para um ativo mesmo se você tiver atribuído a `create` e `modify` permissões. (ASSETS-15956)
* A variável `move` O botão é desativado aleatoriamente ao mover um ativo de um ponto a outro. (ASSETS-14889)
* Os leitores de tela não podem identificar cabeçalhos, pois o texto não é definido nas tags de cabeçalho, mas como o texto geral. (ASSETS-6924)
* O texto alternativo sob a imagem não é obrigatório, mas o texto exibido sob a imagem é repetitivo com um `Type` atributo. (ASSETS-6915)


## [!DNL Assets] - [!DNL Dynamic Media] {#dm-6516}

* O elemento de formulário não contém rótulo. Com leitores de tela como NVDA e JAWS, as informações do rótulo do formulário não são anunciadas corretamente. (CQ-4344078)
* Os menus suspensos não são fechados quando o `Escape` é usada em um teclado. (CQ-4344077)
* O ícone Information (a letra &quot;i&quot;) que aparece para a sugestão de erro em linha após uma entrada inválida ser fornecida não pode ser acessado por teclado. (CQ-4344076)
* `getManifestURI` retorna nulo porque uma propriedade JCR está sendo lida como `toString` em vez de `getString`. (ASSETS-18674)
* O componente de vídeo SmartCrop não está se comportando corretamente. O componente está executando a reprodução em vez da transmissão e as chamadas VTT estão falhando, gerando um erro 404. (ASSETS-18468)
* Selecionar **[!UICONTROL Propriedades]** na página Visualizador de um ativo causa uma exceção de ponteiro nulo. (ASSETS-18420)
* [!DNL Experience Manager] alterações na interface do usuário para transmissão de DASH que inclui o seguinte:
   * Ter um campo CMAF (Common Media Application Format) visível no editor de perfil de vídeo.
   * fazer com que o processo de upload de vídeo envie um sinalizador CMAF.
   * as opções **[!UICONTROL automático]**, **[!UICONTROL hls]**, e **[!UICONTROL traço]** agora estão disponíveis na lista suspensa reprodução, no editor de Predefinições do visualizador **[!UICONTROL Comportamento]** guia.
(ASSETS-17428)
* Na Navegação, ao selecionar **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]** > **[!UICONTROL Criar]** > **[!UICONTROL Conjunto do Carousel]**, o ícone de imagem é sobreposto à sequência de texto &quot;Slide 1&quot;. (ASSETS-18578)
* Os ativos não publicados são publicados novamente. (ASSETS-16428)
* O Experience Manager Author fica inativo devido a um problema de carregamento, solicitando a criação de um alerta sintético. (ASSETS-15937)
* Na página Configurações gerais do Dynamic Media, uma mensagem de erro não traduzida `Failed to fetch data` é exibida. (ASSETS-15617)

## [!DNL Forms] {#forms-6516}

### [!DNL Forms] Principais recursos {#forms-features-6516}

* [Forms adaptável headless](https://experienceleague.corp.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) permita que os desenvolvedores criem, publiquem e gerenciem formulários interativos que possam ser acessados e interagidos por meio de APIs, em vez de uma interface gráfica tradicional.

* [Componentes principais adaptáveis do Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) são um conjunto de 24 componentes de código aberto, compatíveis com BEM, que foram criados com base nos Componentes principais do WCM no Adobe Experience Manager. Esses componentes são de código aberto e fornecem aos desenvolvedores a capacidade de personalizar e estender facilmente esses componentes para atender às necessidades específicas de sua organização. Qualquer pessoa com habilidades existentes para personalizar [Componentes principais do WCM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html?lang=en) O pode personalizar e estilizar facilmente esses componentes.

* O serviço de extensão de Reader no OSGi agora fornece opções separadas para habilitar direitos de uso de importação e exportação em um PDF para importar ou exportar dados no Adobe Acrobat Reader. (NPR-39909)

### [!DNL Forms] Correções {#forms-fixes-6516}

* Ao usar uma etapa Atribuir tarefa** para enviar uma notificação para uma tarefa atribuída, dois emails são enviados em vez de um para o indivíduo atribuído. (NPR-40078)
* Quando um usuário oculta os cabeçalhos da tabela, a largura da coluna definida anteriormente é anulada e todas as colunas mantêm a mesma largura. (NPR-40063)
* Caso altere a senha padrão do usuário administrador de `admin`, enquanto executa a `Prepare Adobe Experience Manager Server For DSC deployment` falha ao verificar o service pack do AEM Forms JEE. (NPR-40062), (NPR-39387)
* As APIs OutputService e AssemblerService falham ao converter o formulário de PDF para PDF/A. (NPR-39990)
* O AssemblerService não pode converter PDF em PDF/A. Quando um usuário converte PDF em PDF/A, ocorre o seguinte erro: `PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Summary" ignoreUnusedResources="true" allowCertificationSignatures="true"> <Violation count="6" key="PDFA_CS_001_NOT_DEVICE_INDEPENDENT" description="ColorSpace is not device independent`. (NPR-39956)
* Quando a validação do lado do servidor falha para uma chamada da API GuideSubmitServlet, os erros não são retornados na resposta enviada ao cliente. (NPR-39925)
* Depois de atualizar para o AEM 6.5.15.0 Service Pack no servidor Windows, o usuário encontra várias mensagens de erro e o serviço de email não está funcionando.(NPR-39919)
* Ao atualizar para o AEM 6.5.14.0 e usar o serviço importData para mesclar PDF com XML, ocorre o seguinte erro: `Caused by: java.lang.NoSuchMethodError: com.adobe.xfa.form.FormModel.isXFABarcode(Lcom/adobe/xfa/Node;)Ljava/lang/Boolean`.(NPR-39807)
* Quando o usuário instala o **Escritório de segurança de documentos** , ocorrem os seguintes problemas:
   * O Microsoft® Excel trava frequentemente.
   * Ao abrir um documento protegido, a variável **Escritório de segurança de documentos** extensão não foi detectada como instalada em um computador. Instrui o usuário a baixar e instalar a extensão de segurança. (NPR-39768)
* Depois que um usuário atualiza para o AEM 6.5.15.0 Service Pack, a conversão de PostScript em Pdf não funciona. (NPR-39765), (NPR-39764)
* Quando um usuário tenta abrir a tela de tour após abrir um Formulário adaptável, ocorre uma falha com uma exceção de NullPointer:`[172.17.0.1[1662032923933]GET/libs/fd/af/content/editors/form/tour/content.htmlHTTP/1.1]com.day.cq.wcm.core.impl.WCMDebugFilterException:org.apache.sling.api.scripting.ScriptEvaluationException:”` (NPR-39654)
* No Windows, quando o usuário ativa as configurações de preto de alto contraste, o conteúdo do HTML5 Forms fica indefinido quando renderizado como uma visualização de HTML no navegador. (NPR-39018)

## Integrações {#integrations-6516}

* Remova o Search &amp; Promote de Adobe e a dependência do Experience Manager 6.5. O Adobe Search &amp; Promote chegou ao fim do serviço em setembro de 2022. Consulte [Anúncio de fim de serviço do Adobe Search &amp; Promote](https://experienceleague.adobe.com/docs/discontinued/using/search-promote.html?lang=en). (NPR-39706)

## [!DNL Sites] {#sites-6516}

* Atual `cq-wcm-core` A versão artesanal não tem o POM. (SITES-10983)
* A ação de visualização de implantação não deve listar a página a ser criada. (SITES-10355, CQ-4266213)
* A implantação após a desanexação do MSM recria a página desanexada. (SITES-9841)
* A criação de uma inicialização está atingindo o tempo limite; o usuário deve aguardar muitos minutos em uma tela de carregamento antes que a solicitação expire. (SITES-9051)
* A interface do usuário da Página de implantação está exibindo caminhos de página principais inexistentes. Você pode implantar a página com uma mensagem de sucesso, mas a página secundária não é implantada porque a página principal nunca é implantada. (SITES-8621)

### [!DNL Sites] - Componentes principais {#sites-core-components-6516}

* Centralize o processamento de links nas páginas de e-mail para que as personalizações de modelo não sejam mais necessárias. (SITES-9002)

### [!DNL Sites] - Interface do usuário do administrador {#sites-adminui-6516}

* A exportação de arquivos CSV não está exportando todas as páginas na página selecionada. (SITES-9390)

### [!DNL Sites] - [!DNL Content Fragments] {#sites-contentfragments-6516}

* Não foi possível imprimir o JSON de um fragmento de conteúdo. O motivo é que a consulta do GraphQL não pode ser gerada ao abrir a página Visualizar do fragmento de conteúdo. (SITES-8619)
* Ao reabrir o Editor de modelos de fragmentos de conteúdo, todas as **[!UICONTROL Data e hora]** Os campos são padronizados para o tipo Data e hora. (SITES-8401)

### [!DNL Sites] - [!DNL Experience Fragments] {#sites-experiencefragments-6516}

* Você não pode mover um fragmento de experiência para outra pasta, mesmo se o modelo estiver listado em modelos permitidos. (SITES-8601)
* (SITES-7989)


### [!DNL Sites] - Editor de página {#sites-pageeditor-6516}

* Atualizar dependências para o aprimoramento do resolvedor de recursos feito no SITES-8464 no qual a renderização da página no modo Criação criou um número alto de `TemplatedResourceImpl` objetos. (SITES-9350)


## Sling {#sling-6516}

* Experience Manager está bloqueado na inicialização. (NPR-39832)
* Quando muitos caminhos personalizados estão presentes no armazenamento da versão do Experience Manager, o Experience Manager não é iniciado. (NPR-38955)


## Projetos de tradução {#translation-6516}

* Entrada `MicrosoftTranslationServiceImpl`, o parâmetro da sequência de consulta `Category` está incorreto. (NPR-39828)
* Criar um projeto de tradução exibe o erro *O recurso de página principal não existe*; o projeto de tradução não é criado. (NPR-39762)
* Não é possível definir uma data de vencimento em um projeto de tradução que usa um conector de tradução humana. (NPR-39593)

## Interface do usuário {#ui-6516}

* Ao alterar para uma resolução menor, o DatePicker não é exibido e a seleção AM/PM não é exibida ou alterada visivelmente. (NPR-39948)
* Quando minify js (minimização do JavaScript) é usada, ela não processa a minificação devido a um erro de análise. (NPR-39650)
* Campo de tag (`/libs/cq/gui/components/coral/common/form/tagfield`) entra em conflito com a linha do tempo. (CQ-4350751)


## WCM {#wcm-6516}

* A ação de visualização de implantação não deve listar a página a ser criada. (CQ-4266213, SITES-10355)

## Fluxo de trabalho {#workflow-6516}

* Exclusão manual do modelo de fluxo de trabalho editável do `/conf` deixa uma instância de modelo de tempo de execução persistente sem um modelo editável. (CQ-4349365)


## Instalar [!DNL Experience Manager] 6.5.16.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] O 6.5.16.0 exige [!DNL Experience Manager] 6.5. Ver [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas. <!-- UPDATE FOR EACH NEW RELEASE -->
* O download do pacote de serviços está disponível no Adobe [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html).
* Em uma implantação com MongoDB e várias instâncias, instale [!DNL Experience Manager] 6.5.16.0 em uma das instâncias do Autor usando o Gerenciador de pacotes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> O Adobe não recomenda que você remova ou desinstale o [!DNL Experience Manager] 6.5.16.0 pacote. Dessa forma, antes de instalar o pacote, você deve criar um backup do `crx-repository` caso precise revertê-la. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Instalar o pacote de serviços em [!DNL Experience Manager] 6.5 {#install-service-pack}

1. Reinicie a instância antes da instalação se ela estiver no modo de atualização (quando a instância tiver sido atualizada de uma versão anterior). O Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar o, faça um instantâneo ou um novo backup de seu [!DNL Experience Manager] instância.

1. Baixe o pacote de serviços de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra o Gerenciador de pacotes e selecione **[!UICONTROL Fazer upload do pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Armazenamento de dados Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>Às vezes, um diálogo na interface do usuário do Gerenciador de pacotes é fechado durante a instalação do pacote de serviços. A Adobe recomenda que você aguarde a estabilização dos logs de erro antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações serão bem-sucedidas. Normalmente, esse problema ocorre em [!DNL Safari] navegador, mas pode ocorrer intermitentemente em qualquer navegador.

**Instalação automática**

Há dois métodos diferentes que você pode usar para instalar automaticamente o [!DNL Experience Manager] 6.5.16.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote em `../crx-quickstart/install` pasta quando o servidor estiver disponível online. O pacote é instalado automaticamente.
* Use o [API HTTP do Gerenciador de pacotes](/help/sites-administering/package-manager.md#package-share). Uso `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Experience Manager 6.5.16.0 não suporta a instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar a instalação**

Para conhecer as plataformas certificadas para trabalhar com esta versão, consulte a [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a string da versão atualizada `Adobe Experience Manager (6.5.16.0)` em [!UICONTROL Produtos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos os pacotes OSGi são **[!UICONTROL ATIVO]** ou **[!UICONTROL FRAGMENTO]** no console OSGi (Use o console da Web: `/system/console/bundles`).

1. O pacote OSGi `org.apache.jackrabbit.oak-core` O é versão 1.22.14 ou posterior (Use o Console da Web: `/system/console/bundles`). <!-- NPR-39939 for 6.5.16.0 --> <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Instalar o Service Pack do [!DNL Experience Manager] Forms {#install-aem-forms-add-on-package}

Para obter instruções sobre como instalar o pacote de serviços no AEM Forms, consulte [Instruções de instalação do AEM Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### UberJar {#uber-jar}

O UberJar para [!DNL Experience Manager] O 6.5.16.0 está disponível na [Repositório central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>No Experience Manager 6.5.16.0, a versão do UberJar (6.5.15.0) permanece a mesma da versão anterior.


Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e inclua a seguinte dependência no POM do projeto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.15</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>O UberJar e outros artefatos relacionados estão disponíveis no Repositório central Maven em vez do repositório Maven público do Adobe (`repo.adobe.com`). O arquivo UberJar principal é renomeado para `uber-jar-<version>.jar`. Então, não há `classifier`, com `apis` como o valor, para o `dependency` tag.

## Recursos obsoletos {#removed-deprecated-features}

Veja abaixo uma lista dos recursos e funcionalidades marcados como obsoletos em [!DNL Experience Manager] 6.5.7.0. Os recursos são marcados como obsoletos inicialmente e removidos posteriormente em uma versão futura. Uma opção alternativa é fornecida.

Revise se se você usa um recurso ou uma funcionalidade em uma implantação. Além disso, planeje alterar a implementação para usar uma opção alternativa.

| Área | Recurso | Substituição |
|---|---|---|
| Integrações | A variável **[!UICONTROL Aceitação dos serviços em nuvem AEM]** está obsoleta desde que a variável [!DNL Experience Manager] e [!DNL Adobe Target] a integração é atualizada em [!DNL Experience Manager] 6.5. A integração é compatível com a API do Adobe Target Standard. A API usa autenticação por meio do Adobe IMS e [!DNL Adobe I/O Runtime]. Apoia o crescente papel do Adobe Launch para instrumentar [!DNL Experience Manager] para o analytics e a personalização, o assistente de aceitação é funcionalmente irrelevante. | Configurar conexões do sistema, autenticação do Adobe IMS e [!DNL Adobe I/O Runtime] integrações por meio das respectivas [!DNL Experience Manager] serviços em nuvem. |
| Conectores | O conector JCR do Adobe para Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 está obsoleto para [!DNL Experience Manager] 6.5. | N/A |

## Problemas conhecidos {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* [Fragmento de conteúdo AEM com pacote de índice GraphQL 1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
Esse pacote é necessário para clientes que usam o GraphQL; isso permite que eles adicionem a definição de índice necessária com base nos recursos que realmente usam.

* Atualize suas consultas do GraphQL que podem ter usado um nome de API personalizado para seu modelo de conteúdo para usar o nome padrão do modelo de conteúdo.

* Como [!DNL Microsoft®® Windows Server 2019] não suporta [!DNL MySQL 5.7] e [!DNL JBoss®® EAP 7.1], [!DNL Microsoft®® Windows Server 2019] O não oferece suporte a instalações por chave na mão para o [!DNL AEM Forms 6.5.10.0].

* Se você atualizar seu [!DNL Experience Manager] 6.5.0 - 6.5.4 para o pacote de serviços mais recente no Java™ 11, você verá `RRD4JReporter` exceções na `error.log` arquivo. Para interromper as exceções, reinicie a instância do [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Os usuários podem renomear uma pasta em uma hierarquia em [!DNL Assets] e publicar uma pasta aninhada no [!DNL Brand Portal]. No entanto, o título da pasta não é atualizado no [!DNL Brand Portal] até que a pasta raiz seja republicada.

* Quando um usuário opta por configurar um campo pela primeira vez em um formulário adaptável, a opção para salvar uma configuração não é exibida no Navegador de propriedades. Selecionar para configurar algum outro campo do formulário adaptável no mesmo editor resolve o problema.

* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação do [!DNL Experience Manager] 6.5.x.x:
   * &quot;Quando a integração do Adobe Target é configurada no [!DNL Experience Manager] usar a API do Target Standard (autenticação IMS) e, em seguida, exportar os Fragmentos de experiência para o Target resulta na criação de tipos de oferta errados. Em vez do tipo &quot;Fragmento de experiência&quot;/origem &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/origem &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: nenhuma janela de manutenção encontrada no granite/operations/maintenance.
   * A validação do lado do servidor do Formulário adaptável falha quando funções agregadas como SUM, MAX e MIN são usadas (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Nenhuma janela de manutenção encontrada no granite/operations/maintenance.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de banner de compra.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tempo limite atingido ao aguardar a conclusão não registrada da alteração de registro.

* Ao tentar mover/excluir/publicar fragmentos de conteúdo ou sites/páginas, há um problema quando as referências de fragmento de conteúdo são buscadas, já que a consulta em segundo plano falha; ou seja, a funcionalidade não funciona.
Para garantir a operação correta, você deve adicionar as seguintes propriedades ao nó de definição de índice `/oak:index/damAssetLucene` (nenhuma reindexação é necessária):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

* No AEM Forms, o protocolo POP3 não funciona com endpoints de email do Microsoft® Office 365.
* Na plataforma JBoss® 7.1.4, quando o usuário instalar o pacote de serviços AEM 6.5.16.0, `adobe-livecycle-jboss.ear` falha na implantação.

## Pacotes OSGi e pacotes de conteúdo incluídos {#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos em [!DNL Experience Manager] 6.5.16.0 <!-- UPDATE FOR EACH NEW RELEASE -->

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.16.0](/help/release-notes/assets/65160_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de pacotes de conteúdo incluídos no Experience Manager 6.5.16.0](/help/release-notes/assets/65160_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites restritos {#restricted-sites}

Esses sites só estão disponíveis para clientes do. Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Entre em contato com o Suporte ao cliente do Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação do 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR)
>* [Inscreva-se em Atualizações de produtos de prioridade da Adobe](https://www.adobe.com/subscription/priority-product-update.html)

