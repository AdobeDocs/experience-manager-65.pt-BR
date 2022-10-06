---
title: Compatibilidade com versões anteriores no AEM 6.5
seo-title: Backward Compatibility in AEM 6.5
description: Saiba como manter seus aplicativos e configurações compatíveis com o AEM 6.5
seo-description: Learn how to keep your apps and configurations compatible with AEM 6.5
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
feature: Upgrading
exl-id: c432a014-2dab-4c49-a25b-e4f461d13f9b
source-git-commit: 50a11e30ccd720065962e8dd03cbcc71ec9f715a
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# Compatibilidade com versões anteriores no AEM 6.5{#backward-compatibility-in-aem}

## Visão geral {#overview}

>[!NOTE]
>
>Para obter uma lista de alterações de conteúdo e configuração que não estão no escopo do Pacote de Compatibilidade, consulte [Reestruturação do Repositório em AEM](/help/sites-deploying/repository-restructuring.md).

No AEM 6.5, todos os recursos foram desenvolvidos tendo em mente a compatibilidade com versões anteriores.

Na maioria dos casos, os clientes que executam o AEM 6.3 não devem precisar alterar o código ou as personalizações ao fazer a atualização. Para clientes AEM 6.1 e 6.2, não há alterações adicionais de quebra que seriam enfrentadas durante uma atualização para o 6.3.

Para exceções em que os recursos não podiam ser mantidos compatíveis com versões anteriores, os problemas de incompatibilidade com versões anteriores de pacotes e conteúdo podem ser atenuados pela instalação de um Pacote de Compatibilidade para a versão 6.4 (consulte como configurar abaixo para obter detalhes sobre onde baixar). Este pacote compat ajudará a restaurar a compatibilidade na maioria dos casos para aplicativos compatíveis com o AEM 6.4.

O Pacote de Compatibilidade permite executar AEM no modo de compatibilidade e adiar o desenvolvimento personalizado em relação aos novos recursos de AEM:

>[!NOTE]
>
>Observe que o pacote de compatibilidade é apenas uma solução temporária para adiar o desenvolvimento necessário para ser compatível com o AEM 6.5, seu recomendado somente como uma última opção se você não conseguir resolver problemas de compatibilidade por meio do desenvolvimento imediatamente após a atualização. É altamente recomendável alternar para o modo nativo e desinstalar o pacote de compatibilidade depois de decidir prosseguir com o desenvolvimento personalizado baseado no 6.5 e aproveitar a funcionalidade 6.5 completa.

![senso](assets/sase.png)

O Pacote de Compatibilidade tem dois modos: **Roteamento Habilitado** e **Roteamento Desativado**.

Isso permite que o AEM 6.5 seja executado em três modos:

**Modo nativo:**

O modo nativo é para clientes que desejam usar todos os novos recursos do AEM 6.5 e estão prontos para fazer desenvolvimento para fazer com que suas personalizações funcionem com todos os novos recursos.

Isso significa que talvez seja necessário fazer ajustes em seu aplicativo imediatamente após a atualização.

**Modo de Compatibilidade: Pacote de Compatibilidade Instalado com Roteamento Ativado**

O Modo de Compatibilidade é para clientes que têm personalizações de interfaces que não são compatíveis com versões anteriores. Isso permite que o AEM seja executado no modo de compatibilidade e adie o desenvolvimento personalizado necessário em relação aos novos recursos de AEM que não são compatíveis com alguns de seus códigos personalizados.

**Modo herdado: Pacote de Compatibilidade Instalado com Roteamento Desativado**

O modo herdado é para clientes que têm interfaces personalizadas baseadas em código herdado ou obsoleto do AEM que foi movido para fora no pacote de compatibilidade.

![safra](assets/sapte.png)

## Como configurar {#how-to-set-up}

O **AEM 6.4 Pacote de compatibilidade para 6.5** pode ser instalado como um pacote usando o Gerenciador de pacotes. Você pode baixar o [AEM 6.4 Pacote de compatibilidade para 6.5 da Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64) site.

Quando o Pacote de Compatibilidade estiver instalado, o roteamento poderá ser ativado ou desativado usando um switch na configuração OSGI, conforme mostrado abaixo:

![Comutadores Compat](assets/compat-switches.png)

Quando o Pacote de Compatibilidade estiver instalado e configurado, os recursos serão usados com base no modo de compatibilidade que foi escolhido.
