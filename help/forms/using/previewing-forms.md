---
title: Visualização de um formulário
seo-title: Visualização de um formulário
description: Você pode pré-visualização seus formulários antes de publicá-los ou ativá-los para garantir que eles atendam às expectativas. As opções de pré-visualização podem variar entre os tipos de formulário suportados.
seo-description: Você pode pré-visualização seus formulários antes de publicá-los ou ativá-los para garantir que eles atendam às expectativas. As opções de pré-visualização podem variar entre os tipos de formulário suportados.
uuid: 9ec359ea-f518-441c-9c3d-e3c1ea07a532
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 2%

---


# Pré-visualização de um formulário {#previewing-a-form}

## Visão geral {#overview}

No AEM Forms, é possível pré-visualização os formulários e documentos presentes no repositório. A pré-visualização ajuda a saber exatamente como os formulários são exibidos e se comportam quando são liberados para os usuários finais.

Ao visualizar formulários, eles são renderizados na interface interativa e o usuário pode preencher os formulários com dados. Ao visualizar documentos, eles são renderizados no modo não interativo e o usuário só pode visualização o documento. Para formulários, uma opção adicional de Pré-visualização personalizada está disponível. Usando essa opção, é possível pré-visualização o formulário usando dados de um arquivo XML. Os dados preenchem alguns ou todos os campos do formulário que está sendo visualizado.

A tabela a seguir lista as opções de pré-visualização disponíveis para diferentes tipos de formulários suportados:

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de ativo</strong><br /> </td>
   <td><strong>Opções de pré-visualização disponíveis</strong><br /> </td>
  </tr>
  <tr>
   <td>Documento</td>
   <td>PRÉ-VISUALIZAÇÃO PDF</td>
  </tr>
  <tr>
   <td>Formulário PDF</td>
   <td>PRÉ-VISUALIZAÇÃO e Pré-visualização de PDF com Dados<br /> </td>
  </tr>
  <tr>
   <td>forma adaptativa</td>
   <td>PRÉ-VISUALIZAÇÃO HTML e pré-visualização HTML com dados</td>
  </tr>
  <tr>
   <td>Modelo de formulário</td>
   <td>PRÉ-VISUALIZAÇÃO PDF, pré-visualização PDF com dados, pré-visualização HTML, pré-visualização HTML com dados<br /> </td>
  </tr>
 </tbody>
</table>

## Pré-visualização de um formulário {#previewing-a-form-1}

1. Selecione um ativo que deseja pré-visualização e clique em Pré-visualização ![aem6forms_pré-visualização](assets/aem6forms_preview.png) na barra de ferramentas de ações.

   >[!NOTE]
   >
   >Para selecionar um ativo, alterne para visualização de Lista na visualização de cartão padrão. Clique em ![aem6forms_viewlist](assets/aem6forms_viewlist.png) ou ![aem6forms_viewcard](assets/aem6forms_viewcard.png) para alternar entre o visualização.

1. Clicar em Pré-visualização lista as possíveis opções de pré-visualização aplicáveis ao Tipo de ativo selecionado. Clique na opção desejada para renderizar o ativo selecionado em uma nova guia.

   Suas opções são:

   * Pré-visualização como HTML
   * Exibir com dados
   * Pré-visualização como PDF (disponível para modelos de formulário)

## Exibir com dados {#preview-with-data}

Quando você seleciona **Pré-visualização com Dados**, pode ver a aparência do formulário com os dados reais inseridos nele. A opção pré-visualização com dados permite carregar um XML que contém dados de amostra do usuário. A amostra de dados do usuário é usada para preencher o formulário de pré-visualização no formato escolhido.

1. Selecione um ativo, clique em Pré-visualização ![aem6forms_pré-visualização](assets/aem6forms_preview.png) e selecione **Pré-visualização com Dados**.
1. Na caixa de diálogo Formulário de Pré-visualização, forneça FormData como um arquivo XML. Clique em Pré-visualização para renderizar o formulário com os dados unidos do XML.

