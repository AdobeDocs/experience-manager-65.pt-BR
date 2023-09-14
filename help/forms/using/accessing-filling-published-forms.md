---
title: Acesso e preenchimento de formulários publicados
description: O Forms Portal equipe os desenvolvedores da Web com componentes para criar e personalizar um Forms Portal em sites criados usando o Adobe Experience Manager AEM ().
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: aedf890c-a2f1-412f-8897-2492ffab335a
source-git-commit: e33816b3b8d190e185d2b23dad3a05aca272f01c
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# Acesso e preenchimento de formulários publicados{#accessing-and-filling-published-forms}

Em uma configuração de implantação de portal centrada em formulários, o desenvolvimento de formulários e o desenvolvimento de portal são duas atividades distintas. Enquanto designers de formulários criam e armazenam formulários em um repositório, os desenvolvedores da Web criam um aplicativo da Web para listar formulários e manipular envios. Em seguida, os Forms são copiados para o nível da Web, pois não há comunicação entre o repositório de formulários e o aplicativo Web.

Isso geralmente resulta em problemas com o gerenciamento de atrasos de configuração e produção. Por exemplo, se uma versão mais recente de um formulário estiver disponível no repositório, o Designer de formulários substituirá o formulário no nível da Web, modificará o aplicativo da Web e reimplantará o formulário no site público. A reimplantação do aplicativo Web pode causar algum tempo de inatividade do servidor. Como o tempo de inatividade do servidor é uma atividade planejada, as alterações não podem ser enviadas para o site público imediatamente.

O Forms Portal reduz as despesas gerais de gerenciamento e os atrasos de produção. Ele equipe os desenvolvedores da Web com componentes para criar e personalizar um Portal do Forms em sites criados usando o Adobe Experience Manager (AEM).

Para obter mais informações sobre o Forms Portal e seus recursos, consulte [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md).

## Introdução ao Forms Portal {#getting-started-with-forms-portal}

Navegue até a página do Forms Portal publicada. Para obter mais informações sobre como criar uma página do Forms Portal, consulte [Criação de uma página do Forms Portal](../../forms/using/creating-form-portal-page.md).

O componente de Pesquisa e Lister do Forms Portal exibe os formulários disponíveis na instância de Publicação do servidor AEM. Essa lista inclui todos os formulários ou os formulários definidos no filtro no momento da criação da página do Forms Portal. Uma página do Forms Portal é semelhante à exibida na imagem a seguir:

![Um exemplo de página do portal de formulários ](assets/forms-portal-page.png)

Um exemplo de página do Forms Portal

### Pesquisa e listagem {#search-and-lister}

O componente de Pesquisa e Lister permite adicionar a seguinte funcionalidade ao Forms Portal:

* Listar formulários na exibição de painel, cartão ou grade que estão disponíveis imediatamente. Também aceita formulários templatesList personalizados de pastas específicas no Forms Manager.
* Especifique como os formulários são renderizados - HTML5, PDF ou ambos.
* Especifique como os formulários PDF e XFA são renderizados - HTML5, PDF ou ambos. Formulários não XFA como HTML5.
* Permita a pesquisa de formulários com base em critérios, como propriedades de formulário, metadados e tags.
* Enviar dados de formulário para um servlet.
* Use folhas de estilos personalizadas (CSS) para personalizar a aparência do portal.
* Criar links para formulários.

Você pode pesquisar formulários na página do Forms Portal usando as seguintes opções:

* Pesquisa de Texto Completo
* Pesquisa avançada

A pesquisa de texto completo permite localizar e listar formulários com base nas palavras-chave especificadas.

![Uma caixa de diálogo de pesquisa avançada](assets/search-panel.png)

Uma caixa de diálogo de pesquisa avançada

A Pesquisa avançada permite pesquisar formulários com base nas propriedades de formulário especificadas. Isso fornece um resultado mais específico do que a pesquisa de texto completo. A pesquisa avançada inclui pesquisas baseadas em tags, propriedades (como Autor, Descrição e Título), data de modificação e texto completo.

A Lista exibe formulários com base nos parâmetros de pesquisa. Cada formulário no resultado da pesquisa é exibido com um ícone, que está hipervinculado ao formulário associado. Você pode clicar no ícone para abrir e trabalhar com o formulário associado.

### Preenchimento de um formulário {#filling-a-form}

![Um exemplo de formulário adaptável](assets/filling_a_form.png)

Um exemplo de formulário adaptável

Os formulários podem ser acessados pelo link fornecido junto com o formulário no componente de Pesquisa e Lister da página.

Cada formulário contém informações de ajuda que permitem ao usuário preencher o formulário.

#### Rascunhos e envio {#drafts-and-submission}

Como opção, um usuário pode salvar o rascunho de um formulário clicando em **Salvar**. Isso permite que o usuário trabalhe em um formulário por um período de tempo antes de enviar o formulário.

Os dados preenchidos no formulário (incluindo anexos) são salvos como rascunho no servidor. O rascunho de um formulário pode ser salvo qualquer número de vezes. O formulário salvo aparece na guia Rascunhos do componente Rascunho e envio da página.

Após o preenchimento do formulário, o usuário envia os formulários clicando no botão Submit no formulário. Os formulários enviados aparecem na guia Envios do componente Rascunho e envio da Página.

>[!NOTE]
>
>Os formulários enviados aparecerão na guia Forms enviado somente se a ação enviar para o formulário adaptável estiver configurada como Ação enviar do Forms Portal. Para obter mais informações sobre ações de envio, consulte [Configuração da ação Enviar](../../forms/using/configuring-submit-actions.md).

![Rascunhos e componentes de envios](assets/draft-submission.png)

Rascunhos e componentes de envios

## Iniciar um novo formulário usando dados de formulário enviados {#start-a-new-form-using-submitted-form-data}

Há determinados formulários que você deve preencher e enviar com frequência. Por exemplo, o formulário para apresentar uma declaração de imposto individual é enviado todos os anos. Nesses casos, enquanto parte das informações muda sempre que você preenche o formulário, a maioria delas, como os detalhes pessoais e familiares, não muda. No entanto, ainda é necessário preencher todo o formulário novamente, do zero.

O AEM Forms pode ajudar a otimizar a experiência de preenchimento do formulário e reduzir significativamente o tempo para preencher e enviar um formulário novamente. Os usuários finais podem iniciar um novo formulário usando dados de um formulário enviado. Essa funcionalidade é incorporada no [Rascunhos e componentes de envios](../../forms/using/draft-submission-component.md). Ao adicionar o componente Rascunhos e envio à página do Forms Portal e publicá-lo, os usuários finais veem uma opção nas guias Forms enviado e Rascunho do Forms. A opção permite iniciar um novo formulário usando dados de um formulário enviado. A imagem a seguir destaca essa opção.

![start-a-new-form](assets/start-a-new-form.png)

Ao clicar no botão para iniciar um novo formulário, ele abre um novo formulário com dados do formulário enviado correspondente. Agora você pode revisar e atualizar as informações, conforme necessário, e enviar o formulário.
