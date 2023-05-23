---
title: Tipos de endpoints
seo-title: Types of endpoints
description: Saiba mais sobre os diferentes tipos de endpoints do.
seo-description: Learn about the different types of endpoints.
uuid: c899245c-14cc-4035-9440-95a5b6c1e47f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8fe572e0-8a53-4129-940f-3fdb990073fe
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Tipos de endpoints {#types-of-endpoints}

Antes de um serviço ser usado, você deve configurar e habilitar um endpoint. Um ponto de extremidade especifica como um serviço deve ser chamado.

>[!NOTE]
>
>No Workbench, os endpoints são chamados de pontos iniciais.

Os seguintes tipos de endpoints podem ser adicionados aos serviços. Nem todos os serviços dão suporte a todos os endpoints:

**Email:** Permite que um usuário chame um serviço, enviando uma mensagem de email com um ou mais anexos de arquivo para uma conta de email especificada. Antes de configurar um endpoint de email, você deve configurar as contas de email necessárias. (Consulte Configuração de endpoints de email.)

**Pasta monitorada:** Permite que um usuário chame um serviço, colocando um arquivo em uma pasta, que é verificada em um intervalo definido. (Consulte Configuração de pontos de extremidade de pastas monitoradas.)

**Gerenciador de tarefas:** Permite que um usuário do Workspace chame o serviço.

**Comunicação remota:** Permite que um aplicativo criado com o Flex chame o serviço usando a comunicação remota de formulários AEM (obsoleto para formulários AEM). Um ponto de extremidade remoto é criado automaticamente para cada serviço ativado. Um destino do Flex que tem o mesmo nome do endpoint é criado, e os clientes Flex podem criar objetos remotos que apontam para esse destino para chamar operações no serviço relevante.

**SOAP:** Permite que um aplicativo cliente desenvolvido com as APIs de programação de formulários AEM chame o serviço usando o modo SOAP. Um ponto de extremidade SOAP é criado automaticamente para cada serviço ativado.

**observação**: *A segurança pode ser removida dos documentos de segurança de documentos quando o endpoint SOAP é usado ao visualizar os documentos no Adobe Acrobat ou no Adobe Reader. Para obter detalhes sobre como desativar pontos de extremidade SOAP em documentos do LCRM, consulte [Desabilitar pontos de extremidade SOAP para documentos de segurança de documentos](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** Permite que um aplicativo cliente desenvolvido com as APIs de programação de formulários AEM chame o serviço usando o modo Enterprise JavaBeans (EJB). Um terminal EJB é criado automaticamente para cada serviço ativado.

**WSDL:** Permite que um aplicativo cliente desenvolvido com as APIs de programação de formulários AEM chame o serviço usando a WSDL (Web Service Definition Language). A página Configurações principais contém uma opção para habilitar a geração de WSDL para todos os serviços que fazem parte de formulários AEM. (Consulte Definir configurações gerais de formulários AEM.)

**REST:** Os processos criados no Workbench podem ser configurados para que você possa chamá-los por meio de solicitações de Transferência de estado representacional (REST). As solicitações REST são enviadas de páginas de HTML. Ou seja, você pode chamar um processo de formulários AEM diretamente de uma página da Web usando uma solicitação REST.

Os pontos de extremidade Email, TaskManager, Watched Folder e Remoting expõem apenas uma operação específica do serviço. A adição desses endpoints requer uma segunda etapa de configuração para selecionar um método para chamar o serviço, definir parâmetros de configuração e especificar mapeamentos de parâmetros de entrada e saída.
