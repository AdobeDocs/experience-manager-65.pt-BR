---
title: Segurança
seo-title: Segurança
description: O Application Security é iniciado durante a fase de desenvolvimento
seo-description: O Application Security é iniciado durante a fase de desenvolvimento
uuid: efd5f3bc-da07-4fc8-a6ce-f1e6f5084c9e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: d2267663-6c1d-413c-9862-e82e21ae6906
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Segurança{#security}

O Application Security é iniciado durante a fase de desenvolvimento. A Adobe recomenda aplicar as seguintes práticas recomendadas de segurança.

## Usar sessão de solicitação {#use-request-session}

Seguindo o princípio de privilégios mínimos, a Adobe recomenda que cada acesso ao repositório seja feito usando a sessão vinculada à solicitação do usuário e o controle de acesso adequado.

## Proteger contra Scripts entre Sites (XSS) {#protect-against-cross-site-scripting-xss}

Scripts entre sites (XSS) permitem que os invasores injetem código em páginas da Web visualizadas por outros usuários. Essa vulnerabilidade de segurança pode ser explorada por usuários maliciosos da Web para ignorar os controles de acesso.

O AEM aplica o princípio de filtrar todo o conteúdo fornecido pelo usuário na saída. A prevenção do XSS é atribuída à prioridade mais alta durante o desenvolvimento e o teste.

O mecanismo de proteção XSS fornecido pelo AEM é baseado na Biblioteca [Java](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) AntiSamy fornecida pela [OWASP (Open Web Application Security Project)](https://www.owasp.org/). A configuração padrão do AntiSamy pode ser encontrada em

`/libs/cq/xssprotection/config.xml`

É importante adaptar essa configuração às suas próprias necessidades de segurança sobrepondo o arquivo de configuração. A documentação [oficial](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project) AntiSamy fornecerá todas as informações necessárias para implementar seus requisitos de segurança.

>[!NOTE]
>
>Recomendamos que você sempre acesse a API de proteção XSS usando a [XSSAPI fornecida pelo AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/xss/XSSAPI.html).

Além disso, um firewall de aplicativo da Web, como [mod_security para Apache](https://www.modsecurity.org), pode fornecer controle central e confiável sobre a segurança do ambiente de implantação e proteger contra ataques de script entre sites não detectados anteriormente.

## Acesso às informações do serviço de nuvem {#access-to-cloud-service-information}

>[!NOTE]
>
>As ACLs para as Informações de serviço em nuvem, bem como as configurações de OSGi necessárias para proteger sua instância, são automatizadas como parte do Modo [Pronto para](/help/sites-administering/production-ready.md)Produção. Embora isso signifique que você não precisa fazer as alterações de configuração manualmente, ainda é recomendável revisá-las antes de entrar em operação com sua implantação.

Ao [integrar sua instância do AEM à Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md) , você usa as configurações [do serviço](/help/sites-developing/extending-cloud-config.md)Cloud. As informações sobre essas configurações, juntamente com quaisquer estatísticas coletadas, são armazenadas no repositório. Recomendamos que, se você estiver usando essa funcionalidade, verifique se a segurança padrão nessas informações corresponde aos seus requisitos.

O módulo webservicesupport grava estatísticas e informações de configuração em:

`/etc/cloudservices`

Com as permissões padrão:

* Ambiente do autor: `read` para `contributors`

* Ambiente de publicação: `read` para `everyone`

## Proteger contra ataques de falsificação de solicitação entre sites {#protect-against-cross-site-request-forgery-attacks}

Para obter mais informações sobre os mecanismos de segurança que o AEM emprega para mitigar ataques do CSRF, consulte a seção Filtro [do referenciador de](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) sling da Lista de verificação de segurança e a documentação [do Quadro de proteção do](/help/sites-developing/csrf-protection.md)CSRF.