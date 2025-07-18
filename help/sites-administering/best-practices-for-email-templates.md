---
title: Práticas recomendadas para modelos de email
description: Encontre práticas recomendadas para a criação de modelos de email no AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
docset: aem65
exl-id: 6666eddc-dc17-4bd4-9d55-e6522f40a680
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
index: false
source-git-commit: 389d5fa8de320a7237fc8290992a33743b15db99
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 0%

---


# Práticas recomendadas para modelos de email {#best-practices-for-email-templates}

>[!CAUTION]
>
>Este artigo se aplica aos componentes de email obsoletos do Foundation com base nos componentes de email do AEM.
>
>Os usuários são incentivados a usar os [Componentes principais de email.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html?lang=pt-BR)

Este documento descreve algumas das práticas recomendadas para design de email, resultando em um modelo de campanha de email bem desenvolvido.

A campanha de demonstração disponível no AEM segue todas essas práticas recomendadas. A forma como as práticas recomendadas são implementadas na campanha de demonstração é descrita para cada prática recomendada.

Use essas práticas recomendadas ao criar seu próprio informativo.

>[!NOTE]
>
>Todo o conteúdo da campanha deve ser criado em uma página `master` do tipo `cq/personalization/components/ambitpage`.
>
>Por exemplo, se a estrutura da campanha planejada for algo como
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>Verifique se ele reside em uma página `master`
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Ao criar um modelo de email para o Adobe Campaign, você deve incluir a propriedade **acMapping** com o valor **mapRecipient** no nó **jcr:content** do modelo. Caso contrário, você não poderá selecionar o modelo Adobe Campaign em **Propriedades da página** do Experience Manager (o campo está desabilitado).

## Componente de modelo/página {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>Prática recomendada</strong></td>
   <td><strong>Implementação</strong></td>
  </tr>
  <tr>
   <td><p>Especifique o tipo de documento para garantir uma renderização consistente.</p> <p>Adicionar DOCTYPE no início (HTML ou XHTML)</p> </td>
   <td><p>É configurável por design alterando a propriedade <i>cq:doctype</i> em<i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i></p> <p>O padrão é "XHTML":</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional/EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>Pode ser alterado para "HTML_5":</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Especifique a definição de caractere para garantir a renderização correta de caracteres especiais.</p> <p>Adicione a declaração CHARSET (por exemplo, iso-8859-15, UTF-8) a &lt;head&gt;</p> </td>
   <td><p>Está definido como UTF-8.</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Codifique toda a estrutura usando o elemento &lt;table&gt;element. Para layouts mais complicados, você deve aninhar tabelas para criar estruturas complexas.</p> <p>O email deve ficar bom mesmo sem o css.</p> </td>
   <td><p>As tabelas são usadas em todo o modelo para estruturar conteúdo. Atualmente usando um máximo de quatro tabelas aninhadas (1 tabela base + máx. 3 níveis de aninhamento)</p> <p>As tags &lt;div&gt; são usadas apenas no modo de autor para garantir a edição adequada de componentes.</p> </td>
  </tr>
  <tr>
   <td>Use atributos de elemento (como preenchimento de célula, valência e largura) para definir dimensões de tabela. Esse método força uma estrutura de modelo de caixa.</td>
   <td><p>Todas as tabelas contêm atributos necessários como <i>borda</i>, <i>preenchimento de célula</i>, <i>espaçamento de célula</i> e <i>largura</i>.</p> <p>Para harmonizar o posicionamento de elementos dentro de tabelas, todas as células da tabela têm o atributo <i>valign="top"</i> sendo definido.</p> </td>
  </tr>
  <tr>
   <td><p>Conte com facilidade de locomoção, se possível. Use consultas de mídia para aumentar o tamanho do texto em telas pequenas e fornecer áreas de ocorrência no tamanho de miniatura para links.</p> <p>Tornar um email responsivo se o design permitir.</p> </td>
   <td>Na medida em que os estilos CSS estão sendo usados para ilustrar o design de demonstração, as consultas de mídia estão sendo usadas para oferecer uma versão móvel amigável.</td>
  </tr>
  <tr>
   <td>O CSS em linha é melhor do que colocar todo o CSS no início.</td>
   <td><p>Para demonstrar melhor a estrutura subjacente do HTML e facilitar a possibilidade de personalizar a estrutura do informativo, somente algumas definições de CSS foram incorporadas.</p> <p>Os estilos base e as variações de modelo foram extraídos para um bloco de estilos no &lt;head&gt; da página. No envio final do informativo, essas definições de CSS são incorporadas ao HTML. Um mecanismo integrado automático está planejado, mas não está disponível no momento.</p> </td>
  </tr>
  <tr>
   <td>Mantenha seu CSS simples. Evite declarações de estilo composto, código abreviado, propriedades de layout CSS, seletores complexos e pseudoelementos.</td>
   <td>Na medida em que os estilos CSS estão sendo usados para ilustrar o design de demonstração, as recomendações de CSS estão sendo seguidas.</td>
  </tr>
  <tr>
   <td>Os emails devem ter no máximo 600-800 pixels de largura. Esse dimensionamento faz com que eles se comportem melhor dentro do tamanho do painel de visualização fornecido por muitos clientes.</td>
   <td>A <i>largura</i> da tabela de conteúdo é limitada a 600 pixels no design de demonstração.</td>
  </tr>
 </tbody>
</table>

### Imagens {#images}

/libs/mcm/campaign/components/image

| **Prática recomendada** | **Implementação** |
|---|---|
| Adicionar atributos de *alt* a imagens | O atributo *alt* foi definido como obrigatório para o componente de imagem. |
| Use o formato *jpg* em vez do *png* para imagens | As imagens são sempre servidas como JPG pelo componente de imagem. |
| Usar elemento `<img>` em vez de imagens de plano de fundo em uma tabela. | Nenhum dado de imagem de fundo é usado nos modelos. |
| Adicione o atributo style=&quot;display block&quot; nas imagens. Isso permite que eles sejam bem exibidos no Gmail. | Todas as imagens contêm por padrão o atributo *style=&quot;display block&quot;*. |

### Texto e links {#text-and-links}

/libs/mcm/campaign/components/header, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>Prática recomendada</strong></td>
   <td><strong>Implementação</strong></td>
  </tr>
  <tr>
   <td>Use html &lt;font&gt; em vez de style no CSS (font-family)</td>
   <td>O RichTextEditor (por exemplo, no componente de imagem de texto) agora é compatível com a escolha e a aplicação de famílias de fontes e tamanhos de fontes a textos selecionados. Eles são renderizados como tags &lt;font&gt;.</td>
  </tr>
  <tr>
   <td>Use fontes básicas em várias plataformas, como <i>Arial®, Verdana, Georgia</i> e <i>Times New Roman®</i>.</td>
   <td><p>Depende do design do informativo.</p> <p>Para o design da demonstração, a fonte "Helvetica®" é usada, mas retorna para uma fonte sans-serif genérica, se não estiver presente.</p> </td>
  </tr>
 </tbody>
</table>

### Genérico {#generic}

| **Prática recomendada** | **Implementação** |
|---|---|
| Use o validador W3C para corrigir o código HTML. Certifique-se de que todas as tags abertas estejam fechadas corretamente. | Código validado. Somente para Doctype de transição XHTML, o atributo xmlns ausente para o elemento `<html>` está ausente. |
| Evite usar JavaScript ou Flash - essas tecnologias geralmente não são compatíveis com clientes de email. | O JavaScript ou Flash não é usado no modelo de boletim informativo. |
| Adicione uma versão de texto sem formatação para envio de várias partes. | Um novo widget foi incorporado às propriedades da página para extrair facilmente uma versão de texto simples do conteúdo da página. Você pode usá-lo como ponto de partida para a versão final do texto sem formatação. |

## Modelos e exemplos do informativo da campanha {#campaign-newsletter-templates-and-examples}

O AEM vem com vários modelos e componentes prontos para uso para você criar informativos da campanha. Você pode usar esses modelos e componentes para criar informativos personalizados.

### Modelos {#templates}

Para oferecer uma base sólida e ampliar a variedade de possibilidades de fluxo de conteúdo, há três tipos de modelo ligeiramente diferentes disponíveis prontos para uso. Você pode usar facilmente esses três tipos para criar um informativo personalizado.

Todos têm uma seção **cabeçalho**, um **rodapé** e uma seção **corpo**. Abaixo da seção do corpo, cada modelo difere no **design de coluna** (uma, duas ou três colunas).

![Variantes de informativos possíveis](assets/chlimage_1-69.png)

### Componentes {#components}

Atualmente, há [sete componentes disponíveis para uso nos modelos de campanha](/help/sites-authoring/adobe-campaign-components.md). Todos esses componentes são baseados na linguagem de marcação do Adobe **HTL**.

| **Nome do componente** | **Caminho do componente** |
|---|---|
| Cabeçalho | /libs/mcm/campaign/components/header |
| Imagem | /libs/mcm/campaign/components/image |
| Text&amp;Personalization | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| Link | /libs/mcm/campaign/components/reference |
| Modelo de imagem do Dynamic Media Classic (antigo Scene7) | /libs/mcm/campaign/s7image |
| Referência direcionada | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>Esses componentes são otimizados para o conteúdo de e-mail; ou seja, seguem as práticas recomendadas descritas neste documento. O uso de outros componentes prontos para uso geralmente viola essas regras.

Estes componentes são descritos em detalhes em [Adobe Campaign components](/help/sites-authoring/adobe-campaign-components.md).
