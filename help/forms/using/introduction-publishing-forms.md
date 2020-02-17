---
title: Introdução à publicação de formulários em um portal
seo-title: Introdução à publicação de formulários em um portal
description: O AEM Forms fornece componentes que podem ser usados para criar o portal de formulários. Este artigo apresenta os componentes disponíveis do portal de formulários.
seo-description: O AEM Forms fornece componentes que podem ser usados para criar o portal de formulários. Este artigo apresenta os componentes disponíveis do portal de formulários.
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# Introdução à publicação de formulários em um portal{#introduction-to-publishing-forms-on-a-portal}

## Visão geral dos componentes do portal do AEM Forms {#aem-forms-portal-components-overview}

Em um cenário típico de implantação de portal centrado em formulários, o desenvolvimento de formulários e o desenvolvimento de portal são duas atividades disjuntas. Enquanto os designers de formulário criam e armazenam formulários em um repositório, os desenvolvedores da Web criam um aplicativo da Web para listar formulários e manipular o envio de formulários. Os formulários são copiados para a camada da Web, pois não há comunicação entre o repositório de formulários e o aplicativo da Web.

Tais cenários muitas vezes resultam em problemas de gerenciamento e atrasos na produção. Por exemplo, se houver uma versão mais recente de um formulário disponível no repositório, será necessário substituir o formulário na camada da Web, modificar o aplicativo da Web e reimplantar o formulário no site público. A reimplantação do aplicativo da Web pode causar algum tempo de inatividade do servidor. Normalmente, o tempo de inatividade do servidor é uma atividade planejada e, portanto, as alterações não podem ser enviadas para o site público instantaneamente.

O AEM Forms fornece componentes de portal que reduzem as despesas gerais de gerenciamento e os atrasos na produção. Os componentes equipam os desenvolvedores da Web para criar e personalizar um portal de formulários em sites criados usando o Adobe Experience Manager (AEM).

![Portal do AEM Forms](assets/aem-forms-portal.png)

Os componentes do portal de formulários permitem adicionar a seguinte funcionalidade:

* Liste formulários em layouts personalizados. Os layouts de exibição de lista, de exibição de cartão e de painel estão prontos para uso. Você pode criar seus próprios layouts personalizados.
* Permite que você exiba metadados personalizados e ações personalizadas ao listá-los.
* Liste os formulários publicados pela interface do usuário do AEM Forms na instância de publicação em que os componentes do Portal do Forms estão sendo usados.
* Permite que os usuários finais renderizem formulários em HTML e PDF.
* Use o perfil HTML personalizado para renderizar formulários.
* Ative a pesquisa de formulários com base em vários critérios, como propriedades de formulários, metadados e tags.
* Enviar dados de formulário para um servlet.
* Use o CSS personalizado para personalizar a aparência do portal.
* Crie links para formulários.
* Lista os rascunhos e envios relacionados ao Formulário adaptativo criado pelo usuário final.

## Componentes disponíveis do portal do AEM Forms {#available-aem-forms-portal-components}

O AEM Forms fornece os seguintes componentes de portal prontos para uso, agrupados em grupos de componentes do **Document Services** e do **Document Services Predicates** :

### Pesquisa e Lister {#search-amp-lister}

O componente de Pesquisa e Lister permite que você liste formulários do repositório de formulários na página do portal e fornece opções de configuração para listar formulários com base em critérios especificados. Também permite especificar critérios de pesquisa para permitir que os usuários do portal pesquisem na lista de formulários.

### Rascunhos e envios {#drafts-amp-submissions}

Enquanto o componente Pesquisar e Lister exibe formulários que são tornados públicos pelo autor do Forms , o componente Rascunhos e Submissões exibe formulários que são salvos como rascunho para preencher formulários posteriores e enviados. Este componente fornece experiência personalizada para qualquer usuário conectado.

### Link {#link}

O componente Link permite criar um link para um formulário em qualquer lugar na página. Considere um cenário em que você está oferecendo um programa de treinamento e deseja que os usuários enviem um formulário para se inscreverem no treinamento. Em seu site, você postou os detalhes do programa. Abaixo dos detalhes, forneça um link para o formulário de inscrição. O componente Link pode ajudá-lo a criar esse link.

## Fluxo de trabalho do Portal de formulários {#forms-portal-workflow}

O portal de formulários permite que você liste formulários do repositório de formulários na página do portal. Também permite especificar critérios de pesquisa para permitir que os usuários do portal pesquisem na lista de formulários. Você também pode usar o componente Rascunhos e envios para exibir formulários salvos como rascunho para preencher formulários posteriores e enviados. É necessário executar um determinado conjunto de operações antes que essas funcionalidades fiquem disponíveis em uma página Sites. Execute as etapas na sequência listada para disponibilizar os componentes e as respectivas funcionalidades em uma página de sites:

1. **Ativar componentes** do Portal de formulários:Os componentes do portal de formulários não estão disponíveis para uso. [Ative os componentes do sidekick](/help/forms/using/enabling-forms-portal-components.md) do AEM para uma página do AEM Sites.
1. **** Listar formulários em uma página (criar página do portal de formulários): Você pode listar formulários em páginas do AEM Sites e páginas que não sejam do AEM Site. A lista contém formulários disponíveis na instância de publicação. Um usuário pode abrir formulários e começar a preenchê-los. Sempre que um usuário abre um formulário, uma nova instância do formulário é criada:

   1. **Listar formulários em uma página** do AEM Sites: Adicione o componente **[Pesquisar e Lister](../../forms/using/creating-form-portal-page.md)**à página e configure o Painel**[ de](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** lista nela, para listar formulários em uma página. Adicione e configure o componente Painel **de** pesquisa no componente **Pesquisar e Lister** também para adicionar a funcionalidade de pesquisa à página. A página com o componente de portal de formulários é conhecida como página [do portal de](../../forms/using/creating-form-portal-page.md)formulários.

   1. **** Listar formulários em uma página que não seja do AEM Sites: Use as APIs [de pesquisa do portal de](/help/forms/using/listing-forms-webpage-using-apis.md) formulários para consultar, recuperar e listar formulários em páginas que não sejam do AEM Sites.

1. **Listar formulários rascunhos e enviados em uma página** do portal de formulários: Adicione e configure o componente Rascunhos e envios para a página do portal de formulários. O componente lista todos os formulários que estão no estado de rascunho e os formulários que já foram enviados.

   Para permitir que um formulário adaptado enviado apareça na guia envios, defina a ação **** Enviar como Ação **[de envio do Portal de](configuring-submit-actions.md)formulários.**Como alternativa, ative a opção Enviar do portal de formulários. Sempre que um usuário envia o formulário, ele é adicionado à guia Envios.

1. **** Configure o armazenamento para os dados de rascunho e formulários enviados: Por padrão, os dados de rascunho e envios são armazenados no repositório do AEM. Em um ambiente de produção, é recomendável não armazenar dados de formulário preliminares ou enviados no repositório do AEM. [Configure o componente do portal de formulários para salvar dados em um local](../../forms/using/draft-submission-component.md#customizing-the-storage)seguro.
1. **** (Opcional) Personalização dos componentes do portal de formulários: [Personalize seus modelos](../../forms/using/customizing-templates-forms-portal-components.md) de página do portal de formulários para fornecer uma aparência distinta aos componentes.
1. **** (Opcional) Adicione metadados personalizados a formulários: [Adicione metadados personalizados a formulários](../../forms/using/customizing-templates-forms-portal-components.md) para melhorar a experiência de listagem e pesquisa.
1. **** Publicar a página do portal de formulários: A página do portal de formulários está pronta. Publique a página.

## Artigos relacionados {#related-articles}

* [Ativar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md)
* [Criar página do portal de formulários](../../forms/using/creating-form-portal-page.md)
* [Listar formulários em uma página da Web usando APIs](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar componente Rascunhos e envios](../../forms/using/draft-submission-component.md)
* [Personalizar o armazenamento de rascunhos e formulários enviados](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [Amostra para integrar o componente de rascunhos e envios ao banco de dados](integrate-draft-submission-database.md)
* [Personalização de modelos para componentes do portal de formulários](../../forms/using/customizing-templates-forms-portal-components.md)
* [Introdução à publicação de formulários em um portal](../../forms/using/introduction-publishing-forms.md)

