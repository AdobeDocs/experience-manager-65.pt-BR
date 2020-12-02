---
title: Acessar e preencher formulários publicados
seo-title: Acessar e preencher formulários publicados
description: O Forms Portal equipe os desenvolvedores da Web com componentes para criar e personalizar um portal de formulários em sites criados usando o Adobe Experience Manager (AEM).
seo-description: O Forms Portal equipe os desenvolvedores da Web com componentes para criar e personalizar um portal de formulários em sites criados usando o Adobe Experience Manager (AEM).
uuid: 44731604-5d97-46fa-baa9-0c020c634fa7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 88dc8ef2-95ce-4906-ac28-eecc3a32a64e
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 0%

---


# Acessar e preencher formulários publicados{#accessing-and-filling-published-forms}

Em uma configuração de implantação de portal centrada em formulários, o desenvolvimento de formulários e o desenvolvimento de portal são duas atividades distintas. Enquanto os designers de formulário criam e armazenam formulários em um repositório, os desenvolvedores da Web criam um aplicativo da Web para esses formulários de lista e lidam com envios. A Forms é copiada para a camada da Web, pois não há comunicação entre o repositório de formulários e o aplicativo da Web.

Geralmente, isso resulta em problemas com o gerenciamento da configuração e dos atrasos de produção. Por exemplo, se uma versão mais recente de um formulário estiver disponível no repositório, o designer de formulários, substituirá o formulário na camada da Web, modificará o aplicativo da Web e reimplantará o formulário no site público. A reimplantação do aplicativo da Web pode causar algum tempo de inatividade do servidor. Como o tempo de inatividade do servidor é uma atividade planejada, as alterações não podem ser enviadas imediatamente para o site público.

O Forms Portal reduz as despesas gerais de gerenciamento e os atrasos na produção. Ela equipe os desenvolvedores da Web com componentes para criar e personalizar um portal de formulários em sites criados usando o Adobe Experience Manager (AEM).

Para obter mais informações sobre o portal de formulários e seus recursos, consulte [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md).

## Introdução ao portal de formulários {#getting-started-with-forms-portal}

Navegue até a página do portal de formulários publicados. Para obter mais informações sobre como criar uma página de portal de formulários, consulte [Criar uma página de portal de formulários](../../forms/using/creating-form-portal-page.md).

O componente de Pesquisa e Lister do portal de roms exibe os formulários disponíveis na instância de Publicação do servidor de AEM. Essa lista inclui todos os formulários ou formulários definidos no filtro no momento da criação da página do portal de formulários. Uma página do portal de formulários é semelhante à exibida na seguinte imagem:

![Uma página de portal de formulários de amostra  ](assets/forms-portal-page.png)

Uma página de portal de formulários de amostra

### Pesquisar e Lister {#search-and-lister}

O componente de Pesquisa e Lister permite que você adicione a seguinte funcionalidade ao seu portal de formulários:

* Formulários de lista no painel, na placa ou na visualização de grade que estão disponíveis prontamente. Também oferece suporte a modelos personalizadosListe formulários de pastas específicas no Forms Manager.
* Especifique como os formulários são renderizados - HTML5, PDF ou ambos.
* Especifique como os formulários PDF e XFA são renderizados - HTML5, PDF ou ambos. Formulários não XFA como HTML5.
* Ative a pesquisa de formulários com base em critérios, como propriedades de formulários, metadados e tags.
* Enviar dados de formulário para um servlet.
* Use folhas de estilos personalizadas (CSS) para personalizar a aparência do portal.
* Crie links para formulários.

Você pode pesquisar formulários na página do Forms Portal usando as seguintes opções:

* Pesquisa de texto completo
* Pesquisa avançada

A pesquisa de texto completo permite que você localize e lista formulários com base nas palavras-chave especificadas.

![Uma caixa de diálogo de pesquisa avançada](assets/search-panel.png)

Uma caixa de diálogo de pesquisa avançada

A pesquisa avançada permite pesquisar formulários com base em propriedades de formulário especificadas. Isso fornece resultados mais específicos do que pesquisa de texto completo. A pesquisa avançada inclui a pesquisa com base em tags, propriedades (como Autor, Descrição e Título), data de modificação e texto completo.

O Lister exibe formulários com base nos parâmetros de pesquisa. Cada formulário no resultado da pesquisa é exibido com um ícone, que é hipervinculado ao formulário associado. Você pode clicar no ícone para abrir e trabalhar com o formulário associado.

### Preenchimento de um formulário {#filling-a-form}

![Um exemplo de formulário adaptável](assets/filling_a_form.png)

Um exemplo de formulário adaptável

Os formulários podem ser acessados a partir do link fornecido junto com o formulário no componente de Pesquisa e Lister da página.

Cada formulário contém informações de ajuda que permitem ao usuário preencher o formulário.

#### Rascunhos e envio {#drafts-and-submission}

Um usuário tem a opção de salvar um rascunho de um formulário clicando no botão Salvar. Isso permite que o usuário trabalhe em um formulário durante um período de tempo antes de enviar o formulário.

Os dados preenchidos no formulário (incluindo anexos) são salvos como rascunho no servidor. O rascunho de um formulário pode ser salvo várias vezes. O formulário salvo é exibido na guia Rascunhos do componente Rascunho e envio da página.

Após o preenchimento do formulário, o usuário envia os formulários clicando no botão Enviar do formulário. Os formulários enviados são exibidos na guia Envios do componente Rascunho e envio da página.

>[!NOTE]
>
>Os formulários enviados são exibidos na guia Forms Enviado somente se a ação de envio para o formulário adaptativo estiver configurada como Ação de envio do Forms Portal. Para obter mais informações sobre ações de envio, consulte [Configuração da ação Enviar](../../forms/using/configuring-submit-actions.md).

![Componente Rascunhos e envios](assets/draft-submission.png)

Componente Rascunhos e envios

## Start de um novo formulário usando dados de formulário enviados {#start-a-new-form-using-submitted-form-data}

Há determinados formulários que você precisa preencher e enviar com muita frequência. Por exemplo, o formulário para o depósito da declaração de imposto individual é enviado todos os anos. Nesses casos, enquanto algumas informações mudam cada vez que você preenche o formulário, a maioria, como os detalhes pessoais e familiares, não é alterada. No entanto, ainda é necessário preencher o formulário inteiro novamente, do zero.

A AEM Forms pode ajudar a otimizar a experiência de preenchimento do formulário e reduzir significativamente o tempo de preenchimento e envio do formulário novamente. Os usuários finais podem start um novo formulário usando dados de um formulário enviado. Essa funcionalidade é integrada no componente [Rascunhos e envios](../../forms/using/draft-submission-component.md). Quando você adiciona rascunhos e componentes de envio à página do portal de formulários e a publica, os usuários finais encontram uma opção nas guias Forms e Forms de rascunho enviados para start de um novo formulário usando dados de um formulário enviado. A imagem a seguir destaca essa opção.

![start-a-novo-formulário](assets/start-a-new-form.png)

Quando você clica no botão para iniciar um novo formulário, ele abre um novo formulário com dados do formulário enviado correspondente. Agora é possível revisar e atualizar as informações, conforme necessário, e enviar o formulário.
