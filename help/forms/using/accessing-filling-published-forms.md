---
title: Acesso e preenchimento de formulários publicados
seo-title: Accessing and filling published forms
description: O Forms Portal equipara os desenvolvedores da Web a componentes para criar e personalizar um portal de formulários em sites criados usando o Adobe Experience Manager (AEM).
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: 44731604-5d97-46fa-baa9-0c020c634fa7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 88dc8ef2-95ce-4906-ac28-eecc3a32a64e
docset: aem65
exl-id: aedf890c-a2f1-412f-8897-2492ffab335a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# Acesso e preenchimento de formulários publicados{#accessing-and-filling-published-forms}

Em uma configuração de implantação de portal centrada em formulários, o desenvolvimento de formulários e o desenvolvimento de portal são duas atividades distintas. Enquanto os designers de formulários criam e armazenam formulários em um repositório, os desenvolvedores da Web criam um aplicativo da Web para esses formulários de lista e lidam com envios. Os Forms são copiados para a camada da Web, pois não há comunicação entre o repositório de formulários e o aplicativo da Web.

Isso geralmente resulta em problemas com o gerenciamento de configuração e atrasos de produção. Por exemplo, se uma versão mais recente de um formulário estiver disponível no repositório, o designer de formulário substituirá o formulário na camada da Web, modificará a aplicação Web e reimplantará o formulário no site público. A reimplantação do aplicativo da Web pode causar algum tempo de inatividade do servidor. Como o tempo de inatividade do servidor é uma atividade planejada, as alterações não podem ser enviadas para o site público imediatamente.

O Forms Portal reduz os custos indiretos de gerenciamento e os atrasos de produção. Ele fornece componentes para os desenvolvedores da Web para criar e personalizar um portal de formulários em sites criados usando o Adobe Experience Manager (AEM).

Para obter mais informações sobre o portal de formulários e seus recursos, consulte [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md).

## Introdução ao portal de formulários {#getting-started-with-forms-portal}

Navegue até a página do portal de formulários publicados. Para obter mais informações sobre como criar uma página de portal de formulários, consulte [Criação de uma página de portal de formulários](../../forms/using/creating-form-portal-page.md).

O componente Pesquisar e lister do portal de formulários exibe os formulários disponíveis na instância Publicar do servidor de AEM. Essa lista inclui todos os formulários ou os formulários definidos no filtro no momento da criação da página do portal de formulários. Uma página do portal de formulários é semelhante à mostrada na seguinte imagem:

![Uma página de portal de formulários de amostra ](assets/forms-portal-page.png)

Uma página de portal de formulários de amostra

### Pesquisar e Lister {#search-and-lister}

O componente Pesquisa e Lister permite adicionar a seguinte funcionalidade ao portal de formulários:

* Liste os formulários na exibição de painel, cartão ou grade que estão disponíveis para uso imediato. Ele também oferece suporte a modelos personalizados, além de formulários de Lista de pastas específicas no Forms Manager.
* Especifique como os formulários são renderizados: HTML5, PDF ou ambos.
* Especifique como os formulários PDF e XFA são renderizados - HTML5, PDF ou ambos. Formulários não XFA como HTML5.
* Ative a pesquisa de formulários com base em critérios, como propriedades de formulário, metadados e tags.
* Enviar dados de formulário para um servlet.
* Use as folhas de estilo personalizadas (CSS) para personalizar a aparência do portal.
* Criar links para formulários.

Você pode pesquisar formulários na página Portal do Forms usando as seguintes opções:

* Pesquisa de texto completo
* Pesquisa avançada

A pesquisa de texto completo permite localizar e listar formulários com base nas palavras-chave especificadas.

![Uma caixa de diálogo de pesquisa avançada](assets/search-panel.png)

Uma caixa de diálogo de pesquisa avançada

A Pesquisa avançada permite pesquisar formulários com base nas propriedades especificadas do formulário. Isso fornece resultados mais específicos do que pesquisa de texto completo. A pesquisa avançada inclui a pesquisa com base em tags, propriedades (como Autor, Descrição e Título), data de modificação e texto completo.

O Lister exibe formulários com base nos parâmetros de pesquisa. Cada formulário no resultado da pesquisa é exibido com um ícone, que é hipervinculado ao formulário associado. Você pode clicar no ícone para abrir e trabalhar com o formulário associado.

### Preenchimento de um formulário {#filling-a-form}

![Um exemplo de formulário adaptável](assets/filling_a_form.png)

Um exemplo de formulário adaptável

Os formulários podem ser acessados no link fornecido junto com o formulário no componente Pesquisar e Lister da página.

Cada formulário contém informações de ajuda que permitem que o usuário preencha o formulário.

#### Rascunhos e Envio {#drafts-and-submission}

Um usuário tem a opção de salvar um rascunho de um formulário clicando no botão Salvar . Isso permite que o usuário trabalhe em um formulário durante um período de tempo antes de enviá-lo.

Os dados preenchidos no formulário (incluindo anexos) são salvos como rascunho no servidor. O rascunho de um formulário pode ser salvo várias vezes. O formulário salvo é exibido na guia Rascunhos do componente Rascunho e envio da página.

Ao concluir o preenchimento do formulário, o usuário envia os formulários clicando no botão Enviar do formulário. Os formulários enviados aparecem na guia Envios do componente Rascunho e envio da página.

>[!NOTE]
>
>Os formulários enviados aparecem na guia Enviado do Forms somente se a ação de envio do formulário adaptável estiver configurada como Ação de envio do Forms Portal. Para obter mais informações sobre enviar ações, consulte [Configuração da ação Enviar](../../forms/using/configuring-submit-actions.md).

![Componente Rascunhos e envios](assets/draft-submission.png)

Componente Rascunhos e envios

## Iniciar um novo formulário usando dados de formulário enviados {#start-a-new-form-using-submitted-form-data}

Há determinados formulários que você precisa preencher e enviar com frequência. Por exemplo, o formulário para depósito da declaração de imposto individual é enviado todos os anos. Nesses casos, enquanto algumas informações mudam toda vez que você preenche o formulário, a maioria delas como os detalhes pessoais e familiares não são alteradas. No entanto, ainda é necessário preencher o formulário inteiro novamente, do zero.

O AEM Forms pode ajudar a otimizar a experiência de preenchimento do formulário e reduzir significativamente o tempo para preencher e enviar um formulário novamente. Os usuários finais podem iniciar um novo formulário usando dados de um formulário enviado. Essa funcionalidade é incorporada na variável [Componente Rascunhos e envios](../../forms/using/draft-submission-component.md). Ao adicionar Rascunhos e Enviar componente à página do portal de formulários e publicá-lo, os usuários finais encontrarão uma opção nas guias Forms e Rascunho enviados do Forms para iniciar um novo formulário usando dados de um formulário enviado. A imagem a seguir destaca essa opção.

![start-a-new-form](assets/start-a-new-form.png)

Ao clicar no botão para iniciar um novo formulário, ele abre um novo formulário com dados do formulário enviado correspondente. Agora é possível revisar e atualizar as informações, conforme necessário, e enviar o formulário.
