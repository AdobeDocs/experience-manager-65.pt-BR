---
title: Configurando o Conector para IBM FileNet
seo-title: Configuring Connector for IBM FileNet
description: Saiba como configurar o Conector para IBM FileNet para permitir a comunicação entre AEM formulários e IBM FileNet.
seo-description: Learn how to configure the Connector for IBM FileNet to enable communication between AEM forms and IBM FileNet.
uuid: 29d4e221-97f7-4cfb-b7e4-75a8289d2604
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: be4994de-12f8-436e-926a-49a6783b006e
exl-id: f4045df5-a35b-41d7-910e-971017148597
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 1%

---

# Configurando o Conector para IBM FileNet {#configuring-connector-for-ibm-filenet}

O conector para IBM FileNet permite a comunicação entre AEM formulários e IBM FileNet. Para obter mais informações de fundo, consulte &quot;Conectores para ECM&quot; em [Referência de serviços](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Em versões anteriores, os ativos podiam ser armazenados em um repositório ECM. Nesta versão, os ativos são armazenados no repositório nativo dos formulários AEM e os serviços do Provedor de Repositório foram descontinuados. A migração de ativos de um repositório ECM para o repositório AEM forms é feita ao executar uma atualização para AEM formulários. Para obter mais informações, consulte o guia de Atualização de formulários AEM para seu servidor de aplicativos.

## Configurar a conexão com o Mecanismo de conteúdo {#configure-the-connection-to-the-content-engine}

O IBM FileNet P8 Content Engine oferece serviços de software para gerenciar conteúdo corporativo e objetos comerciais definidos pelo cliente em repositórios de conteúdo FileNet.

1. No console de administração, clique em Serviços > Conector para IBM FileNet.
1. Na caixa URL do mecanismo de conteúdo , digite o URL de conexão completo. Por exemplo:

   Se estiver usando o FileNet Content Engine 4.x com transporte CEWS, insira:

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   Se você estiver usando o FileNet Content Engine 4.x com transporte EJB, que é suportado somente no WebLogic, informe:

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. Na lista Esquema de Proteção de Credenciais, selecione um destes níveis de proteção:

   * **Limpar:** Envia credenciais pela rede em um modo desprotegido
   * **Simétrica:** Envia credenciais criptografadas pela rede

1. Na caixa Local do arquivo de criptografia, digite o caminho para o arquivo de criptografia:

   * Se você selecionou Limpar como esquema de proteção de credenciais, esta palavra-chave e seu valor serão ignorados.
   * Se você selecionou Simétrica como esquema de proteção de credenciais, o caminho inserido aponta para o local de um arquivo de criptografia no servidor de formulários que contém as chaves criptográficas a serem usadas.

1. Na caixa Armazenamento de objetos padrão, digite o conector do armazenamento de objetos ao qual AEM formulários se conecta por padrão.
1. Na caixa Nome de usuário, digite o nome de usuário de um usuário que tenha direitos de acesso ao armazenamento de objetos padrão especificado na etapa anterior.
1. Na caixa Senha, digite a senha do usuário e clique em Salvar.

## Definir as configurações do mecanismo de processo {#configure-the-process-engine-settings}

O conector para IBM FileNet contém o Process Engine Connector para o serviço IBM FileNet, que é usado para interagir com o IBM FileNet Process Engine. Você pode definir as configurações desse serviço.

1. No console de administração, clique em Serviços > Conector para IBM FileNet.
1. Para habilitar o uso do Process Engine Connector para o serviço IBM FileNet, selecione Usar serviço do Process Engine Connector.
1. Na caixa Process Router/Connection Point, digite o nome do host ou endereço IP e o número da porta seguido do nome do roteador do processo. Por exemplo:

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. Na caixa Nome de usuário, digite o nome de usuário usado para se conectar ao mecanismo de processo.
1. Na caixa Senha, digite a senha usada para se conectar ao mecanismo de processo e clique em Salvar.

## Validação das configurações do serviço {#validation-of-service-settings}

Se você inserir um nome de usuário ou senha incorretos ao definir a conexão com o Mecanismo de conteúdo ou as configurações do mecanismo de processo, você obterá os seguintes resultados, dependendo se os serviços estão em execução no momento:

* Se o serviço do Provedor de Repositório para IBM FileNet e o Conector do Repositório de Conteúdo para o serviço IBM FileNet forem interrompidos, quando você salvar as informações de configuração do serviço, nenhum erro será exibido. No entanto, na próxima vez que você iniciar o serviço, uma exceção será lançada e o serviço não será iniciado.
* Se o serviço Provedor de Repositório para IBM FileNet ou o Conector de Repositório de Conteúdo para o serviço IBM FileNet for iniciado, quando você salva as informações de configuração do serviço, o serviço tenta validar as informações de credencial imediatamente. Nesse caso, ocorre um erro e as informações de configuração não são salvas.

## Alterar o provedor de serviços de repositório {#change-the-repository-service-provider}

Você pode configurar qual provedor de serviço de repositório usar com o FileNet. Chamadas de serviço de repositório são delegadas ao provedor que você configura.

As opções disponíveis são as seguintes:

**Nome do Provedor de Repositório Atual:** O nome do provedor de serviços de repositório atual

**Provedor de Repositório IBM FileNet:** Torna o provedor do repositório FileNet o provedor do repositório. Essa opção foi descontinuada.

**provedor de repositório:** Torna o provedor do repositório nativo o provedor do repositório

>[!NOTE]
>
>Para selecionar um provedor de serviços de repositório diferente daqueles listados, configure o RepositoryService em Aplicativos e Serviços. <!-- Fix broken link(See Managing Services) -->

1. No console de administração, clique em Serviços > Conector para IBM FileNet.
1. Na área Informações do Provedor de Serviços de Repositório, selecione o provedor de serviço de repositório alternativo e clique em Salvar.
