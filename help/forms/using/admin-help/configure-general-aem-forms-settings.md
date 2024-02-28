---
title: Configurações gerais do AEM Forms
description: Saiba como definir as configurações da página Configurações principais no console de administração que podem ajudar a melhorar o desempenho do sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: e1519477-b5a8-4947-8597-26b945a3b819
source-git-commit: d195ac80ee59439bab5b1219a2c1f16e93e3d22b
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 0%

---

# Configurações gerais do AEM Forms {#general-aem-forms-settings}

A página Configurações principais no console de administração fornece configurações que podem ajudar a melhorar o desempenho do sistema. Após definir ou atualizar essas configurações, reinicie o servidor de aplicativos.

>[!NOTE]
>
> É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

Para obter informações sobre como ativar o modo de backup seguro, consulte [Ativando e desativando o modo de backup seguro](/help/forms/using/admin-help/enabling-disabling-safe-backup-mode.md#enabling-and-disabling-safe-backup-mode).


>[!NOTE]
>
>Os arquivos no diretório temporário e os documentos de longa duração no diretório raiz do armazenamento global de documentos (GDS) podem conter informações confidenciais do usuário, como informações que exigem credenciais especiais quando acessadas usando as APIs ou interfaces do usuário. Portanto, é importante que esse diretório seja adequadamente protegido usando os métodos disponíveis para o sistema operacional. Recomenda-se que somente a conta do sistema operacional usada para executar o servidor de aplicativos tenha acesso de leitura e gravação a esse diretório.


1. No console de administração, selecione **[!UICONTROL Configurações > Configurações principais do sistema > Configurações]**.
1. Na página Configurações principais, altere as opções conforme necessário e selecione **[!UICONTROL OK]**. Para obter detalhes sobre as opções, consulte [Opções das Configurações principais](configure-general-aem-forms-settings.md#core-configurations-options).


## Opções das Configurações principais {#core-configurations-options}

**Localização do diretório temporário** O caminho do diretório onde os formulários AEM criarão arquivos temporários do produto. Se o valor dessa configuração estiver vazio, o local assumirá como padrão o diretório temporário do sistema. Verifique se o diretório temporário é uma pasta gravável.

>[!NOTE]
>
>Certifique-se de que o diretório temporário esteja no sistema de arquivos local. O AEM Forms não suporta um diretório temporário em um local remoto.

**Diretório raiz de armazenamento de documento global** *ndash; O diretório raiz do armazenamento global de documentos (GDS) é usado para as seguintes finalidades:

* Armazenar documentos de longa vida. Os documentos de longa duração não têm um tempo de expiração e persistem até serem removidos (por exemplo, os arquivos PDF usados em um processo de workflow). Os documentos de longa duração são uma parte essencial do estado geral do sistema. Se alguns ou todos esses documentos forem perdidos ou corrompidos, o Forms Server poderá se tornar instável. Portanto, é importante que esse diretório seja armazenado em um dispositivo RAID.
* Armazenar documentos temporários necessários durante o processamento.

>[!NOTE]
>
>Você também pode habilitar o armazenamento de documentos no banco de dados de formulários AEM. No entanto, o desempenho do sistema é melhor quando você usa o GDS.

* Transferência de documentos entre nós em um cluster. Se você estiver executando formulários AEM em um ambiente clusterizado, esse diretório deverá ser acessível de todos os nós no cluster.
* Recebimento de parâmetros de entrada de chamadas de API remotas.

Se você não especificar um diretório raiz GDS, o diretório assumirá como default um diretório do servidor de aplicações:

* `[JBOSS_HOME]/server/<server>/svcnative/DocumentStorage`
* `[WEBSPHERE_HOME]/installedApps/adobe/'server'/DocumentStorage`
* `[WEBLOGIC_HOME]/user_projects/<domain>/'server'/adobe/AEMformsserver/DocumentStorage`

>[!NOTE]
>
>A alteração do valor da configuração do diretório raiz GDS deve ser feita com especial cuidado. O diretório GDS é usado para armazenar arquivos de longa duração usados em um processo e componentes críticos do produto de formulários AEM. A alteração do local do diretório GDS é uma grande alteração do sistema. A configuração incorreta da localização do diretório GDS tornará os formulários AEM inoperantes e poderá exigir a reinstalação completa dos formulários AEM. Se você especificar um novo local para o diretório GDS, o servidor de aplicativos precisará ser desligado e os dados migrados antes que o servidor possa ser reiniciado. O administrador do sistema deve mover todos os arquivos do local antigo para o novo local, mas manter a estrutura do diretório interno.

>[!NOTE]
>
>Não especifique o mesmo diretório para o diretório temp e o diretório GDS.

Para obter informações adicionais sobre o diretório GDS, consulte [Preparação para instalar formulários AEM (servidor único)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63).

**Localização do diretório Adobe Server Fonts** *ndash; Digite o caminho para o diretório que contém as fontes do servidor Adobe. Essas fontes são instaladas com formulários AEM. O local padrão para essas fontes é o [raiz de aem-forms]diretório /fonts. Se este diretório não estiver acessível, você poderá copiar as fontes em outro lugar e usar esta configuração para especificar o novo local.

**Localização do diretório de fontes do cliente** *ndash; Digite o caminho para um diretório que contenha fontes adicionais que você deseja usar.

***observação **: as fontes são extraídas do cache de fontes do sistema do Windows e é necessário reiniciar o sistema para atualizar o cache. Depois de especificar o diretório de fontes do Cliente, reinicie o sistema no qual o AEM Forms está instalado.*

**Localização do diretório de Fontes do Sistema** *ndash; Digite o caminho para o diretório de fontes fornecido pelo seu sistema operacional. É possível adicionar vários diretórios, separados por ponto e vírgula **;**.

**Local do arquivo de configuração dos serviços de dados** *ndash; Especifica o local do arquivo services-config.xml. Por padrão, esse arquivo é incorporado ao arquivo adobe-core-appserver.ear e não é acessível ao usuário. Uma cópia do arquivo services-config.xml padrão está em [raiz de aem-forms]\sdk\misc\DataServices\Server-Configuration. Se você alterou este arquivo e o moveu, digite o novo local neste campo.

O arquivo de configuração do Data Services permite a personalização das configurações do Data Services, como tipo de autenticação e saída de depuração.

Essa configuração fica vazia por padrão.

**Tamanho máximo em linha do documento padrão (bytes)** *ndash; O número máximo de bytes mantidos na memória ao transmitir documentos entre vários componentes de formulários AEM. Use esta definição para ajustar o desempenho. Os documentos menores que esse número são armazenados na memória e mantidos no banco de dados. Os documentos que excedem esse máximo são armazenados no disco rígido.

Esta configuração é obrigatória. O valor padrão é 65536 bytes.

**Tempo limite padrão de descarte de documentos (segundos)** *ndash; O tempo máximo, em segundos, durante o qual um documento que está sendo transmitido entre vários componentes de formulários AEM é considerado ativo. Após esse período, os arquivos usados para armazenar esse documento estarão sujeitos à remoção. Use esta configuração para controlar o uso do espaço em disco.

Esta configuração é obrigatória. O valor padrão é de 600 segundos.

**Intervalo de varredura do documento (segundos)** *ndash; O tempo, em segundos, entre tentativas de excluir arquivos que não são mais necessários e que foram usados para transmitir dados de documentos entre serviços.

Esta configuração é obrigatória. O valor padrão é de 30 segundos.

**Habilitar FIPS** *ndash; Selecione esta opção para ativar o modo FIPS. O FIPS (Federal Information Processing Standard, padrão federal de processamento de informações) 140-2 é um padrão de criptografia definido pelo governo dos EUA. Quando executados no modo FIPS, os formulários AEM restringem a proteção de dados a algoritmos aprovados pelo FIPS 140-2 usando o módulo de criptografia RSA BSAFE Crypto-C 2.1.

O modo FIPS não suporta algoritmos de criptografia usados nas versões Adobe Acrobat® anteriores à 7.0. Se o modo FIPS estiver ativado e você usar o serviço de criptografia para criptografar o PDF usando uma senha com um nível de compatibilidade definido como Acrobat 5, a tentativa de criptografia falhará com um erro.

Em geral, quando o FIPS está habilitado, o serviço Assembler não aplicará a criptografia de senha a nenhum documento. Se isso for tentado, um FIPSModeException é lançado, indicando que &quot;A criptografia de senha não é permitida no modo FIPS&quot;. Além disso, o elemento PDFsFromBookmarks de Descrição do documento XML (DDX) não é compatível com o modo FIPS quando o documento base é criptografado por senha.

>[!NOTE]
>
>O software AEM Forms não valida o código para garantir a compatibilidade com FIPS. Ele fornece um modo de operação FIPS para que os algoritmos aprovados pelo FIPS sejam usados para serviços de criptografia das bibliotecas aprovadas pelo FIPS (RSA).

**Ativar WSDL** *ndash; Selecione esta opção para habilitar a geração de WSDL (Web Service Definition Language) para todos os serviços que fazem parte de formulários AEM.

Habilite essa opção em ambientes de desenvolvimento, onde os desenvolvedores usam a geração WSDL para criar seus aplicativos clientes. Você pode optar por desativar a geração WSDL em um ambiente de produção para evitar a exposição dos detalhes internos de um serviço.

**Habilitar armazenamento de documentos no banco de dados** *ndash; Selecione essa opção para armazenar documentos de longa vida no banco de dados de formulários AEM. A ativação dessa opção não elimina a necessidade de um diretório GDS. No entanto, escolher essa opção simplifica os backups de formulários AEM. Se você usar apenas o GDS, um backup envolve colocar o sistema AEM formsAEM Forms no modo de backup e, em seguida, concluir os backups do banco de dados e do GDS. Se você selecionar a opção de banco de dados, o backup envolve a conclusão do backup do banco de dados para uma nova instalação ou a conclusão do backup do banco de dados e o backup único do GDS para uma atualização. O gerenciamento adicional do banco de dados pode ser necessário para limpar trabalhos e dados em comparação a uma configuração somente GDS. (Consulte Opções de backup quando o banco de dados for usado para armazenamento de documentos.)

**Habilitar estatística de invocação de DSC** *ndash; Quando esta opção é selecionada, o AEM rastreia estatísticas de invocação, como o número de invocações, o tempo necessário para invocar e o número de erros em invocações. Essas informações são armazenadas em um bean JMX para que você possa usar o Java™ JConsole ou software de terceiros para consultar as estatísticas. Se você não quiser ver essas estatísticas, desmarque essa opção para melhorar o desempenho dos formulários AEM.

**Habilitar RDS** *ndash; Selecionar essa opção ativa o servlet dos Serviços de desenvolvimento remoto (RDS) nos formulários AEM. Quando essa opção está habilitada, as ferramentas do lado do cliente podem interagir com os Serviços de dados para fazer coisas como implantar ou desimplantar modelos para criar destinos e endpoints ou para descobrir quais modelos foram implantados em endpoints. Por padrão, essa opção não está selecionada.

**Permitir solicitação RDS não segura** *ndash; Quando essa opção é selecionada, as solicitações do RDS não precisam usar https. Por padrão, essa opção não está selecionada e todas as comunicações com os Serviços de dados precisam ser solicitações https.

**Permitir o upload de documentos não seguros por meio de aplicativos Flex** *ndash; O servlet de upload de arquivos usado para carregar documentos de aplicativos Adobe Flex® para formulários AEM requer que os usuários sejam autenticados e autorizados antes que possam carregar documentos. O usuário deve ter a função Usuário do aplicativo de carregamento de documentos atribuída ou outra função que inclua a permissão Upload de documentos. Isso ajuda a impedir que usuários não autorizados façam upload de documentos no servidor do AEM Forms. Selecione essa opção se quiser desativar esse recurso de segurança em um ambiente de desenvolvimento ou para compatibilidade com versões anteriores de formulários AEM. Por padrão, essa opção não está selecionada. Para obter detalhes, consulte &quot;Invocar formulários AEM usando o AEM forms Remoting&quot; em Programação com formulários AEM.

**Permitir o upload de documentos não seguros por meio de aplicativos Java SDK** *ndash; os uploads do DocumentManager HTTP devem ser protegidos. Por padrão, os uploads de HTTP exigem que os usuários sejam autenticados e autorizados antes que possam carregar documentos. O usuário deve ter a função Usuário de Serviços atribuída ou outra função que contenha a permissão Chamar Serviços. Isso ajuda a impedir que usuários não autorizados façam upload de documentos no servidor do Forms. Selecione essa opção se quiser desativar esse recurso de segurança em um ambiente de desenvolvimento, para compatibilidade com versões anteriores de formulários AEM ou com base na configuração do firewall. Por padrão, essa opção não está selecionada. Para obter detalhes, consulte &quot;Chamar formulários AEM usando a API Java&quot; em Programação com formulários AEM.
