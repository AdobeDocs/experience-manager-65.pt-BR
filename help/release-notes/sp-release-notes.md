---
title: 'Notas de versão do AEM 6.5 Service Pack '
description: Notas de versão específicas do Adobe Experience Manager 6.5 Service Pack 3.
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
translation-type: tm+mt
source-git-commit: 9f4a460c7f64d86e35e950e512ed5b6cda1cbf2a

---


# Notas de versão do Adobe Experience Manager 6.5 Service Pack {#aem-service-pack-release-notes}

## Informações da versão {#release-information}

| Produtos | **Adobe Experience Manager 6.5** |
|---|---|
| Versão | 6.5.3.0 |
| Tipo | Lançamento do Service Pack |
| Data | 12 de dezembro de 2019 |
| URL de download | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0) |

## O que está incluído no Adobe Experience Manager 6.5.3.0 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.3.0 is an important release that includes performance, stability, security, and key customer fixes and enhancements released since the general availability of 6.5 release in **April 2019**. Ele pode ser instalado na parte superior do Adobe Experience Manager (AEM) 6.5.

Alguns destaques principais desta versão do Service pack:

* O repositório integrado (Apache Jackrabbit Oak) foi atualizado para a versão 1.10.6.

* Os ativos do Experience Manager agora oferecem suporte a arquivos ZIP criados com o algoritmo Deflate 64.

* A nova coluna para a data criada, que é classificável, foi adicionada na exibição de lista DAM e nos resultados da pesquisa de ativos na exibição de lista.

* A classificação de ativos com base na coluna Nome foi ativada na exibição Lista.

* O Dynamic Media agora é compatível com ativos de vídeo de Recorte inteligente. O Smart Crop é um recurso orientado por aprendizado de máquina que recorta um vídeo enquanto move o quadro para seguir o ponto focal da cena.

* O Dynamic Media suporta a criação de imagens inteligentes.

* Capacidade de [definir preferências de Ausência Temporária](../forms/using/configure-out-of-office-settings.md) nos fluxos de trabalho do AEM.

* Capacidade de [compartilhar itens](../forms/using/configure-shared-queues-osgi.md) de Caixa de entrada ou Caixa de entrada com outros usuários nos fluxos de trabalho do AEM.

* Capacidade de [gerar Comunicações interativas no modo](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)Lote.

* Versão atualizada do jQuery fornecido no ContextHub para 3.4.1.

### Lista de alterações {#list-of-changes}

#### Ativos {#assets-6530-enhancements}

**Aprimoramentos do produto**

* Os ativos do Experience Manager agora oferecem suporte a arquivos ZIP criados com o algoritmo Deflate 64 (NPR-27573).

* A nova coluna para a data criada, que é classificável, foi adicionada na exibição de lista DAM e nos resultados da pesquisa de ativos na exibição de lista (NPR-31312).

* A classificação de ativos com base na coluna Nome foi permitida na exibição Lista (NPR-31299).

* Os arquivos de ativos GLB, GLTF, OBJ e STL suportam a visualização de ativos na página Detalhes do ativo no DAM (CQ-4282277).

* O evento ReplicationOnModifyListener é acionado para nós de segmentos durante o carregamento de segmentos no Dynamic Media (CQ-4281279).

* O Dynamic Media agora é compatível com ativos de vídeo de Recorte inteligente. O Smart Crop é um recurso acionado pelo aprendizado de máquina que recorta um vídeo enquanto move o quadro para seguir o ponto focal da cena (CQ-4278995).

* O Dynamic Media oferece suporte para o Smart Imaging (CQ-4222249).

* A exibição de pesquisa/navegação foi definida como exibição padrão no seletor do Foundation se os parâmetros de consulta forem passados na solicitação (NPR-31601).

**Correções**

* Os metadados de alguns documentos PDF não são atualizados e salvos no PDF ao modificar seu título (NPR-31629).

* O compartilhamento de ativos não funciona para ativos com o caractere &quot;+&quot; em seus nomes (NPR-31547).

* As edições no formulário de pesquisa padrão Assets Admin * Search Rail não funcionam como esperado (NPR-31502).

* As sugestões não são mostradas ao usar a exibição Omnisearch em ativos para pesquisar ativos (NPR-31496).

* As referências de ativos em coleções não são atualizadas quando os ativos referenciados são movidos para outro local, nos casos em que os mesmos ativos são referenciados por coleção diferente por usuários diferentes (NPR-31486).

* Tags IPTC duplicadas são adicionadas aos metadados do ativo (NPR-31328).

* A contagem de resultados da pesquisa no canto superior direito não é atualizada corretamente quando a pesquisa é acionada do painel de filtros (NPR-31316).

* Todas as caixas de seleção são desmarcadas ao desmarcar as caixas de seleção de segundo nível no filtro Tipo de arquivo e o texto na barra de pesquisa não está sincronizado com as propriedades selecionadas/não selecionadas (NPR-31287).

* Não é possível remover todos os membros (utilizadores/grupos) da seção Membros de uma pasta; ao tentar remover todos os usuários, o usuário conectado é adicionado à lista (NPR-31171).

* Os ativos com o símbolo &quot;+&quot; no nome do arquivo não podem ser excluídos (NPR-31162).

* O menu suspenso Criar, que está visível no menu superior ao selecionar uma pasta, não mostra a opção &quot;Pasta&quot; como uma opção de criação (NPR-30877).

* A seleção de pasta Criar > item de ação FileUpload está ausente quando a ACL para Negar jcr:removeChildNodes e jcr:removeNode no caminho é aplicada para um usuário (NPR-30840).

* Os fluxos de trabalho do DAM entram em estado obsoleto quando determinados ativos mp4 são carregados, fazendo com que todos os fluxos de trabalho restantes entrem em estado obsoleto (NPR-30662).

* Erro de falta de memória é observado quando um grande arquivo PDF (de vários Gigabytes) é carregado no DAM e seus subativos são processados (NPR-30614).

* A movimentação em massa de ativos está falhando e exibindo a mensagem de aviso (NPR-30610).

* Os nomes dos ativos são alterados para letras minúsculas ao mover ativos de uma pasta para outra no AEM em execução no modo de execução do Dynamic Media Scene 7 (NPR-31630).

* Ocorreu um erro ao editar um conjunto de imagens remoto, para a imagem que reside na pasta com o mesmo nome que o nome da empresa Scene 7 (NPR-31340).

* Os ativos do Dynamic Media que contêm referências não estão sendo publicados (NPR-31180).

* Os uploads do AEM Dynamic Media - modo de execução do Scene 7 para o Scene 7 estão demorando muito para serem concluídos (NPR-31048).

* O ponto de acesso adicionado a um ativo de imagem não é visível por meio do Visualizador de imagem interativo na página de detalhes do ativo (NPR-30979).

* Grandes trabalhos de sling são criados e o banner Processamento é reexibido quando as ações realizadas em ativos do AEM são passadas para o Scene 7 (NPR-30947).

* O conflito ocorre ao criar a Cópia de idioma dos ativos e os ativos não são carregados no Scene 7 (NPR-30932).

* As renderizações dinâmicas baixadas do AEM em execução no modo Híbrido do Dynamic Media estão quebradas (elas são do tipo de texto com o conteúdo &quot;não é possível localizar a imagem&quot; em vez do tipo de conteúdo da imagem) (NPR-30876).

* O fluxo de trabalho do Dynamic Media Encode Video está falhando ao gerar miniatura para o vídeo que é migrado do Scene 7 para o Dynamic Media - modo de execução do Scene 7 (CQ-4282011).

* IpsApiException observou ao migrar ativos de uma instância para outra usando diferentes IDs de empresa do Scene 7 (CQ-4280548).

* A miniatura de ativos 3D não é informativa quando um modelo 3D suportado é assimilado no AEM (CQ-4283701).

* Os botões de rolagem são exibidos no visualizador, se um ativo 3D tiver poucas exibições de câmera (CQ-4283322).

* Altura incorreta do contêiner de um modelo 3D carregado visualizado no DimensionalViewer na página Detalhes do ativo (CQ-4283309).

* Não é possível reproduzir vídeos com o SmartCropVideoViewer no Internet Explorer 11 e no Safari (CQ-4281422).

* O uso do botão mover para mover vários ativos, de uma pasta para outra, falha no AEM em execução no Dynamic Media - modo de execução cena7 (CQ-4280384).

* Vídeo distorcido é visto nos detalhes do ativo quando o tipo MIME é diferente de MP4 (CQ-4279704).

* Os vídeos recém-ingeridos em pastas com perfil de vídeo permanecem no estado de processamento mesmo após a porcentagem de codificação ser concluída para 100% (CQ-4279389).

* Mover ativos de uma pasta cria um grande número de tarefas de sling (chamadas de API Scene 7) do que o ideal (CQ-4278664).

* Os nomes do conjunto de imagens são alterados para minúsculas na Cena 7, quando o conjunto de imagens (ou conjunto de imagens) é criado e nomeado com a convenção de nomenclatura apropriada no DAM (CQ-4281112).

* O Scene 7 Migrator define o estado de publicação incorretamente (CQ-4263492).

* A página de resultados da pesquisa de interface de toque (feita pelo Omnisearch) rola automaticamente para cima e perde a posição de rolagem do usuário em Fragmentos de conteúdo (CQ-4282898).

* Os arquivos PDF não são indexados e o conteúdo não é pesquisável (CQ-4278916).

* Erro &quot;Grupo não listado pelo seletor de usuários: esperado &quot;falso para verdadeiro igual&quot; é observado ao adicionar o Grupo de usuários fechado com diferentes `principalName` e `authorizableId` (CQ-4278177).

* A Exibição de coluna da interface do usuário do Assets está mostrando todos os caminhos, independentemente do caminho raiz do locatário específico (CQ-4278175).

* A pesquisa do seletor de ativos não está funcionando como esperado (CQ-4275886).

* Os fluxos de trabalho de execução estão falhando (CQ-4271928).

* A Expurgação de evento do DAM exclui os dados de evento mais recentes (maxSavedActivities) e armazena os dados criados anteriormente (NPR-31336).

* A página de resultados da pesquisa de interface de toque (feita pelo Omnisearch) rola automaticamente para cima e perde a posição de rolagem do usuário (NPR-31307).

* A barra de ações e a contagem de ativos não são atualizadas ao selecionar todos e depois desmarcar alguns itens (pastas/ativos individuais) na interface de usuário do toque (NPR-31118).

* Uma exceção é exibida no AEM ao pesquisar os detalhes de um ativo (CQ-4283569).

* Vulnerabilidade XSS no DAM (NPR-31654).

#### Sites {#sites}

* Se a herança do LiveCopy for quebrada, as páginas de Live Copy exibirão links de cópia de idioma em vez de links do LiveCopy (NPR-30980).
* Para um novo Blueprint, se o número de registros for superior a 40, somente os primeiros 40 registros serão exibidos. O Blueprint exibe linhas em branco para o restante dos registros (NPR-31182).
* Quando um usuário adiciona caracteres japoneses ou coreanos na propriedade de descrição de um menu, o menu exibe caracteres distorcidos para o texto em japonês e coreano. (NPR-31331).
* O Editor de Rich Text (RTE) não permite inserir uma Tabela incorporada como um item de lista (NPR-30879).
* Fora da caixa, andaime do Editor de Rich Text (RTE). aplica o tamanho da fonte em linha aos elementos, inesperadamente (NPR-31284).
* Quando um usuário foca nos campos do painel à esquerda e usa um atalho do teclado para colar o conteúdo, ele cola o conteúdo da área de transferência do editor de páginas em vez do conteúdo copiado dos campos do painel à esquerda (NPR-31172).
* Quando um usuário adiciona um campo Upload de arquivo a um campo múltiplo, o caminho da imagem é armazenado no nó do componente em vez do nó de vários campos (NPR-30882).
* A API ResponsiveGridExporter não retorna a interface com.day.cq.wcm.Foundation.model.impl.export.AllowedComponentsExporter. O pacote com.day.cq.wcm.Foundation.model.impl é declarado como pacote privado (NPR-31398).
* Quando uma página que contém alguns Fragmentos de experiência é aberta no modo não editor (no Autor sem o `editor.html` prefixo e `wcmmode=disabled`, ou no Editor)., a solicitação termina no código de erro de status HTTP 500 (NPR-30743).
* Os usuários não podem alterar sua senha e acessar sua página de perfil (NPR-31161).
* Um arquivo JavaScript com dados do usuário é gerado no lado do servidor (NPR-30822).
* A interface de usuário de criação do AEM permite phishing usando conteúdo externo (NPR-29745).
* Vulnerabilidade de injeção de idioma de expressão no editor de metadados AEM 6.5 (NPR-31017).

#### Pesquisa e interface do usuário {#search-ui-interface}

* Ao alternar da exibição Cartão para a exibição Lista em uma página de resultados de pesquisa, há um atraso antes que a página possa ser rolada (NPR-31286).

* A caixa de seleção Selecionar tudo fica oculta na exibição Lista na interface do usuário do Sites (NPR-31614).

* A contagem Selecionar tudo em uma página de resultados de pesquisa está incorreta (NPR-31120).

* O editor de metadados exibe tags que não existem (NPR-31119).

#### Tradução {#translation}

* Dois pop-ups de calendário são exibidos ao selecionar a opção Data de vencimento em um trabalho de tradução (NPR-31270).

#### Plataforma {#platform}

* A opção Mime type no console Web não funciona (NPR-31108).

* O certificado do cliente não é aceito ao configurar o logon único (NPR-31165).

* As atualizações na configuração de tamanho do buffer do serviço HTTP baseado em Java não são salvas (NPR-30925).

* O QueryBuilder agora suporta orderby ``fn:name()`` em consultas xpath (NPR-31322).

* A árvore de ativação duplicada é criada ao atualizar do AEM 6.3 (NPR-31513).

* As solicitações encaminhadas não preservam cabeçalhos de resposta que são definidos durante a autenticação Sling (NPR-30013).

* A pesquisa nos componentes do seletor não funciona (NPR-31692).

* Um erro é exibido ao anexar um arquivo ZIP a uma publicação do AEM Communities devido a diferentes versões do pacote Apache POI e Apache Tika (NPR-31018).

* O ``org.apache.sling.distribution.api`` pacote está oculto no gerenciador de configuração e, portanto, não está disponível para pacotes personalizados (NPR-31720).

#### Projetos {#projects}

* Alternar exibições de calendário não funciona (NPR-31271).

#### Brand Portal {#assets-brand-portal}

**Aprimoramentos do produto**

* O fluxo de trabalho de importação da Origem de ativos nos ativos AEM é modificado para buscar apenas os ativos recém-criados do Portal de marcas para o AEM e ignorar os ativos que já existem na nova pasta para evitar a replicação (CQ-4278527).

**Correções**

* O ícone incorreto é exibido ao criar uma nova pasta Contribuição no recurso Origem de ativos (CQ-4282825).
* Ao criar uma nova pasta de contribuição, uma ou ambas as subpastas (NOVO e COMPARTILHADO) não aparecem na pasta de contribuição (CQ-4282424).
* O sistema lança uma exceção se o usuário tentar publicar novamente a pasta Contribuição do AEM para o Brand Portal depois de receber novos recursos na pasta Contribuição do Portal de Marcas (CQ-4279740).
* A criação da pasta Contribuição em uma pasta Contribuição (pasta aninhada) é proibida para evitar a complexidade (CQ-4278391).
* O sistema lança uma exceção ao fazer upload da lista de usuários do Brand Portal (arquivo .csv) importada do Admin Console do AEM. Somente os campos Email, Nome e Sobrenome no arquivo .csv são obrigatórios (CQ-4278390).

#### Communities {#communities}

**Correções**

* Os links rápidos para gerenciar grupos (Abrir/Editar/Publicar/Excluir grupos) não estão visíveis para os administradores da Comunidade (Administrador de grupo/Administrador de site) (NPR-31627).
* Um blog enviado não é exibido, a menos que a página seja atualizada/recarregada manualmente (NPR-31599).
* A consulta JCR usada pelo recurso &quot;Menções&quot; diferencia maiúsculas de minúsculas e demora muito para retornar os resultados (NPR-31475).
* O arquivo UberJar do AEM 6.5 lança uma exceção, `cq-social-translation` pacote ausente do arquivo UberJar do AEM 6.5 (NPR-31186).
* As bibliotecas de Jackson Databind foram atualizadas para a versão 2.9.9.3 para endereçar novas vulnerabilidades (NPR-30967).
* Os títulos Atividades e Notificações são inconsistentes (NPR-30941).
* A paginação não funciona corretamente no Communities Blogs (NPR-30914).
* Os relatórios do Analytics não são preenchidos no ambiente de criação do AEM, uma página em branco é exibida (NPR-30913).

#### Oak {#oak}

* Atualizações de índice Lucene fazendo com que o servidor do autor fique lento (NPR-31548).

#### Forms {#forms-6530}

>[!NOTE]
>
>O AEM Service Pack não inclui correções para o AEM Forms. Eles são entregues usando um pacote complementar separado do Forms. Além disso, é lançado um instalador cumulativo que inclui correções para o AEM Forms no JEE. For more information, see [Install AEM Forms add-on](#install-aem-forms-add-on-package) and [Install AEM Forms on JEE](#install-aem-forms-jee-installer).

##### Pacote complementar do Forms {#forms-add-on-package-6530}

**Formulários adaptáveis**

* As strings contêm a chave do dicionário ao localizar formulários adaptáveis (NPR-31110).

**Comunicação interativa**

* **MissingNode.toString()** retorna resultados imprecisos após atualizar as bibliotecas Jackson para 2.10.0 (NPR-31549).

* O editor de texto remove aleatoriamente caracteres de espaço do texto copiado do Microsoft Word (NPR-31113).

**Gerenciamento de correspondência**

* As legendas e dicas de ferramentas não são exibidas ao migrar letras do LiveCycle ES4SP1 para o AEM 6.5 (NPR-31615).

* **A formatação do fluxo de texto não é mais exibida uma mensagem de erro compatível** ao salvar letras como rascunhos (NPR-30463).

**Fluxo de trabalho**

* O fluxo de trabalho do OSGi falha devido à utilização de 100% da CPU (NPR-31233).

**Formulários HTML5**

* Gerar a visualização HTML5 de um formulário XDP mostra uma oscilação ao adicionar instâncias de um formulário secundário (NPR-30909).

##### Formulários no instalador JEE {#forms-jee-installer-6530}

**Forms - Serviços de documentos**

* O serviço Web SOAP que usa MTOM em um projeto .NET exibe exceções para a chamada AssemblerServiceClient e métodos HtmlToPDF2 (NPR-4281771).

**Foundation JEE**

* A configuração de ação não carrega os nomes de processo para Chamar uma ação de envio do Forms Workflow (NPR-31478).
* Os usuários do AEM Forms em JEE encontram erros semelhantes aos seguintes ao importar arquivos .lca ou configurar o LDAP no console de administração:

   `com.ibm.ws.webcontainer.filter.FilterInstanceWrapper doFilter SRVE8109W: Uncaught exception thrown by filter um: java.lang.NoClassDefFoundError: org/apache/commons/io/IOUtils at org.apache.commons.fileupload.util.Streams.copy`

   `Error 500: javax.servlet.ServletException: java.lang.NoClassDefFoundError: org.apache.commons.io.IOUtils` (NPR-30931)


### Feature Packs incluídos {#feature-packs-included-6530}

>[!NOTE]
>
>Para clientes do AEM Forms, é essencial instalar o pacote complementar do AEM Forms após instalar qualquer Service Pack, Cumulative Fix Pack ou Feature Pack do AEM.

#### Forms - Foundation JEE {#forms-foundation-jee-feature}

* Suporte do AEM Forms para Oracle 18c (NPR-29155).

## Install 6.5.3.0 {#install}

**Requisitos de configuração**

* AEM 6.5.3.0 requires AEM 6.5. Check [upgrade documentation](/help/sites-deploying/upgrade.md) for detailed instructions.
* O download do Service Pack está disponível no Compartilhamento de pacotes da Adobe, que pode ser acessado diretamente da instância do AEM 6.5.
* Em uma implantação com MongoDB e várias instâncias, instale o AEM 6.5.3.0 em uma das instâncias do autor usando o Gerenciador de pacotes.
* Antes de instalar o Service pack, verifique se você tem um instantâneo ou um backup atualizado da sua instância do AEM.
* Reinicie a instância antes da instalação. Embora isso seja necessário apenas quando a instância ainda está no modo de atualização (e esse é o caso quando a instância foi atualizada de uma versão anterior), é recomendável se a instância estava em execução por um período mais longo.

>[!CAUTION]
>
>A Adobe não recomenda remover ou desinstalar o pacote AEM 6.5.3.0.

### Instalar o Service Pack por meio do Compartilhamento de pacotes {#install-service-pack-via-package-share}

Execute as seguintes etapas para instalar o Service Pack em uma instância do AEM 6.5 existente:

1. Login to Package Share from within AEM or directly from your browser and download the [AEM 6.5.3.0 package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.3.0).

1. Instale o pacote baixado usando o Gerenciador de pacotes.

>[!NOTE]
>
>**A caixa de diálogo na interface do usuário do Gerenciador de pacotes às vezes sai imediatamente durante a instalação da versão 6.5.3.0**
>
>Portanto, é recomendável aguardar a estabilização dos registros de erros antes de acessar a instância. O usuário deve aguardar os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações foram bem-sucedidas. Geralmente isso acontece no Safari, mas pode acontecer intermitentemente em qualquer navegador.

**Instalação automática**

Há duas maneiras de instalar automaticamente o AEM 6.5.3.0 em uma instância em execução:

A. Coloque a embalagem em ..*pasta /crx-quickstart/install* enquanto o servidor estiver disponível online. O pacote é instalado automaticamente.

B. Use the [HTTP API from Package Manager](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) - make sure that you use cmd=install&amp;recursive=true - so the nested packages  are  installed.

>[!NOTE]
>
>O AEM 6.5.3.0 não oferece suporte à instalação do Bootstrap.

**Validar instalação**

1. A página Informações do produto (/system/console/ productinfo) exibe a string da versão atualizada `Adobe Experience Manager, Version 6.5.3.0` em Produtos instalados.

1. All  OSGi  bundles are either **[!UICONTROL ACTIVE]** or **[!UICONTROL FRAGMENT]** in the OSGi Console (Use Web Console: /system/console/bundles).
1. O pacote OSGI org.apache.Jackrabbit.oak-core está na versão 1.10.6 ou superior (Use o console da Web: /system/console/bundles).

In order to see what platforms are certified to run with this release, please refer to the [Technical Requirements](/help/sites-deploying/technical-requirements.md).

### Install AEM Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Pule se você não estiver usando o AEM Forms. As correções do AEM Forms são entregues por meio de um pacote complementar separado.

>[!NOTE]
>
>AEM 6.5.3.0 includes a new version of [AEM Forms Compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT). Se você estiver usando uma versão mais antiga do pacote Compatibilidade com formulários AEM e estiver atualizando para o AEM 6.5.3.0, instale a versão mais recente do pacote Compatibilidade com formulários AEM após a instalação do Pacote complementar de formulários.

1. Verifique se você instalou o AEM Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

### Install AEM Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Pule se você não estiver usando o AEM Forms no JEE. Correções no AEM Forms em JEE são entregues por meio de um instalador separado.

For information about installing the cumulative installer for AEM Forms on JEE and post-deployment configuration, see the [release notes for patch 0007](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0007.html).

#### Instalador do Workbench

Como se trata de um instalador completo, o tamanho do arquivo é maior comparado à versão de correção. Desinstale a versão anterior do Workbench antes de instalar a nova.

## UberJar {#uber-jar}

The UberJar for AEM 6.5.3.0 is available in the [Adobe Public Maven repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.3/).

To use UberJar in a Maven project, refer to the article, [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.3.0</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## Recursos obsoletos {#removed-deprecated-features}

Esta seção lista os recursos e recursos que foram marcados como obsoletos com o AEM 6.5.3.0. Os recursos que estão planejados para serem removidos em uma versão futura são definidos como obsoletos primeiro, com uma opção alternativa a ser usada.

Recomenda-se que os clientes verifiquem se utilizam o recurso ou a capacidade na implantação atual e façam planos para alterar sua implementação para usar a opção alternativa.

| Área | Recurso | Substituição |
|---|---|---|
| Integrações | The **[!UICONTROL AEM Cloud Services Opt-In]** screen has been deprecated. Com a integração do AEM e do Target atualizada no AEM 6.5 para oferecer suporte à API do Target Standard, que usa autenticação por meio do Adobe IMS e E/S, e com a função crescente do Adobe Launch para instrumentar páginas do AEM para análise e personalização, o assistente de aceitação se tornou funcionalmente irrelevante. | Configurar conexões do sistema, autenticação do Adobe IMS e integrações de E/S da Adobe por meio dos respectivos serviços em nuvem do AEM |

## Problemas conhecidos {#known-issues}

* Se o assistente de configuração **de ativos** conectados retornar uma mensagem de erro 404 após a instalação do AEM 6.5.3.0, reinstale manualmente os pacotes **cq-remotedam-client-ui-content** e **cq-remotedam-client-ui-components** usando o Gerenciador de pacotes.
* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação do AEM 6.5.x.x:
   * &quot;Quando a integração do Target é configurada no AEM usando a API do Target Standard (autenticação IMS), a exportação de Fragmentos de experiência para o Target resulta na criação de tipos de ofertas incorretos. Em vez do tipo &quot;Fragmento de experiência&quot;/fonte &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/fonte &quot;Adobe Target Classic&quot;.
   * com.adobe.granite.manutenção.impl.TaskScheduler: nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * A validação do lado do servidor do Formulário adaptável falha quando funções agregadas, como SUM, MAX e MIN são usadas. CQ-4274424
   * com.adobe.granite.manutenção.impl.TaskScheduler: nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de banner de compra.

## Pacotes de conteúdo e pacotes OSGi incluídos {#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos no AEM 6.5.3.0

Lista de pacotes OSGi incluídos no AEM 6.5.3.0

[Obter arquivo](assets/6530_bundles.txt)

Lista de pacotes de conteúdo incluídos no AEM 6.5.3.0

[Obter arquivo](assets/sp_6530_packages.txt)

## Helpful Resources {#helpful-resources}

* [Notas de versão do AEM 6.5](/help/release-notes/release-notes.md)
* [Página do produto AEM](https://www.adobe.com/marketing/experience-manager.html)
* [Documentação do AEM 6.5](https://helpx.adobe.com/support/experience-manager/6-5.html)
* Subscribe to [Adobe priority product updates](https://www.adobe.com/subscription/priority-product-update.html)

## Sites restritos {#restricted-sites}

Estes sites estão disponíveis somente para clientes. Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)
* [Entre em contato com o suporte](https://daycare.day.com/public/contact.html)ao cliente Para obter mais informações sobre como acessar o portal de suporte, consulte [Acesso ao portal](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)de suporte.
