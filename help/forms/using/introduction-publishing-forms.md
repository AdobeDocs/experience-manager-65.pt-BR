---
title: Introdução à publicação de formulários em um portal
seo-title: Introduction to publishing forms on a portal
description: A AEM Forms fornece componentes que você pode usar para criar seu portal de formulários. Este artigo apresenta os componentes disponíveis do portal de formulários.
seo-description: AEM Forms provides with components that you can use to build your forms portal. This articles introduces you to the available forms portal components.
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
exl-id: 240ed4d8-b21b-46eb-80a9-9e8093b77235
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 0%

---

# Introdução à publicação de formulários em um portal{#introduction-to-publishing-forms-on-a-portal}

## Visão geral dos componentes do portal do AEM Forms {#aem-forms-portal-components-overview}

Em um cenário típico de implantação de portal centrada em formulários, o desenvolvimento de formulários e o desenvolvimento de portal são duas atividades distintas. Enquanto os designers de formulários criam e armazenam formulários em um repositório, os desenvolvedores da Web criam um aplicativo da Web para listar formulários e manipular o envio de formulários. Os Forms são copiados para o nível da Web, pois não há comunicação entre o repositório de formulários e o aplicativo web.

Esses cenários geralmente resultam em problemas de gerenciamento e atrasos de produção. Por exemplo, se houver uma versão mais recente de um formulário disponível no repositório, você precisará substituir o formulário no nível da Web, modificar o aplicativo da Web e reimplantar o formulário no site público. A reimplantação do aplicativo Web pode causar algum tempo de inatividade do servidor. Normalmente, o tempo de inatividade do servidor é uma atividade planejada e, portanto, as alterações não podem ser enviadas para o site público instantaneamente.

A AEM Forms fornece componentes de portal que reduzem as despesas gerais de gerenciamento e os atrasos de produção. Os componentes fazem com que os desenvolvedores da Web criem e personalizem um portal de formulários em sites criados usando o Adobe Experience Manager (AEM).

![Portal do AEM Forms](assets/aem-forms-portal.png)

Os componentes do portal de formulários permitem que você adicione a seguinte funcionalidade:

* Listar formulários em layouts personalizados. Os layouts de exibição de Lista, Cartão e Painel prontos para uso são fornecidos. Você pode criar seus próprios layouts personalizados.
* Permite exibir metadados personalizados, bem como ações personalizadas, ao listá-los.
* Listar formulários publicados pela interface do usuário do AEM Forms na instância de publicação em que os componentes do Forms Portal estão sendo usados.
* Permite que os usuários finais renderizem formulários no formato HTML, bem como no formato PDF.
* Use o perfil de HTML personalizado para renderizar formulários.
* Permita a pesquisa de formulários com base em vários critérios, como propriedades de formulário, metadados e tags.
* Enviar dados de formulário para um servlet.
* Use o CSS personalizado para personalizar a aparência do portal.
* Criar links para formulários.
* Lista rascunhos e envios relacionados ao Formulário adaptável criado pelo usuário final.

## Componentes disponíveis do portal do AEM Forms {#available-aem-forms-portal-components}

O AEM Forms fornece os seguintes componentes do portal prontos para uso, agrupados em **Serviços de documento** e **Predicados de serviços de documento** grupos de componentes:

### Pesquisa e Lister {#search-amp-lister}

O componente de Pesquisa e Listagem permite listar formulários do repositório de formulários na página do portal e fornece opções de configuração para listar formulários com base em critérios especificados. Ela também permite especificar critérios de pesquisa para permitir que os usuários do portal pesquisem na lista de formulários.

### Rascunhos e envios {#drafts-amp-submissions}

Enquanto o componente Pesquisa e Lister exibe formulários que são tornados públicos pelo autor do Forms, o componente Rascunhos e envios exibe formulários que são salvos como rascunho para concluir formulários posteriores e enviados. Este componente fornece experiência personalizada para qualquer usuário conectado.

### Link {#link}

O componente Link permite criar um link para um formulário em qualquer lugar da página. Considere um cenário em que você está oferecendo um programa de treinamento e deseja que seus usuários enviem um formulário para se registrarem no treinamento. Em seu site, você postou os detalhes do programa. Abaixo dos detalhes, você deseja fornecer um link para o formulário de registro. O componente Link pode ajudar você a criar esse link.

## Fluxo de trabalho do portal do Forms {#forms-portal-workflow}

O Forms portal permite listar formulários do repositório de formulários na página do portal. Ela também permite especificar critérios de pesquisa para permitir que os usuários do portal pesquisem na lista de formulários. Você também pode usar o componente Rascunhos e envios para exibir formulários salvos como rascunho para preencher formulários e enviados posteriormente. É necessário executar um determinado conjunto de operações antes que essas funcionalidades fiquem disponíveis em uma página do Sites. Execute as etapas na sequência listada para disponibilizar os componentes e as respectivas funcionalidades em uma página de sites:

1. **Habilitar componentes do Forms Portal**: pronto para uso, os componentes do portal de formulários não estão disponíveis para uso. [Ativar os componentes do AEM sidekick](/help/forms/using/enabling-forms-portal-components.md) para uma página do AEM Sites.
1. **Listar formulários em uma página (criar página do portal de formulários):** Você pode listar formulários em páginas de site AEM Sites e não AEM. A lista contém formulários disponíveis na instância de publicação. Um usuário pode abrir formulários e começar a preenchê-los. Sempre que um usuário abrir um formulário, uma nova instância do formulário será criada:

   1. **Listar formulários em uma página do AEM Sites**: adicione o **[Pesquisa e Lister](../../forms/using/creating-form-portal-page.md)** componente à página e configure o **[Painel Lista](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** nele, para listar formulários em uma página. Adicione e configure o **Painel de pesquisa** componente para a **Pesquisa e Lister** também para adicionar a funcionalidade de pesquisa à página. A página com o componente de portal de formulários é conhecida como [página do portal de formulários](../../forms/using/creating-form-portal-page.md).

   1. **Listar formulários em uma página que não seja do AEM Sites:** Use o [APIs de pesquisa do portal de formulários](/help/forms/using/listing-forms-webpage-using-apis.md) para consultar, recuperar e listar formulários em páginas que não sejam do AEM Sites.

1. **Listar rascunhos e formulários enviados em uma página do portal de formulários**: adicione e configure o componente Rascunhos e envios à página do portal Formulários. O componente lista todos os formulários que estão no estado de rascunho e os formulários que já foram enviados.

   Para permitir que um formulário adaptável enviado seja exibido na guia envios, defina o **Enviar ação** para **[Ação de envio do portal do Forms](configuring-submit-actions.md).** Como alternativa, habilite a opção Enviar do Forms Portal. Sempre que um usuário enviar o formulário, ele será adicionado à guia Envios.

1. **Configurar o armazenamento para os dados de rascunho e de formulários enviados:** Por padrão, os dados de rascunho e envio são armazenados no repositório do AEM. Em um ambiente de produção, é recomendável não armazenar dados de rascunho ou de formulário enviados no repositório do AEM. [Configurar o componente de portal de formulários para salvar dados em um local seguro](../../forms/using/draft-submission-component.md#customizing-the-storage).
1. **(Opcional) Personalização dos componentes do portal de formulários:** [Personalizar seus modelos de página do portal de formulários](../../forms/using/customizing-templates-forms-portal-components.md) para dar uma aparência distinta aos componentes.
1. **(Opcional) Adicione metadados personalizados a formulários:** [Adicionar metadados personalizados a formulários](../../forms/using/customizing-templates-forms-portal-components.md) para melhorar a listagem e a experiência de pesquisa.
1. **Publicar a página do portal de formulários:** A página do portal de formulários está pronta. Publique a página.

## Artigos relacionados {#related-articles}

* [Habilitar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md)
* [Criar página do portal de formulários](../../forms/using/creating-form-portal-page.md)
* [Listar formulários em uma página da Web usando APIs](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar componente de rascunhos e envios](../../forms/using/draft-submission-component.md)
* [Personalizar o armazenamento de rascunhos e formulários enviados](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [Amostra para integrar o componente de rascunhos e envios ao banco de dados](integrate-draft-submission-database.md)
* [Personalização de modelos para componentes do portal de formulários](../../forms/using/customizing-templates-forms-portal-components.md)
* [Introdução à publicação de formulários em um portal](../../forms/using/introduction-publishing-forms.md)
