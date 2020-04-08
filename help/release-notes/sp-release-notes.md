---
title: 'Notas de versão do AEM 6.5 Service Pack '
description: Notas de versão específicas do Adobe Experience Manager 6.5 Service Pack 4.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: be4a8a78b8555149809b8026bfd059f4cc9e9401

---


# Notas de versão do Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Informações da versão {#release-information}

| Produtos | **Adobe Experience Manager 6.5** |
|---|---|
| Versão | 6.5.4.0 |
| Tipo | Lançamento do Service Pack |
| Data | 05 de março de 2020 |
| URL de download | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0), Distribuição [de software (Beta)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.4.zip) |

## O que está incluído no Adobe Experience Manager 6.5.4.0 {#what-s-included-in-aem}

O Adobe Experience Manager 6.5.4.0 é uma atualização importante que inclui novos recursos, melhorias importantes solicitadas pelo cliente e desempenho, estabilidade, melhorias de segurança, lançadas desde a disponibilização geral da versão 6.5 em **abril de 2019**. Ele pode ser instalado na parte superior do Adobe Experience Manager (AEM) 6.5.

Alguns dos principais recursos e melhorias introduzidos no AEM 6.5.4.0 incluem:

* O AEM Assets agora está configurado com o Brand Portal por meio do console de E/S da Adobe.

* Uma nova etapa [Gerar saída](../forms/using/aem-forms-workflow-step-reference.md) imprimível agora está disponível para workflows do AEM Forms.

* [Suporte](../forms/using/resize-using-layout-mode.md) para várias colunas no modo de layout para formulários adaptáveis e Comunicações interativas.

* Suporte para [Rich Text](../forms/using/designing-form-template.md) em formulários HTML5.

* [Aprimoramentos](new-features-latest-service-pack.md#accessibility-enhancements) de acessibilidade nos ativos Experience Manager.

* O repositório integrado (Apache Jackrabbit Oak) foi atualizado para a versão 1.10.8.

* Agora você pode sincronizar subárvores de conteúdo seletivo para o *Dynamic Media - modo* Scene7 em vez de todos os disponíveis em `content/dam`.

* A integração do modelo de dados de formulário com o serviço da Web SOAP agora oferece suporte a grupos de escolha ou atributos em elementos.

* A entrada ou saída SOAP e estruturas de dados complexas agora suportam Substituição de Grupo Dinâmico.

Para obter uma lista completa dos recursos, destaques principais, recursos principais introduzidos em service packs AEM 6.5 anteriores, consulte [Novidades do Adobe Experience Manager 6.5 Service Pack 4](new-features-latest-service-pack.md).

### Sites {#sites-fixes}

* Quando um URL de uma página do AEM Sites contiver dois pontos (: ) ou símbolo de porcentagem (%), o navegador subjacente pára de responder e os ciclos da CPU mostram um pico (NPR-32369, NPR-31918).

* Quando uma página do AEM Sites é aberta para edição e um componente é copiado, a ação de colar permanece indisponível para alguns espaços reservados (NPR-32317).

* Quando o assistente Gerenciar publicação é aberto, um Fragmento de experiência vinculado a um Componente principal não é exibido nas listas de referências publicadas (NPR-32233).

* A visão geral da Live Copy na interface do usuário de toque demora muito mais do que a interface clássica para renderizar (NPR-32149).

* Quando a hora do servidor e a hora da máquina estiverem em fusos horários diferentes, a hora de publicação programada exibe a hora do servidor na interface do usuário de toque, enquanto na interface clássica, a hora da máquina é exibida (NPR-32077).

* Falha do AEM Sites ao abrir uma página com um sufixo no URL (NPR-32072).

* Quando um usuário edita um Fragmento de conteúdo, uma variação excluída do Fragmento de conteúdo é restaurada (NPR-32062).

* Os usuários podem salvar um Fragmento de conteúdo sem fornecer informações nos campos obrigatórios (NPR-31988).

* kernel.js e ui.js não são pré-cumpridos ou armazenados em cache. Leva a mais tempo na renderização de páginas (NPR-31891).

* Quando PageEventAuditListener está ativado, o comprimento da fila de confirmação aumenta. Isso afeta o desempenho de muitas operações, como publicação em massa, navegação, movimentação de ativos em massa (NPR-31890).

* Quando os Fragmentos de experiência são arrastados, é observado um tempo de resposta elevado (NPR-31878).

* Quando você seleciona a opção Arrastar o componente aqui no espaço reservado de uma grade responsiva, uma solicitação GET é enviada e a solicitação resulta em erro HTTP 403 (NPR-31845).

* Ao mover o conteúdo dentro da mesma pasta, a opção de movimentação de página é desativada (NPR-31840).

* No modo de estrutura de modelos editáveis, a lista de componentes permitidos no container de layout exibe resultados incorretos. Somente os componentes com caixa de diálogo de design são exibidos no container de layout (NPR-31816).

* Quando uma página tem permissões somente leitura para um usuário, a opção de propriedades Abrir fica visível em sites.html, mas não no editor.html (NPR-31770).

* Quando um usuário clica no botão Criar, a opção de página não está disponível (NPR-31756).

* Não é possível sincronizar a campanha na campanha da Adobe que contém o componente importador de design OOTB (pronto para uso) (NPR-31728).

* Quando você tenta alterar uma lista de marcador para lista numerada, somente os dois primeiros itens da lista são alterados (NPR-31636).

* Quando uma página não é criada e o nó filho é selecionado, a caixa de diálogo de seleção ainda exibe o nó inicial. Quando a página é criada e o usuário clica em navegar, a página redireciona para o nó raiz em vez do nó criado (NPR-31618).

* A caixa de diálogo de configuração da visualização não funciona corretamente para o recurso de fluxo de trabalho de personalização da Caixa de entrada (NPR-32503 e NPR-32492).

* Uma mensagem de erro é exibida ao exibir informações do fluxo de trabalho usando a Caixa de entrada (CQ-4282168).

### Ativos {#assets-6540-enhancements}

* O botão para acionar o fluxo de trabalho na página de coleta de ativos está desativado (NPR-32471).

* Uma pasta sem nome é criada no SPS (Scene7 Publishing System) ao mover um ativo de uma pasta para outra no Experience Manager com a configuração do Dynamic Media Scene7 (NPR-32440).

* A ação para mover todos os ativos (usando Selecionar tudo e mover) para uma pasta que contém os ativos publicados falha com erro (NPR-32366).

* Falha na geração da execução de ativos com ${extension} (NPR-32294).

* Os URLs do histórico de versões são exibidos no campo Referenciado por na página de Propriedades de ativos (NPR-31889).

* O arquivo ZIP baixado do DAM não pode ser aberto usando o WinZip (NPR-32293).

* As permissões originais de uma pasta são atualizadas quando as Configurações da pasta são abertas para alterar o título da pasta ou a imagem em miniatura e salvas (NPR-32292).

* O ícone de calendário para ativação programada não é exibido na coluna Status (na interface clássica da lista de ativos DAM) para ativos cuja ativação está programada para uma data e hora posteriores (NPR-32291).

* A criação de fragmentos usando modelos de fragmento fornece erro ao pesquisar coleções durante o processo de criação de fragmento (NPR-32290).

* Vários query de pesquisa são disparados quando várias tags são selecionadas do filtro de pesquisa (NPR-32143).

* A interface do usuário do Experience Manager Assets exibe nomes de arquivo truncados quando ativos com mais de 50 caracteres no nome do arquivo são carregados (NPR-32054).

* Todas as caixas de seleção no painel Filtro são apagadas quando a primeira e a segunda caixas de seleção são apagadas, quando as caixas de seleção de nível dois da árvore de caixas de seleção no Adobe Stock são selecionadas (NPR-31919).

* A pesquisa de arquivos e pastas usando aspectos Omnisearch dá exceção (NPR-31872).

* O realce de campo para seleção obrigatória de campo no editor de metadados não é removido mesmo depois de selecionar o campo obrigatório, quando as regras de dependência são definidas no formulário de schema de metadados correspondente (NPR-31834).

* Os nomes completos das tags de nível de folha (da hierarquia de tags) não são exibidos na página Propriedades do ativo (NPR-31820).

* O uso do comando back da página Propriedades do ativo no navegador Safari dá um erro (NPR-31753).

* A página de resultados da pesquisa de interface de toque (feita pelo Omnisearch) rola automaticamente para cima e perde a posição de rolagem do usuário (NPR-31307).

* A página de detalhes de ativos de ativos PDF não mostra botões de ação exceto Para coleção e Adicionar representação no Experience Manager em execução no modo de execução do Dynamic Media Scene7 (CQ-4286705).

* Os ativos demoram muito para serem processados pelo processo de upload em lote do Scene7 (CQ-4286445).

* O botão Salvar não importa o Conjunto Remoto quando o usuário não tiver feito nenhuma alteração no Editor de Conjunto no Cliente de Mídia Dinâmica (CQ-4285690).

* A miniatura de ativos 3D não é informativa quando um modelo 3D suportado é assimilado no AEM (CQ-4283701).

* O status não processado da predefinição do visualizador de vídeo de recorte inteligente aparece duas vezes no texto do banner ao lado do nome predefinido (CQ-4283517).

* Altura incorreta do container de um modelo 3D carregado visualizado no visualizador 3D é observada na página de detalhes do ativo (CQ-4283309).

* O Editor de carrossel não abre no IE 11 no modo Híbrido de mídia dinâmica do Experience Manager (CQ-4255590).

* O foco do teclado fica travado no menu suspenso Email na caixa de diálogo Download, nos navegadores Chrome e Safari (NPR-32067).

* A caixa de seleção Sincronizar todo o conteúdo não está ativada por padrão ao tentar adicionar a configuração de nuvem DM no AEM (CQ-4288533).

### Interface do usuário do Foundation {#foundation-ui-6540}

* O controle do mouse muda para o campo de filtro anterior em vez de permanecer no campo de filtro existente enquanto pesquisa ativos usando o painel Filtro (NPR-32538).

* Marcação de plataforma: Pesquise por tags digitando nos campos de tag mostra tags fora dos limites raiz e não respeita a propriedade `rootPath` dos campos de tag (NPR-31895).

* Interface do usuário da plataforma: O navegador de caminho quebra se um caminho inválido for adicionado no campo de texto (NPR-31884).

* A notificação fica oculta atrás de um menu fixo na seleção da página (NPR-31628).

### Plataforma {#platform-sling-6540}

* (HTL) Os sublinhados substituem dois pontos na seção de caminho do URL (NPR-32231).

### Projetos {#projects-6540}

* O botão Criar não estará visível para o usuário mesmo se ele tiver permissão para criar um projeto na subpasta (NPR-31832).

### Tradução de projetos {#projects-translation-6540}

* A criação do projeto de tradução quebra a interface quando a opção Aparar espaços é ativada em `Apache Sling JSP Script Handler` (NPR-32154).

* Erro na interface do usuário e exceção de ponto nulo em registros de erros é observada quando qualquer tag, a ser traduzida, é adicionada a um projeto de tradução (NPR-31896).

### Integrações {#integrations-6540}

* A geração do URL da biblioteca de inicialização é baseada somente em `path` e `library_name` valores da API de inicialização e não se baseia no `library_path` valor (NPR-31550).

* Uma mensagem de erro é exibida durante o processamento de itens relacionados ao LiveFyre (FYR-12420).

### Editor de modelos WCM {#wcm-template-editor-6540}

* No modo de estrutura de modelos editáveis, a lista de componentes permitidos no container de layout não exibe o componente de botão de link (CQ-4282099).

### WCM Page Editor {#wcm-page-editor-6540}

* Erro ao selecionar uma sobreposição e depois selecionar a grade responsiva Arraste os componentes aqui (CQ-4283342).

### Campaign Targeting {#campaign-targeting-6540}

* Falha na configuração da nuvem de Públicos alvos com o erro de obtenção de mboxes (CQ-4279880).

### Brand Portal {#assets-brand-portal}

* Os usuários do Brand Portal não podem publicar ativos de pasta de contribuição nos ativos AEM ao atualizar para a E/S da Adobe no AEM 6.5.4 (CQDOC-15655).

   Esse problema será corrigido no próximo service pack AEM 6.5.5.

   Para corrigir imediatamente o AEM 6.5.4, é recomendável [baixar a correção](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/hotfix/cq-6.5.0-hotfix-33041) e instalá-la na instância do autor.


* Os valores suspensos do schema de metadados não estão visíveis nas propriedades do ativo (CQ-4283287).

* O subesquema de metadados não exibe guias com base no tipo MIME nas propriedades do ativo (CQ-4283288).

* Cancelar a publicação do schema de metadados preenche uma mensagem de erro, embora o schema seja removido do backend.

* A imagem de Pré-visualização não é exibida para um ativo publicado (CQ-4285886).

* O usuário não pode publicar ou cancelar a publicação de ativos contendo aspas simples no nome (CQ-4272686).

* Os termos e condições não são exibidos durante o download de vários ativos (CQ-4281224).

* Pequenas vulnerabilidades de segurança abordadas.

### Communities {#communities}

* O formulário Criar membro é exibido como uma página em branco (NPR-31997).

* O usuário não pode visualização o relatório do Analytics na instância do autor (NPR-30913).

### Oak - Indexação e Query {#oak-indexing-6540}

* Os documentos do MS Word e do MS Excel, que contêm imagem JPEG, quando analisados com o analisador Tika não conseguem analisar e o erro de classe não encontrada é observado (NPR-31952).

### Forms {#forms-6530}

>[!NOTE]
>
>O AEM Service Pack não inclui correções para o AEM Forms. Eles são entregues usando um pacote complementar separado do Forms. Além disso, é lançado um instalador cumulativo que inclui correções para o AEM Forms no JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

* Gerenciamento de correspondência: As letras exibem caracteres extras após o envio aos workflows do processo de publicação (NPR-32626).

* Gerenciamento de correspondência: As letras exibem um espaço reservado suspenso como um componente de texto após a submissão a workflows pós-processo (NPR-32539).

* Gerenciamento de correspondência: Os valores padrão definidos no modelo de letra não são exibidos no modo de Pré-visualização (NPR-32511).

* Formulários móveis: O botão Enviar é exibido como expandido em tamanho ao renderizar um formulário XDP em uma versão HTML (NPR-32514).

* Serviços do Documento: Problemas de acesso ao URL para Cartas e outras páginas após a aplicação do Service Pack 2 (NPR-32508, NPR-32509).

* Serviços do Documento: Se o número de transações em um servidor exceder um limite específico, a conversão de HTML em PDF falhará e as configurações de tipo de arquivo serão removidas do servidor de formulários AEM (NPR-32204).

* Formulários adaptativos: A ferramenta de acessibilidade do navegador relata falhas em formulários adaptáveis de acordo com as diretrizes WCAG2 Nível AA (NPR-32312, NPR-32309, CQ-4285439).

* Formulários adaptativos: A ferramenta de acessibilidade do navegador Chrome informa uma falha de prática recomendada (NPR-32310).

* Formulários adaptativos: Problemas de tradução ao configurar um formulário adaptável incorporado em uma página do AEM Sites (NPR-32168).

* Bancada: Uma mensagem de erro é exibida ao usar a operação Obter propriedades do PDF para o serviço Utilitários do PDF (NPR-32150).

* Segurança do Documento: Um arquivo PDF protegido falha ao abrir offline com a opção DisableGlobalOfflineSynchronizationData definida como True (NPR-32078).

* Designer: Se a opção de marcação estiver ativada, a borda do subformulário desaparecerá na saída PDF gerada (NPR-32547, NPR-31983, NPR-31950).

* Designer: Se houver células unidas em uma tabela, o teste de acessibilidade falhará para o arquivo PDF de saída convertido de um formulário XDP usando o serviço de saída (CQ-4285372).

* JEE de base: Se um servidor do AEM Forms for desconectado de um cluster, problemas de cache impedirão que ele se reconecte ao servidor (NPR-32412).

## Install 6.5.4.0 {#install}

**Requisitos de configuração**

* AEM 6.5.4.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* O download do Service Pack está disponível no Compartilhamento de pacotes da Adobe, que pode ser acessado diretamente da instância do AEM 6.5.
* Em uma implantação com MongoDB e várias instâncias, instale o AEM 6.5.4.0 em uma das instâncias do autor usando o Gerenciador de pacotes.
* Antes de instalar o Service pack, verifique se você tem um instantâneo ou um backup atualizado da sua instância do AEM.
* Reinicie a instância antes da instalação. Embora isso seja necessário apenas quando a instância ainda está no modo de atualização (e esse é o caso quando a instância foi atualizada de uma versão anterior), é recomendável se a instância estava em execução por um período mais longo.

>[!CAUTION]
>
>A Adobe não recomenda remover ou desinstalar o pacote AEM 6.5.4.0.

### Instalar o Service Pack por meio do Compartilhamento de pacotes {#install-service-pack-via-package-share}

Execute as seguintes etapas para instalar o Service Pack em uma instância do AEM 6.5 existente:

1. Login to Package Share from within AEM or directly from your browser and download the [AEM 6.5.4.0 package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0).

1. Instale o pacote baixado usando o Gerenciador de pacotes.

>[!NOTE]
>
>**A caixa de diálogo na interface do usuário do Gerenciador de pacotes às vezes sai imediatamente durante a instalação da versão 6.5.4.0**
>
>Portanto, é recomendável aguardar a estabilização dos registros de erros antes de acessar a instância. O usuário deve aguardar os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações foram bem-sucedidas. Geralmente isso acontece no Safari, mas pode acontecer intermitentemente em qualquer navegador.

**Instalação automática**

Há duas maneiras de instalar automaticamente o AEM 6.5.4.0 em uma instância em execução:

A. Coloque a embalagem em ..*pasta /crx-quickstart/install* enquanto o servidor estiver disponível online. O pacote é instalado automaticamente.

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/pt/crx/2-3/how_to/package_manager.html) - make sure that you use cmd=install&amp;recursive=true - so the nested packages  are  installed.

>[!NOTE]
>
>O AEM 6.5.4.0 não oferece suporte à instalação do Bootstrap.

**Validar instalação**

1. A página Informações do produto (/system/console/ productinfo) exibe a string da versão atualizada `Adobe Experience Manager, Version 6.5.4.0` em Produtos instalados.

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. O pacote OSGI org.apache.Jackrabbit.oak-core está na versão 1.10.6 ou superior (Use o console da Web: /system/console/bundles).

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Install AEM Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Pule se você não estiver usando o AEM Forms. As correções do AEM Forms são entregues por meio de um pacote complementar separado.

>[!NOTE]
>
>AEM 6.5.4.0 includes a new version of [AEM Forms Compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). Se você estiver usando uma versão mais antiga do pacote Compatibilidade com formulários AEM e estiver atualizando para o AEM 6.5.4.0, instale a versão mais recente do pacote Compatibilidade com formulários AEM após a instalação do Pacote complementar de formulários.

1. Verifique se você instalou o AEM Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Pule se você não estiver usando o AEM Forms no JEE. Correções no AEM Forms em JEE são entregues por meio de um instalador separado.

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0011](https://helpx.adobe.com/br/aem-forms/quick-fixes/6-5/jee-patch-0011.html).

#### Instalador do Workbench

Como se trata de um instalador completo, o tamanho do arquivo é maior comparado à versão de correção. Desinstale a versão anterior do Workbench antes de instalar a nova.

### UberJar {#uber-jar}

The UberJar for AEM 6.5.4.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.4/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.4</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

A versão atualizada do UberJar para 6.5.4.0 que inclui o pacote **com.fasterxml.Jackson.core.async** está disponível no repositório [do](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.4-1.0/)Adobe Public Maven.

Se você usar a versão atualizada do UberJar, inclua a seguinte dependência no POM do projeto:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version> 6.5.4-1.0</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Recursos obsoletos {#removed-deprecated-features}

Esta seção lista recursos e recursos que foram marcados como obsoletos com o AEM 6.5.4.0. Os recursos que estão planejados para serem removidos em uma versão futura são definidos como obsoletos primeiro, com uma opção alternativa a ser usada.

Recomenda-se que os clientes revisem se utilizam o recurso ou a capacidade em sua implantação atual e façam planos para alterar sua implementação para usar a opção alternativa.

| Área | Recurso | Substituição |
|---|---|---|
| Integrações | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. Com a integração do AEM e do Público alvo atualizada no AEM 6.5 para suportar a API do Público alvo Standard, que usa autenticação por meio do Adobe IMS e E/S, e a função crescente do Adobe Launch para instrumentar páginas do AEM para análise e personalização, o assistente de opção de participação se tornou funcionalmente irrelevante. | Configurar conexões do sistema, autenticação do Adobe IMS e integrações de E/S da Adobe por meio dos respectivos serviços em nuvem do AEM |

## Problemas conhecidos {#known-issues}

* Se o assistente de configuração **de ativos** conectados retornar uma mensagem de erro 404 após a instalação, reinstale manualmente os pacotes **cq-remotedam-client-ui-content** e **cq-remotedam-client-ui-components** usando o Gerenciador de pacotes.
* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação do AEM 6.5.x.x:
   * &quot;Quando a integração do Target é configurada no AEM usando a API do Target Standard (autenticação IMS), a exportação de Fragmentos de experiência para o Target resulta na criação de tipos de ofertas incorretos. Em vez do tipo &quot;Fragmento de experiência&quot;/fonte &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/fonte &quot;Adobe Target Classic&quot;.
   * com.adobe.granite.manutenção.impl.TaskScheduler: nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * A validação do lado do servidor do Formulário adaptável falha quando funções de agregação, como SUM, MAX e MIN são usadas. CQ-4274424
   * com.adobe.granite.manutenção.impl.TaskScheduler: nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de banner de compra.

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos no AEM 6.5.4.0

Lista de pacotes OSGi incluídos no AEM 6.5.4.0

[Obter arquivo](assets/6540_bundles.txt)

Lista de pacotes de conteúdo incluídos no AEM 6.5.4.0

[Obter arquivo](assets/6540_packages.txt)

## Restricted sites {#restricted-sites}

Estes sites estão disponíveis somente para clientes. Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Entre em contato com o suporte](https://daycare.day.com/public/contact.html)ao cliente Para obter mais informações sobre como acessar o portal de suporte, consulte [Acesso ao portal](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)de suporte.

>[!MORE COMO ESTE]
>
>* [Notas de versão do AEM 6.5](/help/release-notes/release-notes.md)
>* [Página do produto AEM](https://www.adobe.com/solutions/web-experience-management.html)
>* [Documentação do AEM 6.5](https://helpx.adobe.com/support/experience-manager/6-5.html)
>* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

