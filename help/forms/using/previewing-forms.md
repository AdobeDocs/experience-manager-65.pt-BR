---
title: Visualização de um formulário
seo-title: Previewing a form
description: Você pode visualizar seus formulários antes de publicá-los ou ativá-los para garantir que eles atendam às expectativas. As opções de visualização podem variar entre os tipos de formulário compatíveis.
seo-description: You can preview your forms before publishing or activating to ensure it meets the expectations. Preview options may vary across the supported form types.
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
feature: Adaptive Forms
exl-id: aed5703e-4fe6-4839-9657-c660ac48521e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---

# Visualização de um formulário {#previewing-a-form}

## Visão geral {#overview}

No AEM Forms, é possível visualizar os formulários e documentos presentes no repositório. A Visualização ajuda a saber exatamente como os formulários são exibidos e se comportam quando são liberados para os usuários finais.

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
   <td>Visualização do HTML e visualização do HTML com dados</td>
  </tr>
  <tr>
   <td>Modelo de formulário</td>
   <td>Visualização do PDF, visualização do PDF com Dados, visualização do HTML, visualização do HTML com Dados<br /> </td>
  </tr>
 </tbody>
</table>

## Visualização de um formulário {#previewing-a-form-1}

1. Selecione um ativo que deseja visualizar e clique em Visualizar ![aem6forms_preview](assets/aem6forms_preview.png) na barra de ferramentas de ações.

   >[!NOTE]
   >
   >Para selecionar um ativo, alterne para a exibição Lista na exibição Cartão padrão. Clique em ![aem6forms_viewlist](assets/aem6forms_viewlist.png) ou ![aem6forms_viewcard](assets/aem6forms_viewcard.png) para alternar visualizações.

1. Clicar em Visualizar lista as opções de visualização possíveis aplicáveis ao Tipo de ativo selecionado. Clique na opção desejada para renderizar o ativo selecionado em uma nova guia.

   Suas opções são:

   * Visualizar como HTML
   * Exibir com dados
   * Visualizar como PDF (disponível para modelos de formulário)

## Exibir com dados {#preview-with-data}

Ao selecionar **Visualizar com dados**, é possível ver a aparência do formulário com os dados reais inseridos. A opção Visualizar com dados permite carregar um XML que contém dados de exemplo do usuário. A amostra de dados do usuário é usada para preencher o formulário de visualização no formato escolhido.

1. Selecione um ativo, clique em Visualizar ![aem6forms_preview](assets/aem6forms_preview.png)e selecione **Visualizar com dados**.
1. Na caixa de diálogo Visualizar formulário, forneça FormData como um arquivo XML. Clique em Preview para renderizar o formulário com os dados unidos do XML.
