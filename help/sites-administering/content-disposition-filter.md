---
title: Filtro de disposição de conteúdo
description: Saiba como usar o Filtro de disposição de conteúdo para impedir ataques XSS.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# Filtro de disposição de conteúdo {#content-disposition-filter}

O filtro de disposição de conteúdo é um recurso de segurança contra ataques XSS em arquivos SVG.

Depois de instalado, o filtro bloqueia o acesso a todos os ativos. Por exemplo, não é possível exibir um PDF online. Esta seção descreve como configurar o filtro de acordo com suas necessidades.

## Configurar o filtro de disposição de conteúdo {#configure-content-disposition-filter}

É possível exibir a [Filtro de disposição de conteúdo Apache Sling no GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

As opções de Filtro de disposição de conteúdo oferecem a seguinte funcionalidade:

* **Caminhos de disposição do conteúdo:** Uma lista de caminhos em que o filtro é aplicado seguida por uma lista de tipos MIME a serem excluídos nesse caminho. Este caminho deve ser absoluto e pode conter um curinga (`*`) no final, para corresponder cada caminho de recurso ao prefixo de caminho fornecido. Por exemplo: `/content/*:image/jpeg,image/svg+xml` aplica o filtro a cada nó em `/content?` exceto imagens de JPG e SVG.

* **Caminhos de recursos excluídos:** Uma lista de recursos excluídos, cada caminho de recurso deve ser fornecido como um caminho absoluto e totalmente qualificado. Correspondência de prefixos/curingas não são suportados.

* **Ativar Para Todos Os Caminhos De Recursos:** Esse sinalizador controla se esse filtro deve ser habilitado para todos os caminhos, exceto para os caminhos excluídos definidos pelos Caminhos de recursos excluídos. Definir esse sinalizador como &#39;true&#39; resulta na ignorância dos Caminhos de disposição de conteúdo. Independentemente da configuração, somente os caminhos de recursos são cobertos que contêm uma propriedade chamada `jcr:data` ou `jcr:content/jcr:data`.
