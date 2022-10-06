---
title: Aprimoramento do desempenho do servidor de aplicativos
seo-title: Enhancing application server performance
description: Este documento descreve as configurações opcionais que você pode configurar para melhorar o desempenho do servidor de aplicativos do AEM forms.
seo-description: This document describes optional settings that you can configure to improve the performance of your AEM forms application server.
uuid: 88d2f96a-3b59-410d-8160-20581d27acad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fad65765-d56d-4a9f-82d5-bcceb1758953
exl-id: 6e2f3d4c-2ead-45b3-98e7-32cacc7e2985
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 0%

---

# Aprimoramento do desempenho do servidor de aplicativos{#enhancing-application-server-performance}

Este conteúdo descreve as configurações opcionais que podem ser definidas para melhorar o desempenho do servidor de aplicativos do AEM forms.

## Configurar fontes de dados do servidor de aplicativos {#configuring-application-server-data-sources}

AEM forms usa o repositório AEM forms como sua fonte de dados. O repositório AEM forms armazena ativos de aplicativos e, em tempo de execução, os serviços podem recuperar ativos do repositório como parte da conclusão de um processo de negócios automatizado.

O acesso à fonte de dados pode ser significativo, dependendo do número de módulos de formulários de AEM que você está executando e do número de usuários simultâneos que acessam o aplicativo. O acesso à fonte de dados pode ser otimizado usando o pool de conexão. *Pooling de conexão* é uma técnica usada para evitar a sobrecarga de fazer novas conexões de banco de dados sempre que um aplicativo ou objeto de servidor exigir acesso ao banco de dados. O pool de conexões geralmente é usado em aplicativos baseados na Web e corporativos e geralmente é manipulado por, mas não limitado a, um servidor de aplicativos.

É importante configurar corretamente os parâmetros do pool de conexões para que você nunca fique sem conexões, o que pode causar deterioração no desempenho do aplicativo.

Para configurar adequadamente as configurações do pool de conexão, é importante que o administrador do servidor de aplicativos monitore o pool de conexão durante as horas de pico do dia. O monitoramento garante que conexões suficientes estejam sempre disponíveis para aplicativos e usuários. A maioria dos servidores de aplicativos inclui ferramentas de monitoramento.

Você pode monitorar várias estatísticas para cada instância da fonte de dados JDBC em seu domínio usando o Console de Administração do WebLogic Server. Consulte a documentação do WebLogic para obter detalhes.

Quando o administrador do servidor de aplicativos determina as configurações corretas do pool de conexões, essa pessoa deve comunicar essas informações ao administrador do banco de dados. O administrador do banco de dados precisa dessas informações porque o número de conexões do banco de dados é igual ao número de conexões no pool de conexões da fonte de dados. Em seguida, conclua as etapas para definir as configurações do pool de conexões para o servidor de aplicativos e o tipo de fonte de dados, conforme descrito abaixo.

### Definir configurações do pool de conexões para WebLogic para Oracle e MySQL {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. Em Estrutura de domínio, clique em Serviços > JDBC > Fontes de dados e, no painel direito, clique em IDP_DS.
1. Na próxima tela, clique na guia Configuração > Pool de Conexões e insira um valor nas seguintes caixas:

   * Capacidade inicial
   * Capacidade máxima
   * Aumento da capacidade
   * Tamanho do Cache de Instrução

1. Clique em Salvar e em Ativar alterações.
1. Reinicie o servidor gerenciado do WebLogic.

### Definir configurações do pool de conexões para WebLogic para SQLServer {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. Em Centro de alterações, clique em Bloquear e editar.
1. Em Estrutura de domínio, clique em Serviços > JDBC > Fontes de dados e, no painel direito, clique em EDC_DS.
1. Na próxima tela, clique na guia Configuração > Pool de Conexões e insira um valor nas seguintes caixas:

   * Capacidade inicial
   * Capacidade máxima
   * Aumento da capacidade
   * Tamanho do Cache de Instrução

1. Clique em Salvar e em Ativar alterações.
1. Reinicie o servidor gerenciado do WebLogic.

### Definir configurações do pool de conexões para WebSphere para DB2 {#configure-connection-pool-settings-for-websphere-for-db2}

1. Na árvore de navegação, clique em Resources > JDBC > JDBC Providers. No painel direito, clique na fonte de dados criada, Provedor de Driver DB2 Universal JDBC ou LiveCycle - db2 - IDP_DS.
1. Em Propriedades adicionais, clique em Fontes de dados e selecione IDP_DS.
1. Na próxima tela, em Propriedades adicionais, clique em Propriedades do pool de conexões e digite um valor na caixa Máximo de conexões e na caixa Mínimo de conexões .
1. Clique em OK ou Aplicar e em Salvar diretamente na configuração Principal.

### Definir configurações do pool de conexões para WebSphere for Oracle {#configure-connection-pool-settings-for-websphere-for-oracle}

1. Na árvore de navegação, clique em Resources > JDBC > JDBC Providers. No painel direito, clique na fonte de dados do Driver JDBC do Oracle que você criou.
1. Em Propriedades adicionais, clique em Fontes de dados e selecione IDP_DS.
1. Na próxima tela, em Propriedades adicionais, clique em Propriedades do pool de conexões e digite um valor na caixa Máximo de conexões e na caixa Mínimo de conexões .
1. Clique em OK ou Aplicar e em Salvar diretamente na configuração Principal.

### Definir configurações do pool de conexão para o WebSphere para SqlServer {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. Na árvore de navegação, clique em Resources > JDBC > JDBC Providers e, no painel direito, clique na fonte de dados JDBC Definida pelo Usuário criada.
1. Em Propriedades adicionais, clique em Fontes de dados e selecione IDP_DS.
1. Na próxima tela, em Propriedades adicionais, clique em Propriedades do pool de conexões e digite um valor na caixa Máximo de conexões e na caixa Mínimo de conexões :
1. Clique em OK ou Aplicar e em Salvar diretamente na configuração Principal.

## Otimização de documentos em linha e impacto na memória da JVM {#optimizing-inline-documents-and-impact-on-jvm-memory}

Se você normalmente está processando documentos de tamanho relativamente pequeno, é possível melhorar o desempenho associado à velocidade de transferência de documentos e ao espaço de armazenamento. Para fazer isso, implemente as seguintes configurações de produto do AEM forms:

* Aumente o tamanho padrão em linha do documento para formulários de AEM para que seja maior que o tamanho da maioria dos documentos.
* Para processar arquivos maiores, especifique diretórios de armazenamento que estejam em um sistema de disco de alta velocidade ou em um disco RAM.

O tamanho máximo em linha e os diretórios de armazenamento (o diretório de arquivos temporários dos formulários AEM e o diretório GDS) são configurados no console de administração.

### Tamanho do documento e tamanho máximo em linha {#document-size-and-maximum-inline-size}

Quando um documento enviado para processamento por formulários AEM for menor ou igual ao tamanho padrão máximo em linha do documento, ele será armazenado em linha no servidor e o documento será serializado como um objeto de Documento Adobe. Armazenar documentos em linha pode ter benefícios significativos em termos de desempenho. No entanto, se você estiver usando o fluxo de trabalho de formulários, o conteúdo também poderá ser armazenado no banco de dados para fins de rastreamento. Portanto, aumentar o tamanho máximo em linha pode afetar o tamanho do banco de dados.

Um documento maior que o tamanho máximo em linha é armazenado no sistema de arquivos local. O objeto Documento do Adobe transferido de e para o servidor é apenas um ponteiro para esse arquivo.

Quando o conteúdo do documento é incorporado (ou seja, menor que o tamanho máximo em linha), o conteúdo é armazenado no banco de dados como parte da carga útil de serialização do documento. Portanto, aumentar o tamanho máximo em linha pode afetar o tamanho do banco de dados.

**Alterar o tamanho máximo em linha**

1. No console de administração, clique em Configurações > Configurações principais do sistema > Configurações.
1. Insira um valor na caixa Tamanho máximo em linha do documento padrão e clique em OK.

   >[!NOTE]
   >
   >O valor da propriedade Tamanho máximo em linha do documento deve ser idêntico para o AEM Forms no ambiente JEE e AEM Forms no pacote OSGi incluído AEM Forms no ambiente JEE. Essas etapas atualizaram o valor somente para o AEM Forms no ambiente JEE e não para o AEM Forms no pacote OSGi incluíram o AEM Forms no ambiente JEE.

1. Reinicie o servidor de aplicativos com a seguinte propriedade do sistema:

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >A propriedade do sistema acima mencionada substitui o valor da propriedade Tamanho máximo em linha do documento definida para AEM Forms no ambiente JEE e AEM Forms no pacote OSGi incluiu AEM Forms no ambiente JEE.

>[!NOTE]
>
>O tamanho padrão máximo em linha é de 65536 bytes.

### Tamanho máximo de heap da JVM {#jvm-maximum-heap-size}

Um aumento no tamanho máximo em linha requer mais memória para armazenar os documentos serializados. Portanto, geralmente também requer um aumento no tamanho máximo de heap da JVM.

Um sistema altamente carregado que está processando muitos documentos pode saturar rapidamente a memória heap da JVM. Para evitar um OutOfMemoryError, aumente o tamanho máximo de heap da JVM em um valor correspondente ao tamanho dos documentos em linha multiplicado pelo número de documentos que normalmente são executados em um determinado momento.

Aumento máximo do tamanho de heap da JVM = (tamanho dos documentos em linha) x (número médio de documentos processados).

**Calculando o tamanho máximo de heap da JVM**

Neste exemplo, o heap máximo da JVM atual é definido como 512 MB e o tamanho máximo em linha é de 64 KB. O servidor deve ser configurado para o cenário em que 10 trabalhos são executados simultaneamente e cada tarefa tem 9 arquivos de entrada e 1 arquivo de resultado (um total de 10 arquivos por trabalho e 100 arquivos processados simultaneamente). Todos os arquivos têm menos de 512 KB.

Para armazenar todos os arquivos em linha, defina o tamanho máximo em linha como pelo menos 512 KB.

O aumento necessário no tamanho máximo de heap da JVM é calculado usando a seguinte equação:

(512 KB) x (100) = 51200 KB, ou 50 MB

O tamanho máximo de heap da JVM deve ser aumentado em 50 MB para um total de 562 MB.

**Considerando a fragmentação do heap**

Definir o tamanho dos documentos em linha para valores grandes aumenta o risco de um OutOfMemoryError em sistemas que são propensos a heap fragmentação. Para armazenar um documento em linha, a memória heap da JVM deve ter espaço contíguo suficiente. Alguns sistemas operacionais, JVMs e algoritmos de coleta de lixo são susceptíveis à fragmentação do heap. A fragmentação diminui a quantidade de espaço de heap contíguo e pode levar a um OutOfMemoryError mesmo quando há espaço livre total suficiente.

Por exemplo, operações anteriores no servidor de aplicativos deixaram o heap da JVM em um estado fragmentado e o coletor de lixo não pode compactar o heap o suficiente para recuperar grandes blocos de espaço livre. Um OutOfMemoryError pode ocorrer mesmo que o tamanho máximo de heap da JVM tenha sido ajustado para um aumento no tamanho máximo em linha.

Para contabilizar a fragmentação do heap, o tamanho do documento em linha não deve ser definido acima de 0,1% do tamanho total do heap. Por exemplo, um tamanho máximo de heap da JVM de 512 MB pode suportar um tamanho máximo em linha de 512 MB x 0,001 = 0,512 MB ou 512 KB.

## Aprimoramentos do WebSphere Application Server {#websphere-application-server-enhancements}

Esta seção descreve as configurações específicas de um ambiente do WebSphere Application Server.

### Aumento da memória máxima alocada para a JVM {#increasing-the-maximum-memory-allocated-to-the-jvm}

Se você estiver executando o Configuration Manager ou tentando gerar o código de implantação do Enterprise JavaBeans (EJB) usando o utilitário de linha de comando *ejbdeploy* e ocorrer um erro OutOfMemory, aumente a quantidade de memória alocada para a JVM.

1. Edite o script ejbdeploy no *[raiz do appserver]*/deploytool/itp/ diretory:

   * (Windows) `ejbdeploy.bat`
   * (Linux e UNIX) `ejbdeploy.sh`

1. Encontre a `-Xmx256M` e alterá-lo para um valor mais alto, como `-Xmx1024M`.
1. Salve o arquivo.
1. Execute o `ejbdeploy` ou reimplante usando o Configuration Manager.

## Melhorando o desempenho do Windows Server 2003 com o LDAP {#improving-windows-server-2003-performance-with-ldap}

Este conteúdo descreve as configurações específicas de um ambiente do sistema operacional Microsoft Windows Server 2003.

Usar o pool de conexão na conexão de pesquisa pode diminuir o número de portas necessárias em até 50%. Isso ocorre porque essa conexão sempre usa as mesmas credenciais para um determinado domínio, e o contexto e objetos relacionados são fechados explicitamente.

### Configurar o Windows Server para pool de conexão {#configure-your-windows-server-for-connection-pooling}

1. Clique em Iniciar > Executar para iniciar o editor do registro e, na caixa Abrir, digite `regedit` e clique em OK.
1. Vá para a chave do Registro `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. No painel direito do editor do registro, localize o nome do valor TcpTimedWaitDelay. Se o nome não for exibido, selecione Editar > Novo > Valor de DWORD na barra de menu para adicionar o nome.
1. Na caixa Nome, digite `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >Se você não vir um cursor piscante e `New Value #` na caixa, clique com o botão direito do mouse dentro do painel direito, selecione Renomear e, na caixa Nome, digite `TcpTimedWaitDelay`*.*

1. Repita a etapa 4 para os nomes de valor MaxUserPort, MaxHashTableSize e MaxFreeTcbs.
1. Clique duas vezes dentro do painel direito para definir o valor TcpTimedWaitDelay. Em Base, selecione Decimal e, na caixa Valor, digite `30`.
1. Clique duas vezes dentro do painel direito para definir o valor MaxUserPort. Em Base, selecione Decimal e, na caixa Valor, digite `65534`.
1. Clique duas vezes dentro do painel direito para definir o valor MaxHashTableSize. Em Base, selecione Decimal e, na caixa Valor, digite `65536`.
1. Clique duas vezes dentro do painel direito para definir o valor MaxFreeTcbs. Em Base, selecione Decimal e, na caixa Valor, digite `16000`.

>[!NOTE]
>
>Problemas graves podem ocorrer se você modificar o registro incorretamente usando o Editor de Registro ou usando outro método. Esses problemas podem exigir a reinstalação do sistema operacional. Modifique o registro por sua conta e risco.
