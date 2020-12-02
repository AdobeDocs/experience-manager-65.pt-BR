---
title: OWASP Top 10
seo-title: OWASP Top 10
description: Saiba como AEM lidar com os 10 principais riscos de segurança OWASP.
seo-description: Saiba como AEM lidar com os 10 principais riscos de segurança OWASP.
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
translation-type: tm+mt
source-git-commit: cd7331f5f57ec90ea72d41d467891dc832347a3c
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# OWASP Top 10{#owasp-top}

O [Open Aplicação web Security Project](https://www.owasp.org) (OWASP) mantém uma lista daquilo que considera como os [10 Riscos de segurança de Aplicação web mais importantes](https://www.owasp.org/index.php/OWASP_Top_Ten_Project).

Estes estão listados abaixo, juntamente com uma explicação de como o CRX lida com eles.

## 1. Injeção {#injection}

* SQL - Impedido pelo design: A configuração padrão do repositório não inclui nem exige um banco de dados tradicional, todos os dados são armazenados no repositório de conteúdo. Todo o acesso é limitado a usuários autenticados e só pode ser executado por meio da API JCR. O SQL é suportado apenas para query de pesquisa (SELECT). Mais suporte ao vínculo de valor do SQL oferta.
* LDAP - A injeção LDAP não é possível, pois o módulo de autenticação filtros a entrada e executa a importação do usuário usando o método bind.
* SO - Não há execução de shell executada dentro do aplicativo.

## 2. Scripts entre sites (XSS) {#cross-site-scripting-xss}

A prática geral de mitigação é codificar toda a saída de conteúdo gerado pelo usuário usando uma biblioteca de proteção XSS do lado do servidor com base em [OWASP Encoder](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) e [AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

O XSS é uma prioridade máxima durante testes e desenvolvimento, e todos os problemas encontrados são (normalmente) resolvidos imediatamente.

## 3. Autenticação quebrada e Gerenciamento de sessão {#broken-authentication-and-session-management}

AEM usa técnicas de autenticação comprovadas e de som, confiando em [Apache Jackrabbit](https://jackrabbit.apache.org/) e [Apache Sling](https://sling.apache.org/). Sessões de Navegador/HTTP não são usadas em AEM.

## 4. Referências de objeto direto inseguras {#insecure-direct-object-references}

Todo o acesso a objetos de dados é mediado pelo repositório e, portanto, restringido pelo controle de acesso baseado em funções.

## 5. CSRF (Cross-Site Request Forgery) {#cross-site-request-forgery-csrf}

O CSRF (Cross-Site Request Forgery) é mitigado ao injetar automaticamente um token criptográfico em todos os formulários e solicitações de AJAX e verificar esse token no servidor para cada POST.

Além disso, AEM vem com um filtro baseado no cabeçalho da quem indicou, que pode ser configurado para *somente* permitir solicitações POST de hosts específicos (definido em uma lista).

## 6. Configuração de segurança incorreta {#security-misconfiguration}

É impossível garantir que todos os softwares estejam sempre configurados corretamente. No entanto, esforçamo-nos por fornecer o máximo possível de orientações e por tornar a configuração o mais simples possível. Além disso, AEM os navios com [Security Health Checks](/help/sites-administering/operations-dashboard.md) integrados que ajudam a monitorar rapidamente a configuração de segurança.

Consulte a [Lista de verificação de segurança](/help/sites-administering/security-checklist.md) para obter mais informações, que fornecem instruções detalhadas passo a passo.

## 7. Armazenamento Criptográfico Inseguro {#insecure-cryptographic-storage}

As senhas são armazenadas como hashes criptográficos no nó do usuário; por padrão, esses nós só podem ser lidos pelo administrador e pelo próprio usuário.

Dados confidenciais, como credenciais de terceiros, são armazenados em forma criptografada usando uma biblioteca criptográfica certificada pelo FIPS 140-2.

## 8. Falha ao restringir o acesso ao URL {#failure-to-restrict-url-access}

O repositório permite a configuração de [privilégios de granulação fina (conforme especificado pelo JCR)](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html) para qualquer usuário ou grupo em determinado caminho, por meio de entradas de controle de acesso. As restrições de acesso são aplicadas pelo repositório.

## 9. Proteção insuficiente da camada de transporte {#insufficient-transport-layer-protection}

Limitado pela configuração do servidor (por exemplo, use somente HTTPS).

## 10. Redirecionamentos e encaminhamentos não validados {#unvalidated-redirects-and-forwards}

Reduzido restringindo todos os redirecionamentos para destinos fornecidos pelo usuário a locais internos.

