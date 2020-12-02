---
title: Quadro de proteção do QREF
seo-title: Quadro de proteção do QREF
description: A estrutura utiliza tokens para garantir que a solicitação do cliente seja legítima
seo-description: A estrutura utiliza tokens para garantir que a solicitação do cliente seja legítima
uuid: 7cb222ba-fc7a-46ee-8b49-a5f39a53580b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f453427d-c813-48b7-b2f9-adadea39c67d
translation-type: tm+mt
source-git-commit: c83c77c5c313099944dd73c8cbe63d429d84a518
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# A Estrutura de Proteção CSRF{#the-csrf-protection-framework}

Além do Filtro de Quem indicou Apache Sling, o Adobe também oferece uma nova Estrutura de Proteção CSRF para proteção contra esse tipo de ataque.

A estrutura utiliza tokens para garantir que a solicitação do cliente seja legítima. Os tokens são gerados quando o formulário é enviado ao cliente e validado quando o formulário é enviado de volta ao servidor.

>[!NOTE]
>
>Não há tokens nas instâncias de publicação para usuários anônimos.

## Requisitos {#requirements}

### Dependências {#dependencies}

Qualquer componente que dependa da dependência `granite.jquery` se beneficiará automaticamente da Estrutura de Proteção do CSRF. Se esse não for o caso de nenhum de seus componentes, você deverá declarar uma dependência de `granite.csrf.standalone` antes de poder usar a estrutura.

### Replicando a chave de criptografia {#replicating-crypto-keys}

Para usar os tokens, é necessário replicar o binário `/etc/keys/hmac` para todas as instâncias na implantação. Uma maneira conveniente de copiar a chave HMAC para todas as instâncias é criar um pacote contendo a chave e instalá-la por meio do Gerenciador de pacotes em todas as instâncias.

>[!NOTE]
>
>Certifique-se de fazer as [alterações de configuração do Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) necessárias para usar a Estrutura de Proteção do CSRF.

>[!NOTE]
>
>Se você usar o cache manifest com seu aplicativo da Web, certifique-se de adicionar &quot;**&amp;ast;**&quot; ao manifesto para garantir que o token não faça a chamada de geração de token CSRF off-line. Para obter mais informações, consulte este [link](https://www.w3.org/TR/offline-webapps/).
>
>Para obter mais informações sobre ataques CSRF e maneiras de reduzi-los, consulte a [página OWASP de informações sobre falsificações entre sites](https://owasp.org/www-community/attacks/csrf).
