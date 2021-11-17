---
title: Configurar [!DNL Workfront for Experience Manager enhanced connector]
description: Configurar [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
source-git-commit: 8d39e1c86e5185a181400f10b7822a57c9d3aeae
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 0%

---


# Configurar [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

Um usuário com acesso de administrador em [!DNL Adobe Experience Manager] configura o conector aprimorado após instalá-lo. Para obter instruções de instalação, consulte [Instale o conector](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
>O Adobe requer implantação e configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector] somente por parceiros certificados ou [!DNL Adobe Professional Services]. Se implantado e configurado sem um parceiro certificado ou [!DNL Adobe Professional Services], ele não é compatível com o Adobe.
>
>O Adobe pode lançar atualizações para [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] que tornam redundante este conector; se isso ocorrer, os clientes podem ser solicitados a fazer a transição do uso desse conector.

## Configurar assinaturas de evento {#event-subscriptions}

As assinaturas de evento são usadas para notificar AEM de eventos que ocorrem em [!DNL Adobe Workfront]. Há três [!DNL Workfront for Experience Manager enhanced connector] recursos que precisam de assinaturas de evento para funcionarem, são:

* Criação automática de pastas vinculadas ao projeto.
* Sincronização de alterações nos valores de formulário personalizado do documento Workfront para AEM metadados de ativos.
* Publicação automática de ativos no Brand Portal após a conclusão do projeto.

Para usar esses recursos, ative assinaturas de evento.

* Editar [!UICONTROL Ferramentas Workfront] Configuração do Cloud Services criada na etapa 5 e selecione a variável [!UICONTROL Assinaturas do evento] guia .
* Selecione o [!UICONTROL Integração personalizada do Workfront] criado na seção 6.
* Clique em [!UICONTROL Ativar assinaturas de evento do Workfront].

   ![Subscrição do evento](/help/assets/assets/event-subs.png)

## Configurar pastas vinculadas {#linked-folders}

Para se inscrever nos eventos, siga estas etapas:

1. Navegue até o **[!UICONTROL Assinaturas do evento]** nos serviços em nuvem.
1. Selecione a integração personalizada criada em [!DNL Workfront].
1. Clique em **[!UICONTROL Ativar assinaturas de evento do Workfront]**.

### Configuração da estrutura de pastas vinculadas {#linked-folder-structure}

1. Vá para a guia Pastas vinculadas do projeto nos serviços de nuvem.
1. Caminho principal da pasta vinculada: Selecione uma pasta no DAM onde deseja criar as pastas vinculadas. Caso deixado em branco, o padrão será /content/dam. Certifique-se de que o esquema de metadados das Ferramentas do Workfront e o esquema de metadados da pasta de pastas vinculadas do Workfront tenham sido aplicados à pasta selecionada.
1. Estrutura de pastas vinculadas: Insira valores separados por vírgula. Cada valor deve ser `DE:<some-project-custom-form-field>`, Portfolio, Programa, Ano, Nome ou algum &quot;Valor de string literal&quot; (este último com aspas). Atualmente, está definido como Portfolio, Program, Year, DE:Project Type, Name.
1. Criar título de pasta vinculada no Workfront usando a caixa de seleção nomes da estrutura de pastas deve ser marcada se o título da pasta no Workfront deve incluir todas as pastas na estrutura. Caso contrário, será o título da última pasta.
1. Sub-pastas com vários campos permite especificar uma lista de pastas que devem ser criadas como uma pasta secundária da pasta vinculada.
1. Status do projeto: Selecione o status para o qual o projeto deve ser definido para criar a pasta vinculada.
1. Crie uma pasta vinculada em projetos com portfólio: Lista de Portfolio aos quais o projeto deve pertencer para criar a pasta vinculada. Deixe esta lista vazia para criar a pasta vinculada para todo o portfólio do projeto.
1. Crie uma pasta vinculada em projetos com o campo de formulário personalizado: Campo de formulário personalizado e seu valor correspondente que o projeto deve ter para criar a pasta vinculada. Essa configuração será ignorada se ficar vazia. Selecionar `CUSTOM FORMS: Create DAM Linked Folder` para o campo e a entrada `Yes` para o valor .
1. Clique em Habilitar criação automática de pastas vinculadas. Volte para a guia Subscriptions do evento e verá que agora há um evento create .

![configuração de pasta vinculada](/help/assets/assets/wf-linked-folder-config.png)

## Mapeamento do esquema de metadados {#metadata-schema-mapping}

### Configurar o mapeamento de metadados da pasta {#folder-metadata-mapping}

O mapeamento de metadados entre Projetos Workfront e Pastas AEM é definido nos Esquemas de metadados AEM pasta. Os Esquemas de Metadados da Pasta devem ser criados e configurados como de costume em AEM. As Ferramentas do Workfront adicionam uma lista suspensa de preenchimento automático à guia Configuração de cada campo de formulário de esquema de metadados de pasta. Esse menu suspenso de preenchimento automático permitirá especificar para qual campo do Workfront cada propriedade de pasta de AEM deve ser mapeada.

Para configurar os mapeamentos, siga estas etapas:

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados da pasta]**.
1. Selecione o formulário de esquema de metadados da pasta que deseja editar e clique em Editar.
1. Selecione o campo de formulário de esquema de metadados da pasta que você deseja editar e selecione a guia Configurações no painel direito.
1. Em [!UICONTROL Mapeado do campo Workfront] selecione o nome do campo Workfront que deseja mapear para a propriedade AEM folder selecionada. As opções disponíveis são:

   * Campos de formulário personalizado do projeto
   * Campos Visão geral do projeto (ID, Nome, Descrição, Número de referência, Data de conclusão planejada, Proprietário do projeto, Patrocinador do projeto, Portfolio ou Programa)

![configuração de mapeamento de metadados](/help/assets/assets/wf-metadata-mapping-config2.png)

### Configurar o mapeamento de metadados de ativos {#asset-metadata-mapping}

O mapeamento de metadados entre documentos e ativos do Adobe Workfront é definido nos Esquemas de metadados AEM. Os Esquemas de metadados devem ser criados e configurados como de costume no AEM. O Workfront Tools adiciona opções de configuração à guia Configuração de configurações de cada campo de formulário de esquema de metadados. Essas opções permitirão especificar para qual campo do Workfront cada propriedade AEM deve ser mapeada.

Para configurar os mapeamentos, siga estas etapas:

1. Navegar para **Ferramentas** > **Ativos** > **Esquemas de metadados**.
1. Selecione o formulário de esquema de metadados que deseja editar e clique em **Editar** ou criar um novo esquema de metadados do zero.
1. Selecione o campo de formulário de esquema de metadados que deseja editar e selecionar **Configurações** no painel direito.
1. Em [!DNL Workfront] Campo de formulário personalizado selecione o nome da variável [!DNL Workfront] campo que você deseja mapear para a propriedade AEM selecionada. As opções disponíveis são:

   * Campos de formulário personalizado do documento
   * Campos de formulário personalizado do projeto
   * Emitir campos de formulário personalizados
   * Campos de formulário personalizado da tarefa
   * Campos de Visão geral do projeto (ID, Nome, Descrição ou Número de referência)

1. No caso em que a variável [!DNL Workfront] campo selecionado em [!UICONTROL Campo de formulário personalizado do Workfront] for um campo do tipo Usuário do Workfront , será necessário especificar qual campo Usuário do Workfront deseja mapear. Para fazer isso, marque a opção Get value from Workfront referenced object e especifique o nome do objeto de referência do [!UICONTROL Campo de formulário personalizado do usuário do Workfront] do qual recuperar o valor a ser mapeado.

   ![configuração de mapeamento de metadados](/help/assets/assets/wf-metadata-mapping-config1.png)

## Propriedade do mapa {#map-property}

Essa etapa do fluxo de trabalho permite que um usuário mapeie uma propriedade para um [!DNL Workfront] formulário personalizado em um projeto, tarefa, problema ou documento. O [!DNL Workfront] o artefato que essa etapa afeta é pesquisado usando um caminho relativo da carga útil. As propriedades a serem mapeadas são controladas na configuração da caixa de diálogo de etapas.

**Tipo**: Este campo permite selecionar o tipo de objeto Workfront para o qual as propriedades devem ser mapeadas.

**Propriedade da ID**: Este campo permite especificar o caminho para a ID do objeto do Workfront para o qual as propriedades devem ser mapeadas. O caminho especificado neste campo deve ser relativo à carga do workflow.

**Atribuições de propriedade**: Esse multicampo permite especificar os mapeamentos entre AEM propriedades e campos Workfront. Cada item no multicampo especificará um mapeamento. Cada mapeamento deve ter o formato `<workfront-field>=<aem-mapped-property>`.

* O `workfront-field` pode ser

   * Um campo de formulário personalizado identificado pelo prefixo `DE:`.
   * Um campo editável identificado por seu nome. Os nomes dos campos são encontrados em [[!DNL Workfront] API Explorer](https://experience.workfront.com/s/api-explorer).

* O `aem-mapped-property` pode ser:

   * Um valor literal. Elas devem ser cercadas por aspas.
   * Uma propriedade AEM. Essa referência deve ser relativa à carga do workflow.
   * Um valor nomeado. Elas devem ser cercadas por colchetes.
   * Uma concatenação dos 3 itens acima. Especifique-o usando `{+}`.
   * Alteração dos 3 itens acima ao contornar o valor com `{replace(<value>,”old-char”,”new-char”)}`.

* Alguns exemplos:

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL=”https://my-aem-author/assets.html”{+}{path}`

![Configuração para mapear a propriedade](/help/assets/assets/wf-map-property-config.png)

## Definir status {#set-status}

No editor de fluxo de trabalho, edite as propriedades de **[!UICONTROL Workfront - Definir status]** no **[!UICONTROL Argumentos]** guia .

![Editar fluxo de trabalho para definir o status](/help/assets/assets/wf-set-status.png)

## Sincronização de comentários {#comments-sync}

1. Em [!DNL Experience Manager], acesso **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuração das ferramentas do Workfront]**, selecione a configuração e selecione **[!UICONTROL Propriedades]**.

   ![sincronização de comentários](/help/assets/assets/comments-sync1.png)

1. Selecionar **[!UICONTROL Assinaturas do evento]** clique em **[!UICONTROL Ativar Sincronização de Comentários]** on **[!UICONTROL Enviar comentários feitos no Workfront para o AEM]** opção.

   ![A sincronização está ativada](/help/assets/assets/wf-comment-sync-enabled.png)

Para testar a sincronização de comentários do Workfront com o AEM, siga estas etapas:

1. Navegue até um documento vinculado no Workfront e adicione um comentário na guia Atualizações .

   ![deixar comentário no Workfront](/help/assets/assets/comments-sync2.png)

1. Navegue até o mesmo documento vinculado em AEM, selecione o documento e abra o [!UICONTROL Linha do tempo] na navegação à esquerda e selecione [!UICONTROL Comentários]. A barra lateral esquerda exibe os comentários sincronizados da [!DNL Workfront].

## Versões de ativos {#asset-versions}

Para manter o histórico de versões de ativos no AEM, configure o controle de versão de ativos no AEM.

1. No Experience Manager, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuração das ferramentas do Workfront]** e abra o **[!UICONTROL Avançado]** guia .

1. Selecionar opção **[!UICONTROL Armazenar ativos com o mesmo nome das versões do ativo existente]**. Quando marcada, essa opção permite armazenar ativos carregados com o mesmo nome e no mesmo local da versão do ativo existente. Se deixado desmarcado, um novo ativo será criado com um nome diferente (por exemplo, `asset-name.pdf` e `asset-name-1.pdf`).

1. Selecionar opção **[!UICONTROL Atualizar metadados de ativos ao criar uma nova versão]**. Quando marcada, essa opção atualiza os metadados do ativo sempre que uma nova versão do ativo é criada. Se estiver desmarcado, o ativo manterá os metadados que tinha antes de criar a nova versão.

![configurar o controle de versão de ativos](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>O controle de versão não é compatível com pastas vinculadas. Ao criar um [!DNL Workfront] com um documento dentro de uma pasta vinculada, os comentários e anotações sobre a versão anterior do ativo são removidos.

## Anexar formulários personalizados {#attach-custom-forms}

Essa etapa de fluxo de trabalho permite que os usuários anexem um formulário personalizado a um [!DNL Workfront] artefato. Essa etapa do fluxo de trabalho pode ser adicionada a qualquer modelo de fluxo de trabalho. O [!DNL Workfront] O artefato que essa etapa afeta será pesquisado usando um caminho relativo da carga útil.

No editor de fluxo de trabalho no Experience Manager, edite as propriedades da [!UICONTROL Workfront - Anexar formulário personalizado] etapa do fluxo de trabalho.

![formulários personalizados](/help/assets/assets/wf-custom-forms.png).

## Publicar ativos automaticamente {#auto-publish-assets}

1. No Experience Manager, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuração das ferramentas do Workfront]** e abra o **[!UICONTROL Avançado]** guia .

1. Selecionar **[!UICONTROL Publicar automaticamente ativos quando enviados do Workfront]**. Essa opção permite a publicação automática de ativos quando eles são enviados do Workfront para o AEM. Esse recurso pode ser ativado condicionalmente especificando um campo de formulário personalizado Workfront e o valor ao qual deve ser definido. Sempre que um documento é enviado para o AEM, se ele atender a condição, o ativo será publicado automaticamente.

1. Selecionar **[!UICONTROL Publicar todos os ativos do projeto no Brand Portal após a conclusão do projeto]**. Essa opção permite a publicação automática de ativos para [!DNL Brand Portal] quando o status do projeto do Workfront ao qual eles pertencem for alterado para `Complete`.

![configurar a publicação automática](/help/assets/assets/wf-auto-publish-config.png)

## Atualizações de formulário personalizado do documento Workfront {#subscribe-workfront-doc-custom-form-updates}

Para assinar as alterações em [!DNL Workfront] formulários personalizados do documento, selecione a opção relevante na **[!UICONTROL Avançado]** guia . Ao assinar essas atualizações, ele atualiza o mapeado [!DNL Experience Manager] campos de metadados quando o campo correspondente em [!DNL Workfront] o formulário personalizado do documento foi alterado.

![Configuração de atualizações de formulário personalizadas do documento Workfront em [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
