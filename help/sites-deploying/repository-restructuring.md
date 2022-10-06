---
title: Reestruturação do repositório no AEM 6.5
seo-title: Repository Restructuring in AEM 6.5
description: Saiba mais sobre as noções básicas e o raciocínio por trás da reestruturação do repositório no AEM 6.5
seo-description: Learn about the basics and reasoning behind the repository restructuring in AEM 6.5
uuid: e9cd3e88-e352-44a8-9b97-69488d3267cb
contentOwner: chaikels
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: fc879b0b-823b-4bdc-aaa6-36f53a33fb22
feature: Upgrading
exl-id: 2572aa8d-2a3a-4e5b-ae5f-07e1017ea0f4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Reestruturação do repositório no AEM 6.5{#repository-restructuring-in-aem}

## Introdução {#introduction}

Antes do AEM 6.4, o código do cliente era implantado em áreas imprevisíveis do JCR que estavam sujeitas a alterações nas atualizações. Por causa disso, era comum que as versões formais do AEM substituíssem o código, a configuração ou o conteúdo personalizados. Além disso, as alterações no cliente às vezes substituíam AEM código de produto ou conteúdo, quebrando a funcionalidade do produto.

Ao definir claramente hierarquias para AEM código de produto e código de cliente, esses conflitos podem ser evitados.

Para esse fim, a partir do AEM 6.4 e para continuar em versões futuras, o conteúdo está sendo reestruturado de /etc para outras pastas no repositório, juntamente com diretrizes sobre o conteúdo que vai para onde, seguindo as seguintes regras de alto nível:

* AEM código de produto sempre será colocado em /libs, que não deve ser substituído pelo código personalizado
* O código personalizado deve ser colocado em /apps, /content e /conf

## Impacto nas atualizações do 6.5 {#impact-on-upgrades}

Ao atualizar para o AEM 6.5, um grande subconjunto do conteúdo em /etc será duplicado em outras pastas no repositório. Esses novos locais são os locais preferidos em que o conteúdo é referenciado. No entanto, todas as tentativas foram feitas para que a atualização do AEM 6.5 seja retroativamente compatível com os locais anteriores na pasta /etc e, portanto, na maioria dos casos, os locais antigos continuarão a ser referenciados pelo código AEM até que as alterações sejam feitas ativamente — e em muitos casos manualmente — no aplicativo de um cliente. Da perspectiva da linha do tempo, há duas categorias de alterações:

* Com a atualização 6.5 - algumas das alterações de reestruturação /etc não são compatíveis com versões anteriores e, portanto, as modificações devem ser planejadas e implementadas como parte da atualização AEM 6.5.
* Antes da atualização futura - a grande maioria das alterações de reestruturação /etc pode ser adiada até algum tempo no futuro pós-atualização. Como mencionado anteriormente, o código AEM 6.5 continuará referenciando os locais antigos até que as modificações sejam implementadas como parte de uma versão do cliente. Embora não haja uma linha do tempo forçada para a qual as alterações devem ser feitas, recomenda-se que elas sejam feitas antes da atualização futura, já que os recursos futuros podem depender dos novos locais que estão sendo referenciados. Além disso, a documentação de um determinado recurso fará referência por convenção aos novos locais e, portanto, pode ser confuso se os locais antigos ainda estiverem sendo usados.

### Orientação relativa à reestruturação {#restructuring-guidance}

Ao planejar uma atualização para o AEM 6.5, as seguintes páginas por solução devem ser referenciadas para avaliar o esforço de trabalho:

* [Restruturação do repositório comum a todas as soluções AEM](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md)
* [reestruturação de repositório AEM Sites](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md)
* [reestruturação de repositório AEM Assets](/help/sites-deploying/assets-repository-restructuring-in-aem-6-5.md)
* [Reestruturação de repositório AEM Assets Dynamic Media](/help/sites-deploying/dynamicmedia-repository-restructuring-in-aem-6-5.md)
* [reestruturação de repositório AEM Forms](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md)
* [reestruturação de repositório AEM Communities](/help/sites-deploying/communities-repository-restructuring-in-aem-6-5.md)
* [AEM reestruturação do repositório do Commerce](/help/sites-deploying/ecommerce-repository-restructuring-in-aem-6-5.md)

Cada página contém duas seções correspondentes à urgência das alterações necessárias. Qualquer coisa na seção &quot;Atualização 6.5&quot; deve ser abordada como parte do projeto de atualização do AEM 6.5. Qualquer coisa em &quot;Antes da atualização futura&quot; pode ser adiada opcionalmente até a posterior atualização.

Cada entrada na página inclui um campo &quot;Orientação sobre reestruturação&quot;, que detalha a estratégia técnica recomendada para alinhar com o novo modelo de repositório 6.5 para que os novos locais sejam referenciados para o conteúdo localizado anteriormente na pasta /etc. Um campo &quot;Observações&quot; adicional fornece qualquer contexto útil adicional.
