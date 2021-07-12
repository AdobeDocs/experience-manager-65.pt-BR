---
title: Como escolher um tipo de persistência para uma instalação do AEM Forms
seo-title: Como escolher um tipo de persistência para uma instalação do AEM Forms
description: Escolha um tipo de persistência com sabedoria. Ajuda você a criar um ambiente AEM Forms eficiente e escalável.
seo-description: Escolha um tipo de persistência com sabedoria. Ajuda você a criar um ambiente AEM Forms eficiente e escalável.
uuid: 1c692502-5039-4757-9358-1772772b3904
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: a972fb35-38a7-4b83-99bd-6a6dddf8043b
role: Admin
exl-id: 621fe107-f4ac-42b1-8c7b-8abbcaac7380
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---

# Como escolher um tipo de persistência para uma instalação do AEM Forms {#choosing-a-persistence-type-for-an-aem-forms-installation}

Escolha um tipo de persistência com sabedoria. Ajuda você a criar um ambiente AEM Forms eficiente e escalável.

A persistência é o método para armazenar conteúdo nos armazenamentos físicos. Ela define a estrutura de dados real e o mecanismo de armazenamento dos dados. MicroKernels atuam como gerentes de persistência no AEM Forms. A AEM Forms suporta persistência (MicroKernals) do tipo TarMK, MongoMK e RDBMK. Você pode escolher um tipo de persistência para o AEM Forms dependendo da finalidade e do tipo de implantação (Servidor único, Farm ou Cluster) de uma instância do AEM Forms.

>[!NOTE]
>
>O LiveCycle ES4 SP1 usa a persistência do TarPM para armazenar conteúdo.

A tabela a seguir lista todos os tipos de persistência suportados junto com vários parâmetros para ajudá-lo a escolher um tipo de persistência para o seu ambiente:

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
   <th><strong>Configuração de Cluster</strong></th>
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

O TarMK foi projetado para desempenho, enquanto o MongoMK e o RDBMK foram projetados para escalabilidade. O Adobe recomenda o TarMK como a tecnologia de persistência padrão para todos os cenários de implantação do AEM Forms, para instâncias de Autor e Publicação, exceto nos casos de uso descritos na seção [Choosing Mongo or a Relational Database Microkernel over TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

Para obter a lista de Microkernels compatíveis, consulte [AEM Forms em Requisitos Técnicos OSGi](/help/sites-deploying/technical-requirements.md) ou [AEM Forms em combinações de plataforma compatíveis com JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) artigos.

## Escolhendo Mongo ou um Microkernel de Banco de Dados Relacional sobre TarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

Um ambiente AEM Forms escalável (em cluster) é um conjunto de duas ou mais instâncias ativas do autor configuradas horizontalmente. Você pode optar por executar mais de uma instância de autor se um único servidor, compatível com todas as atividades de criação simultâneas, não for mais sustentável.

Somente os tipos de persistência MongoMK e RDBMK são compatíveis com um AEM Forms escalável (em cluster) no ambiente JEE. O número de servidores ou o tamanho do ambiente escalável varia para cada instalação. Para obter uma lista de considerações e exemplos, consulte o artigo [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md) e ou [Arquitetura e topologias de implantação para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md). Você também pode entrar em contato com o suporte da AEM Forms para obter informações detalhadas sobre o planejamento de capacidade do AEM Forms com RDBMK e TarMK.
