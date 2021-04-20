---
title: Configuração das opções do cliente e do servidor
seo-title: Configuração das opções de cliente e servidor
description: Saiba como configurar as várias opções de cliente e servidor, como configurações de servidor, funções de segurança de documento e auditoria de evento.
seo-description: Saiba como configurar as várias opções de cliente e servidor, como configurações de servidor, funções de segurança de documento e auditoria de evento.
uuid: 1f9f9886-726e-4fad-9ff8-0ff11eef653e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0f069fbc-10c2-403e-9419-5e9920035d75
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '10275'
ht-degree: 0%

---


# Configurar o servidor de segurança de documentos {#configure-the-document-security-server}

1. No console de administração, clique em Serviços > segurança do documento > Configuração > Configuração do servidor.
1. Configure as configurações e clique em OK.

## Configurações do servidor {#server-configuration-settings}

**URL base:** o URL de segurança do documento base, contendo o nome do servidor e a porta. Informações anexadas à base criam URLs de conexão. Por exemplo, /edc/Main.do é anexado para acessar as páginas da Web. Os usuários também respondem a convites externos de registro de usuários por meio desse URL.

Se estiver usando IPv6, insira o URL básico como o nome do computador ou o nome DNS. Se você usar um endereço IP numérico, o Acrobat não abrirá os arquivos protegidos por política. Além disso, use o URL seguro HTTP (HTTPS) para seu servidor.

>[!NOTE]
>
>O URL base é incorporado em arquivos protegidos por políticas. Os aplicativos clientes usam o URL básico para se conectar novamente ao servidor. Os arquivos protegidos continuarão a conter o URL base, mesmo se for alterado posteriormente. Se você alterar o URL base, as informações de configuração precisarão ser atualizadas para todos os clientes conectados.

**Período padrão de concessão offline:** o período padrão em que um usuário pode usar um documento protegido offline. Essa configuração determina o valor inicial da configuração do período de concessão automática offline ao criar uma política. (Consulte Criação e edição de políticas.) Quando o período de concessão expira, o recipient deve sincronizar o documento novamente para continuar usando-o.

Para obter uma discussão sobre como a concessão e sincronização offline funcionam, consulte [Primer sobre como configurar a concessão offline e a sincronização](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html).

**Período padrão de sincronização offline:** o tempo máximo que qualquer documento pode ser usado offline de quando ele é inicialmente protegido.

**Tempo limite da sessão do cliente:** o tempo, em minutos, após o qual a segurança do documento se desconecta se um usuário que está conectado por meio de um aplicativo cliente não interagir com a segurança do documento.

**Permitir acesso de usuários anônimos:** selecione essa opção para ativar a capacidade de criar políticas compartilhadas e pessoais que permitem que usuários anônimos abram documentos protegidos por políticas. (Os usuários que não têm contas podem acessar o documento, mas não podem fazer logon na segurança do documento ou usar outros documentos protegidos por políticas).

**Desabilitar acesso a clientes da versão 7:** Especifica se os usuários podem usar o Acrobat ou o Reader 7.0 para se conectar ao servidor. Quando essa opção é selecionada, os usuários devem usar o Acrobat ou o Reader 8.0 e posterior para concluir as operações de segurança de documentos em documentos PDF. Se as políticas exigirem que o Acrobat ou o Reader 8.0 e posterior sejam executados no modo certificado ao abrir documentos protegidos por política, você deve desativar o acesso ao Acrobat ou ao Reader 7. (Consulte Especificar as permissões do documento para usuários e grupos.)

**Permitir acesso offline por** documentoSelecione esta opção para especificar o acesso offline por documento. Se essa configuração estiver ativada, o usuário terá acesso offline somente aos documentos que o usuário abriu online pelo menos uma vez.

**Permitir Autenticação de Senha do Nome de Usuário:** Selecione esta opção para permitir que os aplicativos cliente usem a autenticação de nome de usuário/senha ao se conectar ao servidor.

**Permitir Autenticação Kerberos:** Selecione esta opção para permitir que os aplicativos cliente usem a autenticação Kerberos ao se conectar ao servidor.

**Permitir Autenticação de Certificado de Cliente:** Selecione esta opção para permitir que os aplicativos cliente usem autenticação de certificado ao se conectar ao servidor.

**Permitir** Autenticação EstendidaSelecione para habilitar a autenticação estendida e, em seguida, insira o URL de Aterrissagem da Autenticação Estendida.

A seleção dessa opção permite que aplicativos clientes usem autenticação estendida. A autenticação estendida fornece processos de autenticação personalizados e opções de autenticação diferentes configuradas no servidor de formulários AEM. Por exemplo, agora os usuários podem experimentar a autenticação baseada em SAML em vez de AEM nome de usuário/Senha dos formulários, do Acrobat e do Reader Client. Por padrão, a URL de aterrissagem contém *localhost* como o nome do servidor. Substitua o nome do servidor por um nome de host totalmente qualificado. O nome do host na URL de aterrissagem é preenchido automaticamente a partir da URL base, se a Autenticação estendida ainda não estiver habilitada. Consulte [Adicionar o provedor de autenticação estendido](configuring-client-server-options.md#add-the-extended-authentication-provider).

***observação **: A autenticação estendida é compatível com o Apple Mac OS X com o Adobe Acrobat versão 11.0.6 e superior.*

**Largura de controle HTML preferencial para** autenticação estendidaEspecifique a largura da caixa de diálogo de autenticação estendida que é aberta no Acrobat para inserir credenciais de usuário.

**Altura de Controle HTML Preferencial para** Autenticação EstendidaEspecifique a altura da caixa de diálogo de autenticação estendida que é aberta no Acrobat para inserir credenciais de usuário.

***observação **: Os limites de largura e altura dessa caixa de diálogo são os seguintes:*
Largura: Mínimo = 400, máximo = 900

Altura: Mínimo = 450; máximo = 800

**Ativar o Cache de Credenciais do Cliente:** Selecione esta opção para permitir que os usuários armazenem em cache suas credenciais (nome de usuário e senha). Quando as credenciais dos usuários são armazenadas em cache, eles não precisam digitar as credenciais toda vez que abrirem um documento ou quando clicarem no botão Atualizar na página Gerenciar políticas de segurança no Adobe Acrobat. Você pode especificar o número de dias antes de os usuários deverem fornecer suas credenciais novamente. Definir o número de dias como 0 permite que as credenciais sejam armazenadas em cache indefinidamente.

## Configurar usuários e administradores de segurança de documento {#configuring-document-security-users-and-administrators}

### Atribuindo funções de segurança de documento a administradores {#assigning-document-security-roles-to-administrators}

Seu ambiente de formulários AEM contém um ou mais usuários administradores que têm os privilégios apropriados para criar usuários e grupos. Se sua organização estiver usando a segurança de documentos, pelo menos um administrador também deverá ter o privilégio de gerenciar usuários convidados e locais.

Os administradores também devem ter a função Usuário do console de administração para acessar o console de administração. (Consulte [Criação e configuração de funções](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

### Configuração de usuários e grupos visíveis {#configuring-visible-users-and-groups}

Para visualizar usuários e grupos em domínios selecionados durante pesquisas de usuário de política, um superadministrador ou administrador de conjunto de políticas deve selecionar e adicionar domínios (criados no Gerenciamento de usuários) à lista de usuários e grupos visível para cada conjunto de políticas.

A lista de usuários e grupos visível é visível para o coordenador do conjunto de políticas e é usada para restringir quais domínios o usuário final pode navegar ao escolher usuários ou grupos para adicionar às políticas. Se esta tarefa não for executada, o coordenador do conjunto de políticas não encontrará usuários ou grupos para adicionar à política. Pode haver mais de um coordenador de conjunto de políticas para qualquer conjunto de políticas.

1. Depois de instalar e configurar o ambiente AEM forms com a segurança do documento, configure todos os domínios apropriados no Gerenciamento de usuários. <!-- Fix broken link (See Setting up and managing domains) -->

   ***observação **: A criação de domínios deve ser feita antes que qualquer política possa ser criada.*

1. No console de administração, clique em Serviços > Gerenciamento de documentos > Políticas e, em seguida, clique na guia Conjuntos de políticas .
1. Selecione Conjunto de políticas global e clique na guia Usuários e grupos visíveis .
1. Clique em Adicionar domínio(s) e adicione domínios existentes conforme necessário.
1. Navegue até Serviços > segurança do documento > Configuração > Minhas políticas e clique na guia Usuários e grupos visíveis .
1. Clique em Adicionar domínio(s) e adicione domínios existentes conforme necessário.

## Adicionar o provedor de autenticação estendido {#add-the-extended-authentication-provider}

AEM formulários fornece uma configuração de amostra que pode ser personalizada para seu ambiente. Execute as seguintes etapas:

>[!NOTE]
>
>A autenticação estendida é compatível com o Apple Mac OS X com o Adobe Acrobat versão 11.0.6 e superior.

1. Obtenha o arquivo WAR de amostra para implantá-lo. Consulte o guia de instalação apropriado para seu servidor de aplicativos.
1. Certifique-se de que o servidor de formulários tenha um nome totalmente qualificado em vez de endereços IP como o URL base e que seja um URL HTTPS. Consulte [Configurações do servidor](configuring-client-server-options.md#server-configuration-settings).
1. Habilite Autenticação Estendida na página Configuração do Servidor. Consulte [Configurações do servidor](configuring-client-server-options.md#server-configuration-settings).
1. Adicione os URLs de redirecionamento SSO necessários no arquivo de configuração do Gerenciamento de usuários . Consulte [Adicionar URLs de redirecionamento SSO para autenticação estendida](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication).

### Adicionar URLs de redirecionamento SSO para autenticação estendida {#add-sso-redirect-urls-for-extended-authentication}

Com a autenticação estendida ativada, os usuários que abrem um documento protegido por política no Acrobat XI ou no Reader XI obtêm uma caixa de diálogo para autenticação. Essa caixa de diálogo carrega a página HTML que você especificou como URL de aterrissagem de autenticação estendida nas configurações do servidor de segurança do documento. Consulte [Configurações do servidor](configuring-client-server-options.md#server-configuration-settings).

>[!NOTE]
>
>A autenticação estendida é compatível com o Apple Mac OS X com o Adobe Acrobat versão 11.0.6 e superior.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração.
1. Clique em Exportar e salve o arquivo de configuração no disco.
1. Abra o arquivo em um editor e localize o nó AllowedUrls .
1. No nó `AllowedUrls` , adicione as seguintes linhas: `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. Salve o arquivo e importe o arquivo atualizado da página Configuração manual: No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração.

## Configuração da segurança offline {#configuring-offline-security}

a segurança de documentos fornece a capacidade de utilizar documentos protegidos por políticas offline sem uma ligação à Internet ou à rede. Essa capacidade requer que a política permita acesso offline, conforme descrito em [Especifique as permissões do documento para usuários e grupos](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). Antes de um documento com essa política poder ser usado offline, o destinatário deve abrir o documento enquanto estiver online e ativar o acesso offline, clicando em Sim quando solicitado. O destinatário pode igualmente ser convidado a autenticar a sua identidade. O recipient pode usar documentos offline pela duração do período de concessão offline especificado na política.

Quando o período de concessão offline terminar, o recipient deverá sincronizar novamente com a segurança do documento abrindo um documento online ou usando um comando de menu Acrobat ou Acrobat Reader DC Extensions para sincronizar. (Consulte *Ajuda do Acrobat* ou a *Ajuda do Acrobat Reader DC Extensions apropriada*.)

Como os documentos que permitem acesso offline exigem o armazenamento do material da chave em cache no computador em que os arquivos são armazenados offline, o arquivo pode ser comprometido se um usuário não autorizado puder obter o material da chave. Para compensar essa possibilidade, as opções de sobreposição de chave agendadas e manuais são fornecidas e podem ser configuradas para impedir que uma pessoa não autorizada use a chave para acessar o documento.

### Definir um período de concessão offline padrão {#set-a-default-offline-lease-period}

Os destinatários de documentos protegidos por uma política podem colocar os documentos offline durante o número de dias especificado na política. Após sincronizar inicialmente o documento com a segurança do documento, o recipient poderá usá-lo offline até que o período de concessão offline expire. Quando o período de concessão expira, o recipient deve colocar o documento online e fazer logon para sincronizar com a segurança do documento e continuar usando o documento.

Você pode configurar um período de concessão offline padrão. O período de concessão pode ser alterado a partir do padrão quando qualquer pessoa cria ou edita uma política.

1. Na página de segurança do documento, clique em Configuração > Configuração do Servidor.
1. Na caixa Período padrão de concessão offline , digite o número de dias para o período de concessão offline.
1. Clique em OK.

### Gerenciar sobreposições de chaves {#manage-key-rollovers}

A segurança de documentos usa algoritmos de criptografia e licenças para proteger documentos. Quando criptografa um documento, a segurança do documento gera e gerencia uma chave de descriptografia chamada *DocKey* que ela passa para o aplicativo cliente. Se a política que protege um documento permitir acesso offline, uma chave offline chamada *chave principal* também será gerada para cada usuário que tenha acesso offline ao documento.

>[!NOTE]
>
>Se uma chave principal não existir, a segurança do documento gera uma para proteger um documento.

Para abrir um documento protegido por política offline, o computador do usuário deve ter a chave principal apropriada. O computador obtém a chave principal quando o usuário sincroniza com a segurança do documento (abre um documento protegido online). Se essa chave principal estiver comprometida, qualquer documento ao qual o usuário tenha acesso offline também poderá ser comprometido.

Uma maneira de diminuir a ameaça aos documentos offline é evitar permitir o acesso offline a documentos particularmente sensíveis. Outro método é passar periodicamente sobre as chaves principais. Quando a segurança do documento rola a chave, qualquer chave existente não pode mais acessar os documentos protegidos por políticas. Por exemplo, se um autor obtiver uma chave principal de um laptop roubado, essa chave não poderá ser usada para acessar os documentos protegidos depois que a sobreposição ocorrer. Se você suspeitar que uma chave principal específica foi comprometida, poderá passar o mouse sobre a chave manualmente.

No entanto, você também precisa estar ciente de que uma sobreposição de chave afeta todas as chaves principais, não apenas uma. Também reduz a escalabilidade do sistema, pois os clientes devem armazenar mais chaves para acesso offline. A frequência padrão de sobreposição de chave é de 20 dias. É recomendável não definir esse valor com menos de 14 dias, pois as pessoas podem ser impedidas de visualizar documentos offline e o desempenho do sistema pode ser afetado.

No exemplo a seguir, Key1 é a mais antiga das duas chaves principais e Key2 é a mais nova. Quando você clica no botão Chaves de Sobreposição Agora na primeira vez, a Chave1 se torna inválida e uma chave principal válida mais nova (Chave3) é gerada. Os usuários obterão o Key3 quando sincronizarem com a segurança do documento, normalmente abrindo um documento protegido online. No entanto, os usuários não são forçados a sincronizar com a segurança do documento até atingirem o período máximo de concessão offline especificado em uma política. Após a primeira substituição de chave, os usuários que permanecem offline ainda poderão abrir documentos offline, incluindo aqueles protegidos por Key3, até atingirem o período máximo de concessão offline. Quando você clica no botão Chaves de Rolagem Agora uma segunda vez, a Chave2 se torna inválida e a Chave4 é criada. Os usuários que permanecem offline durante as duas sobreposições de chave não podem abrir documentos protegidos com Chave3 ou Chave4 até sincronizarem com a segurança do documento.

**Alterar a frequência de sobreposição de chave**

Para fins de confidencialidade, quando você está usando documentos offline, a segurança de documento fornece uma opção de sobreposição automática de chave com um período de frequência padrão de 20 dias. Você pode alterar a frequência de sobreposição; no entanto, evite definir o valor com menos de 14 dias, pois as pessoas podem ser impedidas de visualizar documentos offline e o desempenho do sistema pode ser afetado.

1. Na página segurança do documento, clique em Configuração > Gerenciamento de chaves.
1. Na caixa Frequência de sobreposição de chave, digite o número de dias para o período de sobreposição.
1. Clique em OK.

**Rolar manualmente sobre as chaves principais**

Para manter a confidencialidade de documentos offline, é possível reverter manualmente as chaves principais. Você pode achar necessário passar manualmente uma chave (por exemplo, se a chave estiver comprometida por alguém que a obtenha de um computador em que está armazenada em cache para habilitar o acesso offline a um documento).

>[!NOTE]
>
>Evite usar frequentemente a sobreposição manual, pois isso faz com que todas as chaves principais sejam sobrepostas, não apenas uma, e pode impedir temporariamente que os usuários visualizem novos documentos offline.

As chaves principais devem ser submetidas a rollover duas vezes antes de as chaves existentes anteriormente em computadores clientes serem invalidadas. Os computadores clientes que têm chaves principais invalidadas devem sincronizar novamente com o serviço de segurança de documentos para adquirir as novas chaves principais.

1. Na página segurança do documento, clique em Configuração > Gerenciamento de chaves.
1. Clique em Chaves de rolagem agora e em OK.
1. Aguarde aproximadamente 10 minutos. A seguinte mensagem de log é exibida no log do servidor: `Done RightsManagement key rollover for`*N* `principals`. Onde *N* é o número de usuários no sistema de segurança de documentos.
1. Clique em Chaves de rolagem agora e em OK.
1. Aguarde aproximadamente 10 minutos.

## Configuração das configurações de privacidade e auditoria de eventos {#configuring-event-auditing-and-privacy-settings}

A segurança de documentos pode auditar e registrar informações sobre eventos relacionados à interação com documentos, políticas, administradores e o servidor protegidos por políticas. Você pode configurar a auditoria de eventos e especificar os tipos de eventos a serem auditados. Para auditar eventos de um documento específico, a opção de auditoria da política também deve estar habilitada.

Quando a auditoria estiver ativada, você poderá visualizar os detalhes dos eventos auditados na página Eventos. os usuários de segurança de documentos também podem exibir eventos relacionados especificamente aos documentos protegidos por políticas que eles usam ou criam.

Você pode selecionar esses tipos de eventos para auditoria:

* Eventos de documentos protegidos por políticas, como tentativas de abrir documentos por usuários autorizados ou não autorizados
* Eventos de política, como criar, alterar, excluir, ativar e desativar políticas
* Eventos de usuários, como convites e registros externos de usuários, contas de usuários ativadas e desativadas, alterações em senhas de usuários e atualizações de perfis
* AEM eventos de formulários, como incompatibilidades de versão, servidor de diretórios indisponível e provedores de autorização, além de alterações na configuração do servidor

### Ativar ou desativar a auditoria de eventos {#enable-or-disable-event-auditing}

Você pode ativar e desativar a auditoria de eventos relacionados ao servidor, documentos protegidos por políticas, políticas, conjuntos de políticas e usuários. Ao ativar a auditoria de eventos, você pode optar por auditar todos os eventos possíveis ou selecionar eventos específicos para auditar.

Ao ativar a auditoria do servidor, você pode exibir os eventos auditados na página Eventos.

1. No console de administração, clique em Serviços > Segurança de documento > Configuração > Configurações de auditoria e privacidade.
1. Para configurar a auditoria do servidor, em Ativar Auditoria do Servidor, selecione Sim ou Não.
1. Se você selecionou Sim, em cada categoria de evento, execute uma das seguintes ações para selecionar as opções a serem auditadas:

   * Para auditar todos os eventos na categoria , selecione Todos.
   * Para auditar apenas alguns eventos, desmarque Todos e marque as caixas de seleção ao lado dos eventos que deseja auditar.

      (Consulte [Opções de auditoria de eventos](configuring-client-server-options.md#event-auditing-options).)

1. Clique em OK.

>[!NOTE]
>
>Ao trabalhar com as páginas da Web, evite usar os botões do navegador, como o botão Voltar, o botão Atualizar e a seta para trás ou para a frente, pois essa ação pode causar problemas indesejados de captura de dados e de exibição de dados.

### Ativar ou desativar a notificação de privacidade {#enable-or-disable-privacy-notification}

Você pode ativar e desativar uma mensagem de notificação de privacidade. Quando você habilita a notificação de privacidade, uma mensagem é exibida quando um recipient tenta abrir um documento protegido por política. O aviso informa ao usuário que a utilização do documento está sendo auditada. Você também pode especificar um URL que o usuário pode usar para exibir sua página de política de privacidade, se disponível.

1. No console de administração, clique em Serviços > Segurança de documento > Configuração > Configurações de auditoria e privacidade.
1. Para configurar a notificação de privacidade, em Ativar aviso de privacidade, selecione Sim ou Não.

   Se a política anexada a um documento permitir acesso anônimo de usuário e Ativar aviso de privacidade estiver definido como Não, o usuário não será solicitado a fazer logon e a mensagem de notificação de privacidade não será exibida.

   Se a política anexada a um documento não permitir acesso anônimo de usuário, o usuário verá a mensagem de notificação de privacidade.

1. Se aplicável, na caixa URL de privacidade, digite o URL da página da política de privacidade. Se a caixa URL de privacidade for deixada em branco, a página de privacidade do adobe.com será exibida.
1. Clique em OK.

>[!NOTE]
>
>Desativar o aviso de privacidade não desativa a auditoria de uso de documentos. Ações de auditoria e ações personalizadas prontas para uso compatíveis com o rastreamento de uso estendido ainda podem coletar informações de comportamento do usuário.

### Importar um tipo de evento de auditoria personalizada {#import-a-custom-audit-event-type}

Se você estiver usando um aplicativo habilitado para segurança de documento que ofereça suporte à auditoria de eventos adicionais, como eventos específicos de um determinado tipo de arquivo, um parceiro de Adobe pode fornecer a você eventos de auditoria personalizados que podem ser importados para a segurança do documento. Use esse recurso somente se tiver recebido tipos de evento personalizados por um parceiro de Adobe.

1. No console de administração, clique em Serviços > Segurança de documento > Configuração > Gerenciamento de eventos.
1. Clique em Procurar para ir para o arquivo XML a ser importado e clique em Importar.
1. A importação substitui os tipos de evento de auditoria personalizados existentes no servidor, caso sejam encontradas combinações idênticas de código de evento e namespace.
1. Clique em OK.

### Excluir um tipo de evento de auditoria personalizada {#delete-a-custom-audit-event-type}

1. No console de administração, clique em Serviços > segurança do documento > Configuração > Gerenciamento de eventos.
1. Marque a caixa de seleção ao lado do tipo de evento de auditoria personalizada a ser excluído e clique em Excluir.
1. Clique em OK.

### Exportar eventos de auditoria {#export-audit-events}

Você pode exportar eventos de auditoria para um arquivo para fins de arquivamento.

1. No console de administração, clique em Serviços > Segurança de documento > Configuração > Gerenciamento de eventos.
1. Edite as configurações em Exportar eventos de auditoria, conforme necessário. Você pode especificar:

   * a idade mínima dos eventos de auditoria para exportar
   * o número máximo de eventos de auditoria a serem incluídos em um único arquivo. O servidor gera um ou mais arquivos, com base nesse valor.
   * a pasta onde o arquivo será criado. Essa pasta está no servidor de formulários. Se o caminho da pasta for relativo, ele será relativo ao diretório raiz do servidor de aplicativos.
   * o prefixo de arquivo a ser usado para os arquivos de eventos de auditoria
   * o formato do arquivo, seja um arquivo CSV (valores separados por vírgula) compatível com o Microsoft Excel ou um arquivo XML.

1. Clique em Exportar. Se desejar cancelar a exportação, clique em Cancelar exportação. Se outro usuário tiver agendado uma exportação, o botão Cancelar exportação ficará indisponível até que essa exportação seja concluída. O botão Cancelar exportação não estará disponível se outro usuário tiver agendado uma exportação. Para verificar se uma Exportação ou Exclusão programada foi iniciada ou concluída, clique em Atualizar.

### Excluir eventos de auditoria {#delete-audit-events}

Você pode excluir eventos de auditoria que tenham mais de um determinado número de dias.

1. No console de administração, clique em Serviços > Segurança de documento > Configuração > Gerenciamento de eventos.
1. Em Excluir eventos de auditoria, especifique o número de dias na caixa Excluir eventos de auditoria antes de .
1. Clique em Excluir. Clique em Exportar. Se desejar cancelar a exclusão, clique em Cancelar exclusão. Se outro usuário tiver agendado uma exclusão, o botão Cancelar exclusão ficará indisponível até que essa exportação seja concluída. O botão Cancelar exclusão ficará indisponível se outro usuário tiver agendado uma exportação. Para verificar se uma Exclusão programada foi iniciada ou concluída, clique em Atualizar.

### Opções de auditoria de evento {#event-auditing-options}

Você pode ativar e desativar a auditoria de eventos e especificar os tipos de eventos a serem auditados.

**Eventos de documento**

**Exibir Documento:** Um recipient exibe um documento protegido por política.

**Fechar documento:** um recipient fecha um documento protegido por política.

**Imprimir Baixa** ResoluçãoUm recipient imprime um documento protegido por política com a opção de baixa resolução especificada.

**Imprimir alta resolução:** um recipient imprime um documento protegido por política com a opção de alta resolução especificada.

**Adicionar anotação ao documento:** um destinatário adiciona uma anotação a um documento PDF.

**Revogar documento:** um usuário ou administrador revoga o acesso a um documento protegido por política.

**Cancelar revogação de documento:** um usuário ou administrador restabelece o acesso a um documento protegido por política.

**Preenchimento de formulário:** um destinatário insere informações em um documento PDF que é um formulário que pode ser preenchido.

**Política removida:** um editor remove uma política de um documento para retirar as proteções de segurança.

**Alterar URL de revogação de documento:** uma chamada do nível da API altera a URL de revogação especificada para acessar um novo documento que substitui um documento revogado.

**Modificar documento:** um recipient altera o conteúdo de um documento protegido por política.

**Assinar documento:** um recipient assina um documento.

**Proteger um novo documento:** um usuário aplica uma política para proteger um documento.

**Alternar política no documento:** um usuário ou administrador alterna a política anexada a um documento.

**Publicar documento como:** um novo documento cujo documentName e licença são idênticos a um documento existente é registrado no servidor e os documentos não têm uma relação pai-filho. Esse evento pode ser acionado usando o SDK dos formulários AEM.

**Documento Iterar:** um novo documento cujo documentName e licença são idênticos a um documento existente é registrado no servidor e os documentos têm uma relação pai-filho. Esse evento pode ser acionado usando o SDK dos formulários AEM.

**Eventos de política**

**Política criada:** um usuário ou administrador cria uma política.

**Política ativada:** um administrador disponibiliza uma política.

**Política alterada:** um usuário ou administrador altera uma política.

**Política desativada:** um administrador torna uma política indisponível.

**Política Excluída:** Um usuário ou administrador exclui uma política.

**Alterar proprietário da política:** uma chamada do nível da API altera o proprietário da política.

**Eventos do usuário**

**Usuário excluído:** um administrador exclui uma conta de usuário.

**Registrar usuário convidado:** um usuário externo se registra com segurança de documento.

**Logon bem-sucedido:** tentativas de logon bem-sucedidas de administradores ou usuários.

**Usuários convidados:** a segurança de documentos convida um usuário a se registrar.

**Usuários ativados:** usuários externos ativam suas contas usando o URL no email de ativação ou um administrador habilita uma conta.

**Alterar senha:** os usuários convidados alteram suas senhas ou um administrador redefine uma senha para um usuário local.

**Falha de logon:** tentativas de logon feitas por administradores ou usuários.

**Usuários desativados:** um administrador desativa uma conta de usuário local.

**Atualização do perfil:** usuários convidados alteram o nome, o nome da organização e a senha.

**Conta bloqueada:** um administrador bloqueia uma conta.

**Eventos de Conjunto de Políticas**

**Conjunto de políticas criado:** um administrador ou coordenador de conjunto de políticas cria um conjunto de políticas.

**Conjunto de políticas excluído:** um administrador ou coordenador de conjunto de políticas exclui um conjunto de políticas.

**Conjunto de políticas modificado:** um administrador ou coordenador de conjunto de políticas altera um conjunto de políticas.

**Eventos do sistema**

**Sincronização de Diretório Concluída:** Essas informações não estão disponíveis na página Eventos. As informações atuais de sincronização de diretórios, incluindo o estado de sincronização atual e a hora da última sincronização, são exibidas na página Gerenciamento de Domínio . Para acessar a página Gerenciamento de domínio no console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.

**Cliente Ativar Acesso Offline:** Um usuário ativou o acesso offline a documentos que são protegidos contra o servidor no computador do usuário.

**O aplicativo** ClientClient sincronizado deve sincronizar informações com o servidor para permitir acesso offline.

**Incompatibilidade de versão:** uma versão do SDK de formulários AEM incompatível com o servidor tentou se conectar ao servidor.

**Informações de Sincronização de Diretório:** Essas informações não estão disponíveis na página Eventos. As informações atuais de sincronização de diretórios, incluindo o estado de sincronização atual e a hora da última sincronização, são exibidas na página Gerenciamento de Domínio . Para acessar a página Gerenciamento de domínio no console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.

**Alteração na configuração do servidor:** alterações na configuração do servidor que são feitas por meio das páginas da Web ou manualmente importando um arquivo config.xml. Isso inclui alterações no URL base, tempo limite de sessão, travamentos de logon, configurações de diretório, sobreposições de chave, configurações do servidor SMTP para registro externo, configuração de marca d&#39;água, opções de exibição e assim por diante.

## Configurar o rastreamento de uso estendido {#configuring-extended-usage-tracking}

A segurança do documento pode rastrear vários eventos personalizados que podem ser executados em um documento protegido. Você pode habilitar o rastreamento de eventos do servidor de segurança do documento no nível global ou em um nível de política. Em seguida, você pode configurar um JavaScript para capturar ações específicas executadas no documento PDF protegido, como clicar em um botão ou salvar o documento. Esses dados de uso são enviados como um arquivo XML em pares de valores chave, que podem ser usados para análises adicionais. Os usuários finais que acessam os documentos protegidos podem permitir ou recusar esse rastreamento do aplicativo cliente.

Se o rastreamento estiver ativado no nível global, você pode substituir essa configuração no nível da política e desativá-la para uma política específica. A substituição em nível de política não é possível se o rastreamento estiver desativado no nível global. A lista de eventos rastreados é automaticamente enviada para o servidor quando a contagem de eventos atinge 25 ou quando o documento é fechado. Você também pode configurar o script para encaminhar explicitamente a lista de eventos de acordo com seus requisitos. Você pode personalizar o rastreamento de eventos acessando as propriedades e os métodos do objeto de segurança do documento.

Depois de ativar o rastreamento, todas as políticas criadas subsequentemente terão o rastreamento ativado por padrão. As políticas criadas antes de o rastreamento ser ativado no servidor precisarão de atualizações manuais.

### Ativar ou desativar o rastreamento de uso estendido {#enable-or-disable-extended-usage-tracking}

Antes de começar, verifique se a Auditoria do servidor está ativada. Consulte [Configuração de auditoria de evento e configurações de privacidade](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) para obter mais informações sobre auditoria.

1. No console de administração, clique em Serviços > Segurança de documento > Configuração > Configurações de auditoria e privacidade.
1. Para configurar o rastreamento de uso estendido, em Ativar rastreamento, selecione Sim ou Não.
1. Para definir a seleção da caixa de seleção Permitir coleta de dados de uso detalhados na página de logon, em Ativar rastreamento padrão, selecione Sim ou Não.

Para exibir os eventos rastreados, você pode usar o filtro Eventos de documento na página Eventos . Os eventos rastreados com o JavaScript são rotulados como Rastreamento de uso detalhado. Consulte [Monitoramento de eventos](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) para obter mais informações sobre eventos.

## Definir configurações de exibição de segurança do documento {#configure-document-security-display-settings}

1. No console de administração, clique em Serviços > segurança do documento > Configuração > Opções de exibição.
1. Configure as configurações e clique em OK.

### Configurações de exibição {#display-settings}

**Linhas a serem exibidas para resultados de pesquisa:** Número de linhas que aparecem em uma página quando as pesquisas são realizadas.

**Personalização da caixa de diálogo de logon do cliente**

Essas configurações controlam o texto exibido no prompt de logon que aparece quando um usuário faz login na segurança do documento por meio de um aplicativo cliente.

**Texto de boas-vindas:** O texto da mensagem de boas-vindas, como &quot;Por favor, faça logon com seu nome de usuário e senha&quot;. O texto da mensagem de boas-vindas deve conter informações sobre como fazer logon na segurança do documento e como entrar em contato com um administrador ou outra pessoa de suporte designada em sua organização para obter assistência. Por exemplo, usuários externos podem precisar entrar em contato com um administrador caso se esqueçam de suas senhas ou precisem de assistência com o processo de registro ou logon. O comprimento máximo do texto de boas-vindas é de 512 caracteres.

**Texto do nome do usuário:** o rótulo do texto para a caixa do nome do usuário.

**Texto da senha:** o rótulo do texto para a caixa de senha.

**Caixa de diálogo Personalização para autenticação de certificado de cliente**

Essas configurações controlam o texto exibido na caixa de diálogo Autenticação de certificado.

**Escolha o Texto de Tipo de Autenticação:** O texto exibido para direcionar um usuário para selecionar um tipo de autenticação.

**Escolher texto do certificado:** o texto exibido para direcionar um usuário a selecionar um tipo de certificado.

**Texto de erro dos certificados não disponíveis:** mensagem de até 512 caracteres para exibir quando o certificado selecionado não estiver disponível.

**Personalização para exibição de certificado de cliente**

**Exibir somente emissores de credenciais confiáveis:** quando essa opção é selecionada, o aplicativo cliente apresenta ao usuário apenas certificados de emissores de credenciais que AEM formulários estão configurados para confiabilidade (Consulte Gerenciar certificados e credenciais). Quando essa opção não está selecionada, o usuário recebe uma lista de todos os certificados no sistema do usuário.

## Configurar marcas d&#39;água dinâmicas {#configure-dynamic-watermarks}

Usando a segurança do documento, é possível definir as configurações padrão para a opção de marca d&#39;água dinâmica que pode ser aplicada ao criar políticas. Uma *marca d&#39;água* é uma imagem que é sobreposta ao texto no documento. É útil para rastrear o conteúdo de um documento e pode ajudar a identificar o uso ilegal do conteúdo.

Uma marca d&#39;água dinâmica pode consistir em um texto composto de variáveis definidas, como ID de usuário e data e texto personalizado, ou em conteúdo avançado em um PDF. É possível configurar marcas d&#39;água com vários elementos, cada um com seu próprio posicionamento e formatação.

As marcas d&#39;água não são editáveis e, portanto, são um método mais seguro para garantir a confidencialidade do conteúdo do documento. As marcas d&#39;água dinâmicas também garantem que uma marca d&#39;água mostre informações específicas suficientes para o usuário, de modo a dissuadir a distribuição do documento.

A marca d&#39;água que uma política especifica aparece no documento protegido por política quando um destinatário exibe ou imprime o documento. Ao contrário das marcas d&#39;água permanentes, uma marca d&#39;água dinâmica nunca é salva no documento, o que proporciona a flexibilidade necessária ao implantar um documento em um ambiente de intranet para garantir que o aplicativo de exibição exiba a identidade do usuário específico. Além disso, se um documento tiver vários usuários, o uso da marca d&#39;água dinâmica significa que você pode usar um documento em vez de várias versões, cada um com uma marca d&#39;água diferente. A marca d&#39;água que aparece reflete a identidade do usuário atual.

Observe que as marcas d&#39;água dinâmicas são diferentes das marcas d&#39;água que os usuários podem adicionar diretamente ao documento no Acrobat. O resultado é que você pode ter duas marcas d&#39;água em um documento protegido por política.

### Considerações ao criar marcas d&#39;água {#considerations-when-creating-watermarks}

É possível criar marcas d&#39;água dinâmicas com vários elementos de marca d&#39;água com cada elemento especificado como texto ou PDF. É possível incluir até cinco elementos, em uma marca d&#39;água.

Se você escolher uma marca d&#39;água baseada em texto, poderá especificar vários elementos dentro da marca com várias entradas de texto e especificar o posicionamento de cada elemento. Atribua nomes significativos a esses elementos, como cabeçalho, rodapé e assim por diante.

Por exemplo, se você quiser especificar um texto diferente no cabeçalho, no rodapé, nas margens e no documento como uma marca d&#39;água, crie vários elementos de marca d&#39;água e especifique suas posições. Se você quiser que o ID de usuário e a data atual de acesso ao documento apareçam no cabeçalho, o nome da política na margem direita e um texto personalizado &quot;CONFIDENTIAL&quot; apareçam diagonalmente no documento, defina elementos de marca d&#39;água separados com texto como tipo e especifique sua formatação e posicionamento. Quando a marca d&#39;água é aplicada a um documento, todos os elementos da marca d&#39;água são aplicados ao documento ao mesmo tempo, na ordem em que são adicionados à marca d&#39;água.

Normalmente, você usa marcas d&#39;água baseadas em PDF para incluir conteúdo gráfico, como logotipos ou símbolos especiais, como copyright ou marca registrada.

Você pode alterar os limites do número de elementos de marca d&#39;água e o tamanho do arquivo PDF modificando o arquivo de configuração de segurança do documento. Consulte [Alterar os parâmetros de configuração da marca d&#39;água](configuring-client-server-options.md#change-the-watermark-configuration-parameters).

Lembre-se do seguinte ao configurar marcas d&#39;água:

* Não é possível usar um documento PDF protegido por senha como elemento de marca d&#39;água. No entanto, se a marca d&#39;água criada contiver outros elementos que não sejam protegidos por senha, eles serão aplicados como parte da marca d&#39;água.
* Você pode alterar o tamanho máximo do arquivo PDF que deseja usar como elemento de marca d&#39;água. No entanto, documentos PDF grandes usados como marcas d&#39;água degradam o desempenho durante a sincronização offline de documentos aplicados com essas marcas d&#39;água. Consulte [Alterar os parâmetros de configuração da marca d&#39;água](configuring-client-server-options.md#change-the-watermark-configuration-parameters).
* Somente a primeira página do PDF selecionado é usada como marca d&#39;água. Certifique-se de que as informações que deseja exibir como marca d&#39;água estejam disponíveis na primeira página.
* Mesmo que seja possível especificar o dimensionamento do documento PDF, considere o tamanho e o layout da página do PDF se planeja usá-lo como uma marca d&#39;água no cabeçalho, no rodapé ou nas margens.
* Ao especificar o nome da fonte, insira o nome corretamente. AEM formulários substitui a fonte especificada se ela não estiver presente na máquina cliente em que o documento é aberto.
* Se você selecionou o texto como o conteúdo da marca d&#39;água, especificar a opção de dimensionamento como Ajustar à página não funcionará para páginas com largura diferente.
* Ao especificar o posicionamento dos elementos de marca d&#39;água, verifique se não há mais de um elemento com o mesmo posicionamento. Se dois elementos de marca d&#39;água tiverem o mesmo posicionamento, como centro, eles aparecerão sobrepostos no documento e na ordem em que foram adicionados à marca d&#39;água.
* Ao especificar o tamanho e o tipo da fonte, verifique se o comprimento do texto está completamente visível na página. O conteúdo do texto é colocado em novas linhas, de modo que o conteúdo da marca d&#39;água que você pretendia estar presente nas margens pode se sobrepor às áreas de conteúdo nas páginas. No entanto, se o documento for aberto no Acrobat 9, o texto além da única linha será truncado.

### Limitações das marcas d&#39;água dinâmicas {#limitations-of-dynamic-watermarks}

Alguns aplicativos clientes podem não ser compatíveis com marcas d&#39;água dinâmicas. Consulte a Ajuda apropriada das extensões do Acrobat Reader DC. Além disso, lembre-se das versões do Acrobat compatíveis com marcas d&#39;água dinâmicas:

* Não é possível usar um documento PDF protegido por senha como elemento de marca d&#39;água.
* As versões Acrobat e Adobe Reader anteriores à versão 10 não são compatíveis com os seguintes recursos de marca d&#39;água:

   * Marcas d&#39;água do PDF
   * Vários elementos na marca d&#39;água (Texto/PDF)
   * Opções avançadas, como intervalo de páginas, ou opções de exibição
   * Opções de formatação de texto, como fonte especificada, nome da fonte e cor. No entanto, versões anteriores do Acrobat e do Reader exibirão o conteúdo do texto na fonte e na cor padrão.

* Acrobat 9.0 e versões anteriores: Acrobat 9.0 e anterior não são compatíveis com nomes de políticas em marcas d&#39;água dinâmicas. Se o Acrobat 9.0 abrir um documento protegido por política com uma marca d&#39;água dinâmica que inclua um nome de política e outros dados dinâmicos, a marca d&#39;água será exibida sem o nome da política. Se a marca d&#39;água dinâmica incluir apenas o nome da política, o Acrobat exibirá uma mensagem de erro

### Adicionar um modelo dinâmico de marca d&#39;água {#add-a-dynamic-watermark-template}

É possível criar modelos dinâmicos de marcas d&#39;água. Esses modelos permanecem disponíveis como uma opção de configuração para políticas criadas por administradores ou usuários.

>[!NOTE]
>
>As informações de configuração de marcas d&#39;água dinâmicas não são capturadas com as outras informações de configuração ao exportar um arquivo de configuração.

1. No console de administração, clique em Serviços > Segurança de documento > Configuração > Marcas d&#39;água.
1. Clique em Novo.
1. Na caixa Nome, digite um nome para a nova marca d&#39;água.

   ***observação **: Não é possível usar alguns caracteres especiais nos nomes ou descrições de marcas d&#39;água ou elementos de marcas d&#39;água. Consulte as restrições listadas em [Considerações para editar políticas](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies).*

1. Em Nome, ao lado do sinal de mais, insira um nome significativo no elemento da marca d&#39;água, como Cabeçalho, e adicione uma descrição e expanda o sinal de mais para exibir as opções.
1. Em Origem, selecione o tipo de marca d&#39;água como Texto ou PDF.
1. Se você selecionou Texto, faça o seguinte:

   * Selecione os tipos de marcas d&#39;água a serem incluídos. Se você selecionar Texto personalizado, na caixa adjacente, digite o texto a ser exibido para a marca d&#39;água. Lembre-se do comprimento do texto que será exibido como marca d&#39;água.
   * Especifique as propriedades de formatação do texto, como nome da fonte, tamanho da fonte, cor do primeiro plano e cor do plano de fundo para o conteúdo do texto da marca d&#39;água. Especifique a cor do primeiro plano e do plano de fundo como valores hexadecimais.

      ***observação **: Se você selecionar a opção de dimensionamento como Ajustar à página, a propriedade de tamanho da fonte não estará disponível para edição.*

1. Se você selecionou PDF para opções de marcas d&#39;água avançadas, clique em **Procurar** ao lado de Selecionar PDF de marca d&#39;água para selecionar o documento PDF que deseja usar como marca d&#39;água.

   ***observação **: Não use um documento PDF protegido por senha. Se você especificar um PDF protegido por senha como elemento de marca d&#39;água, a marca d&#39;água não será aplicada.*

1. Em Usar Como Plano de Fundo, selecione Sim ou Não.

   **observação**: Atualmente, a marca d&#39;água aparece em primeiro plano independentemente dessa configuração.

1. Para controlar onde a marca d&#39;água é exibida no documento, configure as opções Alinhamento vertical e Alinhamento horizontal .
1. Selecione Ajustar à página ou selecione % e digite uma porcentagem na caixa. O valor deve ser um número inteiro, não uma fração. Para configurar o tamanho da marca d&#39;água, você pode usar um valor que seja a porcentagem da página ou definir a marca d&#39;água para ajustá-la ao tamanho da página.
1. Na caixa Rotação, digite os graus pelos quais deseja girar a marca d&#39;água. O intervalo é de -180 a 180. Use um valor negativo para girar a marca d&#39;água no sentido anti-horário. O valor deve ser um número inteiro, não uma fração.
1. Na caixa Opacidade, digite uma porcentagem. Use um número inteiro, não uma fração.
1. Em Opções avançadas, defina o seguinte:

   **Opções de intervalo de páginas**

   Defina o intervalo de páginas no qual a marca d&#39;água deve ser exibida. Insira a página inicial como 1 e a página final como -1 para ter todas as páginas marcadas com a marca d&#39;água.

   **Opções de exibição**

   Selecione onde deseja que a marca d&#39;água apareça. Por padrão, a marca d&#39;água aparece tanto em cópia suave (online) quanto em cópia impressa (impressa).

1. Clique em **Novo** em Elementos de marca d&#39;água para adicionar mais elementos de marca d&#39;água, se necessário.
1. Clique em OK.

### Editar um modelo dinâmico de marca d&#39;água {#edit-a-dynamic-watermark-template}

1. No console de administração, clique em Serviços > segurança do documento > Configuração > Marcas d&#39;água.
1. Clique na marca d&#39;água apropriada na lista.
1. Na página Editar marcas d&#39;água, altere as configurações conforme necessário.
1. Clique em OK.

### Excluir um modelo dinâmico de marca d&#39;água {#delete-a-dynamic-watermark-template}

Ao excluir uma marca d&#39;água dinâmica, ela não estará mais disponível para adicionar a uma nova política. No entanto, a marca d&#39;água permanece nas políticas existentes que a utilizam no momento e os documentos protegidos atualmente pela política continuam mostrando a marca d&#39;água dinâmica até que você ou um usuário edite a política que contém a marca d&#39;água excluída. Depois que a política é editada, a marca d&#39;água não é mais aplicada. Uma mensagem é exibida, indicando que a marca d&#39;água existente está excluída da política e que o usuário pode selecionar outra para substituí-la.

1. No console de administração, clique em Serviços > Segurança de documento > Configuração > Marcas d&#39;água.
1. Marque a caixa de seleção ao lado da marca d&#39;água apropriada e clique em Excluir.
1. Clique em OK.

## Configurar o registro de usuário convidado {#configuring-invited-user-registration}

Os usuários externos à sua organização podem se registrar na segurança do documento. Os usuários convidados que se registram e ativam suas contas podem fazer logon na segurança do documento usando seu endereço de email e a senha que criam quando se registram. Os usuários convidados registrados podem usar documentos protegidos por políticas para os quais tenham permissões.

Quando usuários convidados são ativados, eles se tornam usuários locais. Os usuários locais podem ser configurados e gerenciados usando a área Usuários locais e convidados . (Consulte [Gerenciamento de contas de usuário convidadas e locais](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts).)

Dependendo dos recursos que você ativar para usuários convidados, eles também poderão usar esses recursos de segurança de documentos:

* Aplicar políticas a documentos
* Criar políticas
* Adicionar usuários convidados às políticas

A segurança do documento gera automaticamente um email de convite de registro quando os seguintes eventos ocorrem, a menos que o usuário já esteja no diretório LDAP de origem ou tenha sido convidado anteriormente para se registrar:

* Um usuário existente adiciona um usuário convidado a uma política
* Um administrador adiciona uma conta de usuário convidada na página Registro de usuário convidado

O email de registro contém um link para uma página Registro e informações sobre como se registrar. Depois que o usuário convidado se registra, a segurança do documento emite um email de ativação com um link para uma página de Ativação. Quando ativada, a conta permanece válida até que você a desative ou exclua.

Se você habilitar o registro integrado, especifique seu servidor SMTP, detalhes do email de registro, recursos de acesso e redefinir informações do email de senha apenas uma vez. Antes de habilitar o registro interno, verifique se você criou um domínio local no Gerenciamento de usuários atribuiu a função &quot;Usuário do convidado de segurança de documentos&quot; aos usuários e grupos apropriados em sua organização. (Consulte [Adicionar um domínio local](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) e [Criar e configurar funções](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).) Se você não usar o registro integrado, deverá ter seu próprio sistema de registro do usuário criado usando o SDK dos formulários AEM. Consulte a ajuda em &quot;Desenvolvimento de SPIs para formulários AEM&quot; em [Programação com formulários AEM](https://www.adobe.com/go/learn-aemforms-programming-63). Se você não usar a opção Registro integrado , é recomendável configurar uma mensagem no email de ativação e na tela de logon do cliente para notificar os usuários sobre como entrar em contato com o administrador para obter uma nova senha ou outras informações.

**Habilitar e configurar o registro de usuário convidado**

Por padrão, o processo de registro do usuário convidado é desativado. Você pode ativar e desativar o registro de usuário convidado para segurança de documento, conforme necessário.

1. No console de administração, clique em Serviços > segurança do documento > Configuração > Registro do usuário convidado.
1. Selecione Habilitar Registro de Usuário Convidado.
1. (Opcional) Atualize as configurações de registro do usuário convidado conforme necessário:

   * [Excluir ou incluir um usuário ou grupo externo](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [Parâmetros da conta de registro e servidor](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [Configurações de email do convite de registro](configuring-client-server-options.md#registration-invitation-email-settings)
   * [Configurações de email de ativação](configuring-client-server-options.md#activation-email-settings)
   * [Configurar um email de redefinição de senha](configuring-client-server-options.md#configure-a-password-reset-email)

1. (Opcional) Em Registro integrado, selecione Sim para ativar essa opção. Se você não ativar o registro integrado, deverá configurar seu próprio sistema de registro de usuário.
1. Clique em OK.

### Excluir ou incluir um usuário ou grupo externo {#exclude-or-include-an-external-user-or-group}

Você pode restringir o registro com a segurança do documento para determinados usuários externos ou grupos de usuários. Essa opção é útil, por exemplo, para permitir o acesso a um determinado grupo de usuários, mas excluir indivíduos específicos que fazem parte do grupo.

As configurações a seguir estão localizadas na área Filtro de restrição de email da página Registro de usuário convidado .

**Exclusão:** digite o endereço de email de um usuário ou grupo a ser excluído. Para excluir vários usuários ou grupos, digite cada endereço de email em uma nova linha. Para excluir todos os usuários que pertencem a um domínio específico, insira um curinga e o nome do domínio. Por exemplo, para excluir todos os usuários no domínio example.com, digite &amp;ast;.example.com.

**Inclusão:** digite o endereço de email de um usuário ou grupo a ser incluído. Para incluir vários usuários ou grupos, digite cada endereço de email em uma nova linha. Para incluir todos os usuários que pertencem a um domínio específico, insira um curinga e o nome do domínio. Por exemplo, para incluir todos os usuários no domínio example.com, digite &amp;ast;.example.com.

### Parâmetros da conta de registro e servidor {#server-and-registration-account-parameters}

As configurações a seguir estão localizadas na área Configurações gerais da página Registro de usuário convidado .

**Host SMTP:** o nome do host do servidor SMTP. O servidor SMTP gerencia os avisos de email de saída para registrar e ativar contas de usuário convidadas.

Se exigido pelo seu host SMTP, digite as informações necessárias nas caixas Nome da Conta do Servidor SMTP e Senha da Conta do Servidor SMTP para se conectar ao servidor SMTP. Algumas organizações não impõem esse requisito. Se precisar de informações, consulte o administrador do sistema.

**Nome da classe do soquete do servidor SMTP:** Nome da classe do soquete para o servidor SMTP. Por exemplo, javax.net.ssl.SSLSocketFactory.

**Tipo de conteúdo de email:** Tipo MIME aceito, como text/plain ou text/html.

**Codificação de email:** formato de codificação a ser usado ao enviar mensagens de email. É possível especificar qualquer codificação, por exemplo, UTF-8 para Unicode ou ISO-8859-1 para Latim. O padrão é UTF-8.

**Redirecionar endereço de email:** ao especificar um endereço de email para essa configuração, qualquer novo convite será enviado para o endereço fornecido. Essa configuração pode ser útil para fins de teste.

**Usar domínios locais:** selecione o domínio apropriado. Em uma nova instalação, certifique-se de ter criado o domínio usando o Gerenciamento de usuários. Se for uma atualização, um domínio de usuário externo foi criado durante a atualização e pode ser usado.

**Usar SSL para servidor SMTP:** selecione essa opção para habilitar o SSL para o servidor SMTP.

**Exibir link de logon na página de registro:** exibe um link de logon na página de registro exibida para usuários convidados.

**Para ativar a Segurança da Camada de Transporte (TLS) para o servidor SMTP**

1. Abra o console de administração.

   O local padrão do Console de administração é `https://<server>:<port>/adminui`.

1. Navegue até Início > Serviços > Segurança de documento > Configuração > Registro de usuário convidado.
1. No Registro de Usuário Convidado, especifique todas as configurações e clique em OK.

   >[!NOTE]
   >
   >Se estiver usando o Microsoft Office 365 como o servidor SMTP para enviar os convites para registro de usuário, use as seguintes configurações:
   >
   >**Host SMTP:** smtp.office365.com
   >**Porta:** 587

1. Em seguida, é necessário atualizar o config.xml. Consulte [Configuração para habilitar o SMTP para TLS (Transport Layer Security)](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>Se você fizer alterações nas opções de Registro de usuário convidado , o arquivo config.xml será substituído e o TLS será desativado. Se você substituir as alterações, precisará executar a etapa acima para reativar o suporte TLS para o Registro de usuário convidado.

### Configurações de email do convite de registro {#registration-invitation-email-settings}

A segurança de documentos emite automaticamente um email de convite de registro quando você cria uma nova conta de usuário convidada ou quando um usuário existente adiciona um recipient externo que não se registrou ou foi convidado a se registrar em uma política. O email contém um link que o recipient pode usar para acessar a página de registro e inserir informações de conta pessoal, incluindo nome de usuário e senha. A senha pode ser qualquer combinação de oito caracteres.

Quando o recipient ativa a conta, o usuário se torna um usuário local.

As configurações a seguir estão localizadas na área Configuração de email de convite da página Registro de usuário convidado .

**De:** o endereço de email para onde o email de convite é enviado. O formato padrão do endereço de email De é postmaster@[your_installation_domain].com.

**Assunto:** Assunto padrão para a mensagem de email do convite.

**Tempo limite:** o número de dias após o qual o convite de registro expira se o usuário externo não se registrar. O valor padrão é de 30 dias.

**Mensagem:** O texto que aparece no corpo da mensagem convidando o usuário a se registrar.

### Configurações de email de ativação {#activation-email-settings}

Depois que os usuários convidados se registram, a segurança do documento envia um email de ativação. O email de ativação contém um link para a página de ativação da conta, onde os usuários podem ativar sua conta. Quando as contas são ativadas, os usuários podem fazer logon na segurança do documento usando seu endereço de email e a senha que criaram ao se registrarem.

Quando o recipient ativa a conta de usuário, o usuário se torna um usuário local.

As configurações a seguir estão localizadas na área Configuração de email de ativação da página Registro de usuário convidado .

>[!NOTE]
>
>Também é recomendável configurar uma mensagem na tela de logon para avisar os usuários externos sobre como entrar em contato com o administrador para obter uma nova senha ou outras informações.

**De:** o endereço de email para onde o email de ativação é enviado. Esse endereço de email recebe avisos de delivery com falha do host de email do registrando e também quaisquer mensagens que o recipient enviar em resposta ao email de registro. O formato padrão do endereço de email De é postmaster@[your_installation_domain].com.

**Assunto:** Assunto padrão para a mensagem de email de ativação.

**Tempo limite:** o número de dias após o qual o convite de ativação expira se o usuário não ativar a conta. O valor padrão é de 30 dias.

**Mensagem:** O texto que aparece no corpo da mensagem é uma mensagem indicando que a conta de usuário do recipient precisa ser ativada. Você também pode incluir informações como entrar em contato com um administrador para obter uma nova senha.

### Configurar um email de redefinição de senha {#configure-a-password-reset-email}

Se você tiver que redefinir a senha de um usuário convidado, um email de confirmação será gerado e convidará o usuário a escolher uma nova senha. A senha de um usuário não pode ser determinada; se o usuário o esquecer, você deve redefini-lo.

As configurações a seguir estão localizadas na área Redefinir e-mail de senha da página Registro de usuário convidado .

**De:** o endereço de email para onde o email de redefinição de senha é enviado. O formato padrão do endereço de email De é postmaster@[your_installation_domain].com.

**Assunto:** Assunto padrão para a mensagem de email de redefinição.

**Mensagem:** o texto que aparece no corpo da mensagem é uma mensagem indicando que a senha externa do usuário do recipient é redefinida.

## Permitir que usuários e grupos criem políticas {#enable-users-and-groups-to-create-policies}

A página Configuração tem um link para a página Minhas políticas , onde você especifica quais usuários finais podem criar minhas políticas e quais usuários e grupos estão visíveis nos resultados da pesquisa. A página Minhas políticas tem duas guias:

**Guia Criar políticas:** use o para configurar permissões de usuário para criar políticas personalizadas.

**Guia Usuários e grupos visíveis:** use para controlar quais usuários e grupos estão visíveis nos resultados da pesquisa do usuário. O superusuário ou administrador de conjunto de políticas deve selecionar e adicionar domínios, criados no Gerenciamento de usuários, ao usuário e grupo visíveis para cada conjunto de políticas. Essa lista é visível para o coordenador do conjunto de políticas e é usada para colocar limites em quais domínios o coordenador do conjunto de políticas pode navegar ao escolher usuários para adicionar às políticas.

Antes de conceder aos usuários permissão para criar políticas personalizadas, considere o acesso ou o controle que você deseja que usuários individuais tenham. Além disso, considere como você deseja que seus usuários e grupos fiquem expostos ao torná-los visíveis para pesquisas.

### Especifique usuários e grupos que podem criar políticas {#specify-users-and-groups-who-can-create-policies}

Como administrador, especifique quais usuários e grupos podem criar políticas personalizadas. Essa permissão pode ser definida no nível do usuário e do grupo. A funcionalidade de pesquisa pesquisa pesquisa usuários e grupos no banco de dados do Gerenciamento de usuários.

1. No console de administração, clique em Serviços > Segurança de documentos > Configuração > Minhas políticas.
1. Na página Minhas políticas , clique na guia Criar políticas e em Adicionar usuários e grupos.
1. Na caixa Localizar, digite o nome de usuário ou endereço de email do usuário ou grupo que você está procurando. Se não tiver essas informações, deixe a caixa vazia. Você também pode digitar um nome parcial ou um endereço de email, como quando souber apenas as duas primeiras letras de um nome de usuário.
1. Na lista Uso, selecione os parâmetros de pesquisa Nome ou Email.
1. Na lista Tipo, selecione Grupo ou Usuário para restringir sua pesquisa.
1. Na lista Em, selecione o domínio a ser pesquisado. Se você não souber o domínio do usuário ou grupo, selecione Todos os domínios.
1. Na lista Exibição, especifique o número de resultados de pesquisa a serem exibidos por página e clique em Localizar.
1. Para adicionar usuários e grupos de Minhas políticas, marque a caixa de seleção de cada usuário e grupo a ser adicionado.
1. Clique em Adicionar e em OK.

Seus usuários e grupos selecionados agora têm permissão para criar políticas personalizadas.

### Remova a permissão de criação de políticas personalizadas de um usuário ou grupo {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. Na página de segurança do documento, clique em Configuração > Minhas políticas.
1. Na página Minhas políticas , clique na guia Criar políticas . Usuários e grupos com permissões para criar políticas personalizadas são exibidos.
1. Marque a caixa de seleção ao lado dos usuários e grupos a serem removidos dessa permissão.
1. Clique em Excluir e em OK.

### Especificar usuários e grupos que estão visíveis em pesquisas {#specify-users-and-groups-that-are-visible-in-searches}

Quando os usuários estão gerenciando suas políticas personalizadas, eles podem procurar usuários e grupos para adicioná-las às suas políticas. Você deve especificar os domínios a partir dos quais os usuários e grupos estarão visíveis nessas pesquisas.

1. Na página de segurança do documento, clique em Configuração > Minhas políticas.
1. Na página Minhas políticas , clique na guia Usuários e grupos visíveis .
1. Para tornar os usuários e grupos em um domínio visíveis, clique em Adicionar domínios, selecione os domínios e clique em Adicionar. Para remover um domínio, marque a caixa de seleção ao lado do nome do domínio e clique em Excluir.

## Editar manualmente o arquivo de configuração de segurança do documento {#manually-editing-the-document-security-configuration-file}

Você pode importar e exportar as informações de configuração armazenadas no banco de dados de segurança do documento. Por exemplo, você pode querer fazer uma cópia de backup das informações de configuração ao mover de um ambiente de preparo para um de produção, ou pode editar opções avançadas que só podem ser configuradas para editar esse arquivo.

Você pode fazer as seguintes alterações usando o arquivo de configuração:

[Exibir permissões CATIA ao criar e editar políticas](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[Especificar um período de tempo limite para sincronização offline](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[Negar serviços de segurança de documentos para aplicações específicas](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[Alterar os parâmetros de configuração da marca d&#39;água](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[Desabilitação de links externos](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>A importação do arquivo de configuração reconfigura seu sistema com base nas informações do arquivo. As exceções são a configuração de marca d&#39;água dinâmica e informações de eventos personalizados, que não são salvas com o arquivo de configuração exportado. Você deve configurar essas informações manualmente no novo sistema. Somente um administrador do sistema ou um consultor de serviços profissionais familiarizado com a segurança de documentos e o XML devem modificar o conteúdo de um arquivo de configuração, por exemplo, para reconfigurar uma configuração corrompida ou ajustar parâmetros para um determinado cenário de implantação corporativa.

**Exportar um arquivo de configuração**

1. No console de administração, clique em Serviços > segurança do documento 11 > Configuração > Configuração manual.
1. Clique em Exportar e salve o arquivo de configuração em outro local. O nome de arquivo padrão é config.xml.
1. Clique em OK.
1. Antes de alterar o arquivo de configuração, faça uma cópia de backup caso precise reverter.

**Importar um arquivo de configuração**

1. No console de administração, clique em Serviços > segurança do documento 11 > Configuração > Configuração manual.
1. Clique em Procurar para ir para o arquivo de configuração e clique em Importar. Não é possível digitar o caminho diretamente na caixa Nome do arquivo.
1. Clique em OK.

### Especificar um período de tempo limite para sincronização offline {#specify-a-timeout-period-for-offline-synchronization}

A segurança de documentos permite que os usuários abram e usem documentos protegidos quando não estiverem conectados ao servidor de segurança de documentos. O aplicativo cliente do usuário deve sincronizar regularmente com o servidor para manter os documentos válidos para uso offline. Na primeira vez que os usuários abrem um documento protegido, eles são solicitados a saber se o computador deve ser autorizado a executar a sincronização periódica do cliente.

Por padrão, a sincronização ocorre automaticamente a cada quatro horas e quando um usuário é conectado ao servidor de segurança do documento. Se o período offline de um documento expirar enquanto o usuário estiver offline, ele deverá se reconectar ao servidor para permitir que o aplicativo cliente sincronize com o servidor.

No arquivo de configuração de segurança do documento, você pode especificar a frequência padrão da sincronização automática em segundo plano. Essa configuração atua como o tempo limite padrão dos aplicativos do cliente, a menos que o cliente defina explicitamente seu próprio valor de tempo limite.

1. Exporte o arquivo de configuração de segurança do documento. (Consulte [Editar manualmente o arquivo de configuração de segurança do documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra o arquivo de configuração em um editor e localize o nó `PolicyServer` . Nesse nó, localize o nó `ServerSettings`.
1. No nó `ServerSettings`, adicione esta entrada e salve o arquivo:

   `<entry key="BackgroundSyncFrequency" value="`*time* `"/>`

   onde *time* é o número de segundos entre as sincronizações automáticas em segundo plano. Se você enviou esse valor para `0`, a sincronização sempre ocorre. O valor padrão é `14400` segundos (a cada quatro horas).

1. Importe o arquivo de configuração. (Consulte [Editar manualmente o arquivo de configuração de segurança do documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Negando serviços de segurança de documento para aplicativos específicos {#denying-document-security-services-for-specific-applications}

Você pode configurar a segurança de documentos para negar serviços a aplicativos que atendem a critérios específicos. Os critérios podem especificar um único atributo, como um nome de plataforma ou podem especificar vários conjuntos de atributos. Este recurso pode ajudá-lo a controlar as solicitações que a segurança do documento deve tratar. Estes são alguns aplicativos deste recurso:

* **Proteção de receita:** você pode negar acesso a qualquer aplicativo cliente que não suporte suas convenções de receita.
* **Compatibilidade de aplicativos:** alguns aplicativos podem ser incompatíveis com as políticas ou o comportamento do servidor de segurança de documentos.

Quando os aplicativos clientes tentam estabelecer um link com a segurança do documento, eles fornecem informações sobre o aplicativo, a versão e a plataforma. A segurança do documento compara essas informações com as configurações de Negações que obtém do arquivo de configuração de segurança do documento.

As configurações de Negações podem conter vários conjuntos de condições de negação. Se todos os atributos de qualquer conjunto corresponderem, o aplicativo solicitante terá acesso negado aos serviços de segurança do documento.

O recurso de negação de serviço requer que os aplicativos clientes usem a segurança de documento do SDK do cliente C++ versão 8.2 ou posterior. Os seguintes produtos de Adobe fornecem informações sobre produtos ao solicitar serviços de segurança de documento:

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard e posterior
* Adobe Reader 9.0 e posterior
* Extensões do Acrobat Reader DC para o Microsoft Office 8.2 e posterior

Os aplicativos clientes usam a API do cliente do SDK do cliente C++ de segurança de documento para solicitar serviços da segurança de documentos. As solicitações da API do cliente incluem informações da plataforma e da versão do SDK (pré-compiladas na API do cliente) e informações do produto obtidas do aplicativo do cliente.

Os aplicativos ou plug-ins do cliente fornecem informações do produto na implementação de uma função de retorno de chamada. O pedido contém as seguintes informações:

* Nome do integrador
* Versão do integrador
* Família de aplicativos
* Nome do aplicativo
* Versão do aplicativo

Se alguma informação não for aplicável, o aplicativo cliente deixará o campo correspondente em branco.

Vários aplicativos do Adobe incluem informações do produto ao solicitar serviços de segurança de documento, incluindo extensões Acrobat, Adobe Reader e Acrobat Reader DC para Microsoft Office.

**Acrobat e Adobe Reader**

Quando a Acrobat ou a Adobe Reader solicita um serviço da segurança do documento, ele fornece as seguintes informações do produto:

* **Integrador:** Adobe Systems, Inc.
* **Versão do integrador:** 1.0
* **Família de aplicativos:** Acrobat
* **Nome do aplicativo:** Acrobat
* **Versão do aplicativo:** 9.0.0

**Extensões do Acrobat Reader DC para o Microsoft Office**

O Acrobat Reader DC Extensions for Microsoft Office é um plug-in usado com os produtos Microsoft Office Microsoft Word, Microsoft Excel e Microsoft PowerPoint. Ao solicitar um serviço, ele fornece as seguintes informações:

* **Integrador:** Adobe Systems Incorporated
* **Versão do integrador:** 8.2
* **Família de aplicativos:** extensões do Acrobat Reader DC para Microsoft Office
* **Nome do aplicativo:** Microsoft Word, Microsoft Excel ou Microsoft PowerPoint
* **Versão do aplicativo:** 2003 ou 2007

**Configurar a segurança do documento para negar serviços para aplicativos específicos**

1. Exporte o arquivo de configuração de segurança do documento. (Consulte [Editar manualmente o arquivo de configuração de segurança do documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra o arquivo de configuração em um editor e localize o nó `PolicyServer` . Adicione um nó `ClientVersionRules` como um filho imediato do nó `PolicyServer`, se esse nó não existir:

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
   * Apple OS X
   * Sun Solaris
   * HP-UX

   `SDKVersions` especifica a versão da API do cliente C++ de segurança do documento usada pelo aplicativo cliente. Por exemplo, `"8.2"`.

   `APPFamilies` é definida pela API do cliente.

   `AppName`especifica o nome do aplicativo cliente. Vírgulas são usadas como separadores de nome. Para incluir uma vírgula em um nome, saia dela com um caractere de barra invertida (\). Por exemplo, *&quot;Adobe Systems\, Inc.&quot;*.

   `AppVersions` especifica a versão do aplicativo cliente.

   `Integrators` especifica o nome da empresa ou grupo que desenvolveu o plug-in ou o aplicativo integrado.

   `IntegratorVersions` é a versão do plug-in ou do aplicativo integrado.

1. Para cada conjunto adicional de dados de negação, adicione outro elemento *MyEntryName*.
1. Salve o arquivo de configuração.
1. Importe o arquivo de configuração. (Consulte [Editar manualmente o arquivo de configuração de segurança do documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

**Exemplos**

Neste exemplo, todos os clientes do Windows têm acesso negado.

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

Neste exemplo, o acesso a My Application version 3.0 e My Other Application version 2.0 é negado. O mesmo URL de informações de negação é usado independentemente do motivo da negação.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value=”https://get.a.new/version.html”/>
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

Neste exemplo, todas as solicitações de uma instalação do Microsoft PowerPoint 2007 ou do Microsoft PowerPoint 2010 de extensões do Acrobat Reader DC para Microsoft Office são negadas.

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value=”https://get.a.new/version.html”/>
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

Por padrão, é possível especificar no máximo cinco elementos em uma marca d&#39;água. Além disso, o tamanho máximo de arquivo do documento PDF que você deseja usar como marca d&#39;água é limitado a 100 KB. Você pode alterar esses parâmetros no arquivo config.xml.

***observação **: Você deve alterar esses parâmetros com cuidado.*

1. Exporte o arquivo de configuração de segurança do documento. (Consulte [Editar manualmente o arquivo de configuração de segurança do documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra o arquivo de configuração em um editor e localize o nó `ServerSettings` .
1. No nó `ServerSettings`, adicione as seguintes entradas e salve o arquivo: `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   A primeira entrada, *max file size* é o tamanho máximo de arquivo (em KB) permitido para um elemento de marca d&#39;água PDF. O padrão é 100KB.

   A segunda entrada, *max elements* é o número máximo de elementos permitidos em uma marca d&#39;água. O padrão é 5.

   ```xml
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. Importe o arquivo de configuração. (Consulte [Editar manualmente o arquivo de configuração de segurança do documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Desabilitação de links externos {#disabling-external-links}

Muitos usuários de segurança de documentos não têm acesso a links externos, como **www.adobe.com** enquanto usam interfaces de usuário de Gerenciamento de Direitos:

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`.

As seguintes alterações no config.xml desabilitam todos os links externos das interfaces de usuário do Gerenciamento de Direitos.

1. Exporte o arquivo de configuração de segurança do documento. (Consulte [Editar manualmente o arquivo de configuração de segurança do documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra o arquivo de configuração em um editor e localize o nó `DisplaySettings` .
1. Para desativar todos os links externos, no nó `DisplaySettings`, adicione a seguinte entrada e salve o arquivo: `<entry key="ExternalLinksAllowed" value="false"/>`

   ```xml
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. Importe o arquivo de configuração. (Consulte [Editar manualmente o arquivo de configuração de segurança do documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Configuração para habilitar o SMTP para TLS {#configuration-to-enable-smtp-for-transport-layer-security-tls}

As seguintes alterações no config.xml habilitam o suporte TLS para o recurso Registro de usuário convidado .

1. Exporte o arquivo de configuração de segurança do documento. (Consulte [Editar manualmente o arquivo de configuração de segurança do documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra o arquivo de configuração em um editor e localize o nó `DisplaySettings` .
1. Localize o seguinte nó: `<node name="ExternalUser">`

   ```xml
   <node name="ExternalUser">
   ```

1. Defina o valor da chave `SmtpUseTls` no nó `ExternalUser` para **true**.
1. Defina o valor da chave `SmtpUseSsl` no nó `ExternalUser` para **false**.
1. Salve o `config.xml`.
1. Importe o arquivo de configuração. (Consulte [Editar manualmente o arquivo de configuração de segurança do documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Desative pontos de extremidade SOAP para documentos de segurança de documento {#disable-soap-endpoints-for-document-security-documents}

As alterações a seguir no config.xml para desabilitar pontos de extremidade SOAP para documentos de segurança de documentos.

1. Exporte o arquivo de configuração de segurança do documento. (Consulte [Editar manualmente o arquivo de configuração de segurança do documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra o arquivo de configuração em um editor e localize o seguinte nó: `<node name="DRM">`

   ```xml
   <node name="DRM">
   ```

1. No nó DRM, localize o nó `entry`:

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. Para desativar pontos de extremidade SOAP para documentos de segurança de documento, defina o atributo de valor como **false**.

   ```xml
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. Salve o `config.xml`.
1. Importe o arquivo de configuração. (Consulte [Editar manualmente o arquivo de configuração de segurança do documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### Aumento da escalabilidade do servidor de segurança de documentos {#increasingscalability}

Por padrão, ao sincronizar um documento para uso offline, juntamente com as informações do documento atual, os clientes de segurança do documento buscam políticas, marcas d&#39;água, licenças e atualizações de revogação para todos os outros documentos aos quais o usuário tem acesso. Se essas atualizações e informações não forem sincronizadas com o cliente, um documento aberto no modo offline ainda poderá ser aberto com informações de política, marca d&#39;água e revogação mais antigas.

Você pode aumentar a escalabilidade do servidor de segurança de documentos limitando as informações enviadas ao cliente. A redução na quantidade de informações enviadas ao cliente resulta em melhor escalabilidade, menos tempo de resposta e melhor desempenho do servidor. Execute as seguintes etapas para aumentar a escalabilidade:

1. Exporte o arquivo de configuração de segurança do documento. (Consulte [Editar manualmente o arquivo de configuração de segurança do documento](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. Abra o arquivo de configuração em um editor e localize o nó ServerSettings .
1. No nó ServerSettings, defina o valor da propriedade `DisableGlobalOfflineSynchronizationData`como `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   Quando definido como true, o servidor de segurança do documento envia informações somente para o documento atual e as informações para o restante dos documentos (os outros documentos aos quais um usuário tem acesso) não são enviadas ao cliente.

   >[!NOTE]
   >
   >Por padrão, o valor da chave `DisableGlobalOfflineSynchronizationData`está definido como `false`.

1. Salve e importe o arquivo de configuração. (Consulte [Editar manualmente o arquivo de configuração de segurança do documento](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

