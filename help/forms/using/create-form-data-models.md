---
title: Criar modelo de dados de formulário
description: Saiba como criar modelos de dados de formulário com ou sem fontes de dados configuradas.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
docset: aem65
feature: Form Data Model
exl-id: 7f5978c3-6c9f-4ce4-b0fb-660ac1d49244
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 1%

---

# Criar modelo de dados de formulário{#create-form-data-model}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/create-form-data-models.html) |
| AEM 6.5 | Este artigo |


![imagem-herói](do-not-localize/data-integration.png)

A integração de dados do AEM Forms fornece uma interface de usuário intuitiva para criar e trabalhar com modelos de dados de formulário. Um modelo de dados de formulário depende de fontes de dados para troca de dados; no entanto, é possível criar um modelo de dados de formulário com ou sem uma fonte de dados. Há duas abordagens para criar um a partir do modelo de dados, dependendo se você configurou as fontes de dados:

* **Usando fontes de dados pré-configuradas**: se você tiver configurado as fontes de dados conforme descrito em [Configurar fontes de dados](../../forms/using/configure-data-sources.md), poderá selecioná-las ao criar um modelo de dados de formulário. Ele traz todos os objetos, propriedades e serviços do modelo de dados das fontes de dados selecionadas disponíveis para uso no modelo de dados de formulário.

* **Sem fontes de dados**: se você não tiver configurado fontes de dados para seu modelo de dados de formulário, ainda poderá criá-lo sem fontes de dados. Você pode usar o modelo de dados de formulário para criar formulários adaptáveis e comunicação interativa e testá-los usando dados de amostra. Quando as fontes de dados estiverem disponíveis, você poderá vincular o modelo de dados de formulário às fontes de dados, que serão refletidas automaticamente nos formulários adaptáveis associados e nas comunicações interativas.

>[!NOTE]
>
>Você deve ser membro de ambos os grupos **fdm-author** e **forms-user** para poder criar e trabalhar com o modelo de dados de formulário. Entre em contato com o administrador do AEM para se tornar um membro dos grupos.

## Criar modelo de dados de formulário {#data-sources}

Verifique se você configurou as fontes de dados que pretende usar no modelo de dados de formulário conforme descrito em [Configurar fontes de dados](../../forms/using/configure-data-sources.md). Faça o seguinte para criar um modelo de dados de formulário com base nas fontes de dados configuradas:

1. Na instância do autor AEM, navegue até **[!UICONTROL Forms > Integrações de dados]**.
1. Selecione **[!UICONTROL Criar > Modelo de dados de formulário]**.
1. Na caixa de diálogo Criar modelo de dados de formulário:

   * Especifique um nome para o modelo de dados de formulário.
   * (**Opcional**) Especifique o título, a descrição e as marcas para o modelo de dados de formulário.
   * (**Opcional e aplicável somente se as fontes de dados estiverem configuradas**) Selecione o ícone de marca de verificação ao lado do campo **[!UICONTROL Configuração do Data Source]** e selecione o nó de configuração onde residem os serviços em nuvem para as fontes de dados que você deseja usar. Ele restringe a lista de origens de dados disponíveis para seleção na próxima página às disponíveis no nó de configuração selecionado. No entanto, qualquer banco de dados JDBC e origens de dados de perfil de usuário AEM são listados por padrão. Se você não selecionar um nó de configuração, as origens de dados de todos os nós de configuração serão listadas.

   Selecione **[!UICONTROL Próximo]**.

1. (**Aplicável somente se as fontes de dados estiverem configuradas**) A tela **[!UICONTROL Selecionar Fonte de Dados]** lista as fontes de dados disponíveis, se houver. Selecione as fontes de dados que deseja usar no modelo de dados do formulário.
1. Selecione **[!UICONTROL Criar]** e, na caixa de diálogo de confirmação, selecione **[!UICONTROL Abrir]** para abrir o editor de modelo de dados de formulário.

Vamos revisar os diferentes componentes da interface do editor do modelo de dados de formulário.

![Um modelo de dados de formulário com três fontes de dados - um serviço RESTful, um perfil de usuário AEM e um RDBMS](assets/fdm-ui.png)

**A Fontes de Dados** Lista fontes de dados em um modelo de dados de formulário. Expanda uma fonte de dados para exibir seus objetos de modelo de dados e serviços.

**B Atualizar Definições da Source de Dados** Busca todas as alterações nas definições de fonte de dados das fontes de dados configuradas e as atualiza na guia Fontes de Dados do editor de modelo de dados de formulário.

**C Modelo** Área de conteúdo em que os objetos de modelo de dados adicionados aparecem.

**D Serviços** Área de conteúdo na qual aparecem as operações ou os serviços da fonte de dados adicionados.

**E Barra de ferramentas** Ferramentas para trabalhar com o modelo de dados de formulário. A barra de ferramentas mostra mais opções dependendo do objeto selecionado no modelo de dados de formulário.

**F Adicionar selecionados** Adiciona objetos e serviços de modelo de dados selecionados ao modelo de dados de formulário.

Para obter mais informações sobre o editor de modelo de dados de formulário e como trabalhar com ele para editar e configurar o modelo de dados de formulário, consulte [Trabalhar com o modelo de dados de formulário](../../forms/using/work-with-form-data-model.md).

## Atualizar fontes de dados {#update}

Faça o seguinte para adicionar ou atualizar fontes de dados a um modelo de dados de formulário existente.

1. Vá para **[!UICONTROL Forms > Integrações de Dados]**, selecione o modelo de dados de formulário no qual deseja adicionar ou atualizar fontes de dados e selecione **[!UICONTROL Propriedades]**.
1. Nas propriedades do modelo de dados de formulário, vá para a guia **[!UICONTROL Atualizar Source]**.

   Na guia Update Source:

   * Selecione o ícone de procura no campo **[!UICONTROL Configuração sensível ao contexto]** e selecione um nó de configuração em que esteja a configuração em nuvem da fonte de dados que você deseja adicionar. Se você não selecionar um nó, as configurações de nuvem que residem somente no nó `global` serão listadas quando você selecionar **[!UICONTROL Adicionar Fontes]**.

   * Para adicionar uma nova fonte de dados, selecione **[!UICONTROL Adicionar Fontes]** e selecione as fontes de dados a serem adicionadas ao modelo de dados de formulário. Todas as fontes de dados configuradas em `global` e o nó de configuração selecionado, se houver, são exibidos.

   * Para substituir uma fonte de dados existente por outra fonte de dados do mesmo tipo, selecione o ícone **[!UICONTROL Editar]** para a fonte de dados e selecione na lista de fontes de dados disponíveis.
   * Para excluir uma fonte de dados existente, selecione o ícone **[!UICONTROL Excluir]** para a fonte de dados. O ícone Excluir será desativado se um objeto de modelo de dados na fonte de dados for adicionado no modelo de dados de formulário.

   ![propriedades-fdm](assets/fdm-properties.png)

1. Selecione **[!UICONTROL Salvar e fechar]** para salvar as atualizações.

>[!NOTE]
>
>Depois de adicionar novas fontes de dados ou atualizar fontes de dados existentes em um modelo de dados de formulário, atualize as referências de associação, conforme apropriado, nos formulários adaptáveis e nas comunicações interativas que usam o modelo de dados de formulário atualizado.

## Próximas etapas {#next-steps}

Agora você tem um modelo de dados de formulário com fontes de dados adicionadas a ele. Em seguida, você pode editar o modelo de dados de formulário para adicionar e configurar objetos e serviços de modelo de dados, adicionar associações entre objetos de modelo de dados, editar propriedades, adicionar objetos e propriedades de modelo de dados personalizados, gerar dados de amostra e assim por diante.

Para obter mais informações, consulte [Trabalhar com o modelo de dados de formulário](../../forms/using/work-with-form-data-model.md).
