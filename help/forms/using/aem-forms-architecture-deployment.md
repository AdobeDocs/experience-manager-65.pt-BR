---
title: Topologias de arquitetura e implantação para AEM Forms
seo-title: Topologias de arquitetura e implantação para AEM Forms
description: Detalhes da arquitetura para AEM Forms e topologias recomendadas para clientes do AEM novos e existentes e clientes que atualizam do LiveCycle ES4 para AEM Forms.
seo-description: Detalhes da arquitetura para AEM Forms e topologias recomendadas para clientes do AEM novos e existentes e clientes que atualizam do LiveCycle ES4 para AEM Forms.
uuid: 90baa57a-4785-4b49-844c-a44717d3c12d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 0156b5c3-3bef-4213-9ada-c7b6ae96ada4
translation-type: tm+mt
source-git-commit: aaedec7314b0fa8551df560eef2574a53c20d1c5
workflow-type: tm+mt
source-wordcount: '2490'
ht-degree: 0%

---


# Topologias de arquitetura e implantação para AEM Forms {#architecture-and-deployment-topologies-for-aem-forms}

## Arquitetura {#architecture}

O AEM Forms é um aplicativo implantado no AEM como um pacote AEM. O pacote é conhecido como AEM Forms add-on package. O pacote de complementos de AEM Forms contém ambos os serviços (provedores de API), que são implantados no container AEM OSGi, e servlets ou JSPs (fornecendo funcionalidade de front-end e REST API) gerenciados pela estrutura AEM Sling. O diagrama a seguir descreve essa configuração:

![arquitetura](assets/architecture.png)

A arquitetura dos AEM Forms inclui os seguintes componentes:

* **Principais serviços do AEM:** Serviços básicos que o AEM fornece a um aplicativo implantado. Esses serviços incluem um repositório de conteúdo compatível com JCR, um container de serviço OSGI, um motor de workflow, uma loja confiável, uma loja de chaves e assim por diante. Esses serviços estão disponíveis para aplicativos AEM Forms, mas não são fornecidos por pacotes AEM Forms. Esses serviços são parte integrante da pilha geral do AEM e vários componentes do AEM Forms usam esses serviços.
* **Serviços de formulários:** Forneça funcionalidades relacionadas a formulários, como criar, montar, distribuir e arquivar documentos PDF, adicionar assinaturas digitais para limitar o acesso a documentos e decodificar formulários com códigos de barras. Esses serviços estão disponíveis ao público para consumo pelo código personalizado co-implantado no AEM.
* **Camada da Web:** JSPs ou servlets, construídos sobre serviços comuns e de formulários, que oferecem as seguintes funcionalidades:

   * **Front-end** de criação: Uma interface de usuário de criação de formulários e gerenciamento de formulários para criação e gerenciamento de formulários.
   * **Entrega e envio de formulário frontende**: Uma interface voltada para o usuário final para uso pelos usuários finais dos AEM Forms (por exemplo, cidadãos acessando um site do governo). Isso fornece execuções de formulário (formulário de exibição em um navegador da Web) e funcionalidades de envio.
   * **REST APIs**: Os JSPs e servlets exportam um subconjunto de serviços de formulários para consumo remoto por clientes baseados em HTTP, como o SDK móvel de formulários.

**AEM Forms no OSGi:** Um AEM Forms no ambiente OSGi é AEM Author ou AEM Publish padrão com o pacote AEM Forms implantado nele. Você pode executar AEM Forms no OSGi em um [único ambiente de servidor, farm e configurações](/help/sites-deploying/recommended-deploys.md)agrupadas. A configuração de cluster está disponível somente para instâncias de AEM Author.

**AEM Forms no JEE:** AEM Forms no JEE são servidores AEM Forms em execução na pilha JEE. Ele tem AEM Author com pacotes de complementos AEM Forms e recursos adicionais JEE AEM Forms co-implantados em uma única pilha JEE em execução em um servidor de aplicativos. Você pode executar AEM Forms em JEE em configurações de servidor único e clusterizadas. Os AEM Forms no JEE são necessários apenas para executar a segurança do documento, o gerenciamento de processos e para clientes do LiveCycle que atualizam para o AEM Forms. Estes são alguns cenários adicionais para usar AEM Forms no JEE:

* **Suporte a espaço de trabalho HTML (para clientes que usam espaço de trabalho HTML):** AEM Forms no JEE habilitam logon único com instâncias de processamento, atendem a determinados ativos renderizados em instâncias de processamento e manipulam o envio de formulários renderizados no espaço de trabalho HTML.
* **Processamento** avançado de dados de formulários/comunicações interativas: AEM Forms no JEE podem ser utilizados para processar adicionalmente dados de formulários/comunicações interativas (e salvar os resultados em um armazenamento de dados adequado) em casos de uso complexos, nos quais são necessários recursos avançados de gerenciamento de processos.

AEM Forms no JEE também incluem os seguintes serviços de suporte aos componentes do AEM:

* **Gerenciamento integrado de usuários:** Permite que os usuários de AEM Forms no JEE sejam reconhecidos como formulários AEM em usuários do OSGi e ajuda a ativar o SSO para usuários do OSGi e JEE. Isso é necessário para cenários em que o logon único entre formulários AEM no OSGi e AEM Forms no JEE é necessário (por exemplo, área de trabalho HTML).
* **Hospedagem de ativos:** AEM Forms no JEE podem servir ativos (por exemplo, formulários HTML5) renderizados em AEM Forms no OSGi.

A interface de usuário de criação de AEM Forms não oferece suporte à criação de Documento de Registros (DOR), PDF forms e Formulários HTML5. Esses ativos são projetados usando o aplicativo Designer independente do Forms e carregados individualmente no Gerenciador de AEM Forms. Como alternativa, para AEM Forms em JEE, os formulários podem ser projetados como ativos de aplicativo (no AEM Forms Workbench) e implantados em AEM Forms no servidor JEE.

AEM Forms no OSGi e AEM Forms no JEE têm recursos de fluxo de trabalho. Você pode criar e implantar rapidamente workflows básicos para várias tarefas nos formulários AEM no OSGi, sem precisar instalar o recurso completo de Gerenciamento de processos dos AEM Forms no JEE. Há alguma diferença nos [recursos do fluxo de trabalho centrado em forma nos AEM Forms no OSGi e no recurso de gerenciamento de processos dos AEM Forms no JEE](capabilities-osgi-jee-workflows.md). O desenvolvimento e o gerenciamento de workflows centrados em formulários em AEM Forms no OSGi usam os recursos familiares do Fluxo de trabalho do AEM e da Caixa de entrada do AEM.

## Terminologias {#terminologies}

A imagem a seguir exibe várias configurações do servidor de formulário AEM e seus componentes usados em uma implantação de AEM Forms típica:

![aem_forms_-_recomenddedtopologia](assets/aem_forms_-_recommendedtopology.png)

**Autor:** Uma instância do autor é um servidor AEM Forms em execução no modo de execução padrão do autor. Pode ser AEM Forms em JEE ou AEM Forms no ambiente OSGi. Destina-se a usuários internos, formulários e designers de comunicação interativos e desenvolvedores. Ele permite as seguintes funcionalidades:

* **Criação e gerenciamento de formulários e comunicações interativas:** Designers e desenvolvedores podem criar e editar formulários adaptativos e comunicações interativas, fazer upload de outros tipos de formulários criados externamente, por exemplo, formulários criados no Adobe Forms Designer, e gerenciar esses ativos usando o console do Forms Manager.
* **Publicação de forma e comunicação interativa:** Os ativos hospedados em uma instância do autor podem ser publicados em uma instância de publicação para executar operações de tempo de execução. A publicação de ativos usa os recursos de replicação do AEM. A Adobe recomenda que um agente de replicação seja configurado em todas as instâncias do autor para encaminhar manualmente os formulários publicados para as instâncias de processamento, e que outro agente de replicação seja configurado em instâncias de processamento com o acionador *On Receive (Ao receber* ) habilitado para replicar automaticamente os formulários recebidos para publicar instâncias.

**Publicar:** Uma instância de publicação é um servidor AEM Forms em execução no modo de execução de publicação padrão. As instâncias de publicação destinam-se a usuários finais de aplicativos baseados em formulários, por exemplo, usuários que acessam um site público e enviam formulários. Ele permite as seguintes funcionalidades:

* Renderização e envio de formulários para usuários finais.
* Transporte de dados brutos de formulários enviados para instâncias de processamento para processamento posterior e armazenamento no sistema de registro final. A implementação padrão fornecida no AEM Forms atinge esse objetivo usando os recursos de replicação reversa do AEM. Uma implementação alternativa também está disponível para enviar os dados do formulário diretamente para os servidores de processamento, em vez de salvá-los localmente primeiro (sendo este último um pré-requisito para a replicação reversa ser ativado). Os clientes que têm preocupações com o armazenamento de dados potencialmente confidenciais em instâncias de publicação podem entrar nessa implementação [](/help/forms/using/configuring-draft-submission-storage.md)alternativa, já que as instâncias de processamento normalmente estão em uma zona mais segura.
* Renderização e envio de comunicações e cartas interativas: Uma comunicação interativa e uma carta são renderizadas nas instâncias de publicação e os dados correspondentes são enviados para as instâncias de processamento do armazenamento e pós-processamento. Os dados podem ser salvos localmente em uma instância de publicação e replicados de forma reversa para uma instância de processamento (a opção padrão) posteriormente, ou enviados diretamente para a instância de processamento sem salvar na instância de publicação. A última implementação é útil para clientes com consciência de segurança.

**Processando:** Uma instância de AEM Forms em execução no modo de execução Autor sem usuários atribuídos ao grupo do gerenciador de formulários. Você pode implantar AEM Forms em JEE ou AEM Forms no OSGi como uma instância de processamento. Os usuários não são atribuídos para garantir que as atividades de criação e gerenciamento de formulários não sejam executadas na instância Processamento e ocorram somente na instância Autor. Uma instância de processamento ativa as seguintes funcionalidades:

* **Processamento de dados brutos de formulário que chegam de uma instância de Publicação:** Isso é feito principalmente em uma instância de Processamento por meio de workflows AEM que são acionados quando os dados chegam. Os workflows podem usar a etapa do Modelo de dados de formulário fornecida prontamente para arquivar os dados ou o documento em um armazenamento de dados adequado.
* **armazenamento seguro dos dados** do formulário: O processamento fornece um repositório por trás do firewall para dados de formulários brutos que são isolados dos usuários. Nem os designers de formulário na instância Autor nem os usuários finais na instância Publicar podem acessar esse repositório.

   >[!NOTE]
   >
   > A Adobe recomenda usar um armazenamento de dados de terceiros para salvar os dados processados finais em vez de usar o repositório do AEM.

* **Armazenamento e pós-processamento de dados de correspondência que chegam de uma instância de Publicação:** Os workflows AEM executam o pós-processamento opcional das definições de letras correspondentes. Esses workflows podem salvar os dados processados finais em armazenamentos de dados externos adequados.

* **Hospedagem** HTML Workspace: Uma instância de processamento hospeda o front-end para o HTML Workspace. A área de trabalho HTML fornece a interface do usuário para atribuição de tarefa/grupo associada para processos de revisão e aprovação.

Uma instância de Processamento está configurada para ser executada no modo de execução Autor porque:

* Ela permite a replicação reversa de dados de formulário brutos de uma instância de Publicação. O manipulador de armazenamentos de dados padrão requer o recurso de replicação reversa.
* Os Workflows AEM, que são o principal meio de processamento de dados brutos de formulário que chegam de uma instância de Publicação, são recomendados para execução em um sistema do estilo autor.

## Amostra de topologias físicas para AEM Forms no JEE {#sample-physical-topologies-for-aem-forms-on-jee}

Os AEM Forms nas topologias JEE recomendados abaixo são principalmente para clientes que atualizam do LiveCycle ou de uma versão anterior dos AEM Forms no JEE. A Adobe recomenda usar AEM Forms no OSGi para instalações novas. Uma nova instalação de AEM Forms no JEE é recomendada apenas para o uso de recursos de Segurança e Gerenciamento de processos do Documento.

### Topologia para usar serviços de documento ou recursos de segurança de documento {#topology-for-using-document-services-or-document-security-capabilities}

Os clientes do AEM Forms que pretendem usar somente os serviços do documento ou os recursos de segurança do documento podem ter uma topologia semelhante à exibida abaixo. Essa topologia recomenda usar uma única instância de AEM Forms. Você também pode criar um cluster ou farm de servidores AEM Forms, se necessário. Essa topologia é recomendada quando a maioria dos usuários acessa programaticamente os recursos do servidor AEM Forms e a intervenção por meio da interface do usuário é mínima. A topologia é útil em operações de processamento em lote dos serviços do documento. Por exemplo, usar o serviço de saída para criar centenas de documentos PDF não editáveis diariamente.

Embora o AEM Forms permita que você configure e execute todas as funcionalidades de um único servidor, ainda assim, você deve fazer planejamento de capacidade, balanceamento de carga e configurar servidores dedicados para recursos específicos em um ambiente de produção. Por exemplo, para um ambiente que usa o serviço Gerador de PDF converter milhares de páginas por dia e adicionar assinaturas digitais para limitar o acesso a documentos, configure servidores AEM Forms separados para o serviço Gerador de PDF e recursos de assinatura digital. Ele ajuda a proporcionar um desempenho ótimo e dimensionar os servidores independentemente uns dos outros.

![recursos básicos](assets/basic-features.png)

### Topologia para usar o gerenciamento de processos do AEM Forms {#topology-for-using-aem-forms-process-management}

Os clientes do AEM Forms que planejam usar recursos de gerenciamento de processos do AEM Forms, por exemplo, a área de trabalho HTML pode ter uma topologia semelhante à exibida abaixo. Os AEM Forms no servidor JEE podem estar em uma única configuração de servidor ou cluster.

Se você estiver atualizando do LiveCycle ES4, essa topologia será espelhada cuidadosamente com o que você já tem no LiveCycle, exceto pela adição do AEM Author incorporado ao AEM Forms no JEE. Além disso, não há alteração nos requisitos de cluster para clientes que executam uma atualização. Se estiver usando AEM Forms em um ambiente agrupado, você pode continuar o mesmo no AEM 6.5 Forms. Para uma nova instalação de AEM Forms de JEE para usar o HTML Workspace, executar a instância do autor de AEM incorporada ao ambiente JEE é um requisito adicional.

O armazenamento de dados de formulário é um armazenamento de dados de terceiros usado para armazenar dados processados finais de formulários e comunicações interativas. Este é um elemento opcional na topologia. Você também pode optar por configurar uma instância de processamento e usar seu repositório como o sistema final de registro, se necessário.

![topology_for_usinghtmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

A topologia é recomendada aos clientes que planejam usar AEM Forms no servidor JEE para recursos de gerenciamento de processos (HTML Workspace) sem usar nenhum recurso de pós-processamento, formulários adaptáveis, formulários HTML5 e recursos de comunicação interativa.

### Topologia para usar formulários adaptáveis, formulários HTML5, recursos de comunicação interativa {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

Os clientes do AEM Forms que planejam usar os recursos de captura de dados do AEM Forms, por exemplo, formulários adaptáveis, formulários HTML5, PDF forms, podem ter uma topologia semelhante à exibida abaixo. Essa topologia também é recomendada para o uso de recursos interativos de comunicação de AEM Forms.

![topology-for-using-forms-osgi-modules](assets/topology-for-using-forms-osgi-modules.png)

É possível fazer as seguintes alterações/personalizações na topologia sugerida acima:

* O uso do aplicativo HTML Workspace e AEM Forms requer uma instância de autor ou processamento do AEM. Você pode usar a instância do autor de AEM incorporada a AEM Forms no servidor JEE em vez de configurar um servidor de autor de AEM externo adicional.
* Uma instância de AEM Author ou Processamento é necessária somente para workflows centrados no Forms em OSGi, formulários adaptáveis, portal de formulários e comunicação interativa.
* a interface do usuário do agente de comunicação interativa geralmente é executada dentro da organização. Portanto, você pode manter um servidor de publicação para a interface do agente na rede privada.
* Os formulários AEM em uma instância OSGi incorporada a AEM Forms no servidor JEE também podem executar workflows centrados em formulários no OSGi e nas Pastas monitoradas.

## Amostra de topologias físicas para usar AEM Forms no OSGi {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### Topologia para captura de dados, comunicação interativa, fluxo de trabalho centrado em forma nos recursos do OSGi {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

Os clientes do AEM Forms que planejam usar os recursos de captura de dados do AEM Forms, por exemplo, formulários adaptáveis, formulários HTML5, PDF forms, podem ter uma topologia semelhante à exibida abaixo. Essa topologia também é recomendada para o uso de comunicações interativas e Workflows centrados em formulários no recurso OSGi, por exemplo, para o uso da Caixa de entrada do AEM e do aplicativo AEM Forms para workflows de processos comerciais.

![interative-use-case-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### Topologia para usar os recursos de pasta monitorada para processamento em lote offline {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

Os clientes do AEM Forms que planejam usar Pastas monitoradas para processamento em lote podem ter uma topologia semelhante à exibida abaixo. A topologia exibe um ambiente clusterizado, mas você decide usar uma única instância ou um farm de servidores AEM Forms dependendo da carga. A fonte de dados de terceiros é seu próprio sistema de registro. Funciona como uma fonte de entrada para Pastas monitoradas. A topologia também exibe a saída na forma de um arquivo impresso. Você também pode armazenar o conteúdo de saída em um sistema de arquivos, enviar por email e usar outros métodos personalizados para consumir a saída.

![processamento em lote offline-via-pastas monitoradas](assets/offline-batch-processing-via-watched-folders.png)

### Topologia para usar recursos de serviços de documento para processamento offline baseado em API {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

Os clientes de AEM Forms que planejam usar somente o recurso de serviços de documento podem ter uma topologia semelhante à exibida abaixo. Essa topologia recomenda usar um cluster de AEM Forms em servidores OSGi. Essa topologia é recomendada quando a maioria dos usuários tem recursos de acesso programaticamente (usando APIs) do servidor AEM Forms e a intervenção por meio da interface do usuário é mínima. A topologia é bastante útil em vários cenários de cliente de software. Por exemplo, vários clientes usando o serviço Gerador de PDF para criar documentos PDF sob demanda.

Embora o AEM Forms permita configurar e executar todas as funcionalidades de um único servidor, você deve fazer planejamento de capacidade, balanceamento de carga e configurar servidores dedicados para recursos específicos em um ambiente de produção. Por exemplo, para um ambiente que usa o serviço Gerador de PDF para converter milhares de páginas por dia e vários formulários adaptáveis para capturar dados, configure servidores AEM Forms separados para o serviço Gerador de PDF e recursos de formulários adaptáveis. Ele ajuda a proporcionar um desempenho ótimo e dimensionar os servidores independentemente uns dos outros.

![processamento baseado em API offline](assets/offline-api-based-processing.png)

