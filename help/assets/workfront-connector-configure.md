---
title: Configurar o [!DNL Workfront for Experience Manager enhanced connector]
description: Configurar o [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Integrations
exl-id: 2660de7c-0281-4884-98d9-e78f20cf571c
hide: true
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1723'
ht-degree: 1%

---

# Configurar o [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-configure.html?lang=en) |
| AEM 6.5 | Este artigo |

Um usuário com acesso de administrador no [!DNL Adobe Experience Manager] configura o conector aprimorado após a instalação. Para obter instruções de instalação, consulte [Instale o conector](/help/assets/workfront-integrations.md).

>[!IMPORTANT]
>
>* O Adobe exige a implantação e a configuração do [!DNL Adobe Workfront for Experience Manager enhanced connector] somente por meio de parceiros certificados ou [!DNL Adobe Professional Services]. Se implantado e configurado sem um parceiro certificado ou [!DNL Adobe Professional Services], não é compatível com o Adobe.
>
>* O Adobe pode lançar atualizações para [!DNL Adobe Workfront] e [!DNL Adobe Experience Manager] que tornam esse conector redundante; se isso ocorrer, pode ser necessário que os clientes façam a transição do uso desse conector.
>
>* O Adobe suporta o conector aprimorado versões 1.7.4 e superiores. As versões anteriores de pré-lançamento e personalizadas não são compatíveis. Para verificar a versão aprimorada do conector, navegue até a `digital.hoodoo` grupo disponível no painel esquerdo no [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR).
>
>* Consulte [Exame de certificação de parceiros para o conector aprimorado do Workfront for Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obter informações sobre o exame, consulte [Guia do exame](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Configurar assinaturas de evento {#event-subscriptions}

Assinaturas de eventos são usadas para notificar o AEM sobre eventos que ocorrem em [!DNL Adobe Workfront]. Há três [!DNL Workfront for Experience Manager enhanced connector] recursos que precisam de assinaturas de evento para funcionar:

* Criação automática de pastas vinculadas ao projeto.
* Sincronização de alterações nos valores de formulário personalizado do documento do Workfront com os metadados de ativos AEM.
* Publicação automática de ativos no Brand Portal após a conclusão do projeto.

Para usar esses recursos, habilite as assinaturas de evento.

* Editar [!UICONTROL Ferramentas do Workfront] configuração do Cloud Service que você criou na etapa 5 e selecione a variável [!UICONTROL Inscrições em eventos] guia.
* Selecione o [!UICONTROL Integração personalizada do Workfront] você criou na seção 6.
* Clique em [!UICONTROL Ativar assinaturas de evento do Workfront].

  ![Assinatura do evento](/help/assets/assets/event-subs.png)

## Configurar pastas vinculadas {#linked-folders}

Para se inscrever nos eventos, siga estas etapas:

1. Navegue até a **[!UICONTROL Inscrições em eventos]** nos serviços em nuvem.
1. Selecione a integração personalizada criada em [!DNL Workfront].
1. Clique em **[!UICONTROL Ativar assinaturas de evento do Workfront]**.

### Configuração da estrutura de pastas vinculada {#linked-folder-structure}

1. Acesse a guia Pastas vinculadas do projeto nos serviços em nuvem.
1. Caminho principal da pasta vinculada: selecione uma pasta no DAM onde deseja criar as pastas vinculadas. Se deixado em branco, o padrão será /content/dam. Verifique se o esquema de metadados das Ferramentas do Workfront e o esquema de metadados da pasta vinculada do Workfront foram aplicados à pasta selecionada.
1. Estrutura de pasta vinculada: insira valores separados por vírgula. Cada valor deve ser `DE:<some-project-custom-form-field>`, Portfolio, Programa, Ano, Nome ou algum &quot;Valor de string literal&quot; (este último com aspas). No momento, está definido como Portfolio, Program, Year, DE:Project Type, Name.
1. Criar título de pasta vinculado no Workfront usando a caixa de seleção de nomes de estrutura de pastas deve ser marcada se o título da pasta no Workfront deve incluir todas as pastas na estrutura. Caso contrário, será o título da última pasta.
1. Sub-folders multifield permite especificar uma lista de pastas que devem ser criadas como uma pasta filho da pasta vinculada.
1. Status do projeto: selecione o status do projeto para criar a pasta vinculada.
1. Criar uma pasta vinculada em projetos com portfólio: lista de Portfolio aos quais o projeto deve pertencer para criar a pasta vinculada. Deixe essa lista vazia para criar a pasta vinculada para todos os portfólios de projetos.
1. Criar uma pasta vinculada em projetos com campo de formulário personalizado: o campo de formulário personalizado e seu valor correspondente que o projeto deve ter para criar a pasta vinculada. Essa configuração será ignorada se for deixada vazia. Selecionar `CUSTOM FORMS: Create DAM Linked Folder` para o campo e a entrada `Yes` para o valor.
1. Clique em Habilitar criação automática de pastas vinculadas. Volte para a guia Inscrições em eventos e você verá que agora há um evento de criação.

![configuração de pasta vinculada](/help/assets/assets/wf-linked-folder-config.png)

## Mapeamento de esquema de metadados {#metadata-schema-mapping}

### Configurar mapeamento de metadados da pasta {#folder-metadata-mapping}

O mapeamento de metadados entre Projetos Workfront e Pastas AEM é definido nos Esquemas de metadados da pasta AEM. Os esquemas de metadados de pasta devem ser criados e configurados como de costume no AEM. O Workfront Tools adiciona uma lista suspensa de preenchimento automático à guia Configurações de cada campo de formulário de esquema de metadados de pasta. Esse menu suspenso de preenchimento automático permite especificar para qual campo do Workfront cada propriedade da pasta AEM deve ser mapeada.

Para configurar os mapeamentos, siga estas etapas:

1. Adicionar `jcr:read` permissões para `/conf/global/settings/dam/adminui-extension/foldermetadataschema` para `wf-workfront-users` grupo.
1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadados de pasta]**.
1. Selecione o formulário de esquema de metadados da pasta que deseja editar e clique em Editar.
1. Selecione o campo de formulário de esquema de metadados da pasta que deseja editar e selecione a guia Configurações no painel direito.
1. Entrada [!UICONTROL Mapeado do campo do Workfront] selecione o nome do campo do Workfront que deseja mapear para a propriedade da pasta AEM selecionada. As opções disponíveis são:

   * Campos de formulário personalizado do projeto
   * Campos de visão geral do projeto (ID, Nome, Descrição, Número de referência, Data de conclusão planejada, Proprietário do projeto, Patrocinador do projeto, Portfolio ou Programa)

![configuração de mapeamento de metadados](/help/assets/assets/wf-metadata-mapping-config2.png)

### Configurar o mapeamento de metadados de ativos {#asset-metadata-mapping}

O mapeamento de metadados entre documentos e ativos do Adobe Workfront é definido em esquemas de metadados AEM. Os esquemas de metadados devem ser criados e configurados como de costume no AEM. O Workfront Tools adiciona opções de configuração à guia Configurações de cada campo de formulário de esquema de metadados. Essas opções permitirão especificar para qual campo do Workfront cada propriedade AEM deve ser mapeada.

Para configurar os mapeamentos, siga estas etapas:

1. Navegue até **Ferramentas** > **Assets** > **Esquemas de metadados**.
1. Selecione o formulário de esquema de metadados que deseja editar e clique em **Editar** ou crie um esquema de metadados do zero.
1. Selecione o campo de formulário de esquema de metadados que deseja editar e selecione **Configurações** no painel direito.
1. Entrada [!DNL Workfront] Campo de formulário personalizado selecione o nome do [!DNL Workfront] que você deseja mapear para a propriedade AEM selecionada. As opções disponíveis são:

   * Campos de formulário personalizado de documento
   * Campos de formulário personalizado do projeto
   * Emitir campos de formulário personalizados
   * Campos de formulário personalizado de tarefa
   * Campos de Visão Geral do Projeto (ID, Nome, Descrição ou Número de Referência)

1. No caso de a [!DNL Workfront] campo selecionado em [!UICONTROL Campo de formulário personalizado do Workfront] for um campo de tipo antecipado do usuário do Workfront, será necessário especificar qual campo do usuário do Workfront você deseja mapear. Para fazer isso, marque o campo Get value from Workfront referenced object e especifique o nome do [!UICONTROL Campo de formulário personalizado do usuário do Workfront] do qual recuperar o valor a ser mapeado.

   ![configuração de mapeamento de metadados](/help/assets/assets/wf-metadata-mapping-config1.png)

## Mapear propriedade {#map-property}

Esta etapa do fluxo de trabalho permite que um usuário mapeie uma propriedade para uma [!DNL Workfront] formulário personalizado em um projeto, tarefa, problema ou documento. A variável [!DNL Workfront] o artefato que essa etapa afeta é pesquisado usando um caminho relativo da carga. As propriedades a serem mapeadas são controladas na configuração da caixa de diálogo de etapas.

**Tipo**: este campo permite selecionar o tipo de objeto do Workfront para o qual as propriedades devem ser mapeadas.

**Propriedade de ID**: este campo permite especificar o caminho para a ID do objeto do Workfront para o qual as propriedades devem ser mapeadas. O caminho especificado neste campo deve ser relativo à carga do fluxo de trabalho.

**Atribuições de propriedade**: esse multicampo permite especificar os mapeamentos entre as propriedades do AEM e os campos do Workfront. Cada item no multicampo especificará um mapeamento. Cada mapeamento deve ter o formato `<workfront-field>=<aem-mapped-property>`.

* A variável `workfront-field` pode ser

   * Um campo de formulário personalizado identificado pelo prefixo `DE:`.
   * Um campo editável identificado por seu nome. Os nomes de campos são encontrados em [[!DNL Workfront] explorador de API](https://experience.workfront.com/s/api-explorer).

* A variável `aem-mapped-property` pode ser:

   * Um valor literal. Elas devem estar entre aspas.
   * Uma propriedade do AEM. Essa referência deve ser relativa à carga do workflow.
   * Um valor nomeado. Eles devem estar entre colchetes.
   * Uma concatenação dos 3 itens acima. Especifique-o usando `{+}`.
   * Uma alteração dos 3 itens acima ao envolver o valor com `{replace(<value>,"old-char","new-char")}`.

* Alguns exemplos são:

   * `status="INP"`
   * `DE:Asset Type=jcr:content/metadata/assetType`
   * `DE:Path={path}`
   * `URL="https://my-aem-author/assets.html"{+}{path}`

![Configuração para mapear a propriedade](/help/assets/assets/wf-map-property-config.png)

## Definir status {#set-status}

No editor de workflow, edite as propriedades de **[!UICONTROL Workfront - Definir status]** no **[!UICONTROL Argumentos]** guia.

![Editar fluxo de trabalho para definir status](/help/assets/assets/wf-set-status.png)

## Sincronização de comentários {#comments-sync}

1. Entrada [!DNL Experience Manager], acesso **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configuração de ferramentas do Workfront]**, selecione a configuração e selecione **[!UICONTROL Propriedades]**.

   ![sincronização de comentários](/help/assets/assets/comments-sync1.png)

1. Selecionar **[!UICONTROL Inscrições em eventos]** clique em **[!UICONTROL Ativar a sincronização de comentários]** em **[!UICONTROL Enviar comentários feitos no Workfront para AEM]** opção.

   ![A sincronização está habilitada](/help/assets/assets/wf-comment-sync-enabled.png)

Para testar a sincronização de comentários do Workfront com o AEM, siga estas etapas:

1. Navegue até um documento vinculado no Workfront e adicione um comentário na guia Atualizações.

   ![deixar comentário no Workfront](/help/assets/assets/comments-sync2.png)

1. Navegue até o mesmo documento vinculado no AEM, selecione o documento e abra o [!UICONTROL Linha do tempo] na navegação à esquerda e selecione [!UICONTROL Comentários]. A barra lateral esquerda exibe os comentários sincronizados de [!DNL Workfront].

## Versões do ativo {#asset-versions}

Para manter o histórico de versões de ativos no AEM, configure o controle de versão de ativos no AEM.

1. No Experience Manager, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configuração de ferramentas do Workfront]** e abra a variável **[!UICONTROL Avançado]** guia.

1. Selecionar opção **[!UICONTROL Armazenar ativos com o mesmo nome que as versões do ativo existente]**. Quando marcada, essa opção permite armazenar ativos carregados com o mesmo nome e no mesmo local que a versão do ativo existente. Se permanecer desmarcada, um novo ativo será criado com um nome diferente (por exemplo, `asset-name.pdf` e `asset-name-1.pdf`).

1. Selecionar opção **[!UICONTROL Atualizar metadados de ativos ao criar uma versão]**. Quando marcada, essa opção atualiza os metadados do ativo sempre que uma nova versão do ativo é criada. Se desmarcado, o ativo manterá os metadados que tinha antes da criação da nova versão.

![configurar controle de versão de ativos](/help/assets/assets/wf-config-versioning.png)

>[!NOTE]
>
>Não há suporte para o controle de versão em pastas vinculadas. Ao criar uma [!DNL Workfront] Ao revisar um documento dentro de uma pasta vinculada, os comentários e as anotações na versão anterior do ativo são removidos.

## Anexar formulários personalizados {#attach-custom-forms}

Esta etapa do fluxo de trabalho permite que os usuários anexem um formulário personalizado a um [!DNL Workfront] artefato. Essa etapa do fluxo de trabalho pode ser adicionada a qualquer modelo de fluxo de trabalho. A variável [!DNL Workfront] o artefato que essa etapa afeta será pesquisado usando um caminho relativo da carga.

No editor de workflow do Experience Manager, edite as propriedades da variável [!UICONTROL Workfront - Anexar formulário personalizado] etapa do fluxo de trabalho.

![formulários personalizados](/help/assets/assets/wf-custom-forms.png).

## Publicar ativos automaticamente {#auto-publish-assets}

1. No Experience Manager, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configuração de ferramentas do Workfront]** e abra a variável **[!UICONTROL Avançado]** guia.

1. Selecionar **[!UICONTROL Publicar ativos automaticamente quando enviados do Workfront]**. Essa opção permite a publicação automática de ativos quando eles são enviados do Workfront para o AEM. Esse recurso pode ser ativado condicionalmente especificando um campo de formulário personalizado do Workfront e o valor para o qual ele deve ser definido. Sempre que um documento for enviado ao AEM, se ele atender à condição, o ativo será publicado automaticamente.

1. Selecionar **[!UICONTROL Publicar todos os ativos do projeto no Brand Portal após a conclusão do projeto]**. Essa opção permite a publicação automática de ativos no [!DNL Brand Portal] quando o status do projeto do Workfront ao qual pertencem é alterado para `Complete`.

![configurar publicação automática](/help/assets/assets/wf-auto-publish-config.png)

## Atualizações de formulário personalizado de documento do Workfront {#subscribe-workfront-doc-custom-form-updates}

Para assinar as alterações no [!DNL Workfront] formulários personalizados do documento, selecione a opção relevante na **[!UICONTROL Avançado]** guia. Quando você se inscreve nessas atualizações, ele atualiza as [!DNL Experience Manager] campos de metadados quando o campo correspondente no [!DNL Workfront] formulário personalizado de documento foi alterado.

![Configuração de atualizações de formulário personalizado de documento do Workfront no [!DNL Experience Manager]](/help/assets/assets/wf-custom-form-update.png)
