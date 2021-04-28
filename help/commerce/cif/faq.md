---
title: AEM - Perguntas frequentes sobre a integração com o Commerce usando a Commerce Integration Framework
description: AEM - Perguntas frequentes sobre a integração com o Commerce usando a Commerce Integration Framework
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45,aece1190-9530-4060-9b08-022da7068987
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 46%

---

# AEM - Perguntas frequentes sobre a integração com o Commerce usando a Commerce Integration Framework

## 1. O GraphQL da CIF é usado apenas para comércio ou será disponibilizado para consultar conteúdo criado AEM JCR?

A Adobe adotou as APIs GraphQL da Magento como a API oficial para todos os dados relacionados ao comércio. Portanto, o AEM usa GraphQL para trocar dados de comércio com a Magento e com qualquer mecanismo de comércio por meio da I/O Runtime. Essa API GraphQL é independente AEM API GraphQL para acessar os Fragmentos de conteúdo.

## 2. Os ativos do produto (imagens) podem ser armazenados e referenciados AEM por meio do administrador do Adobe Commerce (Magento)? Como os ativos do Dynamic Media podem ser consumidos?

Não há integração AEM Assets - Magento oficial disponível. Há um conector de parceiro disponível no [marketplace](https://marketplace.magento.com/bounteous-dam.html).

Ou, como solução alternativa, você pode armazenar ativos de produtos (imagens) no AEM Assets, mas terá que armazenar manualmente os URLs de ativos no Magento. O Dynamic Media agora faz parte do AEM Assets e funcionará da mesma maneira.

## 3. Importa onde a solução comercial é implantada? (No local ou na nuvem)

Não, não importa onde sua solução comercial é implantada. A CIF e a loja de AEM funcionarão independentemente do modelo de implantação. No entanto, se a solução for implantada com a arquitetura de referência E2E recomendada, os testes E2E poderão ser executados em relação aos KPIs de desempenho que representam um perfil de cliente empresarial típico. Isso fornecerá informações adicionais que podem ser usadas como referencial.

## 4. Como as páginas de catálogo ou de produto são criadas no AEM? Como elas continuam a existir no AEM?

Páginas de catálogo e páginas de produto são criadas e armazenadas em cache dinamicamente no AEM com base em catálogos genéricos e modelos de página de produto. Nenhum dado de produto ou catálogo é importado e armazenado no AEM.

## 5. Quando você atualiza os dados do produto em sua solução comercial, isso é um push em tempo real para AEM? Ou é um processo em lote?

O complemento CIF usado com AEM permite que os dados fluam da solução comercial para AEM sob demanda. Portanto, esse não é um processo de push em tempo real ou em lote quando há uma atualização na solução comercial.

## 6. Que tamanho de catálogo AEM com o suporte à CIF?

Isso depende de alguns aspectos adicionais que você precisa considerar. Qual é a proporção de cache dos dados e páginas do catálogo? Quantas solicitações simultâneas você espera durante as horas de pico? Qual é a escala das APIs de suas soluções comerciais?

## 7. Como o PIM atua nessa estrutura?

Os dados do PIM são expostos ao AEM e aos clientes por meio de solicitações de GraphQL. Nossa recomendação é integrar o PIM ao mecanismo de comércio (Magento ou outros) para que os dados do PIM possam ser recuperados do mecanismo de comércio.

## 8. Também é possível armazenar preços e outros dados em cache por meio do Dispatcher? Esse armazenamento gera um desafio frequente de invalidação de cache?

Dados dinâmicos, como preço ou inventário, não são armazenados em cache no Dispatcher. Os dados dinâmicos são obtidos por via direta no lado do cliente com componentes da Web usando APIs GraphQL. Somente dados estáticos (como dados de produto ou categoria) são armazenados em cache no Dispatcher. Se os dados do produto forem alterados, será preciso invalidar o cache.

## 9. Como a invalidação de cache para AEM Dispatcher funciona com AEM e comércio?

Recomendamos configurar a invalidação do cache com base em TTL para páginas armazenadas em cache no Dispatcher. Para obter informações dinâmicas, como preço ou estoque, recomendamos renderizar a data no lado do cliente. Para obter mais informações sobre a invalidação do cache com base em TTL, consulte [AEM Dispatcher](https://helpx.adobe.com/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 10. Há alguma recomendação sobre a pesquisa unificada de conteúdo no AEM com o Commerce?

É fornecida uma implementação de referência de pesquisa de produto, mas não de pesquisa unificada com conteúdo. Geralmente, esse recurso depende muito do cliente e é melhor encontrar uma solução para cada projeto.

## 11. Como a pesquisa funciona com AEM e comércio usando a CIF?

A CIF fornece os componentes Barra de pesquisa e Resultado da pesquisa. O componente Barra de pesquisa envia uma solicitação GraphQL com o termo de pesquisa para a solução de comércio, que retorna uma lista de produtos que inclui nome do produto, preço, SLUG, etc. O componente Resultado da pesquisa exibe os resultados da pesquisa em uma visualização de galeria em uma página de resultados da pesquisa criada no AEM. A Pesquisa aceita pesquisa básica de texto completo. Usamos a chave SLUG/URL para criar uma referência ao PDP.

## 12. Como os dados do produto podem ser usados em MSM ou traduções?

Os dados do produto geralmente já são traduzidos no PIM ou na Magento. A integração AEM–Magento suporta a conexão com várias lojas e visualizações de loja da Magento. Geralmente, em uma configuração MSM um site do AEM está vinculado a uma visualização da loja da Magento.

## 13. Há alguma maneira de aprimorar os dados do produto com texto comercial? Onde é possível fazer isso? No AEM ou na solução comercial?

Recomendamos o gerenciamento de dados e conteúdo relacionados ao marketing no AEM. Decorre dados de produtos de sua solução comercial com atributos adicionais usando Fragmentos de conteúdo ou crie e vincule Fragmentos de experiência para conteúdo não estruturado com seus produtos.

## 14. Como podemos garantir a conformidade com o PCI ao usar o AEM para a camada de apresentação inteira?

Recomendamos o uso de métodos de pagamento abstratos. Isso coloca o cliente do navegador em comunicação direta com o provedor do gateway de pagamento para que nem o Adobe nem as soluções de comércio retenham ou transmitam os dados do titular do cartão. Esta abordagem requer apenas uma conformidade PCI de nível 3. No entanto, há outros aspectos que devem ser considerados em termos de conformidade com o PCI, como o modo como os funcionários interagem com o sistema e os dados. Para obter mais informações sobre a conformidade com a Magento PCI, consulte <https://magento.com/pci-compliance>

## 15. Se eu usar versões de nuvem de AEM e Magento, esta solução conjunta é compatível com PCI?

Sim, o questionário de autoavaliação D e o certificado de conformidade estão disponíveis a pedido.

## 16. Como posso solicitar uma licença de avaliação da I/O Runtime?

Você pode solicitar uma licença de avaliação para usar a I/O Runtime [aqui](https://adobeio.typeform.com/to/obqgRm).
