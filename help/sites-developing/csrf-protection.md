---
title: Quadro de proteção do QREF
seo-title: The CSRF Protection Framework
description: A estrutura usa tokens para garantir que a solicitação do cliente seja legítima
seo-description: The framework makes use of tokens to guarantee that the client request is legitimate
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
exl-id: e6b0f8f7-54b0-4dd6-86ad-5516954c6d90
source-git-commit: f841e3886771fb00eee6e476d7111d4a335a9d51
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Quadro de proteção do QREF{#the-csrf-protection-framework}

Além do Apache Sling Referrer Filter, o Adobe também fornece uma nova Estrutura de Proteção do CSRF para proteger contra esse tipo de ataque.

A estrutura usa tokens para garantir que a solicitação do cliente seja legítima. Os tokens são gerados quando o formulário é enviado ao cliente e validado quando o formulário é enviado de volta ao servidor.

>[!NOTE]
>
>Não há tokens nas instâncias de publicação para usuários anônimos.

## Requisitos {#requirements}

### Dependências {#dependencies}

Qualquer componente que dependa do `granite.jquery` a dependência se beneficiará automaticamente do CSRF Protection Framework. Se esse não for o caso de nenhum de seus componentes, você deve declarar uma dependência para `granite.csrf.standalone` antes de poder usar a estrutura.

### Replicação da chave de criptografia {#replicating-crypto-keys}

Para usar os tokens, é necessário replicar o binário do HMAC para todas as instâncias na implantação. Consulte [Replicação da chave HMAC](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key) para obter mais detalhes.

>[!NOTE]
>
>Certifique-se também de [Alterações na configuração do Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) a fim de utilizar o Quadro de Proteção do QREF.

>[!NOTE]
>
>Se você usar o cache de manifesto com seu aplicativo da Web, adicione &quot;**&amp;ast;**&quot; ao manifesto para garantir que o token não coloque a chamada de geração de token CSRF offline. Para obter mais informações, consulte esta seção [link](https://www.w3.org/TR/offline-webapps/).
>
>Para obter mais informações sobre ataques de CSRF e maneiras de atenuá-los, consulte o [Página OWASP de falsificação de solicitação entre sites](https://owasp.org/www-community/attacks/csrf).
