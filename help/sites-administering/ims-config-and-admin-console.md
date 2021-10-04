---
title: Autenticação do Adobe IMS e [!DNL Admin Console] Suporte para AEM Managed Services
seo-title: Adobe IMS Authentication and [!DNL Admin Console] Support for AEM Managed Services
description: Saiba como usar o  [!DNL Admin Console] no AEM.
seo-description: Learn how to use the [!DNL Admin Console] in AEM.
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
exl-id: 95eae97c-01c2-4f5c-8068-f504eab7c49e
feature: Security
source-git-commit: 3f55ebfe3b1603a573fcb77155227c449c6c0fbb
workflow-type: tm+mt
source-wordcount: '1688'
ht-degree: 10%

---

# Autenticação Adobe IMS e suporte [!DNL Admin Console] para AEM Managed Services {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>Observe que esse recurso está disponível somente para clientes do Adobe Managed Services.

>[!NOTE]
>
>O login do IMS para AEM não é compatível com grupos aninhados no Admin Console.

## Introdução {#introduction}

O AEM 6.4.3.0 apresenta [!DNL Admin Console] suporte para instâncias AEM e autenticação baseada no Adobe IMS (Identity Management System) para **AEM clientes Managed Services**.

AEM integração ao [!DNL Admin Console] permitirá que AEM clientes do Managed Services gerenciem todos os usuários do Experience Cloud em um console. Usuários e grupos podem ser atribuídos a perfis de produto associados a instâncias de AEM, permitindo que eles façam logon em uma instância específica.

## Destaques principais {#key-highlights}

* AEM o suporte de autenticação IMS é somente para autores, administradores ou desenvolvedores do AEM, não para usuários finais externos de visitantes do site do cliente como visitantes do site
* O [!DNL Admin Console] representará AEM clientes do Managed Services como Organizações do IMS e suas Instâncias como Contextos do produto. Os administradores de sistema e de produto do cliente poderão gerenciar o acesso às instâncias
* AEM Managed Services sincronizará as topologias do cliente com o [!DNL Admin Console]. Haverá uma instância do Contexto de Produto AEM Managed Services por Instância no [!DNL Admin Console].
* Os perfis de produto em [!DNL Admin Console] determinarão quais instâncias um usuário pode acessar
* A autenticação federada usando provedores de identidade compatíveis com SAML 2 próprios dos clientes é compatível
* Somente as Enterprise ID ou Federated ID (para logon único do cliente) serão compatíveis, não as IDs de Adobe pessoal.
* [!DNL User Management] (no Adobe  [!DNL Admin Console]) continuará sendo de propriedade dos administradores do cliente.

## Arquitetura {#architecture}

A autenticação IMS funciona usando o protocolo OAuth entre o AEM e o terminal Adobe IMS. Depois que um usuário é adicionado ao IMS e tem uma Adobe Identity, ele pode fazer logon nas instâncias do AEM Managed Services usando as credenciais do IMS.

O fluxo de logon do usuário é mostrado abaixo. O usuário será redirecionado para o IMS e, opcionalmente, para o IDP do cliente para validação do SSO e redirecionado para o AEM.

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## Como configurar {#how-to-set-up}

### Integração de organizações a [!DNL Admin Console] {#onboarding-organizations-to-admin-console}

A integração do cliente a [!DNL Admin Console] é um pré-requisito para usar o Adobe IMS para autenticação de AEM.

Como primeira etapa, os clientes devem ter uma Organização provisionada no Adobe IMS. Os clientes do Adobe Enterprise são representados como Organizações do IMS no [Adobe [!DNL Admin Console]](https://helpx.adobe.com/br/enterprise/using/admin-console.html).

AEM os clientes da Managed Services já devem ter uma organização provisionada e, como parte do provisionamento do IMS, as instâncias do cliente serão disponibilizadas no [!DNL Admin Console] para gerenciar os direitos e o acesso do usuário.

A mudança para o IMS para autenticação de usuário será um esforço conjunto entre o AMS e os clientes, com cada um tendo seus fluxos de trabalho para serem concluídos.

Quando um cliente existe como uma Organização IMS e o AMS é feito com o provisionamento do cliente para IMS, este é o resumo dos workflows de configuração necessários:

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. O Administrador do sistema designado recebe um convite para fazer logon no [!DNL Admin Console]
1. O administrador do sistema reclama o domínio para confirmar a propriedade do domínio (neste exemplo, acme.com)
1. O Administrador do sistema configura os Diretórios de usuário
1. O Administrador do sistema configura o Provedor de identidade (IDP) no [!DNL Admin Console] para configuração do SSO.
1. O AEM Admin gerencia os grupos locais, permissões e privilégios, como de costume. Consulte Sincronização de usuários e grupos

>[!NOTE]
>
>Para obter mais informações sobre os Noções básicas do Adobe Identity Management, incluindo a configuração do IDP, consulte o artigo [this page.](https://helpx.adobe.com/br/enterprise/using/set-up-identity.html)
>
>Para obter mais informações sobre a Administração corporativa e [!DNL Admin Console] consulte o artigo [this page](https://helpx.adobe.com/br/enterprise/managing/user-guide.html).

### Integração de usuários ao [!DNL Admin Console] {#onboarding-users-to-the-admin-console}

Há três maneiras de integrar usuários dependendo do tamanho do cliente e de suas preferências:

1. Criar usuários e grupos manualmente em [!DNL Admin Console]
1. Fazer upload de um arquivo CSV com usuários
1. Sincronize usuários e grupos do Ative Diretory corporativo do cliente.

#### Adição manual por meio da interface [!DNL Admin Console] {#manual-addition-through-admin-console-ui}

Usuários e grupos podem ser criados manualmente na interface do usuário [!DNL Admin Console]. Esse método pode ser usado se eles não tiverem um grande número de usuários para gerenciar. Por exemplo, um número de usuários com menos de 50 AEM.

Os usuários também podem ser criados manualmente se o cliente já estiver usando esse método para administrar outros produtos do Adobe, como aplicativos do Analytics, Target ou Creative Cloud.

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### Upload de arquivo na interface do usuário [!DNL Admin Console] {#file-upload-in-the-admin-console-ui}

Para facilitar a criação de usuários, um arquivo CSV pode ser carregado para adicionar usuários em massa:

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### Ferramenta de sincronização de usuários {#user-sync-tool}

A Ferramenta de sincronização de usuários (UST, User Sync Tool) permite que os clientes corporativos criem ou gerenciem usuários do Adobe utilizando o Ative Diretory ou outros serviços de diretório OpenLDAP testados. Os usuários de destino são Administradores de identidade de TI (Diretório corporativo e Administradores do sistema) que poderão instalar e configurar a ferramenta. A ferramenta de código aberto é personalizável para que os clientes possam modificá-la para atender às suas necessidades específicas.

Quando a Sincronização de usuários é executada, ela obtém uma lista de usuários do Ative Diretory da organização (ou qualquer outra fonte de dados compatível) e a compara com a lista de usuários no [!DNL Admin Console]. Em seguida, chama a API Adobe [!DNL User Management] para que [!DNL Admin Console] seja sincronizado com o diretório da organização. O fluxo de mudanças é totalmente unidirecional; as edições feitas no [!DNL Admin Console] não são enviadas para o diretório.

A ferramenta permite que o administrador do sistema mapeie grupos de usuários no diretório do cliente com a configuração do produto e grupos de usuários no [!DNL Admin Console], a nova versão UST também permite a criação dinâmica de grupos de usuários no [!DNL Admin Console].

Para configurar a Sincronização de usuários, a organização precisa criar um conjunto de credenciais da mesma forma que usaria a [[!DNL User Management] API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html).

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

A Sincronização de usuários é distribuída pelo repositório do Adobe Github neste local:

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

Observe que uma versão de pré-lançamento 2.4RC1 está disponível com suporte à criação de grupos dinâmicos e pode ser encontrada aqui: [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

Os principais recursos desta versão são a capacidade de mapear dinamicamente novos grupos LDAP para associação de usuários no [!DNL Admin Console], bem como a criação dinâmica de grupos de usuários.

Mais informações sobre os novos recursos do grupo podem ser encontradas aqui:

[https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/br/user-manual/advanced_configuration.md#additional-group-options)

>[!NOTE]
>
>Para obter mais informações sobre a Ferramenta de sincronização de usuários, consulte a [página de documentação](https://adobe-apiplatform.github.io/user-sync.py/br/).
>
>
>A Ferramenta de sincronização de usuários precisa se registrar como um UMAPI Adobe I/O client usando o procedimento descrito [here](https://adobe-apiplatform.github.io/umapi-documentation/br/UM_Authentication.html).
>
>A Documentação do console Adobe I/O pode ser encontrada [aqui](https://www.adobe.io/apis/cloudplatform/console.html).
>
>
>A API [!DNL User Management] usada pela Ferramenta de sincronização de usuários é contemplada neste [location](https://www.adobe.io/apis/cloudplatform/umapi-new.html).

>[!NOTE]
>
>A configuração do AEM IMS será gerenciada pela equipe do Adobe Managed Services. No entanto, o administrador do cliente pode modificá-lo de acordo com seus requisitos (por exemplo, Associação automática de grupo ou Mapeamento de grupo). O cliente IMS também será registrado pela equipe da Managed Services.

## Como usar {#how-to-use}

### Gerenciamento de produtos e acesso do usuário em [!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}

Quando o Administrador de produto do cliente fizer logon em [!DNL Admin Console], verá várias instâncias do Contexto de produto do Managed Services AEM, como mostrado abaixo:

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

Neste exemplo, a organização *AEM-MS-Onboard* tem 32 instâncias que abrangem topologias e ambientes diferentes, como Preparo, Produção etc.

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

Os detalhes da instância podem ser verificados para identificar a instância:

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

Em cada instância do Contexto do Produto, haverá um Perfil de Produto associado. Esse perfil de produto é usado para atribuir acesso a usuários e grupos.

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

Todos os usuários e grupos adicionados nesse perfil de produto poderão fazer logon nessa instância, como mostrado no exemplo abaixo:

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### Logon no AEM {#logging-into-aem}

#### Logon do administrador local {#local-admin-login}

AEM pode continuar a suportar logons locais para usuários administradores, pois a tela de logon tem uma opção para fazer logon localmente:

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### Logon baseado no IMS {#ims-based-login}

Para outros usuários, o logon baseado no IMS pode ser usado assim que o IMS for configurado na instância. Primeiro, o usuário clicará no botão **Fazer logon com Adobe**, conforme mostrado abaixo:

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

Eles serão redirecionados para a tela de logon do IMS e inserirão suas credenciais:

![screen_shot_2018-09-17at15629pm](assets/screen_shot_2018-09-17at115629pm.png)

Se um IDP federado for configurado durante a configuração inicial [!DNL Admin Console], o usuário será redirecionado para o IDP do cliente para SSO.

O IDP é Okta no exemplo abaixo:

![screen_shot_2018-09-17at15734pm](assets/screen_shot_2018-09-17at115734pm.png)

Após a conclusão da autenticação, o usuário será redirecionado de volta para o AEM e conectado:

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### Migração de usuários existentes {#migrating-existing-users}

Para instâncias de AEM existentes que estão usando outro método de Autenticação e agora estão sendo migradas para o IMS, é necessário haver uma etapa de migração.

Os usuários existentes no repositório de AEM (originado localmente, via LDAP ou SAML) podem ser migrados para apontar para o IMS como o IDP usando o Utilitário de migração de usuário.

Esse utilitário será executado pela equipe do AMS como parte do provisionamento do IMS.

### Gerenciando permissões e ACLs no AEM {#managing-permissions-and-acls-in-aem}

O controle de acesso e as permissões continuarão a ser gerenciados no AEM, isso pode ser feito usando a separação de Grupos de usuários provenientes de IMS (por exemplo, AEM-GRP-008 no exemplo abaixo) e grupos locais onde as permissões e o controle de acesso são definidos. Os grupos de usuários sincronizados do IMS podem ser atribuídos a grupos locais e herdar as permissões.

No exemplo abaixo, adicionamos grupos sincronizados ao grupo local *Dam_Users*, como exemplo.

Aqui, um usuário também foi atribuído a alguns grupos no [!DNL Admin Console]. (Observe que os usuários e grupos podem ser sincronizados do LDAP usando a ferramenta de sincronização de usuários ou criados localmente, consulte a seção **Usuários onboard para o[!DNL Admin Console]** acima).

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

Como mostrado abaixo, o grupo *AEM-GRP_008* herda as Permissões e os Privilégios dos Usuários do DAM. Essa é uma maneira eficaz de gerenciar permissões para grupos sincronizados, além de ser comumente usada em métodos de autenticação baseados em LDAP.

![screen_shot_2018-09-17at10505pm](assets/screen_shot_2018-09-17at110505pm.png)
