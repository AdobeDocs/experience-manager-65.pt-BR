---
title: Criação de modelos de fluxo de trabalho
description: Crie um modelo de fluxo de trabalho para definir a série de etapas executadas quando um usuário inicia o fluxo de trabalho.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 6790202f-0542-4779-b3ce-d394cdba77b4
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2462'
ht-degree: 3%

---

# Criação de modelos de fluxo de trabalho{#creating-workflow-models}

>[!CAUTION]
>
>Para uso da interface clássica, consulte a [documentação do AEM 6.3](https://helpx.adobe.com/br/experience-manager/6-3/help/sites-developing/workflows-models.html) para referência.

Você cria um [modelo de fluxo de trabalho](/help/sites-developing/workflows.md#model) para definir a série de etapas executadas quando um usuário inicia o fluxo de trabalho. Você também pode definir propriedades do modelo, como se o fluxo de trabalho é transitório ou usa vários recursos.

Quando um usuário inicia um fluxo de trabalho, uma instância é iniciada; este é o modelo de tempo de execução correspondente, criado quando você [Sincroniza](#sync-your-workflow-generate-a-runtime-model) suas alterações.

## Criação de um novo fluxo de trabalho {#creating-a-new-workflow}

Ao criar um modelo de fluxo de trabalho pela primeira vez, ele contém:

* As etapas, **Início do Fluxo** e **Término do Fluxo**.
Eles representam o início e o fim do workflow. Essas etapas são obrigatórias e não podem ser editadas/removidas.
* Um exemplo de etapa **Participante** chamada **Etapa 1**.
Esta etapa é configurada para atribuir um item de trabalho ao iniciador do fluxo de trabalho. Edite ou exclua esta etapa e adicione etapas conforme necessário.

Para criar um workflow com o editor:

1. Abra o console **Modelos de Fluxo de Trabalho**; via **Ferramentas**, **Fluxo de Trabalho**, **Modelos** ou, por exemplo: [https://localhost:4502/aem/workflow](https://localhost:4502/aem/workflow)
1. Selecione **Criar** e depois **Criar Modelo**.
1. A caixa de diálogo **Adicionar modelo de fluxo de trabalho** é exibida. Insira o **Título** e o **Nome** (opcional) antes de selecionar **Concluído**.
1. O novo modelo está listado no console **Modelos de Fluxo de Trabalho**.
1. Selecione o novo fluxo de trabalho e use a [**Edição** para abri-lo para a configuração](#editinganexistingworkflow):
   ![wf-01](assets/wf-01.png)

>[!NOTE]
>
>Se estiver criando modelos de forma programática (usando um pacote crx), você também pode criar uma subpasta em:
>
>`/var/workflow/models`
>
>Por exemplo, `/var/workflow/models/prototypes`
>
>Esta pasta pode ser usada para [gerenciar o acesso aos modelos nessa pasta](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that).

## Editar um fluxo de trabalho {#editing-a-workflow}

É possível editar qualquer modelo de workflow existente para:

* [definir etapas](#addingasteptoamodel-) e seus [parâmetros](#configuring-a-workflow-step)
* configure as propriedades do fluxo de trabalho, incluindo [estágios](#configuring-workflow-stages-that-show-workflow-progress), [se o fluxo de trabalho é transitório](#creatingatransientworkflow-) e/ou [usa vários recursos](#configuring-a-workflow-for-multi-resource-support)

A edição de um fluxo de trabalho [**Padrão e/ou Herdado** (pronto para uso)](#editing-a-default-or-legacy-workflow-for-the-first-time) tem uma etapa adicional, para garantir que uma [cópia segura](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) seja feita antes das alterações.

Quando as atualizações do fluxo de trabalho forem concluídas, você deverá usar **Sincronizar** para **Gerar um Modelo de Tempo de Execução**. Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

### Sincronizar o fluxo de trabalho - Gerar um modelo em tempo de execução {#sync-your-workflow-generate-a-runtime-model}

**Sync** (à direita da barra de ferramentas do editor) gera um [modelo de tempo de execução](/help/sites-developing/workflows.md#runtime-model). O modelo de tempo de execução é o modelo realmente usado quando um usuário inicia um fluxo de trabalho. Se você não **Sincronizar** suas alterações, elas não estarão disponíveis no tempo de execução.

Quando você (ou qualquer outro usuário) faz alterações no fluxo de trabalho, deve usar **Sincronizar** para gerar um modelo de tempo de execução - mesmo quando caixas de diálogo individuais (por exemplo, para etapas) têm suas próprias opções de salvamento.

Quando as alterações são sincronizadas com o modelo de tempo de execução (salvo), **Sincronizado** é exibido.

Algumas etapas têm campos obrigatórios e/ou validação integrada. Quando estas condições não são satisfeitas um erro é mostrado quando você tenta **Sincronizar** o modelo. Por exemplo, quando nenhum participante tiver sido definido para uma etapa **Participante**:

![wf-21](assets/wf-21.png)

### Edição de um fluxo de trabalho padrão ou herdado pela primeira vez {#editing-a-default-or-legacy-workflow-for-the-first-time}

Ao abrir um [modelo Padrão e/ou Herdado](/help/sites-developing/workflows.md#workflow-types) para edição:

* O navegador de Etapas não está disponível (lado esquerdo).
* Há uma ação **Editar** disponível na barra de ferramentas (lado direito).
* Inicialmente, o modelo e suas propriedades são apresentados no modo somente leitura como:
   * Os fluxos de trabalho padrão estão em `/libs`
   * Os fluxos de trabalho herdados estão em `/etc`
Selecionar **Editar** irá:
* fazer uma cópia do fluxo de trabalho em `/conf`
* disponibilizar o navegador de Etapas
* permitir que você faça alterações

>[!NOTE]
>
>Consulte [Locais de Modelos de Fluxo de Trabalho](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) para obter mais informações.

![wf-22](assets/wf-22.png)

### Adicionar uma etapa a um modelo {#adding-a-step-to-a-model}

Adicione etapas ao modelo para representar a atividade a ser executada - cada etapa executa uma atividade específica. Uma seleção de componentes da etapa está disponível em uma instância padrão do AEM.

Ao editar um modelo, as etapas disponíveis aparecem nos vários grupos do **Navegador de etapas**. Por exemplo:

![wf-10](assets/wf-10.png)

>[!NOTE]
>
>Para obter informações sobre os componentes principais da etapa instalados com AEM, consulte [Referência a Etapas do Fluxo de Trabalho](/help/sites-developing/workflows-step-ref.md).

Para adicionar etapas ao modelo de fluxo de trabalho:

1. Abra um modelo de fluxo de trabalho existente para edição. No console **Modelo de Fluxos de Trabalho**, selecione o modelo necessário e **Editar**.
1. Abra o navegador Etapas; usando **Alternar Painel Lateral**, na extremidade esquerda da barra de ferramentas superior. Aqui você pode:

   * **Filtre** por etapas específicas.
   * Use o seletor suspenso para limitar a seleção a um grupo específico de etapas.
   * Selecione o ícone Mostrar descrição ![wf-stepinfo-icon](assets/wf-stepinfo-icon.png) para mostrar mais detalhes sobre a etapa apropriada.

   ![wf-02](assets/wf-02.png)

1. Arraste as etapas apropriadas para o local desejado no modelo.

   Por exemplo, uma **Etapa do participante**.

   Depois de adicionado ao fluxo, você pode [configurar a etapa](#configuring-a-workflow-step).

   ![wf-03](assets/wf-03.png)

1. Adicione quantas etapas ou outras atualizações forem necessárias.

   No tempo de execução, as etapas são executadas na ordem em que aparecem no modelo. Depois de adicionar componentes da etapa, você pode arrastá-los para um local diferente no modelo.

   Você também pode copiar, recortar, colar, agrupar ou excluir etapas existentes; como acontece com o [editor de páginas.](/help/sites-authoring/editing-content.md)

   Etapas divididas também podem ser recolhidas/expandidas usando a opção de barra de ferramentas: ![wf-collapseexpand-toolbar-icon](assets/wf-collapseexpand-toolbar-icon.png)

1. Confirme as alterações com **Sync** (barra de ferramentas do editor) para gerar o modelo de tempo de execução.

   Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

### Configurar uma etapa do fluxo de trabalho {#configuring-a-workflow-step}

Você pode **Configurar** e personalizar o comportamento de uma etapa do fluxo de trabalho usando as caixas de diálogo **Propriedades da Etapa**.

1. Para abrir a caixa de diálogo **Propriedades da Etapa** para uma etapa:

   * Clique na etapa * * do modelo de fluxo de trabalho e selecione **Configurar** na barra de ferramentas do componente.

   * Clique duas vezes na etapa.

   >[!NOTE]
   >
   >Para obter informações sobre os componentes principais da etapa instalados com AEM, consulte [Referência a Etapas do Fluxo de Trabalho](/help/sites-developing/workflows-step-ref.md).

1. Configure as **Propriedades de Etapa** conforme necessário; as propriedades disponíveis dependem do tipo de etapa; também pode haver várias guias disponíveis. Por exemplo, a **Etapa do participante** padrão, presente em um novo fluxo de trabalho como `Step 1`:

   ![wf-11](assets/wf-11.png)

1. Confirme suas atualizações com a marca.
1. Confirme as alterações com **Sync** (barra de ferramentas do editor) para gerar o modelo de tempo de execução.

   Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

### Criar um fluxo de trabalho temporário {#creating-a-transient-workflow}

Você pode criar um modelo de fluxo de trabalho [Transitório](/help/sites-developing/workflows.md#transient-workflows) ao criar um modelo ou ao editar um existente:

1. Abra o modelo de fluxo de trabalho para [edição](#editinganexistingworkflow).
1. Selecione **Propriedades do Modelo de Fluxo de Trabalho** na barra de ferramentas.
1. Na caixa de diálogo, ative o **Fluxo de Trabalho Transitório** (ou desative, se necessário):

   ![wf-07](assets/wf-07.png)

1. Confirme a alteração com **Salvar e fechar**; seguido por **Sincronizar** (barra de ferramentas do editor) para gerar o modelo de tempo de execução.

   Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

>[!NOTE]
>
>Quando você executa um fluxo de trabalho no modo [transitório](/help/sites-developing/workflows.md#transient-workflows), o AEM não armazena nenhum histórico de fluxo de trabalho. Portanto, [Linha do Tempo](/help/sites-authoring/basic-handling.md#timeline) não exibe nenhuma informação relacionada a esse fluxo de trabalho.

## Disponibilizar modelos de fluxo de trabalho na Interface para toque {#classic2touchui}

Se um modelo de fluxo de trabalho estiver presente na interface clássica, mas ausente no menu pop-up de seleção no painel **[!UICONTROL Linha do tempo]** da interface de toque, siga a configuração para disponibilizá-lo. As etapas a seguir ilustram o uso do modelo de fluxo de trabalho chamado **[!UICONTROL Solicitação de ativação]**.

1. Confirme se o modelo não está disponível na interface habilitada para toque. Acesse um ativo usando o caminho `/assets.html/content/dam`. Selecione um ativo. Abra a **[!UICONTROL Linha do tempo]** no painel esquerdo. Clique em **[!UICONTROL Iniciar Fluxo de Trabalho]** e confirme se o modelo **[!UICONTROL Solicitação de Ativação]** não está presente na lista pop-up.

1. Navegue por **[!UICONTROL Ferramentas > Geral > Marcação]**. Selecione **[!UICONTROL Fluxo de trabalho]**.

1. Selecione **[!UICONTROL Criar > Criar Marca]**. Definir **[!UICONTROL Título]** como `DAM` e **[!UICONTROL Nome]** como `dam`. Selecione **[!UICONTROL Enviar]**.
   ![Criar marca no modelo de fluxo de trabalho](assets/workflow_create_tag.png)

1. Navegue até **[!UICONTROL Ferramentas > Fluxo de trabalho > Modelos]**. Selecione **[!UICONTROL Solicitar ativação]** e **[!UICONTROL Editar]**.

1. Selecione **[!UICONTROL Editar]**, abra o menu **[!UICONTROL Informações da Página]** e, a partir daí, selecione **[!UICONTROL Abrir Propriedades]** e vá para a guia **[!UICONTROL Básico]** (se ainda não estiver aberta).

1. Adicionar `Workflow : DAM` ao campo **[!UICONTROL Marcas]**. Confirme a seleção com a marca de seleção (marca de seleção).

1. Confirme a adição da tag com **[!UICONTROL Salvar e Fechar]**.
   ![Editar Propriedades da Página do Modelo](assets/workflow_model_edit_activation1.png)

1. Conclua o processo com **[!UICONTROL Sincronizar]**. O fluxo de trabalho agora está disponível na interface habilitada para toque.

### Configuração de um fluxo de trabalho para suporte a vários recursos {#configuring-a-workflow-for-multi-resource-support}

Você pode configurar um modelo de fluxo de trabalho para o [Suporte a Vários Recursos](/help/sites-developing/workflows.md#multi-resource-support) ao criar um modelo ou ao editar um existente:

1. Abra o modelo de fluxo de trabalho para [edição](#editinganexistingworkflow).
1. Selecione **Propriedades do Modelo de Fluxo de Trabalho** na barra de ferramentas.

1. Na caixa de diálogo, ative o **Suporte a vários recursos** (ou desative, se necessário):

   ![wf-08](assets/wf-08.png)

1. Confirme a alteração com **Salvar e fechar**; seguido por **Sincronizar** (barra de ferramentas do editor) para gerar o modelo de tempo de execução.

   Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

### Configuração de estágios de fluxo de trabalho (que mostram o andamento do fluxo de trabalho) {#configuring-workflow-stages-that-show-workflow-progress}

[Estágios do Fluxo de Trabalho](/help/sites-developing/workflows.md#workflow-stages) ajudam a visualizar o progresso de um fluxo de trabalho ao manipular tarefas.

>[!CAUTION]
>
>Se os estágios do fluxo de trabalho estiverem definidos em **Propriedades da Página**, mas não forem usados para nenhuma das etapas do fluxo de trabalho, a barra de progresso não mostrará nenhum progresso (independentemente da etapa atual do fluxo de trabalho).

Os estágios a serem disponibilizados são definidos nos modelos de fluxo de trabalho; os modelos de fluxo de trabalho existentes podem ser atualizados para incluir definições de estágio. É possível definir qualquer número de estágios para o modelo de fluxo de trabalho.

Para definir **Estágios** para seu fluxo de trabalho:

1. Abra o modelo de fluxo de trabalho para edição.
1. Selecione **Propriedades do Modelo de Fluxo de Trabalho** na barra de ferramentas. Em seguida, abra a guia **Estágios**.
1. Adicione (e posicione) os **Estágios** necessários. É possível definir qualquer número de estágios para o modelo de fluxo de trabalho.

   Por exemplo:

   ![wf-08-1](assets/wf-08-1.png)

1. Clique em **Salvar e fechar** para salvar as propriedades.
1. Atribua um estágio a cada etapa no modelo de fluxo de trabalho. Por exemplo:

   ![wf-09](assets/wf-09.png)

   Um estágio pode ser atribuído a mais de uma etapa. Por exemplo:

   | **Etapa** | **Estágio** |
   |---|---|
   | Etapa 1 | Criar |
   | Etapa 2 | Criar |
   | Etapa 3 | Revisar |
   | Etapa 4 | Aprovar |
   | Etapa 5 | Aprovar |
   | Etapa 6 | Concluído |

1. Confirme as alterações com **Sync** (barra de ferramentas do editor) para gerar o modelo de tempo de execução.

   Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

## Exportação de um modelo de fluxo de trabalho em um pacote {#exporting-a-workflow-model-in-a-package}

Para exportar um modelo de fluxo de trabalho em um pacote:

1. Criar um pacote usando o [Gerenciador de Pacotes](/help/sites-administering/package-manager.md#package-manager):

   1. Navegue até o Gerenciador de Pacotes por meio de **Ferramentas**, **Implantação**, **Pacotes**.

   1. Clique em **Criar Pacote**.
   1. Especifique o **Nome do Pacote** e quaisquer outros detalhes, conforme necessário.
   1. Clique em **OK**.

1. Clique em **Editar** na barra de ferramentas do novo pacote.

1. Abra a guia **Filtros**.

1. Selecione **Adicionar filtro** e especifique o caminho do modelo de fluxo de trabalho *design*:

   `/conf/global/settings/workflow/models/<*your-model-name*>`

   Clique em **Concluído**.

1. Selecione **Adicionar filtro** e especifique o caminho do modelo de fluxo de trabalho *tempo de execução*:

   `/var/workflow/models/<*your-model-name*>`

   Clique em **Concluído**.

1. Adicione filtros adicionais para qualquer script personalizado usado pelo seu modelo.
1. Clique em **Salvar** para confirmar as definições de filtro.
1. Selecione **Build** na barra de ferramentas da definição de pacote.
1. Selecione **Baixar** na barra de ferramentas do pacote.

## Utilização de fluxos de trabalho para processar envios de formulários {#using-workflows-to-process-form-submissions}

Você pode configurar um formulário a ser processado pelo workflow selecionado. Quando os usuários enviam o formulário, uma nova instância de fluxo de trabalho é criada com os dados do envio do formulário como sua carga.

Para configurar o workflow a ser usado com seu formulário:

1. Crie uma página e abra-a para edição.
1. Adicione um componente **Formulário** à página.
1. **Configure** o componente **Início do Formulário** que apareceu na página.
1. Use **Iniciar Fluxo de Trabalho** para selecionar o fluxo de trabalho desejado entre os disponíveis:

   ![wf-12](assets/wf-12.png)

1. Confirme a nova configuração de formulário com a marca de verificação.

## Testar fluxos de trabalho {#testing-workflows}

Ao testar um fluxo de trabalho, é recomendável usar vários tipos de carga, incluindo tipos diferentes daquele para o qual ele foi desenvolvido. Por exemplo, se você pretende que seu fluxo de trabalho lide com o Assets, teste-o definindo uma Página como carga útil e certifique-se de que não gere erros.

Por exemplo, teste seu novo workflow da seguinte maneira:

1. [Inicie seu modelo de fluxo de trabalho](/help/sites-administering/workflows-starting.md) a partir do console.
1. Defina a **Carga** e confirme.

1. Execute ações conforme necessário para que o workflow continue.
1. Monitore os arquivos de log enquanto o workflow está em execução.

Você também pode configurar o AEM para exibir mensagens de **DEBUG** nos arquivos de log. Consulte [Log](/help/sites-deploying/configure-logging.md) para obter mais informações e, quando o desenvolvimento for concluído, redefina o **Nível de Log** como **Info**.

## Exemplos {#examples}

### Exemplo: criação de um fluxo de trabalho (simples) para aceitar ou rejeitar uma solicitação de publicação {#example-creating-a-simple-workflow-to-accept-or-reject-a-request-for-publication}

Para ilustrar algumas das possibilidades de criação de um fluxo de trabalho, o exemplo a seguir cria uma variação do fluxo de trabalho `Publish Example`.

1. [Criar um modelo de fluxo de trabalho](#creating-a-new-workflow).

   O novo workflow conterá:

   * **Início do fluxo**
   * `Step 1`
   * **Fim do Fluxo**

1. Excluir `Step 1` (pois é o tipo de etapa errado para este exemplo):

   * Clique na etapa e selecione **Excluir** na barra de ferramentas do componente. Confirme a ação.

1. Na seleção **Fluxo de Trabalho** do navegador de etapas, arraste uma **Etapa de Participante** para o fluxo de trabalho e posicione-a entre **Início do Fluxo** e **Fim do Fluxo**.
1. Para abrir a caixa de diálogo de propriedades:

   * Clique na etapa do participante e selecione **Configurar** na barra de ferramentas do componente.
   * Clique duas vezes na etapa do participante.

1. Na guia **Comum**, digite `Validate Content` para o **Título** e a **Descrição**.
1. Abra a guia **Usuário/Grupo**:

   * Ativar **Notificar usuário via email**.
   * Selecione `Administrator` ( `admin`) para o campo **Usuário/Grupo**.

   >[!NOTE]
   >
   >Para que emails sejam enviados, [o serviço de email e os detalhes da conta de usuário precisam ser configurados](/help/sites-administering/notification.md).

1. Confirme as atualizações com a marca de verificação.

   Você retornará para a visão geral do modelo de fluxo de trabalho, onde a etapa do participante será renomeada para `Validate Content`.

1. Arraste um **Or Split** para o fluxo de trabalho e posicione-o entre `Validate Content` e **Fim do Fluxo**.
1. Abra a **Ou a Divisão** para configuração.
1. Configurar o:

   * **Comum**: especifique o nome da divisão.
   * **Ramificação 1**: selecione **Rota Padrão**.

   * **Ramificação 2**: certifique-se de que a **Rota Padrão** não esteja selecionada.

1. Confirme suas atualizações para a **OU Split**.
1. Arraste uma **Etapa do participante** para a ramificação esquerda, abra as propriedades, especifique os seguintes valores e confirme as alterações:

   * **Título**: `Reject Publish Request`

   * **Usuário/Grupo**: por exemplo, `projects-administrators`

   * **Notificar usuário por email**: ative para que o usuário seja notificado por email.

1. Arraste uma **Etapa do processo** para a ramificação direita, abra as propriedades, especifique os valores a seguir e confirme as alterações:

   * **Título**: `Publish Page as Requested`

   * **Processo**: selecione `Activate Page`. Esse processo publica a página selecionada nas instâncias do editor.

1. Clique em **Sincronizar** (barra de ferramentas do editor) para gerar o modelo de tempo de execução.

   Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

   Seu novo modelo de fluxo de trabalho será semelhante a:

   ![wf-13](assets/wf-13.png)

1. Aplique este fluxo de trabalho à sua página para que, quando o usuário mudar para **Concluir** a etapa **Validar conteúdo**, possa selecionar se deseja **Página do Publish como Solicitada** ou **Rejeitar solicitação do Publish**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

### Exemplo: Definição de uma Regra para uma Divisão OR usando o script ECMA {#defineruleecmascript}

As etapas **OU Split** permitem introduzir caminhos de processamento condicional no fluxo de trabalho.

Para definir uma regra OR, proceda da seguinte maneira:

1. Crie dois scripts e salve-os no repositório, por exemplo, em:

   `/apps/myapp/workflow/scripts`

   >[!NOTE]
   >
   >Os scripts devem ter uma [função `check()`](#function-check) que retorne um booleano.

1. Edite o fluxo de trabalho e adicione a **OU Split** ao modelo.
1. Edite as propriedades da **Ramificação 1** de **OU Divisão**:

   * Defina esta como a **Rota Padrão** definindo o **Valor** como `true`.

   * Como **Regra**, defina o caminho para o script. Por exemplo:

     `/apps/myapp/workflow/scripts/myscript1.ecma`

   >[!NOTE]
   >
   >Você pode alternar a ordem da ramificação, se necessário.

1. Edite as propriedades da **Ramificação 2** de **OU Divisão**.

   * Como **Regra**, defina o caminho para o outro script. Por exemplo:

     `/apps/myapp/workflow/scripts/myscript2.ecma`

1. Defina as propriedades das etapas individuais em cada ramificação. Verifique se o **Usuário/Grupo** está definido.
1. Clique em **Sincronizar** (barra de ferramentas do editor) para manter suas alterações no modelo de tempo de execução.

   Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

#### Função Check() {#function-check}

>[!NOTE]
>
>Consulte [Usando ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).

O exemplo de script a seguir retornará `true` se o nó for um `JCR_PATH` localizado em `/content/we-retail/us/en`:

```
function check() {
    if (workflowData.getPayloadType() == "JCR_PATH") {
      var path = workflowData.getPayload().toString();
      var node = jcrSession.getItem(path);

      if (node.getPath().indexOf("/content/we-retail/us/en") >= 0) {
       return true;
      } else {
       return false;
      }
     } else {
      return false;
     }
}
```

### Exemplo: solicitação personalizada para ativação {#example-customized-request-for-activation}

Você pode personalizar qualquer um dos workflows prontos para uso. Para personalizar o comportamento, você sobrepõe os detalhes do fluxo de trabalho apropriado.

Por exemplo, **Solicitação de ativação**. Este fluxo de trabalho é usado para publicar páginas em **Sites** e é acionado automaticamente quando um autor de conteúdo não tem os direitos de replicação apropriados. Consulte [Personalizando a criação de páginas - Personalizando a solicitação de fluxo de trabalho de ativação](/help/sites-developing/customizing-page-authoring-touch.md#customizing-the-request-for-activation-workflow) para obter mais detalhes.
