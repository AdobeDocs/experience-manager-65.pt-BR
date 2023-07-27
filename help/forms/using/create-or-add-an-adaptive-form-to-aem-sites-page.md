---
title: Criar ou adicionar um formulário adaptável à página do AEM Sites
description: Descubra como criar ou adicionar facilmente um formulário adaptável à sua página do AEM Sites. Conheça as técnicas passo a passo e as práticas recomendadas para integrar formulários dinâmicos e personalizáveis ao seu site, otimizando suas experiências digitais para obter o máximo impacto.
Keywords: AEM Forms in sites, AF in Sites editor, af in aem sites, aem sites af, add af to a sites page, af aem sites, af sites, create af in a sites page, adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
feature: Adaptive Forms
exl-id: 1813ccfc-87ce-46fa-a1d5-5edffd91efb0
source-git-commit: 600dcc52829ff2c5e54176bda7631845ef24f986
workflow-type: tm+mt
source-wordcount: '2970'
ht-degree: 1%

---

# Criar ou adicionar um formulário adaptável à página do AEM Sites {#create-or-add-an-adaptive-form-to-aem-sites-page}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-br) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM 6.5 | Este artigo |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html) |

Com o AEM Forms, você pode incorporar facilmente formulários adaptáveis em suas páginas da Web. Isso permite que seus visitantes preencham e enviem formulários de maneira conveniente sem nunca sair da página em que estão. Ao fazer isso, eles podem se envolver facilmente com outros elementos do site enquanto interagem ativamente com o formulário.

Você pode usar o Editor de páginas AEM para criar e adicionar rapidamente vários formulários às suas páginas do AEM Sites. Usar o Editor de páginas AEM permite que os autores de conteúdo criem experiências de captura de dados perfeitas em uma página do Sites, usando o potencial dos componentes de formulários adaptáveis, incluindo comportamento dinâmico, validações, integração de dados e geração de documentos de registro e automação de processos comerciais. Ele também permite usar vários recursos de páginas do AEM Sites, como controle de versão, direcionamento, tradução e gerenciador de vários sites.

O AEM Forms fornece o Contêiner de formulário adaptável e os componentes Forms - Incorporar. Você pode usar o Contêiner de formulário adaptável para criar um novo formulário em um Fragmento de experiência ou página do AEM Sites, enquanto o componente Adaptive Forms - Incorporar permite adicionar um formulário adaptável existente ou criar um novo formulário usando o Editor Adaptive Forms.

![Formulário adaptável na página de sites](/help/forms/using/assets/adaptive-form-in-sites-page.png)

## Benefícios do uso do componente de Contêiner de formulário adaptável no Editor de páginas AEM ou no Fragmento de experiência

O uso do Contêiner de formulário adaptável no Editor de páginas AEM permite criar experiências de captura de dados contínua em uma página do Sites, usando o potencial dos componentes adaptáveis do Forms, incluindo comportamento dinâmico, validações, integração de dados, geração de documentos de registro e automação do processo comercial. Ele também permite usar vários recursos de páginas do AEM Sites, como controle de versão, direcionamento, tradução e gerenciador de vários sites, aprimorando a experiência geral de criação e gerenciamento de formulários. Vamos explorar alguns destes recursos:

* **Controle de versão:** Oferta de páginas do AEM Sites [recursos robustos de controle de versão](/help/sites-authoring/working-with-page-versions.md), permitindo rastrear e gerenciar diferentes versões dos formulários. Isso permite fazer alterações e aprimoramentos nos formulários, mantendo a capacidade de reverter para versões anteriores, se necessário. O controle de versão garante uma abordagem controlada e organizada para o desenvolvimento e evolução da forma.
* **Direcionamento (integração com o Adobe Target):** Com os recursos de direcionamento de páginas do AEM Sites, você também pode [personalizar a experiência do formulário para públicos diferentes](/help/sites-administering/target.md). Ao utilizar segmentos de usuários e critérios de direcionamento, você pode adaptar o conteúdo, o design ou o comportamento do formulário a grupos específicos de usuários. Isso permite fornecer uma experiência de formulário personalizada e relevante, aumentando as taxas de engajamento e conversão.
* **Tradução:** AEM Sites [integração perfeita com serviços de tradução](/help/sites-administering/translation.md), permitindo que você traduza formulários em vários idiomas facilmente. Esse recurso simplifica o processo de localização, garantindo que seus formulários estejam acessíveis para um público-alvo global. Você pode gerenciar traduções com eficiência em projetos de tradução AEM, reduzindo o tempo e o esforço necessários para o suporte a formulários multilíngues. Consulte a seção considerações para obter mais informações sobre tradução.
* **Gerenciamento de vários sites e Live Copy:** O AEM Sites oferece [Recursos de gerenciamento de vários sites e Live Copy](/help/sites-administering/msm.md), permitindo criar e gerenciar vários sites em um único ambiente. Esse recurso agora permite reutilizar formulários em sites diferentes, garantindo a consistência e reduzindo os esforços de duplicação. Com controle e gerenciamento centralizados, você pode manter e atualizar formulários de maneira eficiente em vários sites.
* **Temas:** As páginas do AEM Sites fornecem uma estrutura para projetar e manter estilos visuais consistentes em várias páginas da Web. Eles definem cores, fontes, folhas de estilos e outros elementos visuais que contribuem para a aparência geral do site. [Você pode usar os temas criados para uma página do AEM Sites para um Formulário adaptável, economizando tempo e esforço](/help/sites-authoring/style-system.md).
* **Marcação:** As páginas do AEM Sites permitem [atribuir tags ou rótulos a uma página, um ativo ou outro conteúdo](/help/sites-authoring/tags.md). Tags são rótulos de palavras-chave ou metadados que fornecem uma maneira de categorizar e organizar o conteúdo com base em critérios específicos. É possível atribuir uma ou mais tags a páginas, ativos ou qualquer outro conteúdo no AEM para melhorar a pesquisa e a categorização dos ativos.
* **Bloquear e desbloquear conteúdo:** O AEM Sites permite que os usuários [controlar o acesso e as modificações nas páginas](/help/sites-authoring/editing-content.md#locking-a-page-locking-a-page) no ambiente do AEM Sites. Quando uma página é bloqueada, significa que ela está protegida contra alterações ou edições não autorizadas por outros usuários. Somente o usuário que bloqueou o conteúdo ou um administrador designado pode desbloqueá-lo para permitir modificações.


## Várias opções para adicionar um formulário adaptável no editor de páginas AEM

Você pode aproveitar ao máximo esse recurso utilizando as seguintes opções:

* **[Adicionar um formulário adaptável personalizado a uma página do AEM Sites:](#create-an-adaptive-form-in-sites-editor)** Crie um formulário totalmente novo do zero, adaptando-o especificamente às suas necessidades e preferências de design.

* **[Adicionar um formulário adaptável personalizado a um Fragmento de experiência:](#create-an-adaptive-form-in-experience-fragment)** Estenda o alcance de seus formulários adicionando-os aos Fragmentos de experiência de AEM, permitindo uma reutilização contínua em várias páginas ou sites.

* **[Converter um formulário adaptável em fragmento de experiência:](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)** Converta um formulário adaptável adicionado a uma página do AEM Sites em um Fragmento de experiência para reutilizar o formulário em várias páginas do AEM Sites.

* **Criar e adicionar formulários com base em modelos aprovados a uma página do AEM Sites:** Aproveite os modelos pré-aprovados para criar rapidamente formulários que se alinhem às diretrizes de marca e aos padrões de design de sua organização. A opção está disponível somente para o Forms adaptável criado com o Editor Forms adaptável ou o componente Forms adaptável - Incorporar.

* **Adicionar formulários existentes a uma página do AEM Sites:** Integre facilmente formulários que você já criou em seus sites, permitindo que os visitantes interajam diretamente com eles. A opção está disponível somente para o Forms adaptável criado com o Editor Forms adaptável ou o componente Forms adaptável - Incorporar.

* **Adicionar vários formulários a uma página do AEM Sites ou Fragmento de experiência:**  Adicione vários formulários a uma página para fornecer várias opções aos usuários com base em suas preferências e requisitos. Eles podem combinar formulários totalmente novos do zero com formulários existentes.

## Considerações {#consideration}

* Quando você usa o Contêiner de formulário adaptável para criar ou adicionar um formulário, os formulários são submetidos a tradução e localização por meio do fluxo de tradução do AEM Sites. Para cada idioma, uma cópia separada (cópia de idioma) da página de sites e os formulários correspondentes são gerados e, quando um autor de conteúdo modifica uma regra em um formulário na página principal, as mesmas alterações devem ser feitas em todas as cópias de idioma do formulário. O Contêiner de formulário adaptável também permite usar vários recursos das páginas do AEM Sites, como controle de versão, direcionamento, tradução e gerenciador de vários sites.

* Ao criar ou adicionar um formulário usando o componente de incorporação do formulário adaptável, os formulários são submetidos a tradução e localização usando o fluxo de tradução do AEM Forms. Nesse caso, um único formulário é mantido e referenciado em todas as cópias de idioma das páginas do Sites. O componente de Formulário incorporado adaptável não fornece acesso a vários recursos de páginas do AEM Sites, como o, controle de versão, direcionamento, tradução e gerenciador de vários sites.


## Antes de você iniciar {#before-you-start}

+++  Ativar os Componentes principais adaptáveis do Forms para o seu ambiente

Certifique-se de que o [Os Componentes principais adaptáveis do Forms são ativados para o seu ambiente](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/quick-setup/enable-headless-adaptive-forms-and-core-components.html?lang=en).

+++

+++  Adicionar bibliotecas de clientes Forms adaptáveis à sua página do AEM Sites e componentes da página Fragmento de experiência

Para ativar a funcionalidade completa do componente de Contêiner adaptável do Forms, adicione as bibliotecas de clientes Customheaderlibs e Customfooterlibs à sua página do AEM Sites usando o pipeline de implantação. Para adicionar as bibliotecas:

1. Faça logon na instância do AEM Author e abra o CRX DE. O URL padrão de uma instância de Autor em execução localmente é `http://localhost:4502/crx/de`.

1. Abra o `/apps/[your-sites-project]/components/page/customheaderlibs.html` e adicione o seguinte código ao arquivo:

       &quot;
       //Customheaderlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-call=&quot;${clientlib.css @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;}&quot; />
       &lt;/sly>
       
       &quot;
   
1. Abra o `/apps/[your-sites-project]/components/page/customfooterlibs.html` e adicione o seguinte código ao arquivo:

       &quot;
       
       //customfooterlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-test=&quot;${!wcmmode.edit}&quot; data-sly-call=&quot;${clientlib.js @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;, async=true}&quot; />
       &lt;/sly>
       &quot;
   
1. Abra o `/apps/[your-sites-project]/components/xfpage/customheaderlibs.html` e adicione o seguinte código ao arquivo:

       &quot;
       //Customheaderlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-call=&quot;${clientlib.css @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;}&quot; />
       &lt;/sly>
       
       &quot;
   
1. Abra o `/apps/[your-sites-project]/components/customfooterlibs.html` e adicione o seguinte código ao arquivo:

       &quot;
       
       //customfooterlibs.html
       &lt;sly data-sly-use.clientlib=&quot;core/wcm/components/commons/v1/templates/clientlib.html&quot;>
       &lt;sly data-sly-test=&quot;${!wcmmode.edit}&quot; data-sly-call=&quot;${clientlib.js @ categories=&amp;#39;core.forms.components.runtime.all&amp;#39;, async=true}&quot; />
       &lt;/sly>
       &quot;
   
1. Repita as etapas acima para todas as instâncias de Autor e Publicação em seu ambiente.

+++

+++ Ativar contêiner adaptável do Forms

Para habilitar [!UICONTROL Contêiner adaptável do Forms] componente na política do modelo, execute as seguintes etapas:

1. Abra a página do AEM Sites ou o Fragmento de experiência para edição. Para abrir a página para edição, selecione a página e clique em Editar.
1. Abra o modelo da página Sites ou Fragmento de experiência. Para abrir o template, vá para a [!UICONTROL Informações da página] ![Informações da página](/help/forms/using/assets/Smock_Properties_18_N.svg) > [!UICONTROL Editar modelo]. Ele abre o modelo correspondente no editor de modelo.
1. Na visualização Estrutura, clique no botão **[!UICONTROL Política]** ![Política](/help/forms/using/assets/Smock_FeedManagement_18_N.svg) ícone na barra de menus. No **[!UICONTROL Componentes permitidos]** e selecione o **[!UICONTROL Contêiner adaptável do Forms]**  na caixa de seleção **[Nome do projeto do arquétipo AEM] - Formulário adaptável**.
1. Clique em **[!UICONTROL Concluído]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

## Criar um Formulário adaptável {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

Você pode criar um formulário totalmente novo do zero, ajustando-o especificamente às suas necessidades e preferências de design, diretamente em uma página do AEM Sites ou no Fragmento de experiência. Para formulários de uso único, recomenda-se a criação direta em uma página do AEM Sites, enquanto os Fragmentos de experiência são ideais para formulários que precisam ser reutilizados em várias páginas do site.

* [Criar um formulário em uma página do AEM Sites](#create-an-adaptive-form-in-sites-editor)
* [Criar um formulário em um Fragmento de experiência](#create-an-adaptive-form-in-experience-fragment)
* [Converter um formulário adaptável na página AEM Sites em um fragmento de experiência](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Criar um formulário em uma página do AEM Sites {#create-an-adaptive-form-in-sites-editor}

Você pode usar o componente de Contêiner de formulário adaptável no Editor de páginas AEM para criar um formulário personalizado. O componente permite criar um formulário arrastando e soltando os componentes do formulário. Os componentes de formulário são baseados nos Componentes principais. Você pode personalizá-los facilmente de acordo com os requisitos de sua organização.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Para criar um Formulário adaptável em uma página do Sites:

1. Abra a página do AEM Sites no modo de edição.
1. Arraste e solte a variável **[!UICONTROL Contêiner adaptável do Forms]** componente do Navegador de componentes para a página Sites. Ele cria um espaço na página para o formulário. Você pode usar o modo de layout para alterar o Tamanho do espaço do container.
1. Arraste e solte os Componentes principais do formulário adaptável no espaço do contêiner para criar o formulário.
1. Adicione o botão Submit.

Em seguida, você [definir a ação enviar](#configure-submit-action-for-form) e propriedades avançadas.

### Criar um formulário em um Fragmento de experiência {#create-an-adaptive-form-in-experience-fragment}

Você pode estender o alcance de seus formulários adicionando-os aos Fragmentos de experiência de AEM, permitindo uma reutilização contínua em várias páginas ou sites. Por exemplo, você pode incluir um formulário de inscrição de informativo em um Fragmento de experiência. Isso permite reutilizar convenientemente o fragmento em várias páginas do site, eliminando a necessidade de recriar o formulário repetidamente. Quaisquer atualizações ou modificações feitas no formulário de inscrição do boletim informativo no Fragmento de experiência são propagadas automaticamente para todas as páginas em que são utilizadas. Isso simplifica o processo e garante uma experiência perfeita para o usuário, simplificando o gerenciamento dos formulários de seu site.

Para criar um formulário adaptável em um fragmento de experiência:

1. Abra um Fragmento de experiência.
1. Arraste e solte a variável **[!UICONTROL Contêiner adaptável do Forms]** componente do Navegador de componentes para o Fragmento de experiência.
1. Arraste e solte os Componentes principais do formulário adaptável no espaço de contêiner no Fragmento de experiência para criar o formulário.
1. Adicione o botão Submit.

Em seguida, você [definir a ação enviar](#configure-submit-action-for-form) e propriedades avançadas.

### Converter um formulário adaptável na página AEM Sites em um fragmento de experiência {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

Você pode converter um formulário adaptável existente em um Editor de páginas de sites em um Fragmento de experiência para reutilizar o formulário em várias páginas ou sites.

Para converter um formulário adaptável na página AEM Sites em um fragmento de experiência:

1. Abra a página do AEM Sites que contém o formulário adaptável (no componente Contêiner adaptável do Forms) no modo de edição.
1. Abra a Árvore de conteúdo e selecione a **[!UICONTROL Contêiner adaptável do Forms]** que hospeda o formulário adaptável. Uma página do AEM Sites pode hospedar vários Forms adaptáveis. Portanto, selecione cuidadosamente o Contêiner adaptável correto do Forms.
1. Na barra de menus, selecione a opção ![Ícone Converter para variação de fragmento de experiência](/help/forms/using/assets/Smock_FilingCabinet_18_N.svg) Ícone Converter para variação de Fragmento de experiência.
   ![Converter formulário na página Sites em um fragmento de experiência](/help/forms/using/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   Uma caixa de diálogo para converter o contêiner do Formulário adaptável em um novo Fragmento de experiência ou adicionar a um Fragmento de experiência existente é exibida
1. Na caixa de diálogo Converter em variação de Fragmento de experiência, defina valores para as seguintes opções:

   * **Ação:** Selecione para criar um novo fragmento de experiência ou Adicionar a um fragmento de experiência existente.
   * **Caminho principal:** Especifique o caminho da pasta na qual hospedar o fragmento de experiência. A opção está disponível somente para criar um novo Fragmento de experiência.
   * **Modelo:** Especifique o caminho do modelo do Fragmento de experiência. Se você não tiver um modelo de Fragmento de experiência, [criar](/help/sites-developing/experience-fragments.md). A opção está disponível somente para adicionar o Formulário adaptável a um Fragmento de experiência existente.
   * **Título do fragmento:** Especifique o título do Fragmento de experiência. O título identifica exclusivamente um Fragmento de experiência


## Configurar a ação enviar para o formulário {#configure-submit-action-for-form}

Uma ação enviar permite escolher o destino dos dados capturados por meio de um formulário adaptável. É acionado quando um usuário clica no botão Enviar em um Formulário adaptável. Os formulários adaptáveis incluem algumas ações de envio prontas para uso. Você também pode estender ações de envio padrão para criar sua própria ação de envio personalizada. Para configurar uma Ação de envio para o formulário:

1. Abra o Editor de páginas AEM ou o Fragmento de experiência que contém o Formulário adaptável.
1. Abra a Árvore de conteúdo e selecione a **[!UICONTROL Contêiner adaptável do Forms]** que hospeda o formulário adaptável. Uma página do AEM Sites pode hospedar vários Forms adaptáveis. Portanto, selecione cuidadosamente o Contêiner adaptável correto do Forms.
1. Clique nas propriedades do Contêiner de formulário adaptável ![Propriedades do contêiner de formulário adaptável](/help/forms/using/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável para configurar ações de envio é aberta.
   ![Contêiner de formulários adaptáveis](/help/forms/using/assets/adaptive-forms-container.png)
1. Selecione e configure uma ação Enviar, com base em seus requisitos. Para obter informações detalhadas sobre Ações de Envio, consulte [Ação de envio do formulário adaptável](configuring-submit-actions.md)


## Configurar um esquema ou modelo de dados de formulário para um formulário {#configure-schema-or-data-model-for-form}

Você pode usar o Modelo de dados de formulário para conectar um formulário a uma Fonte de dados para enviar e receber dados com base nas ações do usuário. Você também pode conectar um formulário a um esquema JSON para receber os dados enviados em um formato predefinido.

Antes de conectar um formulário a um esquema ou modelo de dados de formulário

* [Crie um esquema JSON e faça upload para o seu ambiente](adaptive-form-json-schema-form-model.md)
* [Criar um modelo de dados de formulário](create-form-data-models.md)

Para configurar um Esquema JSON ou um Modelo de dados de formulário para seu formulário:

1. Abra o Editor de páginas AEM ou o Fragmento de experiência que contém o Formulário adaptável.
1. Abra a Árvore de conteúdo e selecione a **[!UICONTROL Contêiner adaptável do Forms]** que hospeda o formulário adaptável. Uma página do AEM Sites pode hospedar vários Forms adaptáveis. Portanto, selecione cuidadosamente o Contêiner adaptável correto do Forms.
1. Clique nas propriedades do Contêiner de formulário adaptável ![Propriedades do contêiner de formulário adaptável](/help/forms/using/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável para configurar os Modelos de dados é aberta.
   ![Contêiner de formulários adaptáveis do modelo de dados de formulário](/help/forms/using/assets/form-data-model-adaptive-forms-container.png)
1. Selecione e configure um Esquema JSON ou Modelo de dados de formulário, com base em seus requisitos. Para obter informações detalhadas sobre Ações de Envio, consulte [Ação de envio do formulário adaptável](configuring-submit-actions.md).

   * Ao selecionar a variável **[!UICONTROL Modelo de formulário]** , use o **[!UICONTROL Selecionar modelo de dados do formulário]** opção para selecionar um modelo de dados de formulário pré-configurado.
   * Ao selecionar a variável **[!UICONTROL Esquema]** , use o **[!UICONTROL Esquema]** opção para selecionar um esquema JSON para o formulário.

1. Clique em **[!UICONTROL Concluído]**.

## Configurar um serviço de pré-preenchimento para um formulário {#configure-prefill-service-for-form}

Você pode usar o serviço de preenchimento prévio para preencher automaticamente os campos de um Formulário adaptável usando dados existentes. Quando um usuário abre um formulário, os valores desses campos são preenchidos previamente. É possível:

* [Criar um serviço de preenchimento prévio personalizado](prepopulate-adaptive-form-fields.md)
* [Usar o serviço de preenchimento do modelo de dados de formulário](#fdm-prefill-service)

### Usar o serviço de preenchimento do modelo de dados de formulário {#fdm-prefill-service}

Você pode usar o serviço de Preenchimento do modelo de dados de formulário para preencher previamente os campos de um formulário usando um Modelo de dados de formulário configurado. O serviço de Preenchimento do modelo de dados de formulário usa o [Obter serviço do modelo de dados de formulário configurado](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) para recuperar dados. Para usar o serviço de Preenchimento de modelo de dados de formulário para um Formulário adaptável:

1. Abra o Editor de páginas AEM ou o Fragmento de experiência que contém o Formulário adaptável.
1. Abra a Árvore de conteúdo e selecione a **[!UICONTROL Contêiner adaptável do Forms]** que hospeda o formulário adaptável. Uma página do AEM Sites pode hospedar vários Forms adaptáveis. Portanto, selecione cuidadosamente o Contêiner adaptável correto do Forms.
1. Clique nas propriedades do Contêiner de formulário adaptável ![Propriedades do contêiner de formulário adaptável](/help/forms/using/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável para configurar os Modelos de dados é aberta.
   ![Preencher o editor de página do serviço fdm aem sites](/help/forms/using/assets/prefill-service-fdm-aem-sites-page-editor.png)
1. Selecionar um modelo de dados do formulário. Abra o **[!UICONTROL Básico]** guia. No serviço de preenchimento, selecione **[!UICONTROL Serviço de Preenchimento de Rascunho do Portal do Forms]**.
1. Clique em **[!UICONTROL Concluído]**.

## Redirecionar o usuário para um novo usuário no envio do formulário ou mostrar uma mensagem de agradecimento

No envio de um formulário, você pode redirecionar o usuário para outra página da Web ou uma mensagem. Para redirecionar o usuário ou configurar a mensagem de agradecimento:

1. Abra o Editor de páginas AEM ou o Fragmento de experiência que contém o Formulário adaptável.
1. Abra a Árvore de conteúdo e selecione a **[!UICONTROL Contêiner adaptável do Forms]** que hospeda o formulário adaptável. Uma página do AEM Sites pode hospedar vários Forms adaptáveis. Portanto, selecione cuidadosamente o Contêiner adaptável correto do Forms.
1. Clique nas propriedades do Contêiner de formulário adaptável ![Propriedades do contêiner de formulário adaptável](/help/forms/using/assets/configure-icon.svg) ícone. A caixa de diálogo Contêiner de formulário adaptável para configurar os Modelos de dados é aberta.
1. Abra o **[!UICONTROL Envio]** guia.

   * Para configurar um URL de redirecionamento, para na opção Enviar, selecione a opção Redirecionar para URL e forneça um endereço absoluto, um URL de redirecionamento ou um caminho relativo de uma página do AEM Sites.

   * Para configurar uma mensagem personalizada ou de agradecimento, para na opção Enviar, selecione a opção Mostrar mensagem e forneça uma mensagem na caixa Conteúdo da mensagem. É uma caixa de rich text, você pode usar a opção de tela cheia para exibir todos os itens de rich text disponíveis.
