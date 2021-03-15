---
title: '[!DNL Experience Manager] Notas de versão do service pack 6.5'
description: Notas de versão específicas do  [!DNL Adobe Experience Manager] 6.5 service pack 8
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 60764db23115e7f548a82a67955331da2b858973
workflow-type: tm+mt
source-wordcount: '2812'
ht-degree: 4%

---


# [!DNL Adobe Experience Manager] Notas de versão do service pack 6.5  {#aem-service-pack-release-notes}

## Informações da versão {#release-information}

| Produtos | [!DNL Adobe Experience Manager] 6,5 |
| -------- | ---------------------------- |
| Versão | 6.5.8.0 |
| Tipo | Lançamento do Service Pack |
| Data | 11 de março de 2021 |
| URL de download | [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## O que está incluído em [!DNL Adobe Experience Manager] 6.5.8.0 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] A versão 6.5.8.0 inclui novos recursos, principais melhorias solicitadas pelo cliente e melhorias de desempenho, estabilidade e segurança, lançadas desde a disponibilização da versão 6.5 em abril de 2019. O service pack é instalado em [!DNL Adobe Experience Manager] 6.5.

Os principais recursos e aprimoramentos introduzidos em [!DNL Adobe Experience Manager] 6.5.8.0 são:

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* Ao usar [a funcionalidade Ativos conectados](/help/assets/use-assets-across-connected-assets-instances.md), agora é possível visualizar uma lista de todas as páginas [!DNL Sites] que usam o ativo. Essas referências a um ativo estão disponíveis na página [!UICONTROL Propriedades] de um ativo. Isso permite que administradores, profissionais de marketing e bibliotecas tenham uma visão completa do uso dos ativos, permitindo um melhor rastreamento, gerenciamento e consistência da marca.

* Ao excluir um ativo referenciado em uma página da Web, [!DNL Experience Manager] [exibe um aviso](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references). É possível forçar a exclusão de um ativo referenciado ou verificar e modificar as referências exibidas na página [!DNL Properties] do ativo. Clicar nas referências abre as páginas [!DNL Sites] locais e remotas.

* Classificação das páginas da Live Copy disponíveis para implantação usando as propriedades [!UICONTROL Nome], [!UICONTROL Data da última modificação,] e [!UICONTROL Data da última implantação].

* O repositório integrado (Apache Jackrabbit Oak) foi atualizado para 1.22.6. <!-- TBD: Mention the version -->

Para obter uma lista completa dos recursos e aprimoramentos introduzidos em [!DNL Experience Manager] 6.5.8.0, consulte [novidades no [!DNL Adobe Experience Manager] 6.5 Service Pack 8](new-features-latest-service-pack.md).

Esta é a lista de correções fornecidas na versão [!DNL Experience Manager] 6.5.8.0.

### [!DNL Sites] {#sites-6580}

* Quando uma página é movida para o blueprint, o destino dos links não é atualizado (NPR-35724).
* O reprodutor baseado em Tizen não é autenticado em determinados navegadores. O problema ocorre em navegadores que não aceitam o atributo samesite=none (NPR-35589).
* Um contêiner responsivo desbloqueado não exibe componentes permitidos (NPR-35565).
* Ao criar uma live copy de uma página recém-adicionada, o idioma principal cria duas cópias para cada domínio (NPR-35545).
* Deadlock no Registro do Componente SCR quando muitos threads são bloqueados devido ao temporizador `org.apache.felix.scr.impl.ComponentRegistry`. Como resultado, [!DNL Experience Manager] pára de responder por um tempo indefinido (GRANITE-33125,FELIX-6252).
* Quando você pesquisa um ativo específico no painel lateral, o resultado contém alguns ativos não pesquisados (NPR-35524).
* Ao ativar o SSL para uma instância do Experience Manager, o caminho do contexto é removido (NPR-35477).
* Ao criar uma lista, adicionar texto como o primeiro elemento, adicionar uma tabela como o segundo elemento e adicionar uma lista dentro da tabela, a lista pai distorce (NPR-35465).
* Quando você usa plug-ins diferentes em itens de lista consecutivos, uma tag <br> extra é adicionada aos itens da lista (NPR-35464).
* Quando uma lista é colocada entre dois parágrafos, não é possível adicionar uma tabela à lista (NPR-35356).
* Quando você inicia uma atualização de instância de AEM do AEM 6.3 para o AEM 6.5, a instância de atualização demora mais para ser iniciada (NPR-35323).
* Ao replicar um ativo de AEM que inclui um colchete (). no nome, a replicação falha (GRANITE-27004, NPR-35315).
* Quando você adiciona cabeçalhos a um Editor de Rich Text, o botão de parágrafo é desativado (NPR-35256).
* Quando você adiciona um item a uma lista existente, ele exclui a lista de opções ou que pode ser recolhida (NPR-35206).
* Quando a opção Rollout page é selecionada, uma caixa de diálogo com todas as live copies disponíveis é exibida e a implantação automática ocorre. As cópias ao vivo das páginas são distribuídas para todas as regiões geográficas sem ação do usuário (NPR-35138).
* Ao usar a opção incluir filhos, a opção Gerenciar publicação não lista todas as páginas. Apenas 22 páginas estão listadas (NPR-35086).
* Quando uma política é editada, o componente de texto não retém as alterações de política (NPR-35070).
* Ao recuar alguns itens em uma lista numerada, todos os itens mantêm o mesmo número, embora a numeração deva começar de 1 para itens com o mesmo recuo (CQ-4313011).
* Quando a minificação estiver ativada, você não poderá editar nenhuma página ou componente. Os problemas começaram após a instalação do AEM 6.5 Service Pack 7 (CQ-4311133).
* A pesquisa Omni e os filtros de ativos retornam irrelevantes ou nenhum resultado (CQ-4312322, NPR-35793).
* Quando várias páginas acessam simultaneamente uma biblioteca do cliente, o gerenciador da biblioteca HTML falha ao carregar a biblioteca do cliente. Isso leva à renderização incorreta das páginas (NPR-35538).
* O caminho de contexto é removido automaticamente ao configurar um SSL em [!DNL Experience Manager] (NPR-35294).
* O gerenciador de pacotes não desconecta os usuários depois de clicar na opção Logout (NPR-35160).

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] A versão 6.5.8.0  [!DNL Assets] corrige os seguintes problemas e oferece os seguintes aprimoramentos.

* Ao restaurar uma versão anterior de um ativo, o evento DamEvent.Type RESTORED não é acionado no console OSGi (NPR-35789).
* `IndexWriter.merge` causa  `OutOfMemoryError` erro, pois a funcionalidade de marcação inteligente cria grandes  `/oak:index/lucene` e  `/oak:index/ntBaseLucene` índices (NPR-35651).
* Uma mensagem de erro é exibida ao tentar salvar uma pasta do tipo [!UICONTROL Contribuição do ativo] com caracteres multibyte no nome (NPR-35605).
* Quando campos de subtipo de metadados em cascata são usados, ocorre um erro incorreto de &quot;Preencha este campo&quot; (NPR-35643).
* Quando um ativo existente é arrastado na interface do usuário [!DNL Assets] e uma nova versão é criada, as alterações nos metadados não são persistentes (NPR-34940).
* Ao criar regras no editor de esquema de metadados para um menu em cascata, a opção [!UICONTROL Dependant On] repete o mesmo nome (NPR-35596).
* A pesquisa de similaridade não funciona após editar [!UICONTROL Painel de pesquisa do administrador de ativos] (NPR-35588).
* Em uma pasta, se você abrir a pesquisa de ativos no painel à esquerda clicando em [!UICONTROL Filtro], o filtro em [!UICONTROL Status] > [!UICONTROL Check-out] > [!UICONTROL Check-out] não funcionará (NPR-35530).
* Se você tentar excluir todas as Tags inteligentes de um ativo e salvar as alterações, as tags não serão removidas. No entanto, a interface do usuário indica que as alterações foram salvas (NPR-35519).
* Os usuários não podem reorganizar ou classificar ativos na exibição em lista em uma pasta que pode ser solicitada (NPR-35516).
* Se você editar o esquema de metadados padrão, o campo de tags na página [!UICONTROL Propriedades] do ativo será alterado para um campo de texto. A alteração permite que usuários não conscientes adicionem tags sob demanda e as tags são armazenadas como uma string no repositório (NPR-35478).
* Ao baixar um ativo, se você fornecer um nome que não tenha um endereço de email válido, a opção de download ficará indisponível. No entanto, se outra opção na caixa de diálogo de download for selecionada, o botão será ativado, mas um email não será enviado (NPR-35365).
* Os usuários não podem fazer check-in de ativos depois de editá-los em [!DNL Adobe InDesign] e receber um erro sobre falta de permissões (NPR-35341).
* A biblioteca JavaScript do Handlebars é atualizada à v4.7.6 (NPR-35333).
* A interface do editor de metadados para de funcionar conforme esperado ao iniciar a partir de itens de edição e cancelamento de seleção de metadados em massa até que um único item permaneça selecionado (NPR-35144).
* A navegação global não abre o console correto quando clicado de dentro da página `assets.html` (CQ-4312311).
* [!DNL Assets] não exibe a representação RGB de um ativo que tenha a representação RGB (CQ-4310190).
* A opção [!UICONTROL Relate] no menu não é exibida corretamente na página [!UICONTROL Propriedades] (CQ-4310188).
* Se o filtro de tipo de arquivo para documentos for usado para pesquisar ativos e criar uma coleção inteligente, o filtro não será aplicado quando a coleção for acessada. Em vez disso, todos os tipos de ativos são exibidos na pesquisa (NPR-35759).
* Não é possível arrastar e adicionar ativos em um Lightbox da interface do usuário [!DNL Assets] (NPR-35901).
* Quando uma nova versão de um ativo existente é criada após resolver o conflito de nomes, os metadados do ativo original são substituídos (CQ-4313594).
* Ao filtrar a pesquisa de ativos por meio de um filtro de pesquisa ou predicado, abrir um ativo para exibi-lo ou editá-lo e voltar à página de resultados da pesquisa, o filtro não funcionará. Todos os ativos pesquisados são listados como não filtrados (NPR-35913).

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* A opção URL da predefinição de imagem RESS é ativada na página de detalhes do ativo. Agora, as opções de URL e RESS estão disponíveis na página de detalhes do ativo quando a predefinição de imagem RESS é selecionada na seção representações dinâmicas . (CQ-4311241)
* Componente de mídia interativa - o vídeo interativo não funcionará se o usuário tiver [!DNL Experience Manager] com configuração de publicação seletiva (CQ-4311054).
* Se você mover ativos entre pastas, a sincronização entre [!DNL Experience Manager] e [!DNL Dynamic Media–Scene7] por meio da API será muito lenta (CQ-4310001).
* Ao usar o Omnisearch, o tamanho dos logs aumenta significativamente (CQ-4309153).
* Quando a sincronização seletiva está ativada e um ativo é copiado (não movido) para uma pasta de sincronização, ele não sincroniza como esperado (CQ-4307122).
* Para ativos carregados que são publicados automaticamente no DM, o status não exibe Publicado no AEM. Além disso, a coluna Dynamic Media Publish status não mostra o status publicado correto (CQ-4306415).
* Se um ativo for publicado em [!DNL Experience Manager] e estiver definido para publicar em [!DNL Dynamic Media] na ativação, o valor de metadados `scene7FileStatus` não será atualizado conforme esperado (CQ-4308269).
* Ao editar o perfil de vídeo, [!DNL Experience Manager] não exibe os valores de altura e taxa de bits definidos para a predefinição de vídeo. Os campos aparecem em branco (CQ-4311828).

### [!DNL Commerce] {#commerce-6580}

* Não é possível criar uma tag personalizada para todos os produtos no Commerce (CQ-4310682).

* A atualização de referência de ativo do produto faz com que os threads de replicação estejam no estado de espera até que o thread ProductAssetListener complete seus compromissos com o JCR (NPR-35269).

### Plataforma {#platform-6580}

* Quando você usa um componente Exibição de guia do Coral sem guias e, em seguida, aciona um validador do Foundation, ocorre o seguinte erro (NPR-35636):

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* A replicação de encaminhamento do SCD falha para eventos de exclusão para nós que incluem uma vírgula no nome (NPR-35191).

* Após a atualização para o AEM 6.5.7, as builds começam a falhar. O motivo é, uma versão antiga ou nenhum jackson-core é incorporado no uber-jar (GRANITE-33006).

### Interface do usuário {#ui-6580}

* Ao alternar da exibição Cartão para a exibição em Lista de documentos em uma pasta no console Ativos, a classificação não funciona adequadamente (NPR-35842).

* Quando você faz o hiperlink do texto em um componente de texto, o recurso de pesquisa não exibe os resultados apropriados (NPR-35849).

* Quando um valor não é fornecido a um campo oculto marcado como obrigatório, ele o impede de salvar um componente (NPR-35219).

### Integrações {#integrations-6580}

* Quando você usa valores diferentes para ID de locatário IMS e código de cliente do Target, [!DNL Experience Manager] falha ao integrar com [!DNL Adobe Target] (NPR-35342).

### Projetos de tradução {#translation-6580}

* Problemas ao exportar ou importar um trabalho de tradução em [!DNL Experience Manager] (NPR-35259).

### Campanha {#campaign-6580}

* Ao criar uma página de campanha usando um modelo pronto para uso na interface do usuário de toque e abrir a guia Email na caixa de diálogo de propriedades da página, a variável de personalização dos campos de assunto e corpo permanece desativada (CQ-4312388).

### [!DNL Communities] {#communities-6580}

* Ao adicionar uma estrutura de página a um grupo da comunidade, o título do [!UICONTROL Group] na navegação estrutural é alterado para o título da primeira [!UICONTROL Page] (NPR-35803).
* Ao contrário dos moderadores, um membro padrão da comunidade não pode acessar e editar nenhuma publicação de rascunho (NPR-35339).
* Controle de acesso quebrado e negação de serviço com DSRPReindexServlet, o que faz com que o site das comunidades fique inativo até que a indexação seja concluída (NPR-35591).
* Remover [!UICONTROL Todos os Usuários] do campo [!UICONTROL Administradores] não os remove realmente do back-end (NPR-35592, NPR-35611).
* O componente [!UICONTROL Compor mensagem] não retorna nenhum resultado quando o texto inserido é uma correspondência parcial (NPR-35666).

### [!DNL Brand Portal] {#brandportal-6580}

* Adicionar um membro a uma pasta do tipo [!UICONTROL Contribuição de ativos] mostra a legenda [!UICONTROL Adicionar usuário ou grupo] na interface do usuário, embora somente os usuários ativos do Brand Portal sejam suportados e não grupos (NPR-35332).

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>O [!DNL Experience Manager Forms] lança os pacotes complementares uma semana após a data programada de lançamento do [!DNL Experience Manager] Service Pack.

Para obter informações sobre atualizações de segurança, consulte a página [Boletins de segurança do Experience Manager](https://helpx.adobe.com/security/products/experience-manager.html).

## Instalar 6.5.8.0 {#install}

**Requisitos de configuração e mais informações**

* O Experience Manager 6.5.8.0 requer o Experience Manager 6.5. Consulte a [documentação de atualização](/help/sites-deploying/upgrade.md) para obter instruções detalhadas.
* O download do service pack está disponível no Adobe [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* Em uma implantação com MongoDB e várias instâncias, instale o Experience Manager 6.5.8.0 em uma das instâncias do autor usando o Gerenciador de pacotes.

>[!NOTE]
>
>O Adobe não recomenda remover ou desinstalar o pacote [!DNL Adobe Experience Manager] 6.5.8.0.

### Instale o service pack {#install-service-pack}

Para instalar o service pack em uma instância [!DNL Adobe Experience Manager] 6.5, siga estas etapas:

1. Reinicie a instância antes da instalação se a instância estiver no modo de atualização (e esse é o caso quando a instância foi atualizada de uma versão anterior). O Adobe também recomenda uma reinicialização se o tempo de atividade atual de uma instância for alto.

1. Antes de instalar, faça um instantâneo ou um novo backup da sua instância [!DNL Experience Manager].

1. Baixe o service pack de [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip).

1. Abra Gerenciador de pacotes e clique em **[!UICONTROL Fazer upload de pacote]** para fazer upload do pacote. Para saber mais, consulte [Gerenciador de Pacotes](/help/sites-administering/package-manager.md).

1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

1. Para atualizar o conector S3, pare a instância após a instalação do Service Pack, substitua o conector existente por um novo arquivo binário fornecido na pasta de instalação e reinicie a instância. Consulte [Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>A caixa de diálogo na interface do usuário do Gerenciador de Pacotes às vezes sai durante a instalação do service pack. O Adobe recomenda que você aguarde a estabilização dos registros de erros antes de acessar a implantação. Aguarde os registros específicos relacionados à desinstalação do pacote do atualizador antes de ter certeza de que as instalações foram bem-sucedidas. Normalmente, isso acontece em [!DNL Safari], mas pode acontecer intermitentemente em qualquer navegador.

**Instalação automática**

Há duas maneiras de instalar automaticamente o Adobe Experience Manager 6.5.8.0 em uma instância de trabalho:

A. Coloque o pacote na pasta `../crx-quickstart/install` quando o servidor estiver disponível online. O pacote é instalado automaticamente.

B. Use a API HTTP [do Gerenciador de Pacotes](/help/sites-administering/package-manager.md#package-share). Use `cmd=install&recursive=true` para que os pacotes aninhados sejam instalados.

>[!NOTE]
>
>O Adobe Experience Manager 6.5.8.0 não suporta a instalação do Bootstrap.

**Validar instalação**

1. A página de informações do produto (`/system/console/productinfo`) exibe a cadeia de caracteres de versão atualizada `Adobe Experience Manager (6.5.8.0)` em [!UICONTROL Produtos instalados].

1. Todos os pacotes OSGi são **[!UICONTROL ATIVE]** ou **[!UICONTROL FRAGMENTO]** no Console OSGi (Use o Console da Web: `/system/console/bundles`).

1. O pacote OSGi `org.apache.jackrabbit.oak-core` é da versão 1.22.3 ou posterior (Use o Console da Web: `/system/console/bundles`).

Para conhecer as plataformas certificadas para funcionar com esta versão, consulte os [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

### UberJar {#uber-jar}

O UberJar para Experience Manager 6.5.8.0 está disponível no [Repositório Central Maven](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.8/).

Para usar o UberJar em um projeto Maven, consulte [como usar o UberJar](/help/sites-developing/ht-projects-maven.md) e inclua a seguinte dependência no POM do projeto:

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.8</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>O UberJar e os outros artefatos relacionados estão disponíveis no Repositório Central Maven em vez do repositório Maven Adobe Public (`repo.adobe.com`). O arquivo UberJar principal é renomeado para `uber-jar-<version>.jar`. Portanto, não há `classifier`, com `apis` como o valor, para a tag `dependency`.

## Recursos obsoletos {#removed-deprecated-features}

Abaixo está uma lista de recursos e funcionalidades marcados como obsoletos com [!DNL Experience Manager] 6.5.7.0. Os recursos são marcados como obsoletos inicialmente e posteriormente removidos em uma versão futura. Geralmente, uma opção alternativa é fornecida.

Revise se você usa um recurso ou um recurso em uma implantação. Além disso, planeje alterar a implementação para usar uma opção alternativa.

| Área | Recurso | Substituição |
|---|---|---|
| Integrações | A tela de aceitação **[!UICONTROL AEM Cloud Services]** está obsoleta. Com a integração do Experience Manager e do Adobe Target atualizada no Experience Manager 6.5 para oferecer suporte à API do Adobe Target Standard, que usa autenticação via Adobe IMS e E/S, e com a função crescente do Adobe Launch para instrumentar páginas Experience Manager para análise e personalização, o assistente de aceitação se tornou funcionalmente irrelevante. | Configure conexões do sistema, autenticação Adobe IMS e [!DNL Adobe I/O] integrações por meio dos respectivos serviços de nuvem do Experience Manager. |
| Conectores | O Conector Adobe JCR para Microsoft SharePoint 2010 e Microsoft SharePoint 2013 está obsoleto para o Experience Manager 6.5. | N/A |

## Problemas conhecidos {#known-issues}

* Se estiver atualizando sua instância [!DNL Experience Manager] da versão 6.5 para a 6.5.8.0, você poderá visualizar as exceções `RRD4JReporter` no arquivo `error.log`. Reinicie a instância para resolver o problema.

* Se você instalar o [!DNL Experience Manager] 6.5 Service Pack 5 ou um service pack anterior no [!DNL Experience Manager] 6.5, a cópia em tempo de execução do modelo de fluxo de trabalho personalizado de ativos (criado em `/var/workflow/models/dam`) será excluída.
Para recuperar a cópia de tempo de execução, o Adobe recomenda sincronizar a cópia de tempo de design do modelo de fluxo de trabalho personalizado com a cópia de tempo de execução usando a API HTTP:
   `<designModelPath>/jcr:content.generate.json`.

* Entre em contato com o Atendimento ao cliente do Adobe em caso de problemas ao editar e criar regras em cascata no [!UICONTROL Editor do Forms do Esquema de Metadados da Pasta] e [!UICONTROL Editor do Forms do Esquema de Metadados] usando a caixa de diálogo [!UICONTROL Definir Regra]. As regras que já foram criadas e salvas estão funcionando como esperado.

* Se uma pasta na hierarquia for renomeada em [!DNL Experience Manager Assets] e a pasta aninhada contendo um ativo for publicada em [!DNL Brand Portal], o título da pasta não será atualizado em [!DNL Brand Portal] até que a pasta raiz seja publicada novamente.

* Quando um usuário seleciona configurar um campo pela primeira vez em um formulário adaptável, a opção para salvar uma configuração não é exibida no Navegador de propriedades. Selecionar para configurar outro campo do formulário adaptável no mesmo editor resolve o problema.

* Se o assistente [!UICONTROL Connected assets configuration] retornar uma mensagem de erro 404 após a instalação, reinstale manualmente os pacotes `cq-remotedam-client-ui-content` e `cq-remotedam-client-ui-components` usando o Gerenciador de pacotes.

* Os seguintes erros e mensagens de aviso podem ser exibidos durante a instalação do Experience Manager 6.5.x.x:
   * &quot;Quando a integração do Adobe Target é configurada no Experience Manager usando a API do Target Standard (autenticação IMS), a exportação dos Fragmentos de experiência para o Target resulta na criação de tipos de ofertas incorretos. Em vez do tipo &quot;Fragmento de experiência&quot;/fonte &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/fonte &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`: Nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * A validação do lado do servidor do Adaptive Form falha quando funções agregadas como SUM, MAX e MIN são usadas. CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` - Nenhuma janela de manutenção encontrada em granite/operations/maintenance.
   * O ponto de acesso em uma imagem interativa do Dynamic Media não é visível ao visualizar o ativo por meio do visualizador de Banner de compra.

## Pacotes de conteúdo e pacotes OSGi incluídos {#osgi-bundles-and-content-packages-included}

Os seguintes documentos de texto listam os pacotes OSGi e os Pacotes de conteúdo incluídos em [!DNL Experience Manager] 6.5.8.0:

* [Lista de pacotes OSGi incluídos no Experience Manager 6.5.8.0](assets/6580_bundles.txt)

* [Lista de pacotes de conteúdo incluídos na Experience Manager 6.5.8.0](assets/6580_packages.txt)

## Sites restritos {#restricted-sites}

Esses sites só estão disponíveis para clientes do . Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)
* Consulte [como entrar em contato com o Atendimento ao Cliente do Adobe](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] Notas de versão 6.5](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] página do produto](https://www.adobe.com/br/marketing/experience-manager.html)
>* [[!DNL Experience Manager] Documentação 6.5](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR)
>* [Inscreva-se em Atualizações de produtos de prioridade da Adobe](https://www.adobe.com/subscription/priority-product-update.html)

