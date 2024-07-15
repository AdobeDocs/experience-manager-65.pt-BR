---
title: Criação de uma página do portal de formulários
description: O Forms Portal equipe os desenvolvedores da Web com componentes para criar e personalizar um portal de formulários em sites criados usando o Adobe Experience Manager (AEM).
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
feature: Forms Portal
exl-id: 22d7c24e-7a77-4324-afdf-74c1fbf15773
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 2%

---

# Criação de uma página do portal de formulários{#creating-a-forms-portal-page}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

Os componentes do portal do Forms equipam os desenvolvedores da Web com componentes para criar e personalizar um portal de formulários em sites criados usando o Adobe Experience Manager (AEM). Para obter uma visão geral rápida do portal de formulários, consulte [Introdução à publicação de formulários em um portal](../../forms/using/introduction-publishing-forms.md).

## Pré-requisitos {#prerequisites}

Os componentes do portal do Forms não estão disponíveis para uso por padrão. Verifique se as seguintes categorias de componentes do portal de formulários estão habilitadas conforme descrito em [Habilitando componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md).

**Serviços de documentos** Inclui os componentes Pesquisa e Listagem, Link e Rascunhos e Envios.

**Predicados De Serviços De Documento** Inclui Predicado De Data, Predicado De Texto Completo, Predicado De Propriedades E Componentes De Predicado De Marcas. Esses componentes são usados para configurar a pesquisa no componente Pesquisa e Lister.

Uma vez ativadas em uma página de sites AEM, essas categorias de componentes ficam disponíveis para uso no navegador de componentes.

![Componentes do portal do AEM Forms no navegador de componentes](assets/component-categories.png)

Categorias de componentes do portal do Forms

## Componente de pesquisa e listagem {#search-amp-lister-component}

O componente de Pesquisa e listagem, disponível na categoria de componente Serviços de documento, é usado para listar formulários em uma página e implementar a pesquisa nos formulários listados. O componente inclui dois painéis:

* Painel Lista onde os formulários são listados.
* Painel de pesquisa no qual você adiciona a funcionalidade de pesquisa.

Você pode arrastar e soltar o componente Pesquisa e lista da categoria de componentes Serviços de documento no navegador de componentes para a página. O componente, quando adicionado, é semelhante ao seguinte.

![Componente de Pesquisa e Lister em uma página](assets/fp-grid-viw.png)

Componente de Pesquisa e Lister em uma página com layout de Grade

### Painel Lista {#list-pane}

O painel Lista é uma área na qual os formulários são listados. O componente de Pesquisa e Lister fornece várias opções de configuração que você pode usar para controlar a exibição de formulários no painel Lista.

Para configurar o painel Lista, selecione o componente Pesquisa e Lister e selecione ![settings_icon](assets/settings_icon.png). A caixa de diálogo **[!UICONTROL Editar Componente]** é aberta.

![Painel de lista no modo de edição](assets/edit-list.png)

Painel Lista no modo de edição

A caixa de diálogo **Editar** inclui várias guias que fornecem opções de configuração descritas na tabela abaixo. Selecione **OK** para salvar a configuração, quando terminar.

<table>
 <tbody>
  <tr>
   <th>Guia</th>
   <th>Configuração</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Pastas de ativos</strong></code></td>
   <td>Adicionar item</td>
   <td>Configura as pastas em que os ativos são carregados usando a interface do usuário do AEM Forms. Por padrão, ele lista todos os ativos carregados. Para obter mais informações sobre a interface do AEM Forms, consulte <a href="../../forms/using/introduction-managing-forms.md" target="_blank">Introdução ao gerenciamento de formulários</a>.</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>Exibir</strong></code></p> </td>
   <td>Texto do título</td>
   <td>Título para o componente de Pesquisa e Lister. O título padrão é <strong>Forms Portal.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Modelo de layout</td>
   <td>Layout dos ativos. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Desativar pesquisa avançada</td>
   <td>Quando ativado, oculta o ícone de pesquisa avançada.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Desativar pesquisa de texto</td>
   <td>Quando ativado, oculta a barra de pesquisa de texto completo.</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Resultado</strong></code></td>
   <td>Número De Resultados Por Página</td>
   <td>Configura o número máximo de formulários que você deseja exibir em uma página.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Texto de resultados</td>
   <td><p>Configura o texto de resultados (por exemplo, 1-12 de 601 <strong>Resultados</strong>). O valor padrão é <strong>Resultados</strong>.</p> <p>Por exemplo, se você especificar <strong>Forms </strong>neste campo e houver um total de 601 formulários, o texto resultante será alterado para 1-12 de 601 <strong>Forms.</strong></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Texto da página</td>
   <td><p>Configura o texto da página (por exemplo, <strong>Página </strong>1 de 51). O valor padrão é <strong>Página</strong>.</p> <p>Por exemplo, se você especificar <strong>Formulário de Aplicativo </strong>neste campo e houver 51 páginas, o texto da página será alterado para <strong>Formulário de Aplicativo </strong>1 de 51.</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Do Texto</td>
   <td><p>Substitui a palavra <strong>de</strong> pelo texto especificado (Página 1 <strong>de </strong>51). O valor padrão é <strong>de</strong>.</p> <p>Por exemplo, se você especificar <strong>de </strong>neste campo, o texto será alterado para Página 1 <strong>de </strong>51.</p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Link do formulário</strong></code></td>
   <td>Tipo de renderização</td>
   <td>Controla a listagem de formulários com base no tipo de renderização especificado. As opções disponíveis são PDF e HTML. Por exemplo, se você selecionar apenas HTML como tipo de renderização, os PDF forms serão filtrados.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Perfil do HTML</td>
   <td>Configura o perfil de HTML a ser usado para renderização. Todos os perfis disponíveis estão listados na lista suspensa.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Enviar URL</td>
   <td><p>Configura um servlet para o qual os dados de formulário são enviados.</p> <p><strong>Observação:</strong> <em>A URL de envio de um formulário pode ser especificada em vários locais e sua ordem de precedência é a seguinte:</em></p>
    <ol>
     <li><em>O URL de envio incorporado ao formulário (no botão Enviar ) tem a prioridade mais alta.</em></li>
     <li><em>O URL de envio mencionado na interface do usuário do AEM Forms tem a segunda prioridade mais alta.</em></li>
     <li><em>O URL de envio mencionado no portal de formulários tem a prioridade mais baixa.</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Dica de ferramenta de Ação de Renderização do HTML</td>
   <td>Configura o texto para a dica de ferramenta, que é exibida ao passar o ponteiro sobre <img height="16" src="assets/aem6forms_panel-html.png" width="13" /> (o ícone HTML5).</td>
  </tr>
  <tr>
   <td> </td>
   <td>Dica de ferramenta de Ação de Renderização do PDF</td>
   <td>Configura o texto para a dica de ferramenta, que é exibida ao passar o ponteiro sobre <img height="16" src="assets/aem6forms_panel-pdf.png" width="14" /> (o ícone PDF).</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Estilo</strong></code></td>
   <td>Tipo de estilo</td>
   <td>Permite especificar <strong>Sem Estilo, Estilo Padrão</strong> ou <strong>Estilo Personalizado </strong>para listar os formulários.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Caminho de estilo personalizado</td>
   <td>Se você selecionou Personalizado como o Tipo de estilo, procure para especificar o caminho para o CSS personalizado, caso contrário, selecione Padrão.</td>
  </tr>
 </tbody>
</table>

### Painel de pesquisa {#search-pane}

O painel Pesquisar permite adicionar os componentes Predicado de data, Predicado de texto completo, Predicado de propriedades e Predicado de tags da categoria Predicados de serviços de documento no AEM Sidekick. Esses componentes implementam a funcionalidade de pesquisa para que os usuários executem a pesquisa nos formulários listados.

**Dica:** *Você pode controlar a lista de formulários exibida no portal de formulários com base em um critério predefinido e ocultar a funcionalidade de pesquisa para os usuários finais. Para controlar a lista de formulários, use os componentes de Predicado para aplicar filtros de pesquisa. Você também pode especificar os valores de filtro padrão e desabilitar a pesquisa na guia Exibição da caixa de diálogo Editar Componente.*

![Painel de Pesquisa com Data, Texto Completo, Propriedades e Predicado de Marcas](assets/search-with-predicates.png)

Painel de pesquisa com data, texto completo, propriedades e predicado de tags

#### Predicado da data {#date-predicate}

O componente de Predicado de data, quando adicionado, permite a pesquisa nos formulários listados que foram modificados durante uma duração especificada.

Para configurar o componente de Predicado de data:

1. Selecione o componente e, em seguida, selecione ![settings_icon](assets/settings_icon.png). A caixa de diálogo Editar é aberta.
1. Especifique o seguinte:

   * **Tipo:** A única opção disponível é **Data da Última Modificação**

   * **Texto:** Rótulo ou legenda para o componente de Predicado de Data. O valor padrão é **Última Data de Modificação.**

   * **Rótulo de Data de Início:** Rótulo ou legenda do campo de data de início
   * **Rótulo de Data de Término:** Rótulo ou legenda para campo de data de término
   * **Ocultar:** para aplicar o filtro de data padrão para listar formulários

1. Selecione **OK**

#### Predicado de texto completo {#full-text-predicate}

O componente Predicado de texto completo implementa a pesquisa de texto completo nos dados de formulário, como nome e descrição. Os usuários podem pesquisar qualquer string de texto para retornar formulários que contenham o texto em seu nome ou descrição.

Para configurar o componente Predicado de texto completo:

1. Selecione o componente e, em seguida, selecione ![settings_icon](assets/settings_icon.png). A caixa de diálogo Editar é aberta.
1. Especifique o título no campo **Título principal**.
1. Selecionar **Ok**

#### Predicado de propriedades {#properties-predicate}

O componente Predicado de propriedades implementa a pesquisa de formulários com base nas propriedades do formulário, como título, autor e descrição.

Para configurar o componente Predicado de propriedades:

1. Selecione o componente e, em seguida, selecione ![settings_icon](assets/settings_icon.png). A caixa de diálogo Editar é aberta.
1. Na guia General, especifique o rótulo de pesquisa. O valor padrão é **Propriedades**

1. Na guia Opções, selecione **Adicionar Item.**
1. Selecione uma propriedade na lista suspensa e especifique um rótulo de pesquisa para ela no campo abaixo da lista suspensa.
1. Repita a etapa 4 para adicionar mais propriedades. Você também pode especificar um valor de filtro padrão para listar formulários com base nos critérios especificados e ocultar a propriedade para pesquisa por usuários finais. Marque a caixa de seleção Ocultar de uma propriedade e especifique o valor do filtro padrão.
Por exemplo, se você deseja exibir formulários que contêm &quot;Viagem&quot; em seus títulos, selecione Ocultar ao lado da propriedade Título. Além disso, especifique Viagem na caixa de texto de valor do filtro padrão.

1. Selecione **OK**

#### Predicado de tags {#tags-predicate}

O componente Predicado de tags implementa a pesquisa de formulários com base em tags definidas no Forms Manager.

Para configurar o componente Predicado de tags:

1. Selecione o componente e, em seguida, selecione ![settings_icon](assets/settings_icon.png). A caixa de diálogo Editar é aberta.
1. Selecione o botão de seta para baixo ao lado do campo Tags.
1. Selecione as tags apropriadas
1. Selecione **OK**

As tags selecionadas aparecem no painel Pesquisar junto com as caixas de seleção para seleção. Agora os usuários podem restringir sua pesquisa com base nas tags.

## Listar formulários em uma página {#list-forms-on-a-page-br}

Para listar formulários em uma página, adicione o Componente **[!UICONTROL Pesquisa &amp; Lister]** à página e configure o **[!UICONTROL Painel de Lista]**. Para permitir que os usuários finais pesquisem formulários com data, texto e marcas, adicione um componente do **[!UICONTROL Painel de Pesquisa]**.

Para vincular um formulário de qualquer lugar na página, use o componente Link. Para obter mais informações sobre o componente de link, consulte [Incorporando componente de link em uma página](../../forms/using/embedding-link-component-page.md).

Para listar os formulários que estão em um estado de rascunho e os formulários que já foram enviados, use o componente **[!UICONTROL Rascunhos e Envios]**. Para obter mais informações, consulte [Personalizando rascunhos e componentes de envios](../../forms/using/draft-submission-component.md).

## Facilidade para dispositivos móveis {#mobile-device-friendliness}

O componente Forms Portal Search &amp; Lister é compatível com dispositivos móveis e se adapta de acordo. Todas as três visualizações padrão: grade, cartão, painéis de relayouts de acordo com o dispositivo no qual o site é aberto, desde que a página da Web também se adapte. O fato simples é que o Search &amp; Lister é um componente somente e não controla o estilo do nível da página.

A imagem a seguir representa o componente de Pesquisa e Lister quando aberto em um dispositivo móvel:

![Captura de tela do componente de Pesquisa e Lister](assets/search_lister.png)

Componente de pesquisa e listagem

## Personalização da página do portal de formulários {#customizing-a-forms-portal-page-br}

Você pode personalizar uma página do portal de formulários para fornecer uma aparência distinta à página. Você também pode adicionar metadados para melhorar a experiência de pesquisa, alterar o layout da página e adicionar estilos CSS personalizados. Para obter mais informações, consulte [Personalização de modelos para Componentes do Portal Forms](../../forms/using/customizing-templates-forms-portal-components.md).

A interface do usuário do AEM Forms permite adicionar metadados personalizados a formulários. Os metadados personalizados são úteis para fornecer uma listagem e pesquisar a experiência de formulários para os usuários finais. Para obter mais informações sobre Metadados personalizados, consulte [Personalizando modelos para Componentes do Portal Forms](../../forms/using/customizing-templates-forms-portal-components.md).

Pronto para uso, o portal de formulários fornece ações de renderização. Você pode personalizar o portal de formulários para adicionar mais ações. Para obter informações detalhadas, consulte [Adicionando ação personalizada em itens de lista de formulários.](../../forms/using/add-custom-action-form-lister.md)

## Artigos relacionados

* [Habilitar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md)
* [Criar página do portal de formulários](/help/forms/using/creating-form-portal-page.md)
* [Listar formulários em uma página da Web usando APIs](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar componente de rascunhos e envios](/help/forms/using/draft-submission-component.md)
* [Personalizar o armazenamento de rascunhos e formulários enviados](/help/forms/using/draft-submission-component.md)
* [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md)
* [Personalização de modelos para componentes do portal de formulários](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md)
