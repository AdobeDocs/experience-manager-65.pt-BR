---
title: Configuração de várias lojas do Commerce
description: Saiba como mapear várias exibições de loja do Adobe Commerce para o AEM. Isso permite que os projetos suportem casos de uso de vários locatários e várias línguas.
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 1d4e9b7b-848b-4007-b884-dd48682d62e8
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 44%

---

# Configuração de várias lojas do Commerce {#multi-store}

Os Componentes principais da CIF do AEM podem ser usados em várias estruturas de site do AEM e a implementação de cliente do GraphQL subjacente pode se conectar a diferentes lojas/visualizações de loja da Adobe Commerce. Assim, os projetos podem implementar configurações complexas de várias lojas/vários sites.

Um vídeo que detalha detalhadamente as opções para integrar várias visualizações da Adobe Commerce Store ao Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Os recursos de gerenciamento de vários sites do AEM para Live Copy e Language Copy são usados junto com a Commerce Integration Framework para gerenciar sites em várias regiões e locales.

A configuração recomendada é usar uma relação 1:1 entre AEM site e a visualização da loja da Adobe Commerce.

Para conectar um site AEM e AEM os Componentes principais da CIF a uma visualização de loja dedicada, siga as etapas abaixo:

## Configuração {#configuration}

1. Configure várias lojas e visualizações de loja de acordo com o padrão descrito em [Sites, lojas e visualizações da Adobe Commerce](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. Verifique se a conexão entre o AEM e o Adobe Commerce está funcionando.

3. Crie uma configuração secundária da configuração do CIF Cloud Service seguindo estas etapas:

   * AEM acesse Ferramentas -> Geral -> [Navegador de configuração](/help/sites-administering/configurations.md#using-configuration-browser)
   * Selecione a configuração básica que você criou
   * Criar uma nova configuração usando as etapas descritas no ponto 2 acima

   Essa nova configuração será criada como uma configuração secundária da base. Agora você pode acessar Ferramentas -> Geral -> Navegador de configuração e criar as configurações.

   >[!TIP]
   >
   >Os catálogos de comércio podem ser abordados usando IDs ou UIDs. Os UIDs foram introduzidos no Adobe Commerce 2.4.2. Habilite-os somente se o back-end de comércio suportar um esquema GraphQL da versão 2.4.2 ou posterior.

4. Atribua a configuração secundária a um site do AEM

   * Acesse o console do AEM Sites
   * Navegue até a raiz de região ou idioma da estrutura do site, por exemplo /content/venia/us _ou_ /content/venia/us/en para a página de exemplo Venia
   * Selecione a página e abra as propriedades da página
   * Selecione a guia Avançado
   * Na seção `Configuration` selecione a configuração que você criou na etapa 3

## Recursos adicionais

* [Sites, lojas e visualizações da Adobe Commerce](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [Componentes principais da CIF do AEM — Configuração de várias lojas/sites](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [Usar o gerenciamento de vários sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Reutilizar conteúdo: gerenciador de vários sites e Live Copy](/help/sites-administering/msm.md)
