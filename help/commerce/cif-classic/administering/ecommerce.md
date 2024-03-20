---
title: Estrutura de integração de comércio eletrônico
description: O eCommerce AEM ajuda os profissionais de marketing a fornecer experiências de compras personalizadas e de marca em pontos de contato da Web, de dispositivos móveis e sociais.
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: d995f0d6-9e48-4228-ac82-f33a0b25b9d3
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 2%

---

# eCommerce{#ecommerce}

* [Conceitos ](/help/commerce/cif-classic/administering/concepts.md)
* [Administração (genérico)](/help/commerce/cif-classic/administering/generic.md)

O Adobe fornece duas versões do Commerce integration framework:

<table>
 <tbody>
  <tr>
   <th><p> </p> </th>
   <th><p>CIF no local</p> </th>
   <th><p>CIF Cloud</p> </th>
  </tr>
  <tr>
   <td><p>Versões compatíveis do AEM</p> </td>
   <td><p>AEM no local ou AMS 6.x</p> </td>
   <td>AEM AMS 6.4 e 6.5</td>
  </tr>
  <tr>
   <td><p>Back-end</p> </td>
   <td>
    <ul>
     <li>AEM, Java</li>
     <li>Integração monolítica, mapeamento pré-compilação (modelo)</li>
     <li>Repositório JCR</li>
    </ul> </td>
   <td>
    <ul>
     <li>Adobe Commerce</li>
     <li>Java e JavaScript</li>
     <li>Nenhum dado comercial armazenado no repositório JCR</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Front-end</p> </td>
   <td><p>Páginas renderizadas do lado do servidor do AEM</p> </td>
   <td>Aplicativo de página mista (renderização híbrida)</td>
  </tr>
  <tr>
   <td><p>Catálogo de produtos</p> </td>
   <td>
    <ul>
     <li>Importador de produtos, editor e armazenamento em cache no AEM</li>
     <li>Catálogos regulares com páginas de AEM ou proxy</li>
    </ul> </td>
   <td>
    <ul>
     <li>Nenhuma importação de produto</li>
     <li>Modelos genéricos</li>
     <li>Dados sob demanda por meio do conector</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Escalabilidade</p> </td>
   <td>
    <ul>
     <li>Pode oferecer suporte a até alguns milhões de produtos (depende do caso de uso)</li>
     <li>Armazenamento em cache no Dispatcher</li>
    </ul> </td>
   <td>
    <ul>
     <li>Sem limitação de volume</li>
     <li>Armazenamento em cache no Dispatcher ou CDN</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Modelo de dados padronizado</td>
   <td>Não</td>
   <td>Sim, esquema do Adobe Commerce GraphQL</td>
  </tr>
  <tr>
   <td>Disponibilidade</td>
   <td><p>Sim. SAP Commerce Cloud (Extensão atualizada para oferecer suporte a AEM 6.4 e Hybris 5 (padrão) e mantém compatibilidade com o Hybris 4</p> <p>Commerce Cloud do Salesforce (conector de código aberto para suporte ao AEM 6.4)</p> </td>
   <td>Sim, via código aberto via GitHub. Adobe Commerce (Suporta 2.3.2 (padrão) e compatível com 2.3.1).</td>
  </tr>
  <tr>
   <td>Quando usar</td>
   <td>Casos de uso limitados: por exemplo, cenários em que catálogos pequenos e estáticos podem precisar ser importados</td>
   <td>Solução preferida na maioria dos casos de uso</td>
  </tr>
 </tbody>
</table>

O comércio eletrônico, juntamente com o Gerenciamento de informações de produtos (PIM), lida com as atividades de um site focado na venda de produtos por meio de uma loja online:

* Criação, vida útil e obsolescência de um produto
* Gerenciamento de preços
* Gerenciamento de transações
* Gerenciamento de catálogos inteiros
* Registros de armazenamento dinâmicos e centralizados
* Interfaces da Web

O eCommerce AEM ajuda os profissionais de marketing a fornecer experiências de compras personalizadas e de marca em pontos de contato da Web, de dispositivos móveis e sociais. O ambiente de criação do AEM permite personalizar páginas e componentes com base no contexto do visitante do público-alvo e nas estratégias de merchandising; por exemplo:

* Páginas de produto
* Componentes do carrinho de compras
* Fazer check-out dos componentes

A implementação permite acesso em tempo real às informações do produto. Isso pode ser usado para aplicar:

* Integridade das informações do produto
* Preços
* Estoque de manutenção de estoque
* Variações no estado de um carrinho de compras

>[!NOTE]
>
>Para usar a estrutura de integração com provedores externos de comércio eletrônico, primeiro é necessário instalar os pacotes necessários. Para obter mais informações, consulte [Implantação do comércio eletrônico](/help/commerce/cif-classic/deploying/ecommerce.md).
>
>Para obter informações sobre como estender os recursos de comércio eletrônico, consulte [Desenvolvimento do comércio eletrônico](/help/commerce/cif-classic/developing/ecommerce.md).

## Recursos principais {#main-features}

O eCommerce AEM oferece:

* Um certo número de **componentes de AEM prontos para uso** para ilustrar o que pode ser obtido em seu projeto:

   * Exibição do produto
   * Carrinho de compras
   * Check-out
   * Produtos visualizados recentemente
   * Vouchers
   * e outros

  ![exemplo de componentes geometrixx](/help/sites-administering/assets/chlimage_1-130.png)

  >[!NOTE]
  >
  >A estrutura de integração fornecida pelo AEM também permite a criação de componentes adicionais do AEM para recursos de comércio, independentemente do mecanismo de comércio eletrônico específico.

* **Pesquisar** - utilizando:

   * a pesquisa por AEM
   * a pesquisa do sistema de comércio eletrônico
   * uma pesquisa de terceiros
   * ou uma combinação dos mesmos.

  ![exemplo de pesquisa](/help/sites-administering/assets/chlimage_1-131.png)

* Usa a capacidade do AEM para **apresentar seu conteúdo em vários canais**, seja a janela completa do navegador ou o dispositivo móvel. Isso entrega seu conteúdo no formato necessário para seus visitantes.

  ![exemplo de visualização móvel](/help/sites-administering/assets/chlimage_1-132.png)

* A capacidade de **desenvolva sua própria implementação de integração com base no [Estrutura de comércio eletrônico AEM](#the-framework)**.

  As duas implementações disponíveis atualmente são criadas na mesma base, com base na API geral (a estrutura). A implementação de uma nova integração envolve apenas a implementação dos recursos necessários à sua integração. Os componentes de front-end podem ser usados por qualquer nova implementação, à medida que usam interfaces (portanto, são independentes da implementação).

* A possibilidade de **comércio orientado por experiência com base em dados e atividades do comprador**. Isso permite que você realize vários cenários:

   * Um exemplo pode ser fornecer reduções nos custos de envio quando o pedido total exceder um valor específico.
   * Outro pode permitir que você forneça ofertas sazonais que usam dados de perfil (por exemplo, localização). Estes podem então ser destacados, novamente dependendo de outros fatores, quando necessário.

  No exemplo abaixo, um teaser é exibido, pois o conteúdo do carrinho é inferior a US$ 75:

  ![carrinho de compras com contexto do cliente](/help/sites-administering/assets/chlimage_1-133.png)

  Isso pode ser alterado quando o conteúdo do carrinho exceder US$ 75:

  ![carrinho de compras com contexto do cliente após alteração](/help/sites-administering/assets/chlimage_1-134.png)

* E outros recursos, incluindo:

   * Conteúdo do carrinho de compras retido nas sessões
   * Histórico completo do pedido
   * Atualização do catálogo expresso

## A estrutura {#the-framework}

A variável [Conceitos](/help/commerce/cif-classic/administering/concepts.md) A seção aborda a estrutura com mais detalhes, mas a seguir há uma exibição de alto nível e alta velocidade da estrutura:

### O quê? {#what}

* A estrutura de integração fornece a API, uma variedade de componentes para ilustrar a funcionalidade e várias extensões para fornecer exemplos de métodos de conexão.
* A estrutura fornece a estrutura básica necessária para a implementação de um projeto.
* A estrutura é extensível.
* A estrutura não fornece um site pronto para uso imediato. Uma certa quantidade de trabalho de desenvolvimento é sempre necessária para adaptar a estrutura às suas especificações.

### Por quê? {#why}

* Fornecer os mecanismos básicos necessários para realizar rapidamente um site de comércio eletrônico personalizado.
* As dicas fornecem a flexibilidade necessária para desenvolver um site de comércio eletrônico real.
* Ilustrar as práticas recomendadas.
