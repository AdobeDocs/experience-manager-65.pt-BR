---
title: Tipos de endpoints
description: Saiba mais sobre os diferentes tipos de endpoints do. Diferentes tipos de endpoints, como email, pasta monitorada e muito mais, podem ser adicionados aos serviços.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%
---
# Tipos de endpoints {#types-of-endpoints}

Antes de um serviço ser usado, você deve configurar e habilitar um endpoint. Um ponto de extremidade especifica como um serviço deve ser chamado.

>[!NOTE]
>
>No Workbench, os endpoints são chamados de pontos iniciais.

Os seguintes tipos de endpoints podem ser adicionados aos serviços. Nem todos os serviços dão suporte a todos os endpoints:

**Email:** permite que um usuário chame um serviço ao enviar uma mensagem de email com um ou mais anexos de arquivo para uma conta de email especificada. Antes de configurar um endpoint de email, você deve configurar as contas de email necessárias. (Consulte Configuração de endpoints de email.)

**Pasta monitorada:** permite que um usuário chame um serviço ao colocar um arquivo em uma pasta, que é verificada em um intervalo definido. (Consulte Configuração de pontos de extremidade de pastas monitoradas.)

**TaskManager:** permite que um usuário do Workspace chame o serviço.

**Comunicação remota:** permite que um aplicativo criado com o Flex chame o serviço usando (obsoleto para formulários do AEM) Comunicação remota de formulários do AEM. Um ponto de extremidade remoto é criado automaticamente para cada serviço ativado. Um destino do Flex que tem o mesmo nome do endpoint é criado, e os clientes Flex podem criar objetos remotos que apontam para esse destino para chamar operações no serviço relevante.

**SOAP:** permite que um aplicativo cliente desenvolvido com as APIs de programação de formulários do AEM chame o serviço usando o modo SOAP. Um terminal SOAP é criado automaticamente para cada serviço ativado.

**Observação**: *a segurança pode ser removida dos documentos de segurança de documentos quando o ponto de extremidade do SOAP for usado durante a exibição dos documentos no Adobe Acrobat ou no Adobe Reader. Para obter detalhes sobre como desabilitar pontos de extremidade do SOAP em seus documentos do LCRM, consulte [Desabilitar pontos de extremidade do SOAP para documentos de segurança](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** permite que um aplicativo cliente desenvolvido com as APIs de programação de formulários do AEM chame o serviço usando o modo EJB (Enterprise JavaBeans). Um terminal EJB é criado automaticamente para cada serviço ativado.

**WSDL:** Habilita um aplicativo cliente desenvolvido com as APIs de programação de formulários do AEM a invocar o serviço usando a WSDL (linguagem de definição de serviço Web). A página Configurações principais contém uma opção para habilitar a geração de WSDL para todos os serviços que fazem parte dos formulários do AEM. (Consulte Definir configurações gerais de formulários do AEM.)

**REST:** os processos criados no Workbench podem ser configurados para que você possa chamá-los por meio de solicitações de Transferência de Estado Representacional (REST). As solicitações REST são enviadas de páginas do HTML. Ou seja, você pode chamar um processo de formulários do AEM diretamente de uma página da Web usando uma solicitação REST.

Os pontos de extremidade Email, TaskManager, Watched Folder e Remoting expõem apenas uma operação específica do serviço. A adição desses endpoints requer uma segunda etapa de configuração para selecionar um método para chamar o serviço, definir parâmetros de configuração e especificar mapeamentos de parâmetros de entrada e saída.
