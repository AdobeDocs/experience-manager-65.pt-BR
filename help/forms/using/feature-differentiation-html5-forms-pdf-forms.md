---
title: Diferenciação de recursos entre formulários HTML5 e PDF forms
seo-title: Feature differentiation between HTML5 forms and PDF forms
description: Recurso suportado em HTML5 forms e PDF forms
seo-description: Feature supported in HTML5 forms and PDF forms
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
feature: Mobile Forms
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 3%

---

# Diferenciação de recursos entre formulários HTML5 e PDF forms {#feature-differentiation-between-html-forms-and-pdf-forms}

A tabela a seguir especifica o suporte de recursos fornecido para formulários HTML5 e PDF forms:

<table>
 <tbody>
  <tr>
   <th>Recurso</th>
   <th>Formulários HTML5</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>Códigos de barras<br /> </td>
   <td>Não disponível no nível da interface do usuário. </td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Campo de assinatura<br /> </td>
   <td><strong>Assinaturas digitais</strong> não são compatíveis, mas um novo <strong>Assinatura do Scribble</strong> é adicionado para assinaturas do tipo papel. É possível assinar o formulário usando a <strong>Assinatura do Scribble</strong> campo. A assinatura é salva no formulário como uma imagem. Você pode salvar informações de localização geográfica na variável <strong>Assinatura do Scribble</strong> campo.</td>
   <td>Campo de assinatura disponível para <strong>Assinaturas digitais</strong>.</td>
  </tr>
  <tr>
   <td>Mesclagem de dados</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Imagens</td>
   <td>O esquema de URI de dados é usado para exibir imagens. Todas as versões modernas dos navegadores suportam esse esquema, mas há diferenças no intervalo de formatos de imagem suportados por cada navegador.<br /> </td>
   <td>Os formatos .gif, .png, .jpeg, .bmp e .tiff são compatíveis.</td>
  </tr>
  <tr>
   <td>Paginação<br /> </td>
   <td><p>Um formulário HTML5 é dividido em painéis e caixas para dar a ele uma aparência semelhante a PDF forms. O tamanho da página é calculado dinamicamente. Se todo o conteúdo de uma página em um formulário HTML5 for excluído ou marcado como oculto, a página em branco ficará oculta e um espaço vazio (espaço em branco) não será exibido entre as páginas acima e abaixo da página em branco.</p> <p>Se os scripts ou união de dados adicionarem conteúdo a uma página, o comprimento da página será expandido para acomodar o conteúdo recém-adicionado. Nenhuma nova página é adicionada ao formulário para acomodar o conteúdo recém-adicionado. </p> <p><strong>Observação:</strong> Quando todo o conteúdo de uma página em um formulário HTML5 é excluído ou marcado como oculto, a página em branco (espaço em branco) permanece visível entre a primeira e a segunda página, mas não entre quaisquer outras páginas.</p> </td>
   <td>A paginação no PDF depende do conteúdo de dados mesclado ou do conteúdo do usuário e a contagem de páginas é aumentada/reduzida com base nela.</td>
  </tr>
  <tr>
   <td>Cabeçalhos/Rodapés </td>
   <td>Compatível. <br /> <br /> Como os formulários móveis do HTML5 não são compatíveis com quebras de página, os cabeçalhos e rodapés são exibidos apenas uma vez. No entanto, é possível configurá-los no layout para serem exibidos em vários lugares na visualização de formulários móveis.<br /> </td>
   <td>Compatível.</td>
  </tr>
  <tr>
   <td>Widgets personalizados</td>
   <td>É possível personalizar widgets para aprimorar a experiência do usuário em dispositivos móveis.<br /> </td>
   <td>Todos os widgets estão bloqueados e nenhum widget personalizado pode ser conectado.<br /> </td>
  </tr>
  <tr>
   <td>API de script XFA</td>
   <td>Suporta as construções de script XFA mais usadas. Para obter a lista de detalhes de construções compatíveis, consulte <a href="/help/forms/using/scripting-support.md">suporte a scripts</a>.</td>
   <td>Suporta todas as construções de script XFA.</td>
  </tr>
  <tr>
   <td>APIs de script Acrobat </td>
   <td>Os formulários HTML5 são compatíveis com as APIs mais usadas. Para obter detalhes, consulte <a href="/help/forms/using/scripting-support.md">suporte a scripts</a>.</td>
   <td>Se o arquivo PDF for aberto no Acrobat ou Reader, ele também oferecerá suporte a todas as APIs de script fornecidas pelo Acrobat.</td>
  </tr>
  <tr>
   <td>Suporte para idiomas da direita para a esquerda </td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
