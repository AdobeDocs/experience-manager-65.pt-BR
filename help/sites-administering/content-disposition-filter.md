---
title: Filtro de disposição de conteúdo
description: Saiba como usar o Filtro de disposição de conteúdo para impedir ataques XSS.
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Filtro de disposição de conteúdo {#content-disposition-filter}

O filtro de disposição de conteúdo é um recurso de segurança contra ataques XSS em arquivos SVG.

Depois de instalado, o filtro bloqueia o acesso a todos os ativos. Por exemplo, não é possível exibir um PDF online. Esta seção descreve como configurar o filtro de acordo com suas necessidades.

## Configurar o filtro de disposição de conteúdo {#configure-content-disposition-filter}

Você pode exibir o [Filtro de disposição de conteúdo do Apache Sling no GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

As opções de Filtro de disposição de conteúdo oferecem a seguinte funcionalidade:

* **Caminhos de Disposição de Conteúdo:** Uma lista de caminhos em que o filtro é aplicado seguida por uma lista de tipos MIME a serem excluídos nesse caminho. Este caminho deve ser um caminho absoluto e pode conter um curinga (`*`) no final, para corresponder cada caminho de recurso com o prefixo de caminho fornecido. Por exemplo: `/content/*:image/jpeg,image/svg+xml` aplica o filtro a todos os nós em `/content?`, exceto imagens de SVG e JPG.

* **Caminhos de Recursos Excluídos:** Uma lista de recursos excluídos, cada caminho de recurso deve ser fornecido como um caminho absoluto e totalmente qualificado. Correspondência de prefixos/curingas não são suportados.

* **Habilitar Para Todos os Caminhos de Recursos:** Esse sinalizador controla se este filtro deve ser habilitado para todos os caminhos, exceto para os caminhos excluídos definidos pelos Caminhos de Recursos Excluídos. Definir esse sinalizador como &#39;true&#39; resulta na ignorância dos Caminhos de disposição de conteúdo. Independentemente da configuração, somente caminhos de recursos são cobertos que contenham uma propriedade chamada `jcr:data` ou `jcr:content/jcr:data`.
