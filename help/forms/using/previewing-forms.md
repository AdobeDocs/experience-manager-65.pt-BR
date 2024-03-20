---
title: Pré-visualização de um formulário
description: Você pode visualizar seus formulários antes de publicá-los ou ativá-los para garantir que atendam às expectativas. As opções de visualização podem variar entre os tipos de formulário compatíveis.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
feature: Adaptive Forms, Foundation Components
exl-id: aed5703e-4fe6-4839-9657-c660ac48521e
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 2%

---

# Pré-visualização de um formulário {#previewing-a-form}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

## Visão geral {#overview}

No AEM Forms, é possível visualizar os formulários e documentos presentes no repositório. A Pré-visualização ajuda a saber exatamente como os formulários são exibidos e se comportam quando são lançados para os usuários finais.

Ao visualizar formulários, eles são renderizados na interface interativa e o usuário pode preencher os formulários com dados. Ao visualizar documentos, eles são renderizados no modo não interativo e o usuário só pode visualizar o documento. Para formulários, uma opção adicional de Visualização personalizada está disponível. Com essa opção, é possível visualizar o formulário usando dados de um arquivo XML. Os dados preenchem alguns ou todos os campos do formulário que está sendo visualizado.

A tabela a seguir lista as opções de visualização disponíveis para diferentes tipos de formulários compatíveis:

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de ativo</strong><br /> </td>
   <td><strong>Opções de visualização disponíveis</strong><br /> </td>
  </tr>
  <tr>
   <td>Documento</td>
   <td>Visualização do PDF</td>
  </tr>
  <tr>
   <td>Formulário PDF</td>
   <td>Visualização e visualização do PDF com dados<br /> </td>
  </tr>
  <tr>
   <td>formulário adaptável</td>
   <td>Visualização de HTML e visualização de HTML com dados</td>
  </tr>
  <tr>
   <td>Modelo de formulário</td>
   <td>Visualização de PDF, visualização de PDF com dados, visualização de HTML, visualização de HTML com dados<br /> </td>
  </tr>
 </tbody>
</table>

## Pré-visualização de um formulário {#previewing-a-form-1}

1. Selecione um ativo que deseja visualizar e clique em Visualizar ![aem6forms_preview](assets/aem6forms_preview.png) na barra de ferramentas ações.

   >[!NOTE]
   >
   >Para selecionar um ativo, alterne para a Exibição de lista na Exibição de cartão padrão. Clique em ![aem6forms_viewlist](assets/aem6forms_viewlist.png) ou ![aem6forms_viewcard](assets/aem6forms_viewcard.png) para alternar visualizações.

1. Clicar em Visualizar lista as possíveis opções de visualização aplicáveis ao Tipo de ativo selecionado. Clique na opção desejada para renderizar o ativo selecionado em uma nova guia.

   As opções são:

   * Visualizar como HTML
   * Exibir com dados
   * Visualizar como PDF (disponível para modelos de formulário)

## Exibir com dados {#preview-with-data}

Ao selecionar **Visualizar com dados**, é possível ver a aparência do formulário com os dados reais inseridos. A opção Preview with Data permite fazer upload de um XML que contém dados de usuário de amostra. Os dados do usuário de exemplo são usados para preencher o formulário de visualização no formato escolhido.

1. Selecione um ativo e clique em Visualizar ![aem6forms_preview](assets/aem6forms_preview.png)e selecione **Visualizar com dados**.
1. Na caixa de diálogo Visualizar formulário, forneça FormData como um arquivo XML. Clique em Visualizar para renderizar o formulário com os dados mesclados do XML.
