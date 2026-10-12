---
title: Alterações importantes do complemento Commerce integration framework (CIF)
description: Alterações importantes do complemento do Commerce integration framework (CIF) em comparação com versões antigas do CIF.
exl-id: 41dee21a-9ae2-4067-a32a-2d4633323fc4
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%
---
# Alterações importantes no complemento do Commerce integration framework (CIF){#notable-changes}

Este documento destaca as diferenças importantes entre o complemento Commerce integration framework (CIF) e as versões antigas do CIF, conhecidas principalmente como CIF Classic (Quickstart) e CIF Open-Source.

## Instalação e atualizações

O pacote complementar do AEM CIF é instalado e atualizado com o AEM Package Manager.

**Versões anteriores do CIF**

* CIF Classic: nenhuma instalação necessária, o CIF fazia parte do Quickstart. As atualizações do CIF faziam parte das atualizações regulares do AEM ou de service packs
* CIF Open-source: instalação via GitHub. As atualizações faziam parte do trabalho manual de atualização/manutenção.

## Configuração do endpoint

O endpoint é configurado por meio do console OSGi.

**Versões anteriores do CIF**

* CIF Classic: por meio da configuração do OSGi no AEM
* Código aberto do CIF: por meio do navegador de configuração do CIF

## Implantação do projeto CIF Venia

Projeto disponível em [GitHub AEM Guides - CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) e implantação feita pelo Gerenciador de Pacotes do AEM.

**Versões anteriores do CIF**

* CIF Classic: por meio da instalação do pacote do AEM

## Dados do catálogo de produtos

Os dados do catálogo de produtos são solicitados sob demanda por meio de chamadas em tempo real para um endpoint externo que oferece suporte às APIs necessárias do GraphQL. Essas APIs oferecem suporte ao acesso a dados dinâmicos ou em estágios em qualquer data. Nenhuma replicação necessária.

**Versões anteriores do CIF**

* CIF Classic: dados de produtos ao vivo e em preparo são importados e mantidos em JCR no AEM Author por meio de importação completa ou delta de produtos. Os dados do produto em tempo real são replicados para a publicação do AEM.

## Experiências do catálogo de produtos com renderização do AEM

O AEM renderiza experiências de catálogo de produtos dinamicamente usando modelos de catálogo do AEM que foram atribuídos a produtos e categorias. Nenhuma replicação necessária.

**Versões anteriores do CIF**

* CIF Classic: o AEM Author cria uma página do AEM para cada categoria/produto usando a ferramenta de blueprint do catálogo. Essas páginas são replicadas para o AEM Publish.

>[!NOTE]
>
>Para obter a documentação adicional sobre como usar o CIF com o AEM Managed Service ou o AEM no local, consulte [Commerce integration framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
