---
title: A estrutura de proteção CSRF
description: A estrutura usa tokens para garantir que a solicitação do cliente seja legítima
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# A estrutura de proteção CSRF{#the-csrf-protection-framework}

Além do Filtro referenciador Apache Sling, o Adobe também fornece uma nova Estrutura de proteção CSRF para proteger contra esse tipo de ataque.

A estrutura usa tokens para garantir que a solicitação do cliente seja legítima. Os tokens são gerados quando o formulário é enviado ao cliente e validado quando o formulário é enviado de volta ao servidor.

>[!NOTE]
>
>Não há tokens nas instâncias de publicação para usuários anônimos.

## Requisitos {#requirements}

### Dependências {#dependencies}

Qualquer componente que dependa da variável `granite.jquery` A dependência se beneficiará automaticamente da Estrutura de proteção CSRF. Se esse não for o caso de nenhum de seus componentes, você deve declarar uma dependência para `granite.csrf.standalone` antes de usar a estrutura.

### Replicação da chave de criptografia {#replicating-crypto-keys}

Para usar os tokens, é necessário replicar o binário HMAC para todas as instâncias em sua implantação. Consulte [Replicação da chave HMAC](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key) para obter mais detalhes.

>[!NOTE]
>
>Certifique-se também de fazer o necessário [Alterações na configuração do Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) para usar a Estrutura de proteção CSRF.

>[!NOTE]
>
>Se você usar o cache manifest com seu aplicativo web, certifique-se de adicionar &quot;**&amp;ast;**&quot; ao manifesto para garantir que o token não coloque a chamada de geração de token CSRF offline. Para obter mais informações, consulte este [link](https://www.w3.org/TR/offline-webapps/).
>
>Para obter mais informações sobre ataques CSRF e maneiras de atenuá-los, consulte a [Página OWASP de falsificação de solicitação entre sites](https://owasp.org/www-community/attacks/csrf).
