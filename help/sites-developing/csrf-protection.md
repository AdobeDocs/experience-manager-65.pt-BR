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

---


# Quadro de proteção do QREF{#the-csrf-protection-framework}

Além do Filtro de referenciador Apache Sling, a Adobe também fornece uma nova Estrutura de proteção CSRF para proteção contra esse tipo de ataque.

A estrutura utiliza tokens para garantir que a solicitação do cliente seja legítima. Os tokens são gerados quando o formulário é enviado ao cliente e validado quando o formulário é enviado de volta ao servidor.

>[!NOTE]
>
>Não há tokens nas instâncias de publicação para usuários anônimos.

## Requisitos {#requirements}

### Dependências {#dependencies}

Qualquer componente que dependa da `granite.jquery` dependência se beneficiará automaticamente do CSRF Protection Framework. Se esse não for o caso de nenhum de seus componentes, você deverá declarar uma dependência para `granite.csrf.standalone` poder usar a estrutura.

### Replicação da chave de criptografia {#replicating-crypto-keys}

Para usar os tokens, é necessário replicar o `/etc/keys/hmac` binário para todas as instâncias na implantação. Uma maneira conveniente de copiar a chave HMAC para todas as instâncias é criar um pacote contendo a chave e instalá-la por meio do Gerenciador de pacotes em todas as instâncias.

>[!NOTE]
>
>Certifique-se de fazer as alterações [necessárias na configuração do](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) Dispatcher para usar a Estrutura de proteção do CSRF.

>[!NOTE]
>
>Se você usar o cache manifest com seu aplicativo da Web, certifique-se de adicionar &quot;**&amp;ast;**&quot; ao manifesto para garantir que o token não faça a chamada de geração de token CSRF off-line. Para obter mais informações, consulte este [link](https://www.w3.org/TR/offline-webapps/).
>
>Para obter mais informações sobre os ataques de CSRF e sobre como reduzi-los, consulte a página [](https://owasp.org/www-community/attacks/csrf)OWASP de Solicitações de vários sites.
