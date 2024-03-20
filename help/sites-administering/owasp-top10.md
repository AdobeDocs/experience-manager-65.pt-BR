---
title: OWASP 10 melhores
description: Saiba como o AEM lida com os dez principais riscos de segurança da OWASP.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# OWASP 10 melhores{#owasp-top}

A variável [Abrir Projeto de Segurança de Aplicativo Web](https://owasp.org/) (OWASP) mantém uma lista do que consideram ser a [Dez principais riscos à segurança de aplicações web](https://owasp.org/www-project-top-ten/).

Eles estão listados abaixo, junto com uma explicação de como o CRX lida com eles.

## 1. Injeção {#injection}

* SQL — evitado por design: a configuração padrão do repositório não inclui nem exige um banco de dados tradicional; todos os dados são armazenados no repositório de conteúdo. Todo o acesso é limitado a usuários autenticados e só pode ser executado por meio da API JCR. O SQL é compatível somente com consultas de pesquisa (SELECT). Além disso, o SQL oferece suporte à vinculação de valores.
* LDAP - A injeção de LDAP não é possível, pois o módulo de autenticação filtra a entrada e executa a importação do usuário usando o método bind.
* OS - Não há execução de shell a partir do aplicativo.

## 2. Criação de script entre sites (XSS) {#cross-site-scripting-xss}

A prática geral de mitigação é codificar todas as saídas de conteúdo gerado pelo usuário usando uma biblioteca de proteção XSS do lado do servidor com base em [Codificador OWASP](https://owasp.org/www-project-java-encoder/) e [AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

O XSS é uma prioridade principal durante os testes e o desenvolvimento, e todos os problemas encontrados são (normalmente) resolvidos imediatamente.

## 3. Autenticação interrompida e gerenciamento de sessão {#broken-authentication-and-session-management}

O AEM usa técnicas de autenticação comprovadas e de som, contando com [Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) e [Apache Sling](https://sling.apache.org/). As sessões de navegador/HTTP não são usadas no AEM.

## 4. Referências de objeto direto não seguras {#insecure-direct-object-references}

Todo o acesso a objetos de dados é mediado pelo repositório e, portanto, restrito pelo controle de acesso baseado em função.

## 5. Falsificação de solicitação entre sites (CSRF) {#cross-site-request-forgery-csrf}

A CSRF (Falsificação de solicitação entre sites) é atenuada pela injeção automática de um token criptográfico em todos os formulários e solicitações de AJAX e pela verificação desse token no servidor para cada POST.

Além disso, o AEM é enviado com um filtro baseado no cabeçalho do referenciador, que pode ser configurado para *somente* permitir solicitações POST de hosts específicos (definidos em uma lista).

## 6. Erro de configuração de segurança {#security-misconfiguration}

É impossível garantir que todo o software esteja sempre configurado corretamente. No entanto, o Adobe se esforça para fornecer o máximo de orientação possível e tornar a configuração o mais simples possível. Além disso, o AEM [verificações de integridade de segurança integradas](/help/sites-administering/operations-dashboard.md) que ajudam a monitorar rapidamente a configuração de segurança.

Revise o [Lista de verificação de segurança](/help/sites-administering/security-checklist.md) para obter mais informações que fornecem instruções passo a passo sobre como reforçar o.

## 7. Armazenamento criptográfico inseguro {#insecure-cryptographic-storage}

As senhas são armazenadas como hashes criptográficos no nó do usuário. Por padrão, esses nós só podem ser lidos pelo administrador e pelo próprio usuário.

Dados confidenciais, como credenciais de terceiros, são armazenados em formato criptografado usando uma biblioteca criptográfica com certificação FIPS 140-2.

## 8. Falha ao restringir o acesso ao URL {#failure-to-restrict-url-access}

O repositório permite a configuração de [privilégios refinados (conforme especificado pelo JCR)](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) para qualquer usuário ou grupo específico em qualquer caminho, por meio de entradas de controle de acesso. As restrições de acesso são aplicadas pelo repositório.

## 9. Proteção insuficiente da camada de transporte {#insufficient-transport-layer-protection}

Reduzido pela configuração do servidor (por exemplo, use somente HTTPS).

## 10. Redirecionamentos e encaminhamentos não validados {#unvalidated-redirects-and-forwards}

Atenuado pela restrição de todos os redirecionamentos para destinos fornecidos pelo usuário para locais internos.
