---
title: Configuração de várias lojas do Commerce
description: Saiba como mapear várias exibições de loja do Adobe Commerce para o AEM. Isso permite que os projetos sejam compatíveis com casos de uso de vários locatários e vários idiomas.
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
exl-id: 1d4e9b7b-848b-4007-b884-dd48682d62e8
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 15%

---

# Configuração de várias lojas do Commerce {#multi-store}

AEM Os Componentes principais do CIF podem ser usados em várias estruturas de site do AEM e a implementação de cliente GraphQL subjacente pode se conectar a diferentes lojas/visualizações de loja da Adobe Commerce. Assim, os projetos podem implementar configurações complexas de várias lojas/vários sites.

Uma apresentação em vídeo detalhando as opções para integrar várias visualizações da Adobe Commerce Store ao Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Os recursos de Gerenciamento de vários sites do AEM para Live Copy e Language Copy são usados com o Commerce integration framework para gerenciar sites globalmente em regiões e localidades.

A configuração recomendada é usar uma relação 1:1 entre o site do AEM e a exibição da loja da Adobe Commerce.

Para conectar um site de AEM AEM e os componentes principais de CIF também a uma visualização de loja dedicada, siga as etapas abaixo:

## Configuração {#configuration}

1. Configure várias lojas e visualizações de loja de acordo com o padrão descrito em [Sites, lojas e visualizações da Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)

2. Verifique se a conexão entre AEM e Adobe Commerce está funcionando.

3. Crie uma configuração secundária da configuração do CIF Cloud Service seguindo estas etapas:

   * No AEM, vá para Ferramentas > Geral > [Navegador de Configuração](/help/sites-administering/configurations.md#using-configuration-browser)
   * Selecione a configuração básica que você criou
   * Crie uma configuração usando as etapas descritas no ponto 2 acima

   Essa nova configuração é criada como uma configuração secundária da base. Agora você pode acessar Ferramentas > Geral > Navegador de configuração e criar as configurações.

   >[!TIP]
   >
   >Os catálogos do Commerce podem ser endereçados usando IDs ou UIDs. Os UIDs foram introduzidos no Adobe Commerce 2.4.2. Habilite isso somente se o back-end de comércio suportar um esquema do GraphQL versão 2.4.2 ou posterior.

4. Atribua a configuração secundária a um site do AEM

   * Acesse o console do AEM Sites
   * Acesse a raiz de região ou idioma da estrutura do site, por exemplo, /content/venia/us _ou_ /content/venia/us/en para a página de exemplo Venia.
   * Selecione a página e abra as propriedades dela
   * Selecione a guia Avançado
   * Na seção `Configuration`, selecione a configuração criada na etapa

## Recursos adicionais

* [Sites, Lojas e Exibições do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)
* [Componentes principais da CIF do AEM — Configuração de várias lojas/sites](https://github.com/adobe/aem-core-cif-components#multi-store--site-configuration)
* [Usar o gerenciamento de vários sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Reutilizar conteúdo: gerenciador de vários sites e Live Copy](/help/sites-administering/msm.md)
