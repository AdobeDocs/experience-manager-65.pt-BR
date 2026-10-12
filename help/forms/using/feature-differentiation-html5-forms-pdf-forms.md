---
title: Diferenciação de recursos entre o HTML5 Forms e o PDF forms
description: Saiba mais sobre as diferenças de recursos entre o HTML5 Forms e o PDF forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 2%
---
# Diferenciação de recursos entre o HTML5 Forms e o PDF forms {#feature-differentiation-between-html-forms-and-pdf-forms}

A tabela a seguir especifica o suporte ao recurso fornecido para o HTML5 Forms e o PDF forms:

<table>
 <tbody>
  <tr>
   <th>Destaque</th>
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
   <td>Não há suporte para <strong>Assinaturas Digitais</strong>, mas um novo campo <strong>Assinatura Escrita</strong> foi adicionado para assinaturas tipo papel. É possível criar assinatura com script no formulário usando o campo <strong>Assinatura com Rabisco</strong>. A assinatura é salva no formulário como uma imagem. Você pode salvar informações de localização geográfica no campo <strong>Assinatura Escrita</strong>.</td>
   <td>Campo de assinatura disponível para <strong>Assinaturas digitais</strong>.</td>
  </tr>
  <tr>
   <td>Mesclagem de dados</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Imagens</td>
   <td>O esquema do URI de dados é usado para exibir imagens. Todas as versões modernas dos navegadores oferecem suporte a esse esquema, mas há diferenças no intervalo de formatos de imagem que cada navegador aceita.<br /> </td>
   <td>Os formatos .gif, .png, .jpeg, .bmp e .tiff são suportados.</td>
  </tr>
  <tr>
   <td>Paginação<br /> </td>
   <td><p>Um formulário HTML5 é dividido em painéis e caixas para dar a ele uma aparência semelhante ao PDF forms. O tamanho da página é calculado dinamicamente. Se todo o conteúdo de uma página em um formulário HTML5 for excluído ou marcado como oculto, a página em branco ficará oculta. Um espaço vazio (espaço em branco) não é exibido entre as páginas acima e abaixo da página em branco.</p> <p>Se a mesclagem de dados ou os scripts adicionarem conteúdo a uma página, o comprimento da página se expandirá para acomodar o conteúdo recém-adicionado. Nenhuma página nova é adicionada ao formulário para acomodar o conteúdo recém-adicionado. </p> <p><strong>Observação:</strong> quando todos os conteúdos de uma página em um formulário HTML5 são excluídos ou marcados como ocultos, a página em branco (espaço em branco) permanece visível entre a primeira e a segunda página, mas não entre as outras páginas.</p> </td>
   <td>A paginação no PDF depende do conteúdo de dados mesclado ou do conteúdo do usuário e a contagem de páginas é aumentada/reduzida com base nela.</td>
  </tr>
  <tr>
   <td>Cabeçalhos/Rodapés </td>
   <td>Compatível. <br /> <br /> Como os formulários móveis HTML5 não são compatíveis com quebras de página, os cabeçalhos e rodapés são exibidos apenas uma vez. No entanto, você pode configurá-los no layout para serem exibidos em vários locais na visualização de formulários para dispositivos móveis.<br /> </td>
   <td>Compatível.</td>
  </tr>
  <tr>
   <td>Widgets personalizados</td>
   <td>É possível personalizar widgets para aprimorar a experiência do usuário em dispositivos móveis.<br /> </td>
   <td>Todos os widgets estão bloqueados e nenhum widget personalizado pode ser conectado.<br /> </td>
  </tr>
  <tr>
   <td>API de script XFA</td>
   <td>Oferece suporte às construções de script XFA mais usadas. Para obter uma lista detalhada das construções compatíveis, consulte <a href="/help/forms/using/scripting-support.md">suporte a script</a>.</td>
   <td>Suporta todas as construções de script XFA.</td>
  </tr>
  <tr>
   <td>APIs de script do Acrobat </td>
   <td>Os formulários HTML5 são compatíveis com as APIs mais usadas. Para obter detalhes, consulte <a href="/help/forms/using/scripting-support.md">suporte a scripts</a>.</td>
   <td>Se o arquivo do PDF for aberto no Acrobat ou no Reader, ele também oferecerá suporte a todas as APIs de script fornecidas pelo Acrobat.</td>
  </tr>
  <tr>
   <td>Suporte para idiomas da direita para a esquerda </td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
