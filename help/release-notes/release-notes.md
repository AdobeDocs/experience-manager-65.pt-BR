---
title: Notas de versão para [!DNL Adobe Experience Manager] 6,5
description: Encontre informações sobre a versão, novidades, instruções de instalação e uma lista detalhada de alterações para [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 3
source-git-commit: 156e83ad9f73e200da70f824b598a713c0e2e97f
workflow-type: tm+mt
source-wordcount: '2195'
ht-degree: 4%

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

Novo suporte de protocolo DASH (Dynamic Adaptive Streaming over HTTP) lançado para transmissão adaptável em vídeo fornecido pelo Dynamic Media (com CMAF [Formato de aplicativo de mídia comum] ativado).

* O streaming adaptativo (DASH/HLS) garante uma melhor experiência de visualização do usuário final para vídeos.
* DASH é o protocolo padrão internacional para transmissão de vídeo adaptável e é amplamente adotado no setor.
* Disponível agora na América do Norte (para ser habilitado por meio de tíquete de suporte), em breve na Ásia-Pacífico e Europa-Oriente Médio-África.

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

>[!NOTE]
>
>Correções na [!DNL Experience Manager] O Forms é fornecido por meio de um pacote complementar separado uma semana após o agendamento [!DNL Experience Manager] Data de lançamento do Service Pack. Nesse caso, os pacotes complementares serão lançados na quinta-feira, 2 de março de 2023. Além disso, uma lista de correções e aprimoramentos do Forms é adicionada a esta seção.

<!--
### [!DNL Forms] Fixes {#forms-fixes-6516}
-->

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

>[!NOTE]
>
>Ignorar se não estiver usando [!DNL Experience Manager] Forms.

Correções na [!DNL Experience Manager] O Forms é fornecido por meio de um pacote complementar separado uma semana após a [!DNL Experience Manager] Versão do Service Pack.

<!-- 

For instructions to install the service pack on AEM Forms, see [AEM Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).
-->

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

| Área | Recurso | Substituição |
|---|---|---|
| Integrações | O **[!UICONTROL Aceitação dos serviços em nuvem AEM]** está obsoleta desde que o [!DNL Experience Manager] e [!DNL Adobe Target] a integração do é atualizada em [!DNL Experience Manager] 6.5. A integração é compatível com a API do Adobe Target Standard. A API usa autenticação por meio do Adobe IMS e [!DNL Adobe I/O Runtime]. Ele suporta o papel crescente do Adobe Launch como instrumento [!DNL Experience Manager] páginas para análise e personalização, o assistente de aceitação é funcionalmente irrelevante. | Configurar conexões do sistema, autenticação do Adobe IMS e [!DNL Adobe I/O Runtime] integrações por meio das respectivas [!DNL Experience Manager] serviços em nuvem. |
| Conectores | O Conector Adobe JCR para Microsoft® SharePoint 2010 e Microsoft® SharePoint 2013 está obsoleto para [!DNL Experience Manager] 6.5. | N/A |

## Problemas conhecidos {#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.
 -->
<!-- REMOVED AS PER CQDOC-20022, JANUARY 23, 2023 * If you install [!DNL Experience Manager] 6.5 Service Pack 10 or a previous service pack on [!DNL Experience Manager] 6.5, the runtime copy of your assets custom workflow model (created in `/var/workflow/models/dam`) is deleted.
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
`<designModelPath>/jcr:content.generate.json`. -->

* [AEM Fragmento de conteúdo com o Pacote de índice GraphQL 1.0.5](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Fcfm-graphql-index-def-1.0.5.zip)
Esse pacote é necessário para clientes que usam o GraphQL; isso permite que eles adicionem a definição de índice necessária com base nos recursos que realmente usam.

* Atualize suas consultas do GraphQL que podem ter usado um nome de API personalizado para seu modelo de conteúdo para usar o nome padrão do modelo de conteúdo.

* As [!DNL Microsoft® Windows Server 2019] não suporta [!DNL MySQL 5.7] e [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] não suporta instalações turnkey para [!DNL AEM Forms 6.5.10.0].

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

## Pacotes de conteúdo e pacotes OSGi incluídos {#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos no [!DNL Experience Manager] 6.5.16.0: <!-- UPDATE FOR EACH NEW RELEASE -->

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.16.0](/help/release-notes/assets/65160_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Lista de pacotes de conteúdo incluídos na Experience Manager 6.5.16.0](/help/release-notes/assets/65160_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## Sites restritos {#restricted-sites}

Esses sites só estão disponíveis para clientes do . Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Entre em contato com o Suporte ao Cliente Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] página do produto](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] Documentação 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR)
>* [Inscreva-se em Atualizações de produtos de prioridade da Adobe](https://www.adobe.com/subscription/priority-product-update.html)

