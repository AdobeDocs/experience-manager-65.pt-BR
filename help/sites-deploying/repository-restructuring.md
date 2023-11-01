---
title: Reestruturação do repositório no AEM 6.5
seo-title: Repository Restructuring in AEM 6.5
description: Saiba mais sobre as noções básicas e os motivos por trás da reestruturação do repositório no AEM 6.5
seo-description: Learn about the basics and reasoning behind the repository restructuring in AEM 6.5
uuid: e9cd3e88-e352-44a8-9b97-69488d3267cb
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: fc879b0b-823b-4bdc-aaa6-36f53a33fb22
feature: Upgrading
exl-id: 2572aa8d-2a3a-4e5b-ae5f-07e1017ea0f4
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Reestruturação do repositório no AEM 6.5{#repository-restructuring-in-aem}

## Introdução {#introduction}

Antes do AEM 6.4, o código do cliente era implantado em áreas imprevisíveis do JCR, que estavam sujeitas a alterações nas atualizações. Por causa disso, era comum que as versões formais do AEM substituíssem o código personalizado, a configuração ou o conteúdo. Além disso, as alterações do cliente às vezes substituíam o código ou conteúdo do produto AEM, quebrando a funcionalidade do produto.

Ao definir claramente hierarquias para código de produto AEM e código de cliente, esses conflitos podem ser evitados.

Para esse fim, a partir do AEM 6.4 e para continuar em versões futuras, o conteúdo está sendo reestruturado da pasta /etc para outras pastas no repositório, juntamente com diretrizes sobre o conteúdo que vai para onde, seguindo as seguintes regras de alto nível:

* O código do produto AEM sempre será colocado em /libs, que não deve ser substituído pelo código personalizado
* O código personalizado deve ser colocado em /apps, /content e /conf

## Impacto nas atualizações do 6.5 {#impact-on-upgrades}

Ao atualizar para o AEM 6.5, um grande subconjunto do conteúdo em /etc será duplicado em outras pastas no repositório. Esses novos locais são os locais preferidos nos quais o conteúdo é referenciado. No entanto, foi feita cada tentativa de atualizar o AEM 6.5 para que seja compatível com versões anteriores nos locais anteriores na pasta /etc. Portanto, na maioria dos casos, os locais antigos continuarão a ser referenciados pelo código AEM até que as alterações sejam feitas ativamente — e em muitos casos manualmente — no aplicativo de um cliente. Do ponto de vista da linha do tempo, há duas categorias de alterações:

* Com a atualização do 6.5 - algumas das alterações de reestruturação do /etc não são compatíveis com versões anteriores e, portanto, as alterações devem ser planejadas e implementadas como parte da atualização do AEM 6.5.
* Antes de uma atualização futura - a grande maioria das alterações de reestruturação de /etc pode ser adiada até algum momento no futuro pós-atualização. Como mencionado anteriormente, o código do AEM 6.5 continuará fazendo referência aos locais antigos até que as modificações sejam implementadas como parte de um lançamento de cliente. Embora não haja uma linha do tempo forçada para a qual as alterações devem ser feitas, recomenda-se que elas sejam feitas antes da atualização futura, pois os recursos futuros podem depender dos novos locais que estão sendo referenciados. Além disso, a documentação de um determinado recurso referenciará, por convenção, os novos locais e, portanto, poderá ser confuso se os locais antigos ainda estiverem sendo usados.

### Orientações em matéria de reestruturação {#restructuring-guidance}

Ao planejar uma atualização para o AEM 6.5, as seguintes páginas por solução devem ser referenciadas para avaliar o esforço de trabalho:

* [Reestruturação do repositório comum a todas as soluções de AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [Reestruturação de repositório do AEM Sites](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [Reestruturação de repositório do AEM Assets](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [Reestruturação de repositório do AEM Assets Dynamic Media](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [Reestruturação de repositório do AEM Forms](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [Reestruturação de repositório do AEM Communities](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [Restruturação do repositório de comércio AEM](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

Cada página contém duas seções correspondentes à urgência das alterações necessárias. Qualquer coisa na seção &quot;Com atualização do 6.5&quot; deve ser abordada como parte do projeto de atualização do AEM 6.5. Qualquer item em &quot;Antes da atualização futura&quot; pode ser opcionalmente adiado até a pós-atualização.

Cada entrada na página inclui um campo &quot;Orientação de reestruturação&quot;, que detalha a estratégia técnica recomendada para o alinhamento com o novo modelo de repositório 6.5, para que os novos locais sejam referenciados para o conteúdo anteriormente localizado na pasta /etc. Um campo &quot;Notas&quot; adicional fornece qualquer contexto útil adicional.
