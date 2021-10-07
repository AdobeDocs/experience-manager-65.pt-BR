---
title: OWASP Top 10
seo-title: OWASP Top 10
description: Saiba como o AEM lida com os 10 principais riscos de segurança da OWASP.
seo-description: Learn how AEM deals with the top 10 OWASP security risks.
uuid: a5a7e130-e15b-47ae-ba21-448f9ac76074
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: e5323ae8-bc37-4bc6-bca6-9763e18c8e76
exl-id: 8b2a2f1d-8286-4ba5-8fe2-627509c72a45
feature: Security
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# OWASP Top 10{#owasp-top}

O [Open Web Application Security Project](https://www.owasp.org) (OWASP) mantém uma lista do que considera como os [Os 10 principais riscos de segurança da aplicação web](https://www.owasp.org/index.php/OWASP_Top_Ten_Project).

Elas estão listadas abaixo, juntamente com uma explicação de como o CRX lida com elas.

## 1. Injeção {#injection}

* SQL - Impedido pelo design: A configuração padrão do repositório não inclui nem requer um banco de dados tradicional, todos os dados são armazenados no repositório de conteúdo. Todo o acesso está limitado a usuários autenticados e só pode ser executado por meio da API JCR. O SQL é compatível somente com consultas de pesquisa (SELECT). Mais o SQL oferece suporte à vinculação de valor.
* LDAP - A injeção LDAP não é possível, pois o módulo de autenticação filtra a entrada e executa a importação do usuário usando o método bind.
* SO - Não há execução de shell executada no aplicativo.

## 2. Script entre sites (XSS) {#cross-site-scripting-xss}

A prática geral de mitigação é codificar toda a saída de conteúdo gerado pelo usuário usando uma biblioteca de proteção XSS do lado do servidor com base em [Codificador OWASP](https://www.owasp.org/index.php/OWASP_Java_Encoder_Project) e [AntiSamy](https://www.owasp.org/index.php/Category:OWASP_AntiSamy_Project).

O XSS é uma prioridade máxima durante testes e desenvolvimento, e todos os problemas encontrados são (normalmente) resolvidos imediatamente.

## 3. Autenticação quebrada e gerenciamento de sessão {#broken-authentication-and-session-management}

AEM usa técnicas de autenticação comprovadas e de som, que dependem do [Apache Jackrabbit](https://jackrabbit.apache.org/) e [Apache Sling](https://sling.apache.org/). Sessões de Navegador/HTTP não são usadas em AEM.

## 4. Referências inseguras de objeto direto {#insecure-direct-object-references}

Todo o acesso a objetos de dados é mediado pelo repositório e, portanto, restringido pelo controle de acesso baseado em funções.

## 5. Falsificação de solicitação entre sites (CSRF) {#cross-site-request-forgery-csrf}

A falsificação de solicitação entre sites (CSRF) é atenuada ao injetar automaticamente um token criptográfico em todos os formulários e solicitações de AJAX e verificar esse token no servidor para cada POST.

Além disso, AEM vem com um filtro baseado no cabeçalho do referenciador, que pode ser configurado para *somente* permitir solicitações de POST de hosts específicos (definido em uma lista).

## 6. Configuração incorreta da segurança {#security-misconfiguration}

É impossível garantir que todos os softwares estejam sempre configurados corretamente. No entanto, nos esforçamos para fornecer o máximo de orientação possível e tornar a configuração o mais simples possível. Além disso, AEM vem com [verificações de integridade de segurança integradas](/help/sites-administering/operations-dashboard.md) que ajudam a monitorar a configuração de segurança imediatamente.

Revise a [Lista de verificação de segurança](/help/sites-administering/security-checklist.md) para obter mais informações, que fornecem instruções de proteção passo a passo.

## 7. Armazenamento Criptográfico Inseguro {#insecure-cryptographic-storage}

As senhas são armazenadas como hashes criptográficos no nó do usuário; por padrão, esses nós só podem ser lidos pelo administrador e pelo próprio usuário.

Dados confidenciais, como credenciais de terceiros, são armazenados em formulários criptografados usando uma biblioteca criptográfica certificada pelo FIPS 140-2.

## 8. Falha ao restringir o acesso ao URL {#failure-to-restrict-url-access}

O repositório permite a configuração de [privilégios finamente granulados (conforme especificado pelo JCR)](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html) para qualquer usuário ou grupo em um determinado caminho, por meio de entradas de controle de acesso. As restrições de acesso são aplicadas pelo repositório.

## 9. Proteção insuficiente da camada de transporte {#insufficient-transport-layer-protection}

Atenuado pela configuração do servidor (por exemplo, usar somente HTTPS).

## 10. Redirecionamentos e encaminhamentos não validados {#unvalidated-redirects-and-forwards}

Atenuado ao restringir todos os redirecionamentos para destinos fornecidos pelo usuário a locais internos.
