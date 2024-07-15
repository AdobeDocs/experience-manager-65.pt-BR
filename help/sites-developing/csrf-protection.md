---
title: A estrutura de proteção CSRF
description: A estrutura usa tokens para garantir que a solicitação do cliente seja legítima
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '235'
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

Qualquer componente que depende da dependência `granite.jquery` pode se beneficiar automaticamente da Estrutura de proteção CSRF. Caso contrário, para qualquer um de seus componentes, você deve declarar uma dependência para `granite.csrf.standalone` antes de poder usar a estrutura.

### Replicação da chave de criptografia {#replicating-crypto-keys}

Para usar os tokens, é necessário replicar o binário HMAC para todas as instâncias em sua implantação. Consulte [Replicando a chave HMAC](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key) para obter mais detalhes.

>[!NOTE]
>
>Certifique-se também de fazer as [alterações necessárias na configuração do Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) para usar a Estrutura de Proteção CSRF.

>[!NOTE]
>
>Se você usar o cache manifest com seu aplicativo web, adicione &quot;**&amp;ast;**&quot; ao manifesto para garantir que o token não coloque a chamada de geração de token CSRF offline. Para obter mais informações, consulte este [link](https://www.w3.org/TR/offline-webapps/).
>
Para obter mais informações sobre ataques CSRF e maneiras de atenuá-los, consulte a [página OWASP de falsificação de solicitação entre sites](https://owasp.org/www-community/attacks/csrf).
