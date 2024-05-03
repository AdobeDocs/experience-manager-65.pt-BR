---
title: Configuração das opções de cliente e servidor
description: Saiba como você pode configurar as várias opções de cliente e servidor, como as definições de configuração do servidor, as funções de segurança de documentos e a auditoria de eventos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: fe132f13-5f9a-4c86-a385-0a0026c812e2
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '10266'
ht-degree: 0%

---

# Configurar o servidor de segurança de documentos {#configure-the-document-security-server}

1. No console de administração, clique em Serviços > Segurança de documentos > Configuração > Configuração do servidor.
1. Defina as configurações e clique em OK.

## Definições de configuração do servidor {#server-configuration-settings}

**URL base:** O URL de segurança do documento base, contendo o nome e a porta do servidor. Informações anexadas à base criam URLs de conexão. Por exemplo, /edc/Main.do é anexado para acessar as páginas da Web. Os usuários também respondem a convites de registro de usuário externo por meio desse URL.

Se você estiver usando IPv6, insira o URL de base como o nome do computador ou o nome DNS. Se você usar um endereço IP numérico, o Acrobat não conseguirá abrir arquivos protegidos por política. Além disso, use o URL HTTP seguro (HTTPS) para seu servidor.

>[!NOTE]
>
>O URL base é incorporado em arquivos protegidos por política. Os aplicativos clientes usam o URL de base para se conectar de volta ao servidor. Os arquivos protegidos continuarão a conter o URL básico, mesmo que ele seja alterado posteriormente. Se você alterar o URL de base, as informações de configuração deverão ser atualizadas para todos os clientes que estão se conectando.

**Período de concessão offline padrão:** O período de tempo padrão em que um usuário pode usar um documento protegido off-line. Essa configuração determina o valor inicial da configuração Período de concessão offline automático ao criar uma política. (Consulte Criação e edição de políticas.) Quando o período de concessão expirar, o recipient deverá sincronizar o documento novamente para continuar a usá-lo.

Para obter uma discussão sobre como a concessão e a sincronização offline funcionam, consulte [Primer sobre configuração de concessão e sincronização offline](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html).

**Período de Sincronização Offline Padrão:** O tempo máximo durante o qual qualquer documento pode ser usado off-line quando estiver protegido inicialmente.

**Tempo limite da sessão do cliente:** O período de tempo, em minutos, após o qual a segurança de documentos é desconectada se um usuário que está conectado por meio de um aplicativo cliente não interagir com a segurança de documentos.

**Permitir acesso de usuários anônimos:** Selecione esta opção para habilitar a capacidade de criar políticas pessoais e compartilhadas que permitem que usuários anônimos abram documentos protegidos por política. (Os usuários que não têm contas podem acessar o documento, mas não podem fazer logon na segurança de documentos ou usar outros documentos protegidos por política.)

**Desabilitar acesso a clientes da versão 7:** Especifica se os usuários podem usar o Acrobat ou o Reader 7.0 para se conectar ao servidor. Quando essa opção é selecionada, os usuários devem usar o Acrobat ou Reader 8.0 e posterior para concluir operações de segurança de documentos em documentos PDF. Se as políticas exigirem que o Acrobat ou o Reader 8.0 e posterior seja executado no modo certificado ao abrir documentos protegidos por política, você deverá desativar o acesso ao Acrobat ou Reader 7. (Consulte Especificar as permissões de documento para usuários e grupos.)

**Permitir acesso offline por documento** Selecione esta opção para especificar o acesso off-line por documento. Se essa configuração estiver ativada, o usuário terá acesso offline somente aos documentos que tiver aberto online pelo menos uma vez.

**Permitir Autenticação de Senha de Nome de Usuário:** Selecione esta opção para permitir que os aplicativos clientes usem autenticação de nome de usuário/senha ao se conectarem ao servidor.

**Permitir autenticação Kerberos:** Selecione esta opção para permitir que os aplicativos clientes usem a autenticação Kerberos ao se conectarem ao servidor.

**Permitir Autenticação de Certificado de Cliente:** Selecione esta opção para permitir que os aplicativos clientes usem autenticação de certificado ao se conectarem ao servidor.

**Permitir autenticação estendida** Selecione para habilitar a autenticação estendida e, em seguida, insira o URL de aterrissagem da autenticação estendida.

A seleção dessa opção permite que os aplicativos clientes usem autenticação estendida. A autenticação estendida oferece processos de autenticação personalizados e diferentes opções de autenticação configuradas no servidor do AEM Forms. Por exemplo, agora os usuários podem experimentar a autenticação baseada em SAML em vez de nome de usuário/senha de formulários AEM do Acrobat e do Reader Client. Por padrão, o URL inicial contém *localhost* como o nome do servidor. Substitua o nome do servidor por um nome de host totalmente qualificado. O nome do host no URL de aterrissagem é preenchido automaticamente a partir do URL base, se a Autenticação estendida ainda não estiver ativada. Consulte [Adicionar o provedor de autenticação estendida](configuring-client-server-options.md#add-the-extended-authentication-provider).

***observação **: a autenticação estendida é compatível com o Apple Mac OS X com o Adobe Acrobat versão 11.0.6 e superior.*

**Largura preferencial do controle de HTML para autenticação estendida** Especifique a largura da caixa de diálogo de autenticação estendida que é aberta no Acrobat para inserir credenciais de usuário.

**Altura preferencial do controle de HTML para autenticação estendida** Especifique a altura da caixa de diálogo de autenticação estendida que é aberta no Acrobat para inserir credenciais de usuário.

***observação **: Os limites de largura e altura dessa caixa de diálogo são os seguintes:*
Largura: Mínimo = 400, máximo = 900

Altura: mínimo = 450; máximo = 800

**Habilitar Cache de Credenciais do Cliente:** Selecione esta opção para permitir que os usuários armazenem suas credenciais em cache (nome de usuário e senha). Quando as credenciais dos usuários são armazenadas em cache, eles não precisam inserir suas credenciais sempre que abrirem um documento ou quando clicarem no botão Atualizar na página Gerenciar políticas de segurança no Adobe Acrobat. Você pode especificar o número de dias antes que os usuários precisem fornecer suas credenciais novamente. Definir o número de dias como 0 permite que as credenciais sejam armazenadas em cache indefinidamente.

## Configurar usuários e administradores da segurança de documentos {#configuring-document-security-users-and-administrators}

### Atribuição de funções de segurança de documentos a administradores {#assigning-document-security-roles-to-administrators}

Seu ambiente do AEM Forms contém um ou mais usuários administradores que têm os privilégios apropriados para criar usuários e grupos. Se sua organização estiver usando a segurança de documentos, pelo menos um administrador também deverá receber o privilégio de gerenciar usuários convidados e locais.

Os administradores também devem ter a função Usuário do console de administração para acessar o console de administração. (Consulte [Criação e configuração de funções](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

### Configuração de usuários e grupos visíveis {#configuring-visible-users-and-groups}

Para exibir usuários e grupos em domínios selecionados durante pesquisas de usuário de política, um superadministrador ou administrador de conjunto de políticas deve selecionar e adicionar domínios (criados no Gerenciamento de usuários) à lista de usuários e grupos visíveis para cada conjunto de políticas.

A lista de usuários e grupos visíveis é visível para o coordenador de conjuntos de políticas e é usada para restringir quais domínios o usuário final pode navegar ao escolher usuários ou grupos para adicionar às políticas. Se essa tarefa não for executada, o coordenador de definições de políticas não localizará nenhum usuário ou grupo para adicionar à política. Pode haver mais de um coordenador de conjunto de políticas para qualquer conjunto de políticas fornecido.

1. Depois de instalar e configurar o ambiente de formulários AEM com segurança de documentos, configure todos os domínios apropriados no Gerenciamento de usuários. <!-- Fix broken link (See Setting up and managing domains) -->

   ***observação **: a criação de domínios deve ser realizada antes que qualquer política possa ser criada.*

1. No console de administração, clique em Serviços > Gerenciamento de documentos > Políticas e, em seguida, clique na guia Conjuntos de políticas.
1. Selecione Conjunto de Políticas Globais e clique na guia Usuários e Grupos Visíveis.
1. Clique em Adicionar domínio(s) e adicione os domínios existentes conforme necessário.
1. Navegue até Serviços > segurança de documentos > Configuração > Minhas políticas e clique na guia Usuários e grupos visíveis.
1. Clique em Adicionar domínio(s) e adicione os domínios existentes conforme necessário.

## Adicionar o provedor de autenticação estendida {#add-the-extended-authentication-provider}

Os formulários AEM fornecem uma amostra da configuração que você pode personalizar para o seu ambiente. Execute as seguintes etapas:

>[!NOTE]
>
>A autenticação estendida é compatível com o Apple Mac OS X com o Adobe Acrobat versão 11.0.6 e superior.

1. Obtenha o arquivo WAR de amostra para implantá-lo. Consulte o guia de instalação apropriado para o seu servidor de aplicativos.
1. Certifique-se de que o servidor do Forms tenha um nome totalmente qualificado em vez de endereços IP como o URL base e que seja um URL HTTPS. Consulte [Definições de configuração do servidor](configuring-client-server-options.md#server-configuration-settings).
1. Habilite a Autenticação Estendida na página Configuração do Servidor. Consulte [Definições de configuração do servidor](configuring-client-server-options.md#server-configuration-settings).
1. Adicione os URLs de redirecionamento de SSO necessários no arquivo de configuração do Gerenciamento de usuários. Consulte [Adicionar URLs de redirecionamento de SSO para autenticação estendida](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication).

### Adicionar URLs de redirecionamento de SSO para autenticação estendida {#add-sso-redirect-urls-for-extended-authentication}

Com a autenticação estendida ativada, os usuários que abrem um documento protegido por política no Acrobat XI ou Reader XI recebem uma caixa de diálogo para autenticação. Essa caixa de diálogo carrega a página de HTML especificada como o URL de aterrissagem da autenticação estendida nas configurações do servidor de segurança de documentos. Consulte [Definições de configuração do servidor](configuring-client-server-options.md#server-configuration-settings).

>[!NOTE]
>
>A autenticação estendida é compatível com o Apple Mac OS X com o Adobe Acrobat versão 11.0.6 e superior.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração.
1. Clique em Export e salve o arquivo de configuração no disco.
1. Abra o arquivo em um editor e localize o nó AllowedUrls.
1. No `AllowedUrls` adicione as seguintes linhas: `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. Salve o arquivo e importe-o da página Configuração Manual: no console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração.

## Configurando a segurança off-line {#configuring-offline-security}

a segurança de documentos oferece a capacidade de usar documentos protegidos por política off-line sem uma conexão com a Internet ou com a rede. Essa capacidade exige que a política permita o acesso off-line, conforme descrito em [Especificar as permissões de documento para usuários e grupos](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). Para que um documento com essa política possa ser usado off-line, o destinatário deve abrir o documento on-line e ativar o acesso off-line, clicando em Sim quando solicitado. O recipient também pode ser solicitado a autenticar sua identidade. O recipient pode então usar documentos offline durante o período de concessão offline especificado na política.

Quando o período de concessão offline terminar, o recipient deverá sincronizar novamente com a segurança de documentos abrindo um documento online ou usando um comando de menu de extensões do Acrobat ou do Acrobat Reader DC para sincronizar. (Consulte *Ajuda do Acrobat* ou o apropriado *Ajuda de extensões do Acrobat Reader DC*.)

Como os documentos que permitem acesso offline exigem o armazenamento em cache de material essencial no computador em que os arquivos são armazenados offline, o arquivo poderá ser comprometido se um usuário não autorizado puder obter o material principal. Para compensar essa possibilidade, são fornecidas opções de substituição de chaves programadas e manuais que você pode configurar para impedir que uma pessoa não autorizada use a chave para acessar o documento.

### Definir um período de concessão offline padrão {#set-a-default-offline-lease-period}

Os recipients de documentos protegidos por política podem colocar os documentos offline pelo número de dias especificado na política. Depois de sincronizar inicialmente o documento com a segurança de documentos, o recipient pode usá-lo offline até que o período de concessão offline expire. Quando o período de concessão expirar, o destinatário deverá colocar o documento online e fazer logon para sincronizar com a segurança de documentos para continuar usando o documento.

Você pode configurar um período de concessão offline padrão. O período de concessão pode ser alterado do padrão quando qualquer pessoa cria ou edita uma política.

1. Na página de segurança de documentos, clique em Configuração > Configuração do servidor.
1. Na caixa Período de concessão offline padrão, digite o número de dias para o período de concessão offline.
1. Clique em OK.

### Gerenciar sobreposições de chaves {#manage-key-rollovers}

A segurança de documentos usa algoritmos de criptografia e licenças para proteger documentos. Ao criptografar um documento, a segurança de documentos gera e gerencia uma chave de descriptografia chamada *ChaveDoc* que ele passa para o aplicativo cliente. Se a política que protege um documento permitir acesso offline, uma chave offline chamada *chave principal* também é gerado para cada usuário que tem acesso offline ao documento.

>[!NOTE]
>
>Se uma chave principal não existir, a segurança de documentos gerará uma para proteger um documento.

Para abrir um documento protegido por política offline, o computador do usuário deve ter a chave principal apropriada. O computador obtém a chave principal quando o usuário sincroniza com a segurança de documentos (abre um documento protegido online). Se essa chave principal for comprometida, qualquer documento ao qual o usuário tenha acesso offline também poderá ser comprometido.

Uma maneira de diminuir a ameaça aos documentos off-line é evitar permitir o acesso off-line a documentos particularmente confidenciais. Outro método é rolar periodicamente sobre as chaves principais. Quando a segurança de documentos transferir a chave, as chaves existentes não poderão mais acessar os documentos protegidos por política. Por exemplo, se um autor obtiver uma chave principal de um notebook roubado, essa chave não poderá ser usada para acessar os documentos protegidos após a substituição. Se você suspeitar que uma chave principal específica tenha sido comprometida, poderá passar manualmente sobre a chave.

No entanto, uma substituição de chaves afeta todas as chaves principais, não apenas uma. Também reduz a escalabilidade do sistema, pois os clientes devem armazenar mais chaves para acesso off-line. A frequência padrão de substituição de chave é de 20 dias. É recomendável não definir esse valor para menos de 14 dias, pois as pessoas podem ser impedidas de visualizar documentos offline e o desempenho do sistema pode ser afetado.

No exemplo a seguir, Key1 é a mais antiga das duas chaves principais, e Key2 é a mais recente. Quando você clica no botão Sobrepor chaves agora na primeira vez, Key1 se torna inválida e uma chave principal válida mais recente (Key3) é gerada. Os usuários obterão a chave 3 ao sincronizarem com a segurança de documentos, normalmente abrindo um documento protegido online. No entanto, os usuários não são forçados a sincronizar com a segurança de documentos até que atinjam o período máximo de concessão offline especificado em uma política. Após a primeira substituição de chave, os usuários que permanecerem offline ainda poderão abrir documentos offline, incluindo aqueles protegidos pela Chave 3, até atingirem o período máximo de concessão offline. Quando você clica no botão Teclas de sobreposição agora uma segunda vez, a tecla 2 se torna inválida e a tecla 4 é criada. Os usuários que permanecem offline durante as duas sobreposições de chave não podem abrir documentos protegidos com Key3 ou Key4 até que eles sincronizem com a segurança do documento.

**Alterar a frequência de sobreposição de chave**

Para fins de confidencialidade, ao usar documentos offline, a segurança de documentos fornece uma opção de substituição automática de chaves com um período de frequência padrão de 20 dias. Você pode alterar a frequência de sobreposição; no entanto, evite definir o valor com menos de 14 dias, pois as pessoas podem ser impedidas de visualizar documentos offline e o desempenho do sistema pode ser afetado.

1. Na página de segurança de documentos, clique em Configuração > Gerenciamento de chaves.
1. Na caixa Frequência de Rolagem de Chave, digite o número de dias para o período de rolagem.
1. Clique em OK.

**Sobrepor manualmente as chaves principais**

Para manter a confidencialidade de documentos offline, você pode passar manualmente sobre as chaves principais. Você pode achar necessário rolar manualmente uma chave (por exemplo, se a chave for comprometida por alguém que a obtenha de um computador onde ela esteja armazenada em cache para ativar o acesso offline a um documento).

>[!NOTE]
>
>Evite usar a sobreposição manual com frequência, pois ela faz com que todas as chaves principais sejam sobrepostas, não apenas uma, e pode impedir temporariamente que os usuários exibam novos documentos offline.

As chaves principais devem ser sobrepostas duas vezes antes que chaves existentes anteriormente em computadores cliente sejam invalidadas. Os computadores cliente que têm chaves principais invalidadas devem sincronizar novamente com o serviço de segurança de documentos para adquirir as novas chaves principais.

1. Na página de segurança de documentos, clique em Configuração > Gerenciamento de chaves.
1. Clique em Teclas de sobreposição agora e em OK.
1. Espere aproximadamente 10 minutos. A seguinte mensagem de registro é exibida no registro do servidor: `Done RightsManagement key rollover for`*N* `principals`. Onde *N* é o número de usuários no sistema de segurança de documentos.
1. Clique em Teclas de sobreposição agora e em OK.
1. Espere aproximadamente 10 minutos.

## Definição de configurações de privacidade e auditoria de eventos {#configuring-event-auditing-and-privacy-settings}

A segurança de documentos pode auditar e registrar informações sobre eventos relacionados à interação com documentos protegidos por política, políticas, administradores e o servidor. Você pode configurar a auditoria de eventos e especificar os tipos de eventos que serão auditados. Para auditar eventos de um documento específico, a opção de auditoria na política também deve estar ativada.

Quando a auditoria estiver ativada, você poderá exibir detalhes dos eventos auditados na página Eventos. os usuários da segurança de documentos também podem exibir eventos relacionados especificamente aos documentos protegidos por política que usam ou criam.

Você pode selecionar os seguintes tipos de eventos para auditoria:

* Eventos de documentos protegidos por política, como tentativas de usuários autorizados ou não autorizados de abrir documentos
* Eventos de política, como criar, alterar, excluir, ativar e desativar políticas
* Eventos de usuário, como convites e registros de usuários externos, contas de usuário ativadas e desativadas, alterações em senhas de usuário e atualizações de perfil
* Eventos de formulários AEM, como incompatibilidade de versões, provedores de autorização e servidores de diretórios indisponíveis e alterações na configuração do servidor

### Ativar ou desativar a auditoria de eventos {#enable-or-disable-event-auditing}

Você pode ativar e desativar a auditoria de eventos relacionados ao servidor, documentos protegidos por política, políticas, conjuntos de políticas e usuários. Quando você habilita a auditoria de eventos, pode optar por auditar todos os eventos possíveis ou selecionar eventos específicos para auditar.

Ao habilitar a auditoria do servidor, você pode exibir os eventos auditados na página Eventos.

1. No console de administração, clique em Serviços > Segurança de documentos > Configuração > Configurações de auditoria e privacidade.
1. Para configurar a auditoria do servidor, em Habilitar Auditoria do Servidor, selecione Sim ou Não.
1. Se você selecionou Sim, em cada categoria de evento, execute uma das seguintes ações para selecionar as opções a serem auditadas:

   * Para auditar todos os eventos na categoria, selecione Todos.
   * Para auditar apenas alguns eventos, desmarque Tudo e marque as caixas de seleção ao lado dos eventos que deseja auditar.

     (Consulte [Opções de auditoria de evento](configuring-client-server-options.md#event-auditing-options).)

1. Clique em OK.

>[!NOTE]
>
>Ao trabalhar com as páginas da Web, evite usar os botões do navegador, como o botão Voltar, o botão Atualizar e a seta para trás ou para a frente, pois essa ação pode causar problemas de captura de dados indesejados e exibição de dados.

### Ativar ou desativar a notificação de privacidade {#enable-or-disable-privacy-notification}

Você pode ativar e desativar uma mensagem de notificação de privacidade. Ao ativar a notificação de privacidade, uma mensagem é exibida quando um recipient tenta abrir um documento protegido por política. O aviso informa ao usuário que o uso do documento está sendo auditado. Você também pode especificar um URL que o usuário pode usar para exibir a página da sua política de privacidade, se disponível.

1. No console de administração, clique em Serviços > Segurança de documentos > Configuração > Configurações de auditoria e privacidade.
1. Para configurar a notificação de privacidade, em Ativar aviso de privacidade, selecione Sim ou Não.

   Se a política anexada a um documento permitir acesso anônimo ao usuário e Ativar aviso de privacidade estiver definida como Não, o usuário não será solicitado a fazer logon e a mensagem de notificação de privacidade não será exibida.

   Se a política anexada a um documento não permitir acesso anônimo ao usuário, ele verá a mensagem de notificação de privacidade.

1. Se aplicável, na caixa URL de privacidade, digite o URL da página da política de privacidade. Se a caixa URL de privacidade for deixada em branco, a página de privacidade de adobe.com será exibida.
1. Clique em OK.

>[!NOTE]
>
>Desabilitar o aviso de privacidade não desabilita a auditoria de uso do documento. As ações de auditoria prontas e as ações personalizadas compatíveis com o rastreamento de uso estendido ainda podem coletar informações sobre o comportamento do usuário.

### Importar um tipo de evento de auditoria personalizado {#import-a-custom-audit-event-type}

Se você estiver usando um aplicativo habilitado para segurança de documentos que ofereça suporte à auditoria de eventos adicionais, como eventos específicos a um determinado tipo de arquivo, um parceiro de Adobe poderá fornecer eventos de auditoria personalizados que você pode importar para a segurança de documentos. Use esse recurso somente se você tiver recebido tipos de evento personalizados por um parceiro de Adobe.

1. No console de administração, clique em Serviços > Segurança de documentos > Configuração > Gerenciamento de eventos.
1. Clique em Procurar para acessar o arquivo XML a ser importado e clique em Importar.
1. A importação substitui tipos de evento de auditoria personalizados existentes no servidor se combinações idênticas de código de evento e namespace forem encontradas.
1. Clique em OK.

### Excluir um tipo de evento de auditoria personalizado {#delete-a-custom-audit-event-type}

1. No console de administração, clique em Serviços > segurança de documentos > Configuração > Gerenciamento de eventos.
1. Marque a caixa de seleção ao lado do tipo de evento de auditoria personalizado a ser excluído e clique em Excluir.
1. Clique em OK.

### Exportar eventos de auditoria {#export-audit-events}

Você pode exportar eventos de auditoria para um arquivo para fins de arquivamento.

1. No console de administração, clique em Serviços > Segurança de documentos > Configuração > Gerenciamento de eventos.
1. Edite as configurações em Exportar eventos de auditoria, conforme necessário. Você pode especificar:

   * a idade mínima dos eventos de auditoria a serem exportados
   * o número máximo de eventos de auditoria a serem incluídos em um único arquivo. O servidor gera um ou mais arquivos com base nesse valor.
   * a pasta onde o arquivo será criado. Esta pasta está no servidor do Forms. Se o caminho da pasta for relativo, ele será relativo ao diretório raiz do servidor de aplicativos.
   * o prefixo de arquivo a ser usado para os arquivos de eventos de auditoria
   * o formato do arquivo, um arquivo CSV (valores separados por vírgula) compatível com o Microsoft Excel ou um arquivo XML.

1. Clique em Exportar. Para cancelar a exportação, clique em Cancelar exportação. Se outro usuário tiver programado uma exportação, o botão Cancelar exportação não estará disponível até que a exportação seja concluída. O botão Cancelar exportação não estará disponível se outro usuário tiver programado uma exportação. Para verificar se uma Exportação ou Exclusão programada foi iniciada ou concluída, clique em Atualizar.

### Excluir eventos de auditoria {#delete-audit-events}

Você pode excluir eventos de auditoria com mais de um número especificado de dias.

1. No console de administração, clique em Serviços > Segurança de documentos > Configuração > Gerenciamento de eventos.
1. Em Excluir eventos de auditoria, especifique o número de dias na caixa Excluir eventos de auditoria mais antigos que.
1. Clique em Excluir. Clique em Exportar. Para cancelar a exclusão, clique em Cancelar exclusão. Se outro usuário tiver programado uma exclusão, o botão Cancelar exclusão não estará disponível até que a exportação seja concluída. O botão Cancelar exclusão não estará disponível se outro usuário tiver agendado uma exportação. Para verificar se uma Exclusão programada foi iniciada ou concluída, clique em Atualizar.

### Opções de auditoria de evento {#event-auditing-options}

Você pode ativar e desativar a auditoria de eventos e especificar os tipos de eventos a serem auditados.

**Eventos de documento**

**Visualizar Documento:** Um recipient exibe um documento protegido por política.

**Fechar documento:** Um recipient fecha um documento protegido por política.

**Imprimir Baixa resolução** Um destinatário imprime um documento protegido por política com a opção de baixa resolução especificada.

**Imprimir Alta resolução:** Um destinatário imprime um documento protegido por política com a opção de alta resolução especificada.

**Adicionar anotação ao documento:** Um recipient adiciona uma anotação a um documento PDF.

**Revogar documento:** Um usuário ou administrador revoga o acesso a um documento protegido por política.

**Cancelar revogação do documento:** Um usuário ou administrador restaura o acesso a um documento protegido por política.

**Preenchimento de formulário:** Um recipient insere informações em um documento PDF que é um formulário preenchível.

**Política removida:** Um editor remove uma política de um documento para retirar as proteções de segurança.

**Alterar URL de Revogação de Documentos:** Uma chamada do nível da API altera o URL de revogação especificado para acessar um novo documento que substitui um documento revogado.

**Modificar documento:** Um recipient altera o conteúdo de um documento protegido por política.

**Assinar documento:** Um destinatário assina um documento.

**Proteger um novo documento:** Um usuário aplica uma política para proteger um documento.

**Alternar Política no Documento:** Um usuário ou administrador alterna a política anexada a um documento.

**Publicar documento como:** Um novo documento cujo documentName e a licença são idênticos a um documento existente é registrado no servidor e os documentos não têm um relacionamento pai-filho. Esse evento pode ser acionado usando o SDK de formulários do AEM.

**Iterar documento:** Um novo documento cujo documentName e a licença são idênticos a um documento existente é registrado no servidor e os documentos têm um relacionamento pai-filho. Esse evento pode ser acionado usando o SDK de formulários do AEM.

**Eventos de política**

**Política criada:** Um usuário ou administrador cria uma política.

**Política Habilitada:** Um administrador disponibiliza uma política.

**Política Alterada:** Um usuário ou administrador altera uma política.

**Política Desabilitada:** Um administrador torna uma política indisponível.

**Política excluída:** Um usuário ou administrador exclui uma política.

**Alterar Proprietário da Política:** Uma chamada do nível da API altera o proprietário da política.

**Eventos de usuário**

**Usuário excluído:** Um administrador exclui uma conta de usuário.

**Registrar usuário convidado:** Um usuário externo se registra com a segurança do documento.

**Logon bem-sucedido:** Tentativas de logon bem-sucedidas por administradores ou usuários.

**Usuários convidados:** A segurança de documentos convida um usuário a se registrar.

**Usuários Ativados:** Os usuários externos ativam suas contas usando o URL no email de ativação, ou um administrador ativa uma conta.

**Alterar senha:** Usuários convidados alteram suas senhas ou um administrador redefine uma senha para um usuário local.

**Falha no login:** Tentativas de login falhas por administradores ou usuários.

**Usuários desativados:** Um administrador desativa uma conta de usuário local.

**Atualização do perfil:** Os usuários convidados alteram seu nome, nome da organização e senha.

**Conta bloqueada:** Um administrador bloqueia uma conta.

**Eventos de definição de políticas**

**Conjunto de Políticas Criado:** Um administrador ou coordenador de conjunto de políticas cria um conjunto de políticas.

**Conjunto de políticas excluído:** Um administrador ou coordenador de conjunto de políticas exclui um conjunto de políticas.

**Conjunto de Políticas Modificado:** Um administrador ou coordenador de conjunto de políticas altera um conjunto de políticas.

**Eventos do sistema**

**Sincronização de Diretórios Concluída:** Essas informações não estão disponíveis na página Eventos. As informações de sincronização de diretórios atuais, incluindo o estado e o horário da última sincronização, são exibidas na página Gerenciamento de Domínio. Para acessar a página Gerenciamento de domínio no console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.

**Habilitar Acesso Offline de Cliente:** Um usuário habilitou o acesso off-line a documentos protegidos contra o servidor no computador do usuário.

**Cliente Sincronizado** O aplicativo cliente deve sincronizar informações com o servidor para permitir acesso offline.

**Incompatibilidade de versão:** Uma versão do SDK do AEM Forms incompatível com o servidor tentou se conectar ao servidor.

**Informações de Sincronização de Diretórios:** Essas informações não estão disponíveis na página Eventos. As informações de sincronização de diretórios atuais, incluindo o estado e o horário da última sincronização, são exibidas na página Gerenciamento de Domínio. Para acessar a página Gerenciamento de domínio no console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.

**Alteração de configuração do servidor:** Alterações na configuração do servidor que são feitas por meio das páginas da Web ou manualmente importando um arquivo config.xml. Isso inclui alterações no URL básico, tempo limite da sessão, bloqueios de logon, configurações de diretório, substituições de chaves, configurações do servidor SMTP para registro externo, configuração de marca d&#39;água, opções de exibição e assim por diante.

## Configuração do rastreamento de uso estendido {#configuring-extended-usage-tracking}

A segurança de documentos pode rastrear vários eventos personalizados que podem ser executados em um documento protegido. Você pode ativar o rastreamento de eventos do servidor de segurança de documentos no nível global ou no nível de políticas. Em seguida, você pode configurar um JavaScript para capturar ações específicas executadas no documento de PDF protegido, como clicar em um botão ou salvar o documento. Esses dados de uso são enviados como um arquivo XML em pares de valores chave, que podem ser usados para análise adicional. Os usuários finais que acessam os documentos protegidos podem permitir ou recusar esse rastreamento no aplicativo cliente.

Se o rastreamento estiver ativado no nível global, você poderá substituir essa configuração no nível da política e desativá-la para uma política específica. A substituição no nível da política não é possível se o rastreamento estiver desativado no nível global. A lista de eventos rastreados é enviada automaticamente para o servidor quando a contagem de eventos atinge 25 ou quando o documento é fechado. Você também pode configurar o script para enviar explicitamente a lista de eventos de acordo com seus requisitos. Você pode personalizar o rastreamento de eventos acessando as propriedades e os métodos do objeto de segurança de documentos.

Após habilitar o rastreamento, o rastreamento será ativado por padrão em todas as políticas criadas posteriormente. As políticas criadas antes da ativação do rastreamento no servidor precisarão de atualizações manuais.

### Habilitar ou desabilitar o rastreamento de uso estendido {#enable-or-disable-extended-usage-tracking}

Antes de começar, verifique se a Auditoria do Servidor está ativada. Consulte [Definição de configurações de privacidade e auditoria de eventos](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) para obter mais informações sobre auditoria.

1. No console de administração, clique em Serviços > Segurança de documentos > Configuração > Configurações de auditoria e privacidade.
1. Para configurar o rastreamento de uso estendido, em Ativar rastreamento, selecione Sim ou Não.
1. Para definir a seleção da caixa de seleção Permitir coleta de dados de uso detalhados na página de logon, em Ativar rastreamento padrão, selecione Sim ou Não.

Para exibir os eventos rastreados, é possível usar o filtro Eventos de documento na página Eventos. Os eventos rastreados com JavaScript são rotulados como Rastreamento de uso detalhado. Consulte [Monitoramento de eventos](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) para obter mais informações sobre eventos.

## Definir configurações de exibição de segurança de documentos {#configure-document-security-display-settings}

1. No console de administração, clique em Serviços > segurança de documentos > Configuração > Opções de exibição.
1. Defina as configurações e clique em OK.

### Configurações de exibição {#display-settings}

**Linhas a serem exibidas para os resultados da pesquisa:** Número de linhas que aparecem em uma página quando as pesquisas são realizadas.

**Personalização da caixa de diálogo de logon do cliente**

Essas configurações controlam o texto exibido no prompt de logon que é exibido quando um usuário faz logon na segurança de documentos por meio de um aplicativo cliente.

**Texto de boas-vindas:** O texto da mensagem de boas-vindas, como &quot;Faça logon com seu nome de usuário e senha&quot;. O texto da mensagem de boas-vindas deve conter informações sobre como fazer logon na segurança de documentos e como entrar em contato com um administrador ou outra pessoa de suporte designada em sua organização para obter assistência. Por exemplo, os usuários externos podem precisar entrar em contato com um administrador se esquecerem as senhas ou precisarem de assistência no processo de registro ou logon. O comprimento máximo do texto de boas-vindas é de 512 caracteres.

**Texto do nome de usuário:** O rótulo de texto da caixa de nome de usuário.

**Texto da senha:** O rótulo de texto para a caixa de senha.

**Personalização da caixa de diálogo de autenticação de certificado do cliente**

Essas configurações controlam o texto exibido na caixa de diálogo de autenticação de certificado.

**Escolher Tipo de Autenticação Texto:** O texto exibido para direcionar um usuário para selecionar um tipo de autenticação.

**Escolher texto do certificado:** O texto exibido para direcionar um usuário para selecionar um tipo de certificado.

**Texto de erro de certificados não disponíveis:** Mensagem de até 512 caracteres a ser exibida quando o certificado selecionado não estiver disponível.

**Personalização para exibição de certificado de cliente**

**Exibir Somente Emissores de Credenciais Confiáveis:** Quando essa opção é selecionada, o aplicativo cliente apresenta ao usuário somente certificados de emissores de credencial nos quais os formulários AEM estão configurados para confiança (consulte Gerenciamento de certificados e credenciais.) Quando essa opção não está selecionada, o usuário recebe uma lista de todos os certificados no sistema do usuário.

## Configurar marcas d&#39;água dinâmicas {#configure-dynamic-watermarks}

Usando a segurança de documentos, é possível definir configurações padrão para a opção de marca d&#39;água dinâmica que pode ser aplicada ao criar políticas. A *marca d&#39;água* é uma imagem sobreposta ao texto no documento. É útil para rastrear o conteúdo de um documento e pode ajudar a identificar o uso ilegal do conteúdo.

Uma marca d&#39;água dinâmica pode consistir em um texto composto de variáveis definidas, como ID de usuário e data e texto personalizado, ou conteúdo avançado em um PDF. É possível configurar marcas d&#39;água com vários elementos, cada um com seu próprio posicionamento e formatação.

As marcas d&#39;água não são editáveis e, portanto, são um método mais seguro para garantir a confidencialidade do conteúdo do documento. As marcas d&#39;água dinâmicas também garantem que uma marca d&#39;água mostre informações específicas do usuário suficientes para atuar como um impedimento para distribuir ainda mais o documento.

A marca d&#39;água especificada por uma política aparece no documento protegido por política quando um destinatário exibe ou imprime o documento. Diferentemente das marcas d&#39;água permanentes, uma marca d&#39;água dinâmica nunca é salva no documento, o que fornece a flexibilidade necessária ao implantar um documento em um ambiente de intranet para garantir que o aplicativo de exibição exiba a identidade do usuário específico. Além disso, se um documento tiver vários usuários, o uso da marca d&#39;água dinâmica significa que você pode usar um documento em vez de várias versões, cada uma com uma marca d&#39;água diferente. A marca d&#39;água exibida reflete a identidade do usuário atual.

Observe que as marcas d&#39;água dinâmicas são diferentes das marcas d&#39;água que os usuários podem adicionar diretamente ao documento no Acrobat. O resultado é que você pode ter duas marcas d&#39;água em um documento protegido por política.

### Considerações ao criar marcas d&#39;água {#considerations-when-creating-watermarks}

Você pode criar marcas d&#39;água dinâmicas com vários elementos de marca d&#39;água com cada elemento especificado como texto ou PDF. É possível incluir até cinco elementos, em uma marca d&#39;água.

Se você escolher uma marca d&#39;água baseada em texto, poderá especificar vários elementos dentro da marca d&#39;água com várias entradas de texto e especificar o posicionamento de cada elemento. Atribua nomes significativos a esses elementos, como cabeçalho, rodapé e assim por diante.

Por exemplo, se você quiser especificar texto diferente no cabeçalho, rodapé, nas margens e no documento como uma marca d&#39;água, crie vários elementos de marca d&#39;água e especifique suas posições. Se desejar que a ID de usuário e a data atual de acesso ao documento sejam exibidas no cabeçalho, o nome da política na margem direita e um texto personalizado &quot;CONFIDENCIAL&quot; seja exibido diagonalmente no documento, defina elementos de marca d&#39;água separados com texto como o tipo e especifique sua formatação e posicionamento. Quando a marca d&#39;água é aplicada a um documento, todos os elementos na marca d&#39;água são aplicados ao documento ao mesmo tempo, na ordem em que são adicionados à marca d&#39;água.

Normalmente, você usa marcas d&#39;água baseadas em PDF para incluir conteúdo gráfico, como logotipos ou símbolos especiais, como direitos autorais ou marca registrada.

Você pode alterar os limites do número de elementos de marca d&#39;água e o tamanho do arquivo de PDF modificando o arquivo de configuração de segurança de documentos. Consulte [Alterar os parâmetros de configuração da marca d&#39;água](configuring-client-server-options.md#change-the-watermark-configuration-parameters).

Lembre-se do seguinte ao configurar marcas d&#39;água:

* Não é possível usar um documento de PDF protegido por senha como o elemento de marca d&#39;água. No entanto, se a marca d&#39;água que você criar contiver outros elementos que não estejam protegidos por senha, eles serão aplicados como parte da marca d&#39;água.
* Você pode alterar o tamanho máximo do arquivo de PDF que deseja usar como elemento de marca d&#39;água. No entanto, documentos de PDF grandes usados como marcas d&#39;água degradam o desempenho durante a sincronização offline de documentos aplicados com essas marcas d&#39;água. Consulte [Alterar os parâmetros de configuração da marca d&#39;água](configuring-client-server-options.md#change-the-watermark-configuration-parameters).
* Somente a primeira página do PDF selecionado é usada como marca d&#39;água. Verifique se as informações que você deseja exibir como marca d&#39;água estão disponíveis na própria primeira página.
* Mesmo que você possa especificar o dimensionamento do documento PDF, considere o tamanho e o layout da página do PDF se planeja usá-lo como marca d&#39;água no cabeçalho, rodapé ou margens.
* Ao especificar o nome da fonte, digite o nome corretamente. Os formulários AEM substituirão a fonte especificada se ela não estiver presente na máquina cliente onde o documento está aberto.
* Se você selecionou texto como o conteúdo da marca d&#39;água, especificar a opção de dimensionamento como Ajustar à página não funcionará para páginas com largura diferente.
* Ao especificar o posicionamento dos elementos de marca d&#39;água, certifique-se de que não mais de um elemento tenha o mesmo posicionamento. Se dois elementos de marca d&#39;água tiverem o mesmo posicionamento, como centralizado, aparecerão sobrepostos no documento e na ordem em que foram adicionados à marca d&#39;água.
* Ao especificar o tamanho e o tipo da fonte, verifique se o comprimento do texto está completamente visível na página. O conteúdo do texto é sobreposto em novas linhas, de modo que o conteúdo da marca d&#39;água que você pretende que esteja presente nas margens pode se sobrepor nas áreas de conteúdo das páginas. No entanto, se o documento for aberto no Acrobat 9, o texto além da única linha será truncado.

### Limitações das marcas d&#39;água dinâmicas {#limitations-of-dynamic-watermarks}

Alguns aplicativos clientes podem não suportar marcas d&#39;água dinâmicas. Consulte a Ajuda das extensões apropriadas do Acrobat Reader DC. Além disso, lembre-se do seguinte sobre as versões do Acrobat compatíveis com marcas d&#39;água dinâmicas:

* Não é possível usar um documento de PDF protegido por senha como o elemento de marca d&#39;água.
* As versões do Acrobat e do Adobe Reader anteriores à 10 não são compatíveis com os seguintes recursos de marca d&#39;água:

   * Marcas d&#39;água do PDF
   * Vários elementos na marca d&#39;água (Texto/PDF)
   * Opções avançadas, como intervalo de páginas, ou opções de exibição
   * Opções de formatação de texto, como fonte, nome de fonte e cor especificados. No entanto, as versões anteriores do Acrobat e do Reader exibirão o conteúdo do texto na fonte e cor padrão.

* Acrobat 9.0 e versões anteriores: o Acrobat 9.0 e versões anteriores não oferecem suporte a nomes de políticas em marcas d&#39;água dinâmicas. Se o Acrobat 9.0 abrir um documento protegido por política com uma marca d&#39;água dinâmica que inclui um nome de política e outros dados dinâmicos, a marca d&#39;água será exibida sem o nome da política. Se a marca d&#39;água dinâmica incluir apenas o nome da política, o Acrobat exibirá uma mensagem de erro

### Adicionar um modelo de marca d&#39;água dinâmica {#add-a-dynamic-watermark-template}

É possível criar modelos de marca d&#39;água dinâmicos. Esses modelos permanecem disponíveis como uma opção de configuração para políticas criadas por administradores ou usuários.

>[!NOTE]
>
>As informações de configuração de marca d&#39;água dinâmica não são capturadas com outras informações de configuração quando você exporta um arquivo de configuração.

1. No console de administração, clique em Serviços > Segurança de documentos > Configuração > Marcas d&#39;água.
1. Clique em Novo.
1. Na caixa Nome, digite um nome para a nova marca d&#39;água.

   ***observação **: Não é possível usar alguns caracteres especiais nos nomes ou descrições de marcas d&#39;água ou elementos de marca d&#39;água. Consulte as restrições listadas em [Considerações para a edição de políticas](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies).*

1. Em Nome, ao lado do sinal de mais, insira um nome significativo para o elemento de marca d&#39;água, como Cabeçalho, adicione uma descrição e expanda o sinal de mais para exibir as opções.
1. Em Origem, selecione o tipo de marca d&#39;água como Texto ou PDF.
1. Se você selecionou Texto, faça o seguinte:

   * Selecione os tipos de marca d&#39;água a serem incluídos. Se você selecionar Texto personalizado, na caixa adjacente, digite o texto a ser exibido para a marca d&#39;água. Lembre-se do comprimento do texto que será exibido como marca d&#39;água.
   * Especifique as propriedades de formatação do texto, como nome da fonte, tamanho da fonte, cor do primeiro plano e cor do plano de fundo, para o conteúdo do texto da marca d&#39;água. Especifique a cor do primeiro plano e do plano de fundo como valores hexadecimais.

     ***observação **: se você selecionar a opção de dimensionamento como Ajustar à página, a propriedade de tamanho da fonte não estará disponível para edição.*

1. Se você selecionou PDF para opções de marca d&#39;água avançada, clique em **Procurar** ao lado de Selecionar PDF de marca d&#39;água para selecionar o documento PDF que deseja usar como marca d&#39;água.

   ***observação **: Não use um documento de PDF protegido por senha. Se você especificar um PDF protegido por senha como o elemento de marca d&#39;água, a marca d&#39;água não será aplicada.*

1. Em Usar como Plano de Fundo, selecione Sim ou Não.

   **observação**: atualmente, a marca d&#39;água aparece em primeiro plano independentemente dessa configuração.

1. Para controlar onde a marca d&#39;água é exibida no documento, configure as opções Alinhamento Vertical e Alinhamento Horizontal.
1. Selecione Ajustar à página ou % e digite uma porcentagem na caixa. O valor deve ser um número inteiro, não uma fração. Para configurar o tamanho da marca d&#39;água, você pode usar um valor que seja a porcentagem da página ou definir a marca d&#39;água para se ajustar ao tamanho da página.
1. Na caixa Rotação, digite os graus pelos quais girar a marca d&#39;água. O intervalo é de -180 a 180. Use um valor negativo para girar a marca d&#39;água no sentido anti-horário. O valor deve ser um número inteiro, não uma fração.
1. Na caixa Opacidade, digite uma porcentagem. Use um número inteiro, não uma fração.
1. Em Opções avançadas, defina o seguinte:

   **Opções de intervalo de páginas**

   Defina o intervalo de páginas no qual a marca d&#39;água deve ser exibida. Insira a página inicial como 1 e a página final como -1 para ter todas as páginas marcadas com a marca d&#39;água.

   **Opções de Exibição**

   Selecione onde deseja que a marca d&#39;água apareça. Por padrão, a marca d&#39;água aparece tanto na cópia eletrônica (online) quanto na cópia impressa (impressa).

1. Clique em **Novo** em Elementos de marca d&#39;água para adicionar mais elementos de marca d&#39;água, se necessário.
1. Clique em OK.

### Editar um modelo de marca d&#39;água dinâmica {#edit-a-dynamic-watermark-template}

1. No console de administração, clique em Serviços > segurança de documentos > Configuração > Marcas d&#39;água.
1. Clique na marca d&#39;água apropriada na lista.
1. Na página Editar marcas d&#39;água, altere as configurações conforme necessário.
1. Clique em OK.

### Excluir um modelo de marca d&#39;água dinâmica {#delete-a-dynamic-watermark-template}

Quando você exclui uma marca d&#39;água dinâmica, ela não está mais disponível para ser adicionada a uma nova política. No entanto, a marca d&#39;água permanece nas políticas existentes que a utilizam no momento, e os documentos protegidos no momento continuam a mostrar a marca d&#39;água dinâmica até que você ou um usuário edite a política que contém a marca d&#39;água excluída. Depois que a política é editada, a marca d&#39;água não é mais aplicada. Uma mensagem é exibida, indicando que a marca d&#39;água existente foi excluída da política e que o usuário pode selecionar outra para substituí-la.

1. No console de administração, clique em Serviços > Segurança de documentos > Configuração > Marcas d&#39;água.
1. Marque a caixa de seleção ao lado da marca d&#39;água apropriada e clique em Excluir.
1. Clique em OK.

## Configurando o registro de usuário convidado {#configuring-invited-user-registration}

Os usuários externos à sua organização podem se registrar na segurança de documentos. Os usuários convidados que se registram e ativam suas contas podem fazer logon na segurança de documentos usando seu endereço de email e a senha que eles criam ao se registrarem. Os usuários convidados registrados podem usar documentos protegidos por política para os quais têm permissões.

Quando os usuários convidados são ativados, eles se tornam usuários locais. Os usuários locais podem ser configurados e gerenciados usando a área Usuários Locais e Convidados. (Consulte [Gerenciar contas de usuário convidadas e locais](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts).)

Dependendo dos recursos ativados para usuários convidados, eles também podem usar estes recursos de segurança de documentos:

* Aplicação de políticas a documentos
* Criar políticas
* Adicionar usuários convidados às políticas

A Segurança de documentos gera automaticamente um email de convite de registro quando os seguintes eventos ocorrem, a menos que o usuário já esteja no diretório LDAP de origem ou tenha sido convidado anteriormente para se registrar:

* Um usuário existente adiciona um usuário convidado a uma política
* Um administrador adiciona uma conta de usuário convidado na página Registro de usuário convidado

O e-mail de registro contém um link para uma página de Registro e informações sobre como se registrar. Depois que o usuário convidado é registrado, a segurança de documentos emite um email de ativação com um link para uma página de Ativação. Quando ativada, a conta permanece válida até que você a desative ou exclua.

Se você habilitar o registro integrado, especifique o servidor SMTP, os detalhes do email de registro, os recursos de acesso e redefina as informações de email da senha apenas uma vez. Antes de habilitar o registro incorporado, verifique se você criou um domínio local no Gerenciamento de usuários e se atribuiu a função &quot;Segurança de documentos Convidar usuário&quot; aos usuários e grupos apropriados em sua organização. (Consulte [Adicionar um domínio local](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) e [Criação e configuração de funções](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).) Se você não usar o registro integrado, deverá ter seu próprio sistema de registro de usuário criado usando o SDK de formulários do AEM. Consulte a ajuda em &quot;Desenvolvendo SPIs para formulários AEM&quot; em [Programação com formulários AEM](/help/forms/developing/introducing-java-api-soap-quick.md). Se você não usar a opção Registro interno, é recomendável configurar uma mensagem no email de ativação e na tela de logon do cliente para notificar os usuários sobre como entrar em contato com o administrador para obter uma nova senha ou outras informações.

**Habilitar e configurar o registro de usuários convidados**

Por padrão, o processo de registro do usuário convidado é desativado. Você pode ativar e desativar o registro de usuário convidado para segurança de documentos, conforme necessário.

1. No console de administração, clique em Serviços > segurança de documentos > Configuração > Registro de usuário convidado.
1. Selecione Habilitar Registro de Usuário Convidado.
1. (Opcional) Atualize as configurações de registro do usuário convidado conforme necessário:

   * [Excluir ou incluir um usuário ou grupo externo](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [Parâmetros da conta de registro e do servidor](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [Configurações de email do convite de registro](configuring-client-server-options.md#registration-invitation-email-settings)
   * [Configurações de email de ativação](configuring-client-server-options.md#activation-email-settings)
   * [Configurar um email de redefinição de senha](configuring-client-server-options.md#configure-a-password-reset-email)

1. (Opcional) Em Registro interno, selecione Sim para ativar essa opção. Se você não habilitar o registro incorporado, deverá configurar seu próprio sistema de registro de usuário.
1. Clique em OK.

### Excluir ou incluir um usuário ou grupo externo {#exclude-or-include-an-external-user-or-group}

É possível restringir o registro com segurança de documentos para determinados usuários externos ou grupos de usuários. Essa opção é útil, por exemplo, para permitir o acesso a um determinado grupo de usuários, mas excluir indivíduos específicos que fazem parte do grupo.

As configurações a seguir estão na área Filtro de restrição de email da página Registro de usuário convidado.

**Exclusão:** Digite o endereço de email de um usuário ou grupo a ser excluído. Para excluir vários usuários ou grupos, digite cada endereço de email em uma nova linha. Para excluir todos os usuários que pertencem a um domínio específico, digite um curinga e o nome do domínio. Por exemplo, para excluir todos os usuários no domínio example.com, digite &amp;ast;.example.com.

**Inclusão:** Digite o endereço de email de um usuário ou grupo para incluir. Para incluir vários usuários ou grupos, digite cada endereço de email em uma nova linha. Para incluir todos os usuários que pertencem a um domínio específico, digite um curinga e o nome do domínio. Por exemplo, para incluir todos os usuários no domínio example.com, digite &amp;ast;.example.com.

### Parâmetros da conta de registro e do servidor {#server-and-registration-account-parameters}

As configurações a seguir estão na área Configurações gerais da página Registro de usuário convidado.

**Host SMTP:** O nome do host do servidor SMTP. O servidor SMTP gerencia os avisos de email de saída para registrar e ativar contas de usuários convidados.

Se necessário para o host SMTP, digite as informações necessárias nas caixas Nome da conta do servidor SMTP e Senha da conta do servidor SMTP para se conectar ao servidor SMTP. Algumas organizações não impõem esse requisito. Se precisar de informações, consulte o administrador do sistema.

**Nome da classe de soquete do servidor SMTP:** Nome da classe de soquete para o servidor SMTP. Por exemplo, javax.net.ssl.SSLSocketFactory.

**Tipo de conteúdo do email:** Tipo MIME aceito, como text/plain ou text/html.

**Codificação de email:** Formato de codificação a ser usado ao enviar mensagens de email. Você pode especificar qualquer codificação, por exemplo, UTF-8 para Unicode ou ISO-8859-1 para Latin. O padrão é UTF-8.

**Endereço de email de redirecionamento:** Quando você especifica um endereço de email para essa configuração, qualquer novo convite é enviado para o endereço fornecido. Essa configuração pode ser útil para fins de teste.

**Usar domínios locais:** Selecione o domínio apropriado. Em uma nova instalação, certifique-se de criar o domínio usando o Gerenciamento de usuários. Se isso for uma atualização, um domínio de usuário externo foi criado durante a atualização e pode ser usado.

**Usar SSL para servidor SMTP:** Selecione esta opção para ativar o SSL para o servidor SMTP.

**Exibir link de logon na página de registro:** Exibe um link de login na página de registro exibida para usuários convidados.

**Para ativar o protocolo TLS para o servidor SMTP**

1. Abra o console de administração.

   O local padrão do console de Administração é `https://<server>:<port>/adminui`.

1. Navegue até Início > Serviços > Segurança de documentos > Configuração > Registro de usuário convidado.
1. No Registro de usuário convidado, especifique todas as definições de configuração e clique em OK.

   >[!NOTE]
   >
   >Se você estiver usando o Microsoft Office 365 como servidor SMTP para enviar os convites para registro de usuário, use as seguintes configurações:
   >
   >**Host SMTP:** smtp.office365.com
   >**Porta:** 587

1. Em seguida, é necessário atualizar o config.xml. Consulte [Configuração para habilitar SMTP para TLS (Transport Layer Security)](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>Se você fizer alterações nas opções Registro de usuário convidado, o arquivo config.xml será substituído e o TLS será desativado. Se você substituir as alterações, será necessário executar a etapa acima para reativar o suporte TLS para o Registro de usuário convidado.

### Configurações de email do convite de registro {#registration-invitation-email-settings}

A Segurança de documentos emite automaticamente um email de convite de registro quando você cria uma conta de usuário convidado ou quando um usuário existente adiciona um destinatário externo que não se registrou anteriormente ou foi convidado a se registrar em uma política. O email contém um link que o destinatário pode usar para acessar a página de registro e inserir informações pessoais da conta, incluindo nome de usuário e senha. A senha pode ser qualquer combinação de oito caracteres.

Quando o recipient ativa a conta, o usuário se torna um usuário local.

As configurações a seguir estão na área Configuração de email de convite da página Registro de usuário convidado.

**De:** O endereço de email do qual o email de convite é enviado. O formato padrão do endereço de email Do é postmaster@[your_installation_domain].com

**Assunto:** Assunto padrão da mensagem de email de convite.

**Tempo limite:** O número de dias após o qual o convite de registro expira se o usuário externo não se registrar. O valor padrão é 30 dias.

**Mensagem:** O texto que aparece no corpo da mensagem convidando o usuário a se registrar.

### Configurações de email de ativação {#activation-email-settings}

Depois que os usuários convidados se registrarem, a segurança de documentos enviará um email de ativação. O email de ativação contém um link para a página de ativação da conta, onde os usuários podem ativar sua conta. Quando as contas são ativadas, os usuários podem fazer logon na segurança de documentos usando seu endereço de email e a senha que criaram ao se registrarem.

Quando o recipient ativa a conta do usuário, ele se torna um usuário local.

As configurações a seguir estão na área Configuração de email de ativação da página Registro de usuário convidado.

>[!NOTE]
>
>Também é recomendável configurar uma mensagem na tela de logon para avisar aos usuários externos como entrar em contato com o administrador para obter uma nova senha ou outras informações.

**De:** O endereço de email do qual o email de ativação é enviado. Esse endereço de email recebe avisos de falha no delivery do host de email do inscrito e também todas as mensagens que o recipient enviar em resposta ao email de registro. O formato padrão do endereço de email Do é postmaster@[your_installation_domain].com

**Assunto:** Assunto padrão da mensagem de email de ativação.

**Tempo limite:** O número de dias após os quais o convite de ativação expira se o usuário não ativar a conta. O valor padrão é 30 dias.

**Mensagem:** O texto que aparece no corpo da mensagem uma mensagem indicando que a conta de usuário do recipient precisa ser ativada. Também é possível incluir informações como como entrar em contato com um administrador para obter uma nova senha.

### Configurar um email de redefinição de senha {#configure-a-password-reset-email}

Se você precisar redefinir a senha de um usuário convidado, será gerado um email de confirmação convidando o usuário a escolher uma nova senha. A senha de um usuário não pode ser determinada; se o usuário a esquecer, você deverá redefini-la.

As configurações a seguir estão na área Redefinir e-mail de senha da página Registro de usuário convidado.

**De:** O endereço de email do qual o email de redefinição de senha é enviado. O formato padrão do endereço de email Do é postmaster@[your_installation_domain].com

**Assunto:** Assunto padrão da mensagem de email de redefinição.

**Mensagem:** O texto que aparece no corpo da mensagem uma mensagem indicando que a senha do usuário externo do recipient foi redefinida.

## Permitir que usuários e grupos criem políticas {#enable-users-and-groups-to-create-policies}

A página Configuração tem um link para a página Minhas Políticas, onde você especifica quais usuários finais podem criar minhas políticas e quais usuários e grupos estão visíveis nos resultados da pesquisa. A página Minhas Políticas tem duas guias:

**Guia Criar Políticas:** Use para configurar permissões de usuário para criar políticas personalizadas.

**Guia Usuários e grupos visíveis:** Use para controlar quais usuários e grupos ficam visíveis nos resultados da pesquisa de usuários. É necessário que o superusuário ou o administrador do conjunto de políticas selecione e adicione domínios, criados no Gerenciamento de usuários, ao usuário e grupo visíveis para cada conjunto de políticas. Essa lista é visível para o coordenador de conjunto de políticas e é usada para colocar limites em quais domínios o coordenador de conjunto de políticas pode navegar ao escolher usuários para adicionar às políticas.

Antes de dar aos usuários permissão para criar políticas personalizadas, considere quanto acesso ou controle você deseja que os usuários individuais tenham. Além disso, considere como você deseja que seus usuários e grupos estejam expostos ao torná-los visíveis para pesquisas.

### Especificar usuários e grupos que podem criar políticas {#specify-users-and-groups-who-can-create-policies}

Como administrador, especifique quais usuários e grupos podem criar políticas personalizadas. Essa permissão pode ser definida no nível do usuário e do grupo. A funcionalidade de pesquisa pesquisa usuários e grupos no banco de dados de Gerenciamento de usuários.

1. No console de administração, clique em Serviços > Segurança de documentos > Configuração > Minhas políticas.
1. Na página Minhas políticas, clique na guia Criar políticas e clique em Adicionar usuários e grupos.
1. Na caixa Localizar, digite o nome de usuário ou endereço de email do usuário ou grupo que você está procurando. Se você não tiver essas informações, deixe a caixa vazia. Você também pode digitar um nome parcial ou endereço de email, como quando conhece apenas as duas primeiras letras de um nome de usuário.
1. Na lista Utilizando, selecione o Nome ou Email dos parâmetros de pesquisa.
1. Na lista Tipo, selecione Grupo ou Usuário para restringir sua pesquisa.
1. Na lista Em, selecione o domínio a ser pesquisado. Se você não souber o domínio do usuário ou grupo, selecione Todos os domínios.
1. Na lista Exibir, especifique o número de resultados da pesquisa a serem exibidos por página e clique em Localizar.
1. Para adicionar usuários e grupos em Minhas políticas, marque a caixa de seleção para cada usuário e grupo a serem adicionados.
1. Clique em Adicionar e em OK.

Os usuários e grupos selecionados agora têm permissão para criar políticas personalizadas.

### Remover a permissão Criar políticas personalizadas de um usuário ou grupo {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. Na página Segurança de documentos, clique em Configuração > Minhas políticas.
1. Na página Minhas Políticas, clique na guia Criar Políticas. Usuários e grupos com permissões para criar políticas personalizadas são exibidos.
1. Marque a caixa de seleção ao lado dos usuários e grupos a serem removidos dessa permissão.
1. Clique em Excluir e em OK.

### Especificar usuários e grupos que estão visíveis em pesquisas {#specify-users-and-groups-that-are-visible-in-searches}

Quando os usuários estão gerenciando suas políticas personalizadas, eles podem pesquisar usuários e grupos para adicionar às suas políticas. Especifique os domínios a partir dos quais os usuários e grupos ficam visíveis nessas pesquisas.

1. Na página Segurança de documentos, clique em Configuração > Minhas políticas.
1. Na página Minhas políticas, clique na guia Usuários e grupos visíveis.
1. Para tornar visíveis os usuários e grupos em um domínio, clique em Adicionar domínios, selecione os domínios e clique em Adicionar. Para remover um domínio, marque a caixa de seleção ao lado do nome do domínio e clique em Excluir.

## Editando manualmente o arquivo de configuração de segurança de documentos {#manually-editing-the-document-security-configuration-file}

Você pode importar e exportar as informações de configuração armazenadas no banco de dados de segurança de documentos. Por exemplo, talvez você queira fazer uma cópia de backup das informações de configuração ao migrar de um ambiente de preparo para um ambiente de produção, ou editar opções avançadas que só podem ser configuradas para editar esse arquivo.

Você pode fazer as seguintes alterações usando o arquivo de configuração:

[Exibir permissões CATIA ao criar e editar políticas](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[Especifique um período de tempo limite para a sincronização offline](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[Negação de serviços de segurança de documentos para aplicativos específicos](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[Alterar os parâmetros de configuração da marca d&#39;água](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[Desabilitação de links externos](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>A importação do arquivo de configuração reconfigura seu sistema com base nas informações do arquivo. As exceções são a configuração de marca d&#39;água dinâmica e informações de eventos personalizados, que não são salvas com o arquivo de configuração exportado. Configure essas informações manualmente no novo sistema. Somente um administrador de sistema ou um consultor de serviços profissionais familiarizado com a segurança de documentos e XML deve modificar o conteúdo de um arquivo de configuração, por exemplo, para redefinir uma configuração corrompida ou ajustar parâmetros para um cenário de implantação corporativa específico.

**Exportar um arquivo de configuração**

1. No console de administração, clique em Serviços > segurança de documentos 11 > Configuração > Configuração manual.
1. Clique em Exportar e salve o arquivo de configuração em outro local. O nome de arquivo padrão é config.xml.
1. Clique em OK.
1. Antes de alterar o arquivo de configuração, faça uma cópia de backup caso precise reverter.

**Importar um arquivo de configuração**

1. No console de administração, clique em Serviços > segurança de documentos 11 > Configuração > Configuração manual.
1. Clique em Procurar para acessar o arquivo de configuração e clique em Importar. Não é possível digitar o caminho diretamente na caixa Nome do arquivo.
1. Clique em OK.

### Especifique um período de tempo limite para a sincronização offline {#specify-a-timeout-period-for-offline-synchronization}

A segurança de documentos permite que os usuários abram e usem documentos protegidos quando não estiverem conectados ao servidor de segurança de documentos. O aplicativo cliente do usuário deve sincronizar regularmente com o servidor para manter os documentos válidos para uso offline. Na primeira vez que os usuários abrirem um documento protegido, será perguntado se o computador deve ser autorizado a executar a sincronização periódica do cliente.

Por padrão, a sincronização ocorre automaticamente a cada quatro horas e conforme necessário quando um usuário está conectado ao servidor de segurança de documentos. Se o período offline de um documento expirar enquanto o usuário estiver offline, ele deverá se reconectar ao servidor para habilitar o aplicativo cliente para sincronizar com o servidor.

No arquivo de configuração de segurança de documentos, você pode especificar a frequência padrão da sincronização automática em segundo plano. Essa configuração atua como os aplicativos cliente de período de tempo limite padrão, a menos que o cliente defina explicitamente seu próprio valor de tempo limite.

1. Exporte o arquivo de configuração de segurança de documentos. (Consulte [Editando manualmente o arquivo de configuração de segurança de documentos](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra o arquivo de configuração em um editor e localize o `PolicyServer` nó. Nesse nó, localize a variável `ServerSettings` nó.
1. No `ServerSettings` adicione esta seguinte entrada e salve o arquivo:

   `<entry key="BackgroundSyncFrequency" value="`*hora* `"/>`

   onde *hora* é o número de segundos entre sincronizações automáticas em segundo plano. Se você enviou esse valor para `0`, a sincronização sempre ocorre. O valor padrão é `14400` segundos (a cada quatro horas).

1. Importe o arquivo de configuração. (Consulte [Editando manualmente o arquivo de configuração de segurança de documentos](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Negação de serviços de segurança de documentos para aplicativos específicos {#denying-document-security-services-for-specific-applications}

Você pode configurar a segurança de documentos para negar serviços a aplicativos que atendam a critérios específicos. Os critérios podem especificar um único atributo, como um nome de plataforma, ou podem especificar vários conjuntos de atributos. Este recurso pode ajudá-lo a controlar as solicitações que a segurança do documento deve processar. Estas são algumas aplicações deste recurso:

* **Proteção de receita:** Você pode negar acesso a qualquer aplicativo cliente que não suporte suas convenções de receita.
* **Compatibilidade de aplicativos:** Alguns aplicativos podem ser incompatíveis com as políticas ou o comportamento do servidor de segurança de documentos.

Quando os aplicativos clientes tentam estabelecer um link com a segurança de documentos, eles fornecem informações sobre o aplicativo, a versão e a plataforma. A segurança de documentos compara essas informações com as configurações de Negações que elas obtêm do arquivo de configuração de segurança de documentos.

As configurações de Negações podem conter vários conjuntos de condições de negação. Se todos os atributos de qualquer conjunto forem correspondentes, o aplicativo solicitante não terá acesso aos serviços de segurança de documentos.

O recurso de negação de serviço exige que os aplicativos clientes usem o C++ Client SDK de segurança de documentos versão 8.2 ou posterior. Os seguintes produtos de Adobe fornecem informações sobre produtos ao solicitar serviços de segurança de documentos:

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard e posterior
* Adobe Reader 9.0 e posterior
* Extensões do Acrobat Reader DC para Microsoft Office 8.2 e posterior

Os aplicativos clientes usam a API do cliente a partir do C++ Client SDK para segurança de documentos para solicitar serviços da segurança de documentos. As solicitações de API do cliente incluem informações de versão da plataforma e do SDK (pré-compiladas na API do cliente) e informações do produto obtidas do aplicativo do cliente.

Aplicativos ou plug-ins clientes fornecem informações sobre o produto em sua implementação de uma função de retorno de chamada. O aplicativo fornece as seguintes informações:

* Nome do integrador
* Versão do integrador
* Família de aplicativos
* Nome do aplicativo
* Versão do aplicativo

Se alguma informação não for aplicável, o aplicativo cliente deixará o campo correspondente em branco.

Vários aplicativos Adobe incluem informações de produto ao solicitar serviços de segurança de documentos, incluindo Acrobat, Adobe Reader e extensões Acrobat Reader DC para o Microsoft Office.

**ACROBAT e ADOBE READER**

Quando a Acrobat ou a Adobe Reader solicitam um serviço da segurança de documentos, ela fornece as seguintes informações do produto:

* **Integrador:** Adobe Systems, Inc.
* **Versão do integrador:** 1.0
* **Família de aplicativos:** Acrobat
* **Nome do aplicativo:** Acrobat
* **Versão do aplicativo:** 9.0.0

**Extensões do Acrobat Reader DC para Microsoft Office**

Extensões do Acrobat Reader DC para Microsoft Office é um plug-in usado com os produtos Microsoft Office Microsoft Word, Microsoft Excel e Microsoft PowerPoint. Quando solicita um serviço, fornece as seguintes informações:

* **Integrador:** Adobe Systems Incorporated
* **Versão do integrador:** 8.2
* **Família de aplicativos:** Extensões do Acrobat Reader DC para Microsoft Office
* **Nome do aplicativo:** Microsoft Word, Microsoft Excel ou Microsoft PowerPoint
* **Versão do aplicativo:** 2003 ou 2007

**Configurar a segurança de documentos para negar serviços para aplicativos específicos**

1. Exporte o arquivo de configuração de segurança de documentos. (Consulte [Editando manualmente o arquivo de configuração de segurança de documentos](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra o arquivo de configuração em um editor e localize o `PolicyServer` nó. Adicionar um `ClientVersionRules` nó como filho imediato de `PolicyServer` nó, se um não existir:

   ```xml
    <node name="ClientVersionRules">
        <map>
            <entry key="infoURL" value="URL"/>
        </map>
        <node name="Denials">
            <map/>
            <node name="MyEntryName">
                <map>
                    <entry key="SDKPlatforms" value="platforms"/>
                    <entry key="SDKVersions" value="versions"/>
                    <entry key="AppFamilies" value="families"/>
                    <entry key="AppNames" value="names"/>
                    <entry key="AppVersions" value="versions"/>
                    <entry key="Integrators" value="integrators"/>
                    <entry key="IntegratorVersions" value="versions"/>
                </map>
            </node>
            <node name="MyOtherEntryName"
                <map>
                    [...]
                </map>
            </node>
            [...]
        </node>
    </node>
   ```

   em que:

   `SDKPlatforms` especifica a plataforma que hospeda o aplicativo cliente. Os valores possíveis são:

   * Microsoft Windows
   * APPLE OS X
   * Sun Solaris
   * HP-UX

   `SDKVersions` especifica a versão da API do Cliente C++ de segurança de documentos usada pelo aplicativo cliente. Por exemplo, `"8.2"`.

   `APPFamilies` é definido pela API do cliente.

   `AppName`especifica o nome do aplicativo cliente. Vírgulas são usadas como separadores de nome. Para incluir uma vírgula em um nome, use um caractere de barra invertida (\) no escape. Por exemplo, *&quot;Adobe Systems&quot;*.

   `AppVersions` especifica a versão do aplicativo cliente.

   `Integrators` especifica o nome da empresa ou grupo que desenvolveu o plug-in ou o aplicativo integrado.

   `IntegratorVersions` é a versão do plug-in ou do aplicativo integrado.

1. Para cada conjunto adicional de dados de negação, adicione outro *MyEntryName* elemento.
1. Salve o arquivo de configuração.
1. Importe o arquivo de configuração. (Consulte [Editando manualmente o arquivo de configuração de segurança de documentos](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

**Exemplos**

Neste exemplo, todos os clientes Windows têm o acesso negado.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://www.dont.use/windows.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="SDKPlatforms" value="Microsoft Windows"/>
             </map>
         </node>
     </node>
 </node>
```

Neste exemplo, o acesso é negado às versões 3.0 e 2.0 do Meu outro aplicativo. O mesmo URL de informações de negação é usado independentemente do motivo da negação.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://get.a.new/version.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="FirstDenialSettings">
             <map>
                 <entry key="AppNames" value="My Application"/>
                 <entry key="AppVersions" value="3.0"/>
             </map>
         </node>
         <node name="SecondDenialSettings">
             <map>
                 <entry key="AppNames" value="My Other Application"/>
                 <entry key="AppVersions" value="2.0"/>
             </map>
         </node>
     </node>
 </node>
```

Neste exemplo, todas as solicitações de uma instalação do Microsoft PowerPoint 2007 ou Microsoft PowerPoint 2010 de extensões do Acrobat Reader DC para Microsoft Office são negadas.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://get.a.new/version.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="AppFamilies" value=
     "document security Extension for Microsoft Office"/>
                 <entry key="AppNames" value= "Microsoft PowerPoint"/>
                 <entry key="AppVersions" value="2007,2010"/>
             </map>
         </node>
     </node>
 </node
```

### Alterar os parâmetros de configuração da marca d&#39;água {#change-the-watermark-configuration-parameters}

Por padrão, você pode especificar no máximo cinco elementos em uma marca d&#39;água. Além disso, o tamanho máximo de arquivo do documento PDF que você deseja usar como marca d&#39;água é limitado a 100 KB. Você pode alterar esses parâmetros no arquivo config.xml.

***observação **: Altere esses parâmetros com cuidado.*

1. Exporte o arquivo de configuração de segurança de documentos. (Consulte [Editando manualmente o arquivo de configuração de segurança de documentos](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra o arquivo de configuração em um editor e localize o `ServerSettings` nó.
1. No `ServerSettings` adicione as seguintes entradas e salve o arquivo: `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   A primeira entrada, *tamanho máximo do arquivo* é o tamanho máximo de arquivo (em KB) permitido para um elemento de marca d&#39;água PDF. O padrão é 100KB.

   A segunda entrada, *máximo de elementos* é o número máximo de elementos permitidos em uma marca d&#39;água. O padrão é 5.

   ```xml
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. Importe o arquivo de configuração. (Consulte [Editando manualmente o arquivo de configuração de segurança de documentos](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Desabilitação de links externos {#disabling-external-links}

Muitos usuários da segurança de documentos não têm acesso a links externos, como **www.adobe.com** enquanto usam as interfaces de usuário do Rights Management:

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`.

As seguintes alterações no config.xml desabilitam todos os links externos das interfaces do usuário do Rights Management.

1. Exporte o arquivo de configuração de segurança de documentos. (Consulte [Editando manualmente o arquivo de configuração de segurança de documentos](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra o arquivo de configuração em um editor e localize o `DisplaySettings` nó.
1. Para desativar todos os links externos, na variável `DisplaySettings` adicione a seguinte entrada e salve o arquivo: `<entry key="ExternalLinksAllowed" value="false"/>`

   ```xml
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. Importe o arquivo de configuração. (Consulte [Editando manualmente o arquivo de configuração de segurança de documentos](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Configuração para habilitar SMTP para TLS (Transport Layer Security) {#configuration-to-enable-smtp-for-transport-layer-security-tls}

As alterações a seguir no config.xml habilitam o suporte TLS para o recurso Registro de usuário convidado.

1. Exporte o arquivo de configuração de segurança de documentos. (Consulte [Editando manualmente o arquivo de configuração de segurança de documentos](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra o arquivo de configuração em um editor e localize o `DisplaySettings` nó.
1. Localize o seguinte nó: `<node name="ExternalUser">`

   ```xml
   <node name="ExternalUser">
   ```

1. Defina o valor de `SmtpUseTls` na caixa `ExternalUser` nó para **true**.
1. Defina o valor de `SmtpUseSsl` na caixa `ExternalUser` nó para **false**.
1. Salve o `config.xml`.
1. Importe o arquivo de configuração. (Consulte [Editando manualmente o arquivo de configuração de segurança de documentos](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Desabilitar pontos de extremidade SOAP para documentos de Segurança de documentos {#disable-soap-endpoints-for-document-security-documents}

As alterações a seguir no config.xml para desabilitar pontos de extremidade SOAP para documentos de segurança de documentos.

1. Exporte o arquivo de configuração de segurança de documentos. (Consulte [Editando manualmente o arquivo de configuração de segurança de documentos](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra o arquivo de configuração em um editor e localize o seguinte nó: `<node name="DRM">`

   ```xml
   <node name="DRM">
   ```

1. No nó DRM, localize a variável `entry` nó:

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. Para desativar pontos de extremidade SOAP para documentos de segurança de documentos, defina o atributo value como **false**.

   ```xml
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. Salve o `config.xml`.
1. Importe o arquivo de configuração. (Consulte [Editando manualmente o arquivo de configuração de segurança de documentos](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Aumento da escalabilidade do servidor de segurança de documentos {#increasingscalability}

Por padrão, ao sincronizar um documento para uso offline, juntamente com as informações do documento atual, os clientes de segurança de documentos buscam políticas, marcas d&#39;água, licenças e informações de atualizações de revogação para todos os outros documentos aos quais o usuário tem acesso. Se essas atualizações e informações não estiverem sincronizadas com o cliente, um documento aberto no modo offline ainda poderá ser aberto com informações mais antigas de política, marca d&#39;água e revogação.

Você pode aumentar a escalabilidade do servidor de segurança de documentos limitando as informações que estão sendo enviadas ao cliente. A redução no volume de informações enviadas ao cliente resulta em melhor escalabilidade, menor tempo de resposta e melhor desempenho do servidor. Execute as seguintes etapas para aumentar a escalabilidade:

1. Exporte o arquivo de configuração de segurança de documentos. (Consulte [Editando manualmente o arquivo de configuração de segurança de documentos](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra o arquivo de configuração em um editor e localize o nó ServerSettings.
1. No nó ServerSettings, defina o valor do `DisableGlobalOfflineSynchronizationData`propriedade para `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   Quando definido como verdadeiro, o servidor de segurança de documentos envia informações somente para o documento atual e as informações para o restante dos documentos (os outros documentos aos quais um usuário tem acesso) não são enviadas ao cliente.

   >[!NOTE]
   >
   >Por padrão, o valor de `DisableGlobalOfflineSynchronizationData`a chave está definida como `false`.

1. Salve e importe o arquivo de configuração. (Consulte [Editando manualmente o arquivo de configuração de segurança de documentos](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
