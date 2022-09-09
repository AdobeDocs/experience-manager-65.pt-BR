---
title: eCommerce
description: AEM eCommerce ajuda os profissionais de marketing a fornecer experiências de compras personalizadas e com marca em todos os pontos de contato da Web, móveis e sociais.
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: d995f0d6-9e48-4228-ac82-f33a0b25b9d3
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# comércio eletrônico{#ecommerce}

* [Conceitos ](/help/commerce/cif-classic/administering/concepts.md)
* [Administração (genérica)](/help/commerce/cif-classic/administering/generic.md)

O Adobe fornece duas versões da Estrutura de integração de comércio:

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
     <li>Integração monolítica, mapeamento pré-criado (modelo)</li>
     <li>Repositório JCR</li>
    </ul> </td>
   <td>
    <ul>
     <li>Adobe Commerce</li>
     <li>Java e Javascript</li>
     <li>Nenhum dado de comércio armazenado no repositório JCR</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Front-end</p> </td>
   <td><p>AEM páginas renderizadas do lado do servidor</p> </td>
   <td>Aplicativo de página mista (renderização híbrida)</td>
  </tr>
  <tr>
   <td><p>Catálogo de produtos</p> </td>
   <td>
    <ul>
     <li>Importador de produto, editor, armazenamento em cache em AEM</li>
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
   <td>Sim, esquema GraphQL da Adobe Commerce</td>
  </tr>
  <tr>
   <td>Disponibilidade</td>
   <td><p>Sim. SAP Commerce Cloud (Extensão atualizada para oferecer suporte ao AEM 6.4 e Hybris 5 (padrão) e mantém compatibilidade com Hybris 4</p> <p>Salesforce Commerce Cloud (Conector de software aberto para suporte ao AEM 6.4)</p> </td>
   <td>Sim por meio do código aberto via GitHub. Adobe Commerce (Suporta 2.3.2 (padrão) e compatível com 2.3.1).</td>
  </tr>
  <tr>
   <td>Quando usar</td>
   <td>Casos de uso limitados: Por exemplo, cenários em que catálogos pequenos e estáticos podem precisar ser importados</td>
   <td>Solução preferencial na maioria dos casos de uso</td>
  </tr>
 </tbody>
</table>

O eCommerce, juntamente com o Product Information Management (PIM), lida com as atividades de um site focado na venda de produtos por meio de uma loja online:

* Criação, duração e obsolescência de um produto
* Gestão de preços
* Gerenciamento de transações
* Gestão de catálogos inteiros
* Registros de armazenamento ao vivo e centralizado
* Interfaces da Web

AEM eCommerce ajuda os profissionais de marketing a fornecer experiências de compras personalizadas e com marca em todos os pontos de contato da Web, móveis e sociais. O ambiente de criação de AEM permite personalizar páginas e componentes com base no contexto do visitante do público-alvo e nas estratégias de comercialização; por exemplo:

* Páginas de produto
* Componentes do carrinho de compras
* Componentes de check-out

A implementação permite acesso em tempo real às informações do produto. Isso pode ser usado para impor:

* Integridade das informações do produto
* Preços
* Inventário de manutenção de estoque
* Variações no estado de um carrinho de compras

>[!NOTE]
>
>Para usar a estrutura de integração com provedores externos de comércio eletrônico, primeiro é necessário instalar os pacotes necessários. Para obter mais informações, consulte [Implantação do comércio eletrônico](/help/commerce/cif-classic/deploying/ecommerce.md).
>
>Para obter informações sobre como estender os recursos de comércio eletrônico, consulte [Desenvolvimento do comércio eletrônico](/help/commerce/cif-classic/developing/ecommerce.md).

## Recursos principais {#main-features}

AEM eCommerce fornece:

* Um número de **componentes de AEM prontos para uso** para ilustrar o que pode ser feito para o seu projeto:

   * Exibição do produto
   * Carrinho de compras
   * Check-out
   * Produtos visualizados recentemente
   * Vouchers
   * e outros

   ![](/help/sites-administering/assets/chlimage_1-130.png)

   >[!NOTE]
   >
   >A estrutura de integração fornecida pelo AEM também permite que você crie componentes de AEM adicionais para recursos de comércio, independentemente do mecanismo de comércio eletrônico específico.

* **Pesquisar** - utilizando:

   * a pesquisa de AEM
   * a pesquisa do sistema de comércio eletrônico
   * uma pesquisa de terceiros
   * ou uma combinação destes.

   ![](/help/sites-administering/assets/chlimage_1-131.png)

* Usa a capacidade AEM para **apresentar seu conteúdo em vários canais**, seja essa janela completa do navegador ou dispositivo móvel. Isso entrega seu conteúdo no formato necessário para seus visitantes.

   ![](/help/sites-administering/assets/chlimage_1-132.png)

* A capacidade de **desenvolva sua própria implementação de integração com base no [Estrutura de comércio eletrônico AEM](#the-framework)**.

   As duas implementações atualmente disponíveis são criadas na mesma base - além da API geral (a estrutura). A implementação de uma nova integração envolve apenas a implementação dos recursos de que sua integração precisa. Os componentes de front-end podem ser usados por qualquer nova implementação, pois usam interfaces (assim, são independentes da implementação).

* A possibilidade de desenvolver **comércio orientado para a experiência com base em dados e atividade do comprador**. Isso permite que você perceba vários cenários:

   * Um exemplo pode ser fornecer reduções nos custos de envio quando o pedido total exceder um valor específico.
   * Outro pode permitir que você forneça ofertas sazonais que usam dados de perfil (por exemplo, localização). Estes podem ser realçados, novamente dependendo de outros fatores, quando necessário.

   No exemplo abaixo, um teaser é mostrado, pois o conteúdo do carrinho é inferior a US$ 75:

   ![](/help/sites-administering/assets/chlimage_1-133.png)

   Isso pode ser alterado quando o conteúdo do carrinho exceder $75:

   ![](/help/sites-administering/assets/chlimage_1-134.png)

* E outros recursos, incluindo:

   * Conteúdo do carrinho de compras retido nas sessões
   * Histórico completo do pedido
   * Atualização do catálogo expresso

## Enquadramento {#the-framework}

O [Conceitos](/help/commerce/cif-classic/administering/concepts.md) A seção aborda a estrutura com mais detalhes, mas o seguinte fornece uma visão de alto nível e de alta velocidade da estrutura:

### O quê? {#what}

* A estrutura de integração fornece a API, uma variedade de componentes para ilustrar a funcionalidade e várias extensões para fornecer exemplos de métodos de conexão.
* O quadro fornece a estrutura básica necessária para a implementação de um projeto.
* A estrutura é extensível.
* A estrutura não fornece um site pronto para uso e pronto para uso. É sempre necessário um certo trabalho de desenvolvimento para adaptar a estrutura às suas especificações.

### Por quê? {#why}

* Fornecer os mecanismos básicos necessários para realizar rapidamente um site personalizado de eCommerce.
* A Tp oferece a flexibilidade necessária para desenvolver um site de comércio eletrônico real.
* Ilustre as práticas recomendadas.
