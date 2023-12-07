---
title: Escolha de um tipo de persistência para uma instalação do AEM Forms
description: Escolha um tipo de persistência sabiamente. Ele ajuda a criar um ambiente AEM Forms eficiente e escalável.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 621fe107-f4ac-42b1-8c7b-8abbcaac7380
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 1%

---

# Escolha de um tipo de persistência para uma instalação do AEM Forms {#choosing-a-persistence-type-for-an-aem-forms-installation}

Escolha um tipo de persistência sabiamente. Ele ajuda a criar um ambiente AEM Forms eficiente e escalável.

Persistência é o método para armazenar conteúdo nos armazenamentos físicos. Ele define a estrutura de dados real e o mecanismo de armazenamento dos dados. Os micronúcleos atuam como gerenciadores de persistência no AEM Forms. O AEM Forms oferece suporte à persistência (MicroKernals) do tipo TarMK, MongoMK e RDBMK. Você pode escolher um tipo de persistência para o AEM Forms, dependendo da finalidade e do tipo de implantação (Servidor único, Farm ou Cluster) de uma instância do AEM Forms.

>[!NOTE]
>
>O LiveCycle ES4 SP1 usa a persistência TarPM para armazenar conteúdo.

A tabela a seguir lista todos os tipos de persistência compatíveis, juntamente com vários parâmetros, para ajudá-lo a escolher um tipo de persistência para seu ambiente:

<table>
 <tbody>
  <tr>
   <th><strong>Tipo de Instalação/Custo</strong></th>
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
   <td>É necessária uma licença separada</td>
   <td>É necessária uma licença separada</td>
  </tr>
 </tbody>
</table>

O TarMK foi projetado para desempenho, enquanto o MongoMK e o RDBMK foram projetados para escalabilidade. A Adobe recomenda fortemente o TarMK como a tecnologia de persistência padrão para todos os cenários de implantação do AEM Forms, para instâncias de Autor e Publicação, exceto nos casos de uso descritos na seção [Escolhendo Mongo ou um Microkernel de Banco de Dados Relacional sobre TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p).

Para ver a lista de micronúcleos suportados, consulte [Requisitos técnicos do AEM Forms no OSGi](/help/sites-deploying/technical-requirements.md) ou [Combinações de plataforma compatíveis com AEM Forms no JEE](/help/forms/using/aem-forms-jee-supported-platforms.md) artigos.

## Escolhendo Mongo ou um Microkernel de Banco de Dados Relacional sobre TarMK {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

Um ambiente escalável (em cluster) do AEM Forms é um conjunto de duas ou mais instâncias de autor ativas configuradas horizontalmente. Você pode optar por executar mais de uma instância do autor se um único servidor, que suporta todas as atividades de criação simultâneas, não for mais sustentável.

Somente os tipos de persistência MongoMK e RDBMK são compatíveis com um AEM Forms escalável (em cluster) no ambiente JEE. O número de servidores ou o tamanho do ambiente escalável varia para cada instalação. Para obter uma lista de considerações e exemplos, consulte [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md) e ou [Arquitetura e topologias de implantação do AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md) artigo. Você também pode entrar em contato com o suporte da AEM Forms para obter informações detalhadas sobre o planejamento de capacidade do AEM Forms com RDBMK e TarMK.
