---
title: Segurança
seo-title: Security
description: A segurança de aplicativos começa durante a fase de desenvolvimento
seo-description: Application Security starts during the development phase
exl-id: c4f7f45f-224b-4fc3-b4b0-f5b21b8a466f
source-git-commit: c55b70ec11842d3f7d82adbf552b2624c1dcc599
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Segurança{#security}

A Segurança de aplicativos é iniciada durante a fase de desenvolvimento. O Adobe recomenda aplicar as seguintes práticas recomendadas de segurança.

## Usar sessão de solicitação {#use-request-session}

Seguindo o princípio de privilégio mínimo, o Adobe recomenda que todo acesso ao repositório seja feito usando a sessão vinculada à solicitação do usuário e o controle de acesso adequado.

## Protect contra Scripts entre sites (XSS) {#protect-against-cross-site-scripting-xss}

A criação de script entre sites (XSS) permite que invasores injetem código em páginas da Web visualizadas por outros usuários. Essa vulnerabilidade de segurança pode ser explorada por usuários mal-intencionados da Web para ignorar controles de acesso.

O AEM aplica o princípio de filtrar todo o conteúdo fornecido pelo usuário na saída. É dada a maior prioridade à prevenção de XSS durante o desenvolvimento e o teste.

O mecanismo de proteção XSS fornecido pelo AEM baseia-se no [Biblioteca Java do AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) fornecido por [OWASP (The Open Web Application Security Project, Projeto de Segurança de Aplicações Web Abertas)](https://www.owasp.org/). A configuração padrão do AntiSamy pode ser encontrada em

`/libs/cq/xssprotection/config.xml`

É importante adaptar essa configuração às suas necessidades de segurança, sobrepondo o arquivo de configuração. O funcionário [Documentação do AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) O fornecerá todas as informações necessárias para implementar seus requisitos de segurança.

>[!NOTE]
>
>Recomendamos que você sempre acesse a API de proteção XSS usando o [XSSAPI fornecido por AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

Além disso, um firewall de aplicativo web, como [mod_security para Apache](https://www.modsecurity.org)O, oferece controle confiável e central sobre a segurança do ambiente de implantação e proteção contra ataques de script entre sites não detectados anteriormente.

## Acesso às informações do Cloud Service {#access-to-cloud-service-information}

>[!NOTE]
>
>As ACLs para as Informações de Cloud Service, bem como as configurações de OSGi necessárias para proteger sua instância são automatizadas como parte da [Modo de produção pronto](/help/sites-administering/production-ready.md). Embora isso signifique que você não precisa fazer as alterações de configuração manualmente, ainda é recomendável revisá-las antes de entrar em funcionamento com a implantação.

Quando você [integrar sua instância do AEM à Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md) você usa [configurações de Cloud Service](/help/sites-developing/extending-cloud-config.md). As informações sobre essas configurações, juntamente com quaisquer estatísticas coletadas, são armazenadas no repositório. Recomendamos que, se estiver usando essa funcionalidade, você verifique se a segurança padrão nessas informações corresponde aos seus requisitos.

O módulo webservicesupport grava estatísticas e informações de configuração em:

`/etc/cloudservices`

Com as permissões padrão:

* Ambiente do autor: `read` para `contributors`

* Ambiente de publicação: `read` para `everyone`

## Protect contra ataques de falsificação de solicitação entre sites {#protect-against-cross-site-request-forgery-attacks}

Para obter mais informações sobre os mecanismos de segurança que o AEM utiliza para mitigar ataques de CSRF, consulte [Sling Referrer Filter](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) seção da Lista de verificação de segurança e da [Documentação da Estrutura de proteção CSRF](/help/sites-developing/csrf-protection.md).
