---
title: AEM Foundation e repositório
description: Notas de versão para plataforma e repositório Adobe Experience Manager.
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 62%

---


# AEM Foundation e repositório {#aem-foundation-repository}

## Lista de alterações {#list-of-changes}

### Repositório {#repository}

* A base do Adobe Experience Manager 6.5 integrada na parte superior das versões atualizadas da estrutura baseada em OSGi (Apache Sling e Apache Felix) e o repositório de conteúdo do Java: Apache Jackrabbit Oak 1.10.2.
* Para obter uma visão geral dos problemas corrigidos, consulte [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt), [Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) e [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt).

>[!CAUTION]
>
>A nova versão do Oak Segment Tar presente desde o AEM 6.3 exige uma migração de repositório. Esta etapa é obrigatória se você estiver atualizando de uma versão mais antiga do TarMK ou quiser alternar o novo segmento de Tar de outro tipo de persistência. Para obter mais informações sobre quais são os benefícios da nova barra de segmentos, consulte [Migração para Oak Segment Tar FAQ](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar).

### Suporte ao Java {#java-support}

* Novo suporte para o Java 11, bem como o Java 8 já compatível.
* Para melhor desempenho, substitua os valores GC padrão por outros valores. Para obter informação, consulte a seção [Instalar e atualizar](/help/sites-deploying/custom-standalone-install.md).
* As atualizações de manutenção do Java 11 e Java 8 são distribuídas pela Adobe para uso pelo cliente em projetos relacionados a AEM, quando não estiverem disponíveis publicamente na Oracle.

### OSGI {#osgi}

* Adição de bibliotecas do utilitário de promessas e conversor do OSGi.

### Projetos e fluxos de trabalho {#projects-and-workflows}

* O novo editor do Modelo de Fluxo de Trabalho introduzido no 6.4 foi melhorado para incluir mais operações como Copiar e Publicar, Suporte a variáveis em etapas do Fluxo de trabalho e divisões aprimoradas `OR` e `AND`.

### Pesquisar {#searching}

* A pesquisa no Oak agora suporta aspectos dinâmicos. Por exemplo, o painel de filtros na pesquisa de ativos mostra a quantidade estimada de resultados.
* O QueryBuilder foi expandido para fornecer resultados com aspectos dinâmicos.

### Segurança {#security}

* Adição de expiração de senha para o usuário administrador.

### Interface do usuário {#user-interface}

Vários aprimoramentos foram feitos à interface do usuário para torná-la mais produtiva e fácil de usar.

* O AEM 6.5 introduz a nova interface do usuário do gerenciamento de permissões para usuários e grupos, que facilita visualizar e configurar todo o conjunto de privilégios e restrições sem a necessidade de acessar o CRXDE.
* As exibições em coluna agora também só carregam entradas visíveis na tela e só carregam mais quando o usuário começa a rolar. A exibição em lista e cartão já faziam isso desde a versão 6.0 (aprimorado na 6.4).
* As exibições em coluna agora incluem o status de fluxo de trabalho de páginas/ativos, quando aplicável.
* A ação Selecionar tudo é uma forma rápida de executar uma ação com todas as páginas/ativos na mesma pasta.
* A ação Selecionar tudo tenta executar a ação para todas as páginas/ativos, não só nos que foram carregados. Se a ação não for atualizada para lidar com Ações em massa, um aviso será exibido.

>[!CAUTION]
>
>O Adobe não fará mais aprimoramentos na interface clássica. O Experience Manager 6.5 inclui a interface clássica para compatibilidade com versões anteriores. A interface de usuário clássica permanece totalmente compatível enquanto está sendo substituída [Leia mais](/help/sites-deploying/ui-recommendations.md).

### Atualização {#upgrade}

* O procedimento de atualização permanece amplamente o mesmo no 6.5.
* Ainda oferecemos suporte à compatibilidade com versões anteriores, à avaliação de complexidade da atualização e aos recursos de atualizações sustentáveis inseridos na versão 6.4. Foram feitas atualizações específicas da versão a essas áreas onde foi necessário.
* O empacotamento de detector de padrão foi simplificado, e haverá um pacote que avalia atualizações no 6.5 para as versões de origem disponíveis.
* Para obter detalhes sobre o procedimento de atualização, consulte a [documentação de atualização](/help/sites-deploying/upgrade.md).

### Servidor Web {#web-server}

* A distribuição do Quickstart usa o Eclipse Jetty 9.4.15 como mecanismo de servlet (AEM 6.4 fornecido com 9.3.22).
