---
title: Introdução ao conteúdo e comércio de AEM
description: Saiba como implantar um projeto de conteúdo e comércio do AEM.
topics: Commerce
feature: Commerce Integration Framework
exl-id: 92b964f8-6672-4f76-8a9f-5782c3ceb83f
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 6%

---

# Introdução ao conteúdo e comércio de AEM {#start}

Para começar a usar o AEM Content and Commerce, é necessário instalar o AEM Content and Commerce Add-On para AEM 6.5.

## Requisito mínimo de software

[Pacote de serviços do AEM 6.5](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html) 7 ou posterior é obrigatório.

## Integração {#onboarding}

A integração de conteúdo e comércio do AEM é um processo de duas etapas:

1. Instalar o complemento de conteúdo e comércio do AEM para AEM 6.5

2. Conectar o AEM à sua solução comercial

### Instalar o complemento de conteúdo e comércio do AEM para AEM 6.5 {#install-add-on}

Baixe e instale o complemento AEM Commerce para AEM 6.5 da [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html) portal.

Inicie e instale o AEM 6.5 Service Pack necessário. Recomendamos instalar o último service pack disponível.

>[!NOTE]
>
>Isso será feito pelo CSE para clientes do AEM Managed Service.

### Conectar o AEM ao seu sistema do Commerce {#connect}

O AEM pode ser conectado a qualquer sistema comercial que tenha um terminal GraphQL acessível para AEM. Esses endpoints geralmente estão disponíveis publicamente ou podem ser conectados por VPN privada ou conexões locais, dependendo da configuração individual do projeto.

Como opção, o cabeçalho de autenticação pode ser fornecido para usar recursos CIF adicionais que exigem autenticação.

Projetos gerados pelo [Arquétipo de projeto AEM](https://github.com/adobe/aem-project-archetype), e o [Loja de referência AEM Venia](https://github.com/adobe/aem-cif-guides-venia) que já está incluído na lista [configuração padrão](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json) deve ser ajustado.

Substitua o valor de `url` in `com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` com o terminal GraphQL do seu sistema de comércio. Essa configuração pode ser feita por meio do console OSGI ou implantando a configuração OSGI por meio do projeto. Diferentes configurações para sistemas de preparo e produção são compatíveis com o uso de diferentes modos de execução do AEM.

O complemento de conteúdo e comércio para AEM e os componentes principais da CIF usam conexões AEM do lado do servidor e do lado do cliente. Os Componentes principais da CIF do lado do cliente e as ferramentas de criação do complemento CIF se conectam por padrão a `/api/graphql`. Isso pode ser ajustado por meio da configuração do Cloud Service da CIF, se necessário (veja abaixo).

O complemento CIF fornece um servlet proxy do GraphQL em `/api/graphql` que podem ser usados opcionalmente para [desenvolvimento local](develop.md). Para implantações de produção, é altamente recomendável configurar um proxy reverso para o endpoint do GraphQL de comércio por meio do AEM Dispatcher ou em outras camadas de rede (como o CDN).

## Configurando lojas e catálogos {#catalog}

O Complemento e o [Componentes principais da CIF](https://github.com/adobe/aem-core-cif-components) pode ser usado em várias estruturas de site de AEM conectadas a diferentes lojas de comércio (ou visualizações de loja e assim por diante). Por padrão, o complemento CIF é implantado com uma configuração padrão conectada ao armazenamento e catálogo padrão da Adobe Commerce.

Essa configuração pode ser ajustada para o projeto por meio da configuração de Cloud Service da CIF seguindo estas etapas:

1. No AEM, acesse Ferramentas -> Cloud Services -> Configuração da CIF

2. Selecione a configuração de comércio que deseja alterar

3. Abrir as propriedades de configuração por meio da barra de ações

![Configuração de Cloud Services da CIF](/help/commerce/cif/assets/cif-cloud-service-config.png)

As seguintes propriedades podem ser configuradas:

- Cliente GraphQL - selecione o cliente GraphQL configurado para comunicação de back-end de comércio. Normalmente, isso deve permanecer no padrão.
- Exibição de loja - o identificador de exibição de loja. Se estiver vazia, a visualização de loja padrão será usada.
- Caminho de proxy do GraphQL - o caminho de URL que o proxy do GraphQL no AEM usa para solicitações de proxy para o endpoint do GraphQL de back-end de comércio.

   >[!NOTE]
   >
   >Na maioria das configurações, o valor padrão é `/api/graphql` não deve ser alterado. Somente a configuração avançada que não usa o proxy do GraphQL fornecido deve alterar essa configuração.

- Habilitar suporte a UID do catálogo - habilite o suporte para UID em vez de ID nas chamadas de GraphQL de back-end de comércio.

   >[!NOTE]
   >
   >O suporte para UIDs foi introduzido no Adobe Commerce 2.4.2. Habilite isso somente se o back-end de comércio suportar um esquema do GraphQL versão 2.4.2 ou posterior.

- Identificador de categoria raiz do catálogo - o identificador (UID ou ID) da raiz do catálogo de armazenamento

   >[!CAUTION]
   >
   >A partir da versão 2.0.0 dos Componentes principais da CIF, o suporte para `id` foi removido e substituído por `uid`. Se o projeto usar os Componentes principais da CIF versão 2.0.0, você deverá ativar o Suporte à UID do catálogo e usar uma UID de categoria válida como &quot;Identificador de categoria raiz do catálogo&quot;.

A configuração mostrada acima serve como referência. Os projetos devem fornecer suas próprias configurações.

Para configurações mais complexas usando várias estruturas de site AEM combinadas com diferentes catálogos de comércio, consulte a [Configuração de várias lojas do Commerce](configuring/multi-store-setup.md) tutorial.

## Recursos adicionais {#additional-resources}

- [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype)
- [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia)
- [Configuração de várias lojas do Commerce](configuring/multi-store-setup.md)
