---
title: Configurações gerais do AEM Forms
seo-title: Configurações gerais do AEM Forms
description: Saiba como configurar as configurações da página Principais configurações no console de administração que podem ajudar a melhorar o desempenho do sistema.
seo-description: Saiba como configurar as configurações da página Principais configurações no console de administração que podem ajudar a melhorar o desempenho do sistema.
uuid: 940680fd-b7ab-4376-aa5b-e139223522ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
discoiquuid: bd648c38-731b-420e-973d-a4728b69868e
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Configurações gerais do AEM Forms {#general-aem-forms-settings}

A página Configurações principais no console de administração fornece configurações que podem ajudar a melhorar o desempenho do sistema. Após definir ou atualizar essas configurações, reinicie o servidor de aplicativos.

Para obter informações sobre como ativar o modo de backup seguro, consulte [Ativar e desativar o modo](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode)de backup seguro.


>[!NOTE]
>
>Os arquivos no diretório temporário e os documentos de longa duração no diretório raiz GDS (armazenamento global) podem conter informações confidenciais do usuário, como informações que exigem credenciais especiais quando acessadas por meio das APIs ou interfaces do usuário. Portanto, é importante que esse diretório esteja adequadamente protegido usando quaisquer métodos disponíveis para o sistema operacional. É recomendável que somente a conta do sistema operacional usada para executar o servidor de aplicativos tenha acesso de leitura e gravação a esse diretório.


1. No console de administração, clique em **[!UICONTROL Configurações > Configurações principais do sistema > Configurações]**.
1. Na página Configurações principais, altere as opções conforme necessário e clique em **[!UICONTROL OK]**. Para obter detalhes sobre as opções, consulte Opções [de configurações](configure-general-aem-forms-settings.md#core-configurations-options)principais.


## Opções de configurações principais {#core-configurations-options}

**Localização do diretório** temporário O caminho do diretório onde os formulários AEM criarão arquivos temporários do produto. Se o valor dessa configuração estiver vazio, o local assumirá como padrão o diretório temporário do sistema. Verifique se o diretório temporário é uma pasta gravável.

>[!NOTE]
>
>Verifique se o diretório temporário está no sistema de arquivos local. Os formulários AEM não oferecem suporte a um diretório temporário em um local remoto.

**Diretório** raiz do armazenamento global O diretório raiz do armazenamento global do documento (GDS) é usado para os seguintes fins:

* Armazenando documentos de vida longa. Os documentos de longa duração não têm um tempo de expiração e persistem até serem removidos (por exemplo, os arquivos PDF usados em um processo de fluxo de trabalho). Os documentos de longa duração são uma parte crítica do estado geral do sistema. Se alguns ou todos esses documentos forem perdidos ou corrompidos, o servidor de formulários poderá ficar instável. Portanto, é importante que esse diretório seja armazenado em um dispositivo RAID.
* Armazenamento de documentos temporários necessários durante o processamento.

>[!NOTE]
>
>Você também pode ativar o armazenamento de documentos no banco de dados de formulários do AEM. No entanto, o desempenho do sistema é melhor quando você usa o GDS.

* Transferência de documentos entre nós em um cluster. Se você estiver executando formulários AEM em um ambiente clusterizado, esse diretório deverá estar acessível de todos os nós dentro do cluster.
* Recebendo parâmetros de entrada de chamadas de API remotas.

Se você não especificar um diretório raiz GDS, o diretório assumirá como padrão um diretório do servidor de aplicativos:

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>A alteração do valor da configuração do diretório raiz GDS deve ser feita com cuidado especial. O diretório GDS é usado para armazenar arquivos de longa duração usados em um processo, bem como componentes críticos do produto para formulários AEM. Alterar a localização do diretório GDS é uma alteração importante do sistema. Configurar incorretamente o local do diretório GDS tornará os formulários AEM inoperantes e pode exigir uma reinstalação completa dos formulários AEM. Se você especificar um novo local para o diretório GDS, o servidor de aplicativos precisará ser desligado e os dados migrados antes que o servidor possa ser reiniciado. O administrador do sistema deve mover todos os arquivos do local antigo para o novo local, mas manter a estrutura do diretório interno.

>[!NOTE]
>
>Não especifique o mesmo diretório para o diretório temporário e o diretório GDS.

Para obter informações adicionais sobre o diretório GDS, consulte [Preparação para instalar formulários AEM (Single Server)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Localização do diretório** Fontes do Adobe Server Digite o caminho para o diretório que contém as fontes do servidor Adobe. Essas fontes são instaladas com formulários AEM. O local padrão dessas fontes é o diretório raiz [/fontes de formulários]aem. Se esse diretório não estiver acessível, você poderá copiar as fontes em outro lugar e usar essa configuração para especificar o novo local.

**Localização do diretório** Fontes do clienteDigite o caminho para um diretório que contenha fontes adicionais que você deseja usar.

***observação **: As fontes são escolhidas do cache de fontes do sistema do Windows e é necessário reiniciar o sistema para atualizar o cache. Depois de especificar o diretório de fontes do Cliente, reinicie o sistema no qual os formulários AEM estão instalados.*

**Localização do diretório** Fontes do sistema Digite o caminho para o diretório de fontes fornecido pelo sistema operacional. Vários diretórios podem ser adicionados, separados por ponto-e-vírgula **;**.

**Localização do arquivo** de Configuração dos Serviços de Dados Especifica o local do arquivo services-config.xml. Por padrão, esse arquivo é incorporado ao arquivo adobe-core-appserver.ear e não é acessível ao usuário. Uma cópia do arquivo padrão services-config.xml está localizada em [aem-forms root]\sdk\misc\DataServices\Server-Configuration. Se você alterou esse arquivo e o moveu, digite o novo local nesse campo.

O arquivo de configuração dos Serviços de dados permite a personalização das configurações dos Serviços de dados, como o tipo de autenticação e a saída de depuração.

Esta configuração está vazia por padrão.

**Tamanho inline máximo de documento padrão (bytes)** O número máximo de bytes mantidos na memória ao passar documentos entre vários componentes de formulários AEM. Use essa configuração para ajuste de desempenho. Documentos menores que esse número são armazenados na memória e persistentes no banco de dados. Os Documentos que excedem esse máximo são armazenados no disco rígido.

Esta configuração é obrigatória. O valor padrão é 65536 bytes.

**Tempo limite de descarte do documento padrão (segundos)** O tempo máximo, em segundos, durante o qual um documento que está sendo transmitido entre vários componentes de formulários AEM é considerado ativo. Após esse tempo, os arquivos usados para armazenar esse documento serão removidos. Use essa configuração para controlar o uso do espaço em disco.

Esta configuração é obrigatória. O valor padrão é 600 segundos.

**Intervalo de varredura do Documento (segundos)** A quantidade de tempo, em segundos, entre as tentativas de excluir arquivos que não são mais necessários e que foram usados para transmitir dados do documento entre os serviços.

Esta configuração é obrigatória. O valor padrão é 30 segundos.

**Habilitar FIPS** Selecione esta opção para habilitar o modo FIPS. O Federal Information Processing Standard (FIPS) 140-2 é um padrão de criptografia definido pelo governo dos Estados Unidos. Durante a execução no modo FIPS, os formulários AEM restringem a proteção de dados a algoritmos aprovados pelo FIPS 140-2 usando o módulo de criptografia RSA BSAFE Crypto-C 2.1.

O modo FIPS não oferece suporte a algoritmos de criptografia usados em versões do Adobe Acrobat® anteriores à 7.0. Se o modo FIPS estiver ativado e você usar o serviço de Criptografia para criptografar o PDF usando uma senha com um nível de compatibilidade definido como Acrobat 5, a tentativa de criptografia falhará com um erro.

Em geral, quando o FIPS estiver ativado, o serviço Assembler não aplicará criptografia de senha a nenhum documento. Se isso for tentado, um FIPSModeException será lançado indicando que &quot;A criptografia de senha não é permitida no modo FIPS&quot;. Além disso, o elemento XML de descrição do Documento (DDX) PDFsFromBookmarks não é suportado no modo FIPS quando o documento base é criptografado por senha.

>[!NOTE]
>
>O software de formulários AEM não valida o código para garantir a compatibilidade com FIPS. Ele fornece um modo de operação FIPS para que os algoritmos aprovados pelo FIPS sejam usados para serviços de criptografia das bibliotecas aprovadas pelo FIPS (RSA).

**Habilitar WSDL** Selecione essa opção para habilitar a geração WSDL (Web Service Definition Language) para todos os serviços que fazem parte dos formulários do AEM.

Ative essa opção em ambientes de desenvolvimento, onde os desenvolvedores usam a geração WSDL para criar seus aplicativos clientes. Você pode optar por desativar a geração WSDL em um ambiente de produção para evitar a exposição dos detalhes internos de um serviço.

**Ativar armazenamento de documento no banco de dados** Selecione esta opção para armazenar documentos de longa duração no banco de dados de formulários do AEM. Habilitar essa opção não remove a necessidade de um diretório GDS. No entanto, escolher essa opção simplifica os backups de formulários do AEM. Se você usar apenas o GDS, um backup envolve colocar o sistema de formulários AEM em modo de backup e, em seguida, concluir os backups do banco de dados e do GDS. Se você selecionar a opção do banco de dados, o backup envolve a conclusão do backup do banco de dados para uma nova instalação ou a conclusão do backup do banco de dados e o backup único do GDS para uma atualização. O gerenciamento adicional do banco de dados pode ser necessário para expurgar trabalhos e dados em comparação a uma configuração somente GDS. (Consulte Opções de backup quando o banco de dados é usado para o armazenamento do documento.)

**Ativar estatística** de invocação do DSC Quando essa opção é selecionada, os formulários do AEM rastreiam estatísticas de invocação, como o número de invocações, o tempo necessário para invocar e o número de erros nas invocações. Essas informações são armazenadas em um bean JMX para que você possa usar o Java™ JConsole ou software de terceiros para verificar as estatísticas. Se não quiser ver essas estatísticas, desmarque essa opção para melhorar o desempenho dos formulários do AEM.

**Ativar RDS** A seleção dessa opção ativa o servlet RDS (Remote Development Services, Serviços de desenvolvimento remoto) nos formulários AEM. Quando essa opção está ativada, as ferramentas do cliente podem interagir com os Serviços de dados para fazer coisas como implantar ou desimplantar modelos para criar destinos e pontos de extremidade, ou descobrir quais modelos foram implantados nos pontos de extremidade. Por padrão, essa opção não está selecionada.

**Permitir solicitação** RDS não seguras Quando essa opção é selecionada, as solicitações RDS não precisam usar https. Por padrão, essa opção não está selecionada e todas as comunicações para os Serviços de dados precisam ser solicitações https.

**Permitir upload de documentos não protegidos de aplicativos Flex:** O servlet de upload de arquivos usado para carregar documentos de aplicativos Adobe Flex® para formulários AEM exige que os usuários sejam autenticados e autorizados antes de poderem carregar documentos. O usuário deve receber a função Usuário do aplicativo de upload do Documento ou outra função que inclua a permissão de Upload do Documento. Isso ajuda a impedir que usuários não autorizados façam upload de documentos no servidor de formulários do AEM. Selecione essa opção se desejar desativar esse recurso de segurança em um ambiente de desenvolvimento ou para compatibilidade retroativa com versões anteriores de formulários AEM. Por padrão, essa opção não está selecionada. Para obter detalhes, consulte &quot;Invocar formulários AEM usando o AEM Forms Remoting&quot; em Programação com formulários AEM.

**Permitir o upload de documentos não protegidos de aplicativos Java SDK:** Os uploads HTTP do DocumentManager devem estar protegidos. Por padrão, os uploads HTTP exigem que os usuários sejam autenticados e autorizados antes de poderem carregar documentos. Ao usuário deve ser atribuída a função Usuário de Serviços ou outra função que contenha a permissão Chamada de Serviço. Isso ajuda a impedir que usuários não autorizados façam upload de documentos no servidor de formulários. Selecione essa opção se desejar desativar esse recurso de segurança em um ambiente de desenvolvimento, para compatibilidade retroativa com versões anteriores de formulários AEM ou com base na configuração do firewall. Por padrão, essa opção não está selecionada. Para obter detalhes, consulte &quot;Invocar formulários AEM usando a API Java&quot; em Programação com formulários AEM.
