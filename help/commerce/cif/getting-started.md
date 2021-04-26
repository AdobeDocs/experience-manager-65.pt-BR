---
title: Introdução ao conteúdo e comércio AEM
description: Saiba como implantar um projeto de Conteúdo e Comércio AEM.
topics: Commerce
feature: Estrutura de integração de comércio
thumbnail: 37843.jpg
translation-type: tm+mt
source-git-commit: 8ead3d1b24177effa4d40141408c5676eaabcc30
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 5%

---

# Introdução ao conteúdo e comércio AEM {#start}

Para começar a usar AEM Content and Commerce, é necessário instalar o AEM Content and Commerce Add-On for AEM 6.5.

## Requisito mínimo de software

[AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) 7 ou posterior é necessário.

## Integração {#onboarding}

A integração do conteúdo e do comércio AEM é um processo de duas etapas:

1. Instale o complemento Conteúdo AEM e Commerce para o AEM 6.5

2. Conectar AEM com sua solução comercial

### Instale o complemento Conteúdo AEM e Commerce para o AEM 6.5

Baixe e instale o AEM Commerce Add-On para AEM 6.5 no portal [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).

Inicie e instale o AEM 6.5 Service Pack necessário. Recomendamos instalar o último service pack disponível.

    >[!NOTA]
     > 
     > Isso será feito pelo CSE para clientes do Serviço gerenciado AEM.

### Conectar AEM ao seu sistema de comércio

AEM pode ser conectado a qualquer sistema de comércio que tenha um ponto de extremidade GraphQL acessível para AEM. Normalmente, esses pontos de extremidade estão disponíveis publicamente ou podem ser conectados via VPN privada ou conexões locais, dependendo da configuração individual do projeto.

Opcionalmente, é possível fornecer o cabeçalho de autenticação para usar recursos adicionais da CIF que exigem autenticação.

Os projetos gerados pelo [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) e o [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) que já está incluído no [default config](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.grafql.client.impl.GraphqlClientImpl~default.cfg.json) devem ser ajustados.

Substitua o valor de `url` em `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` pelo ponto de extremidade GraphQL do sistema de comércio. Essa configuração pode ser feita por meio do console OSGI ou da implantação da configuração OSGI por meio do projeto. Diferentes configurações para sistemas de armazenamento temporário e de produção são suportadas usando diferentes modos de execução de AEM.

Os Componentes principais do AEM Content and Commerce e da CIF usam conexões AEM lado do servidor e do cliente. Os Componentes principais da CIF do lado do cliente e as ferramentas de criação do complemento CIF se conectam por padrão ao `/api/graphql`. Isso pode ser ajustado através da configuração do Cloud Service da CIF, se necessário (veja abaixo).

O complemento CIF fornece um servlet proxy GraphQL em `/api/graphql` que pode ser usado opcionalmente para [desenvolvimento local](develop.md). Para implantações de produção, é altamente recomendável configurar um proxy reverso para o ponto de extremidade GraphQL de comércio por meio do Dispatcher AEM ou em outras camadas de rede (como CDN).

## Configuração de lojas e catálogos {#catalog}

O complemento e os [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components) podem ser usados em várias estruturas de site de AEM conectadas a diferentes lojas de comércio (ou visualizações de loja, etc). Por padrão, o complemento CIF é implantado com uma configuração padrão que se conecta à loja e ao catálogo padrão do Adobe Commerce (Magento).

Essa configuração pode ser ajustada para o projeto por meio da configuração do Cloud Service da CIF, seguindo estas etapas:

1. AEM acesse Ferramentas -> Cloud Services -> Configuração da CIF

2. Selecione a configuração de comércio que deseja alterar

3. Abra as propriedades de configuração na barra de ações

![Configuração do CIF Cloud Services](/help/commerce/cif/assets/cif-cloud-service-config.png)

As seguintes propriedades podem ser configuradas:

- Cliente GraphQL - selecione o cliente GraphQL configurado para comunicação de back-end de comércio. Normalmente, isso deve permanecer no padrão.
- Exibição de armazenamento - o identificador de exibição de loja (Magento). Se estiver vazia, a exibição de loja padrão será usada.
- Caminho do proxy GraphQL - o caminho do URL Proxy GraphQL no AEM usado para solicitações de proxy no ponto de extremidade GraphQL de back-end do comércio.
   >[!NOTE]
   >
   > Na maioria das configurações, o valor padrão `/api/graphql` não deve ser alterado. Somente a configuração avançada que não usa o proxy GraphQL fornecido deve alterar essa configuração.
- Ativar o suporte à UID do catálogo - ative o suporte para UID em vez da ID nas chamadas GraphQL de back-end de comércio.
   >[!NOTE]
   >
   > O suporte para UIDs foi introduzido no Adobe Commerce (Magento) 2.4.2. Habilite-o somente se o back-end comercial suportar um esquema GraphQL da versão 2.4.2 ou posterior.
- Identificador de categoria raiz do catálogo - o identificador (UID ou ID) da raiz do catálogo de loja

A configuração mostrada acima é para referência. Os projetos devem fornecer suas próprias configurações.

Para configurações mais complexas usando várias estruturas de site de AEM combinadas com diferentes catálogos de comércio, consulte o tutorial [Configuração de várias lojas do Commerce](configuring/multi-store-setup.md).

## Recursos adicionais {#additional-resources}

- [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype)
- [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia)
- [Configuração de várias lojas do Commerce](configuring/multi-store-setup.md)
