---
title: Aprimorando o desempenho do servidor de aplicativos
seo-title: Aprimorando o desempenho do servidor de aplicativos
description: Este documento descreve as configurações opcionais que você pode configurar para melhorar o desempenho do servidor de aplicativos para formulários AEM.
seo-description: Este documento descreve as configurações opcionais que você pode configurar para melhorar o desempenho do servidor de aplicativos para formulários AEM.
uuid: 88d2f96a-3b59-410d-8160-20581d27acad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fad65765-d56d-4a9f-82d5-bcceb1758953
translation-type: tm+mt
source-git-commit: a26bc4e4ea10370dd2fc3403500004b9e378c418

---


# Aprimorando o desempenho do servidor de aplicativos{#enhancing-application-server-performance}

Este conteúdo descreve as configurações opcionais que você pode configurar para melhorar o desempenho do servidor de aplicativos para formulários AEM.

## Configuração de fontes de dados do servidor de aplicativos {#configuring-application-server-data-sources}

Os formulários do AEM usam o repositório de formulários do AEM como sua fonte de dados. O repositório de formulários do AEM armazena ativos de aplicativos e, em tempo de execução, os serviços podem recuperar ativos do repositório como parte da conclusão de um processo de negócios automatizado.

O acesso à fonte de dados pode ser significativo, dependendo do número de módulos de formulários AEM que você está executando e do número de usuários simultâneos acessando o aplicativo. O acesso à fonte de dados pode ser otimizado usando o pooling de conexão. *Pooling* de conexão é uma técnica usada para evitar a sobrecarga de fazer novas conexões de banco de dados sempre que um objeto de aplicativo ou servidor exigir acesso ao banco de dados. O pooling de conexão é geralmente usado em aplicativos corporativos e baseados na Web e geralmente é manipulado por, mas não limitado a, um servidor de aplicativos.

É importante configurar corretamente os parâmetros do pool de conexões para que você nunca perca as conexões, o que pode causar a deterioração do desempenho do aplicativo.

Para configurar adequadamente as configurações do pool de conexões, é importante que o administrador do servidor de aplicativos monitore o pool de conexões durante as horas de pico do dia. O monitoramento garante que conexões suficientes estejam disponíveis para aplicativos e usuários o tempo todo. A maioria dos servidores de aplicativos inclui ferramentas de monitoramento.

Você pode monitorar várias estatísticas para cada instância da fonte de dados JDBC em seu domínio usando o Console de Administração do WebLogic Server. Consulte a documentação do WebLogic para obter detalhes.

Quando o administrador do servidor de aplicativos determinar as configurações corretas do pool de conexões, essa pessoa deverá comunicar essas informações ao administrador do banco de dados. O administrador do banco de dados precisa dessas informações porque o número de conexões do banco de dados é igual ao número de conexões no pool de conexões da fonte de dados. Em seguida, complete as etapas para configurar as configurações do pool de conexões para o servidor de aplicativos e o tipo de fonte de dados, conforme descrito abaixo.

### Definir configurações do pool de conexões para WebLogic para Oracle e MySQL {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. Em Estrutura do domínio, clique em Serviços > JDBC > Fontes de dados e, no painel direito, clique em IDP_DS.
1. Na tela seguinte, clique na guia Configuração > Pool de conexões e digite um valor nas seguintes caixas:

   * Capacidade inicial
   * Capacidade máxima
   * Aumento da capacidade
   * Tamanho do cache de demonstrativo

1. Clique em Salvar e em Ativar alterações.
1. Reinicie o servidor gerenciado WebLogic.

### Definir configurações do pool de conexões para WebLogic para SQLServer {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. Em Centro de alterações, clique em Bloquear e editar.
1. Em Estrutura do domínio, clique em Serviços > JDBC > Fontes de dados e, no painel direito, clique em EDC_DS.
1. Na tela seguinte, clique na guia Configuração > Pool de conexões e digite um valor nas seguintes caixas:

   * Capacidade inicial
   * Capacidade máxima
   * Aumento da capacidade
   * Tamanho do cache de demonstrativo

1. Clique em Salvar e em Ativar alterações.
1. Reinicie o servidor gerenciado WebLogic.

### Definir configurações do pool de conexões para WebSphere para DB2 {#configure-connection-pool-settings-for-websphere-for-db2}

1. Na árvore de navegação, clique em Recursos > JDBC > Provedores JDBC. No painel direito, clique na fonte de dados criada, seja DB2 Universal JDBC Driver Provider ou LiveCycle - db2 - IDP_DS.
1. Em Propriedades adicionais, clique em Fontes de dados e selecione IDP_DS.
1. Na tela seguinte, em Propriedades adicionais, clique em Propriedades do pool de conexões e digite um valor na caixa Máximo de conexões e na caixa Mínimo de conexões.
1. Clique em OK ou Aplicar e em Salvar diretamente na configuração mestre.

### Definir configurações do pool de conexões para WebSphere para Oracle {#configure-connection-pool-settings-for-websphere-for-oracle}

1. Na árvore de navegação, clique em Recursos > JDBC > Provedores JDBC. No painel direito, clique na fonte de dados Oracle JDBC Driver que você criou.
1. Em Propriedades adicionais, clique em Fontes de dados e selecione IDP_DS.
1. Na tela seguinte, em Propriedades adicionais, clique em Propriedades do pool de conexões e digite um valor na caixa Máximo de conexões e na caixa Mínimo de conexões.
1. Clique em OK ou Aplicar e em Salvar diretamente na configuração mestre.

### Definir configurações do pool de conexões para WebSphere para SqlServer {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. Na árvore de navegação, clique em Recursos > JDBC > Provedores JDBC e, no painel direito, clique na fonte de dados do Driver JDBC Definido pelo Usuário que você criou.
1. Em Propriedades adicionais, clique em Fontes de dados e selecione IDP_DS.
1. Na tela seguinte, em Propriedades adicionais, clique em Propriedades do pool de conexões e digite um valor na caixa Máximo de conexões e na caixa Mínimo de conexões:
1. Clique em OK ou Aplicar e em Salvar diretamente na configuração mestre.

## Otimizar documentos em linha e impacto na memória JVM {#optimizing-inline-documents-and-impact-on-jvm-memory}

Se você estiver processando documentos de tamanho relativamente pequeno, é possível melhorar o desempenho associado à velocidade de transferência do documento e ao espaço do armazenamento. Para fazer isso, implemente as seguintes configurações de produto de formulários AEM:

* Aumente o tamanho em linha máximo do documento padrão para formulários AEM para que ele seja maior que o tamanho da maioria dos documentos.
* Para processar arquivos maiores, especifique diretórios de armazenamento que estejam em um sistema de disco de alta velocidade ou em um disco RAM.

O tamanho máximo em linha e os diretórios de armazenamento (o diretório de arquivos temporários de formulários AEM e o diretório GDS) são configurados no console de administração.

### Tamanho do Documento e tamanho máximo em linha {#document-size-and-maximum-inline-size}

Quando um documento enviado para processamento por formulários AEM for menor ou igual ao tamanho em linha máximo do documento padrão, o documento será armazenado no servidor em linha e o documento será serializado como um objeto de Documento da Adobe. Armazenar documentos em linha pode ter benefícios significativos de desempenho. No entanto, se você estiver usando o fluxo de trabalho de formulários, o conteúdo também poderá ser armazenado no banco de dados para fins de rastreamento. Portanto, aumentar o tamanho máximo em linha pode afetar o tamanho do banco de dados.

Um documento maior que o tamanho máximo em linha é armazenado no sistema de arquivos local. O objeto de Documento da Adobe transferido de e para o servidor é apenas um ponteiro para esse arquivo.

Quando o conteúdo do documento é incorporado (ou seja, menor que o tamanho máximo em linha), o conteúdo é armazenado no banco de dados como parte da carga da serialização do documento. Portanto, aumentar o tamanho máximo em linha pode afetar o tamanho do banco de dados.

**Alterar o tamanho máximo em linha**

1. No console de administração, clique em Configurações > Configurações principais do sistema > Configurações.
1. Enter a value in the Default Document Max Inline Size box and click OK.

   >[!NOTE]
   >
   >The value of Document Max Inline Size property must be identical for AEM Forms on JEE environment and AEM Forms on OSGi bundle included AEM Forms on JEE environment. This steps updated value only for AEM Forms on JEE environment and not for AEM Forms on OSGi bundle included AEM Forms on JEE environment.

1. Restart the application server with the following system property:

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >The above-mentioned system property overrides value of Document Max Inline Size property set for AEM Forms on JEE environment and AEM Forms on OSGi bundle included AEM Forms on JEE environment.

>[!NOTE]
>
>O tamanho padrão máximo em linha é de 65536 bytes.

### JVM maximum heap size {#jvm-maximum-heap-size}

An increase in the maximum inline size requires more memory for storing the serialized documents. Therefore, it generally also requires an increase in the JVM maximum heap size.

A heavily loaded system that is processing many documents can rapidly saturate the JVM heap memory. Para evitar um OutOfMemoryError, aumente o tamanho máximo do heap da JVM em uma quantidade correspondente ao tamanho dos documentos em linha multiplicado pelo número de documentos que normalmente são executados em um determinado momento.

Aumento do tamanho máximo do heap JVM = (tamanho dos documentos em linha) x (número médio de documentos processados).

**Cálculo do tamanho máximo do heap JVM**

Neste exemplo, o heap máximo JVM atual está definido como 512 MB e o tamanho máximo em linha é 64 KB. O servidor deve ser configurado para o cenário em que 10 trabalhos são executados simultaneamente e cada tarefa tem 9 arquivos de entrada e 1 arquivo de resultado (um total de 10 arquivos por tarefa e 100 arquivos processados simultaneamente). Todos os arquivos têm menos de 512 KB.

Para armazenar todos os arquivos em linha, defina o tamanho máximo em linha de pelo menos 512 KB.

O aumento necessário no tamanho máximo do heap JVM é calculado usando a seguinte equação:

(512 KB) x (100) = 51200 KB, ou 50 MB

O tamanho máximo do heap JVM deve ser aumentado em 50 MB para um total de 562 MB.

**Considerando a fragmentação do heap**

A definição do tamanho dos documentos em linha para valores grandes aumenta o risco de um OutOfMemoryError em sistemas que são propensos a hepar a fragmentação. Para armazenar um documento em linha, a memória do heap JVM deve ter espaço contíguo suficiente. Alguns sistemas operacionais, JVMs e algoritmos de coleta de lixo estão sujeitos à fragmentação do heap. A fragmentação diminui a quantidade de espaço de heap contíguo e pode levar a um OutOfMemoryError mesmo quando existe espaço livre total suficiente.

Por exemplo, operações anteriores no servidor de aplicativos deixaram o heap JVM em um estado fragmentado e o coletor de lixo não pode compactar o heap o suficiente para recuperar grandes blocos de espaço livre. Um OutOfMemoryError pode ocorrer mesmo que o tamanho máximo do heap JVM tenha sido ajustado para um aumento no tamanho máximo em linha.

Para contabilizar a fragmentação do heap, o tamanho do documento em linha não deve ser definido acima de 0,1% do tamanho total do heap. Por exemplo, um tamanho máximo de heap JVM de 512 MB pode suportar um tamanho máximo em linha de 512 MB x 0,001 = 0,512 MB, ou 512 KB.

## Aprimoramentos do WebSphere Application Server {#websphere-application-server-enhancements}

Esta seção descreve as configurações específicas de um ambiente do WebSphere Application Server.

### Aumentando a memória máxima alocada para a JVM {#increasing-the-maximum-memory-allocated-to-the-jvm}

Se você estiver executando o Configuration Manager ou tentando gerar o código de implantação do Enterprise JavaBeans (EJB) usando o utilitário de linha de comando *ejbdeployment* e ocorrer um erro OutOfMemory, aumente a quantidade de memória alocada para a JVM.

1. Edite o script ejbdeploy no diretório raiz *[/deploytool/itp/ do]* appserver:

   * (Windows) `ejbdeploy.bat`
   * (Linux e UNIX) `ejbdeploy.sh`

1. Localize o `-Xmx256M` parâmetro e altere-o para um valor maior, como `-Xmx1024M`.
1. Salve o arquivo.
1. Execute o `ejbdeploy` comando ou reimplante usando o Configuration Manager.

## Melhorando o desempenho do Windows Server 2003 com LDAP {#improving-windows-server-2003-performance-with-ldap}

Este conteúdo descreve as configurações específicas de um ambiente do sistema operacional Microsoft Windows Server 2003.

O uso do pooling de conexão na conexão de pesquisa pode diminuir o número de portas necessárias em até 50%. Isso ocorre porque essa conexão sempre usa as mesmas credenciais para um determinado domínio, e o contexto e os objetos relacionados são fechados explicitamente.

### Configurar o Windows Server para pooling de conexão {#configure-your-windows-server-for-connection-pooling}

1. Clique em Start > Executar para start do editor de registro e, na caixa Abrir, digite `regedit` e clique em OK.
1. Ir para a chave do Registro `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. No painel direito do editor do Registro, localize o nome do valor TcpTimedWaitDelay. Se o nome não for exibido, selecione Editar > Novo > Valor DWORD na barra de menus para adicionar o nome.
1. Na caixa Nome, digite `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >Se você não vir um cursor piscando e `New Value #` dentro da caixa, clique com o botão direito do mouse dentro do painel direito, selecione Renomear e, na caixa Nome, digite `TcpTimedWaitDelay`*.*

1. Repita a etapa 4 para os nomes MaxUserPort, MaxHashTableSize e MaxFreeTcbs.
1. Clique com o Duplo no painel direito para definir o valor TcpTimedWaitDelay. Em Base, selecione Decimal e, na caixa Valor, digite `30`.
1. Clique com o Duplo no painel direito para definir o valor MaxUserPort. Em Base, selecione Decimal e, na caixa Valor, digite `65534`.
1. Clique com o Duplo no painel direito para definir o valor MaxHashTableSize. Em Base, selecione Decimal e, na caixa Valor, digite `65536`.
1. Clique com o Duplo no painel direito para definir o valor MaxFreeTcbs. Em Base, selecione Decimal e, na caixa Valor, digite `16000`.

>[!NOTE]
>
>Problemas graves podem ocorrer se você modificar o Registro incorretamente usando o Editor do Registro ou outro método. Esses problemas podem exigir a reinstalação do sistema operacional. Modifique o registro por sua conta e risco.

