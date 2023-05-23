---
title: Como integrar o AEM Forms com o Adobe Analytics?
description: O AEM Forms integra-se ao Adobe Analytics para capturar e rastrear métricas de desempenho para seus formulários publicados.
docset: aem65
exl-id: 030fe9f2-cd41-4290-b8a6-2f9ade6b5789
source-git-commit: 45ca98ffb68e1e31e2f45f352e86f5aa1b6f0f00
workflow-type: tm+mt
source-wordcount: '1806'
ht-degree: 0%

---

# Analytics usando [!DNL Adobe Launch] {#analyticsusingadobelaunch}

O AEM Forms integra-se com [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en) para permitir que você capture e rastreie métricas de desempenho para seus formulários publicados. O objetivo por trás da análise dessas métricas é permitir que os usuários empresariais obtenham insights sobre o comportamento do usuário final e otimizem a experiência de captura de dados. Você pode capturar e rastrear o comportamento de usuários conectados e não conectados (anônimos) por meio do Adobe Analytics para Forms adaptável.

Também é possível executar a análise usando a Estrutura Cloud Service. Para obter mais informações sobre como integrar o AEM Forms com o Cloud Service Framework, consulte [Analytics usando a estrutura Cloud Service](/help/forms/using/configure-analytics-forms-documents.md). A principal vantagem de usar o Adobe Launch em relação ao Analytics usando a Estrutura de Cloud Service é que você também pode definir eventos personalizados, além desses eventos prontos para uso. Os eventos personalizados são definidos usando o editor de regras ou clientlibs do cliente e são mapeados para eventos no [!DNL Adobe Analytics].

Depois de executar as ações mencionadas neste artigo, você pode configurar e visualizar relatórios em [!DNL Adobe Analytics], conforme demonstrado no vídeo a seguir:

>[!VIDEO](https://video.tv.adobe.com/v/337262)

Você pode usar [!DNL Adobe Analytics] para descobrir padrões de interação e problemas que os usuários enfrentam ao usar formulários adaptáveis. Pronto para uso, [!DNL Adobe Analytics] O rastreia e armazena informações sobre os seguintes eventos:

* **Renderizar**: Número de vezes que um formulário é aberto.

* **Enviar**: Número de vezes que um formulário é enviado.

* **Abandona**: Número de vezes que os usuários saem sem preencher o formulário.

* **Erro**: Número de erros encontrados no painel e nos campos do painel.

* **Ajuda**: Número de vezes que um usuário abre a ajuda de um painel e os campos do painel.

* **Visita de campo**: Número de vezes que um usuário visita um campo no formulário.

* **Salvar**: Número de vezes que os usuários salvam um formulário no Portal do Forms.

Além desses eventos prontos para uso, também é possível definir eventos personalizados.

A figura a seguir ilustra as ações que devem ser executadas antes de exibir relatórios no [!DNL Adobe Analytics]:

![Visão geral do Analytics](/help/forms/using/assets/analyticsworkflow.png)

## 1. Configurar [!DNL Adobe Analytics] {#Configure-adobe-analytics}

Antes de configurar [!DNL Adobe Analytics], criar:

* Um Adobe ID para fazer logon no [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* A [conjunto de relatórios](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).


### Instale o AEM Forms e [!DNL Adobe Analytics] extensões {#install-extensions}

Execute as seguintes etapas para configurar o AEM Forms e o [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html) extensões:

1. Faça logon no Adobe Experience Cloud e selecione um nome apropriado para a empresa.

1. Toque **[!UICONTROL Launch/Coleção de dados]** e toque em **[!UICONTROL Ir para Launch/Coleção de dados]**.

1. Toque **[!UICONTROL Nova propriedade]** e especifique um nome para a configuração.

1. Especifique um nome de domínio e toque em **[!UICONTROL Salvar]** para salvar a propriedade.

1. Toque no nome da configuração disponível na lista de Propriedades da tag.

1. No **[!UICONTROL Criação]** seção, toque em **[!UICONTROL Extensões]**.

1. Toque **[!UICONTROL Catálogo]** e toque em **[!UICONTROL Instalar]** para o **[!UICONTROL Adobe Experience Manager Forms]** extensão. **[!UICONTROL Adobe Experience Manager Forms]** é exibida na lista de extensões instaladas disponíveis na **Instalado** guia.

1. Toque **[!UICONTROL Instalar]** para o **[!UICONTROL Adobe Analytics]** extensão.
1. Selecione o nome do conjunto de relatórios na **[!UICONTROL Conjuntos de relatórios de desenvolvimento]**, **[!UICONTROL Preparação de conjuntos de relatórios]**, e **[!UICONTROL Conjuntos de relatórios do produto]** listas suspensas e toque em **[!UICONTROL Salvar]** para salvar a extensão.

### Configurar elementos de dados {#configure-data-elements}

Você pode selecionar qualquer um dos elementos de dados configurados em uma regra criada para um evento. Quando um evento ocorre em um formulário adaptável, o AEM Forms envia esses elementos de dados para o [!DNL Adobe Analytics].

Após instalar o **[!UICONTROL Adobe Experience Manager Forms]** você poderá criar os seguintes elementos de dados:

<table>
 <tbody>
  <tr>
   <td>NomeCampo</th>
   <td>TítuloDoCampo</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>FormName<br /> </td>
   <td>Título do formulário<br /> </td>
   <td>PageName</td>
  </tr>
  <tr>
   <td>PageURL<br /> </td>
   <td>PanelTitle<br /> </td>
   <td>Tempo gasto</td>
  </tr>
 </tbody>
</table>

Execute as seguintes etapas para configurar elementos de dados:

1. No **[!UICONTROL Criação]** seção, toque em **[!UICONTROL Elementos de dados]**.

1. Toque **[!UICONTROL Criar novo elemento de dados]**.

1. Especifique um nome para o Elemento de dados. Por exemplo, Título do formulário para o tipo de elemento de dados FormTitle.

1. Especificar **[!UICONTROL Adobe Experience Manager Forms]** como o Nome da extensão.

1. Selecione o **[!UICONTROL Tipo de elemento de dados]**.

1. Toque **[!UICONTROL Salvar]** para salvar o elemento de dados.

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### Configurar regras {#configure-rules}

Execute as seguintes etapas para criar regras com base na **[!UICONTROL Adobe Experience Manager Forms]** extensão:

1. No **[!UICONTROL Criação]** seção, toque em **[!UICONTROL Regras]**.

1. Toque **[!UICONTROL Criar nova regra]**.

1. Especifique um nome para a Regra. Por exemplo, Envio de formulário para registrar envios de formulário.

1. No **[!UICONTROL Eventos]** seção, toque em **[!UICONTROL Adicionar]**.

1. Especificar **[!UICONTROL Adobe Experience Manager Forms]** como o Nome da extensão.

1. Selecione o tipo de evento. A entrada para o **[!UICONTROL Nome]** O campo é preenchido automaticamente com base no tipo de evento selecionado.

1. Toque **[!UICONTROL Manter alterações]** para salvar o evento.

1. No **[!UICONTROL Ações]** seção, toque em **[!UICONTROL Adicionar]**.

1. Especificar **[!UICONTROL Adobe Analytics]** como o Nome da extensão.

1. Selecionar **[!UICONTROL Definir variáveis]** como o Tipo de ação. As opções disponíveis na lista suspensa incluem:

   * **[!UICONTROL Definir variáveis]**: use esse tipo de ação para definir o tipo de evento para o qual os elementos de dados selecionados são enviados do AEM Forms para o [!DNL Adobe Analytics].

   * **[!UICONTROL Enviar sinal]**: use esse tipo de ação para enviar dados do AEM Forms para o [!DNL Adobe Analytics].

   * **[!UICONTROL Limpar variáveis]**: use esse tipo de ação para limpar a trilha de dados para que o evento seja registrado apenas uma vez em [!DNL Adobe Analytics].

      A abordagem recomendada é utilizar a **[!UICONTROL Definir variáveis]** tipo de ação para configurar o evento e os elementos de dados, depois use **[!UICONTROL Enviar sinal]** para enviar dados e, em seguida, usar **[!UICONTROL Limpar variáveis]** para limpar a trilha de dados.

1. No **[!UICONTROL Props]** mapeie as opções do conjunto de relatórios disponíveis na lista suspensa com os elementos de dados definidos com o [Configurar elementos de dados](#configure-data-elements).

   Por exemplo, para enviar **Título do formulário** elemento de dados do AEM Forms para [!DNL Adobe Analytics] ao enviar um formulário:
   1. No **[!UICONTROL Props]** selecione uma prop para Título do formulário disponível no conjunto de relatórios e toque em ![Ícone do banco de dados](/help/forms/using/assets/database-icon.svg) para mapeá-lo para o Título do formulário criado em [Configurar elementos de dados](#configure-data-elements).

      ![define-props](/help/forms/using/assets/define-props.png)

   1. Toque **[!UICONTROL Adicionar outro]** para adicionar mais elementos de dados à lista.

1. No **[!UICONTROL Eventos]** selecione um evento entre as opções disponíveis no conjunto de relatórios e toque em **[!UICONTROL Manter alterações]**.

1. No **[!UICONTROL Ações]** seção, toque em + e especifique **[!UICONTROL Adobe Analytics]** como o Nome da extensão.

1. Selecionar **[!UICONTROL Enviar sinal]** como o Tipo de ação. No painel direito, selecione **[!UICONTROL s.t()]** para enviar dados ao [!DNL Adobe Analytics] e trate-o como uma exibição de página ou **[!UICONTROL s.tl()]** para enviar dados ao [!DNL Adobe Analytics] e não a trate como uma exibição de página. Toque **[!UICONTROL Manter alterações]**.

1. No **[!UICONTROL Ações]** seção, toque em + e especifique **[!UICONTROL Adobe Analytics]** como o Nome da extensão.

1. Selecionar **[!UICONTROL Limpar variáveis]** como o Tipo de ação. Toque **[!UICONTROL Manter alterações]**. Após executar essas etapas, a variável **[!UICONTROL Ações]** é exibida como:
   ![Configuração de ações](/help/forms/using/assets/actions-config.png)

   Personalize o **[!UICONTROL Ações]** seção de acordo com suas necessidades. Por exemplo, você pode definir dois **Enviar sinal** etapas em um fluxo de Ações para enviar dados para o [!DNL Adobe Analytics] e trate-a como uma exibição de página em uma etapa e envie dados para [!DNL Adobe Analytics] e não a trate como uma exibição de página na segunda etapa.

   ![Configuração de ações](/help/forms/using/assets/actions-config-2.png)

1. Toque **[!UICONTROL Salvar]** para salvar a regra.

   Você pode criar regras para todos os tipos de evento, como Abandonar, Erro, Visita de campo, Ajuda, Renderizar, Salvar e Enviar.

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### Fluxos de publicação {#publish-flow}

Depois de criar os elementos de dados e usá-los nas regras, publique a configuração para coletar dados do formulário no [!DNL Adobe Analytics].

Execute as seguintes etapas para publicar a configuração:

1. No **[!UICONTROL Publicação]** seção, toque em **[!UICONTROL Fluxo de publicação]**.

1. Toque **[!UICONTROL Adicionar biblioteca]** e especifique um nome e selecione o ambiente para a biblioteca.

1. Toque **[!UICONTROL Adicionar todos os recursos alterados]** e toque em **[!UICONTROL Salvar e criar no desenvolvimento]**.

1. No **[!UICONTROL Desenvolvimento]** seção, toque em ![Mais opções](/help/forms/using/assets/more-options-icon.svg) e toque em **[!UICONTROL Aprovar e publicar na produção]**.

1. Confirme as alterações e o fluxo de publicação será exibido em breve na **[!UICONTROL Publicado]** seção.

![Fluxo de publicação](/help/forms/using/assets/publish-flow.png)

## 2. Configurar o AEM Forms {#configure-aem-forms}

Antes de criar a configuração do Adobe Launch, crie um [Configuração do Adobe IMS usando o Adobe Launch como a solução em nuvem](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

### Criar configuração do Adobe Launch {#create-adobe-launch-configuration}

Execute as seguintes etapas para criar uma configuração do Adobe Launch:

1. Na instância do autor do AEM Forms, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configurações do Adobe Launch]**.

1. Selecione uma pasta para criar a configuração e toque em **[!UICONTROL Criar]**.

1. Especifique um título para a configuração no campo **[!UICONTROL Título]** campo.

1. Selecione o [configuração IMS da Adobe associada](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

1. Selecione o nome da empresa usada enquanto [configuração do Adobe Analytics](#Configure-adobe-analytics).

1. Selecione o nome da propriedade criada enquanto [configuração do Adobe Analytics](#install-extensions).

1. Toque **[!UICONTROL Salvar e fechar]**.

1. Publique a configuração.

### Ativar [!DNL Adobe Analytics] para um formulário adaptável {#enable-analytics-adaptive-form}

Para usar [!DNL Adobe Launch] em um Formulário adaptável existente:

1. Na instância do autor do AEM Forms, navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]**.
1. Selecione o Formulário adaptável e toque em **[!UICONTROL Propriedades]**.
1. No **[!UICONTROL Básico]** , selecione a [contêiner de configuração](#create-adobe-launch-configuration) usado ao criar a configuração do Adobe Launch.
1. Toque **[!UICONTROL Salvar e fechar]**. O formulário adaptável está ativado para [!DNL Adobe Analytics].
1. Publique o formulário.

Depois de habilitar [!DNL Adobe Analytics] para um formulário adaptável, é possível [validar](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon) se houver um fluxo de evento de dados apropriado entre o AEM Forms e [!DNL Adobe Analytics]. A integração do AEM Forms com o Adobe Analytics está concluída. Agora você pode [configurar e exibir relatórios no Adobe Analytics](#view-reports-adobe-analytics).

>[!NOTE]
>Se ambos [Analytics usando a estrutura Cloud Service](/help/forms/using/configure-analytics-forms-documents.md) e **Analytics usando o Adobe Launch** recursos são ativados simultaneamente, **Analytics usando o Adobe Launch** terá precedência.

### Criar regras para capturar eventos personalizados (Opcional) {#capture-custom-events}

Crie regras em campos específicos de um formulário adaptável usando o editor de regras para enviar dados do Analytics de um formulário adaptável para o [!DNL Adobe Analytics].

Em um processo de dois estágios, você define uma regra em um campo em um formulário adaptável. A regra despacha um evento. O nome do evento é mapeado para um evento de captura personalizado no Adobe Launch.

Para criar regras usando o editor de regras em um formulário adaptável:

1. Toque no campo e selecione ![Editor de regras](/help/forms/using/assets/rule-editor-icon.svg) para abrir a página do editor de regras.
1. Defina uma condição no campo [!UICONTROL Quando] seção da regra.
1. No [!UICONTROL Depois] da regra, selecione **[!UICONTROL Evento de envio]** do **[!UICONTROL Selecionar ação]** lista suspensa.
1. Especifique o nome do evento na variável **[!UICONTROL Digite o nome do evento]** campo.

Por exemplo, se a data de nascimento for anterior a uma determinada data, o AEM Forms enviará o **Segurança** evento.

![Evento de envio](/help/forms/using/assets/security-event.png)

Para mapear o evento para um evento de captura personalizado no [!DNL Adobe Analytics]:

1. [Criar uma regra](#configure-rules).

1. No **[!UICONTROL Eventos]** seção, toque em **[!UICONTROL Adicionar]**.

1. Especificar **[!UICONTROL Adobe Experience Manager Forms]** como o Nome da extensão.

1. Selecionar **[!UICONTROL Capturar evento personalizado]** do **[!UICONTROL Tipo de evento]** lista suspensa.

1. Especifique o nome do evento especificado na etapa 4 ao criar uma regra usando o editor de regras.

1. Toque **Manter alterações** e executar o restante das ações especificadas no [Configurar regras](#configure-rules).

## 3. Configurar e exibir relatórios no [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

Depois de configurar um formulário adaptável para enviar dados do evento para o [!DNL Adobe Analytics], é possível começar a exibir relatórios no [!DNL Adobe Analytics]:

1. Toque ![Selecionar produto](/help/forms/using/assets/select-analytics.png) e selecione **[!UICONTROL Analytics]**.

1. Toque **[!UICONTROL Criar projeto]** e selecione **[!UICONTROL Projeto em branco]**.

1. Selecione o nome do conjunto de relatórios na lista suspensa na parte superior direita da forma livre.

1. Especificar **Título do formulário** no **[!UICONTROL Pesquisar itens de dimensão]** texto para exibir todos os títulos de formulário.

1. Solte o título do formulário adaptável para a **[!UICONTROL Solte um segmento aqui (ou qualquer outro componente)]** texto.

1. No **[!UICONTROL Métricas]** solte os eventos a serem rastreados para **[!UICONTROL Solte uma métrica aqui (ou qualquer outro componente)]** texto.

1. Toque ![Visualizações](/help/forms/using/assets/visualization-icon.svg) e solte um tipo de gráfico na seção Forma livre. Da mesma forma, você pode adicionar vários tipos de gráfico à seção Forma livre.

1. Toque em Ctrl + S chaves e especifique um nome para salvar o projeto.

Para obter informações detalhadas sobre a exibição de relatórios de análise de formulários, consulte [Visualização e compreensão de relatórios do AEM Forms Analytics](../../forms/using/view-understand-aem-forms-analytics-reports.md).
