---
title: Criação de uma página do portal de formulários
seo-title: Creating a forms portal page
description: O Forms Portal equipe os desenvolvedores da Web com componentes para criar e personalizar um portal de formulários em sites criados usando o Adobe Experience Manager (AEM).
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: a5017de5-616c-4ce4-81aa-f28c741f8e8f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 8fff78cb-9ef9-426e-8b30-d70b4f26887f
docset: aem65
feature: Forms Portal
exl-id: 22d7c24e-7a77-4324-afdf-74c1fbf15773
source-git-commit: 1683338f02d01d5d9843368955fa42f309718f26
workflow-type: tm+mt
source-wordcount: '1663'
ht-degree: 2%

---

# Criação de uma página do portal de formulários{#creating-a-forms-portal-page}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html) |
| AEM 6.5 | Este artigo |

Os componentes do portal do Forms equipam os desenvolvedores da Web com componentes para criar e personalizar um portal de formulários em sites criados usando o Adobe Experience Manager (AEM). Para obter uma visão geral rápida do portal de formulários, consulte [Introdução à publicação de formulários em um portal](../../forms/using/introduction-publishing-forms.md).

## Pré-requisitos {#prerequisites}

Os componentes do portal do Forms não estão disponíveis para uso por padrão. Verifique se as seguintes categorias de componente do portal de formulários estão habilitadas, conforme descrito em [Habilitar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md).

**Serviços de documento** Inclui os componentes Pesquisa e Lister, Link e Rascunhos e Envios.

**Predicados de serviços de documento** Inclui o Predicado de data, o Predicado de texto completo, o Predicado de propriedades e os componentes Predicado de tags. Esses componentes são usados para configurar a pesquisa no componente Pesquisa e Lister.

Uma vez ativadas em uma página de sites AEM, essas categorias de componentes ficam disponíveis para uso no navegador de componentes.

![Componentes do portal do AEM Forms no navegador de componentes](assets/component-categories.png)

Categorias de componentes do portal do Forms

## Componente de pesquisa e listagem {#search-amp-lister-component}

O componente de Pesquisa e listagem, disponível na categoria de componente Serviços de documento, é usado para listar formulários em uma página e implementar a pesquisa nos formulários listados. O componente inclui dois painéis:

* Painel Lista onde os formulários são listados.
* Painel de pesquisa no qual você adiciona a funcionalidade de pesquisa.

Você pode arrastar e soltar o componente Pesquisa e lista da categoria de componentes Serviços de documento no navegador de componentes para a página. O componente, quando adicionado, é semelhante ao seguinte.

![Componente de pesquisa e listagem em uma página](assets/fp-grid-viw.png)

Componente de Pesquisa e Lister em uma página com layout de Grade

### Painel Lista {#list-pane}

O painel Lista é uma área na qual os formulários são listados. O componente de Pesquisa e Lister fornece várias opções de configuração que você pode usar para controlar a exibição de formulários no painel Lista.

Para configurar o painel Lista, toque no componente Pesquisa e Lister e toque em ![settings_icon](assets/settings_icon.png). A variável **[!UICONTROL Editar componente]** será aberta.

![Painel Lista no modo de edição](assets/edit-list.png)

Painel Lista no modo de edição

A variável **Editar** A caixa de diálogo inclui várias guias que fornecem opções de configuração descritas na tabela abaixo. Toque **OK** para salvar a configuração, quando concluído.

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
   <td>Configura as pastas em que os ativos são carregados usando a interface do usuário do AEM Forms. Por padrão, ele lista todos os ativos carregados. Para obter mais informações sobre a interface do AEM Forms, consulte <a href="../../forms/using/introduction-managing-forms.md" target="_blank">Introdução ao gerenciamento de formulários</a>.</td>
  </tr>
  <tr>
   <td><p><span class="uicontrol"><strong>Exibir</strong></code></p> </td>
   <td>Texto do título</td>
   <td>Título para o componente de Pesquisa e Lister. O título padrão é <strong>Portal Forms.</strong></td>
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
   <td><p>Configura o texto da página (por exemplo, <strong>Página </strong>1 de 51). O valor padrão é <strong>Página</strong>.</p> <p>Por exemplo, se você especificar <strong>Formulário de inscrição </strong>neste campo e se houver 51 páginas, o texto da página será alterado para <strong>Formulário de inscrição </strong>1 de 51.</p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Do Texto</td>
   <td><p>Substitui a palavra <strong>de</strong> com o texto especificado (Página 1 <strong>de </strong>51). O valor padrão é <strong>de</strong>.</p> <p>Por exemplo, se você especificar <strong>de </strong>neste campo, o texto muda para a Página 1 <strong>de </strong>51.</p> </td>
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
   <td><p>Configura um servlet para o qual os dados de formulário são enviados.</p> <p><strong>Nota:</strong> <em>A URL de envio de um formulário pode ser especificada em vários locais e sua ordem de precedência é a seguinte:</em></p>
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
   <td>Permite especificar <strong>Sem Estilo, Estilo Padrão</strong>ou <strong>Estilo personalizado </strong>para listar os formulários.</td>
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

**Dica:** *Você pode controlar a lista de formulários exibida no portal de formulários com base em um critério predefinido e ocultar a funcionalidade de pesquisa para os usuários finais. Para controlar a lista de formulários, use os componentes de Predicado para aplicar filtros de pesquisa. Você também pode especificar os valores de filtro padrão e desativar a pesquisa na guia Exibição da caixa de diálogo Editar componente.*

![Painel de pesquisa com data, texto completo, propriedades e predicado de tags](assets/search-with-predicates.png)

Painel de pesquisa com data, texto completo, propriedades e predicado de tags

#### Predicado da data {#date-predicate}

O componente de Predicado de data, quando adicionado, permite a pesquisa nos formulários listados que foram modificados durante uma duração especificada.

Para configurar o componente de Predicado de data:

1. Toque no componente e em ![settings_icon](assets/settings_icon.png). A caixa de diálogo Editar é aberta.
1. Especifique o seguinte:

   * **Tipo:** A única opção disponível é **Última data de modificação**

   * **Texto:** Rótulo ou legenda do componente de Predicado de data. O valor padrão é **Data da última modificação.**

   * **Rótulo da data inicial:** Rótulo ou legenda do campo de data de início
   * **Rótulo de data final:** Rótulo ou legenda para o campo de data final
   * **Ocultar:** Para aplicar o filtro de data padrão para listar formulários

1. Toque **OK**

#### Predicado de texto completo {#full-text-predicate}

O componente Predicado de texto completo implementa a pesquisa de texto completo nos dados de formulário, como nome e descrição. Os usuários podem pesquisar qualquer string de texto para retornar formulários que contenham o texto em seu nome ou descrição.

Para configurar o componente Predicado de texto completo:

1. Toque no componente e em ![settings_icon](assets/settings_icon.png). A caixa de diálogo Editar é aberta.
1. Especifique o título no campo **Título principal** campo.
1. Toque **Ok**

#### Predicado de propriedades {#properties-predicate}

O componente Predicado de propriedades implementa a pesquisa de formulários com base nas propriedades do formulário, como título, autor e descrição.

Para configurar o componente Predicado de propriedades:

1. Toque no componente e em ![settings_icon](assets/settings_icon.png). A caixa de diálogo Editar é aberta.
1. Na guia General, especifique o rótulo de pesquisa. O valor padrão é **Propriedades**

1. Na guia Opções, toque em **Adicionar item.**
1. Selecione uma propriedade na lista suspensa e especifique um rótulo de pesquisa para ela no campo abaixo da lista suspensa.
1. Repita a etapa 4 para adicionar mais propriedades. Você também pode especificar um valor de filtro padrão para listar formulários com base nos critérios especificados e ocultar a propriedade para pesquisa por usuários finais. Marque a caixa de seleção Ocultar de uma propriedade e especifique o valor do filtro padrão.
Por exemplo, se você deseja exibir formulários que contêm &quot;Viagem&quot; em seus títulos, selecione Ocultar ao lado da propriedade Título. Além disso, especifique Viagem na caixa de texto de valor do filtro padrão.

1. Toque **OK**

#### Predicado de tags {#tags-predicate}

O componente Predicado de tags implementa a pesquisa de formulários com base em tags definidas no Forms Manager.

Para configurar o componente Predicado de tags:

1. Toque no componente e em ![settings_icon](assets/settings_icon.png). A caixa de diálogo Editar é aberta.
1. Toque no botão de seta para baixo ao lado do campo Tags.
1. Selecione as tags apropriadas
1. Toque **OK**

As tags selecionadas aparecem no painel Pesquisar junto com as caixas de seleção para seleção. Agora os usuários podem restringir sua pesquisa com base nas tags.

## Listar formulários em uma página {#list-forms-on-a-page-br}

Para listar formulários em uma página, adicione o **[!UICONTROL Pesquisa e Lister]** Componente à página e configure o **[!UICONTROL Painel Lista]**. Para permitir que os usuários finais pesquisem formulários com data, texto e tags, adicione um **[!UICONTROL Painel de pesquisa]** componente.

Para vincular um formulário de qualquer lugar na página, use o componente Link. Para obter mais informações sobre o componente de link, consulte [Incorporação do componente de link em uma página](../../forms/using/embedding-link-component-page.md).

Para listar os formulários que estão em um estado de rascunho e os formulários que já foram enviados, use o **[!UICONTROL Rascunhos e envios]** componente. Para obter mais informações, consulte [Personalização do componente Rascunhos e Envios](../../forms/using/draft-submission-component.md).

## Facilidade para dispositivos móveis {#mobile-device-friendliness}

O componente Forms Portal Search &amp; Lister é compatível com dispositivos móveis e se adapta de acordo. Todas as três visualizações padrão: grade, cartão, painéis de relayouts de acordo com o dispositivo no qual o site é aberto, desde que a página da Web também se adapte. O fato simples é que o Search &amp; Lister é um componente somente e não controla o estilo do nível da página.

A imagem a seguir representa o componente de Pesquisa e Lister quando aberto em um dispositivo móvel:

![Captura de tela do componente de Pesquisa e Lister](assets/search_lister.png)

Componente de pesquisa e listagem

## Personalização da página do portal de formulários {#customizing-a-forms-portal-page-br}

Você pode personalizar uma página do portal de formulários para fornecer uma aparência distinta à página. Você também pode adicionar metadados para melhorar a experiência de pesquisa, alterar o layout da página e adicionar estilos CSS personalizados. Para obter mais informações, consulte [Personalização de modelos para Componentes do Forms Portal](../../forms/using/customizing-templates-forms-portal-components.md).

A interface do usuário do AEM Forms permite adicionar metadados personalizados a formulários. Os metadados personalizados são úteis para fornecer uma listagem e pesquisar a experiência de formulários para os usuários finais. Para obter mais informações sobre Metadados personalizados, consulte [Personalização de modelos para Componentes do Forms Portal](../../forms/using/customizing-templates-forms-portal-components.md).

Pronto para uso, o portal de formulários fornece ações de renderização. Você pode personalizar o portal de formulários para adicionar mais ações. Para obter informações detalhadas, consulte [Adição de ação personalizada em itens de lista de formulários.](../../forms/using/add-custom-action-form-lister.md)

## Artigos relacionados

* [Habilitar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md)
* [Criar página do portal de formulários](/help/forms/using/creating-form-portal-page.md)
* [Listar formulários em uma página da Web usando APIs](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar componente de rascunhos e envios](/help/forms/using/draft-submission-component.md)
* [Personalizar o armazenamento de rascunhos e formulários enviados](/help/forms/using/draft-submission-component.md)
* [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md)
* [Personalização de modelos para componentes do portal de formulários](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md)
