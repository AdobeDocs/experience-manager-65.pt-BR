---
title: AEM - Perguntas frequentes sobre a integração do Commerce usando a Commerce Integration Framework
description: AEM - Perguntas frequentes sobre a integração do Commerce usando a Commerce Integration Framework
exl-id: d541607f-c4c9-4dd5-aadf-64d4cb5f9f2a
source-git-commit: c96f83b84ed1473aee0ddcca08a0e585ec088aa1
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 23%

---

# AEM - Perguntas frequentes sobre a integração do Commerce usando a Commerce Integration Framework

## 1. O CIF GraphQL é usado apenas para comércio ou está disponível para consultar conteúdo criado no AEM JCR?

A Adobe adotou as APIs do GraphQL da Adobe Commerce como a API oficial para todos os dados relacionados ao comércio. Portanto, o AEM usa o GraphQL para trocar dados de comércio com o Adobe Commerce e com qualquer mecanismo de comércio por meio da I/O Runtime. Essa API do GraphQL é independente da API do AEM GraphQL para acessar fragmentos de conteúdo.

## 2. Os ativos do produto (imagens) podem ser armazenados e referenciados pelo AEM por meio do administrador do Adobe Commerce? Como os ativos do Dynamic Media podem ser consumidos?

Não há integração oficial entre o AEM Assets e o Adobe Commerce disponível. Há um conector parceiro disponível na [marketplace](https://marketplace.magento.com/partner/bounteous_ecomm).

Ou, como solução alternativa, você pode armazenar ativos de produtos (imagens) no AEM Assets, mas precisa armazenar manualmente os URLs de ativos no Adobe Commerce. O Dynamic Media faz parte do AEM Assets e funciona da mesma maneira.

## 3. O local de implantação da solução comercial é importante? (No local ou na nuvem)

Não, não importa onde a solução comercial é implantada. A CIF e a loja AEM funcionam independentemente do modelo de implantação. No entanto, se a solução for implantada com a arquitetura de referência E2E recomendada, os testes E2E poderão ser executados em KPIs de desempenho que representam um perfil de cliente empresarial típico. Esse processo fornece informações adicionais que podem ser usadas como referencial.

## 4. Como as páginas de catálogo ou de produto são criadas no AEM? Como elas continuam a existir no AEM?

Páginas de catálogo e páginas de produto são criadas e armazenadas em cache dinamicamente no AEM com base em catálogos genéricos e modelos de página de produto. Nenhum dado de produto ou catálogo é importado e armazenado no AEM.

## 5. A atualização dos dados do produto na solução comercial é um push em tempo real para o AEM? Ou é um processo em lote?

O complemento CIF usado com AEM permite que os dados fluam da solução comercial para o AEM sob demanda. Portanto, esse workflow não é um processo de push em tempo real ou em lote quando há uma atualização na solução comercial.

## 6. Que tamanho de catálogo o AEM é compatível com a CIF?

O suporte ao tamanho do catálogo depende de alguns aspectos adicionais que você deve considerar. Qual é a taxa de cache de seus dados e páginas de catálogo? Quantas solicitações simultâneas você espera durante as horas de pico? Qual é a escalabilidade das APIs das suas soluções comerciais?

## 7. Como o PIM atua nessa estrutura?

Os dados do PIM são expostos ao AEM e aos clientes por meio de solicitações do GraphQL. A recomendação do Adobe é integrar o PIM ao mecanismo de comércio (Adobe Commerce ou outros) para que os dados do PIM possam ser recuperados do mecanismo de comércio.

## 8. Também é possível armazenar preços e outros dados em cache por meio do Dispatcher? Esse armazenamento gera um desafio frequente de invalidação de cache?

Dados dinâmicos, como preço ou inventário, não são armazenados em cache no Dispatcher. Os dados dinâmicos são obtidos por via direta no lado do cliente com componentes da Web usando APIs GraphQL. Somente dados estáticos (como dados de produto ou categoria) são armazenados em cache no Dispatcher. Se os dados do produto forem alterados, a invalidação de cache será necessária.

## 9. Como a invalidação de cache para o AEM Dispatcher funciona com AEM e comércio?

O Adobe recomenda configurar a invalidação do cache com base em TTL para páginas armazenadas em cache no Dispatcher. Para obter informações dinâmicas, como preço ou estoque, a Adobe recomenda renderizar a data no lado do cliente. Para obter mais informações sobre a invalidação do cache com base em TTL, consulte [Dispatcher AEM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html?lang=pt-BR)

## 10. Há alguma recomendação sobre a pesquisa unificada de conteúdo no AEM com o Commerce?

É fornecida uma implementação de referência de pesquisa de produto, mas não de pesquisa unificada com conteúdo. Esse recurso é específico do cliente e é melhor encontrar uma solução para cada projeto.

## 11. Como a pesquisa funciona com AEM e comércio usando a CIF?

A CIF fornece os componentes Barra de pesquisa e Resultado da pesquisa. O componente Barra de pesquisa envia uma solicitação GraphQL com o termo de pesquisa para a solução comercial, que retorna uma lista de produtos que inclui nome do produto, preço, SLUG e assim por diante. O componente Resultado da pesquisa exibe os resultados da pesquisa em uma visualização de galeria em uma página de resultados da pesquisa criada no AEM. A Pesquisa aceita pesquisa básica de texto completo. Use a chave SLUG/url para criar uma referência ao PDP.

## 12. Como os dados do produto podem ser usados em MSM ou traduções?

Os dados do produto já estão traduzidos no PIM ou no Adobe Commerce. A Integração AEM - Adobe Commerce oferece suporte à conexão com várias lojas e visualizações de loja da Adobe Commerce. Em uma configuração do MSM, normalmente um site de AEM é vinculado a uma visualização de loja da Adobe Commerce.

## 13. Há alguma maneira de aprimorar os dados do produto com texto comercial? Em caso afirmativo, onde é feito? No AEM ou na solução comercial?

a Adobe recomenda gerenciar dados e conteúdo relacionados ao marketing no AEM. Decorar dados de produtos a partir de sua solução comercial com atributos adicionais usando Fragmentos de conteúdo ou criar e vincular Fragmentos de experiência para conteúdo não estruturado com seus produtos.

## 14. Como uma empresa garante a conformidade com o PCI ao usar AEM para toda a camada de apresentação?

Adobe recomenda usar métodos de pagamento abstratos. Isso coloca o cliente do navegador em comunicação direta com o provedor do gateway de pagamento para que o Adobe não mantenha ou transmita a data do titular do cartão nem as soluções comerciais. Essa abordagem requer somente uma conformidade com PCI de nível 3. No entanto, há outros aspectos que devem ser considerados em termos de conformidade com o PCI, como a forma como os funcionários interagem com o sistema e os dados. Para obter mais informações sobre a conformidade da Adobe Commerce com o PCI, consulte [Conformidade com o PCI](https://business.adobe.com/products/magento/pci-compliance.html)

## 15. Se eu usar as versões em nuvem do AEM e do Adobe Commerce, essa solução conjunta é compatível com o PCI?

Sim, o Questionário de autoavaliação D e o Atestado de conformidade estão disponíveis mediante solicitação.

## 16. Como posso solicitar uma licença de avaliação da I/O Runtime?

Você pode solicitar uma licença de avaliação para usar a I/O Runtime [aqui](https://adobeio.typeform.com/to/obqgRm).
