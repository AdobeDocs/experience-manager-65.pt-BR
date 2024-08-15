---
title: Autenticação do Adobe IMS e  [!DNL Admin Console] Suporte para o Adobe Experience Manager Managed Services
description: Saiba como usar o  [!DNL Admin Console] no Adobe Experience Manager.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 95eae97c-01c2-4f5c-8068-f504eab7c49e
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '1602'
ht-degree: 6%

---

# Autenticação do Adobe IMS e suporte [!DNL Admin Console] para AEM Managed Services {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>Esse recurso está disponível somente para clientes do Adobe Managed Services.

## Introdução {#introduction}

O AEM 6.4.3.0 apresenta suporte [!DNL Admin Console] para instâncias AEM e autenticação baseada no Adobe IMS (Identity Management AEM System) para clientes do **Managed Services**.

A integração do AEM ao [!DNL Admin Console] permitirá que os clientes do AEM Managed Services gerenciem todos os usuários do Experience Cloud em um console. Os usuários podem ser atribuídos a perfis de produtos associados a instâncias do AEM, permitindo que façam logon em uma instância específica.

## Destaques principais {#key-highlights}

* O suporte à autenticação IMS do AEM é somente para autores, administradores ou desenvolvedores do AEM, não para usuários finais externos do site do cliente, como visitantes do site
* O [!DNL Admin Console] representará os clientes do AEM Managed Services como Organizações IMS e suas Instâncias como Contextos de Produto. O Sistema do cliente e os Administradores de produtos poderão gerenciar o acesso às instâncias
* O AEM Managed Services sincronizará as topologias do cliente com o [!DNL Admin Console]. Haverá uma instância do Contexto de Produto do Managed Services AEM por Instância no [!DNL Admin Console].
* Os Perfis de Produto no [!DNL Admin Console] determinarão quais instâncias um usuário poderá acessar
* A autenticação federada usando os Provedores de Identidade compatíveis com SAML 2 dos próprios clientes é compatível
* Somente IDs Enterprise ou Federated (para Logon único do cliente) serão compatíveis, não IDs de Adobe pessoais.
* [!DNL User Management] (no Adobe [!DNL Admin Console]) continuará a ser de propriedade dos administradores do cliente.

## Arquitetura {#architecture}

A autenticação do IMS funciona usando o protocolo OAuth entre o AEM e o terminal Adobe IMS. Depois que um usuário é adicionado ao IMS e tem uma Adobe Identity, ele pode fazer logon nas instâncias do AEM Managed Services usando as credenciais do IMS.

O fluxo de logon do usuário é mostrado abaixo. O usuário será redirecionado para o IMS e, como opção, para o IDP do cliente para validação de SSO e redirecionado para o AEM.

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## Como Configurar {#how-to-set-up}

### Integração de organizações a [!DNL Admin Console] {#onboarding-organizations-to-admin-console}

A integração do cliente ao [!DNL Admin Console] é um pré-requisito para o uso do Adobe IMS para autenticação AEM.

Como primeira etapa, os clientes devem ter uma Organização provisionada no Adobe IMS. Os clientes do Adobe Enterprise são representados como Organizações do IMS no [Adobe [!DNL Admin Console]](https://helpx.adobe.com/br/enterprise/using/admin-console.html).

Os clientes do Managed Services AEM já devem ter uma organização provisionada e, como parte do provisionamento do IMS, as instâncias do cliente serão disponibilizadas no [!DNL Admin Console] para gerenciar os direitos e o acesso do usuário.

A mudança para o IMS para autenticação de usuários será um esforço conjunto entre o AMS e os clientes, com cada um tendo seus fluxos de trabalho para concluir.

Quando um cliente existir como uma Organização IMS e o AMS terminar de provisionar o cliente para IMS, este será o resumo dos fluxos de trabalho de configuração necessários:

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. O Administrador do Sistema designado recebe um convite para fazer login no [!DNL Admin Console]
1. O domínio de declarações do administrador do sistema para confirmar a propriedade do domínio (neste exemplo acme.com)
1. O administrador do sistema configura os diretórios de usuário
1. O Administrador do Sistema configura o Provedor de Identidade (IDP) no [!DNL Admin Console] para configuração de SSO.
1. O Administrador do AEM gerencia os grupos locais, permissões e privilégios, como de costume. Consulte Sincronização de usuários e grupos

>[!NOTE]
>
>Para obter mais informações sobre as noções básicas do Adobe Identity Management, incluindo a configuração do IDP, consulte o artigo sobre [Configurar identidade e logon único](https://helpx.adobe.com/br/enterprise/using/set-up-identity.html).
>
>Para obter mais informações sobre a Administração da Empresa e [!DNL Admin Console], consulte o [Guia de boas-vindas à empresa e às equipes](https://helpx.adobe.com/br/enterprise/managing/user-guide.html).

### Integração de usuários ao [!DNL Admin Console] {#onboarding-users-to-the-admin-console}

Há três maneiras de integrar os usuários dependendo do tamanho do cliente e de sua preferência:

1. Criar usuários e grupos manualmente no [!DNL Admin Console]
1. Carregar um arquivo CSV com usuários
1. Sincronizar usuários e grupos do Ative Diretory corporativo do cliente.

#### Adição manual por meio da interface do usuário [!DNL Admin Console] {#manual-addition-through-admin-console-ui}

Usuários e grupos podem ser criados manualmente na interface do usuário do [!DNL Admin Console]. Esse método pode ser usado se eles não tiverem muitos usuários para gerenciar. Por exemplo, menos de 50 usuários de AEM.

Os usuários também podem ser criados manualmente se o cliente já estiver usando esse método para administrar outros produtos de Adobe, como aplicativos Adobe Analytics, Adobe Target ou Adobe Creative Cloud.

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### Upload de arquivo na interface do usuário do [!DNL Admin Console] {#file-upload-in-the-admin-console-ui}

Para facilitar a criação de usuários, um arquivo CSV pode ser carregado para adicionar usuários em massa:

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### Ferramenta de sincronização de usuários {#user-sync-tool}

A Ferramenta de sincronização de usuários (UST, User Sync Tool) permite que clientes corporativos criem ou gerenciem usuários de Adobe que usam o Ative Diretory ou outros serviços de diretório OpenLDAP testados. Os usuários de destino são Administradores de identidade de TI (Diretório corporativo e Administradores do sistema) que poderão instalar e configurar a ferramenta. A ferramenta de código aberto é personalizável para que os clientes possam solicitar que um desenvolvedor a modifique para se adequar aos seus próprios requisitos específicos.

Quando a Sincronização de Usuários é executada, ela obtém uma lista de usuários do Ative Diretory da organização (ou qualquer outra fonte de dados compatível) e a compara com a lista de usuários no [!DNL Admin Console]. Em seguida, ele chama a API de Adobe [!DNL User Management] para que [!DNL Admin Console] seja sincronizado com o diretório da organização. O fluxo de alterações é totalmente unidirecional; as edições feitas no [!DNL Admin Console] não são enviadas para o diretório.

A ferramenta permite que o administrador do sistema mapeie grupos de usuários no diretório do cliente com a configuração do produto e grupos de usuários no [!DNL Admin Console]. A nova versão da UST também permite a criação dinâmica de grupos de usuários no [!DNL Admin Console].

Para configurar a Sincronização de Usuários, a organização precisa criar um conjunto de credenciais da mesma forma que usaria a [[!DNL User Management] API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html).

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

A Sincronização de usuários é distribuída pelo repositório do GitHub Adobe neste local:

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

Observe que uma versão de pré-lançamento 2.4RC1 está disponível com suporte à criação de grupos dinâmicos e pode ser encontrada aqui: [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

Os principais recursos desta versão são a capacidade de mapear dinamicamente novos grupos LDAP para associação de usuários no [!DNL Admin Console] e criação dinâmica de grupos de usuários.

Mais informações sobre os novos recursos do grupo podem ser encontradas aqui:

[https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options](https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options)

>[!NOTE]
>
>Para obter mais detalhes, consulte:
>
>* a [Ferramenta de Sincronização de Usuários - Sincronização de Usuários Adobe](https://adobe-apiplatform.github.io/user-sync.py/bp/)
>
>* a Ferramenta de Sincronização de Usuários precisa se registrar como uma UMAPI de cliente Adobe I/O usando o procedimento descrito em [Autenticação para Acesso à API](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)
>
>* a [Documentação do Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/).
>
>* a [Documentação da API de Gerenciamento de Usuários](https://adobe-apiplatform.github.io/umapi-documentation/en/).
>

>[!NOTE]
>
>A configuração IMS do AEM será feita pela equipe do Adobe Managed Services. No entanto, o administrador do cliente pode modificá-lo de acordo com seus requisitos (por exemplo, Associação de grupo automática ou Mapeamento de grupo). O cliente IMS também será registrado pela equipe do Managed Services.

## Como usar {#how-to-use}

### Gerenciando Produtos e o Acesso de Usuários no [!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}

Quando o Administrador de Produto do cliente fizer logon no [!DNL Admin Console], ele verá várias instâncias do Contexto de Produto do AEM Managed Services, como mostrado abaixo:

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

Neste exemplo, a organização *AEM-MS-Onboard* tem 32 instâncias que abrangem topologias e ambientes diferentes, como Preparo, Produção e assim por diante.

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

Os detalhes da instância podem ser verificados para identificá-la:

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

Em cada instância do Contexto do produto, haverá um Perfil de produto associado. Este perfil de produto é usado para atribuir acesso aos usuários.

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

Todos os usuários adicionados nesse perfil de produto poderão fazer logon nessa instância, como mostra o exemplo abaixo:

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### Fazendo login no AEM {#logging-into-aem}

#### Logon do administrador local {#local-admin-login}

O AEM pode continuar a oferecer suporte a logons locais para usuários Administradores, já que a tela de logon tem uma opção para fazer logon localmente:

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### Logon baseado no IMS {#ims-based-login}

Para outros usuários, o logon baseado no IMS pode ser usado assim que o IMS for configurado na instância. O usuário clica primeiro em **Entrar com Adobe**, conforme mostrado abaixo:

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

Eles serão redirecionados para a tela de logon do IMS e inserirão suas credenciais:

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

Se um IDP federado for configurado durante a instalação inicial de [!DNL Admin Console], o usuário será redirecionado ao IDP do cliente para SSO.

O IDP é Okta no exemplo abaixo:

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

Após a conclusão da autenticação, o usuário será redirecionado de volta para o AEM e conectado:

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### Migração de usuários existentes {#migrating-existing-users}

Para instâncias de AEM existentes que estão usando outro método de autenticação e estão sendo migradas para IMS, é necessário haver uma etapa de migração.

Os usuários existentes no repositório AEM (originado localmente, via LDAP ou SAML) podem ser migrados para apontar para o IMS como o IDP usando o Utilitário de migração de usuários.

Esse utilitário será executado pela equipe do AMS como parte do provisionamento do IMS.

### Gerenciando permissões e ACLs no AEM {#managing-permissions-and-acls-in-aem}

O controle de acesso e as permissões continuarão a ser gerenciados no AEM, isso pode ser obtido usando a separação de Grupos de usuários provenientes do IMS (por exemplo, AEM-GRP-008 no exemplo abaixo) e de grupos locais onde as permissões e o controle de acesso são definidos. Os grupos de usuários sincronizados do IMS podem ser atribuídos a grupos locais e herdar as permissões.

No exemplo abaixo, adicionamos grupos sincronizados ao grupo local *Dam_Users*, como exemplo.

Aqui, um usuário também foi atribuído a alguns grupos no [!DNL Admin Console]. (Os usuários e grupos podem ser sincronizados do LDAP usando a ferramenta de sincronização de usuários ou criados localmente. Consulte **Integração de usuários ao[!DNL Admin Console]** anteriormente).

>[!NOTE]
>
>Os grupos de usuários só são sincronizados quando os usuários fazem logon na instância.

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

O usuário faz parte dos seguintes Grupos no IMS:

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

Quando o usuário faz logon, as Associações de grupo são sincronizadas, como mostrado abaixo:

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

No AEM, os grupos de usuários sincronizados do IMS podem ser adicionados como membros a grupos locais existentes, por exemplo, Usuários do DAM.

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

Como mostrado abaixo, o grupo *AEM-GRP_008* herda as Permissões e os Privilégios dos Usuários do DAM. Essa é uma maneira eficaz de gerenciar permissões para grupos sincronizados e também é usada em métodos de autenticação baseados em LDAP.

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)
