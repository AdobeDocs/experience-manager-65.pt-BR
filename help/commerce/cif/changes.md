---
title: Alterações importantes do complemento Commerce Integration Framework (CIF)
description: Alterações importantes do complemento Commerce Integration Framework (CIF) em comparação às versões antigas da CIF.
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
source-git-commit: 78359fb8ecbcc0227ab5a3910175aed73d823902
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# Alterações importantes no complemento Commerce Integration Framework (CIF){#notable-changes}

Este documento destaca as importantes diferenças entre o complemento Commerce Integration Framework (CIF) e as versões antigas da CIF, principalmente conhecidas como CIF clássica (início rápido) e CIF fonte aberta.

## Instalação e atualizações

O pacote complementar da CIF do AEM é instalado e atualizado com AEM Gerenciador de pacotes.

**Versões anteriores da CIF**

* CIF Classic: Sem a necessidade de instalação, a CIF fazia parte do Início rápido. As atualizações da CIF faziam parte de atualizações regulares de AEM ou service pack
* Código aberto da CIF: Instalação via GitHub. As atualizações faziam parte do trabalho manual de atualização/manutenção.

## Configuração do ponto de extremidade

O terminal é configurado pelo console OSGi.

**Versões anteriores da CIF**

* CIF Classic: Por meio da configuração OSGi no AEM
* Código aberto da CIF: Por meio do navegador de configuração da CIF

## Implantação do projeto CIF Venia

Projeto disponível em [Guias de AEM do GitHub - Projeto CIF Venia](https://github.com/adobe/aem-cif-guides-venia) e implantação feita pelo Gerenciador de pacotes AEM.

**Versões anteriores da CIF**

* CIF Classic: Via instalação AEM pacote

## Dados do catálogo de produtos

Os dados do catálogo de produtos são solicitados sob demanda por meio de chamadas em tempo real para um endpoint externo que oferece suporte às APIs GraphQL necessárias. Essas APIs oferecem suporte para o acesso a dados ao vivo ou preparados em qualquer data específica. Não é necessária replicação.

**Versões anteriores da CIF**

* CIF Classic: Os dados de produtos em tempo real e preparados são importados e mantidos no JCR no AEM Author por meio de importação completa ou delta de produtos. Os dados do produto em tempo real são replicados para o AEM Publish.

## Experiências do catálogo de produtos com renderização de AEM

AEM renderiza experiências de catálogo de produtos dinamicamente usando modelos de catálogo AEM que foram atribuídos a produtos e categorias. Não é necessária replicação.

**Versões anteriores da CIF**

* CIF Classic: O AEM Author cria uma página de AEM para cada categoria/produto usando a ferramenta de blueprint do catálogo. Essas páginas são replicadas para o AEM Publish.

>[!NOTE]
>
>Para obter a documentação adicional sobre como usar a CIF com AEM Managed Service ou AEM no local, consulte [Estrutura de integração de comércio](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
