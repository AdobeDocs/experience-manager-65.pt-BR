---
title: Notas de versão para [!DNL Adobe Experience Manager] 6,5
description: Encontre informações sobre a versão, novidades, instruções de instalação e uma lista detalhada de alterações para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
source-git-commit: 3430897fc98aecbcf6cc7bf6bdc9b3df24e92366
workflow-type: tm+mt
source-wordcount: '2986'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5 Notas de versão mais recentes do Service Pack {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/Documents/issue_tracker_sp_cfp_updates.xlsx?d=w3ea81ae4e6054153b132f2698c86f84e&csf=1&web=1&e=WRAZ43&nav=MTVfezk2OTJDQTNFLUI4QTQtNDY2RS05NEVCLUQ5QjcyNEVENkJDNn0 -->

## Informações da versão {#release-information}

| Produto | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.16.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| Tipo | Versão do Service Pack |
| Data | quinta-feira, 23 de fevereiro de 2023 <!-- UPDATE FOR EACH NEW RELEASE --> |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]be/packages/cq650/servicepack/aem-service-pkg-6.5.16.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## O que está incluído em [!DNL Experience Manager] 6.5.16.0 {#what-is-included-in-aem-6516}

[!DNL Experience Manager] O 6.5.16.0 inclui novos recursos, principais melhorias solicitadas pelo cliente, correções de bugs e melhorias de desempenho, estabilidade e segurança, lançadas desde a disponibilização inicial do 6.5 em abril de 2019. [Instalar este service pack](#install) on [!DNL Experience Manager] 6.5. <!-- UPDATE FOR EACH NEW RELEASE -->

<!-- Some of the key features and improvements are the following:

* _REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

Um aprimoramento importante no Dynamic Media é o seguinte:

Novo suporte de protocolo DASH (Dynamic Adaptive Streaming over HTTP) lançado para o streaming adaptável de taxa de bits na entrega de vídeo do Dynamic Media (com CMAF [Formato de aplicativo de mídia comum] ativado).

* O streaming adaptativo (DASH/HLS) garante uma melhor experiência de visualização do usuário final para vídeos.
* DASH é o protocolo padrão internacional para transmissão de vídeo adaptável e é amplamente adotado no setor.
* Disponível agora na Ásia-Pacífico e na América do Norte (para ser ativado por meio de um tíquete de apoio); em breve na Europa-Oriente Médio-África.

Consulte [Habilitar o DASH em sua conta](/help/assets/video.md#enable-dash).

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## [!DNL Assets] {#assets-6516}

* Ativos conectados: Quando você ativa as opções de Recorte inteligente para imagens no DAM remoto, carrega imagens em uma pasta e sincroniza a pasta em sites locais, a pasta não abre na implantação local do Sites. (NPR-39912)
* Ao classificar uma coleção por nome, a exibição de lista não está funcionando adequadamente (ASSETS-19401)
* Quando um arquivo de mídia grande (JPEG) é carregado nas Coleções, o Experience Manager para de responder. (ATIVO-19387)
* No painel da árvore de conteúdo, o nome do ativo exibido está incorreto, pois o local do ativo não é renderizado adequadamente. (ATIVO-18870)
* Ao compartilhar uma coleção usando um link, os dados no URL não correspondem entre a visualização de cartão e a exibição de lista. (ATIVO-18758)
* Quando você executa uma pesquisa omnisearch usando um filtro no tipo de pasta, os resultados de pesquisa são inconsistentes. (ATIVO-18227)
* O `dam:size` A propriedade não é atualizada após XMP write-back, o que resulta em informações incorretas serem retornadas do `/platform/path/to/asset.jpg;resource=metadata` API. (ATIVO-17631)
* Resolvedor de recursos não fechado em todas as instâncias do Experience Manager. (ATIVO-16904)
* Não é possível criar uma versão para um ativo mesmo que você tenha atribuído a variável `create` e `modify` permissões. (ATIVO-15956)
* O `move` é desativado aleatoriamente ao mover um ativo de um ponto para outro. (ATIVO-14889)
* Os leitores de tela não conseguem identificar cabeçalhos, pois o texto não é definido dentro das tags de cabeçalho, mas como o texto geral. (ATIVO-6924)
* O texto alternativo sob a imagem não é obrigatório, mas o texto exibido sob a imagem é repetitivo com uma `Type` atributo. (ATIVO-6915)


## [!DNL Assets] - [!DNL Dynamic Media] {#dm-6516}

* O elemento de formulário não contém rótulo. Com leitores de tela como NVDA e JAWS, as informações de rótulo do Formulário não são anunciadas corretamente. (CQ-4344078)
* Os detalhamentos não estão sendo fechados quando a variável `Escape` é usada em um teclado. (CQ-4344077)
* O ícone Informações (a letra &quot;i&quot;) que aparece para a sugestão de erro em linha depois que uma entrada inválida é fornecida, não é acessível com teclado. (CQ-4344076)
* `getManifestURI` retorna null devido a uma propriedade JCR estar sendo lida como `toString` em vez de `getString`. (ATIVO-18674)
* O componente de vídeo SmartCrop não está funcionando corretamente. O componente está realizando a reprodução em vez de streaming, e as chamadas VTT estão falhando, o que causa um erro 404. (ATIVO-18468)
* Selecionar **[!UICONTROL Propriedades]** na página Visualizador de um ativo causa uma exceção de ponteiro nulo. (ATIVO-18420)
* [!DNL Experience Manager] alterações na interface do usuário para transmissão DASH, incluindo o seguinte:
   * ter um campo CMAF visível (Common Media Application Format) no editor de Perfil de vídeo.
   * fazer com que o processo de upload de vídeo envie um sinalizador CMAF.
   * as opções **[!UICONTROL auto]**, **[!UICONTROL hls]** e **[!UICONTROL traço]** estão disponíveis na lista suspensa reprodução do editor de predefinição do visualizador **[!UICONTROL Comportamento]** guia .
(ATIVO-17428)
* Em Navegação, ao selecionar **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]** > **[!UICONTROL Criar]** > **[!UICONTROL Conjunto de carrossel]**, o ícone de imagem é sobreposto por uma string de texto &quot;Slide 1&quot;. (ATIVO-18578)
* Os ativos não publicados são publicados novamente. (ATIVO-16428)
* O Experience Manager Author fica inativo devido a um problema de carregamento, solicitando a criação de um alerta sintético. (ATIVO-15937)
* Na página Configurações gerais do Dynamic Media , uma mensagem de erro não traduzida `Failed to fetch data` é exibido. (ATIVO-15617)

## [!DNL Forms] {#forms-6516}

### [!DNL Forms] Principais recursos {#forms-features-6516}

* [Forms adaptável headless](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) permitir que seus desenvolvedores criem, publiquem e gerenciem formulários interativos que podem ser acessados e interagidos com por meio de APIs, em vez de por meio de uma interface gráfica tradicional.

* [Componentes principais adaptáveis do Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) são um conjunto de 24 componentes de código aberto compatíveis com BEM, criados na base dos Componentes principais do WCM Adobe Experience Manager. Esses componentes são de código aberto e fornecem aos desenvolvedores a capacidade de personalizar e estender facilmente esses componentes para atender às necessidades específicas de sua organização. Qualquer pessoa com habilidades existentes para personalizar [Componentes principais do WCM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html?lang=en) O pode personalizar e estilizar facilmente esses componentes.

* O serviço Extensão do Reader no OSGi agora fornece opções separadas para habilitar direitos de uso de importação e exportação em um PDF para importar ou exportar dados no Adobe Acrobat Reader. (NPR-39909)

### [!DNL Forms] Correções {#forms-fixes-6516}

* Ao usar um **Atribuir tarefa** para enviar uma notificação para uma tarefa atribuída, dois emails são enviados em vez de um para o indivíduo atribuído. (NPR-40078)
* Quando um usuário oculta os cabeçalhos da tabela, a largura da coluna definida anteriormente fica indefinida e todas as colunas retêm a mesma largura. (NPR-40063)
* Caso você altere a senha padrão do usuário administrador de `admin`ao executar a `Prepare Adobe Experience Manager Server For DSC deployment` verifique se o service pack do AEM Forms JEE falha. (NPR-40062), (NPR-39387)
* As APIs OutputService e AssemblerService não convertem o Formulário PDF para PDF/A. (NPR-39990)
* O AssemblerService não pode converter PDF em PDF/A. Quando um usuário converte o PDF para PDF/A, ocorre o seguinte erro: `PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Summary" ignoreUnusedResources="true" allowCertificationSignatures="true"> <Violation count="6" key="PDFA_CS_001_NOT_DEVICE_INDEPENDENT" description="ColorSpace is not device independent`. (NPR-39956)
* Quando a validação do lado do servidor falha para uma chamada à API GuideSubmitServlet , os erros não são retornados na resposta enviada ao cliente. (NPR-39925)
* Após a atualização para o AEM 6.5.15.0 Service Pack no servidor Windows, o usuário encontra várias mensagens de erro e o serviço de email não está funcionando.(NPR-39919)
* Quando você atualiza para o AEM 6.5.14.0 e usa o serviço importData para mesclar PDF com XML, ocorre o seguinte erro: `Caused by: java.lang.NoSuchMethodError: com.adobe.xfa.form.FormModel.isXFABarcode(Lcom/adobe/xfa/Node;)Ljava/lang/Boolean`.(NPR-39807)
* Quando o usuário instala **Serviço de segurança de documentos** , ocorrem os seguintes problemas:
   * O Microsoft® Excel falha com frequência.
   * Ao abrir um documento protegido, a variável **Serviço de segurança de documentos** A extensão não é detectada como instalada em uma máquina. Instrui o usuário a baixar e instalar a extensão de segurança. (NPR-39768)
* Depois que um usuário atualiza para o AEM 6.5.15.0 Service Pack, a conversão de PostScript para Pdf não está funcionando. (NPR-39765), (NPR-39764)
* Quando o usuário tenta abrir a tela turnê após abrir um Formulário adaptável, ele falha com uma exceção de NullPointer:`[172.17.0.1[1662032923933]GET/libs/fd/af/content/editors/form/tour/content.htmlHTTP/1.1]com.day.cq.wcm.core.impl.WCMDebugFilterException:org.apache.sling.api.scripting.ScriptEvaluationException:"` (NPR-39654)
* No Windows, quando o usuário ativa configurações em preto de alto contraste, o conteúdo do HTML5 Forms fica indefinido quando renderizado como uma visualização de HTML no navegador. (NPR-39018)
* Quando o usuário tenta adicionar metadados, o botão Salvar fica inoperante para os componentes Rascunho e Submissão .(CQ-4349601)
* Após a atualização para o AEM 6.5.15.0 Service Pack, o redirecionamento de URLs relativos não funciona mais no Visual Editor. (NPR-39947)
* Quando um usuário atualiza para o AEM 6.5.15.0 Service Pack, o redirecionamento para não funcionar com o Internet Explorer. (CQ-4351745)
* Depois que um usuário atualiza para o AEM 6.5.15.0 Service Pack, a tag do cabeçalho do HTML não é reconhecida. O código de HTML para a tag de cabeçalho é exibido como texto no formulário de HTML. (NPR-39915)
* Quando o usuário tenta enviar um formulário adaptável, ocorre um erro de tipecast: `ERROR [10.207.64.167 [1668589530607] POST /app/LS4/content/forms/af/revalidate/jcr:content/guideContainer.af.submit.jsp HTTP/1.1]`(NPR-39809)
* Quando um usuário visualiza um Documento de registro usando o **Enviar Email** enviar ação, ela não é exibida corretamente. O modelo de email é incorporado na pré-visualização do Documento de registro. (CQ-4352155)
* Quando um usuário visualiza um Formulário adaptável como HTML no navegador Microsoft Edge com o modo de compatibilidade do IE, ele não é exibido corretamente.(CQ-4352216)
* O dicionário precisa incluir novas localidades com caracteres especiais, como sublinhados ou hifens, para permitir a tradução. (NPR-40088)

Após instalar o AEM 6.5.16.0 Forms Add-on Service Pack, os clientes enfrentavam os problemas listados abaixo. Assim, uma versão atualizada do [AEM 6.5.16.0 Pacote de serviço complementar do Forms - 6.0.914](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) for liberado. O Adobe recomenda usar o service pack atualizado:
* Quando um usuário tenta criar um formulário adaptável com um usuário no grupo forms-users , a opção para selecionar qualquer modelo não está presente e o erro semelhante ao seguinte ocorre: erro interno do servidor: java.lang.NullPointerException em com.adobe.aem.formsndocuments.servlet.ThemeClientLibraryDataSourceServlet.lambda$getThemeClientLibCategoryList$3(ThemeClientLibraryDataSourceServlet.java:76) em java.base/java.util.stream.ReferencePipeline$2 1.accept(ReferencePipeline.java:176) at java.base/java.util.Iterator.foreachRemaining(Iterator.java:133) (FORMS-7629)
* As alterações feitas nas regras do editor de códigos não estão sendo salvas.(FORMS-7532)

## Integrações {#integrations-6516}

* Remova o código do Search &amp; Promote Adobe e a dependência do Experience Manager 6.5. O Search &amp; Promote Adobe chegou ao fim do serviço em setembro de 2022. Consulte [Anúncio de fim de serviço do Adobe Search &amp; Promote](https://experienceleague.adobe.com/docs/discontinued/using/search-promote.html?lang=en). (NPR-39706)

## [!DNL Sites] {#sites-6516}

* Atual `cq-wcm-core` A versão de fábrica não tem o POM. (SITES-10983)
* A ação de visualização de implementação não deve listar a página a ser criada. (SITES-10355, CQ-4266213)
* Implantação após a desconexão do MSM recria a página desanexada. (SITES-9841)
* A criação de um lançamento está atingindo o tempo limite; O usuário deve aguardar muitos minutos em uma tela de carregamento antes que a solicitação atinja o tempo limite. (SITES-9051)
* A interface do usuário da Página de implantação está exibindo caminhos de página pai inexistentes. Você pode implantar a página com uma mensagem de sucesso, mas a página secundária não é distribuída porque a página principal nunca é distribuída em primeiro lugar. (SITES-8621)

### [!DNL Sites] - Componentes principais {#sites-core-components-6516}

* Centralize o processamento de link nas páginas de email para que as personalizações de modelo não sejam mais necessárias. (SITES-9002)

### [!DNL Sites] - Interface do usuário administrador {#sites-adminui-6516}

* A exportação de arquivos CSV não está exportando todas as páginas na página selecionada. (SITES-9390)

### [!DNL Sites] - [!DNL Content Fragments] {#sites-contentfragments-6516}

* Não é possível imprimir o JSON de um fragmento de conteúdo. O motivo é que a consulta GraphQL não pode ser gerada quando você abre a página Visualização do fragmento de conteúdo. (SITES-8619)
* Ao reabrir o Editor do modelo de fragmento de conteúdo, todas as **[!UICONTROL Data e hora]** os campos são padronizados para o tipo Data e hora . (SITES-8401)

### [!DNL Sites] - [!DNL Experience Fragments] {#sites-experiencefragments-6516}

* Não é possível mover um Fragmento de experiência para outra pasta mesmo se o modelo estiver listado em modelos permitidos. (SITES-8601)
* (SITES-7989)


### [!DNL Sites] - Editor de página {#sites-pageeditor-6516}

* Atualize as dependências para o aprimoramento do resolvedor de recursos feito no SITES-8464, em que a renderização de página no modo Criação criou um alto número de `TemplatedResourceImpl` objetos. (SITES-9350)


## Sling {#sling-6516}

* Experience Manager está bloqueado na inicialização. (NPR-39832)
* Quando caminhos personalizados estão presentes em muitas versões de armazenamento do Experience Manager, o Experience Manager falha ao iniciar. (NPR-38955)


## Projetos de tradução {#translation-6516}

* Em `MicrosoftTranslationServiceImpl`, o parâmetro da string de consulta `Category` está incorreto. (NPR-39828)
* A criação de um projeto de tradução exibe o erro *O recurso de página principal não existe*; o projeto de tradução não é criado. (NPR-39762)
* Não é possível definir uma data de vencimento em um projeto de tradução que use um conector de tradução humano. (NPR-39593)

## Interface do usuário {#ui-6516}

* Ao alterar para uma resolução menor, o DatePicker não é exibido e a seleção de AM/PM não é exibida ou alterada visivelmente. (NPR-39948)
* Quando minificar js (minimização do JavaScript) é usado, ele não processa a minificação devido a um erro de análise. (NPR-39650)
* Campo de tag (`/libs/cq/gui/components/coral/common/form/tagfield`) está em conflito com a linha do tempo. (CQ-4350751)


## WCM {#wcm-6516}

* A ação de visualização de implementação não deve listar a página a ser criada. (CQ-4266213, SITES-10355)

## Fluxo de trabalho {#workflow-6516}

* Excluindo manualmente o modelo de fluxo de trabalho editável de `/conf` deixa uma instância de modelo de tempo de execução remanescente sem um modelo editável. (CQ-4349365)


## Instalar [!DNL Experience Manager] 6.5.16.0 {#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.16.0 exige [!DNL Experience Manager] 6.5. Ver [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas. <!-- UPDATE FOR EACH NEW RELEASE -->
* O download do service pack está disponível no Adobe [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html).
* Em uma implantação com MongoDB e várias instâncias, instale [!DNL Experience Manager] 6.5.16.0 em uma das instâncias do autor usando o Gerenciador de pacotes.<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> O Adobe não recomenda remover ou desinstalar o [!DNL Experience Manager] Pacote 6.5.16.0. Assim, antes de instalar o pacote, você deve criar um backup do `crx-repository` caso precise revertê-lo. <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### Instalar o service pack em [!DNL Experience Manager] 6,5 {#install-service-pack}

1. Reinicie a instância antes da instalação se a instância estiver no modo de atualização (quando a instância foi atualizada de uma versão anterior). O Adobe recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar, faça um instantâneo ou um novo backup de sua [!DNL Experience Manager] instância.

1. Baixe o service pack de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. Abra o Gerenciador de Pacotes e selecione **[!UICONTROL Fazer upload do pacote]** para carregar o pacote. Para saber mais, consulte [Gerenciador de pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e selecione **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Armazenamento de dados do Amazon S3](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>A caixa de diálogo na interface do usuário do Gerenciador de Pacotes às vezes sai durante a instalação do service pack. O Adobe recomenda que você aguarde a estabilização dos registros de erros antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações foram bem-sucedidas. Normalmente, esse problema ocorre em [!DNL Safari] mas pode ocorrer intermitentemente em qualquer navegador.

**Instalação automática**

Há dois métodos diferentes que podem ser usados para instalar automaticamente [!DNL Experience Manager] 6.5.16.0<!-- UPDATE FOR EACH NEW RELEASE -->

* Coloque o pacote em `../crx-quickstart/install` quando o servidor estiver disponível online. O pacote é instalado automaticamente.
* Use o [API HTTP do Gerenciador de pacotes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Experience Manager 6.5.16.0 não suporta a instalação do Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validar a instalação**

Para conhecer as plataformas certificadas para funcionar com esta versão, consulte o [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

1. A página de informações do produto (`/system/console/productinfo`) exibe a sequência de caracteres da versão atualizada `Adobe Experience Manager (6.5.16.0)` under [!UICONTROL Produtos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Todos os pacotes OSGi são **[!UICONTROL ATIVO]** ou **[!UICONTROL FRAGMENTO]** no console OSGi (Use o console da Web: `/system/console/bundles`).

1. O pacote OSGi `org.apache.jackrabbit.oak-core` é a versão 1.22.14 ou posterior (Use o Console da Web: `/system/console/bundles`). <!-- NPR-39939 for 6.5.16.0 --> <!-- NPR-39436 for 6.5.15.0 --> <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### Instalar o Service Pack para [!DNL Experience Manager] Forms {#install-aem-forms-add-on-package}

Para obter instruções sobre como instalar o service pack no AEM Forms, consulte [Instruções de instalação do AEM Forms Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

### Instalar o pacote de índice do GraphQL para fragmentos de conteúdo do Experience Manager {#install-aem-graphql-index-add-on-package}

Os clientes que usam o GraphQL devem instalar o [AEM Fragmento de conteúdo com o Pacote de índice GraphQL 1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip).

Isso permite adicionar a definição de índice necessária com base nos recursos que eles realmente usam.

A falha na instalação deste pacote pode resultar em consultas GraphQL lentas ou com falha.

>[!NOTE]
>
>Este pacote só deve ser instalado uma vez por instância; ele não precisa ser reinstalado com cada Service Pack.

### UberJar {#uber-jar}

O UberJar para [!DNL Experience Manager] 6.5.16.0 está disponível no [Repositório central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.15/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

>[!NOTE]
>
>No Experience Manager 6.5.16.0, a versão UberJar (6.5.15.0) permanece a mesma da versão anterior.


Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e incluir a seguinte dependência no POM do projeto: <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

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
>O UberJar e os outros artefatos relacionados estão disponíveis no Repositório Central Maven em vez do repositório Maven Adobe Public (`repo.adobe.com`). O arquivo UberJar principal é renomeado para `uber-jar-<version>.jar`. Portanto, não há `classifier`, com `apis` como o valor, para a variável `dependency` .

## Recursos obsoletos {#removed-deprecated-features}

Abaixo está uma lista de recursos e funcionalidades marcados como obsoletos [!DNL Experience Manager] 6.5.7.0. Os recursos são marcados como obsoletos inicialmente e posteriormente removidos em uma versão futura. Uma opção alternativa é fornecida.

Revise se você usa um recurso ou um recurso em uma implantação. Além disso, planeje alterar a implementação para usar uma opção alternativa.

| Área | Destaque | Substituição |
|---|---|---|
| Integrações | O **[!UICONTROL Aceitação dos serviços em nuvem AEM]** está obsoleta desde que o [!DNL Experience Manager] e [!DNL Adobe Target] a integração do é atualizada em [!DNL Experience Manager] 6.5. A integração é compatível com a API do Adobe Target Standard. A API usa autenticação por meio do Adobe IMS e [!DNL Adobe I/O Runtime]. Ele suporta o papel crescente do Adobe Launch como instrumento [!DNL Experience Manager] páginas para análise e personalização, o assistente de aceitação é funcionalmente irrelevante. | Configurar conexões do sistema, autenticação do Adobe IMS e [!DNL Adobe I/O Runtime] integrações por meio das respectivas [!DNL Experience Manager] serviços em nuvem. |
| Conectores | O Conector Adobe JCR para Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 está obsoleto para [!DNL Experience Manager] 6.5. | N/A |

## Problemas conhecidos {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* Atualize suas consultas do GraphQL que podem ter usado um nome de API personalizado para seu modelo de conteúdo para usar o nome padrão do modelo de conteúdo.

* Um query GraphQL pode usar a variável `damAssetLucene` em vez de `fragments` índice. Isso pode resultar em queries GraphQL que falham ou levam muito tempo para serem executados.

   Para corrigir o problema, `damAssetLucene` precisa ser configurado para incluir as duas propriedades a seguir:

   * `contentFragment`
   * `model`

   Após a definição do índice ser alterada, é necessária uma reindexação (`reindex` = `true`).

   Após essas etapas, as consultas do GraphQL devem ser executadas mais rapidamente.

* As [!DNL Microsoft®® Windows Server 2019] não suporta [!DNL MySQL 5.7] e [!DNL JBoss®® EAP 7.1], [!DNL Microsoft®® Windows Server 2019] não suporta instalações turnkey para [!DNL AEM Forms 6.5.10.0].

* Se você atualizar seu [!DNL Experience Manager] exemplo de 6.5.0 - 6.5.4 para o service pack mais recente no Java™ 11, você verá `RRD4JReporter` exceções na `error.log` arquivo. Para interromper as exceções, reinicie sua instância de [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* Os usuários podem renomear uma pasta em uma hierarquia em [!DNL Assets] e publicar uma pasta aninhada em [!DNL Brand Portal]. No entanto, o título da pasta não é atualizado em [!DNL Brand Portal] até que a pasta raiz seja republicada.

* Quando um usuário seleciona configurar um campo pela primeira vez em um formulário adaptável, a opção para salvar uma configuração não é exibida no Navegador de propriedades. Selecionar para configurar outro campo do formulário adaptável no mesmo editor resolve o problema.

* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação de [!DNL Experience Manager] 6.5.x.x:
   * &quot;Quando a integração do Adobe Target é configurada em [!DNL Experience Manager] usando a API do Target Standard (autenticação IMS), a exportação de Fragmentos de experiência para o Target resulta na criação de tipos de ofertas incorretos. Em vez do tipo &quot;Fragmento de experiência&quot;/fonte &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/fonte &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * A validação do lado do servidor do Adaptive Form falha quando funções agregadas, como SUM, MAX e MIN são usadas (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de Banner de compra.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` : Tempo limite aguardando a conclusão da alteração de registro não registrada.

* Ao tentar mover/excluir/publicar Fragmentos de conteúdo ou Sites/Páginas, há um problema quando as referências do Fragmento de conteúdo são buscadas, uma vez que a consulta em segundo plano falha; ou seja, a funcionalidade não funciona.
Para garantir a operação correta, você deve adicionar as seguintes propriedades ao nó de definição de índice `/oak:index/damAssetLucene` (não é necessária reindexação):

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

* No AEM Forms, o protocolo POP3 não funciona com pontos de extremidade de email do Microsoft® Office 365.
* Na plataforma JBoss® 7.1.4, quando o usuário instala AEM service pack 6.5.16.0, `adobe-livecycle-jboss.ear` falha na implantação.

## Pacotes de conteúdo e pacotes OSGi incluídos {#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos no [!DNL Experience Manager] 6.5.16.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.16.0](/help/release-notes/assets/65160_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de pacotes de conteúdo incluídos na Experience Manager 6.5.16.0](/help/release-notes/assets/65160_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites restritos {#restricted-sites}

Esses sites só estão disponíveis para clientes do . Se você for um cliente do e precisar de acesso, entre em contato com o gerente de conta do Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Entre em contato com o Suporte ao Cliente Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR)
>* [Inscreva-se em Atualizações de produtos de prioridade da Adobe](https://www.adobe.com/subscription/priority-product-update.html)

