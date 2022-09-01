---
title: Como integrar o AEM Forms com o Adobe Analytics?
seo-title: Learn how to integrate AEM Forms with Adobe Analytics.
description: O AEM Forms integra-se com o Adobe Analytics para capturar e rastrear métricas de desempenho para seus formulários publicados.
seo-description: To discover interaction patterns and problems users face while using adaptive forms.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '1720'
ht-degree: 0%

---

# Integrar com a [!DNL Adobe Analytics] {#integrate-aem-forms-with-adobe-analytics}

O AEM Forms integra-se ao [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en) para permitir capturar e rastrear métricas de desempenho para seus formulários publicados. O objetivo por trás da análise dessas métricas é permitir que os usuários corporativos obtenham insights sobre o comportamento do usuário final e otimizem a experiência de captura de dados. Você pode capturar e rastrear o comportamento de usuários conectados e não conectados (anônimos) pelo Adobe Analytics for Adaptive Forms.

Depois de executar as ações mencionadas neste artigo, você pode configurar e exibir os relatórios em [!DNL Adobe Analytics], conforme demonstrado no vídeo a seguir:

>[!VIDEO](https://video.tv.adobe.com/v/337262)

Você pode usar [!DNL Adobe Analytics] para descobrir padrões e problemas de interação que os usuários enfrentam ao usar formulários adaptáveis. Pronto para uso, [!DNL Adobe Analytics] rastreia e armazena informações sobre os seguintes eventos:

* **Renderizar**: Número de vezes que um formulário é aberto.

* **Enviar**: Número de vezes que um formulário é enviado.

* **Abandono**: Número de vezes que os usuários saem sem preencher o formulário.

* **Erro**: Número de erros encontrados no painel e nos campos do painel.

* **Ajuda**: Número de vezes que um usuário abre a ajuda de um painel e os campos do painel.

* **Visita em campo**: Número de vezes que um usuário visita um campo no formulário.

* **Salvar**: Número de vezes que os usuários salvam um formulário no Portal do Forms.

Além desses eventos prontos para uso, você pode definir eventos personalizados em formulários adaptáveis usando o editor de regras e mapear esses eventos para eventos em [!DNL Adobe Analytics]

A figura a seguir ilustra as ações que você precisa executar antes de visualizar os relatórios em [!DNL Adobe Analytics]:

![Visão geral do Analytics](/help/forms/using/assets/analytics-workflow.png)

## 1. Configurar [!DNL Adobe Analytics] {#Configure-adobe-analytics}

Antes de configurar [!DNL Adobe Analytics], criar:

* Uma Adobe ID para fazer logon no [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* A [conjunto de relatórios](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).


### Instalar o AEM Forms e [!DNL Adobe Analytics] extensões {#install-extensions}

Execute as etapas a seguir para configurar o AEM Forms e [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html) extensões:

1. Faça logon no Adobe Experience Cloud e selecione um nome apropriado para a empresa.

1. Toque **[!UICONTROL Launch/Coleta de dados]** e tocar **[!UICONTROL Ir para Launch/Data Collection]**.

1. Toque **[!UICONTROL Nova propriedade]** e especifique um nome para a configuração.

1. Especifique um nome de domínio e toque em **[!UICONTROL Salvar]** para salvar a propriedade.

1. Toque no nome da configuração disponível na lista de Propriedades da tag.

1. No **[!UICONTROL Criação]** seção, toque em **[!UICONTROL Extensões]**.

1. Toque **[!UICONTROL Catálogo]** e tocar **[!UICONTROL Instalar]** para **[!UICONTROL Adobe Experience Manager Forms]** extensão. **[!UICONTROL Adobe Experience Manager Forms]** é exibida na lista de extensões instaladas disponível no **Instalado** guia .

1. Toque **[!UICONTROL Instalar]** para **[!UICONTROL Adobe Analytics]** extensão.
1. Selecione o nome do conjunto de relatórios no **[!UICONTROL Conjuntos de relatórios de desenvolvimento]**, **[!UICONTROL Conjuntos de relatórios de preparo]** e **[!UICONTROL Conjuntos de relatórios do produto]** listas suspensas e toque em **[!UICONTROL Salvar]** para salvar a extensão do .

### Configurar elementos de dados {#configure-data-elements}

Você pode selecionar qualquer um dos elementos de dados configurados em uma regra criada para um evento. Quando um evento ocorre em um formulário adaptável, o AEM Forms envia esses elementos de dados para o [!DNL Adobe Analytics].

Depois de instalar o **[!UICONTROL Adobe Experience Manager Forms]** , você pode criar os seguintes elementos de dados:

<table>
 <tbody>
  <tr>
   <td>FieldName</th>
   <td>FieldTitle</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>FormName<br /> </td>
   <td>FormTitle<br /> </td>
   <td>PageName</td>
  </tr>
  <tr>
   <td>PageURL<br /> </td>
   <td>TítuloDoPainel<br /> </td>
   <td>TimeSpent</td>
  </tr>
 </tbody>
</table>

Execute as seguintes etapas para configurar elementos de dados:

1. No **[!UICONTROL Criação]** seção, toque em **[!UICONTROL Elementos de dados]**.

1. Toque **[!UICONTROL Criar novo elemento de dados]**.

1. Especifique um nome para o Elemento de dados. Por exemplo, Título do formulário para o tipo de elemento de dados FormTitle .

1. Especificar **[!UICONTROL Adobe Experience Manager Forms]** como o nome da Extensão.

1. Selecione o **[!UICONTROL Tipo de elemento de dados]**.

1. Toque **[!UICONTROL Salvar]** para salvar o elemento de dados.

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### Configurar regras {#configure-rules}

Execute as etapas a seguir para criar regras baseadas no **[!UICONTROL Adobe Experience Manager Forms]** extensão:

1. No **[!UICONTROL Criação]** seção, toque em **[!UICONTROL Regras]**.

1. Toque **[!UICONTROL Criar nova regra]**.

1. Especifique um nome para a Regra. Por exemplo, Enviar formulário para registrar os envios de formulário.

1. No **[!UICONTROL Eventos]** seção, toque em **[!UICONTROL Adicionar]**.

1. Especificar **[!UICONTROL Adobe Experience Manager Forms]** como o nome da Extensão.

1. Selecione o tipo de evento. A entrada para o **[!UICONTROL Nome]** O campo é preenchido automaticamente com base no tipo de evento selecionado.

1. Toque **[!UICONTROL Manter alterações]** para salvar o evento.

1. No **[!UICONTROL Ações]** seção, toque em **[!UICONTROL Adicionar]**.

1. Especificar **[!UICONTROL Adobe Analytics]** como o nome da Extensão.

1. Selecionar **[!UICONTROL Definir variáveis]** como Tipo de ação. As opções disponíveis na lista suspensa incluem:

   * **[!UICONTROL Definir variáveis]**: Use esse tipo de ação para definir o tipo de evento para o qual os elementos de dados selecionados são enviados do AEM Forms para [!DNL Adobe Analytics].

   * **[!UICONTROL Enviar beacon]**: Use esse tipo de ação para enviar dados do AEM Forms para o [!DNL Adobe Analytics].

   * **[!UICONTROL Limpar variáveis]**: Use esse tipo de ação para limpar a trilha de dados para que o evento se registre apenas uma vez em [!DNL Adobe Analytics].

      A abordagem recomendada é usar o **[!UICONTROL Definir variáveis]** tipo de ação para configurar o evento e os elementos de dados, em seguida, use **[!UICONTROL Enviar beacon]** para enviar dados e, em seguida, usar **[!UICONTROL Limpar variáveis]** para limpar a trilha de dados.

1. No **[!UICONTROL Props]** mapeie as opções do conjunto de relatórios disponíveis na lista suspensa com os elementos de dados definidos usando [Configurar elementos de dados](#configure-data-elements).

   Por exemplo, para enviar **Título do formulário** elemento de dados do AEM Forms para o [!DNL Adobe Analytics] ao enviar um formulário:
   1. No **[!UICONTROL Props]** , selecione uma prop para o Título do formulário disponível no conjunto de relatórios e toque em ![Ícone do banco de dados](/help/forms/using/assets/database-icon.svg) para mapeá-lo para o Título do formulário criado em [Configurar elementos de dados](#configure-data-elements).

      ![define-props](/help/forms/using/assets/define-props.png)

   1. Toque **[!UICONTROL Adicionar outro]** para adicionar mais elementos de dados à lista.

1. No **[!UICONTROL Eventos]** selecione um evento nas opções disponíveis no conjunto de relatórios e toque em **[!UICONTROL Manter alterações]**.

1. No **[!UICONTROL Ações]** toque em + e especifique **[!UICONTROL Adobe Analytics]** como o nome da Extensão.

1. Selecionar **[!UICONTROL Enviar beacon]** como Tipo de ação. No painel direito, selecione **[!UICONTROL s.t()]** para enviar dados para [!DNL Adobe Analytics] e tratá-la como uma exibição de página ou **[!UICONTROL s.tl()]** para enviar dados para [!DNL Adobe Analytics] e não tratá-la como uma exibição de página. Toque **[!UICONTROL Manter alterações]**.

1. No **[!UICONTROL Ações]** toque em + e especifique **[!UICONTROL Adobe Analytics]** como o nome da Extensão.

1. Selecionar **[!UICONTROL Limpar variáveis]** como Tipo de ação. Toque **[!UICONTROL Manter alterações]**. Depois de executar essas etapas, a **[!UICONTROL Ações]** é exibida como:
   ![Configuração de ações](/help/forms/using/assets/actions-config.png)

   Personalize o **[!UICONTROL Ações]** de acordo com suas necessidades. Por exemplo, você pode definir dois **Enviar beacon** etapas em um fluxo Ações para enviar dados para [!DNL Adobe Analytics] e tratá-la como uma visualização de página em uma etapa e enviar dados para o [!DNL Adobe Analytics] e não tratá-la como uma visualização de página na segunda etapa.

   ![Configuração de ações](/help/forms/using/assets/actions-config-2.png)

1. Toque **[!UICONTROL Salvar]** para salvar a regra.

   Você pode criar regras para todos os tipos de eventos, como Abandono, Erro, Visita em campo, Ajuda, Renderizar, Salvar e Enviar.

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### Fluxos de publicação {#publish-flow}

Depois de criar os elementos de dados e usá-los nas regras, publique a configuração para coletar dados do formulário no [!DNL Adobe Analytics].

Execute as seguintes etapas para publicar a configuração:

1. No **[!UICONTROL Publicação]** seção, toque em **[!UICONTROL Fluxo de publicação]**.

1. Toque **[!UICONTROL Adicionar biblioteca]** e especifique um nome e selecione o ambiente para a biblioteca.

1. Toque **[!UICONTROL Adicionar todos os recursos alterados]** em seguida, toque em **[!UICONTROL Salvar e criar no desenvolvimento]**.

1. No **[!UICONTROL Desenvolvimento]** seção, toque em ![Mais opções](/help/forms/using/assets/more-options-icon.svg) em seguida, toque em **[!UICONTROL Aprovar e publicar na produção]**.

1. Confirme as alterações e o fluxo de publicação será exibido em breve no **[!UICONTROL Publicado]** seção.

![Fluxo de publicação](/help/forms/using/assets/publish-flow.png)

## 2. Configurar o AEM Forms {#configure-aem-forms}

Antes de criar a configuração do Adobe Launch, crie um [Configuração do Adobe IMS usando o Adobe Launch como a solução da nuvem](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

### Criar configuração do Adobe Launch {#create-adobe-launch-configuration}

Execute as seguintes etapas para criar uma configuração do Adobe Launch:

1. Na instância do autor do AEM Forms, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurações do Adobe Launch]**.

1. Selecione uma pasta para criar a configuração e toque em **[!UICONTROL Criar]**.

1. Especifique um título para a configuração no **[!UICONTROL Título]** campo.

1. Selecione o [configuração associada do Adobe IMS](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

1. Selecione o nome da empresa usada durante [configuração do Adobe Analytics](#Configure-adobe-analytics).

1. Selecione o nome da propriedade criada enquanto [configuração do Adobe Analytics](#install-extensions).

1. Toque **[!UICONTROL Salvar e fechar]**.

1. Publique a configuração.

### Habilitar [!DNL Adobe Analytics] para um formulário adaptável {#enable-analytics-adaptive-form}

Para usar [!DNL Adobe Launch] configuração em um formulário adaptável existente:

1. Na instância do autor do AEM Forms, navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Selecione o formulário adaptável e toque em **[!UICONTROL Propriedades]**.
1. No **[!UICONTROL Básico]** selecione a guia [contêiner de configuração](#create-adobe-launch-configuration) usada ao criar a configuração do Adobe Launch.
1. Toque **[!UICONTROL Salvar e fechar]**. O formulário adaptável está ativado para [!DNL Adobe Analytics].
1. Publicar o formulário.

Depois de ativar [!DNL Adobe Analytics] para um formulário adaptável, é possível [validate](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon) se houver um fluxo de evento de dados apropriado entre a AEM Forms e a [!DNL Adobe Analytics]. A integração do AEM Forms com o Adobe Analytics foi concluída. Agora você pode [configurar e exibir relatórios no Adobe Analytics](#view-reports-adobe-analytics).

>[!NOTE]
>No caso de ambos [Analytics herdado](/help/forms/using/configure-analytics-forms-documents.md) e os recursos do Launch Analytics são ativados simultaneamente, **Iniciar o Analytics** terá precedência.

### Criar regras para capturar eventos personalizados (Opcional) {#capture-custom-events}

Crie regras em campos específicos de um formulário adaptável usando o editor de regras para enviar dados do Analytics de um formulário adaptável para [!DNL Adobe Analytics].

Em um processo de duas etapas, é possível definir uma regra em um campo em um formulário adaptável. A regra despacha um evento. O nome do evento é mapeado para um evento de captura personalizado no Adobe Launch.

Para criar regras usando o editor de regras em um formulário adaptável:

1. Toque no campo e selecione ![Editor de regras](/help/forms/using/assets/edit-rules-icon.svg) para abrir a página do editor de regras.
1. Defina uma condição no [!UICONTROL When] da regra.
1. No [!UICONTROL Então] da regra, selecione **[!UICONTROL Evento de despacho]** do **[!UICONTROL Selecionar ação]** lista suspensa.
1. Especifique o nome do evento no **[!UICONTROL Nome do evento de tipo]** campo.

Por exemplo, se a data de nascimento for antes de uma determinada data, o AEM Forms despachará o **Segurança** evento.

![Evento de envio](/help/forms/using/assets/security-event.png)

Para mapear o evento para um evento de captura personalizado em [!DNL Adobe Analytics]:

1. [Criar uma regra](#configure-rules).

1. No **[!UICONTROL Eventos]** seção, toque em **[!UICONTROL Adicionar]**.

1. Especificar **[!UICONTROL Adobe Experience Manager Forms]** como o nome da Extensão.

1. Selecionar **[!UICONTROL Capturar evento personalizado]** do **[!UICONTROL Tipo de evento]** lista suspensa.

1. Especifique o nome do evento especificado na etapa 4 ao criar uma regra usando o editor de regras.

1. Toque **Manter alterações** e executar o resto das ações especificadas em [Configurar regras](#configure-rules).

## 3. Configure e exiba relatórios em [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

Após configurar um formulário adaptável para enviar dados de evento para o [!DNL Adobe Analytics], você pode começar a visualizar relatórios em [!DNL Adobe Analytics]:

1. Toque ![Selecionar produto](/help/forms/using/assets/select-analytics.png) e selecione **[!UICONTROL Analytics]**.

1. Toque **[!UICONTROL Criar projeto]** e selecione **[!UICONTROL Projeto em branco]**.

1. Selecione o nome do conjunto de relatórios na lista suspensa na parte superior direita da forma livre.

1. Especificar **Título do formulário** no **[!UICONTROL Pesquisar itens de dimensão]** texto para exibir todos os títulos do formulário.

1. Solte o título do formulário adaptável no **[!UICONTROL Solte um segmento aqui (ou qualquer outro componente)]** caixa de texto.

1. No **[!UICONTROL Métricas]** , solte os eventos para rastrear **[!UICONTROL Solte uma métrica aqui (ou qualquer outro componente)]** caixa de texto.

1. Toque ![Visualizações](/help/forms/using/assets/visualization-icon.svg) e solte um tipo de gráfico na seção Forma livre . Da mesma forma, é possível adicionar vários tipos de gráfico à seção Forma livre .

1. Toque nas teclas Ctrl + S e especifique um nome para salvar o projeto.