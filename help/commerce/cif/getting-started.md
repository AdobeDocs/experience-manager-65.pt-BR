---
title: Introdução ao conteúdo e comércio AEM
description: Saiba como implantar um projeto de Conteúdo e Comércio AEM.
topics: Commerce
feature: Commerce Integration Framework
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
source-git-commit: a467009851937c4a10b165a3d253c47bf990bbc5
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 6%

---

# Introdução ao conteúdo e comércio AEM {#start}

Para começar a usar AEM Content and Commerce, é necessário instalar o AEM Content and Commerce Add-On for AEM 6.5.

## Requisito mínimo de software

[AEM 6.5 Service Pack](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html) 7 ou posterior é necessário.

## Integração {#onboarding}

A integração do conteúdo e do comércio AEM é um processo de duas etapas:

1. Instale o complemento Conteúdo AEM e Commerce para o AEM 6.5

2. Conectar AEM com sua solução comercial

### Instale o complemento Conteúdo AEM e Commerce para o AEM 6.5 {#install-add-on}

Baixe e instale o AEM Commerce Add-On para AEM 6.5 no [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) portal.

Inicie e instale o AEM 6.5 Service Pack necessário. Recomendamos instalar o último service pack disponível.

>[!NOTE]
>
>Isso será feito pelo CSE para AEM clientes do Managed Service.

### Conecte AEM ao seu sistema de comércio {#connect}

AEM pode ser conectado a qualquer sistema de comércio que tenha um ponto de extremidade GraphQL acessível para AEM. Normalmente, esses pontos de extremidade estão disponíveis publicamente ou podem ser conectados via VPN privada ou conexões locais, dependendo da configuração individual do projeto.

Opcionalmente, é possível fornecer o cabeçalho de autenticação para usar recursos adicionais da CIF que exigem autenticação.

Projetos gerados pela [Arquétipo de projeto AEM](https://github.com/adobe/aem-project-archetype)e o [Loja de referência Venia AEM](https://github.com/adobe/aem-cif-guides-venia) que já está incluída no [configuração padrão](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) deve ser ajustado.

Substitua o valor da variável `url` em `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` com o ponto de extremidade GraphQL do sistema de comércio. Essa configuração pode ser feita por meio do console OSGI ou da implantação da configuração OSGI por meio do projeto. Diferentes configurações para sistemas de armazenamento temporário e de produção são suportadas usando diferentes modos de execução de AEM.

Os Componentes principais do AEM Content and Commerce e da CIF usam conexões AEM lado do servidor e do cliente. Os Componentes principais da CIF do lado do cliente e as ferramentas de criação do complemento CIF se conectam por padrão ao `/api/graphql`. Isso pode ser ajustado através da configuração do Cloud Service da CIF, se necessário (veja abaixo).

O complemento CIF fornece um servlet proxy GraphQL em `/api/graphql` que podem, opcionalmente, ser utilizadas para [desenvolvimento local](develop.md). Para implantações de produção, é altamente recomendável configurar um proxy reverso para o ponto de extremidade GraphQL de comércio por meio do Dispatcher AEM ou em outras camadas de rede (como CDN).

## Configuração de lojas e catálogos {#catalog}

O complemento e o [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components) pode ser usado em várias estruturas de site AEM conectadas a diferentes lojas de comércio (ou visualizações de loja, e assim por diante). Por padrão, o complemento CIF é implantado com uma configuração padrão que se conecta à loja e ao catálogo padrão da Adobe Commerce.

Essa configuração pode ser ajustada para o projeto por meio da configuração do Cloud Service da CIF, seguindo estas etapas:

1. AEM acesse Ferramentas -> Cloud Services -> Configuração da CIF

2. Selecione a configuração de comércio que deseja alterar

3. Abra as propriedades de configuração na barra de ações

![Configuração do CIF Cloud Services](/help/commerce/cif/assets/cif-cloud-service-config.png)

As seguintes propriedades podem ser configuradas:

- Cliente GraphQL - selecione o cliente GraphQL configurado para comunicação de back-end de comércio. Normalmente, isso deve permanecer no padrão.
- Exibição da loja - o identificador de exibição da loja. Se estiver vazia, a exibição de loja padrão será usada.
- Caminho do proxy GraphQL - o caminho do URL Proxy GraphQL no AEM usado para solicitações de proxy no ponto de extremidade GraphQL de back-end do comércio.
   >[!NOTE]
   >
   > Na maioria das configurações, o valor padrão `/api/graphql` não deve ser alterado. Somente a configuração avançada que não usa o proxy GraphQL fornecido deve alterar essa configuração.
- Ativar o suporte à UID do catálogo - ative o suporte para UID em vez da ID nas chamadas GraphQL de back-end de comércio.
   >[!NOTE]
   >
   > O suporte para UIDs foi introduzido no Adobe Commerce 2.4.2. Habilite-o somente se o back-end de comércio suportar um esquema GraphQL da versão 2.4.2 ou posterior.
- Identificador de categoria raiz do catálogo - o identificador (UID ou ID) da raiz do catálogo de loja
   >[!CAUTION]
   >
   > A partir da versão 2.0.0 dos Componentes principais da CIF, o suporte para o `id` foi removido e substituído por `uid`. Se o seu projeto usa a versão 2.0.0 dos Componentes principais da CIF, você deve ativar o Suporte à UID de catálogo e usar uma UID de categoria válida como &quot;Identificador de categoria raiz do catálogo&quot;.

A configuração mostrada acima é para referência. Os projetos devem fornecer suas próprias configurações.

Para configurações mais complexas usando várias estruturas de site de AEM combinadas com catálogos de comércio diferentes, consulte o [Configuração de várias lojas do Commerce](configuring/multi-store-setup.md) tutorial.

## Recursos adicionais {#additional-resources}

- [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype)
- [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia)
- [Configuração de várias lojas do Commerce](configuring/multi-store-setup.md)
