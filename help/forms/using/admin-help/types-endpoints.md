---
title: Tipos de pontos finais
seo-title: Tipos de pontos finais
description: Saiba mais sobre os diferentes tipos de endpoints.
seo-description: Saiba mais sobre os diferentes tipos de endpoints.
uuid: c899245c-14cc-4035-9440-95a5b6c1e47f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8fe572e0-8a53-4129-940f-3fdb990073fe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# Tipos de pontos finais {#types-of-endpoints}

Antes que um serviço possa ser usado, você deve configurar e ativar um terminal. Um endpoint especifica como um serviço deve ser chamado.

>[!NOTE]
>
>No Workbench, os pontos de extremidade são chamados de pontos de start.

Os seguintes tipos de endpoints podem ser adicionados aos serviços. Nem todos os serviços suportam todos os pontos de extremidade:

**Email:** permite que um usuário chame um serviço enviando uma mensagem de email com um ou mais anexos de arquivo para uma conta de email especificada. Antes de configurar um terminal de email, configure as contas de email necessárias. (Consulte Configurar pontos de extremidade de email.)

**Pasta assistida:** permite que um usuário chame um serviço colocando um arquivo em uma pasta, que é digitalizada em um intervalo definido. (Consulte Configuração de pontos de extremidade de pasta monitorados.)

**Gerenciador de tarefas:** permite que um usuário do Workspace chame o serviço.

**Remoção:** permite que um aplicativo criado com a Flex chame o serviço usando (obsoleto para formulários AEM) AEM Remoção de formulários. Um terminal remoto é criado automaticamente para cada serviço ativado. É criado um destino Flex com o mesmo nome que o ponto de extremidade, e os clientes Flex podem criar objetos remotos que apontam para esse destino para chamar operações no serviço relevante.

**SOAP:** permite que um aplicativo cliente desenvolvido usando as APIs de programação de formulários AEM chame o serviço usando o modo SOAP. Um terminal SOAP é criado automaticamente para cada serviço ativado.

**observação**:  *A segurança pode ser removida dos documentos de segurança do documento quando o terminal SOAP é usado durante a visualização dos documentos no Adobe Acrobat ou Adobe Reader. Para obter detalhes sobre como desativar os pontos de extremidade SOAP em seus documentos LCRM, consulte [Desativar pontos de extremidade SOAP para documentos de segurança do documento](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** permite que um aplicativo cliente desenvolvido usando as APIs de programação de formulários AEM chame o serviço usando o modo Enterprise JavaBeans (EJB). Um terminal EJB é criado automaticamente para cada serviço ativado.

**WSDL:** permite que um aplicativo cliente desenvolvido usando as APIs de programação de formulários AEM chame o serviço usando a WSDL (Web Service Definition Language). A página Configurações principais contém uma opção para permitir a geração de WSDL para todos os serviços que fazem parte de formulários AEM. (Consulte Configurar configurações gerais AEM formulários.)

**REST:** Os processos criados no Workbench podem ser configurados para que você possa invocá-los por meio de solicitações de transferência de estado de representação (REST). As solicitações REST são enviadas de páginas HTML. Ou seja, você pode invocar um processo de formulários AEM diretamente de uma página da Web usando uma solicitação REST.

Os pontos finais Email, TaskManager, Pasta assistida e Remoto expõem apenas uma operação específica do serviço. A adição desses pontos finais requer uma segunda etapa de configuração para selecionar um método para chamar o serviço, definir parâmetros de configuração e especificar mapeamentos de parâmetros de entrada e saída.
