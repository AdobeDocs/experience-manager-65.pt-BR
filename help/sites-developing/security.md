---
title: Segurança
seo-title: Security
description: A segurança do aplicativo é iniciada durante a fase de desenvolvimento
seo-description: Application Security starts during the development phase
uuid: efd5f3bc-da07-4fc8-a6ce-f1e6f5084c9e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: d2267663-6c1d-413c-9862-e82e21ae6906
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Segurança{#security}

A segurança do aplicativo é iniciada durante a fase de desenvolvimento. O Adobe recomenda aplicar as seguintes práticas recomendadas de segurança.

## Usar sessão de solicitação {#use-request-session}

Seguindo o princípio de menos privilégios, o Adobe recomenda que cada acesso ao repositório seja feito usando a sessão vinculada à solicitação do usuário e o controle de acesso apropriado.

## Protect contra script entre sites (XSS) {#protect-against-cross-site-scripting-xss}

O cross-site scripting (XSS) permite que invasores injetem código em páginas da Web visualizadas por outros usuários. Essa vulnerabilidade de segurança pode ser explorada por usuários maliciosos da Web para ignorar controles de acesso.

AEM aplica o princípio de filtrar todo o conteúdo fornecido pelo usuário na saída. A prevenção do XSS recebe a prioridade mais alta durante o desenvolvimento e o teste.

O mecanismo de proteção XSS fornecido pela AEM baseia-se no [Biblioteca Java AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) , [OWASP (Projeto de Segurança de Aplicativo Web Aberto)](https://www.owasp.org/). A configuração padrão do AntiSamy pode ser encontrada em

`/libs/cq/xssprotection/config.xml`

É importante adaptar essa configuração às suas próprias necessidades de segurança ao sobrepor o arquivo de configuração. O funcionário [Documentação do AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) O fornecerá todas as informações necessárias para implementar seus requisitos de segurança.

>[!NOTE]
>
>Recomendamos que você sempre acesse a API de proteção do XSS usando o [XSSAPI fornecida pelo AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

Além disso, um firewall de aplicativo Web, como [mod_security para Apache](https://www.modsecurity.org)O pode fornecer controle central e confiável sobre a segurança do ambiente de implantação e proteção contra ataques de script entre sites não detectados anteriormente.

## Acesso às informações do Cloud Service {#access-to-cloud-service-information}

>[!NOTE]
>
>As ACLs para as Informações do Cloud Service, bem como as configurações OSGi necessárias para proteger sua instância são automatizadas como parte do [Modo Pronto para produção](/help/sites-administering/production-ready.md). Embora isso signifique que não é necessário fazer as alterações de configuração manualmente, ainda é recomendável revisá-las antes de entrar em vigor com a implantação.

Quando você [integre sua instância do AEM à Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md) você usa [Configurações do Cloud Service](/help/sites-developing/extending-cloud-config.md). As informações sobre essas configurações, juntamente com qualquer estatística coletada, são armazenadas no repositório. Recomendamos que, se estiver usando essa funcionalidade, você verifique se a segurança padrão nessas informações corresponde aos seus requisitos.

O módulo webservicesupport grava estatísticas e informações de configuração em:

`/etc/cloudservices`

Com as permissões padrão:

* Ambiente do autor: `read` para `contributors`

* Ambiente de publicação: `read` para `everyone`

## Protect contra ataques de falsificação de solicitação entre sites {#protect-against-cross-site-request-forgery-attacks}

Para obter mais informações sobre os mecanismos de segurança AEM empregados para mitigar ataques de CSRF, consulte o [Filtro de referenciador do Sling](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) seção da lista de verificação de segurança e do [Documentação do Quadro de proteção CSRF](/help/sites-developing/csrf-protection.md).
