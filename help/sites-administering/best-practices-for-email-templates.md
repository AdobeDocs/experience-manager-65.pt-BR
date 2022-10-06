---
title: Práticas recomendadas para modelos de email
seo-title: Best Practices for Email Templates
description: Encontre as práticas recomendadas para criar modelos de email no AEM.
seo-description: Find best practices on creating email templates in AEM.
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
exl-id: 6666eddc-dc17-4bd4-9d55-e6522f40a680
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 1%

---

# Práticas recomendadas para modelos de email {#best-practices-for-email-templates}

>[!CAUTION]
>
>Os componentes de email AEM foram descontinuados. Devido à natureza do email, que mescla conteúdo e estilo, os componentes de email fornecidos prontos para uso pelo AEM se tornam de reutilização limitada para clientes devido à necessidade de implementar estilos personalizados em quaisquer componentes necessários para os projetos.
>
>Os componentes de email podem ser implementados no nível do projeto, e os componentes de email AEM obsoletos ilustram como isso pode ser feito. No entanto, esses componentes obsoletos não devem ser usados em projetos.

Este documento descreve algumas das práticas recomendadas em relação ao design de email, resultando em um template de campanha de email bem desenvolvido.

A campanha de demonstração disponível no AEM segue todas essas práticas recomendadas. Como as práticas recomendadas são implementadas na campanha de demonstração é descrito para cada prática recomendada.

Use essas práticas recomendadas ao criar seu próprio boletim informativo.

>[!NOTE]
>
>Todo o conteúdo da campanha deve ser criado em um `master` página do tipo `cq/personalization/components/ambitpage`.
>
>Por exemplo, se a estrutura de campanha planejada é algo como
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>Você deve certificar-se de que ele esteja sob uma `master` página
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Ao criar um template de email para o Adobe Campaign, você deve incluir a propriedade **acMapping** com o valor **mapRecipient** no **jcr:content** do modelo, ou você não poderá selecionar o modelo do Adobe Campaign em **Propriedades da página** de AEM (o campo está desativado).

## Componente Modelo/página {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>Prática recomendada</strong></td>
   <td><strong>Implementação</strong></td>
  </tr>
  <tr>
   <td><p>Especifique o tipo de documento para garantir uma renderização consistente.</p> <p>Adicione DOCTYPE no início (HTML ou XHTML)</p> </td>
   <td><p>É configurável por design alterando a variável <i>cq:doctype</i> propriedade em<i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i></p> <p>O padrão é "XHTML":</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>Pode ser alterado para "HTML_5":</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Especifique a definição de caractere para garantir a renderização correta de caracteres especiais.</p> <p>Adicionar declaração CHARSET (por exemplo, iso-8859-15, UTF-8) a &lt;head&gt;</p> </td>
   <td><p>Está definido como UTF-8.</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Codifique toda a estrutura usando o &lt;table&gt;elemento. Para layouts mais complicados, você deve aninhar tabelas para criar estruturas complexas.</p> <p>O email deve ficar bom mesmo sem css.</p> </td>
   <td><p>Tabelas são usadas em todo o modelo para estruturar conteúdo. Atualmente usando no máximo quatro tabelas aninhadas (1 tabela base + máx. 3 níveis de aninhamento)</p> <p>&lt;div&gt; tags são usadas somente no modo de criação para garantir a edição adequada do componente.</p> </td>
  </tr>
  <tr>
   <td>Use atributos de elemento (como preenchimento de celular, valência e largura) para definir dimensões de tabela. Isso força uma estrutura de modelo de caixa.</td>
   <td><p>Todas as tabelas contêm atributos necessários, como <i>border</i>, <i>alvéolo</i>, <i>espaçamento entre células</i> e <i>largura</i>.</p> <p>Para harmonizar o posicionamento de elementos dentro de tabelas, todas as células da tabela têm o atributo <i>valign="top"</i> sendo definido.</p> </td>
  </tr>
  <tr>
   <td><p>Se possível, considere a acessibilidade dos dispositivos móveis. Use consultas de mídia para aumentar os tamanhos do texto em telas pequenas e fornecer áreas de ocorrência de tamanho em miniatura para links.</p> <p>Torne um email responsivo se o design permitir.</p> </td>
   <td>No que diz respeito aos estilos de CSS usados para ilustrar o design da demonstração, as consultas de mídia estão sendo usadas para oferecer uma versão compatível com dispositivos móveis.</td>
  </tr>
  <tr>
   <td>O CSS em linha é melhor do que colocar todo o CSS no início.</td>
   <td><p>Para demonstrar melhor a estrutura de HTML subjacente e facilitar a possibilidade de personalizar a estrutura do boletim informativo, apenas algumas definições de CSS foram incorporadas.</p> <p>Os estilos básicos e as variações do modelo foram extraídos para um bloco de estilos no &lt;head&gt; da página. No envio final do boletim informativo, essas definições de CSS devem ser incluídas no HTML. Prevê-se um mecanismo automático de interligação, mas atualmente não está disponível.</p> </td>
  </tr>
  <tr>
   <td>Mantenha seu CSS simples. Evite declarações de estilo composto, código abreviado, propriedades de layout CSS, seletores complexos e pseudo-elementos.</td>
   <td>No que diz respeito aos estilos de CSS usados para ilustrar o design da demonstração, as recomendações de CSS estão sendo seguidas.</td>
  </tr>
  <tr>
   <td>Os emails devem ter de 600 a 800 pixels de largura máxima. Isso fará com que se comportem melhor dentro do tamanho do painel de visualização fornecido por muitos clientes.</td>
   <td>O <i>largura</i> da tabela de conteúdo é limitada a 600px no design de demonstração.</td>
  </tr>
 </tbody>
</table>

### Imagens {#images}

/libs/mcm/campaign/components/image

| **Prática recomendada** | **Implementação** |
|---|---|
| Adicionar *alt* atributos para imagens | O *alt* foi definido como obrigatório para o componente de imagem. |
| Use *jpg* em vez de *png* formato para imagens | As imagens sempre serão exibidas como JPG pelo componente de imagem. |
| Use `<img>` em vez de imagens de plano de fundo em uma tabela. | Nenhum dado de imagem de plano de fundo é usado nos modelos. |
| Adicione o atributo style=&quot;display block&quot; nas imagens. Permite exibir bem no Gmail. | Todas as imagens contêm, por padrão, a variável *style=&quot;display block&quot;* atributo. |

### Texto e links {#text-and-links}

/libs/mcm/campaign/components/header, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>Prática recomendada</strong></td>
   <td><strong>Implementação</strong></td>
  </tr>
  <tr>
   <td>Use html em vez de estilo em CSS (família de fontes)</td>
   <td>O RichTextEditor (por exemplo, no componente textimage) agora é compatível com a escolha e aplicação de famílias de fontes e tamanhos de fonte a textos selecionados. Eles serão renderizados como tags.</td>
  </tr>
  <tr>
   <td>Use fontes básicas e em várias plataformas, como <i>Arial, Verdana, Geórgia</i> e <i>Times New Roman</i>.</td>
   <td><p>Depende do design do boletim informativo.</p> <p>Para o design da demonstração, a fonte "Helvetica" é usada, mas voltará para a fonte sans-serif genérica, se não estiver presente.</p> </td>
  </tr>
 </tbody>
</table>

### Genérico {#generic}

| **Prática recomendada** | **Implementação** |
|---|---|
| Use o validador W3C para corrigir o código HTML. Certifique-se de que todas as tags abertas estejam fechadas corretamente. | O código foi validado. Para o XHTML transition Doctype somente o atributo xmlns ausente para o `<html>` elemento ausente. |
| Não se incomode com JavaScript ou Flash - essas tecnologias não são amplamente suportadas pelos clientes de email. | Nem o JavaScript nem o Flash são usados no modelo do informativo. |
| Adicione uma versão de texto simples para envio de várias partes. | Um novo widget foi criado nas propriedades da página para extrair facilmente uma versão de texto simples do conteúdo da página. Isso pode ser usado como ponto de partida para a versão final de texto simples. |

## Templates e exemplos de informativo do Campaign {#campaign-newsletter-templates-and-examples}

AEM vem com vários modelos e componentes prontos para você criar boletins informativos do Campaign. Você pode usar esses modelos e componentes para criar seus boletins informativos personalizados.

### Modelos {#templates}

Para oferecer uma base sólida e ampliar a variedade de possibilidades de fluxo de conteúdo, há três tipos de modelo ligeiramente diferentes disponíveis imediatamente. Você pode usá-los facilmente para criar um informativo personalizado.

Todos têm um **header**, a **rodapé** e **corpo** seção. Abaixo da seção de corpo, cada modelo difere em **design de coluna** (1, 2 ou 3 colunas).

![](assets/chlimage_1-69.png)

### Componentes {#components}

Atualmente, existem [sete componentes disponíveis para uso dentro de templates de campanha](/help/sites-authoring/adobe-campaign-components.md). Esses componentes são todos baseados na linguagem de marcação Adobe **HTL**.

| **Nome do componente** | **Caminho do componente** |
|---|---|
| Cabeçalho | /libs/mcm/campaign/components/header |
| Imagem | /libs/mcm/campaign/components/image |
| Texto e personalização | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| Link | /libs/mcm/campaign/components/reference |
| Modelo de imagem do Dynamic Media Classic (antigo Scene7) | /libs/mcm/campaign/s7image |
| Referência direcionada | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>Esses componentes são otimizados para conteúdo de email; ou seja, seguem as práticas recomendadas descritas neste documento. O uso de outros componentes prontos para uso geralmente viola essas regras.

Esses componentes são descritos detalhadamente em [Componentes do Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md).
