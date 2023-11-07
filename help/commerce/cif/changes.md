---
title: Alterações importantes do complemento Commerce integration framework (CIF)
description: Alterações notáveis do add-on do Commerce integration framework (CIF) em comparação com versões antigas do CIF.
exl-id: 41dee21a-9ae2-4067-a32a-2d4633323fc4
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 1%

---

# Alterações importantes no complemento Commerce integration framework (CIF){#notable-changes}

Este documento destaca as importantes diferenças entre o complemento Commerce integration framework (CIF) e as versões antigas do CIF CIF CIF, conhecidas principalmente como Classic (Quickstart) e Open-source.

## Instalação e atualizações

O pacote complementar CIF AEM é instalado e atualizado com o Gerenciador de pacotes AEM.

**Versões anteriores do CIF**

* CIF Classic: Nenhuma instalação necessária, CIF foi parte do Quickstart. As atualizações do CIF faziam parte das atualizações regulares do AEM ou do service pack
* CIF Open-source: instalação via GitHub. As atualizações faziam parte do trabalho manual de atualização/manutenção.

## Configuração do endpoint

O endpoint é configurado por meio do console OSGi.

**Versões anteriores do CIF**

* CIF Classic: por meio da configuração OSGi no AEM
* CIF Open-source: por meio do navegador de configuração CIF

## Implantação do projeto CIF Venia

Projeto disponível em [Guias do GitHub AEM - Projeto CIF Venia](https://github.com/adobe/aem-cif-guides-venia) e implantação feitas pelo Gerenciador de pacotes AEM.

**Versões anteriores do CIF**

* CIF Classic: por meio da instalação do pacote AEM

## Dados do catálogo de produtos

Os dados do catálogo de produtos são solicitados sob demanda por meio de chamadas em tempo real para um endpoint externo que oferece suporte às APIs necessárias do GraphQL. Essas APIs oferecem suporte ao acesso a dados dinâmicos ou em estágios em qualquer data. Nenhuma replicação necessária.

**Versões anteriores do CIF**

* CIF Classic: dados de produtos ao vivo e preparados são importados e mantidos no JCR no AEM Author por meio de importação completa ou delta de produtos. Os dados de produtos em tempo real são replicados para publicação no AEM.

## Experiências do catálogo de produtos com renderização por AEM

O AEM renderiza experiências de catálogo de produtos dinamicamente usando modelos de catálogo de AEM que foram atribuídos a produtos e categorias. Nenhuma replicação necessária.

**Versões anteriores do CIF**

* CIF Classic: AEM Author cria uma página do AEM para cada categoria/produto usando a ferramenta de blueprint do catálogo. Essas páginas são replicadas para AEM Publish.

>[!NOTE]
>
>Para obter a documentação adicional sobre como usar o CIF com AEM Managed Service ou AEM no local, consulte [Commerce integration framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
