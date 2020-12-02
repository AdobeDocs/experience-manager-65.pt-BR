---
title: eCommerce
seo-title: eCommerce
description: AEM eCommerce ajuda os comerciantes a oferecerem experiências de compras personalizadas e com marca em pontos de contato da Web, móveis e sociais.
seo-description: AEM eCommerce ajuda os comerciantes a oferecerem experiências de compras personalizadas e com marca em pontos de contato da Web, móveis e sociais.
uuid: 75818c60-1cf1-4a91-94ce-d722563b661c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: e972ee05-f0cb-40ca-9ae2-34395791c709
docset: aem65
translation-type: tm+mt
source-git-commit: 46610888fd61900c52b197e73a8a5850dc9c4c35
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 1%

---


# eCommerce{#ecommerce}

* [Conceitos ](/help/sites-administering/concepts.md)
* [Administração (genérica)](/help/sites-administering/generic.md)

O Adobe fornece duas versões da Commerce Integration Framework:

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
     <li>Magento</li>
     <li>Java e Javascript</li>
     <li>Nenhum dado de comércio armazenado no repositório JCR</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Front-end</p> </td>
   <td><p>Páginas renderizadas do servidor AEM</p> </td>
   <td>Aplicativo de página mista (renderização híbrida)</td>
  </tr>
  <tr>
   <td><p>Catálogo de produtos</p> </td>
   <td>
    <ul>
     <li>Importador de produtos, editor, cache em AEM</li>
     <li>Catálogos regulares com páginas AEM ou proxy</li>
    </ul> </td>
   <td>
    <ul>
     <li>Nenhuma importação de produto</li>
     <li>Modelos genéricos</li>
     <li>Dados sob demanda por conector</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Escalabilidade</p> </td>
   <td>
    <ul>
     <li>Pode suportar até alguns milhões de produtos (depende do caso de uso)</li>
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
   <td>Sim, schema Magento GraphQL</td>
  </tr>
  <tr>
   <td>Disponibilidade</td>
   <td><p>Sim. SAP Commerce Cloud (Extensão atualizada para suportar AEM 6.4 e Hybris 5 (padrão) e mantém a compatibilidade com Hybris 4</p> <p>Salesforce Commerce Cloud (Conector de fonte aberta para suporte ao AEM 6.4)</p> </td>
   <td>Sim via código aberto via GitHub. Magento Commerce (Suporta Magento 2.3.2 (padrão) e compatível com Magento 2.3.1).</td>
  </tr>
  <tr>
   <td>Quando usar</td>
   <td>Casos de utilização limitados: Por exemplo, para situações em que catálogos pequenos e estáticos podem precisar ser importados</td>
   <td>Solução preferencial na maioria dos casos de uso</td>
  </tr>
 </tbody>
</table>

O eCommerce, juntamente com o Gerenciamento de Informações do Produto (PIM), trata das atividades de um site focado na venda de produtos por meio de uma loja online:

* Criação, duração e obsolescência de um produto
* Gestão de preços
* Gerenciamento de transações
* Gerenciamento de catálogos inteiros
* Registros de armazenamentos ao vivo e centralizados
* Interfaces Web

AEM eCommerce ajuda os comerciantes a oferecerem experiências de compras personalizadas e com marca em pontos de contato da Web, móveis e sociais. O ambiente de criação de AEM permite personalizar páginas e componentes com base no contexto do visitante do público alvo e nas estratégias de comercialização; por exemplo:

* Páginas de produto
* Componentes do carrinho de compras
* Componentes de checkout

A implementação permite acesso em tempo real às informações do produto. Isso pode ser usado para impor:

* Integridade das informações do produto
* Preços
* Inventário de manutenção de existências
* Variações no estado de um carrinho de compras

>[!NOTE]
>
>Para usar a estrutura de integração com provedores externos de comércio eletrônico, primeiro é necessário instalar os pacotes necessários. Para obter mais informações, consulte [Implantação do eCommerce](/help/sites-deploying/ecommerce.md).
>
>Para obter informações sobre como estender os recursos de comércio eletrônico, consulte [Desenvolvimento do comércio eletrônico](/help/sites-developing/ecommerce.md).

## Principais recursos {#main-features}

AEM eCommerce fornece:

* Uma série de **componentes predefinidos AEM** para ilustrar o que pode ser obtido para o seu projeto:

   * Exibição do produto
   * Carrinho de compras
   * Check-out
   * Produtos visualizados recentemente
   * Vouchers
   * e outros

   ![](assets/chlimage_1-130.png)

   >[!NOTE]
   >
   >A estrutura de integração fornecida pela AEM também permite que você construa componentes AEM adicionais para recursos de comércio, independentemente do seu mecanismo específico de eCommerce.

* **Pesquisar**  - usando:

   * a pesquisa AEM
   * a pesquisa do sistema de comércio eletrônico
   * uma pesquisa de terceiros (como o Search &amp; Promote)
   * ou uma combinação dos mesmos.

   ![](assets/chlimage_1-131.png)

* Usa a capacidade AEM de **apresentar seu conteúdo em vários canais**, seja na janela completa do navegador ou no dispositivo móvel. Isso fornece o conteúdo no formato necessário aos seus visitantes.

   ![](assets/chlimage_1-132.png)

* A capacidade de **desenvolver sua própria implementação de integração com base na [AEM estrutura de comércio eletrônico](#the-framework)**.

   As duas implementações atualmente disponíveis são ambas construídas na mesma base - além da API geral (a estrutura). A implementação de uma nova integração envolve apenas a implementação dos recursos de que sua integração precisa. Os componentes front-end podem ser usados por qualquer nova implementação, pois usam interfaces (portanto, são independentes da implementação).

* A possibilidade de desenvolver **comércio orientado por experiência com base nos dados do comprador e na atividade**. Isso permite que você realize vários cenários:

   * Um exemplo pode ser o de fornecer reduções nos custos de envio quando o pedido total exceder uma quantia específica.
   * Outra opção pode permitir que você forneça ofertas sazonais que usam dados do perfil (por exemplo, localização). Estes podem ser depois salientados, dependendo novamente de outros fatores, quando necessário.

   No exemplo abaixo, um teaser é mostrado, pois o conteúdo do carrinho é inferior a $75:

   ![](assets/chlimage_1-133.png)

   Isso pode ser alterado quando o conteúdo do carrinho exceder $75:

   ![](assets/chlimage_1-134.png)

* E outros recursos, incluindo:

   * Conteúdo do carrinho de compras retido nas sessões
   * Histórico completo do pedido
   * Atualização do catálogo expresso

## A Estrutura {#the-framework}

A seção [Conceitos](/help/sites-administering/concepts.md) cobre a estrutura com mais detalhes, mas o seguinte fornece uma visualização de alto nível e alta velocidade da estrutura:

### O quê? {#what}

* A estrutura de integração fornece a API, uma variedade de componentes para ilustrar a funcionalidade e várias extensões para fornecer exemplos de métodos de conexão.
* O quadro fornece a estrutura básica necessária para a execução de um projeto.
* A estrutura é extensível.
* A estrutura não fornece um site pronto para uso e pronto para uso. É sempre necessário um certo trabalho de desenvolvimento para adaptar a estrutura às suas especificações.

### Por quê? {#why}

* Fornecer os mecanismos básicos necessários para realizar rapidamente um site personalizado de eCommerce.
* A Tp oferece a flexibilidade necessária para desenvolver um site real de comércio eletrônico.
* Ilustrar as práticas recomendadas.