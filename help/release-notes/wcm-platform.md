---
title: Base e repositório do AEM
description: Notas de versão específicas da plataforma e do repositório do AEM no Adobe Experience Manager 6.3.
uuid: 70626eda-c514-44bd-9f28-ff7abdc22f53
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 66ecf4c5-6d0f-4586-880d-7d1c8a5a5614
docset: aem65
translation-type: tm+mt
source-git-commit: 4dc4a518c212555b7833ac27de02087a403d3517

---


# Base e repositório do AEM{#aem-foundation-repository}

## Lista de alterações {#list-of-changes}

### Repositório {#repository}

* A base do Adobe Experience Manager 6.5 integrada na parte superior das versões atualizadas da estrutura baseada em OSGi (Apache Sling e Apache Felix) e o repositório de conteúdo do Java: Apache Jackrabbit Oak 1.10.2.
* Please see [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) and [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt) for a full overview of fixed issues.

>[!CAUTION]
>
>* A nova versão do Oak Segment Tar presente desde o AEM 6.3 exige uma migração de repositório. Esta etapa é obrigatória se você estiver atualizando de uma versão mais antiga do TarMK ou quiser alternar o novo segmento de Tar de outro tipo de persistência. For more information on what the benefits of the new Segment Tar are, see the [Migrating to Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).
>



### Suporte ao Java {#java-support}

* Novo suporte para o Java 11, bem como o Java 8 já compatível
* Para melhor desempenho, substitua os valores GC padrão por outros valores. Para obter informação, consulte a seção [Instalar e atualizar](/help/sites-deploying/custom-standalone-install.md).
* As atualizações de manutenção do Java 11 e Java 8 serão distribuídas pela Adobe para o uso dos clientes em projetos relacionados ao AEM, quando não disponibilizadas publicamente no Oracle

### OSGI {#osgi}

* Adição de bibliotecas do utilitário de promessas e conversor do OSGi

### Projetos e fluxos de trabalho {#projects-and-workflows}

* O novo editor de modelo de fluxo de trabalho introduzido na versão 6.4 foi aprimorado para incluir operações como Copiar e publicar, Suporte à variável em etapas do fluxo de trabalho e divisões OR e AND aprimoradas.

### Pesquisar {#searching}

* A pesquisa no Oak agora suporta aspectos dinâmicos. Por exemplo, o painel de filtros na pesquisa de ativos mostra a quantidade estimada de resultados.
* O QueryBuilder foi expandido para fornecer resultados com aspectos dinâmicos

### Segurança {#security}

* Adição de expiração de senha para o usuário administrador.

### Interface do usuário {#user-interface}

Vários aprimoramentos foram feitos à interface do usuário para torná-la mais produtiva e fácil de usar.

* O AEM 6.5 introduz a nova interface do usuário do gerenciamento de permissões para usuários e grupos, que facilita visualizar e configurar todo o conjunto de privilégios e restrições sem a necessidade de acessar o CRXDE.
* As exibições em coluna agora também só carregam entradas visíveis na tela e só carregam mais quando o usuário começa a rolar. A exibição em lista e cartão já faziam isso desde a versão 6.0 (aprimorado na 6.4)
* As exibições em coluna agora incluem o status de fluxo de trabalho de páginas/ativos, quando aplicável
* A ação &quot;Selecionar tudo&quot; é uma forma rápida de executar uma ação com todas as páginas/ativos na mesma pasta
* A ação “Selecionar tudo” tenta executar a ação para todas as páginas/ativos, não só nos que foram carregados. Uma caixa de diálogo de aviso será exibida se a ação não tiver sido atualizada para tratar de ações em massa

>[!CAUTION]
>
>* A Adobe não planeja fazer aprimoramentos adicionais à interface do usuário clássica. O AEM 6.5 tem a interface do usuário clássica incluída, e os clientes que atualizam de versões anteriores podem continuar a usando da mesma forma. Note that Classic UI remains fully supported while being deprecated [Read more](/help/sites-deploying/ui-recommendations.md).
>



### Atualização {#upgrade}

* O procedimento de atualização permanece amplamente o mesmo no 6.5.
* Ainda oferecemos suporte à compatibilidade com versões anteriores, à avaliação de complexidade da atualização e aos recursos de atualizações sustentáveis inseridos na versão 6.4. Foram feitas atualizações específicas da versão a essas áreas onde foi necessário.
* O empacotamento de detector de padrão foi simplificado, e haverá um pacote que avalia atualizações no 6.5 para as versões de origem disponíveis.
* Please see the [Upgrade documentation](/help/sites-deploying/upgrade.md) for more details on upgrade procedure.

### Servidor Web {#web-server}

* A distribuição Quickstart usa o Eclipse Jetty 9.4.15 como mecanismo de servlet (AEM 6.4 fornecido com 9.3.22)

