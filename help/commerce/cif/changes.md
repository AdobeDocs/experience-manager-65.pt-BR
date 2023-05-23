---
title: Alterações importantes do complemento Commerce Integration Framework (CIF)
description: Alterações importantes do complemento Commerce Integration Framework (CIF) em comparação às versões antigas da CIF.
exl-id: 41dee21a-9ae2-4067-a32a-2d4633323fc4
source-git-commit: a2ababa9dd9115e963b91a7271d204d287557c40
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# Alterações importantes no complemento Commerce Integration Framework (CIF){#notable-changes}

Este documento destaca as diferenças importantes entre o complemento Commerce Integration Framework (CIF) e as versões antigas da CIF, conhecidas principalmente como CIF Classic (Quickstart) e CIF Open-source.

## Instalação e atualizações

O pacote complementar CIF para AEM é instalado e atualizado com o Gerenciador de pacotes AEM.

**Versões anteriores da CIF**

* CIF clássica: não é necessária nenhuma instalação. A CIF fazia parte do Quickstart. As atualizações da CIF faziam parte das atualizações regulares do AEM ou do service pack
* Código aberto da CIF: instalação via GitHub. As atualizações faziam parte do trabalho manual de atualização/manutenção.

## Configuração do endpoint

O endpoint é configurado por meio do console OSGi.

**Versões anteriores da CIF**

* CIF clássica: por meio da configuração OSGi no AEM
* Código aberto da CIF: por meio do navegador de configuração da CIF

## Implantação do projeto CIF Venia

Projeto disponível em [Guias do GitHub AEM - Projeto CIF Venia](https://github.com/adobe/aem-cif-guides-venia) e implantação feitas pelo Gerenciador de pacotes AEM.

**Versões anteriores da CIF**

* CIF Classic: Instalação do pacote por AEM

## Dados do catálogo de produtos

Os dados do catálogo de produtos são solicitados sob demanda por meio de chamadas em tempo real para um endpoint externo que oferece suporte às APIs necessárias do GraphQL. Essas APIs oferecem suporte ao acesso a dados dinâmicos ou em estágios em qualquer data. Nenhuma replicação necessária.

**Versões anteriores da CIF**

* CIF Clássico: dados de produtos em tempo real e em etapas são importados e mantidos em JCR no AEM Author por meio de uma importação completa ou delta de produtos. Os dados de produtos em tempo real são replicados para a publicação do AEM.

## Experiências do catálogo de produtos com renderização por AEM

O AEM renderiza experiências de catálogo de produtos dinamicamente usando modelos de catálogo de AEM que foram atribuídos a produtos e categorias. Nenhuma replicação necessária.

**Versões anteriores da CIF**

* CIF Clássica: o AEM Author cria uma página de AEM para cada categoria/produto usando a ferramenta de blueprint do catálogo. Essas páginas são replicadas para o AEM Publish.

>[!NOTE]
>
>Para obter a documentação adicional sobre como usar a CIF com AEM Managed Service ou AEM no local, consulte [Estrutura de integração do Commerce](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
