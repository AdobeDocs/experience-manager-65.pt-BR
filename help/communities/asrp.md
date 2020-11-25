---
title: ASRP - Provedor de Recursos de Armazenamento de Adobe
seo-title: ASRP - Provedor de Recursos de Armazenamento de Adobe
description: Configurar a AEM Communities para usar um banco de dados relacional como sua loja comum
seo-description: Configurar a AEM Communities para usar um banco de dados relacional como sua loja comum
uuid: abe47ad9-9f72-4dad-a5e9-6d621a9722d4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 3e81b519-57ca-4ee1-94bd-7adac4605407
docset: aem65
translation-type: tm+mt
source-git-commit: fd205cd6253991f527f87b9868d503f64a99a600
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---


# ASRP - Provedor de Recursos de Armazenamento de Adobe {#asrp-adobe-storage-resource-provider}

## Sobre o ASRP {#about-asrp}

Quando a AEM Communities está configurada para usar o ASRP como sua loja comum, o conteúdo gerado pelo usuário (UGC) é acessível de todas as instâncias de autor e publicação sem a necessidade de sincronização nem replicação.

Consulte também [Características das opções](/help/communities/working-with-srp.md#characteristics-of-srp-options) de SRP e das topologias [](/help/communities/topologies.md)recomendadas.

## Requisitos {#requirements}

É necessária uma licença adicional para o uso do ASRP.

Para configurar seu site da AEM Communities para usar o ASRP para UGC, verifique se você tem o seguinte:

* URL do centro de dados (endereço do ponto final ASRP)
* Chave do consumidor
* Chave secreta
* ID(s) do conjunto de relatórios

O consumidor e as chaves secretas são compartilhados em todos os conjuntos de relatórios para uma empresa. Há um conjunto de relatórios por locatário.

## Configuração {#configuration}

### Selecionar ASRP {#select-asrp}

O console [Configuração do](/help/communities/srp-config.md) Armazenamento permite a seleção da configuração padrão do armazenamento, que identifica qual implementação do SRP usar.

**Na instância do autor de AEM:**

* Na navegação global, navegue até **[!UICONTROL Ferramentas > Comunidades > Configuração]** do Armazenamento e selecione Provedor de recursos do Armazenamento **[!UICONTROL Adobe (ASRP)]**.

![asrp-default](assets/asrp-default.png)

As seguintes informações vêm do processo de provisionamento:

* **URL** do data center: Puxe para baixo para selecionar o centro de dados de produção identificado pelo seu representante de conta.
* **Conjunto** de relatórios padrão: Insira o nome do conjunto de relatórios padrão.
* **consumer key**: Entre na consumer key.
* **Segredo**: Insira o segredo.
* Selecione **Enviar**.

Prepare as instâncias de publicação:

* [Replicar a chave criptografada](#replicate-the-crypto-key)
* [Replicar a configuração](#publishing-the-configuration)

Após enviar a configuração, teste a conexão:

* Selecione **Testar configuração**.

   Para cada instância de autor e publicação, teste a conexão com o data center a partir do console Configuração do Armazenamento.

* Certifique-se de que os URLs do site para dados de perfil sejam roteáveis a partir do data center, [externalizando links](#externalize-links).

### Replicar a chave de criptografia {#replicate-the-crypto-key}

O Consumer key e a chave secreta estão criptografados. Para que as chaves sejam criptografadas/descriptografadas corretamente, a chave principal Criptografia Granite deve ser a mesma em todas as instâncias AEM.

Siga as instruções em [Replicate the Crypto Key (Replicar a chave](/help/communities/deploy-communities.md#replicate-the-crypto-key)de criptografia).

### Externalizar links {#externalize-links}

Para obter os links corretos de imagem de perfil e perfil, certifique-se de [configurar corretamente o Externalizador](/help/sites-developing/externalizer.md)de link.

Certifique-se de definir os domínios como URLs roteáveis a partir do URL do data center (terminal ASRP).

### Sincronização de tempo {#time-synchronization}

Para que a autenticação com o terminal ASRP tenha êxito, os computadores que executam seu AEM Communities hospedado devem ser sincronizados no tempo, como com o Protocolo de Tempo de [Rede (NTP)](https://www.ntp.org/).

### Publicar a configuração {#publishing-the-configuration}

O ASRP deve ser identificado como o repositório comum em todas as instâncias de autor e publicação.

Para disponibilizar a configuração idêntica no ambiente publish:

Na instância do autor de AEM:

* Navegue do menu principal até **[!UICONTROL Ferramentas > Operações > Replicação]**.
* Selecionar **Ativar árvore**
* **Caminho** do start: navegar até `/etc/socialconfig/srpc/`
* Cancelar seleção **somente modificada**
* Selecionar **Ativar**

## Atualização do AEM 6.0 {#upgrading-from-aem}

>[!CAUTION]
>
>Se você ativar o ASRP em um site da comunidade publicada, qualquer UGC já armazenado no [JCR](/help/communities/jsrp.md) não estará mais visível, pois não há sincronização de dados entre o armazenamento local e o armazenamento em nuvem.

**`AEM Communities Extension`** foi introduzido anteriormente em AEM 6.0 comunidades sociais como um serviço em nuvem. A partir AEM Comunidades 6.1, nenhuma configuração de nuvem é necessária, basta selecionar ASRP no console [de configuração do](/help/communities/srp-config.md)armazenamento.

Devido à nova estrutura do armazenamento, é necessário seguir as instruções de [atualização](/help/communities/upgrade.md#adobe-cloud-storage) ao atualizar de comunidades sociais para Comunidades.

## Gerenciamento de dados do usuário {#managing-user-data}

Para obter informações sobre *usuários*, perfis *de* usuários e grupos *de* usuários, normalmente inseridos no ambiente de publicação, visite

* [Sincronização do usuário](/help/communities/sync.md)
* [Gerenciamento de usuários e grupos de usuários](/help/communities/users.md)

## Resolução de problemas {#troubleshooting}

### O UGC desaparece após a atualização {#ugc-disappears-after-upgrade}

Se estiver atualizando de um site da comunidade social AEM 6.0, siga as instruções [de](/help/communities/upgrade.md#adobe-cloud-storage)atualização; caso contrário, o UGC parece estar perdido.

### Erros de autenticação {#authentication-errors}

Se estiver recebendo erros de autenticação no URL do data center e o AEM error.log contiver mensagens sobre carimbos de data e hora obsoletos, verifique se a sincronização de hora está ocorrendo.

Use uma ferramenta como o NTP ( [Network Time Protocol, Protocolo de tempo de rede)](https://www.ntp.org/) para sincronizar o tempo de todos os servidores de autor e publicação AEM.

### Novo conteúdo não aparece nas pesquisas {#new-content-does-not-appear-in-searches}

A infraestrutura de armazenamento em nuvem do Adobe usa *uma consistência* eventual para atingir suas metas de dimensionamento e desempenho. Por essa razão, o novo conteúdo não está disponível instantaneamente e leva vários segundos para aparecer nos resultados da pesquisa.

Enquanto o intervalo que afeta uma eventual consistência é monitorado, entre em contato com seu representante de conta se ele levar mais de alguns segundos para que o novo conteúdo apareça nas pesquisas.

### UGC não visível no ASRP {#ugc-not-visible-in-asrp}

Verifique se o ASRP foi configurado para ser o provedor padrão ao verificar a configuração da opção de armazenamento. Por padrão, o provedor de recursos do armazenamento é JSRP, não ASRP.

Em todas as instâncias do autor e publicação AEM, revisite o console Configuração do Armazenamento ou verifique o repositório AEM.

No JCR, se [/etc/socialconfig](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* Não contém um nó [srpc](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) , isso significa que o provedor do armazenamento é JSRP.
* Se o nó srpc existir e contiver a configuração [padrão](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)do nó, as propriedades da configuração padrão definirão o ASRP como o provedor padrão.

