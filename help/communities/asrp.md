---
title: ASRP - Provedor de recurso de armazenamento de Adobe
description: Configurar o AEM Communities para usar um banco de dados relacional como seu armazenamento comum
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 6430ed96-5d96-41b6-866f-90b34ff84f7a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---

# ASRP - Provedor de recurso de armazenamento de Adobe {#asrp-adobe-storage-resource-provider}

## Sobre ASRP {#about-asrp}

Quando o AEM Communities é configurado para usar o ASRP como seu armazenamento comum, o conteúdo gerado pelo usuário (UGC) é acessível de todas as instâncias de criação e publicação sem a necessidade de sincronização ou replicação.

Consulte também [Características das Opções SRP](/help/communities/working-with-srp.md#characteristics-of-srp-options) e [Topologias Recomendadas](/help/communities/topologies.md).

## Requisitos {#requirements}

É necessária uma licença adicional para o uso do ASRP.

Para configurar o site do AEM Communities para usar o ASRP para UGC, entre em contato com o representante da conta para obter:

* URL do data center (endereço do endpoint ASRP)
* Chave do consumidor
* Chave secreta
* ID(s) do conjunto de relatórios

O consumidor e as chaves secretas são compartilhados em todos os conjuntos de relatórios de uma empresa. Há um conjunto de relatórios por locatário.

## Configuração {#configuration}

### Selecionar ASRP {#select-asrp}

O [console de Configuração de Armazenamento](/help/communities/srp-config.md) permite a seleção da configuração de armazenamento padrão, que identifica qual implementação de SRP usar.

**Na instância do Autor AEM:**

* Na navegação global, navegue até **[!UICONTROL Ferramentas > Comunidades > Configuração de Armazenamento]** e selecione **[!UICONTROL Provedor de Recurso de Armazenamento de Adobe (ASRP)]**.

![asrp-padrão](assets/asrp-default.png)

As seguintes informações vêm do processo de provisionamento:

* **URL do data center**: puxe para baixo para selecionar o data center de produção identificado pelo seu representante de conta.
* **Conjunto de relatórios padrão**: insira o nome do conjunto de relatórios padrão.
* **Chave do consumidor**: insira a chave do consumidor.
* **Segredo**: insira o segredo.
* Selecione **Enviar**.

Prepare as instâncias de publicação:

* [Replicar a chave de criptografia](#replicate-the-crypto-key)
* [Replicar a configuração](#publishing-the-configuration)

Depois de enviar a configuração, teste a conexão:

* Selecione **Configuração de Teste**.

  Para cada instância de criação e publicação, teste a conexão com o data center pelo console Configuração de armazenamento.

* Verifique se as URLs de site para dados de perfil podem ser roteadas do Data Center por [externalizando links](#externalize-links).

### Replicar a chave de criptografia {#replicate-the-crypto-key}

A Consumer Key e a Secret Key são criptografadas. Para que as chaves sejam criptografadas/descriptografadas corretamente, a chave primária do Granite Crypto deve ser a mesma em todas as instâncias do AEM.

Siga as instruções em [Replicar a Chave de Criptografia](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Externalizar links {#externalize-links}

Para obter os links corretos do perfil e da imagem do perfil, certifique-se de [Configurar corretamente o Externalizador de links](/help/sites-developing/externalizer.md).

Certifique-se de definir os domínios como URLs roteáveis do URL do data center (ponto de extremidade ASRP).

### Sincronização de tempo {#time-synchronization}

Para que a autenticação com o ponto de extremidade ASRP seja bem-sucedida, as máquinas que executam o AEM Communities hospedado devem ter o horário sincronizado, como com o [NTP (Network Time Protocol)](https://www.ntp.org/).

### Publicar a configuração {#publishing-the-configuration}

O ASRP deve ser identificado como o armazenamento comum em todas as instâncias de autor e publicação.

Para disponibilizar a configuração idêntica no ambiente de publicação:

Na instância do autor AEM:

* Navegue do menu principal para **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]**
* Selecionar **Ativar árvore**
* **Caminho Inicial**: navegar até `/conf/global/settings/communities/srpc/`
* Desmarcar **Somente modificados**
* Selecionar **Ativar**

## Atualização do AEM 6.0 {#upgrading-from-aem}

>[!CAUTION]
>
>Se você habilitar o ASRP em um site de comunidade publicado, qualquer UGC já armazenado em [JCR](/help/communities/jsrp.md) não estará mais visível, pois não há sincronização de dados entre o armazenamento local e o armazenamento na nuvem.

O **`AEM Communities Extension`** foi introduzido anteriormente em comunidades sociais AEM 6.0 como um serviço na nuvem. Desde Comunidades AEM 6.1, nenhuma configuração de nuvem é necessária, basta selecionar ASRP no [console de configuração de armazenamento](/help/communities/srp-config.md).

Devido à nova estrutura de armazenamento, é necessário seguir as instruções de [atualização](/help/communities/upgrade.md#adobe-cloud-storage) ao atualizar de comunidades sociais para Comunidades.

## Gerenciamento de dados do usuário {#managing-user-data}

Para obter informações sobre *usuários*, *perfis de usuários* e *grupos de usuários*, inseridos com frequência no ambiente de publicação, visite

* [Sincronização de usuário](/help/communities/sync.md)
* [Gerenciar usuários e grupos de usuários](/help/communities/users.md)

## Resolução de problemas {#troubleshooting}

### O UGC desaparece após a atualização {#ugc-disappears-after-upgrade}

Se estiver atualizando de um site da comunidade social AEM 6.0 existente, siga as [instruções de atualização](/help/communities/upgrade.md#adobe-cloud-storage); caso contrário, o UGC parece ter sido perdido.

### Erros de autenticação {#authentication-errors}

Se receber erros de autenticação no URL do data center e o error.log de AEM contiver mensagens sobre carimbos de data e hora obsoletos, verifique se a sincronização de tempo está acontecendo.

Use uma ferramenta como o [NTP (Network Time Protocol)](https://www.ntp.org/) para sincronizar com o tempo todos os servidores de autor e publicação do AEM.

### O novo conteúdo não aparece nas pesquisas {#new-content-does-not-appear-in-searches}

A infraestrutura de armazenamento em nuvem do Adobe usa *consistência eventual* para atingir suas metas de dimensionamento e desempenho. Por esse motivo, o novo conteúdo não fica disponível instantaneamente e leva vários segundos para aparecer nos resultados da pesquisa.

Embora o intervalo que afeta a consistência final seja monitorado, entre em contato com o representante de conta se levar mais do que alguns segundos para que o novo conteúdo apareça nas pesquisas.

### UGC não visível no ASRP {#ugc-not-visible-in-asrp}

Verifique se o ASRP foi configurado como o provedor padrão, verificando a configuração da opção de armazenamento. Por padrão, o provedor de recursos de armazenamento é JSRP, não ASRP.

Em todas as instâncias de criação e publicação do AEM, visite novamente o console de Configuração de armazenamento ou verifique o repositório AEM.

No JCR, se [/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* Não contém um nó [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp), significa que o provedor de armazenamento é JSRP.
* Se o nó srpc existir e contiver o nó [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration), as propriedades defaultconfiguration definirão o ASRP como o provedor padrão.
