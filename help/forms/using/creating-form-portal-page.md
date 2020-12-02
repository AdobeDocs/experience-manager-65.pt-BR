---
title: Criação de uma página de portal de formulários
seo-title: Criação de uma página de portal de formulários
description: O Forms Portal equipe os desenvolvedores da Web com componentes para criar e personalizar um portal de formulários em sites criados usando o Adobe Experience Manager (AEM).
seo-description: O Forms Portal equipe os desenvolvedores da Web com componentes para criar e personalizar um portal de formulários em sites criados usando o Adobe Experience Manager (AEM).
uuid: a5017de5-616c-4ce4-81aa-f28c741f8e8f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 8fff78cb-9ef9-426e-8b30-d70b4f26887f
docset: aem65
translation-type: tm+mt
source-git-commit: 13cc8ba8fda8fa0e5fac6bb92d1d4fc4849492eb
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 1%

---


# Criar uma página do portal de formulários{#creating-a-forms-portal-page}

Os componentes do portal da Forms equipam os desenvolvedores da Web com componentes para criar e personalizar um portal de formulários em sites criados usando o Adobe Experience Manager (AEM). Para obter uma visão geral rápida do portal de formulários, consulte [Introdução à publicação de formulários em um portal](../../forms/using/introduction-publishing-forms.md).

## Pré-requisitos {#prerequisites}

Por padrão, os componentes do portal do Forms não estão disponíveis para uso. Certifique-se de que as seguintes categorias de componentes do portal de formulários estejam ativadas conforme descrito em [Ativando componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md).

**Documento** ServicesInclui os componentes Pesquisa e Lister, Link e Rascunhos e Envio.

**Predicados** dos serviços do DocumentoInclui os componentes Predicado de data, Predicado de texto completo, Predicado de propriedades e Predicado de tags. Esses componentes são usados para configurar a pesquisa no componente Pesquisar e Lister.

Depois de ativadas em uma página de sites AEM, essas categorias de componentes estão disponíveis para uso no navegador de componentes.

![Componentes do portal da AEM Forms no navegador de componentes](assets/component-categories.png)

Categorias de componentes do portal do Forms

## Componente do Search &amp; Lister {#search-amp-lister-component}

O componente de Pesquisa e Lister, disponível em categoria de componentes de Serviços de Documento, é usado para lista de formulários em uma página e para implementar a pesquisa nos formulários listados. O componente inclui dois painéis:

* painel lista onde os formulários estão listados.
* Painel de pesquisa no qual você adiciona a funcionalidade de pesquisa.

Você pode arrastar e soltar o componente de Pesquisa e Lister da categoria de componentes Serviços de Documento no navegador de componentes para a página. O componente, quando adicionado, é semelhante ao seguinte.

![Componente de pesquisa e lister em uma página](assets/fp-grid-viw.png)

Componente de pesquisa e lister em uma página com layout de Grade

### painel lista {#list-pane}

O painel Lista é uma área em que seus formulários são listados. O componente de Pesquisa e Lister fornece várias opções de configuração que podem ser usadas para controlar a exibição de formulários no painel de Lista.

Para configurar o painel de Lista, toque no componente Pesquisar e Lister e, em seguida, toque em ![settings_icon](assets/settings_icon.png). A caixa de diálogo **[!UICONTROL Editar componente]** é aberta.

![Painel de lista no modo de edição](assets/edit-list.png)

Painel de lista no modo de edição

A caixa de diálogo **Editar** inclui várias guias que fornecem as opções de configuração descritas na tabela abaixo. Toque em **OK** para salvar a configuração, quando terminar.

<table>
 <tbody>
  <tr>
   <th>Guia</th>
   <th>Configuração</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Pastas de ativos</strong></code></td>
   <td>Adicionar Item</td>
   <td>Configura as pastas onde os ativos são carregados usando a interface do usuário do AEM Forms. Por padrão, ele lista todos os ativos carregados. Para obter mais informações sobre a interface do usuário do AEM Forms, consulte <a href="../../forms/using/introduction-managing-forms.md" target="_blank">Introdução ao gerenciamento de formulários</a>.</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>Exibir</strong></code></p> </td>
   <td>Texto do título</td>
   <td>Título do componente de Pesquisa e Lister. O título padrão é <strong>Forms Portal.</strong></td>
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
   <td>Quando ativada, oculta a barra de pesquisa de texto completo.</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Resultado</strong></code></td>
   <td>Número de resultados por página</td>
   <td>Configura o número máximo de formulários que você deseja exibir em uma página.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Texto de resultados</td>
   <td><p>Configura o texto dos resultados (por exemplo, 1-12 de 601 <strong>Results</strong>). O valor padrão é <strong>Results</strong>.</p> <p>Por exemplo, se você especificar <strong>Forms </strong>neste campo e houver um total de 601 formulários, o texto resultante mudará para 1-12 de 601 <strong>Forms.</strong></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Texto da página</td>
   <td><p>Configura o texto da página (por exemplo, <strong>Página </strong>1 de 51). O valor padrão é <strong>Page</strong>.</p> <p>Por exemplo, se você especificar <strong>Formulário de Aplicativo </strong>neste campo e houver 51 páginas, o texto da página será alterado para <strong>Formulário de Aplicativo </strong>1 de 51.</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Do Texto</td>
   <td><p>Substitui a palavra <strong>de</strong> pelo texto especificado (Página 1 <strong>de </strong>51). O valor padrão é <strong>de</strong>.</p> <p>Por exemplo, se você especificar <strong>de </strong>nesse campo, o texto mudará para Página 1 <strong>de </strong>51.</p> </td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Link do formulário</strong></code></td>
   <td>Tipo de renderização</td>
   <td>Controla a listagem de formulários com base no tipo de renderização especificado. As opções disponíveis são PDF e HTML. Por exemplo, se você selecionar somente HTML como tipo de renderização, os PDF forms serão filtrados.</td>
  </tr>
  <tr>
   <td> </td>
   <td>PERFIL HTML</td>
   <td>Configura o perfil HTML a ser usado para renderização. Todos os perfis disponíveis são listados na lista suspensa.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Enviar URL</td>
   <td><p>Configura um servlet no qual os dados do formulário são enviados.</p> <p><strong>Observação: </strong> <em>Enviar URL para um formulário pode ser especificado em vários locais e sua ordem de precedência é a seguinte:</em></p>
    <ol>
     <li><em>O URL de envio incorporado no formulário (no botão Enviar) tem a prioridade mais alta.</em></li>
     <li><em>O URL de envio mencionado na interface do usuário do AEM Forms tem a segunda prioridade mais alta.</em></li>
     <li><em>O URL de envio mencionado no portal de formulários tem a prioridade mais baixa.</em></li>
    </ol> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Dica da ferramenta Ação de renderização HTML</td>
   <td>Configura o texto da dica de ferramenta, que é exibida ao passar o ponteiro do mouse sobre <img height="16" src="assets/aem6forms_panel-html.png" width="13" /> (o ícone HTML5).</td>
  </tr>
  <tr>
   <td> </td>
   <td>Dica da ferramenta Ação de renderização de PDF</td>
   <td>Configura o texto da dica de ferramenta, que é exibida ao passar o ponteiro do mouse sobre <img height="16" src="assets/aem6forms_panel-pdf.png" width="14" /> (o ícone PDF).</td>
  </tr>
  <tr>
   <td><span class="uicontrol"><strong>Estilo</strong></code></td>
   <td>Tipo de estilo</td>
   <td>Permite que você especifique <strong>Sem estilo, Estilo padrão</strong> ou <strong>Estilo personalizado </strong>para listar os formulários.</td>
  </tr>
  <tr>
   <td> </td>
   <td>Caminho de estilo personalizado</td>
   <td>Se você selecionou Personalizado como o Tipo de estilo, navegue para especificar o caminho para o CSS personalizado, caso contrário selecione Padrão.</td>
  </tr>
 </tbody>
</table>

### Painel de pesquisa {#search-pane}

O painel de pesquisa permite que você adicione os componentes Predicado de data, Predicado de texto completo, Predicado de propriedades e Predicado de tags da categoria Predicados de serviços de Documento no Sidekick AEM. Esses componentes implementam a funcionalidade de pesquisa para que os usuários realizem a pesquisa nos formulários listados.

**Dica:** *você pode controlar a lista de formulários exibidos no portal de formulários com base em critérios predefinidos e ocultar a funcionalidade de pesquisa para usuários finais. Para controlar a lista de formulários, use os componentes Predicar para aplicar filtros de pesquisa. Você também pode especificar os valores de filtro padrão e desativar a pesquisa na guia Exibir da caixa de diálogo Editar componente.*

![Painel de pesquisa com data, texto completo, propriedades e previsão de tags](assets/search-with-predicates.png)

Painel de pesquisa com data, texto completo, propriedades e previsão de tags

#### Predicado de data {#date-predicate}

O componente Predicado de data, quando adicionado, permite a pesquisa nos formulários listados que foram modificados durante uma duração especificada.

Para configurar o componente Predicado de data:

1. Toque no componente e toque em ![settings_icon](assets/settings_icon.png). A caixa de diálogo Editar é aberta.
1. Especifique o seguinte:

   * **Tipo:** A única opção disponível é Data da  **Última Modificação**

   * **Texto:** Rótulo ou legenda para o Componente de previsão de data. O valor padrão é **Data da Última Modificação.**

   * **Rótulo da data do start:** Rótulo ou legenda do campo de data do start
   * **Rótulo de data final:** Rótulo ou legenda para o campo de data final
   * **Ocultar:** Para aplicar o filtro de data padrão a formulários de lista

1. Toque em **OK**

#### Predicado de texto completo {#full-text-predicate}

O componente Predicado de texto completo implementa a pesquisa de texto completo nos dados do formulário, como nome e descrição. Os usuários podem pesquisar qualquer string de texto para retornar formulários que contenham o texto em seu nome ou descrição.

Para configurar o componente Predicado de texto completo:

1. Toque no componente e toque em ![settings_icon](assets/settings_icon.png). A caixa de diálogo Editar é aberta.
1. Especifique o título no campo **Título principal**.
1. Toque em **Ok**

#### Predicado de propriedades {#properties-predicate}

O componente Predicado de propriedades implementa a pesquisa de formulários com base nas propriedades do formulário, como título, autor e descrição.

Para configurar o componente Predicado de propriedades:

1. Toque no componente e toque em ![settings_icon](assets/settings_icon.png). A caixa de diálogo Editar é aberta.
1. Na guia Geral, especifique o rótulo de pesquisa. O valor padrão é **Properties**

1. Na guia Opções, toque em **Adicionar Item.**
1. Selecione uma propriedade na lista suspensa e especifique um rótulo de pesquisa para ela no campo abaixo da lista suspensa.
1. Repita a etapa 4 para adicionar mais propriedades. Você também pode especificar um valor de filtro padrão para formulários de lista com base nos critérios especificados e ocultar a propriedade para pesquisa por usuários finais. Marque a caixa de seleção Ocultar para uma propriedade e especifique o valor do filtro padrão.
Por exemplo, se você deseja exibir formulários que contêm &quot;Viagem&quot; em seus títulos, selecione Ocultar ao lado da propriedade Título. Além disso, especifique Viagem na caixa de texto de valor de filtro padrão.

1. Toque em **OK**

#### Predicado de tags {#tags-predicate}

O componente Predicado de tags implementa a pesquisa de formulários com base em tags definidas no Forms Manager.

Para configurar o componente Predicado de tags:

1. Toque no componente e toque em ![settings_icon](assets/settings_icon.png). A caixa de diálogo Editar é aberta.
1. Toque no botão de seta para baixo ao lado do campo Tags.
1. Selecionar tags apropriadas
1. Toque em **OK**

As tags selecionadas são exibidas no painel Pesquisar junto com as caixas de seleção. Os usuários agora podem restringir sua pesquisa com base nas tags.

## Lista de formulários em uma página {#list-forms-on-a-page-br}

Para lista de formulários em uma página, adicione o componente **[!UICONTROL Pesquisar e Lister]** à página e configure o **[!UICONTROL Painel de Lista]**. Para permitir que os usuários finais pesquisem formulários com data, texto e tags, adicione um componente **[!UICONTROL Painel de pesquisa]**.

Para vincular um formulário de qualquer lugar na página, use o componente Link. Para obter mais informações sobre o componente de link, consulte [Incorporação do componente de link em uma página](../../forms/using/embedding-link-component-page.md).

Para lista dos formulários que estão em um estado de rascunho e dos formulários que já foram enviados, use o componente **[!UICONTROL Rascunhos e Envios]**. Para obter mais informações, consulte [Personalizando o componente Rascunhos e Envios](../../forms/using/draft-submission-component.md).

## Compatibilidade com dispositivos móveis {#mobile-device-friendliness}

O componente de Pesquisa e Lister do Forms Portal é compatível com dispositivos móveis e se adapta de acordo. Todas as três visualizações padrão: Os relaios em grade, placa e painel de acordo com o dispositivo no qual o site é aberto, são fornecidos com o fato de que a página da Web também se adapta. O fato simples é que o Search &amp; Lister é apenas um componente e não governa o estilo de nível de página.

A imagem a seguir mostra o componente de Pesquisa e Lister quando aberto em um dispositivo móvel:

![Captura de tela do componente de Pesquisa e Lister](assets/search_lister.png)

Componente de pesquisa e lister

## Personalizar uma página do portal de formulários {#customizing-a-forms-portal-page-br}

Você pode personalizar uma página do portal de formulários para fornecer uma aparência distinta à página. Você também pode adicionar metadados para melhorar a experiência de pesquisa, alterar o layout da página e adicionar estilos CSS personalizados. Para obter mais informações, consulte [Personalizar modelos para componentes do Forms Portal](../../forms/using/customizing-templates-forms-portal-components.md).

A interface do usuário do AEM Forms permite que você adicione metadados personalizados a formulários. Os metadados personalizados são úteis para fornecer uma experiência de listagem e pesquisa de formulários aos usuários finais. Para obter mais informações sobre metadados personalizados, consulte [Personalizar modelos para Componentes do Portal Forms](../../forms/using/customizing-templates-forms-portal-components.md).

O portal de formulários fornece ações de renderização. Você pode personalizar o portal de formulários para adicionar mais ações. Para obter informações detalhadas, consulte [Adicionar ação personalizada em itens do lister de formulários.](../../forms/using/add-custom-action-form-lister.md)

## Artigos relacionados

* [Ativar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md)
* [Criar página do portal de formulários](/help/forms/using/creating-form-portal-page.md)
* [Lista de formulários em uma página da Web usando APIs](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar componente Rascunhos e envios](/help/forms/using/draft-submission-component.md)
* [Personalizar o armazenamento de rascunhos e formulários enviados](/help/forms/using/draft-submission-component.md)
* [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md)
* [Personalização de modelos para componentes do portal de formulários](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md)
