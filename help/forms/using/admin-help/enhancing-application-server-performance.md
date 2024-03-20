---
title: Aprimoramento do desempenho do servidor de aplicativos
description: Este documento descreve as configurações opcionais que você pode definir para melhorar o desempenho do servidor de aplicativos de formulários AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6e2f3d4c-2ead-45b3-98e7-32cacc7e2985
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1870'
ht-degree: 0%

---

# Aprimoramento do desempenho do servidor de aplicativos{#enhancing-application-server-performance}

Este conteúdo descreve as configurações opcionais que você pode configurar para melhorar o desempenho do servidor de aplicativos de formulários AEM.

## Configurando origens de dados do servidor de aplicações {#configuring-application-server-data-sources}

O AEM Forms usa o repositório de formulários AEM como fonte de dados. O repositório de formulários AEM armazena ativos de aplicativos e, no tempo de execução, os serviços podem recuperar ativos do repositório como parte da conclusão de um processo de negócios automatizado.

O acesso à fonte de dados pode ser significativo, dependendo do número de módulos de formulários AEM que você está executando e do número de usuários simultâneos que acessam o aplicativo. O acesso à fonte de dados pode ser otimizado usando o pool de conexões. *Pool de conexão* é uma técnica usada para evitar a sobrecarga de fazer novas conexões de banco de dados sempre que um aplicativo ou objeto de servidor exigir acesso ao banco de dados. O pool de conexões é geralmente usado em aplicativos empresariais e baseados na Web e geralmente é manipulado por, mas não limitado a, um servidor de aplicativos.

É importante configurar corretamente os parâmetros do pool de conexões para que as conexões não fiquem esgotadas, o que pode deteriorar o desempenho do aplicativo.

Para definir corretamente as configurações do pool de conexões, é importante que o administrador do servidor de aplicativos monitore o pool de conexões durante os horários de pico do dia. O monitoramento garante que conexões suficientes estejam sempre disponíveis para aplicativos e usuários. A maioria dos servidores de aplicativos inclui ferramentas de monitoramento.

Você pode monitorar várias estatísticas para cada instância de origem de dados JDBC no domínio usando o Console de Administração do WebLogic Server. Consulte a documentação do WebLogic para obter detalhes.

Quando o administrador do servidor de aplicativos determina as configurações corretas do pool de conexões, essa pessoa deve comunicar essas informações ao administrador do banco de dados. O administrador do banco de dados precisa dessas informações porque o número de conexões de banco de dados é igual ao número de conexões no pool de conexões da fonte de dados. Em seguida, conclua as etapas para definir as configurações do pool de conexões para seu servidor de aplicativos e tipo de origem de dados conforme descrito abaixo.

### Configurar definições do pool de conexão do WebLogic para Oracle e MySQL {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. Em Estrutura do domínio, clique em Serviços > JDBC > Fontes de dados e, no painel direito, clique em IDP_DS.
1. Na próxima tela, clique na guia Configuração > Pool de Conexões e insira um valor nas seguintes caixas:

   * Capacidade inicial
   * Capacidade máxima
   * Incremento de capacidade
   * Tamanho do Cache de Declaração

1. Clique em Salvar e em Ativar alterações.
1. Reinicie o servidor gerenciado WebLogic.

### Configurar definições do pool de conexão do WebLogic para SQLServer {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. Em Centro de alterações, clique em Bloquear e editar.
1. Em Estrutura do domínio, clique em Serviços > JDBC > Fontes de dados e, no painel direito, clique em EDC_DS.
1. Na próxima tela, clique na guia Configuração > Pool de Conexões e insira um valor nas seguintes caixas:

   * Capacidade inicial
   * Capacidade máxima
   * Incremento de capacidade
   * Tamanho do Cache de Declaração

1. Clique em Salvar e em Ativar alterações.
1. Reinicie o servidor gerenciado WebLogic.

### Definir configurações do pool de conexão para o WebSphere for DB2 {#configure-connection-pool-settings-for-websphere-for-db2}

1. Na árvore de navegação, clique em Recursos > JDBC > Provedores JDBC. No painel direito, clique na origem de dados criada, Provedor de Driver DB2 Universal JDBC ou LiveCycle - db2 - IDP_DS.
1. Em Propriedades adicionais, clique em Fontes de dados e selecione IDP_DS.
1. Na próxima tela, em Propriedades Adicionais, clique em Propriedades do Pool de Conexões e insira um valor nas caixas Máximo de Conexões e Mínimo de Conexões.
1. Clique em OK ou em Aplicar e, em seguida, clique em Salvar diretamente na configuração principal.

### Definir configurações do pool de conexões para o WebSphere for Oracle {#configure-connection-pool-settings-for-websphere-for-oracle}

1. Na árvore de navegação, clique em Recursos > JDBC > Provedores JDBC. No painel direito, clique na fonte de dados do Driver JDBC do Oracle que você criou.
1. Em Propriedades adicionais, clique em Fontes de dados e selecione IDP_DS.
1. Na próxima tela, em Propriedades Adicionais, clique em Propriedades do Pool de Conexões e insira um valor nas caixas Máximo de Conexões e Mínimo de Conexões.
1. Clique em OK ou em Aplicar e, em seguida, clique em Salvar diretamente na configuração principal.

### Definir configurações do pool de conexões para o WebSphere for SqlServer {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. Na árvore de navegação, clique em Recursos > JDBC > Provedores JDBC e, no painel direito, clique na fonte de dados do Driver JDBC Definido pelo Usuário que você criou.
1. Em Propriedades adicionais, clique em Fontes de dados e selecione IDP_DS.
1. Na próxima tela, em Propriedades Adicionais, clique em Propriedades do Pool de Conexões e insira um valor na caixa Máximo de Conexões e na caixa Mínimo de Conexões:
1. Clique em OK ou em Aplicar e, em seguida, clique em Salvar diretamente na configuração principal.

## Otimização de documentos em linha e impacto na memória JVM {#optimizing-inline-documents-and-impact-on-jvm-memory}

Se você estiver processando documentos de tamanho relativamente pequeno, poderá melhorar o desempenho associado à velocidade de transferência de documentos e ao espaço de armazenamento. Para fazer isso, implemente as seguintes configurações de produto do AEM Forms:

* Aumente o tamanho incorporado máximo do documento padrão para formulários AEM, de modo que seja maior do que o tamanho da maioria dos documentos.
* Para processar arquivos maiores, especifique diretórios de armazenamento que estejam em um sistema de disco de alta velocidade ou em um disco RAM.

O tamanho máximo em linha e os diretórios de armazenamento (o diretório de arquivos temporários dos formulários AEM e o diretório GDS) são configurados no console de administração.

### Tamanho do documento e tamanho máximo em linha {#document-size-and-maximum-inline-size}

Quando um documento enviado para processamento por formulários AEM é menor ou igual ao tamanho máximo em linha do documento padrão, o documento é armazenado no servidor em linha e é serializado como um objeto Documento Adobe. O armazenamento de documentos em linha pode ter benefícios significativos de desempenho. No entanto, se você estiver usando o workflow de formulários, o conteúdo também poderá ser armazenado no banco de dados para fins de rastreamento. Portanto, aumentar o tamanho máximo em linha pode afetar o tamanho do banco de dados.

Um documento maior que o tamanho máximo em linha é armazenado no sistema de arquivos local. O objeto do documento de Adobe que é transferido de e para o servidor é apenas um ponteiro para esse arquivo.

Quando o conteúdo do documento é embutido (ou seja, menor que o tamanho máximo embutido), o conteúdo é armazenado no banco de dados como parte da carga de serialização do documento. Portanto, aumentar o tamanho máximo em linha pode afetar o tamanho do banco de dados.

**Alterar o tamanho máximo em linha**

1. No console de administração, clique em Configurações > Configurações do sistema principal > Configurações.
1. Insira um valor na caixa Tamanho Inline Máximo do Documento Padrão e clique em OK.

   >[!NOTE]
   >
   >O valor da propriedade Tamanho máximo em linha do documento deve ser idêntico para o ambiente AEM Forms no JEE e para o pacote AEM Forms no OSGi incluído no ambiente AEM Forms no JEE. Essas etapas atualizaram o valor somente para o ambiente AEM Forms no JEE e não para o pacote AEM Forms no OSGi incluído no ambiente AEM Forms no JEE.

1. Reinicie o servidor de aplicativos com a seguinte propriedade do sistema:

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >A propriedade do sistema mencionada acima substitui o valor da propriedade Tamanho máximo em linha do documento definido para o ambiente AEM Forms no JEE e AEM Forms no pacote OSGi incluído no ambiente AEM Forms no JEE.

>[!NOTE]
>
>O tamanho máximo em linha padrão é de 65.536 bytes.

### Tamanho máximo de heap de JVM {#jvm-maximum-heap-size}

Um aumento no tamanho máximo em linha requer mais memória para armazenar os documentos serializados. Portanto, geralmente também requer um aumento no tamanho máximo de heap do JVM.

Um sistema muito carregado que está processando muitos documentos pode saturar rapidamente a memória heap JVM. Para evitar um OutOfMemoryError, aumente o tamanho máximo do heap do JVM em uma quantidade correspondente ao tamanho dos documentos em linha multiplicado pelo número de documentos que normalmente são executados em um determinado momento.

Aumento do tamanho máximo do heap do JVM = (tamanho dos documentos em linha) x (número médio de documentos processados).

**Calculando o tamanho máximo do heap do JVM**

Neste exemplo, o heap máximo de JVM atual é definido como 512 MB e o tamanho máximo em linha é 64 KB. O servidor deve ser configurado para o cenário em que 10 trabalhos são executados simultaneamente e cada trabalho tem 9 arquivos de entrada e 1 arquivo de resultado (um total de 10 arquivos por trabalho e 100 arquivos processados simultaneamente). Todos os arquivos têm menos de 512 KB.

Para armazenar todos os arquivos em linha, defina o tamanho máximo em linha como pelo menos 512 KB.

O aumento necessário no tamanho máximo do heap do JVM é calculado usando a seguinte equação:

(512 KB) x (100) = 51200 KB ou 50 MB

O tamanho máximo do heap do JVM deve ser aumentado em 50 MB para um total de 562 MB.

**Considerar fragmentação de heap**

Definir o tamanho de documentos em linha como valores grandes aumenta o risco de um OutOfMemoryError em sistemas propensos à fragmentação de heap. Para armazenar um documento em linha, a memória heap JVM deve ter espaço contíguo suficiente. Alguns sistemas operacionais, JVMs e algoritmos de coleta de lixo são propensos à fragmentação de heap. A fragmentação diminui a quantidade de espaço de heap contíguo e pode levar a um OutOfMemoryError, mesmo quando há espaço livre total suficiente.

Por exemplo, as operações anteriores no servidor de aplicativos deixaram o heap do JVM em um estado fragmentado e o coletor de lixo não pode compactá-lo o suficiente para recuperar grandes blocos de espaço livre. Um OutOfMemoryError pode ocorrer mesmo se o tamanho máximo de heap do JVM tiver sido ajustado para um aumento no tamanho máximo em linha.

Para levar em conta a fragmentação de heap, o tamanho do documento em linha não deve ser definido como maior que 0,1% do tamanho total do heap. Por exemplo, um tamanho máximo de heap de JVM de 512 MB pode suportar um tamanho máximo em linha de 512 MB x 0,001 = 0,512 MB ou 512 KB.

## Aprimoramentos no WebSphere Application Server {#websphere-application-server-enhancements}

Esta seção descreve configurações específicas para um ambiente do WebSphere Application Server.

### Aumentando a memória máxima alocada para a JVM {#increasing-the-maximum-memory-allocated-to-the-jvm}

Se você estiver executando o Configuration Manager ou tentando gerar o código de implantação do Enterprise JavaBeans (EJB) usando o utilitário de linha de comando *ejbdeploy* e ocorrer um erro OutOfMemory, aumente a quantidade de memória alocada para a JVM.

1. Edite o script ejbdeploy na variável *[raiz do appserver]* diretório /deploytool/itp/:

   * (Windows) `ejbdeploy.bat`
   * (Linux e UNIX) `ejbdeploy.sh`

1. Localize o `-Xmx256M` e altere para um valor maior, como `-Xmx1024M`.
1. Salve o arquivo.
1. Execute o `ejbdeploy` ou reimplante usando o Configuration Manager.

## Aprimoramento do desempenho do Windows Server 2003 com LDAP {#improving-windows-server-2003-performance-with-ldap}

Este conteúdo descreve configurações específicas para um ambiente de sistema operacional Microsoft Windows Server 2003.

O uso do pool de conexões na conexão de pesquisa pode reduzir o número de portas necessárias em até 50%. Isso ocorre porque essa conexão sempre usa as mesmas credenciais para um determinado domínio, e o contexto e os objetos relacionados são fechados explicitamente.

### Configurar o Windows Server para pool de conexão {#configure-your-windows-server-for-connection-pooling}

1. Clique em Iniciar > Executar para iniciar o editor do Registro e, na caixa Abrir, digite `regedit` e clique em OK.
1. Ir para a chave do Registro `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. No painel direito do editor de registro, localize o nome do valor TcpTimedWaitDelay. Se o nome não for exibido, selecione Editar > Novo > Valor DWORD na barra de menus para adicionar o nome.
1. Na caixa Nome, digite `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >Se você não vir um cursor piscando e `New Value #` dentro da caixa, clique com o botão direito do mouse dentro do painel direito, selecione Renomear e, na caixa Nome, digite `TcpTimedWaitDelay`*.*

1. Repita a etapa 4 para os nomes de valor MaxUserPort, MaxHashTableSize e MaxFreeTcbs.
1. Clique duas vezes dentro do painel direito para definir o valor TcpTimedWaitDelay. Em Base, selecione Decimal e, na caixa Valor, digite `30`.
1. Clique duas vezes dentro do painel direito para definir o valor MaxUserPort. Em Base, selecione Decimal e, na caixa Valor, digite `65534`.
1. Clique duas vezes dentro do painel direito para definir o valor MaxHashTableSize. Em Base, selecione Decimal e, na caixa Valor, digite `65536`.
1. Clique duas vezes dentro do painel direito para definir o valor de MaxFreeTcbs. Em Base, selecione Decimal e, na caixa Valor, digite `16000`.

>[!NOTE]
>
>Problemas sérios podem ocorrer se você modificar o Registro incorretamente usando o Editor do Registro ou usando outro método. Esses problemas podem exigir a reinstalação do sistema operacional. Modifique o registro por sua conta e risco.
