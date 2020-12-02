---
title: Introdução à publicação de formulários em um portal
seo-title: Introdução à publicação de formulários em um portal
description: A AEM Forms fornece componentes que você pode usar para criar o portal de formulários. Este artigo apresenta os componentes disponíveis do portal de formulários.
seo-description: A AEM Forms fornece componentes que você pode usar para criar o portal de formulários. Este artigo apresenta os componentes disponíveis do portal de formulários.
uuid: 658de12b-66e5-438b-ae8f-872ec11a9c3e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9f1beb89-8eb1-4e37-a5e8-19752b21374a
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 0%

---


# Introdução à publicação de formulários em um portal{#introduction-to-publishing-forms-on-a-portal}

## Visão geral dos componentes do portal do AEM Forms {#aem-forms-portal-components-overview}

Em um cenário típico de implantação de portal centrado em formulários, o desenvolvimento de formulários e o desenvolvimento de portal são duas atividades disjuntas. Enquanto os Form Designers criam e armazenam formulários em um repositório, os desenvolvedores da Web criam um aplicativo da Web para lista de formulários e manipular o envio de formulários. A Forms é copiada para a camada da Web, pois não há comunicação entre o repositório de formulários e o aplicativo da Web.

Tais cenários muitas vezes resultam em problemas de gerenciamento e atrasos na produção. Por exemplo, se houver uma versão mais recente de um formulário disponível no repositório, será necessário substituir o formulário na camada da Web, modificar o aplicativo da Web e reimplantar o formulário no site público. A reimplantação do aplicativo da Web pode causar algum tempo de inatividade do servidor. Geralmente, o tempo de inatividade do servidor é uma atividade planejada e, portanto, as alterações não podem ser enviadas para o site público instantaneamente.

A AEM Forms fornece componentes de portal que reduzem as despesas gerais de gerenciamento e os atrasos na produção. Os componentes equipam os desenvolvedores da Web para criar e personalizar um portal de formulários em sites criados usando o Adobe Experience Manager (AEM).

![Portal AEM Forms](assets/aem-forms-portal.png)

Os componentes do portal de formulários permitem adicionar a seguinte funcionalidade:

* Lista de formulários em layouts personalizados. São fornecidos layouts prontos para uso imediato, visualização da Lista, visualização da placa e visualização do painel. Você pode criar seus próprios layouts personalizados.
* Permite que você exiba metadados personalizados e ações personalizadas ao listá-los.
* Formulários de lista publicados pela interface do usuário do AEM Forms na instância de publicação em que os componentes do Forms Portal estão sendo usados.
* Permite que os usuários finais renderizem formulários em HTML e PDF.
* Use o perfil HTML personalizado para renderizar formulários.
* Ative a pesquisa de formulários com base em vários critérios, como propriedades de formulários, metadados e tags.
* Enviar dados de formulário para um servlet.
* Use o CSS personalizado para personalizar a aparência do portal.
* Crie links para formulários.
* Rascunhos e envios do Lista relacionados ao Formulário adaptável criado pelo usuário final.

## Componentes disponíveis do portal da AEM Forms {#available-aem-forms-portal-components}

A AEM Forms fornece os seguintes componentes de portal prontos para uso, agrupados em **Documento Services** e **Documentos Services Predicates** grupos de componentes:

### Pesquisa e Lister {#search-amp-lister}

O componente de Pesquisa e Lister permite que você lista formulários do repositório de formulários para a página do portal e fornece opções de configuração para lista de formulários com base em critérios especificados. Também permite especificar critérios de pesquisa para permitir que os usuários do portal pesquisem na lista de formulários.

### Rascunhos e envios {#drafts-amp-submissions}

Enquanto o componente Pesquisar e Lister exibe formulários que são tornados públicos pelo autor do Forms, o componente Rascunhos e envios exibe formulários que são salvos como rascunho para preencher formulários posteriores e enviados. Este componente fornece experiência personalizada para qualquer usuário conectado.

### Link {#link}

O componente Link permite criar um link para um formulário em qualquer lugar na página. Considere um cenário em que você está oferecendo um programa de treinamento e deseja que os usuários enviem um formulário para se inscreverem no treinamento. Em seu site, você postou os detalhes do programa. Abaixo dos detalhes, forneça um link para o formulário de inscrição. O componente Link pode ajudá-lo a criar esse link.

## Fluxo de trabalho do Forms Portal {#forms-portal-workflow}

O portal da Forms permite que você lista formulários do repositório de formulários para a página do portal. Também permite especificar critérios de pesquisa para permitir que os usuários do portal pesquisem na lista de formulários. Você também pode usar o componente Rascunhos e envios para exibir formulários salvos como rascunho para preencher formulários posteriores e enviados. É necessário executar um determinado conjunto de operações antes que essas funcionalidades fiquem disponíveis em uma página Sites. Execute as etapas na sequência listada para disponibilizar os componentes e as respectivas funcionalidades em uma página de sites:

1. **Ativar componentes** do Forms Portal: Os componentes do portal de formulários não estão disponíveis para uso. [Habilite os componentes AEM ](/help/forms/using/enabling-forms-portal-components.md) sidekickickickie para uma página do AEM Sites.
1. **Lista de formulários em uma página (criar página do portal de formulários):** É possível lista de formulários em páginas do AEM Sites e não AEM Site. A lista contém formulários disponíveis na instância de publicação. Um usuário pode abrir formulários e start preenchendo esses formulários. Sempre que um usuário abre um formulário, uma nova instância do formulário é criada:

   1. **Lista de formulários em uma página** do AEM Sites: Adicione o componente  **[Pesquisar e](../../forms/using/creating-form-portal-page.md)** Listerer à página e configure a  **[Lista](../../forms/using/creating-form-portal-page.md#p-list-pane-p)** e coloque-o em um formulário de lista em uma página. Adicione e configure o componente **Painel de pesquisa** para o componente **Pesquisar e Lister** também para adicionar a funcionalidade de pesquisa à página. A página com o componente do portal de formulários é conhecida como [página do portal de formulários](../../forms/using/creating-form-portal-page.md).

   1. **Formulários de lista em uma página que não seja a AEM Sites:** Use as  [APIs de pesquisa do portal de formulários ](/help/forms/using/listing-forms-webpage-using-apis.md) para query, recuperação e lista de formulários em páginas que não sejam da AEM Sites.

1. **Rascunho de lista e formulários enviados em uma página** do portal de formulários: Adicione e configure o componente Rascunhos e envios para a página do portal de formulários. O componente lista todos os formulários que estão no estado de rascunho e os formulários que já foram enviados.

   Para permitir que um formulário adaptado enviado apareça na guia envios, defina **Enviar ação** como **[Ação de envio do portal do Forms](configuring-submit-actions.md).** Como alternativa, ative a opção Enviar do Forms Portal. Sempre que um usuário envia o formulário, ele é adicionado à guia Envios.

1. **Configurar armazenamento para os dados de rascunho e formulários enviados:** Por padrão, os dados de rascunho e envio são armazenados no repositório AEM. Em um ambiente de produção, é recomendável não armazenar dados de formulário preliminares ou enviados AEM repositório. [Configure o componente do portal de formulários para salvar dados em um local](../../forms/using/draft-submission-component.md#customizing-the-storage) seguro.
1. **(Opcional) Personalizar os componentes do portal de formulários:** [Personalize os ](../../forms/using/customizing-templates-forms-portal-components.md) modelos de página do portal de formulários para fornecer uma aparência distinta aos componentes.
1. **(Opcional) Adicione metadados personalizados a formulários:** [adicione metadados personalizados a ](../../forms/using/customizing-templates-forms-portal-components.md) formulários para aprimorar a experiência de pesquisa e listagem.
1. **Publicar a página do portal de formulários:** Sua página do portal de formulários está pronta. Publique a página.

## Artigos relacionados {#related-articles}

* [Ativar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md)
* [Criar página do portal de formulários](../../forms/using/creating-form-portal-page.md)
* [Lista de formulários em uma página da Web usando APIs](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar componente Rascunhos e envios](../../forms/using/draft-submission-component.md)
* [Personalizar o armazenamento de rascunhos e formulários enviados](../../forms/using/draft-submission-component.md#customizing-the-storage)
* [Amostra para integrar o componente de rascunhos e envios ao banco de dados](integrate-draft-submission-database.md)
* [Personalização de modelos para componentes do portal de formulários](../../forms/using/customizing-templates-forms-portal-components.md)
* [Introdução à publicação de formulários em um portal](../../forms/using/introduction-publishing-forms.md)

