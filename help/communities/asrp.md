---
title: ASRP - Provedor de Recursos de Armazenamento Adobe
seo-title: ASRP - Provedor de Recursos de Armazenamento Adobe
description: Configurar o AEM Communities para usar um banco de dados relacional como armazenamento comum
seo-description: Configurar o AEM Communities para usar um banco de dados relacional como armazenamento comum
uuid: abe47ad9-9f72-4dad-a5e9-6d621a9722d4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 3e81b519-57ca-4ee1-94bd-7adac4605407
docset: aem65
role: Admin
exl-id: 6430ed96-5d96-41b6-866f-90b34ff84f7a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# ASRP - Provedor de Recursos de Armazenamento Adobe {#asrp-adobe-storage-resource-provider}

## Sobre o ASRP {#about-asrp}

Quando o AEM Communities é configurado para usar o ASRP como armazenamento comum, o conteúdo gerado pelo usuário (UGC) é acessível de todas as instâncias de autor e publicação sem a necessidade de sincronização nem replicação.

Consulte também [Características das Opções de SRP](/help/communities/working-with-srp.md#characteristics-of-srp-options) e [Topologias recomendadas](/help/communities/topologies.md).

## Requisitos {#requirements}

É necessária uma licença adicional para a utilização do ASRP.

Para configurar seu site AEM Communities para usar o ASRP para UGC, entre em contato com seu representante de conta para:

* URL do centro de dados (endereço do ponto final ASRP)
* Chave do consumidor
* Chave secreta
* ID(s) de conjunto de relatórios

As chaves secretas e de consumidor são compartilhadas em todos os conjuntos de relatórios de uma empresa. Há um conjunto de relatórios por locatário.

## Configuração {#configuration}

### Selecionar ASRP {#select-asrp}

O [console Configuração de Armazenamento](/help/communities/srp-config.md) permite a seleção da configuração de armazenamento padrão, que identifica qual implementação do SRP usar.

**Na instância do autor do AEM:**

* Na navegação global, navegue até **[!UICONTROL Tools > Communities > Storage Configuration]** e selecione **[!UICONTROL Adobe Storage Resource Provider (ASRP)]**.

![asrp-default](assets/asrp-default.png)

As seguintes informações vêm do processo de provisionamento:

* **URL** do data center: Puxe para baixo para selecionar o data center de produção identificado pelo seu representante de conta.
* **Conjunto** de relatórios padrão: Insira o nome do conjunto de relatórios padrão.
* **Chave** do consumidor: Insira a chave do consumidor.
* **Segredo**: Insira o segredo.
* Selecione **Enviar**.

Prepare as instâncias de publicação:

* [Replicar a chave de criptografia](#replicate-the-crypto-key)
* [Replicar a configuração](#publishing-the-configuration)

Após enviar a configuração, teste a conexão:

* Selecione **Test Config**.

   Para cada instância de criação e publicação, teste a conexão com o data center a partir do console Configuração de Armazenamento.

* Certifique-se de que os URLs do site para dados de perfil sejam roteáveis a partir do data center por [externalizar links](#externalize-links).

### Replicar a chave de criptografia {#replicate-the-crypto-key}

A chave do consumidor e a chave secreta estão criptografadas. Para que as chaves sejam criptografadas/descriptografadas corretamente, a chave primária de criptografia do Granite deve ser a mesma em todas as instâncias AEM.

Siga as instruções em [Replicar a chave de criptografia](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Externalizar links {#externalize-links}

Para os links corretos de perfil e imagem de perfil, certifique-se de configurar corretamente o Link Externalizer](/help/sites-developing/externalizer.md).[

Certifique-se de definir os domínios como URLs roteáveis a partir do URL do data center (ponto de extremidade ASRP).

### Sincronização de Tempo {#time-synchronization}

Para que a autenticação com o ponto de extremidade ASRP seja bem-sucedida, as máquinas que executam o AEM Communities hospedado devem ser sincronizadas no tempo, como com o [Network Time Protocol (NTP)](https://www.ntp.org/).

### Publicar a configuração {#publishing-the-configuration}

O ASRP deve ser identificado como o armazenamento comum em todas as instâncias de autor e publicação.

Para disponibilizar a configuração idêntica no ambiente de publicação:

Na instância do autor do AEM:

* Navegue do menu principal para **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Replicação]**
* Selecione **Ativar árvore**
* **Caminho** inicial: navegue até  `/conf/global/settings/communities/srpc/`
* Desmarque **Somente Modificado**
* Selecione **Ativar**

## Atualização do AEM 6.0 {#upgrading-from-aem}

>[!CAUTION]
>
>Se você habilitar o ASRP em um site de comunidade publicado, qualquer UGC já armazenado em [JCR](/help/communities/jsrp.md) não estará mais visível, pois não há sincronização de dados entre o armazenamento local e o armazenamento em nuvem.

**`AEM Communities Extension`** O foi introduzido anteriormente no AEM 6.0 social communities as a cloud service. A partir AEM Comunidades 6.1, nenhuma configuração de nuvem é necessária, basta selecionar ASRP no [console de configuração de armazenamento](/help/communities/srp-config.md).

Devido à nova estrutura de armazenamento, é necessário seguir as instruções [upgrade](/help/communities/upgrade.md#adobe-cloud-storage) ao atualizar das comunidades sociais para as Comunidades.

## Gerenciar dados do usuário {#managing-user-data}

Para obter informações sobre *usuários*, *perfis de usuário* e *grupos de usuários*, normalmente inseridos no ambiente de publicação, visite

* [Sincronização de usuários](/help/communities/sync.md)
* [Gerenciar usuários e grupos de usuários](/help/communities/users.md)

## Resolução de problemas {#troubleshooting}

### O UGC desaparece após a atualização {#ugc-disappears-after-upgrade}

Se estiver atualizando de um site de comunidade social AEM 6.0 existente, certifique-se de seguir as [instruções de atualização](/help/communities/upgrade.md#adobe-cloud-storage), caso contrário, o UGC aparecerá perdido.

### Erros de autenticação {#authentication-errors}

Se estiver recebendo erros de autenticação com o URL do data center e o AEM error.log contiver mensagens sobre carimbos de data e hora obsoletos, verifique se a sincronização de hora está acontecendo.

Use uma ferramenta como o [Network Time Protocol (NTP)](https://www.ntp.org/) para sincronizar o tempo de todos os servidores de criação e publicação AEM.

### Novo conteúdo não aparece em pesquisas {#new-content-does-not-appear-in-searches}

A infraestrutura de armazenamento de nuvem do Adobe usa *eventual consistência* para atingir suas metas de dimensionamento e desempenho. Por isso, o novo conteúdo não está disponível instantaneamente e leva vários segundos para aparecer nos resultados da pesquisa.

Embora o intervalo que afeta uma eventual consistência seja monitorado, entre em contato com seu representante de conta se for demorado mais de alguns segundos para que o novo conteúdo apareça em pesquisas.

### UGC não visível no ASRP {#ugc-not-visible-in-asrp}

Certifique-se de que o ASRP foi configurado para ser o provedor padrão marcando a configuração da opção de armazenamento. Por padrão, o provedor de recursos de armazenamento é JSRP, não ASRP.

Em todas as instâncias de criação e publicação AEM, revise o console Configuração de armazenamento ou verifique o repositório AEM.

No JCR, se [/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* Não contém um nó [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp), significa que o provedor de armazenamento é JSRP.
* Se o nó srpc existir e contiver o nó [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration), as propriedades da configuração padrão definirão ASRP para ser o provedor padrão.
