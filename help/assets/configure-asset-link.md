---
title: Configurar o Experience Manager Assets para o Adobe Asset Link
description: Configure o Experience Manager Assets para uso com a extensão do Adobe Asset Link para aplicativos Creative Cloud.
contentOwner: Vishabh Gupta
role: Admin
feature: Asset Management
exl-id: 3a9b44d4-1756-4ad5-91df-df8d53e82193
solution: Experience Manager, Experience Manager Assets
source-git-commit: 6ab943894398733d178f561430d3f391e8722195
workflow-type: tm+mt
source-wordcount: '3059'
ht-degree: 0%

---

# Configurar o Experience Manager Assets para o Adobe Asset Link {#adobe-asset-link}

O [Adobe Asset Link (AAL)](https://www.adobe.com/br/creativecloud/business/enterprise/adobe-asset-link.html) simplifica a colaboração entre profissionais de criação e marketing no processo de criação de conteúdo. Ele conecta o Adobe Experience Manager Assets com os aplicativos de desktop da Creative Cloud Adobe InDesign, Adobe Photoshop e Adobe Illustrator. O painel Adobe Asset Link permite que os criadores acessem e modifiquem o conteúdo armazenado no AEM Assets sem sair dos aplicativos de criação mais conhecidos.

Para configurar o Experience Manager Assets para ser usado com o Asset Link, implemente as seguintes tarefas. Use a conta de administrador do Experience Manager para fazer a configuração:

1. Instale os pacotes conforme necessário. Os detalhes estão nos [pré-requisitos](#prerequisites).

1. Configure o Experience Manager [manualmente](#manual-configuration) ou usando um [pacote](#configure-using-package).

1. Para mapear usuários licenciados do Creative Cloud com usuários do Experience Manager, gerencie o [controle de acesso do usuário](#user-access).

1. Crie o [índice de consulta personalizado](#create-custom-index), configure as [representações FPO](/help/assets/configure-fpo-renditions.md) para o InDesign, configure a [integração com o Adobe Stock](/help/assets/aem-assets-adobe-stock.md) e configure a [pesquisa visual ou de semelhança](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html?lang=pt-BR#configvisualsearch).

## Pré-requisitos e suporte para várias funcionalidades {#prerequisites}

Instale o pacote de serviços e o pacote apropriados, conforme necessário. Consulte os seguintes requisitos para cada versão do Experience Manager e para recursos específicos.

| Recurso do Assets | Versão do Experience Manager e requisitos de suporte |
|--- |--- |
| O Asset Link funciona por padrão | Experience Manager 6.5 e 6.5.2 ou posterior. </br> Experience Manager 6.4.4 e 6.4.6 ou posterior. </br> A Adobe recomenda instalar o [Experience Manager service pack (SP)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=pt-BR) mais recente antes de usar o AAL. |
| O Asset Link funciona após instalar um pacote | Para o Experience Manager 6.4.0 - 6.4.3, instale o pacote [adobe-asset-link-support](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support). |
| Integração do Adobe Stock | Experience Manager 6.4.2 ou posterior |
| Pesquisa visual ou por semelhança | Experience Manager 6.5.0 ou posterior |


## Configurar o Experience Manager usando o pacote de configuração {#configure-using-package}

A Adobe recomenda instalar o pacote de configuração [adobe-asset-link-config](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/adobe-asset-link-config) para automatizar a maioria das tarefas de configuração, seguido de algumas tarefas manuais. Como alternativa, você pode [configurar manualmente](#manual-configuration).

>[!CAUTION]
>
>Se a instância do Experience Manager estiver configurada para logon de usuário com contas do Adobe IMS, não use o pacote de configuração. Em vez disso, [configure](#manual-configuration) manualmente sua instância do Experience Manager.

1. Para abrir o Gerenciador de Pacotes, na interface da Web do Experience Manager, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Compartilhamento de Pacotes]**. Instalar pacote `adobe-asset-link-config`.

1. Acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**. Localize a configuração do **[!UICONTROL Provedor de IMS do Adobe Granite OAuth]** e clique nele para editá-lo.

   Defina as propriedades a seguir e salve as alterações.

   * [!UICONTROL Mapeamentos de grupos]: deixe vazio, a menos que seja desejado. Para obter detalhes, consulte [Mapeamento de grupos](#group-mapping).
   * [!UICONTROL Organização]: insira a ID da organização que você está usando na Adobe Admin Console. Para obter mais informações sobre IDs de organização, consulte [Criar grupo de usuários](https://helpx.adobe.com/br/enterprise/using/create-aal-user-group.html).

1. Localize a configuração do **[!UICONTROL Manipulador de autenticação do portador do Adobe Granite]** e clique nele para editá-la.

   Adicionar IDs de cliente do **[!UICONTROL InDesignAem2]** à propriedade de configuração **[!UICONTROL IDs de cliente do OAuth]** permitidas.


## Configurar o Experience Manager manualmente {#manual-configuration}

Configure manualmente o Experience Manager se optar por não usar um pacote de configuração ou se a implantação do Experience Manager estiver configurada para oferecer suporte ao logon do usuário com contas do Adobe IMS.

Para configurar manualmente o Experience Manager:

1. Para acessar o gerenciador de configurações, acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**. Selecione **[!UICONTROL OSGi]** > **[!UICONTROL Configuração]** no menu na parte superior.

1. Localize a configuração do **[!UICONTROL Provedor de IMS do Adobe Granite OAuth]** e clique nele para editá-lo.

   Defina a configuração a seguir e clique em **[!UICONTROL Salvar]**.

   * [!UICONTROL Ponto de Extremidade de Autorização]: ` https://ims-na1.adobelogin.com/ims/authorize/v1`
   * [!UICONTROL Ponto de Extremidade do Token]: ` https://ims-na1.adobelogin.com/ims/token/v1`
   * [!UICONTROL Ponto de Extremidade do Perfil]: ` https://ims-na1.adobelogin.com/ims/profile/v1`
   * [!UICONTROL URL de validação]: ` https://ims-na1.adobelogin.com/ims/validate_token/v1`
   * [!UICONTROL Organização]: definida como a ID da organização na [Adobe Admin Console](https://adminconsole.adobe.com/).
   * [!UICONTROL Mapeamentos de grupos]: deixe vazio a menos que você tenha um caso especial. Para obter detalhes, consulte [Mapeamento de grupos](#group-mapping).

1. Localize a configuração do **[!UICONTROL Manipulador de autenticação do portador do Adobe Granite]** e clique nele para editá-la.

   Adicione as seguintes IDs do cliente à propriedade de configuração **[!UICONTROL IDs do cliente OAuth permitidas]**: `InDesignAem2, cc-europa-desktop_0_1, cc-europa-desktop_1_0, cc-europa-desktop_2_0, cc-europa-desktop_3_0, cc-europa-desktop_4_0, cc-europa-desktop_5_0, cc-europa-desktop_6_0, cc-europa-desktop_7_0, cc-europa-desktop_8_0, cc-europa-desktop_9_0, and cc-europa-desktop_10_0`.

   Para adicionar cada `Client ID`, clique em `+`. Clique em **[!UICONTROL Salvar]** depois de adicionar todas as IDs.

1. Na configuração do **[!UICONTROL Aplicativo e Provedor do Adobe Granite OAuth]**, inspecione as **[!UICONTROL instâncias existentes do Aplicativo e Provedor do Adobe Granite OAuth]**. Se você localizar uma instância com o valor `Config ID` de `ims`, use-a para obter as instruções deste procedimento. Caso contrário, clique em `+` para criar uma instância de configuração. Defina os seguintes valores de propriedade e clique em **[!UICONTROL Salvar]**.

   * [!UICONTROL ID do cliente]: não alterar
   * [!UICONTROL Segredo do cliente]: não alterar
   * [!UICONTROL ID de configuração]: ` ims`
   * [!UICONTROL Escopo]: `AdobeID, OpenID, read_organizations` (outros valores também podem estar na configuração)
   * [!UICONTROL Identificação do Provedor]: ` ims`
   * [!UICONTROL Criar usuários]: ` Checked`
   * [!UICONTROL Propriedade de ID do Usuário]: `Email` para configuração recém-criada. Caso contrário, não altere.

1. Localize a configuração do **[!UICONTROL Manipulador de sincronização padrão do Apache Jackrabbit Oak]** com o **[!UICONTROL Nome do Manipulador de sincronização]** `ims` e clique nele para editá-lo.

   Defina as propriedades de configuração a seguir e clique em **[!UICONTROL Salvar]**.

   * [!UICONTROL Hora de Expiração do Usuário e Expiração da Associação do Usuário]: tempo em minutos seguido por &#39;m&#39; sem espaço. Por exemplo, `15m` por 15 minutos. Para obter detalhes, consulte [Mapeamento de grupos](#group-mapping).
   * [!UICONTROL Associação automática de usuário]: não alterar
   * [!UICONTROL Associação Dinâmica de Usuário]: ` Deslect`

1. Localize a configuração do **[!UICONTROL Manipulador de autenticação OAuth do Adobe Granite]** e clique nele para editá-lo. Sem fazer alterações, clique em **[!UICONTROL Salvar]**.

1. Para ajustar a prioridade relativa do manipulador de autenticação do portador, no CRXDE, navegue até `/apps/system/config`. Localize `com.adobe.granite.auth.oauth.impl.BearerAuthenticationHandler.config` e abra sua configuração. No final, adicione `service.ranking=I"-10"`. Salve as alterações.

   >[!NOTE]
   >
   >Cada solicitação autenticada com um token de portador incorre na sobrecarga de três chamadas para o Adobe IMS, na sincronização de usuários e na criação de um token de logon no Experience Manager. Para superar essa sobrecarga, o Adobe Asset Link captura o token de logon retornado na resposta do Experience Manager e o envia com solicitações subsequentes. Para que esse processo funcione, a prioridade relativa do manipulador de autenticação do portador deve ser ajustada.

1. (Opcional) Se os usuários do Experience Manager tiverem nomes de domínio em maiúsculas ou minúsculas mistas nas IDs de email, selecione **[!UICONTROL Alterar usuário de bloqueio para minúsculas]** em **[!UICONTROL Configurações da plataforma Adobe Granite ACP]** no Console da Web do Experience Manager.

## Configuração adicional após a migração para perfis empresariais {#configure-migration-activity}

Os usuários do Adobe Asset Link podem se conectar ao Experience Manager para permitir o logon no IMS na organização principal do Creative Cloud para corporações (CCE). O Experience Manager usa as IDs do cliente para identificar a organização IMS permitida. Após a migração para Perfis comerciais, é necessário configurar a ID do cliente e a Chave secreta para a organização IMS no Experience Manager para o Manipulador de autenticação do portador. Para obter mais informações sobre Perfis comerciais, consulte [introdução aos Perfis Adobe](https://helpx.adobe.com/br/enterprise/kb/introducing-adobe-profiles.html).

A configuração adicional é necessária somente se você estiver usando organizações diferentes do Adobe IMS para Experience Manager e Creative Cloud para corporações (CCE), e uma relação de confiança de domínio for estabelecida entre essas duas organizações.

>[!NOTE]
>
>* A correção para Perfis Comerciais é fornecida no Experience Manager 6.5.11.0.
>* A configuração existente continua a funcionar se você estiver usando a mesma organização do Adobe IMS com o Experience Manager e o CCE.


**Pré-requisitos**

1. Uma instância ativa e em execução do Experience Manager com Autenticação do Portador configurada para AAL.
1. Instale o seguinte pacote (Service Pack 11) na sua instância do Experience Manager 6.5.

   [Baixar Experience Manager 6.5.11.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. Contate o [!UICONTROL Suporte ao Cliente] para obter a ID do Cliente e a Chave Secreta para a Autenticação do Portador da sua Organização IMS.

Veja a seguir as configurações adicionais necessárias após a migração para Perfis comerciais:

1. Em **[!UICONTROL Provedor de Configuração IMS do Adobe Granite OAuth]** (`com.adobe.granite.auth.ims.impl.ImsConfigProviderImpl`), defina:

   * ID da Configuração do OAuth (`oauth.configmanager.ims.configid`): `ims` (Verifique uma vez, você pode tê-lo configurado)

   * Entidade Proprietária do IMS (`ims.owningEntity`): Sua ID da Organização IMS

   ![ID de Configuração IMS](assets/bearer-authentication1.png)

1. Abra a configuração do **[!UICONTROL Manipulador de Autenticação do Portador]** e adicione a ID do Cliente obtida do [!UICONTROL Suporte ao Cliente] à lista de **[!UICONTROL IDs de cliente OAuth permitidas]**.

   ![Adicionar ID do Cliente](assets/add-clientid-bearer-auth.png)

1. Abra a configuração do **[!UICONTROL Provedor e Aplicativo OAuth do Adobe Granite]** e adicione a **[!UICONTROL ID do Cliente]** e o **[!UICONTROL Segredo do Cliente]** (Chave Secreta) obtidos do Suporte ao Cliente.

   Verifique se o campo **[!UICONTROL ID da Configuração]** (`oauth.config.id`) contém o mesmo valor fornecido no campo **[!UICONTROL ID da configuração OAuth]** (`oauth.configmanager.ims.configid`) acima.

   ![Verificar ID do Cliente](assets/clientid-secretkey.png)

1. Abra a configuração do **[!UICONTROL Pré-processador de Token do Exchange do Cluster IMS do Adobe Granite]** e defina-a como `enable`.

## Gerenciar o controle de acesso do usuário {#user-access}

Esta seção descreve como gerenciar usuários e seu acesso ao repositório do Experience Manager.

### Mapeamento de grupo {#group-mapping}

O mapeamento de grupos determina como os grupos no Experience Manager correspondem aos grupos no Adobe IMS. Ele desempenha uma função importante em como os usuários do Adobe Asset Link recebem permissão para acessar o Experience Manager Assets.

Quando usado com o Adobe Asset Link, o Experience Manager delega funções de gerenciamento de usuários ao Adobe IMS. Ele cria automaticamente usuários e grupos que correspondem a usuários e grupos no Adobe IMS. Além disso, sincroniza usuários, grupos e associações de grupo no Experience Manager para corresponder aos do Adobe IMS.

Por exemplo, considere um cenário em que os usuários do Adobe Asset Link sejam membros do grupo Adobe IMS assetlink-users. Nesse caso, um grupo sincronizado chamado assetlink-users é criado no Experience Manager quando um usuário desse grupo do Adobe IMS se conecta ao Adobe Asset Link pela primeira vez. Cada novo usuário no grupo Adobe IMS é adicionado ao grupo correspondente no Experience Manager quando ele se conecta ao Experience Manager por meio do Adobe Asset Link pela primeira vez.

Os grupos no Experience Manager que correspondem a e são sincronizados com grupos no Adobe IMS podem receber acesso diretamente ou tornando-os membros de outro grupo. Este é um exemplo de como as permissões podem ser gerenciadas.

![exemplos de grupo](assets/group-examples.png)

As seguintes regras se aplicam aos mapeamentos de grupo no Experience Manager:

* Verifique se a propriedade **[!UICONTROL Mapeamentos de grupo]** na configuração do **[!UICONTROL Provedor de IMS OAuth do Adobe Granite]** está em branco.
* A associação do grupo de usuários do Adobe Asset Link é avaliada quando o usuário é autenticado e o período na propriedade **[!UICONTROL Tempo de expiração do usuário]** na configuração do **[!UICONTROL Manipulador de sincronização padrão do Apache Jackrabbit Oak]** expira. Atualmente, os usuários podem ser adicionados e removidos de grupos no Experience Manager para sincronizar com o que é encontrado no Adobe IMS.
* Evite conflitos de nome de grupo. Verifique se os nomes usados para grupos criados no Adobe IMS (para gerenciar usuários) são diferentes de todos os nomes de grupos do sistema Experience Manager.

  Por exemplo, verifique se eles são diferentes do grupo `dam-users` e dos grupos criados pelo administrador do Experience Manager.

  Um grupo IMS da Adobe cujo nome conflita com o nome de um grupo de sistema do Experience Manager ou de um grupo criado manualmente não é usado para controlar permissões de usuário.
* Se um usuário do Adobe IMS se conectar a uma instância do Experience Manager, na qual o nome do usuário entra em conflito com um usuário do Experience Manager criado anteriormente, o usuário do Adobe IMS receberá outro nome com números adicionados para torná-lo exclusivo.

**Configurar controle de acesso pela primeira vez**

Os usuários que se conectam por meio do Adobe Asset Link só podem visualizar e interagir com ativos depois que recebem a permissão necessária. A seção [Mapeamento de grupo](#group-mapping) acima discute como os grupos de usuários são criados no Experience Manager, que correspondem a e são sincronizados com os grupos de usuários em sua organização no Adobe IMS. É recomendável que os administradores do Experience Manager usem esses grupos para gerenciar o controle de acesso para usuários do Adobe Asset Link.

Para cada grupo do Experience Manager que é sincronizado com um grupo do Adobe IMS (usado para gerenciar o controle de acesso do usuário):

1. Verifique se o grupo tem um membro que possa ser usado para uma conexão inicial do Adobe Asset Link.
1. Use esse usuário para fazer logon no Adobe Asset Link e se conectar ao Experience Manager. Espera-se que essa conexão falhe.
1. No Experience Manager, localize o grupo que corresponde ao grupo no Adobe IMS e conceda a ele o controle de acesso desejado. Por exemplo, o novo grupo se torna membro do grupo dam-users.
1. Feche o Adobe Asset Link e reinicie o aplicativo do Creative Cloud.
1. Para verificar se o usuário tem o acesso esperado, reabra o Adobe Asset Link.

Depois que essas etapas forem executadas, outros usuários no mesmo grupo poderão se conectar ao Experience Manager com o Adobe Asset Link na primeira tentativa. Eles têm automaticamente as mesmas permissões que os outros usuários no grupo.

## Gerenciar usuários do Experience Manager para o Adobe Asset Link {#manage-users}

Os usuários do Adobe Asset Link podem se conectar ao Experience Manager quando estão conectados ao aplicativo Creative Cloud. Essa autenticação usa a tecnologia Adobe IMS e cria informações do usuário no Experience Manager, se ela não existir. É comum que os clientes corporativos da Experience Manager gerenciem seus usuários com um provedor de identidade externo integrado ao Experience Manager. Os provedores de identidade incluem o Adobe IMS e outros produtos que usam os protocolos SAML e LDAP. Como alternativa, os usuários podem ser criados e gerenciados localmente no Experience Manager.

Os usuários que se conectam ao Experience Manager a partir do Adobe Asset Link não têm conflito com as informações existentes do usuário armazenadas no Experience Manager a partir do logon direto anterior, se:

* Todos os nomes de usuários usados para logon direto no Experience Manager são diferentes dos nomes de usuários usados no Adobe IMS para logon no Creative Cloud.
* O Adobe IMS é usado como o provedor de identidade para logon direto na Experience Manager.
* Os usuários se conectam ao Experience Manager pelo Adobe Asset Link antes de fazer logon direto no Experience Manager com a mesma conta.


Por outro lado, as informações do usuário criadas como resultado do logon direto na Experience Manager devem ser atualizadas para funcionar com o Adobe Asset Link, nos seguintes cenários:

* O mesmo nome de usuário, como o endereço de email do usuário, é usado para a conta no Creative Cloud, que usa o Adobe IMS, e para a conta em um provedor de identidade externo diferente do Adobe IMS.
* O mesmo nome de usuário é usado para a conta no Creative Cloud e para uma conta local do Experience Manager.
* As contas do Creative Cloud no Adobe IMS são Federated IDs, que são atendidas pelo mesmo provedor de identidade externo que é integrado ao Experience Manager para logon direto.

Os usuários criados por meio desses cenários não têm uma propriedade necessária para usuários, que são sincronizados com o Adobe IMS.

Para atualizar esses usuários no Experience Manager para trabalhar com o Adobe Asset Link:

1. No console da Web do Experience Manager, localize a configuração **[!UICONTROL Apache Jackrabbit Oak External PrincipalConfiguration]** e clique em para editá-la. Desmarque a caixa de seleção **[!UICONTROL Proteção de identidade externa]** e clique em **[!UICONTROL Salvar]**.
1. Para acessar a interface de Gerenciamento de Usuários no Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**. Selecione o usuário que deseja atualizar e anote o final do caminho de URL do navegador para esse usuário, começando com `/home/users`. Como alternativa, você pode pesquisar pelo nome de usuário no CRXDE. Um exemplo de caminho de usuário: `/home/users/x/xTac082TDh-guJzzG7WM`.
1. No CRXDE, navegue até o caminho do usuário, selecione o nó do usuário e visualize as propriedades do nó selecionando a guia **[!UICONTROL Propriedades]** na área inferior central. Este nó tem um valor de propriedade `jcr:primaryType` de `rep:User`.
1. Na parte inferior da área de guia **[!UICONTROL Propriedades]**, insira um valor `Name` de `rep:externalId`, um valor `Type` de `String` e um valor `Value` de `rep:authorizableId`;`ims`, onde `rep:authorizableId` é o valor da propriedade `rep:authorizableId` do nó. (Um ponto e vírgula é usado sem espaços para separar o valor `rep:authorizableId` de `ims`.)
1. Clique no botão **[!UICONTROL Adicionar]** à direita da nova entrada e clique em **[!UICONTROL Salvar tudo]**.
1. Repita as etapas de 2 a 5 para qualquer outro usuário que queira atualizar para trabalhar com o Adobe Asset Link.
1. No console da Web do Experience Manager, localize a configuração **[!UICONTROL Apache Jackrabbit Oak External PrincipalConfiguration]** e clique em para editá-la. Desmarque a caixa de seleção **[!UICONTROL Proteção de identidade externa]** e clique em **[!UICONTROL Salvar]**.

>[!NOTE]
>
>Se os serviços não forem restaurados em alguns minutos, reinicie o Experience Manager para permitir autenticações bem-sucedidas.

Após essa alteração, um usuário atualizado do Experience Manager pode se conectar ao Adobe Asset Link e continuar a usar o método de logon direto no Experience Manager usado antes da atualização. Na autenticação bem-sucedida com o Adobe IMS, as informações do perfil do usuário do Experience Manager são sincronizadas com o perfil do usuário no Adobe IMS.

Há um método pelo qual uma migração em massa de vários usuários do Experience Manager pode ser executada para permitir que eles trabalhem com o Adobe Asset Link. Entre em contato com o Adobe Care para obter mais informações e assistência para ativar essa opção.

Como alternativa às etapas, em determinadas circunstâncias, um usuário do Adobe Asset Link pode receber acesso rápido ao Experience Manager. Nesses casos, as informações pré-existentes do usuário são encontradas e excluídas com o Gerenciamento de usuários do Experience Manager ou o Experience Manager CRXDE antes da conexão com o Adobe Asset Link. As novas informações do usuário são criadas no Experience Manager após a conexão. Use essa abordagem somente se tiver certeza de que não há dados importantes adicionados como secundários do nó do usuário. Esses dados extras são qualquer nó filho do nó do usuário que não seja dos nós `tokens`, `preferences`, `profile`, `profiles`, `profiles/public` e `rep:policy/*`.

## Fluxo de trabalho de início automático para processar ativos condicionalmente {#auto-start-workflow}

No Experience Manager 6.4 e Experience Manager 6.5, os administradores podem configurar fluxos de trabalho para executar e processar ativos automaticamente com base em condições predefinidas.

A configuração é útil para usuários e profissionais de marketing da linha de negócios, por exemplo, criar um fluxo de trabalho personalizado em algumas pastas específicas. Digamos que todos os ativos da sessão de fotos de uma agência possam ter uma marca d&#39;água ou que todos os ativos carregados por um freelancer possam ser processados para criar representações específicas.

Para obter mais informações e para a configuração do Experience Manager, consulte [executar fluxo de trabalho automaticamente em ativos](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html?lang=pt-BR#auto-execute-workflow-on-some-assets).


## Criar um índice personalizado nas versões do Experience Manager 6.4.x {#create-custom-index}

O Experience Manager contém índices que são usados para consulta. Crie o índice personalizado a seguir para a versão especificada. O Experience Manager 6.5.0 contém esse índice por padrão. O Adobe Asset Link exige esse índice para determinar quais ativos um usuário fez check-out.

1. No CRXDE, localize o nó `/oak:index`. Crie um nó chamado `cqDrivelock` e defina seu `Type` como `oak:QueryIndexDefinition`.

1. Adicione as seguintes propriedades ao novo nó e salve as alterações:

   * `Name: type; Type: string; Value: property`

   * `Name: propertyNames; Type: Name[] (click the "Multi" button); Value: cq:drivelock`


## Configurar pesquisa visual ou por semelhança {#configure-visual-similarity-search}

O recurso de pesquisa visual permite pesquisar ativos visualmente semelhantes no repositório do AEM Assets, usando o painel Adobe Asset Link. A funcionalidade está disponível na versão 6.5.0 ou posterior e somente os ativos indexados são pesquisados. Para obter mais informações, consulte [como configurar a pesquisa visual](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html?lang=pt-BR#configvisualsearch).

## Gerar para representações somente de posicionamento para o Adobe InDesign {#fpo-renditions}

O Experience Manager fornece representações usadas somente para posicionamento (FPO). Essas representações FPO têm um tamanho de arquivo pequeno, mas têm a mesma proporção. Se uma representação FPO não estiver disponível para um ativo, a Adobe InDesign usará o ativo original. Esse mecanismo de fallback garante que o workflow criativo continue sem interrupções. Para obter mais informações, consulte [gerar representações FPO](/help/assets/configure-fpo-renditions.md).


## Integrar ao Adobe Stock {#adobe-stock-integration}

As organizações integram suas contas do Adobe Stock com a Experience Manager Assets. Ele ajuda os profissionais de marketing a disponibilizar fotos, vetores, ilustrações, vídeos, modelos e ativos 3D licenciados e de alta qualidade e isentos de royalties para seus projetos criativos e de marketing. Os profissionais de criação podem usar esses ativos usando o painel Link de ativos.

Para integrar com o Adobe Stock, consulte [Adobe Stock assets in Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md). O Experience Manager 6.4.2 ou posterior é necessário para a integração com o Adobe Stock.


## Solucionar problemas relacionados ao Experience Manager {#troubleshoot}


Se você enfrentar problemas ao configurar ou usar o Adobe Asset Link, tente o seguinte:

* Verifique se a implantação atende aos pré-requisitos. Especificamente, verifique se os pacotes ou pacotes de recursos apropriados estão instalados.
* Entre em contato com o parceiro ou integrador de sistemas de sua organização.
* Se os usuários do Creative Cloud não conseguirem verificar os ativos com check-out, verifique se há letras maiúsculas e minúsculas dos nomes de domínio nas IDs de email. Para corrigir, consulte [configuração manual](#manual-configuration).
* Para obter mais informações, consulte [solucionar problemas do Asset Link](https://helpx.adobe.com/br/enterprise/kb/asset-link-troubleshooting.html).


>[!MORELIKETHIS]
>
>* [Sobre o Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html)
>* [Usar o Asset Link no aplicativo de desktop Creative Cloud e gerenciar ativos](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html)
>* [Configurar Adobe Experience Manager Assets as a Cloud Service](https://helpx.adobe.com/br/enterprise/using/configure-aem-assets-for-asset-link.html).
