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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%
---
# Filtro de disposição de conteúdo {#content-disposition-filter}

O filtro de disposição de conteúdo é um recurso de segurança contra ataques XSS em arquivos SVG.

Depois de instalado, o filtro bloqueia o acesso a todos os ativos. Por exemplo, não era possível exibir uma PDF online. Esta seção descreve como configurar o filtro de acordo com suas necessidades.

## Configurar o filtro de disposição de conteúdo {#configure-content-disposition-filter}

Você pode exibir o [Filtro de disposição de conteúdo do Apache Sling no GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

As opções de Filtro de disposição de conteúdo oferecem a seguinte funcionalidade:

* **Caminhos de Disposição de Conteúdo:** Uma lista de caminhos em que o filtro é aplicado seguida por uma lista de tipos MIME a serem excluídos nesse caminho. Este caminho deve ser um caminho absoluto e pode conter um curinga (`*`) no final, para corresponder cada caminho de recurso com o prefixo de caminho fornecido. Por exemplo: `/content/*:image/jpeg,image/svg+xml` aplica o filtro a cada nó em `/content?`, exceto imagens JPG e SVG.

* **Caminhos de Recursos Excluídos:** Uma lista de recursos excluídos, cada caminho de recurso deve ser fornecido como um caminho absoluto e totalmente qualificado. Correspondência de prefixos/curingas não são suportados.

* **Habilitar Para Todos os Caminhos de Recursos:** Esse sinalizador controla se este filtro deve ser habilitado para todos os caminhos, exceto para os caminhos excluídos definidos pelos Caminhos de Recursos Excluídos. Definir esse sinalizador como &#39;true&#39; resulta na ignorância dos Caminhos de disposição de conteúdo. Independentemente da configuração, somente caminhos de recursos são cobertos que contenham uma propriedade chamada `jcr:data` ou `jcr:content/jcr:data`.
