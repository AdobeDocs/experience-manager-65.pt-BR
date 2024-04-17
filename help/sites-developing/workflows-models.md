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
>Para uso da interface clássica, consulte a [Documentação do AEM 6.3](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/workflows-models.html) para referência.

Você cria um [modelo de fluxo de trabalho](/help/sites-developing/workflows.md#model) para definir a série de etapas executadas quando um usuário inicia o workflow. Você também pode definir propriedades do modelo, como se o fluxo de trabalho é transitório ou usa vários recursos.

Quando um usuário inicia um workflow, uma instância é iniciada; esse é o modelo de tempo de execução correspondente, criado quando você [Sincronizar](#sync-your-workflow-generate-a-runtime-model) suas alterações.

## Criação de um novo fluxo de trabalho {#creating-a-new-workflow}

Ao criar um modelo de fluxo de trabalho pela primeira vez, ele contém:

* As etapas, **Início do fluxo** e **Fim do fluxo**.
Eles representam o início e o fim do workflow. Essas etapas são obrigatórias e não podem ser editadas/removidas.
* Um exemplo **Participante** etapa chamada **Etapa 1**.
Esta etapa é configurada para atribuir um item de trabalho ao iniciador do fluxo de trabalho. Edite ou exclua esta etapa e adicione etapas conforme necessário.

Para criar um workflow com o editor:

1. Abra o **Modelos de fluxo de trabalho** console; via **Ferramentas**, **Fluxo de trabalho**, **Modelos** ou, por exemplo: [https://localhost:4502/aem/workflow](https://localhost:4502/aem/workflow)
1. Selecionar **Criar**, depois **Criar modelo**.
1. A variável **Adicionar modelo de fluxo de trabalho** será exibida. Insira o **Título** e **Nome** (opcional) antes de selecionar **Concluído**.
1. O novo modelo está listado no **Modelos de fluxo de trabalho** console.
1. Selecione o novo fluxo de trabalho e use [**Editar** para abri-lo para configuração](#editinganexistingworkflow):
   ![wf-01](assets/wf-01.png)

>[!NOTE]
>
>Se estiver criando modelos de forma programática (usando um pacote crx), você também pode criar uma subpasta em:
>
>`/var/workflow/models`
>
>Por exemplo, `/var/workflow/models/prototypes`
>
>Essa pasta pode ser usada para [gerenciamento do acesso aos modelos nessa pasta](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that).

## Editar um fluxo de trabalho {#editing-a-workflow}

É possível editar qualquer modelo de workflow existente para:

* [definir etapas](#addingasteptoamodel-) e seus [parâmetros](#configuring-a-workflow-step)
* configurar propriedades do fluxo de trabalho, incluindo [estágios](#configuring-workflow-stages-that-show-workflow-progress), [se o fluxo de trabalho é transitório](#creatingatransientworkflow-) e/ou [usa vários recursos](#configuring-a-workflow-for-multi-resource-support)

Edição de um [**Padrão e/ou herdado** Fluxo de trabalho (pronto para uso)](#editing-a-default-or-legacy-workflow-for-the-first-time) tem uma etapa adicional, para garantir que uma [cópia segura](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) é feita antes de suas alterações.

Quando as atualizações do fluxo de trabalho estiverem concluídas, você deverá usar **Sincronizar** para **Gerar um modelo em tempo de execução**. Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

### Sincronizar o fluxo de trabalho - Gerar um modelo em tempo de execução {#sync-your-workflow-generate-a-runtime-model}

**Sincronizar** (à direita na barra de ferramentas do editor) gera um [modelo de tempo de execução](/help/sites-developing/workflows.md#runtime-model). O modelo de tempo de execução é o modelo realmente usado quando um usuário inicia um fluxo de trabalho. Se você não **Sincronizar** suas alterações, as alterações não estarão disponíveis no tempo de execução.

Quando você (ou qualquer outro usuário) faz alterações no fluxo de trabalho, é necessário usar **Sincronizar** para gerar um modelo de tempo de execução - mesmo quando caixas de diálogo individuais (por exemplo, para etapas) tiverem suas próprias opções de salvamento.

Quando as alterações são sincronizadas com o modelo de tempo de execução (salvo), **Sincronizado** é exibido em vez disso.

Algumas etapas têm campos obrigatórios e/ou validação integrada. Quando essas condições não forem satisfeitas, um erro será exibido ao tentar **Sincronizar** o modelo. Por exemplo, quando nenhum participante tiver sido definido para um **Participante** etapa:

![wf-21](assets/wf-21.png)

### Edição de um fluxo de trabalho padrão ou herdado pela primeira vez {#editing-a-default-or-legacy-workflow-for-the-first-time}

Ao abrir uma [Modelo padrão e/ou herdado](/help/sites-developing/workflows.md#workflow-types) para edição:

* O navegador de Etapas não está disponível (lado esquerdo).
* Existe uma **Editar** ação disponível na barra de ferramentas (lado direito).
* Inicialmente, o modelo e suas propriedades são apresentados no modo somente leitura como:
   * Os workflows padrão estão em `/libs`
   * Os fluxos de trabalho herdados estão em `/etc`
Selecionar **Editar** irá:
* fazer uma cópia do fluxo de trabalho em `/conf`
* disponibilizar o navegador de Etapas
* permitir que você faça alterações

>[!NOTE]
>
>Consulte [Locais dos modelos de fluxo de trabalho](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) para obter mais informações.

![wf-22](assets/wf-22.png)

### Adicionar uma etapa a um modelo {#adding-a-step-to-a-model}

Adicione etapas ao modelo para representar a atividade a ser executada - cada etapa executa uma atividade específica. Uma seleção de componentes da etapa está disponível em uma instância padrão do AEM.

Ao editar um modelo, as etapas disponíveis aparecem nos vários grupos da **Navegador de etapas**. Por exemplo:

![wf-10](assets/wf-10.png)

>[!NOTE]
>
>Para obter informações sobre os componentes da etapa principal instalados com AEM, consulte [Referência de etapas do fluxo de trabalho](/help/sites-developing/workflows-step-ref.md).

Para adicionar etapas ao modelo de fluxo de trabalho:

1. Abra um modelo de fluxo de trabalho existente para edição. No **Modelo de fluxos de trabalho** selecione o modelo necessário e, em seguida, **Editar**.
1. Abra o navegador Etapas; usando **Ativar/desativar painel lateral**, na extremidade esquerda da barra de ferramentas superior. Aqui você pode:

   * **Filtro** para obter etapas específicas.
   * Use o seletor suspenso para limitar a seleção a um grupo específico de etapas.
   * Selecione o ícone Mostrar descrição ![wf-stepinfo-icon](assets/wf-stepinfo-icon.png) para mostrar mais detalhes sobre a etapa apropriada.

   ![wf-02](assets/wf-02.png)

1. Arraste as etapas apropriadas para o local desejado no modelo.

   Por exemplo, uma variável **Etapa do participante**.

   Depois de adicionado ao fluxo, você pode [configurar a etapa](#configuring-a-workflow-step).

   ![wf-03](assets/wf-03.png)

1. Adicione quantas etapas ou outras atualizações forem necessárias.

   No tempo de execução, as etapas são executadas na ordem em que aparecem no modelo. Depois de adicionar componentes da etapa, você pode arrastá-los para um local diferente no modelo.

   Também é possível copiar, recortar, colar, agrupar ou excluir etapas existentes; como no [editor de página.](/help/sites-authoring/editing-content.md)

   Etapas divididas também podem ser recolhidas/expandidas usando a opção da barra de ferramentas: ![wf-collapseexpand-toolbar-icon](assets/wf-collapseexpand-toolbar-icon.png)

1. Confirmar as alterações com **Sincronizar** (barra de ferramentas do editor) para gerar o modelo de tempo de execução.

   Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

### Configurar uma etapa do fluxo de trabalho {#configuring-a-workflow-step}

Você pode **Configurar** e personalizar o comportamento de uma etapa do fluxo de trabalho usando o **Propriedades da etapa** caixas de diálogo.

1. Para abrir o **Propriedades da etapa** para uma etapa:

   * Clique na etapa * * do modelo de fluxo de trabalho e selecione **Configurar** na barra de ferramentas do componente.

   * Clique duas vezes na etapa.

   >[!NOTE]
   >
   >Para obter informações sobre os componentes da etapa principal instalados com AEM, consulte [Referência de etapas do fluxo de trabalho](/help/sites-developing/workflows-step-ref.md).

1. Configure o **Propriedades da etapa** conforme necessário; as propriedades disponíveis dependem do tipo de etapa; também pode haver várias guias disponíveis. Por exemplo, o padrão **Etapa do participante**, presente em um novo fluxo de trabalho como `Step 1`:

   ![wf-11](assets/wf-11.png)

1. Confirme suas atualizações com a marca.
1. Confirmar as alterações com **Sincronizar** (barra de ferramentas do editor) para gerar o modelo de tempo de execução.

   Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

### Criar um fluxo de trabalho temporário {#creating-a-transient-workflow}

Você pode criar um [Temporário](/help/sites-developing/workflows.md#transient-workflows) modelo de fluxo de trabalho ao criar um modelo ou ao editar um existente:

1. Abrir o modelo de fluxo de trabalho para [edição](#editinganexistingworkflow).
1. Selecionar **Propriedades do modelo de fluxo de trabalho** na barra de ferramentas.
1. Na caixa de diálogo, ative **Fluxo de trabalho transitório** (ou desativar, se necessário):

   ![wf-07](assets/wf-07.png)

1. Confirmar a alteração com **Salvar e fechar**; seguido por **Sincronizar** (barra de ferramentas do editor) para gerar o modelo de tempo de execução.

   Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

>[!NOTE]
>
>Ao executar um fluxo de trabalho no [transitório](/help/sites-developing/workflows.md#transient-workflows) O modo AEM não armazena nenhum histórico de fluxo de trabalho. Por conseguinte, [Linha do tempo](/help/sites-authoring/basic-handling.md#timeline) não exibe nenhuma informação relacionada a esse workflow.

## Disponibilizar modelos de fluxo de trabalho na Interface para toque {#classic2touchui}

Se um modelo de fluxo de trabalho estiver presente na interface clássica, mas ausente no menu pop-up de seleção na **[!UICONTROL Linha do tempo]** da interface para toque, siga a configuração para disponibilizá-la. As etapas a seguir ilustram o uso do modelo de fluxo de trabalho chamado **[!UICONTROL Solicitação para ativação]**.

1. Confirme se o modelo não está disponível na interface habilitada para toque. Acessar um ativo usando o `/assets.html/content/dam` caminho. Selecione um ativo. Abertura **[!UICONTROL Linha do tempo]** no painel esquerdo. Clique em **[!UICONTROL Iniciar fluxo de trabalho]** e confirmar que a **[!UICONTROL Solicitação para ativação]** não está presente na lista pop-up.

1. Navegar até **[!UICONTROL Ferramentas > Geral > Tags]**. Selecionar **[!UICONTROL Fluxo de trabalho]**.

1. Selecionar **[!UICONTROL Criar > Criar tag]**. Definir **[!UICONTROL Título]** as `DAM` e **[!UICONTROL Nome]** as `dam`. Selecione **[!UICONTROL Enviar]**.
   ![Criar tag no modelo de fluxo de trabalho](assets/workflow_create_tag.png)

1. Navegue até **[!UICONTROL Ferramentas > Fluxo de trabalho > Modelos]**. Selecionar **[!UICONTROL Solicitação para ativação]** e selecione **[!UICONTROL Editar]**.

1. Selecionar **[!UICONTROL Editar]**, abra o **[!UICONTROL Informações da página]** e, nesse menu, selecione **[!UICONTROL Abrir propriedades]** e vá para a página **[!UICONTROL Básico]** (se ainda não estiver aberta).

1. Adicionar `Workflow : DAM` para **[!UICONTROL Tags]** campo. Confirme a seleção com a marca de seleção (marca de seleção).

1. Confirme a adição da tag com **[!UICONTROL Salvar e fechar]**.
   ![Editar propriedades de página do modelo](assets/workflow_model_edit_activation1.png)

1. Conclua o processo com **[!UICONTROL Sincronizar]**. O fluxo de trabalho agora está disponível na interface habilitada para toque.

### Configuração de um fluxo de trabalho para suporte a vários recursos {#configuring-a-workflow-for-multi-resource-support}

É possível configurar um modelo de fluxo de trabalho para [Suporte a vários recursos](/help/sites-developing/workflows.md#multi-resource-support) ao criar um modelo ou editar um existente:

1. Abrir o modelo de fluxo de trabalho para [edição](#editinganexistingworkflow).
1. Selecionar **Propriedades do modelo de fluxo de trabalho** na barra de ferramentas.

1. Na caixa de diálogo, ative **Suporte a vários recursos** (ou desativar, se necessário):

   ![wf-08](assets/wf-08.png)

1. Confirmar a alteração com **Salvar e fechar**; seguido por **Sincronizar** (barra de ferramentas do editor) para gerar o modelo de tempo de execução.

   Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

### Configuração de estágios de fluxo de trabalho (que mostram o andamento do fluxo de trabalho) {#configuring-workflow-stages-that-show-workflow-progress}

[Estágios do fluxo de trabalho](/help/sites-developing/workflows.md#workflow-stages) ajuda a visualizar o progresso de um workflow ao manipular tarefas.

>[!CAUTION]
>
>Se os estágios do fluxo de trabalho estiverem definidos em **Propriedades da página**, mas não usado para nenhuma das etapas do fluxo de trabalho, a barra de progresso não mostrará nenhum progresso (independentemente da etapa atual do fluxo de trabalho).

Os estágios a serem disponibilizados são definidos nos modelos de fluxo de trabalho; os modelos de fluxo de trabalho existentes podem ser atualizados para incluir definições de estágio. É possível definir qualquer número de estágios para o modelo de fluxo de trabalho.

Para definir **Estágios** para o seu workflow:

1. Abra o modelo de fluxo de trabalho para edição.
1. Selecionar **Propriedades do modelo de fluxo de trabalho** na barra de ferramentas. Em seguida, abra o **Estágios** guia.
1. Adicione (e posicione) o que for necessário **Estágios**. É possível definir qualquer número de estágios para o modelo de fluxo de trabalho.

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

1. Confirmar as alterações com **Sincronizar** (barra de ferramentas do editor) para gerar o modelo de tempo de execução.

   Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

## Exportação de um modelo de fluxo de trabalho em um pacote {#exporting-a-workflow-model-in-a-package}

Para exportar um modelo de fluxo de trabalho em um pacote:

1. Criar um pacote usando o [Gerenciador de pacotes](/help/sites-administering/package-manager.md#package-manager):

   1. Navegue até o Gerenciador de pacotes via **Ferramentas**, **Implantação**, **Pacotes**.

   1. Clique em **Criar pacote**.
   1. Especifique a **Nome do pacote** e quaisquer outros detalhes conforme necessário.
   1. Clique em **OK**.

1. Clique em **Editar** na barra de ferramentas do novo pacote.

1. Abra o **Filtros** guia.

1. Selecionar **Adicionar filtro** e especifique o caminho do modelo de fluxo de trabalho *design*:

   `/conf/global/settings/workflow/models/<*your-model-name*>`

   Clique em **Concluído**.

1. Selecionar **Adicionar filtro** e especifique o caminho do seu *tempo de execução* modelo de fluxo de trabalho:

   `/var/workflow/models/<*your-model-name*>`

   Clique em **Concluído**.

1. Adicione filtros adicionais para qualquer script personalizado usado pelo seu modelo.
1. Clique em **Salvar** para confirmar as definições de filtro.
1. Selecionar **Build** na barra de ferramentas da definição de pacote.
1. Selecionar **Baixar** na barra de ferramentas do pacote.

## Utilização de fluxos de trabalho para processar envios de formulários {#using-workflows-to-process-form-submissions}

Você pode configurar um formulário a ser processado pelo workflow selecionado. Quando os usuários enviam o formulário, uma nova instância de fluxo de trabalho é criada com os dados do envio do formulário como sua carga.

Para configurar o workflow a ser usado com seu formulário:

1. Crie uma página e abra-a para edição.
1. Adicionar um **Formulário** componente à página.
1. **Configurar** o **Início do formulário** componente que apareceu na página.
1. Uso **Iniciar fluxo de trabalho** para selecionar o fluxo de trabalho desejado entre os disponíveis:

   ![wf-12](assets/wf-12.png)

1. Confirme a nova configuração de formulário com a marca de verificação.

## Testar fluxos de trabalho {#testing-workflows}

Ao testar um fluxo de trabalho, é recomendável usar vários tipos de carga, incluindo tipos diferentes daquele para o qual ele foi desenvolvido. Por exemplo, se você pretende que o fluxo de trabalho lide com ativos, teste-o definindo uma Página como carga útil e certifique-se de que não gere erros.

Por exemplo, teste seu novo workflow da seguinte maneira:

1. [Inicie seu modelo de fluxo de trabalho](/help/sites-administering/workflows-starting.md) do console.
1. Defina o **Carga** e confirme.

1. Execute ações conforme necessário para que o workflow continue.
1. Monitore os arquivos de log enquanto o workflow está em execução.

Também é possível configurar o AEM para exibir **DEPURAR** nos arquivos de log. Consulte [Logs](/help/sites-deploying/configure-logging.md) para obter mais informações e quando o desenvolvimento estiver concluído, defina o **Nível de registro** voltar para **Informações**.

## Exemplos {#examples}

### Exemplo: criação de um fluxo de trabalho (simples) para aceitar ou rejeitar uma solicitação de publicação {#example-creating-a-simple-workflow-to-accept-or-reject-a-request-for-publication}

Para ilustrar algumas das possibilidades de criação de um workflow, o exemplo a seguir cria uma variação do `Publish Example` fluxo de trabalho.

1. [Criar um modelo de fluxo de trabalho](#creating-a-new-workflow).

   O novo workflow conterá:

   * **Início do fluxo**
   * `Step 1`
   * **Fim do fluxo**

1. Excluir `Step 1` (pois é o tipo de etapa errado para este exemplo):

   * Clique na etapa e selecione **Excluir** na barra de ferramentas do componente. Confirme a ação.

1. No **Fluxo de trabalho** seleção do navegador de etapas, arraste uma **Etapa do participante** no fluxo de trabalho e posicione-o entre **Início do fluxo** e **Fim do fluxo**.
1. Para abrir a caixa de diálogo de propriedades:

   * Clique na etapa do participante e selecione **Configurar** na barra de ferramentas do componente.
   * Clique duas vezes na etapa do participante.

1. No **Comum** entrada de guia `Validate Content` para ambos **Título** e **Descrição**.
1. Abra o **Usuário/Grupo** guia:

   * Ativar **Notificar usuário por e-mail**.
   * Selecionar `Administrator` ( `admin`) para o **Usuário/Grupo** campo.

   >[!NOTE]
   >
   >Para que os emails sejam enviados, [os detalhes do serviço de email e da conta de usuário precisam ser configurados](/help/sites-administering/notification.md).

1. Confirme as atualizações com a marca de verificação.

   Você retornará para a visão geral do modelo de fluxo de trabalho, em que a etapa do participante será renomeada para `Validate Content`.

1. Arraste um **Ou dividir** no fluxo de trabalho e posicione-o entre `Validate Content` e **Fim do fluxo**.
1. Abra o **Ou dividir** para configuração.
1. Configurar o:

   * **Comum**: especifique o nome da divisão.
   * **Ramificação 1**: selecionar **Rota Padrão**.

   * **Ramificação 2**: certifique-se **Rota Padrão** não está selecionado.

1. Confirme suas atualizações na **OU dividir**.
1. Arraste um **Etapa do participante** à ramificação esquerda, abra as propriedades, especifique os seguintes valores e confirme as alterações:

   * **Título**: `Reject Publish Request`

   * **Usuário/Grupo**: por exemplo, `projects-administrators`

   * **Notificar usuário por e-mail**: ative para que o usuário seja notificado por email.

1. Arraste um **Etapa do processo** à ramificação direita, abra as propriedades, especifique os seguintes valores e confirme as alterações:

   * **Título**: `Publish Page as Requested`

   * **Processo**: selecionar `Activate Page`. Esse processo publica a página selecionada nas instâncias do editor.

1. Clique em **Sincronizar** (barra de ferramentas do editor) para gerar o modelo de tempo de execução.

   Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

   Seu novo modelo de fluxo de trabalho será semelhante a:

   ![wf-13](assets/wf-13.png)

1. Aplique esse fluxo de trabalho à sua página, para que, quando o usuário mudar para **Concluído** o **Validar conteúdo** etapa, eles podem selecionar se desejam **Publicar página como solicitado** ou **Rejeitar solicitação de publicação**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

### Exemplo: Definição de uma Regra para uma Divisão OR usando o script ECMA {#defineruleecmascript}

**OU dividir** As etapas permitem introduzir caminhos de processamento condicional no fluxo de trabalho.

Para definir uma regra OR, proceda da seguinte maneira:

1. Crie dois scripts e salve-os no repositório, por exemplo, em:

   `/apps/myapp/workflow/scripts`

   >[!NOTE]
   >
   >Os scripts devem ter um [função `check()`](#function-check) que retorna um valor booleano.

1. Edite o workflow e adicione o **OU dividir** para o modelo.
1. Editar as propriedades de **Ramificação 1** do **OU dividir**:

   * Defina como o **Rota Padrão** definindo o **Valor** para `true`.

   * Como **Regra**, defina o caminho para o script. Por exemplo:
     `/apps/myapp/workflow/scripts/myscript1.ecma`

   >[!NOTE]
   >
   >Você pode alternar a ordem da ramificação, se necessário.

1. Edite as propriedades do **Ramificação 2** do **OU dividir**.

   * Como **Regra**, defina o caminho para o outro script. Por exemplo:
     `/apps/myapp/workflow/scripts/myscript2.ecma`

1. Defina as propriedades das etapas individuais em cada ramificação. Verifique se **Usuário/Grupo** está definido.
1. Clique em **Sincronizar** (barra de ferramentas do editor) para manter as alterações no modelo de tempo de execução.

   Consulte [Sincronizar o fluxo de trabalho](#sync-your-workflow-generate-a-runtime-model) para obter detalhes.

#### Função Check() {#function-check}

>[!NOTE]
>
>Consulte [Utilização do ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).

O exemplo de script a seguir retorna `true` se o nó for um `JCR_PATH` localizado em `/content/we-retail/us/en`:

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

Por exemplo, **Solicitação para ativação**. Esse fluxo de trabalho é usado para publicar páginas no **Sites** e é acionado automaticamente quando um autor de conteúdo não tem os direitos de replicação apropriados. Consulte [Personalização da criação de página - Personalização da solicitação para o fluxo de trabalho de ativação](/help/sites-developing/customizing-page-authoring-touch.md#customizing-the-request-for-activation-workflow) para obter mais detalhes.
