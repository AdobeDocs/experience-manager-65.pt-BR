---
title: Configurando o conector para o IBM FileNet
seo-title: Configuring Connector for IBM FileNet
description: Saiba como configurar o Conector para o IBM FileNet para permitir a comunicação entre os formulários AEM e o IBM FileNet.
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

# Configurando o conector para o IBM FileNet {#configuring-connector-for-ibm-filenet}

O conector para IBM FileNet permite a comunicação entre os formulários AEM e o IBM FileNet. Para obter informações adicionais, consulte &quot;Conectores para ECM&quot; em [Referência de serviços](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Em versões anteriores, os ativos podiam ser armazenados em um repositório ECM. Nesta versão, os ativos são armazenados no repositório nativo de formulários AEM e os serviços do Provedor do repositório foram descontinuados. A migração de ativos de um repositório de ECM para o repositório de formulários AEM é feita ao fazer uma atualização para formulários AEM. Para obter mais informações, consulte o Guia de atualização de formulários AEM para o servidor de aplicativos.

## Configurar a conexão com o mecanismo de conteúdo {#configure-the-connection-to-the-content-engine}

O IBM FileNet P8 Content Engine fornece serviços de software para gerenciar conteúdo corporativo e objetos comerciais definidos pelo cliente em repositórios de conteúdo FileNet.

1. No console de administração, clique em Serviços > Conector para IBM FileNet.
1. Na caixa URL do mecanismo de conteúdo, digite o URL de conexão completo. Por exemplo:

   Se você estiver usando o FileNet Content Engine 4.x com transporte CEWS, digite:

   `cemp:https://ContentEngineHostNameorIP:port/wsi/FNCEWS40DIME?jaasConfigurationName=FileNetP8WSI`

   Se você estiver usando o FileNet Content Engine 4.x com transporte EJB, que é suportado somente no WebLogic, digite:

   `cemp:t3://ContentEngineHostNameorIP:port/FileNet/Engine?jaasConfigurationName=FileNetP8Engine`

1. Na lista Esquema de Proteção de Credenciais, selecione um destes níveis de proteção:

   * **Limpar:** Envia credenciais pela rede em um modo desprotegido
   * **Simétrico:** Envia credenciais criptografadas pela rede

1. Na caixa Local do Arquivo de Criptografia, digite o caminho para o arquivo de criptografia:

   * Se você selecionou Limpar como o esquema de proteção de credencial, essa palavra-chave e seu valor serão ignorados.
   * Se você selecionou Simétrico como esquema de proteção de credencial, o caminho inserido aponta para o local de um arquivo de criptografia no servidor de formulários que contém as chaves criptográficas a serem usadas.

1. Na caixa Armazenamento de objetos padrão, digite o conector de armazenamento de objetos ao qual o AEM Forms se conecta por padrão.
1. Na caixa Nome do Usuário, informe o nome de um usuário que tenha direitos de acesso ao armazenamento de objetos default especificado na etapa anterior.
1. Na caixa Senha, digite a senha do usuário e clique em Salvar.

## Definir as configurações do mecanismo de processo {#configure-the-process-engine-settings}

O conector para IBM FileNet contém o serviço Process Engine Connector for IBM FileNet, que é usado para interagir com o IBM FileNet Process Engine. Você pode definir as configurações para este serviço.

1. No console de administração, clique em Serviços > Conector para IBM FileNet.
1. Para habilitar o uso do Serviço FileNet do Process Engine Connector para IBM, selecione Usar Serviço do Process Engine Connector.
1. Na caixa Process Router/Connection Point, digite o nome do host ou o endereço IP e o número da porta seguido do nome do roteador de processo. Por exemplo:

   `rmi://ProcessEngineHostNameorIP:port/Name`

1. Na caixa Nome do Usuário, digite o nome do usuário usado para conexão com o mecanismo do processo.
1. Na caixa Senha, digite a senha usada para a conexão com o mecanismo de processo e clique em Salvar.

## Validação das configurações de serviço {#validation-of-service-settings}

Se você digitar um nome de usuário ou senha incorretos ao configurar a conexão com o Mecanismo de conteúdo ou as configurações do mecanismo de processo, você obterá os seguintes resultados, dependendo se os serviços estão sendo executados no momento:

* Se o serviço do Provedor do Repositório para o IBM FileNet e o serviço do Conector do Repositório de Conteúdo para o IBM FileNet forem interrompidos, quando você salvar as informações de configuração do serviço, nenhum erro será exibido. No entanto, na próxima vez que você iniciar o serviço, uma exceção será lançada e o serviço não será iniciado.
* Se o serviço do Provedor de Repositório do IBM FileNet ou o Conector de Repositório de Conteúdo do serviço IBM FileNet forem iniciados, quando você salvar as informações de configuração do serviço, o serviço tentará validar as informações de credencial imediatamente. Nesse caso, ocorre um erro e as informações de configuração não são salvas.

## Alterar o provedor de serviços do repositório {#change-the-repository-service-provider}

Você pode configurar qual provedor de serviço de repositório usar com o FileNet. As chamadas de serviço do repositório são delegadas ao provedor configurado.

As opções disponíveis são as seguintes:

**Nome do provedor do repositório atual:** O nome do provedor de serviços de repositório atual

**Provedor de Repositório IBM FileNet:** Torna o provedor do repositório FileNet o provedor do repositório. Essa opção foi substituída.

**provedor do repositório:** Torna o provedor do repositório nativo o provedor do repositório

>[!NOTE]
>
>Para selecionar um provedor de serviços de repositório diferente dos listados, configure Serviço de Repositório em Aplicativos e Serviços. <!-- Fix broken link(See Managing Services) -->

1. No console de administração, clique em Serviços > Conector para IBM FileNet.
1. Na área Informações do Provedor de Serviços do Repositório, selecione o provedor de serviços do repositório alternativo e clique em Salvar.
