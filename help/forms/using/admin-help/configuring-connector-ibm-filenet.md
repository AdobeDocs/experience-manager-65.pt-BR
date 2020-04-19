---
title: Configurando o Connector para IBM FileNet
seo-title: Configurando o Connector para IBM FileNet
description: Saiba como configurar o Connector para IBM FileNet para permitir a comunicação entre formulários AEM e IBM FileNet.
seo-description: Saiba como configurar o Connector para IBM FileNet para permitir a comunicação entre formulários AEM e IBM FileNet.
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Configurando o Connector para IBM FileNet {#configuring-connector-for-ibm-filenet}

O Connector for IBM FileNet permite a comunicação entre formulários AEM e IBM FileNet. Para obter informações adicionais de plano de fundo, consulte &quot;Conectores para ECM&quot; na Referência [de](https://www.adobe.com/go/learn_aemforms_services_63)serviços.

>[!NOTE]
>
>Em versões anteriores, os ativos podiam ser armazenados em um repositório ECM. Nesta versão, os ativos são armazenados no repositório nativo de formulários do AEM e os serviços do Provedor de repositório foram descontinuados. A migração de ativos de um repositório ECM para o repositório de formulários AEM é feita quando você faz uma atualização para formulários AEM. Para obter mais informações, consulte o Guia de atualização de formulários do AEM para seu servidor de aplicativos.

## Configurar a conexão com o mecanismo de conteúdo {#configure-the-connection-to-the-content-engine}

O IBM FileNet P8 Content Engine fornece serviços de software para gerenciar conteúdo corporativo e objetos comerciais definidos pelo cliente em repositórios de conteúdo FileNet.

1. No console de administração, clique em Serviços > Conector para IBM FileNet.
1. Na caixa URL do mecanismo de conteúdo, insira o URL de conexão completo. Por exemplo:

   Se você estiver usando o FileNet Content Engine 4.x com transporte CEWS, digite:

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   Se você estiver usando o FileNet Content Engine 4.x com transporte EJB, compatível apenas com WebLogic, informe:

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. Na lista do Esquema de Proteção Credencial, selecione um destes níveis de proteção:

   * **Limpar:** Envia credenciais pela rede em um modo desprotegido
   * **Simétrica:** Envia credenciais criptografadas pela rede

1. Na caixa Local do arquivo de criptografia, digite o caminho para o arquivo de criptografia:

   * Se você selecionou Limpar como esquema de proteção de credenciais, essa palavra-chave e seu valor serão ignorados.
   * Se você selecionou Simétrica como esquema de proteção de credenciais, o caminho inserido aponta para o local de um arquivo de criptografia no servidor de formulários que contém as chaves criptográficas a serem usadas.

1. Na caixa Armazenamento de objetos padrão, digite o conector de armazenamento de objetos ao qual os formulários AEM se conectam por padrão.
1. Na caixa Nome de usuário, digite o nome de usuário de um usuário que tenha direitos de acesso ao armazenamento de objetos padrão especificado na etapa anterior.
1. Na caixa Senha, digite a senha do usuário e clique em Salvar.

## Definir as configurações do mecanismo de processo {#configure-the-process-engine-settings}

O Connector for IBM FileNet contém o Process Engine Connector for IBM FileNet Service, que é usado para interagir com o IBM FileNet Process Engine. Você pode definir as configurações para este serviço.

1. No console de administração, clique em Serviços > Conector para IBM FileNet.
1. Para ativar o uso do Process Engine Connector para o serviço IBM FileNet, selecione Usar o Process Engine Connector Service.
1. Na caixa Process Router/Connection Point, digite o nome do host ou endereço IP e o número da porta seguido do nome do roteador do processo. Por exemplo:

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. Na caixa Nome de usuário, digite o nome de usuário usado para conectar-se ao mecanismo de processo.
1. Na caixa Senha, digite a senha usada para conectar-se ao mecanismo de processo e clique em Salvar.

## Validação das configurações de serviço {#validation-of-service-settings}

Se você inserir um nome de usuário ou senha incorretos ao configurar a conexão com o Mecanismo de conteúdo ou as configurações do mecanismo de processo, você obterá os seguintes resultados, dependendo se os serviços estão em execução no momento:

* Se o serviço Provedor de Repositório para IBM FileNet e o Content Repository Connector for IBM FileNet forem interrompidos, quando você salvar as informações de configuração do serviço, nenhum erro será exibido. No entanto, na próxima vez que você start o serviço, uma exceção será lançada e o serviço não será start.
* Se o serviço Provedor de Repositório para IBM FileNet ou o Content Repository Connector for IBM FileNet for iniciado, quando você salvar as informações de configuração do serviço, o serviço tentará validar as informações de credenciais imediatamente. Nesse caso, ocorre um erro e as informações de configuração não são salvas.

## Alterar o provedor de serviço do repositório {#change-the-repository-service-provider}

Você pode configurar qual provedor de serviço de repositório usar com o FileNet. As chamadas de serviço do repositório são delegadas ao provedor configurado.

As opções disponíveis são as seguintes:

**Nome atual do provedor do repositório:** O nome do provedor de serviço do repositório atual

**Provedor de repositório IBM FileNet:** Torna o provedor do repositório FileNet o provedor do repositório. Esta opção foi substituída.

**provedor de repositório:** Torna o provedor de repositório nativo o provedor do repositório

>[!NOTE]
>
>Para selecionar um provedor de serviço de repositório diferente daqueles listados, configure o RepositoryService em Aplicativos e Serviços. <!-- Fix broken link(See Managing Services) -->

1. No console de administração, clique em Serviços > Conector para IBM FileNet.
1. Na área Informações do Provedor de serviço do repositório, selecione o provedor de serviço do repositório alternativo e clique em Salvar.
