---
title: Configurações gerais do AEM Forms
seo-title: General AEM Forms settings
description: Saiba como definir as configurações da página Configurações principais no console de administração que pode ajudar a melhorar o desempenho do sistema.
seo-description: Learn to configure the Core Configurations page settings in administration console that can help improve system performance.
uuid: 940680fd-b7ab-4376-aa5b-e139223522ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bd648c38-731b-420e-973d-a4728b69868e
exl-id: e1519477-b5a8-4947-8597-26b945a3b819
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 1%

---

# Configurações gerais do AEM Forms {#general-aem-forms-settings}

A página Configurações principais no console de administração fornece configurações que podem ajudar a melhorar o desempenho do sistema. Após definir ou atualizar essas configurações, reinicie o servidor de aplicativos.

Para obter informações sobre como ativar o modo de backup seguro, consulte [Ativação e desativação do modo de backup seguro](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>Os arquivos no diretório temporário e os documentos de longa duração no diretório raiz do armazenamento global de documentos (GDS) podem conter informações confidenciais do usuário, como informações que exigem credenciais especiais quando acessadas usando as APIs ou interfaces do usuário. Portanto, é importante que esse diretório seja protegido adequadamente usando os métodos disponíveis para o sistema operacional. Recomenda-se que somente a conta do sistema operacional usada para executar o servidor de aplicativos tenha acesso de leitura e gravação a esse diretório.


1. No console de administração, clique em **[!UICONTROL Configurações > Configurações principais do sistema > Configurações]**.
1. Na página Configurações principais , altere as opções conforme necessário e clique em **[!UICONTROL OK]**. Para obter detalhes sobre as opções, consulte [Opções de configurações principais](configure-general-aem-forms-settings.md#core-configurations-options).


## Opções de configurações principais {#core-configurations-options}

**Localização do diretório temporário** O caminho do diretório onde AEM formulários criarão arquivos temporários do produto. Se o valor dessa configuração estiver vazio, o local assumirá como padrão o diretório temporário do sistema. Certifique-se de que o diretório temporário seja uma pasta gravável.

>[!NOTE]
>
>Certifique-se de que o diretório temporário esteja no sistema de arquivos local. AEM forms não suporta um diretório temporário em um local remoto.

**Diretório raiz de armazenamento de documentos global** O diretório raiz do armazenamento de documento global (GDS) é usado para os seguintes fins:

* Armazenando documentos de longa duração. Documentos de vida longa não têm um tempo de expiração e persistem até serem removidos (por exemplo, os arquivos PDF usados em um processo de fluxo de trabalho). Os documentos de longa duração são uma parte essencial do estado geral do sistema. Se alguns ou todos esses documentos forem perdidos ou corrompidos, o servidor de formulários poderá se tornar instável. Portanto, é importante que esse diretório seja armazenado em um dispositivo RAID.
* Armazenando documentos temporários necessários durante o processamento.

>[!NOTE]
>
>Você também pode ativar o armazenamento de documentos no banco de dados de formulários AEM. No entanto, o desempenho do sistema é melhor quando você usa o GDS.

* Transferência de documentos entre nós em um cluster. Se você estiver executando AEM formulários em um ambiente em cluster, esse diretório deverá estar acessível de todos os nós no cluster.
* Recebendo parâmetros recebidos de chamadas remotas da API.

Se você não especificar um diretório raiz GDS, o diretório assumirá como padrão um diretório de servidor de aplicativos:

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>A alteração do valor da configuração do diretório raiz GDS deve ser feita com cuidado especial. O diretório GDS é usado para armazenar arquivos de longa duração usados em um processo, bem como componentes de produto de formulários AEM críticos. Alterar a localização do diretório GDS é uma alteração importante do sistema. A configuração incorreta do local do diretório GDS tornará AEM formulários inoperacionais e poderá exigir uma reinstalação completa de AEM formulários. Se você especificar um novo local para o diretório GDS, o servidor de aplicativos precisará ser desligado e os dados migrados antes que o servidor possa ser reiniciado. O administrador do sistema deve mover todos os arquivos do local antigo para o novo local, mas manter a estrutura do diretório interno.

>[!NOTE]
>
>Não especifique o mesmo diretório para o diretório temporário e o diretório GDS.

Para obter informações adicionais sobre o diretório GDS, consulte [Preparação para instalar formulários de AEM (Servidor único)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Localização do diretório de fontes do servidor Adobe** Digite o caminho para o diretório que contém as fontes do servidor Adobe. Essas fontes são instaladas com formulários AEM. O local padrão para essas fontes é o [raiz do aem-forms]diretório /fonts. Se esse diretório não estiver acessível, você poderá copiar as fontes em outro lugar e usar essa configuração para especificar o novo local.

**Localização do diretório de fontes do cliente** Digite o caminho para um diretório que contenha fontes adicionais que você deseja usar.

***observação **: As fontes são selecionadas do cache de fontes do sistema Windows e é necessário reiniciar o sistema para atualizar o cache. Depois de especificar o diretório de fontes do cliente, reinicie o sistema no qual AEM formulários está instalado.*

**Localização do diretório de fontes do sistema** Digite o caminho para o diretório de fontes fornecido pelo sistema operacional. Vários diretórios podem ser adicionados, separados por ponto e vírgula **;**.

**Localização do arquivo de configuração dos serviços de dados** Especifica o local do arquivo services-config.xml. Por padrão, esse arquivo é incorporado no arquivo adobe-core-appserver.ear e não é acessível ao usuário. Uma cópia do arquivo services-config.xml padrão está localizada em [raiz do aem-forms]\sdk\misc\DataServices\Server-Configuration. Se você alterou esse arquivo e o moveu, digite o novo local neste campo.

O arquivo de configuração dos Serviços de dados permite a personalização das configurações dos Serviços de dados, como tipo de autenticação e saída de depuração.

Essa configuração fica vazia por padrão.

**Tamanho máximo em linha do documento padrão (bytes)** O número máximo de bytes mantidos na memória ao transmitir documentos entre vários componentes de formulários AEM. Use esta configuração para ajuste de desempenho. Os documentos menores que esse número são armazenados na memória e mantidos no banco de dados. Os documentos que excedem esse máximo são armazenados no disco rígido.

Essa configuração é obrigatória. O valor padrão é 65536 bytes.

**Tempo limite de eliminação de documentos predefinido (segundos)** O tempo máximo, em segundos, durante o qual um documento que está sendo transmitido entre vários componentes de formulários AEM é considerado ativo. Após esse tempo, os arquivos usados para armazenar este documento estarão sujeitos à remoção. Use essa configuração para controlar o uso do espaço em disco.

Essa configuração é obrigatória. O valor padrão é de 600 segundos.

**Intervalo de varredura do documento (segundos)** O tempo, em segundos, entre as tentativas de excluir arquivos que não são mais necessários e foram usados para transmitir dados do documento entre os serviços.

Essa configuração é obrigatória. O valor padrão é de 30 segundos.

**Ativar FIPS** Selecione esta opção para ativar o modo FIPS. O Federal Information Processing Standard (FIPS) 140-2 é um padrão de criptografia definido pelo governo dos Estados Unidos. Ao executar no modo FIPS, AEM formulários restringe a proteção de dados a algoritmos aprovados pelo FIPS 140-2 usando o módulo de criptografia RSA BSAFE Crypto-C 2.1.

O modo FIPS não suporta algoritmos de criptografia usados em versões Adobe Acrobat® anteriores à 7.0. Se o modo FIPS estiver ativado e você usar o serviço de Criptografia para criptografar o PDF usando uma senha com um nível de compatibilidade definido como Acrobat 5, a tentativa de criptografia falhará com um erro.

Em geral, quando o FIPS estiver ativado, o serviço Assembler não aplicará a criptografia de senha a nenhum documento. Se isso for tentado, um FIPSModeException será lançado, indicando que &quot;A criptografia de senha não é permitida no modo FIPS&quot;. Além disso, o elemento PDFsFromBookmarks XML (DDX) da Descrição do Documento não é compatível no modo FIPS quando o documento base é criptografado por senha.

>[!NOTE]
>
>AEM software forms não valida o código para garantir a compatibilidade com FIPS. Ele fornece um modo de operação FIPS para que os algoritmos aprovados pelo FIPS sejam usados para serviços criptográficos a partir das bibliotecas aprovadas pelo FIPS (RSA).

**Ativar WSDL** Selecione essa opção para ativar a geração WSDL (Linguagem de definição de serviço da Web) para todos os serviços que fazem parte AEM formulários.

Ative essa opção em ambientes de desenvolvimento, onde os desenvolvedores usam a geração WSDL para criar seus aplicativos clientes. Você pode optar por desativar a geração de WSDL em um ambiente de produção para evitar a exposição dos detalhes internos de um serviço.

**Habilitar armazenamento de documentos no banco de dados** Selecione essa opção para armazenar documentos de longa duração no banco de dados de formulários AEM. Habilitar essa opção não remove a necessidade de um diretório GDS. No entanto, escolher essa opção simplifica os backups de formulários AEM. Se você usar apenas o GDS, um backup envolve colocar o sistema AEM formsAEM forms em modo de backup e, em seguida, concluir os backups do banco de dados e do GDS. Se você selecionar a opção do banco de dados, o backup envolve concluir o backup do banco de dados para uma nova instalação ou concluir o backup do banco de dados e o backup único do GDS para uma atualização. O gerenciamento adicional do banco de dados pode ser necessário para limpar tarefas e dados em comparação a uma configuração somente GDS. (Consulte Opções de backup quando o banco de dados é usado para armazenamento de documentos.)

**Ativar estatística de invocação DSC** Quando essa opção é selecionada, o AEM forms rastreia estatísticas de invocação, como o número de invocações, a quantidade de tempo para invocar e o número de erros em invocações. Essas informações são armazenadas em um Bean JMX para que você possa usar o Java™ JConsole ou software de terceiros para analisar as estatísticas. Se não quiser ver essas estatísticas, desmarque essa opção para melhorar o desempenho AEM formulários.

**Ativar RDS** A seleção dessa opção ativa o servlet dos Serviços de desenvolvimento remoto (RDS) em AEM formulários. Quando essa opção é ativada, as ferramentas do lado do cliente podem interagir com os Serviços de dados para fazer coisas como implantar ou cancelar a implantação de modelos para criar destinos e endpoints, ou descobrir quais modelos foram implantados em endpoints. Por padrão, essa opção não está selecionada.

**Permitir solicitação RDS não segura** Quando essa opção é selecionada, as solicitações de RDS não precisam usar https. Por padrão, essa opção não está selecionada e todas as comunicações para os Serviços de dados precisam ser solicitações https.

**Permitir o upload de documentos não protegidos de aplicativos Flex:** O servlet de upload de arquivos usado para fazer upload de documentos de aplicativos Adobe Flex® para AEM formulários exige que os usuários sejam autenticados e autorizados antes de poderem fazer upload de documentos. O usuário deve receber a função Usuário do Aplicativo de Upload de Documento ou outra função que inclua a permissão Upload de Documento. Isso ajuda a impedir que usuários não autorizados façam upload de documentos para o servidor de formulários AEM. Selecione essa opção se desejar desativar esse recurso de segurança em um ambiente de desenvolvimento ou para compatibilidade com versões anteriores de formulários AEM. Por padrão, essa opção não está selecionada. Para obter detalhes, consulte &quot;Chamar formulários AEM usando AEM formulário remoto&quot; em Programação com formulários AEM.

**Permitir o upload de documentos não protegidos de aplicativos Java SDK:** Os uploads do DocumentManager HTTP devem ser protegidos. Por padrão, os uploads de HTTP exigem que os usuários sejam autenticados e autorizados antes de poderem fazer upload de documentos. O usuário deve receber a função de Usuário de Serviços ou outra função que contenha a permissão de Chamada de Serviço. Isso ajuda a impedir que usuários não autorizados façam upload de documentos para o servidor de formulários. Selecione essa opção se quiser desativar esse recurso de segurança em um ambiente de desenvolvimento, para compatibilidade com versões anteriores de formulários AEM ou com base na configuração do firewall. Por padrão, essa opção não está selecionada. Para obter detalhes, consulte &quot;Chamar formulários AEM usando a API Java&quot; em Programação com formulários AEM.
