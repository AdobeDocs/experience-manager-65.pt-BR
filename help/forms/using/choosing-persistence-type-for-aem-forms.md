---
title: Como escolher um tipo de persistência para uma instalação do AEM Forms
seo-title: Como escolher um tipo de persistência para uma instalação do AEM Forms
description: Escolha um tipo de persistência com sabedoria. Ele ajuda a criar um ambiente AEM Forms eficiente e escalonável.
seo-description: Escolha um tipo de persistência com sabedoria. Ele ajuda a criar um ambiente AEM Forms eficiente e escalável.
uuid: 1c692502-5039-4757-9358-1772772b3904
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: a972fb35-38a7-4b83-99bd-6a6dddf8043b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---


# Escolhendo um tipo de persistência para uma instalação do AEM Forms {#choosing-a-persistence-type-for-an-aem-forms-installation}

Escolha um tipo de persistência com sabedoria. Ele ajuda a criar um ambiente AEM Forms eficiente e escalonável.

A persistência é o método para armazenar conteúdo nos armazenamentos físicos. Define a estrutura real dos dados e o mecanismo de armazenamento dos dados. MicroKernels atuam como gerentes de persistência no AEM Forms. A AEM Forms suporta persistência (MicroKernals) do tipo TarMK, MongoMK e RDBMK. Você pode escolher um tipo de persistência para o AEM Forms dependendo da finalidade e do tipo de implantação (Servidor único, Farm ou Cluster) de uma instância do AEM Forms.

>[!NOTE]
>
>O LiveCycle ES4 SP1 usa a persistência do TarPM para armazenar conteúdo.

A tabela a seguir lista todos os tipos de persistência suportados junto com vários parâmetros para ajudar a escolher um tipo de persistência para o seu ambiente:

<table>
 <tbody>
  <tr>
   <th><strong>Tipo/custo de instalação</strong></th>
   <th><strong>TarMK</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>Configuração independente</strong></th>
   <td>Compatível<br /> </td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <th><strong>Configuração de cluster</strong></th>
   <td>Incompatível</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <th><strong>Custo da licença</strong></th>
   <td>Incluído com AEM </td>
   <td>Licença separada necessária</td>
   <td>Licença separada necessária</td>
  </tr>
 </tbody>
</table>

A TarMK foi projetada para o desempenho, enquanto a MongoMK e a RDBMK foram projetadas para a escalabilidade. O Adobe recomenda altamente o TarMK como a tecnologia de persistência padrão para todos os cenários de implantação do AEM Forms, para instâncias de Autor e Publicação, exceto nos casos de uso descritos na seção [Escolhendo Mongo ou um Microkernel de Banco de Dados Relacional sobre o TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

Para obter a lista dos Microkernels suportados, consulte os artigos [AEM Forms on OSGi Technical Requirements](/help/sites-deploying/technical-requirements.md) ou [AEM Forms on JEE supported platform Combinations](/help/forms/using/aem-forms-jee-supported-platforms.md).

## Escolhendo Mongo ou um Microkernel de Banco de Dados Relacional sobre TarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

Um ambiente AEM Forms escalável (clusterizado) é um conjunto de duas ou mais instâncias ativas configuradas horizontalmente. Você pode optar por executar mais de uma instância do autor se um único servidor, compatível com todas as atividades de criação simultâneas, não for mais sustentável.

Somente os tipos de persistência MongoMK e RDBMK são suportados para um AEM Forms escalável (clusterizado) no ambiente JEE. O número de servidores ou o tamanho do ambiente escalável varia para cada instalação. Para obter uma lista de considerações e exemplos, consulte o artigo [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md) ou [Arquitetura e topologias de implantação para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md). Você também pode entrar em contato com o suporte da AEM Forms para obter informações detalhadas sobre o planejamento de capacidade da AEM Forms com RDBMK e TarMK.
