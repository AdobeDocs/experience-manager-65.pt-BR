---
title: Configuração das opções de cliente e servidor
seo-title: Configuração de opções de cliente e servidor
description: Saiba como configurar as várias opções de cliente e servidor, como configurações do servidor, funções de segurança do documento e auditoria do evento.
seo-description: Saiba como configurar as várias opções de cliente e servidor, como configurações do servidor, funções de segurança do documento e auditoria do evento.
uuid: 1f9f9886-726e-4fad-9ff8-0ff11eef653e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0f069fbc-10c2-403e-9419-5e9920035d75
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '10273'
ht-degree: 0%

---


# Configurar o servidor de segurança do documento {#configure-the-document-security-server}

1. No console de administração, clique em Serviços > Segurança do documento > Configuração > Configuração do servidor.
1. Configure as configurações e clique em OK.

## Configurações do servidor {#server-configuration-settings}

**URL de base:** O URL de segurança do documento base, que contém o nome do servidor e a porta. As informações anexadas à base criam URLs de conexão. Por exemplo, /edc/Main.do é anexado para acessar as páginas da Web. Os usuários também respondem a convites externos de registro de usuário por meio desse URL.

Se você estiver usando o IPv6, insira o URL básico como o nome do computador ou o nome DNS. Se você usar um endereço IP numérico, o Acrobat não abrirá os arquivos protegidos por política. Além disso, use o URL protegido por HTTP (HTTPS) para seu servidor.

>[!NOTE]
>
>O URL base é incorporado em arquivos protegidos por política. Os aplicativos cliente usam o URL básico para se conectar novamente ao servidor. Os arquivos protegidos continuarão a conter o URL base, mesmo se for alterado posteriormente. Se você alterar o URL base, as informações de configuração precisarão ser atualizadas para todos os clientes conectados.

**Período Padrão de Concessão Offline:** O tempo padrão durante o qual um usuário pode usar um documento protegido offline. Essa configuração determina o valor inicial da configuração do período de empréstimo Offline Automática ao criar uma política. (Consulte Criar e editar políticas.) Quando o período de empréstimo expirar, o recipient deverá sincronizar o documento novamente para continuar a usá-lo.

Para obter uma discussão sobre como a concessão e sincronização offline funcionam, consulte [Primer sobre como configurar a concessão e sincronização](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html)offline.

**Período de sincronização offline padrão:** O tempo máximo que qualquer documento pode ser usado offline a partir do momento em que é protegido pela primeira vez.

**Tempo limite da sessão do cliente:** A duração, em minutos, após a qual a segurança do documento se desconecta se um usuário que está conectado por meio de um aplicativo cliente não interagir com a segurança do documento.

**Permitir acesso de usuários anônimos:** Selecione essa opção para permitir a criação de políticas compartilhadas e pessoais que permitam que usuários anônimos abram documentos protegidos por política. (Os usuários que não têm contas podem acessar o documento, mas não podem fazer logon na segurança do documento ou usar outros documentos protegidos por política.)

**Desabilitar acesso aos clientes da versão 7:** Especifica se os usuários podem usar o Acrobat ou o Reader 7.0 para se conectar ao servidor. Quando essa opção é selecionada, os usuários devem usar o Acrobat ou o Reader 8.0 e posterior para concluir as operações de segurança do documento em documentos PDF. Se as políticas exigirem que o Acrobat ou o Reader 8.0 e posterior sejam executados no modo certificado ao abrir documentos protegidos por política, você deverá desativar o acesso ao Acrobat ou ao Reader 7. (Consulte Especificar as permissões do documento para usuários e grupos.)

**Permitir acesso offline por documento** Selecione esta opção para especificar o acesso offline por documento. Se essa configuração estiver ativada, o usuário terá acesso offline somente aos documentos que o usuário tiver aberto online pelo menos uma vez.

**Permitir Autenticação de Senha de Nome de Usuário:** Selecione esta opção para permitir que os aplicativos clientes usem a autenticação de nome de usuário/senha ao se conectar ao servidor.

**Permitir autenticação Kerberos:** Selecione essa opção para permitir que os aplicativos clientes usem a autenticação Kerberos ao se conectar ao servidor.

**Permitir Autenticação de Certificado de Cliente:** Selecione esta opção para permitir que os aplicativos clientes usem autenticação de certificado ao se conectar ao servidor.

**Permitir Autenticação** Estendida Selecione para habilitar a autenticação estendida e insira o URL de Aterrissagem da Autenticação Estendida.

A seleção dessa opção permite que os aplicativos clientes usem autenticação estendida. A autenticação estendida fornece processos de autenticação personalizados e diferentes opções de autenticação configuradas no servidor de formulários AEM. Por exemplo, os usuários agora podem experimentar a autenticação baseada em SAML em vez do nome de usuário/senha dos formulários AEM, do Acrobat e do Reader Client. Por padrão, o URL de aterrissagem contém *localhost* como o nome do servidor. Substitua o nome do servidor por um nome de host totalmente qualificado. O nome do host no URL inicial é automaticamente preenchido a partir do URL base, se a Autenticação estendida ainda não estiver ativada. Consulte [Adicionar o provedor](configuring-client-server-options.md#add-the-extended-authentication-provider)de autenticação estendida.

***observação **: A autenticação estendida é compatível com o Apple Mac OS X com o Adobe Acrobat versão 11.0.6 e superior.*

**Largura de controle de HTML preferencial para autenticação** estendida Especifique a largura da caixa de diálogo de autenticação estendida que é aberta no Acrobat para inserir credenciais de usuário.

**Altura de controle de HTML preferencial para autenticação** estendida Especifique a altura da caixa de diálogo de autenticação estendida que é aberta no Acrobat para inserir as credenciais do usuário.

***observação **: Os limites de largura e altura dessa caixa de diálogo são os seguintes:*Largura: Mínimo = 400, máximo = 900

Altura: Mínimo = 450; máximo = 800

**Ativar Cache de Credenciais do Cliente:** Selecione essa opção para permitir que os usuários armazenem suas credenciais em cache (nome de usuário e senha). Quando as credenciais dos usuários são armazenadas em cache, eles não precisam digitar suas credenciais toda vez que abrirem um documento ou quando clicarem no botão Atualizar na página Gerenciar políticas de segurança do Adobe Acrobat. Você pode especificar o número de dias antes que os usuários forneçam suas credenciais novamente. Definir o número de dias como 0 permite que as credenciais sejam armazenadas em cache indefinidamente.

## Configuração de usuários e administradores da segurança do documento {#configuring-document-security-users-and-administrators}

### Atribuindo funções de segurança do documento a administradores {#assigning-document-security-roles-to-administrators}

Seu ambiente de formulários do AEM contém um ou mais usuários administradores que têm os privilégios adequados para criar usuários e grupos. Se sua organização estiver usando segurança de documento, pelo menos um administrador também deverá receber o privilégio de gerenciar usuários convidados e locais.

Os administradores também devem ter a função Usuário do console de administração para acessar o console de administração. (Consulte [Criação e configuração de funções](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

### Configuração de usuários e grupos visíveis {#configuring-visible-users-and-groups}

Para visualização de usuários e grupos em domínios selecionados durante pesquisas de usuários de políticas, um superadministrador ou administrador de conjuntos de políticas deve selecionar e adicionar domínios (criados no Gerenciamento de usuários) à lista visível de usuários e grupos para cada conjunto de políticas.

A lista visível de usuário e grupo está visível para o coordenador do conjunto de políticas e é usada para restringir quais domínios o usuário final pode navegar ao escolher usuários ou grupos para adicionar às políticas. Se essa tarefa não for executada, o coordenador do conjunto de políticas não encontrará nenhum usuário ou grupo a ser adicionado à política. Pode haver mais de um coordenador de conjunto de políticas para qualquer conjunto de políticas.

1. Depois de instalar e configurar o ambiente de formulários do AEM com segurança de documento, configure todos os domínios apropriados no Gerenciamento de usuários. <!-- Fix broken link (See Setting up and managing domains) -->

   ***observação **: A criação de domínios deve ser feita antes que qualquer política possa ser criada.*

1. No console de administração, clique em Serviços > Gerenciamento de Documentos > Políticas e, em seguida, clique na guia Conjuntos de políticas.
1. Selecione Conjunto de políticas global e clique na guia Usuários e grupos visíveis.
1. Clique em Adicionar domínio(s) e adicione domínios existentes conforme necessário.
1. Navegue até Serviços > Segurança do documento > Configuração > Minhas políticas e clique na guia Usuários e grupos visíveis.
1. Clique em Adicionar domínio(s) e adicione domínios existentes conforme necessário.

## Adicionar o provedor de autenticação estendida {#add-the-extended-authentication-provider}

Os formulários AEM fornecem uma configuração de amostra que você pode personalizar para seu ambiente. Execute as seguintes etapas:

>[!NOTE]
>
>A autenticação estendida é compatível com o Apple Mac OS X com o Adobe Acrobat versão 11.0.6 e superior.

1. Obtenha o arquivo WAR de amostra para implantá-lo. Consulte o guia de instalação apropriado para seu servidor de aplicativos.
1. Certifique-se de que o servidor de formulários tenha um nome totalmente qualificado, em vez de endereços IP, como o URL base e que seja um URL HTTPS. Consulte Configurações [do](configuring-client-server-options.md#server-configuration-settings)servidor.
1. Ative a Autenticação estendida na página Configuração do servidor. Consulte Configurações [do](configuring-client-server-options.md#server-configuration-settings)servidor.
1. Adicione os URLs de redirecionamento SSO necessários no arquivo de configuração do Gerenciamento de usuários. Consulte [Adicionar URLs de redirecionamento SSO para autenticação](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication)estendida.

### Adicionar URLs de redirecionamento SSO para autenticação estendida {#add-sso-redirect-urls-for-extended-authentication}

Com a autenticação estendida ativada, os usuários que abrem um documento protegido por política no Acrobat XI ou no Reader XI recebem uma caixa de diálogo para autenticação. Essa caixa de diálogo carrega a página HTML que você especificou como o URL inicial de autenticação estendida nas configurações do servidor de segurança do documento. Consulte Configurações [do](configuring-client-server-options.md#server-configuration-settings)servidor.

>[!NOTE]
>
>A autenticação estendida é compatível com o Apple Mac OS X com o Adobe Acrobat versão 11.0.6 e superior.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração.
1. Clique em Exportar e salve o arquivo de configuração no disco.
1. Abra o arquivo em um editor e localize o nó AllowedUrls.
1. No `AllowedUrls` nó, adicione as seguintes linhas: `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. Salve o arquivo e importe o arquivo atualizado da página Configuração manual: No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração.

## Configuração da segurança offline {#configuring-offline-security}

A segurança do documento fornece a capacidade de usar documentos offline protegidos por política sem uma conexão com a Internet ou a rede. Esse recurso exige que a política permita acesso offline, conforme descrito em [Especificar as permissões de documento para usuários e grupos](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). Antes que um documento que tenha tal política possa ser usado offline, o recipient deve abrir o documento enquanto estiver online e habilitar o acesso offline, clicando em Sim quando solicitado. O recipient pode igualmente ser convidado a autenticar a sua identidade. O recipient pode usar documentos off-line durante o período de empréstimo off-line especificado na política.

Quando o período de empréstimo offline terminar, o recipient deverá sincronizar novamente com a segurança do documento abrindo um documento online ou usando um comando de menu de extensões do Acrobat ou do Acrobat Reader DC para sincronizar. (Consulte a Ajuda *do* Acrobat ou a Ajuda *das extensões apropriadas do* Acrobat Reader DC.)

Como os documentos que permitem acesso offline exigem material de chave em cache no computador onde os arquivos são armazenados offline, o arquivo pode ser comprometido se um usuário não autorizado puder obter o material de chave. Para compensar essa possibilidade, são fornecidas opções de sobreposição de chaves programadas e manuais que podem ser configuradas para impedir que pessoas não autorizadas usem a chave para acessar o documento.

### Definir um período padrão de empréstimo offline {#set-a-default-offline-lease-period}

Recipient de documentos protegidos por política podem colocar os documentos offline pelo número de dias especificado na política. Depois de sincronizar inicialmente o documento com a segurança do documento, o recipient pode usá-lo offline até que o período de empréstimo offline expire. Quando o período de empréstimo expira, o recipient deve colocar o documento online e fazer logon para sincronizar com a segurança do documento para continuar usando o documento.

Você pode configurar um período padrão de empréstimo offline. O período de empréstimo pode ser alterado a partir do padrão quando qualquer pessoa cria ou edita uma política.

1. Na página Segurança do documento, clique em Configuração > Configuração do servidor.
1. Na caixa Período de concessão offline padrão, digite o número de dias para o período de empréstimo offline.
1. Clique em OK.

### Gerenciar sobreposições de chave {#manage-key-rollovers}

A segurança do Documento usa algoritmos de criptografia e licenças para proteger documentos. Quando criptografa um documento, a segurança do documento gera e gerencia uma chave de descriptografia chamada *DocKey* que é transmitida para o aplicativo cliente. Se a política que protege um documento permitir acesso offline, uma chave offline chamada chave ** principal também será gerada para cada usuário que tiver acesso offline ao documento.

>[!NOTE]
>
>Se uma chave principal não existir, a segurança do documento gerará uma para proteger um documento.

Para abrir um documento offline protegido por política, o computador do usuário deve ter a chave principal apropriada. O computador obtém a chave principal quando o usuário sincroniza com a segurança do documento (abre um documento protegido on-line). Se essa chave principal estiver comprometida, qualquer documento ao qual o usuário tiver acesso offline também poderá estar comprometido.

Uma maneira de diminuir a ameaça aos documentos offline é evitar permitir o acesso offline a documentos particularmente sensíveis. Outro método é passar periodicamente sobre as chaves principais. Quando a segurança do documento arrasta a tecla, qualquer chave existente não pode mais acessar os documentos protegidos por política. Por exemplo, se um autor de uma ação obtiver uma chave principal de um laptop roubado, essa chave não poderá ser usada para acessar os documentos protegidos depois que a sobreposição ocorrer. Se você suspeitar que uma chave principal específica foi comprometida, poderá rolar manualmente sobre a chave.

No entanto, você também precisa estar ciente de que uma sobreposição de chave afeta todas as chaves principais, não apenas uma. Também reduz a escalabilidade do sistema, pois os clientes devem armazenar mais chaves para acesso offline. A frequência de sobreposição de chave padrão é de 20 dias. É recomendável não definir esse valor em menos de 14 dias, pois as pessoas podem ser impedidas de visualizar documentos offline e o desempenho do sistema pode ser afetado.

No exemplo a seguir, Key1 é a mais antiga das duas chaves principais, e Key2 é a mais nova. Quando você clica no botão Chaves de rolagem agora na primeira vez, a Chave1 se torna inválida e uma chave principal (Chave3) mais nova e válida é gerada. Os usuários obterão o Key3 quando sincronizarem com a segurança do documento, normalmente abrindo um documento protegido on-line. No entanto, os usuários não são forçados a sincronizar com a segurança do documento até atingirem o período máximo de empréstimo offline especificado em uma política. Após a primeira sobreposição de chave, os usuários que permanecem offline ainda poderão abrir documentos offline, incluindo aqueles protegidos por Key3, até atingirem o período máximo de concessão offline. Quando você clica no botão Rollover Keys Now (Chaves de rolagem agora) uma segunda vez, Key2 se torna inválido e Key4 é criado. Os usuários que permanecerem off-line durante as duas sobreposições de chave não poderão abrir documentos protegidos com Key3 ou Key4 até que sincronizem com a segurança do documento.

**Alterar a frequência de sobreposição da chave**

Para fins de confidencialidade, quando você estiver usando documentos offline, a segurança do documento fornece uma opção automática de sobreposição de chave com um período de frequência padrão de 20 dias. Você pode alterar a frequência de sobreposição; no entanto, evite definir o valor em menos de 14 dias, pois as pessoas podem ser impedidas de visualizar documentos offline e o desempenho do sistema pode ser afetado.

1. Na página Segurança do documento, clique em Configuração > Gerenciamento de chaves.
1. Na caixa Frequência de sobreposição de chave, digite o número de dias para o período de sobreposição.
1. Clique em OK.

**Passe manualmente sobre as teclas principais**

Para manter a confidencialidade dos documentos offline, é possível rolar manualmente sobre as chaves principais. Você pode achar necessário rolar manualmente sobre uma tecla (por exemplo, se a chave estiver comprometida por alguém que a obtenha de um computador em que ela esteja armazenada em cache para permitir o acesso offline a um documento).

>[!NOTE]
>
>Evite usar frequentemente sobreposições manuais, pois isso faz com que todas as chaves principais sejam sobrepostas, não apenas uma, e pode impedir temporariamente que os usuários visualizem novos documentos offline.

As chaves principais devem ser revertidas duas vezes antes de as chaves existentes anteriormente nos computadores clientes serem invalidadas. Os computadores clientes que têm chaves principais invalidadas devem sincronizar novamente com o serviço de segurança do documento para adquirir as novas chaves principais.

1. Na página Segurança do documento, clique em Configuração > Gerenciamento de chaves.
1. Clique em Chaves de rolagem agora e em OK.
1. Aguarde aproximadamente 10 minutos. A seguinte mensagem de registro é exibida no log do servidor: `Done RightsManagement key rollover for`*N *`principals`. Onde* N *é o número de usuários no sistema de segurança do documento.
1. Clique em Chaves de rolagem agora e em OK.
1. Aguarde aproximadamente 10 minutos.

## Definição das configurações de auditoria e privacidade do evento {#configuring-event-auditing-and-privacy-settings}

A segurança do Documento pode auditar e registrar informações sobre eventos relacionados à interação com documentos, políticas, administradores e o servidor protegidos por política. Você pode configurar a auditoria de eventos e especificar os tipos de eventos para auditoria. Para auditar eventos de um determinado documento, a opção de auditoria da política também deve estar ativada.

Quando a auditoria estiver ativada, você poderá visualização os detalhes dos eventos auditados na página Eventos. Os usuários de segurança do documento também podem visualização eventos relacionados especificamente aos documentos protegidos por política que usam ou criam.

Você pode selecionar estes tipos de eventos para auditoria:

* eventos de documento protegidos por política, como tentativas de usuários autorizados ou não autorizados para abrir documentos
* eventos de políticas, como criação, alteração, exclusão, ativação e desativação de políticas
* eventos de usuários, como convites e registros externos de usuários, contas de usuários ativadas e desativadas, alterações em senhas de usuários e atualizações de perfis
* eventos de formulários AEM, como incompatibilidades de versão, servidor de diretórios indisponível e provedores de autorização, e alterações na configuração do servidor

### Ativar ou desativar a auditoria de eventos {#enable-or-disable-event-auditing}

Você pode ativar e desativar a auditoria de eventos relacionados ao servidor, documentos protegidos por política, políticas, conjuntos de políticas e usuários. Ao ativar a auditoria de eventos, você pode optar por auditar todos os eventos possíveis ou selecionar eventos específicos para auditoria.

Ao ativar a auditoria do servidor, você pode visualização os eventos auditados na página Eventos.

1. No console de administração, clique em Serviços > Segurança do Documento > Configuração > Configurações de auditoria e privacidade.
1. Para configurar a auditoria do servidor, em Ativar auditoria do servidor, selecione Sim ou Não.
1. Se você selecionou Sim, em cada categoria de evento, execute uma das ações a seguir para selecionar as opções a serem auditadas:

   * Para auditar todos os eventos na categoria, selecione Todos.
   * Para auditar apenas alguns eventos, desmarque Todas e marque as caixas de seleção ao lado dos eventos que deseja auditar.

      (Consulte Opções [de auditoria de](configuring-client-server-options.md#event-auditing-options)Eventos.)

1. Clique em OK.

>[!NOTE]
>
>Ao trabalhar com as páginas da Web, evite usar os botões do navegador, como o botão Voltar, o botão Atualizar e a seta para trás ou para frente, pois essa ação pode causar problemas indesejados de captura de dados e exibição de dados.

### Ativar ou desativar a notificação de privacidade {#enable-or-disable-privacy-notification}

Você pode ativar e desativar uma mensagem de notificação de privacidade. Quando você habilita a notificação de privacidade, uma mensagem é exibida quando um recipient tenta abrir um documento protegido por política. O aviso informa o usuário de que a utilização do documento está sendo auditada. Você também pode especificar um URL que o usuário pode usar para visualização na sua página de política de privacidade, se disponível.

1. No console de administração, clique em Serviços > Segurança do Documento > Configuração > Configurações de auditoria e privacidade.
1. Para configurar a notificação de privacidade, em Ativar aviso de privacidade, selecione Sim ou Não.

   Se a política anexada a um documento permitir o acesso anônimo do usuário e a opção Ativar aviso de privacidade estiver definida como Não, o usuário não será solicitado a fazer logon e a mensagem de notificação de privacidade não será exibida.

   Se a política anexada a um documento não permitir acesso anônimo, o usuário verá a mensagem de notificação de privacidade.

1. Se aplicável, na caixa URL de privacidade, digite o URL para a página da política de privacidade. Se a caixa URL de privacidade for deixada em branco, a página de privacidade do adobe.com será exibida.
1. Clique em OK.

>[!NOTE]
>
>Desativar o aviso de privacidade não desativa a auditoria de uso do documento. As ações de auditoria e as ações personalizadas que são suportadas por meio do rastreamento de uso estendido ainda podem coletar informações de comportamento do usuário.

### Importar um tipo de evento de auditoria personalizado {#import-a-custom-audit-event-type}

Se você estiver usando um aplicativo habilitado para segurança de documento que ofereça suporte à auditoria de eventos adicionais, como eventos específicos de um determinado tipo de arquivo, um parceiro da Adobe poderá fornecer eventos de auditoria personalizados que você pode importar para a segurança do documento. Use esse recurso somente se você tiver recebido tipos de evento personalizados por um parceiro da Adobe.

1. No console de administração, clique em Serviços > Segurança do Documento > Configuração > Gerenciamento de Eventos.
1. Clique em Procurar para ir até o arquivo XML a ser importado e clique em Importar.
1. A importação substitui tipos de evento de auditoria personalizados existentes no servidor se forem encontradas combinações idênticas de código de evento e namespace.
1. Clique em OK.

### Excluir um tipo de evento de auditoria personalizado {#delete-a-custom-audit-event-type}

1. No console de administração, clique em Serviços > Segurança do documento > Configuração > Gerenciamento de Eventos.
1. Marque a caixa de seleção ao lado do tipo de evento de auditoria personalizado a ser excluído e clique em Excluir.
1. Clique em OK.

### Exportar eventos de auditoria {#export-audit-events}

É possível exportar eventos de auditoria para um arquivo para fins de arquivamento.

1. No console de administração, clique em Serviços > Segurança do Documento > Configuração > Gerenciamento de Eventos.
1. Edite as configurações em Exportar Eventos de auditoria, conforme necessário. Você pode especificar:

   * a idade mínima dos eventos de auditoria para exportar
   * o número máximo de eventos de auditoria a serem incluídos em um único arquivo. O servidor gera um ou mais arquivos, com base nesse valor.
   * a pasta onde o arquivo será criado. Essa pasta está no servidor de formulários. Se o caminho da pasta for relativo, ele será relativo ao diretório raiz do servidor de aplicativos.
   * o prefixo de arquivo a ser usado para os arquivos de eventos de auditoria
   * o formato do arquivo, seja um arquivo CSV (valores separados por vírgula) compatível com o Microsoft Excel ou um arquivo XML.

1. Clique em Exportar. Se desejar cancelar a exportação, clique em Cancelar exportação. Se outro usuário agendou uma exportação, o botão Cancelar exportação ficará indisponível até que essa exportação seja concluída. O botão Cancelar exportação estará indisponível se outro usuário tiver programado uma exportação. Para verificar se uma Exportação programada ou Excluir foi iniciada ou concluída, clique em Atualizar.

### Excluir eventos de auditoria {#delete-audit-events}

É possível excluir eventos de auditoria com mais de um número especificado de dias.

1. No console de administração, clique em Serviços > Segurança do Documento > Configuração > Gerenciamento de Eventos.
1. Em Excluir Eventos de auditoria, especifique o número de dias na caixa Excluir Eventos de auditoria anteriores a.
1. Clique em Excluir. Clique em Exportar. Se desejar cancelar a exclusão, clique em Cancelar exclusão. Se outro usuário agendou uma exclusão, o botão Cancelar exclusão ficará indisponível até que a exportação seja concluída. O botão Cancelar exclusão estará indisponível se outro usuário tiver programado uma exportação. Para verificar se uma exclusão programada foi iniciada ou concluída, clique em Atualizar.

### Opções de auditoria de Eventos {#event-auditing-options}

Você pode ativar e desativar a auditoria de eventos e especificar os tipos de eventos a serem auditados.

**eventos Documentos**

**Documento da Visualização:** Um recipient visualização um documento protegido por política.

**Fechar Documento:** Um recipient fecha um documento protegido por política.

**Imprimir baixa resolução** Um recipient imprime um documento protegido por política com a opção de baixa resolução especificada.

**Imprimir em alta resolução:** Um recipient imprime um documento protegido por política com a opção de alta resolução especificada.

**Adicionar anotação ao Documento:** Um recipient adiciona uma anotação a um documento PDF.

**Revogar Documento:** Um usuário ou administrador revoga o acesso a um documento protegido por política.

**Cancelar revogação do Documento:** Um usuário ou administrador restabelece o acesso a um documento protegido por política.

**Preenchimento do formulário:** Um recipient insere informações em um documento PDF que é um formulário preenchível.

**Política removida:** Um editor remove uma política de um documento para retirar as proteções de segurança.

**Alterar URL de revogação do Documento:** Uma chamada do nível da API altera a URL de revogação especificada para acessar um novo documento que substitui um documento revogado.

**Modificar Documento:** Um recipient altera o conteúdo de um documento protegido por política.

**Assinar Documento:** Um recipient assina um documento.

**Proteger um novo Documento:** Um usuário aplica uma política para proteger um documento.

**Alternar política no Documento:** Um usuário ou administrador alterna a política anexada a um documento.

**Publicar Documento como:** Um novo documento cujo documentName e licença são idênticos a um documento existente é registrado no servidor e os documentos não têm uma relação pai-filho. Esse evento pode ser acionado usando o SDK de formulários do AEM.

**Iterar Documento:** Um novo documento cujo documentName e licença são idênticos a um documento existente é registrado no servidor e os documentos têm uma relação pai-filho. Esse evento pode ser acionado usando o SDK de formulários do AEM.

**eventos de políticas**

**Política criada:** Um usuário ou administrador cria uma política.

**Política ativada:** Um administrador disponibiliza uma política.

**Política alterada:** Um usuário ou administrador altera uma política.

**Política desativada:** Um administrador indisponibiliza uma política.

**Política excluída:** Um usuário ou administrador exclui uma política.

**Alterar proprietário da política:** Uma chamada do nível da API altera o proprietário da política.

**eventos do usuário**

**Usuário excluído:** Um administrador exclui uma conta de usuário.

**Registrar usuário convidado:** Um usuário externo se registra com segurança de documento.

**Logon bem-sucedido:** Tentativas de logon bem-sucedidas de administradores ou usuários.

**Usuários convidados:** A segurança do Documento convida o usuário a se registrar.

**Usuários ativados:** Usuários externos ativam suas contas usando o URL no e-mail da ativação, ou um administrador ativa uma conta.

**Alterar senha:** Os usuários convidados mudam suas senhas ou um administrador redefine uma senha para um usuário local.

**Falha de logon:** Tentativas de login com falha por administradores ou usuários.

**Usuários desativados:** Um administrador desativa uma conta de usuário local.

**Atualização do Perfil:** Os usuários convidados mudam seu nome, nome da organização e senha.

**Conta bloqueada:** Um administrador bloqueia uma conta.

**Eventos do Conjunto de Políticas**

**Conjunto de políticas criadas:** Um administrador ou coordenador de conjunto de políticas cria um conjunto de políticas.

**Conjunto de Políticas Excluído:** Um administrador ou coordenador de conjunto de políticas exclui um conjunto de políticas.

**Conjunto de Políticas Modificado:** Um administrador ou coordenador de conjunto de políticas altera um conjunto de políticas.

**eventos do sistema**

**DiretorySynchronization Complete:** Essas informações não estão disponíveis na página Eventos. As informações atuais de sincronização de diretório, incluindo o estado e a hora atuais da última sincronização, são exibidas na página Gerenciamento de domínio. Para acessar a página Gerenciamento de domínio no console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.

**Cliente Ativar Acesso Offline:** Um usuário habilitou o acesso offline a documentos protegidos contra o servidor no computador do usuário.

**O aplicativo Cliente** Sincronizado deve sincronizar informações com o servidor para permitir o acesso offline.

**Incompatibilidade de versão:** Uma versão do SDK de formulários AEM incompatível com o servidor tentou se conectar ao servidor.

**Informações de sincronização de diretório:** Essas informações não estão disponíveis na página Eventos. As informações atuais de sincronização de diretório, incluindo o estado e a hora atuais da última sincronização, são exibidas na página Gerenciamento de domínio. Para acessar a página Gerenciamento de domínio no console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.

**Alteração na configuração do servidor:** Alterações na configuração do servidor que são feitas pelas páginas da Web ou manualmente importando um arquivo config.xml. Isso inclui alterações no URL básico, tempos limite de sessão, bloqueios de login, configurações de diretório, sobreposições de chave, configurações do servidor SMTP para registro externo, configuração de marca d&#39;água, opções de exibição e assim por diante.

## Configuração do rastreamento de uso estendido {#configuring-extended-usage-tracking}

A segurança do Documento pode rastrear vários eventos personalizados que podem ser executados em um documento protegido. Você pode ativar o rastreamento de eventos do servidor de segurança do documento no nível global ou em um nível de política. Em seguida, é possível configurar um JavaScript para capturar ações específicas executadas dentro do documento PDF protegido, como clicar em um botão ou salvar o documento. Esses dados de uso são enviados como um arquivo XML em pares de valores chave, que podem ser usados para análise adicional. Os usuários finais que acessam os documentos protegidos podem permitir ou recusar esse rastreamento do aplicativo cliente.

Se o rastreamento estiver ativado no nível global, você poderá substituir essa configuração no nível da política e desativá-la para uma política específica. A substituição em nível de política não é possível se o rastreamento estiver desativado em nível global. A lista de eventos rastreados é automaticamente empurrada para o servidor quando a contagem de eventos atinge 25 ou quando o documento é fechado. Você também pode configurar seu script para encaminhar explicitamente a lista do evento de acordo com seus requisitos. Você pode personalizar o rastreamento de eventos acessando as propriedades e os métodos do objeto de segurança do documento.

Depois de ativar o rastreamento, todas as políticas criadas subsequentemente terão o rastreamento ativado por padrão. As políticas criadas antes de o rastreamento ser ativado no servidor precisarão de atualizações manuais.

### Ativar ou desativar o rastreamento de uso estendido {#enable-or-disable-extended-usage-tracking}

Antes de começar, verifique se a Auditoria de Servidor está ativada. Consulte [Configuração de auditoria de eventos e configurações](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) de privacidade para obter mais informações sobre auditoria.

1. No console de administração, clique em Serviços > Segurança do Documento > Configuração > Configurações de auditoria e privacidade.
1. Para configurar o rastreamento de uso estendido, em Ativar rastreamento, selecione Sim ou Não.
1. Para definir a seleção da caixa de seleção Permitir coleta de dados de uso detalhado na página de logon, em Ativar rastreamento padrão, selecione Sim ou Não.

Para visualização dos eventos rastreados, você pode usar o filtro Eventos de Documentos na página Eventos. Os eventos rastreados por JavaScript são rotulados como Monitoramento de uso detalhado. Consulte [Monitoramento de eventos](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) para obter mais informações sobre eventos.

## Definir configurações de exibição de segurança do documento {#configure-document-security-display-settings}

1. No console de administração, clique em Serviços > Segurança do documento > Configuração > Opções de exibição.
1. Configure as configurações e clique em OK.

### Display settings {#display-settings}

**Linhas a serem exibidas para os resultados da pesquisa:** Número de linhas que aparecem em uma página quando as pesquisas são realizadas.

**Personalização da caixa de diálogo de logon do cliente**

Essas configurações controlam o texto exibido no prompt de logon que aparece quando um usuário faz login na segurança do documento por meio de um aplicativo cliente.

**Texto de boas-vindas:** O texto da mensagem de boas-vindas, como &quot;Faça logon com seu nome de usuário e senha&quot;. O texto da mensagem de boas-vindas deve conter informações sobre como fazer logon na segurança do documento e como entrar em contato com um administrador ou outra pessoa de suporte designada em sua organização para obter assistência. Por exemplo, os usuários externos podem precisar entrar em contato com um administrador caso se esqueçam de suas senhas ou precisem de ajuda com o processo de registro ou login. O comprimento máximo do texto de boas-vindas é de 512 caracteres.

**Texto do nome do usuário:** O rótulo do texto da caixa de nome do usuário.

**Texto da senha:** O rótulo do texto para a caixa de senha.

**Caixa de diálogo Personalização da autenticação de certificado do cliente**

Essas configurações controlam o texto exibido na caixa de diálogo de autenticação de certificado.

**Texto do tipo ChooseAuthentication:** O texto exibido para direcionar um usuário a selecionar um tipo de autenticação.

**Escolher texto do certificado:** O texto exibido para direcionar um usuário a selecionar um tipo de certificado.

**Texto de erro de certificados não disponíveis:** Mensagem de até 512 caracteres para exibir quando o certificado selecionado não estiver disponível.

**Personalização para exibição de certificado do cliente**

**Exibir Somente Emissores de Credenciais Confiáveis:** Quando essa opção é selecionada, o aplicativo cliente apresenta ao usuário somente certificados de emissores de credenciais nos quais os formulários AEM estão configurados para confiar (Consulte Gerenciamento de certificados e credenciais). Quando essa opção não estiver selecionada, o usuário receberá uma lista de todos os certificados no sistema do usuário.

## Configurar marcas d&#39;água dinâmicas {#configure-dynamic-watermarks}

Usando a segurança do documento, você pode definir as configurações padrão para a opção de marca d&#39;água dinâmica que pode ser aplicada ao criar políticas. Uma *marca d&#39;água* é uma imagem que é sobreposta ao texto no documento. É útil para rastrear o conteúdo de um documento e pode ajudar a identificar o uso ilegal do conteúdo.

Uma marca d&#39;água dinâmica pode consistir em texto composto de variáveis definidas, como ID de usuário e data e texto personalizado, ou conteúdo avançado em um PDF. É possível configurar marcas d&#39;água com vários elementos, cada um com seu próprio posicionamento e formatação.

As marcas d&#39;água não são editáveis e, portanto, são um método mais seguro para garantir a confidencialidade do conteúdo do documento. As marcas d&#39;água dinâmicas também asseguram que uma marca d&#39;água exiba informações específicas suficientes para agir como um dissuasor para distribuir o documento.

A marca d&#39;água que uma política especifica aparece no documento protegido por política quando um recipient visualização ou imprime o documento. Diferentemente das marcas d&#39;água permanentes, uma marca d&#39;água dinâmica nunca é salva no documento, o que proporciona a flexibilidade necessária ao implantar um documento em um ambiente da intranet para garantir que o aplicativo de visualização exiba a identidade do usuário específico. Além disso, se um documento tiver vários usuários, o uso da marca d&#39;água dinâmica significa que você pode usar um documento em vez de várias versões, cada uma com uma marca d&#39;água diferente. A marca d&#39;água que aparece reflete a identidade do usuário atual.

Observe que as marcas d&#39;água dinâmicas são diferentes das marcas d&#39;água que os usuários podem adicionar diretamente ao documento no Acrobat. O resultado é que você pode ter duas marcas d&#39;água em um documento protegido por política.

### Considerações ao criar marcas d&#39;água {#considerations-when-creating-watermarks}

É possível criar marcas d&#39;água dinâmicas com vários elementos de marca d&#39;água com cada elemento especificado como texto ou PDF. É possível incluir até cinco elementos, em uma marca d&#39;água.

Se você escolher uma marca d&#39;água baseada em texto, poderá especificar vários elementos dentro da marca d&#39;água com várias entradas de texto e especificar o posicionamento de cada elemento. Atribua nomes significativos a esses elementos, como cabeçalho, rodapé e assim por diante.

Por exemplo, se você quiser especificar um texto diferente no cabeçalho, rodapé, nas margens e no documento como uma marca d&#39;água, crie vários elementos de marca d&#39;água e especifique suas posições. Se desejar que a ID de usuário e a data atual de acesso ao documento apareçam no cabeçalho, o nome da política na margem direita e um texto personalizado &quot;CONFIDENTIAL&quot; apareçam na diagonal no documento, defina elementos de marca d&#39;água separados com texto como o tipo e especifique sua formatação e posicionamento. Quando a marca de água é aplicada a um documento, todos os elementos da marca de água são aplicados ao documento ao mesmo tempo, na ordem em que são adicionados à marca de água.

Normalmente, você usa marcas d&#39;água baseadas em PDF para incluir conteúdo gráfico, como logotipos ou símbolos especiais, como copyright ou marca registrada.

É possível alterar os limites do número de elementos de marca d&#39;água e o tamanho do arquivo PDF modificando o arquivo de configuração de segurança do documento. Consulte [Alterar os parâmetros](configuring-client-server-options.md#change-the-watermark-configuration-parameters)de configuração de marca d&#39;água.

Lembre-se do seguinte ao configurar marcas d&#39;água:

* Não é possível usar um documento PDF protegido por senha como elemento de marca d&#39;água. No entanto, se a marca d&#39;água criada contiver outros elementos que não sejam protegidos por senha, eles serão aplicados como parte da marca d&#39;água.
* Você pode alterar o tamanho máximo do arquivo PDF que deseja usar como elemento de marca d&#39;água. No entanto, documentos PDF grandes usados como marcas d&#39;água degradam o desempenho durante a sincronização offline de documentos aplicados com essas marcas d&#39;água. Consulte [Alterar os parâmetros](configuring-client-server-options.md#change-the-watermark-configuration-parameters)de configuração de marca d&#39;água.
* Somente a primeira página do PDF selecionado é usada como marca d&#39;água. Certifique-se de que as informações que você deseja que sejam exibidas como marca d&#39;água estejam disponíveis na primeira página.
* Mesmo que você possa especificar o dimensionamento do documento PDF, considere o tamanho e o layout da página do PDF se planeja usá-lo como uma marca d&#39;água no cabeçalho, no rodapé ou nas margens.
* Ao especificar o nome da fonte, insira o nome corretamente. Os formulários AEM substituem a fonte especificada se não estiver presente no computador cliente em que o documento é aberto.
* Se você selecionou o texto como o conteúdo da marca d&#39;água, especificar a opção de dimensionamento como Ajustar à página não funciona para páginas com largura diferente.
* Ao especificar o posicionamento dos elementos de marca d&#39;água, certifique-se de que não haja mais de um elemento com o mesmo posicionamento. Se dois elementos de marca d&#39;água tiverem o mesmo posicionamento, como centro, eles aparecerão sobrepostos no documento e na ordem em que foram adicionados à marca d&#39;água.
* Ao especificar o tamanho e o tipo da fonte, verifique se o comprimento do texto está completamente visível na página. O conteúdo do texto é revertido para novas linhas, de modo que o conteúdo da marca d&#39;água que você deseja que esteja presente nas margens pode se sobrepor nas áreas de conteúdo das páginas. Entretanto, se o documento for aberto no Acrobat 9, o texto além da linha única será truncado.

### Limitações das marcas d&#39;água dinâmicas {#limitations-of-dynamic-watermarks}

Alguns aplicativos clientes podem não suportar marcas d&#39;água dinâmicas. Consulte a Ajuda apropriada das extensões do Acrobat Reader DC. Além disso, lembre-se das seguintes versões do Acrobat compatíveis com marcas d&#39;água dinâmicas:

* Não é possível usar um documento PDF protegido por senha como elemento de marca d&#39;água.
* As versões do Acrobat e do Adobe Reader anteriores à versão 10 não são compatíveis com os seguintes recursos de marca d&#39;água:

   * Marcas d&#39;água do PDF
   * Vários elementos na marca d&#39;água (Texto/PDF)
   * Opções avançadas, como intervalo de páginas ou opções de exibição
   * Opções de formatação de texto, como fonte especificada, nome da fonte e cor. No entanto, as versões anteriores do Acrobat e do Reader exibirão o conteúdo do texto na fonte e na cor padrão.

* Acrobat 9.0 e versões anteriores: O Acrobat 9.0 e anterior não suporta nomes de políticas em marcas d&#39;água dinâmicas. Se o Acrobat 9.0 abrir um documento protegido por política com uma marca d&#39;água dinâmica que inclui um nome de política e outros dados dinâmicos, a marca d&#39;água será exibida sem o nome da política. Se a marca d&#39;água dinâmica incluir apenas o nome da política, o Acrobat exibirá uma mensagem de erro

### Adicionar um modelo de marca d&#39;água dinâmica {#add-a-dynamic-watermark-template}

Você pode criar modelos dinâmicos de marca d&#39;água. Esses modelos permanecem disponíveis como uma opção de configuração para políticas criadas por administradores ou usuários.

>[!NOTE]
>
>As informações de configuração de marca d&#39;água dinâmica não são capturadas com as outras informações de configuração ao exportar um arquivo de configuração.

1. No console de administração, clique em Serviços > Segurança do Documento > Configuração > Marcas d&#39;água.
1. Clique em Novo.
1. Na caixa Nome, digite um nome para a nova marca d&#39;água.

   ***observação **: Não é possível usar alguns caracteres especiais nos nomes ou descrições de marcas d&#39;água ou elementos de marcas d&#39;água. Consulte as restrições listadas em[Considerações para políticas](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies)de edição.*

1. Em Nome, ao lado do sinal de mais, digite um nome significativo para o elemento de marca d&#39;água, como Cabeçalho, adicione uma descrição e expanda o sinal de mais para exibir as opções.
1. Em Origem, selecione o tipo de marca d&#39;água como Texto ou PDF.
1. Se você selecionou Texto, faça o seguinte:

   * Selecione os tipos de marca d&#39;água a serem incluídos. Se você selecionar Texto personalizado, na caixa adjacente, digite o texto a ser exibido para a marca d&#39;água. Lembre-se do comprimento do texto que será exibido como marca d&#39;água.
   * Especifique as propriedades de formatação do texto, como nome da fonte, tamanho da fonte, cor do primeiro plano e cor do plano de fundo, para o conteúdo do texto da marca d&#39;água. Especifique a cor do primeiro plano e do plano de fundo como valores hexadecimais.

      ***observação **: Se você selecionar a opção de dimensionamento como Ajustar à página, a propriedade de tamanho da fonte não estará disponível para edição.*

1. Se você selecionou PDF para opções de marca d&#39;água avançada, clique em **Procurar** ao lado de Selecionar PDF de marca d&#39;água para selecionar o documento PDF que deseja usar como marca d&#39;água.

   ***observação **: Não use um documento PDF protegido por senha. Se você especificar um PDF protegido por senha como elemento de marca d&#39;água, a marca d&#39;água não será aplicada.*

1. Em Usar como plano de fundo, selecione Sim ou Não.

   **observação**: Atualmente, a marca d&#39;água aparece no primeiro plano independentemente dessa configuração.

1. Para controlar onde a marca d&#39;água é exibida no documento, configure as opções Alinhamento vertical e Alinhamento horizontal.
1. Selecione Ajustar à página ou % e digite uma porcentagem na caixa. O valor deve ser um número inteiro, não uma fração. Para configurar o tamanho da marca d&#39;água, você pode usar um valor que seja a porcentagem da página ou definir a marca d&#39;água para ajustar ao tamanho da página.
1. Na caixa Rotação, digite os graus pelos quais girar a marca d&#39;água. O intervalo é de -180 a 180. Use um valor negativo para girar a marca d&#39;água no sentido anti-horário. O valor deve ser um número inteiro, não uma fração.
1. Na caixa Opacidade, digite uma porcentagem. Use um número inteiro, não uma fração.
1. Em Opções avançadas, defina o seguinte:

   **Opções de intervalo de páginas**

   Defina o intervalo de páginas no qual a marca d&#39;água deve ser exibida. Insira a página do start como 1 e a página final como -1 para que todas as páginas sejam marcadas com a marca d&#39;água.

   **Opções de exibição**

   Selecione onde deseja que a marca d&#39;água apareça. Por padrão, a marca d&#39;água aparece tanto em cópia em papel (online) quanto em papel (impresso).

1. Clique em **Novo** em Elementos de marca d&#39;água para adicionar mais elementos de marca d&#39;água, se necessário.
1. Clique em OK.

### Editar um modelo de marca d&#39;água dinâmica {#edit-a-dynamic-watermark-template}

1. No console de administração, clique em Serviços > Segurança do documento > Configuração > Marcas d&#39;água.
1. Clique na marca d&#39;água apropriada na lista.
1. Na página Editar marcas d&#39;água, altere as configurações conforme necessário.
1. Clique em OK.

### Excluir um modelo de marca d&#39;água dinâmica {#delete-a-dynamic-watermark-template}

Quando você exclui uma marca d&#39;água dinâmica, ela não está mais disponível para adicionar a uma nova política. No entanto, a marca d&#39;água permanece nas políticas existentes que a utilizam no momento, e documentos que a política protege no momento continuam mostrando a marca d&#39;água dinâmica até que você ou um usuário edite a política que contém a marca d&#39;água excluída. Depois que a política é editada, a marca d&#39;água não é mais aplicada. Uma mensagem é exibida, indicando que a marca d&#39;água existente é excluída na política e que o usuário pode selecionar outra para substituí-la.

1. No console de administração, clique em Serviços > Segurança do Documento > Configuração > Marcas d&#39;água.
1. Marque a caixa de seleção ao lado da marca d&#39;água apropriada e clique em Excluir.
1. Clique em OK.

## Configurar o registro de usuário convidado {#configuring-invited-user-registration}

Os usuários externos à sua organização podem se registrar com segurança de documento. Os usuários convidados que se registram e ativam suas contas podem fazer logon na segurança do documento usando seu endereço de email e a senha criados ao se registrarem. Os usuários convidados registrados podem usar documentos protegidos por política aos quais têm permissões.

Quando os usuários convidados são ativados, eles se tornam usuários locais. Os usuários locais podem ser configurados e gerenciados usando a área Usuários convidados e locais. (Consulte [Gerenciamento de contas](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts)de usuários convidados e locais.)

Dependendo dos recursos que você ativar para usuários convidados, eles também poderão usar estes recursos de segurança do documento:

* Aplicar políticas a documentos
* Criar políticas
* Adicionar usuários convidados a políticas

A segurança do Documento gera automaticamente um e-mail de convite de registro quando os seguintes eventos ocorrem, a menos que o usuário já esteja no diretório LDAP de origem ou tenha sido previamente convidado a se registrar:

* Um usuário existente adiciona um usuário convidado a uma política
* Um administrador adiciona uma conta de usuário convidada na página Registro de usuário convidado

O email de inscrição contém um link para a página de inscrição e informações sobre como se registrar. Depois que o usuário convidado se registra, a segurança do documento emite um email de ativação com um link para uma página de Ativação. Quando ativada, a conta permanece válida até que você a desative ou exclua.

Se você habilitar o registro integrado, especifique seu servidor SMTP, detalhes de e-mail de registro, recursos de acesso e redefina as informações de e-mail de senha apenas uma vez. Antes de ativar o registro interno, certifique-se de que você criou um domínio local no Gerenciamento de usuários atribuiu a função &quot;Usuário do convite para a segurança do Documento&quot; aos usuários e grupos apropriados em sua organização. (Consulte [Adicionar um domínio](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) local e [Criar e configurar funções](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).) Se você não usar o registro incorporado, precisará ter seu próprio sistema de registro de usuário criado usando o SDK de formulários AEM. Consulte a ajuda sobre &quot;Desenvolvimento de SPIs para formulários AEM&quot; em [Programação com formulários](https://www.adobe.com/go/learn-aemforms-programming-63)AEM. Se você não usar a opção Registro incorporado, é recomendável configurar uma mensagem no email de ativação e na tela de login do cliente para notificar os usuários sobre como entrar em contato com o administrador para obter uma nova senha ou outras informações.

**Ativar e configurar o registro de usuário convidado**

Por padrão, o processo de registro do usuário convidado está desativado. Você pode ativar e desativar o registro de usuário convidado para segurança de documento, conforme necessário.

1. No console de administração, clique em Serviços > Segurança do documento > Configuração > Registro de usuário convidado.
1. Selecione Ativar registro de usuário convidado.
1. (Opcional) Atualize as configurações de registro do usuário convidado, conforme necessário:

   * [Excluir ou incluir um usuário ou grupo externo](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [Parâmetros de servidor e conta de registro](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [Configurações de email de convite de registro](configuring-client-server-options.md#registration-invitation-email-settings)
   * [Configurações de e-mail de Ativação](configuring-client-server-options.md#activation-email-settings)
   * [Configurar um email de redefinição de senha](configuring-client-server-options.md#configure-a-password-reset-email)

1. (Opcional) Em Registro incorporado, selecione Sim para ativar essa opção. Se você não ativar o registro integrado, deverá configurar seu próprio sistema de registro de usuário.
1. Clique em OK.

### Excluir ou incluir um usuário ou grupo externo {#exclude-or-include-an-external-user-or-group}

Você pode restringir o registro com segurança de documento para determinados usuários externos ou grupos de usuários. Essa opção é útil, por exemplo, para permitir o acesso a um determinado grupo de usuários, mas excluir indivíduos específicos que fazem parte do grupo.

As configurações a seguir estão localizadas na área Filtro de restrições de email da página Registro de usuário convidado.

**Exclusão:** Digite o endereço de email de um usuário ou grupo a ser excluído. Para excluir vários usuários ou grupos, digite cada endereço de email em uma nova linha. Para excluir todos os usuários que pertencem a um domínio específico, insira um curinga e o nome do domínio. Por exemplo, para excluir todos os usuários no domínio example.com, insira &amp;ast;.example.com.

**Inclusão:** Digite o endereço de email de um usuário ou grupo a ser incluído. Para incluir vários usuários ou grupos, digite cada endereço de email em uma nova linha. Para incluir todos os usuários que pertencem a um domínio específico, insira um curinga e o nome do domínio. Por exemplo, para incluir todos os usuários no domínio example.com, insira &amp;ast;.example.com.

### Parâmetros de servidor e conta de registro {#server-and-registration-account-parameters}

As configurações a seguir estão localizadas na área Configurações gerais da página Registro de usuário convidado.

**Host SMTP:** O nome do host do servidor SMTP. O servidor SMTP gerencia os avisos de email de saída para registrar e ativar contas de usuário convidadas.

Se exigido pelo host SMTP, digite as informações necessárias nas caixas Nome da conta do servidor SMTP e Senha da conta do servidor SMTP para conectar-se ao servidor SMTP. Algumas organizações não aplicam esse requisito. Se precisar de informações, consulte o administrador do sistema.

**Nome da classe de soquete do servidor SMTP:** Nome da classe Socket para o servidor SMTP. Por exemplo, javax.net.ssl.SSLSocketFactory.

**Tipo de conteúdo de email:** Tipo MIME aceito, como text/plain ou text/html.

**Codificação de email:** Formato de codificação a ser usado ao enviar mensagens de email. É possível especificar qualquer codificação, por exemplo, UTF-8 para Unicode ou ISO-8859-1 para Latim. O padrão é UTF-8.

**Redirecionar endereço de email:** Ao especificar um endereço de email para essa configuração, qualquer novo convite será enviado para o endereço fornecido. Essa configuração pode ser útil para fins de teste.

**Usar domínios locais:** Selecione o domínio apropriado. Em uma nova instalação, verifique se você criou o domínio usando o Gerenciamento de usuários. Se esta for uma atualização, um domínio de usuário externo foi criado durante a atualização e pode ser usado.

**Usar SSL para servidor SMTP:** Selecione esta opção para habilitar SSL para o servidor SMTP.

**Exibir link de logon na página de registro:** Exibe um link de logon na página de registro exibida para os usuários convidados.

**Para habilitar o Transport Layer Security (TLS) para o servidor SMTP**

1. Abra o console de administração.

   O local padrão do console Administração é `https://<server>:<port>/adminui`.

1. Navegue até Início > Serviços > Segurança do Documento > Configuração > Registro de usuário convidado.
1. No Registro de usuário convidado, especifique todas as configurações e clique em OK.

   >[!NOTE]
   >
   >Se você estiver usando o Microsoft Office 365 como servidor SMTP para enviar os convites para registro de usuário, use as seguintes configurações:
   >
   >**Host SMTP:** smtp.office365.com
   >**Porta:** 587

1. Em seguida, é necessário atualizar o config.xml. Consulte [Configuração para ativar o SMTP para TLS (Transport Layer Security)](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>Se você fizer alterações nas opções de Registro de usuário convidado, o arquivo config.xml será substituído e o TLS será desativado. Se você substituir as alterações, será necessário executar a etapa acima para reativar o suporte TLS para o Registro de usuário convidado.

### Configurações de email de convite de registro {#registration-invitation-email-settings}

A segurança do Documento emite automaticamente um e-mail de convite de registro quando você cria uma nova conta de usuário convidado ou quando um usuário existente adiciona um recipient externo que não se registrou anteriormente ou foi convidado para se registrar em uma política. O e-mail contém um link que o recipient pode usar para acessar a página de registro e inserir informações pessoais da conta, incluindo nome de usuário e senha. A senha pode ser qualquer combinação de oito caracteres.

Quando o recipient ativa a conta, o usuário se torna um usuário local.

As configurações a seguir estão localizadas na área Configuração de e-mail de convite da página Registro de usuário convidado.

**De:** O endereço de e-mail do qual o e-mail de convite é enviado. O formato padrão do endereço de email De é postmaster@[your_installation_domain].com.

**Assunto:** Assunto padrão para a mensagem de email do convite.

**Tempo limite:** O número de dias após o qual o convite de inscrição expira se o usuário externo não se registrar. O valor padrão é 30 dias.

**Mensagem:** O texto que aparece no corpo da mensagem convidando o usuário a se registrar.

### Configurações de e-mail de Ativação {#activation-email-settings}

Depois que os usuários convidados se registrarem, a segurança do documento enviará um email de ativação. O e-mail de ativação contém um link para a página de ativação da conta onde os usuários podem ativar suas contas. Quando as contas são ativadas, os usuários podem fazer logon na segurança do documento usando seu endereço de email e a senha que criaram quando se registraram.

Quando o recipient ativa a conta do usuário, ele se torna um usuário local.

As configurações a seguir estão localizadas na área Configuração de e-mail de Ativação da página Registro de usuário convidado.

>[!NOTE]
>
>Também é recomendável configurar uma mensagem na tela de logon para avisar aos usuários externos como entrar em contato com o administrador para obter uma nova senha ou outras informações.

**De:** O endereço de email do qual o email de ativação é enviado. Este endereço de email recebe avisos de falha de delivery do host de email do registrante e também mensagens que o recipient envia em resposta ao email de inscrição. O formato padrão do endereço de email De é postmaster@[your_installation_domain].com.

**Assunto:** Assunto padrão para a mensagem de e-mail de ativação.

**Tempo limite:** O número de dias após o qual o convite de ativação expira se o usuário não ativar a conta. O valor padrão é 30 dias.

**Mensagem:** O texto que aparece no corpo da mensagem é uma mensagem indicando que a conta de usuário do recipient precisa ser ativada. Você também pode incluir informações como entrar em contato com um administrador para obter uma nova senha.

### Configurar um email de redefinição de senha {#configure-a-password-reset-email}

Se você precisar redefinir a senha de um usuário convidado, um email de confirmação será gerado e convidará o usuário a escolher uma nova senha. Não é possível determinar a senha de um usuário; se o usuário o esquecer, é necessário redefini-lo.

As configurações a seguir estão localizadas na área Redefinir e-mail de senha da página Registro de usuário convidado.

**De:** O endereço de email do qual o email de redefinição de senha é enviado. O formato padrão do endereço de email De é postmaster@[your_installation_domain].com.

**Assunto:** Assunto padrão para a mensagem de email de redefinição.

**Mensagem:** O texto que aparece no corpo da mensagem é uma mensagem indicando que a senha externa do usuário do recipient foi redefinida.

## Permitir que usuários e grupos criem políticas {#enable-users-and-groups-to-create-policies}

A página Configuração tem um link para a página Minhas políticas, onde você especifica quais usuários finais podem criar minhas políticas e quais usuários e grupos estão visíveis nos resultados da pesquisa. A página Minhas políticas tem duas guias:

**Guia Criar Políticas:** Use para configurar permissões de usuário para criar políticas personalizadas.

**Guia Usuários e grupos visíveis:** Use para controlar quais usuários e grupos estão visíveis nos resultados da pesquisa do usuário. O superusuário ou administrador do conjunto de políticas é necessário para selecionar e adicionar domínios, criados no Gerenciamento de usuários, ao usuário e grupo visíveis para cada conjunto de políticas. Essa lista é visível para o coordenador do conjunto de políticas e é usada para colocar limites em quais domínios o coordenador do conjunto de políticas pode navegar ao escolher usuários a serem adicionados às políticas.

Antes de conceder aos usuários permissão para criar políticas personalizadas, considere quanto acesso ou controle você deseja que os usuários individuais tenham. Além disso, considere como você deseja que seus usuários e grupos fiquem expostos ao torná-los visíveis para pesquisas.

### Especificar usuários e grupos que podem criar políticas {#specify-users-and-groups-who-can-create-policies}

Como administrador, especifique quais usuários e grupos podem criar políticas personalizadas. Essa permissão pode ser definida no nível do usuário e do grupo. A funcionalidade de pesquisa pesquisa pesquisa usuários e grupos no banco de dados Gerenciamento de usuários.

1. No console de administração, clique em Serviços > Segurança do Documento > Configuração > Minhas políticas.
1. Na página Minhas políticas, clique na guia Criar políticas e clique em Adicionar usuários e grupos.
1. Na caixa Localizar, digite o nome de usuário ou endereço de email do usuário ou grupo que você está procurando. Se você não tiver essas informações, deixe a caixa vazia. Você também pode digitar um nome parcial ou um endereço de email, como quando sabe apenas as duas primeiras letras de um nome de usuário.
1. Na lista Using, selecione seus parâmetros de pesquisa Name (Nome) ou Email.
1. Na lista Tipo, selecione Grupo ou Usuário para restringir sua pesquisa.
1. Na lista In, selecione o domínio a ser pesquisado. Se você não souber o domínio do usuário ou grupo, selecione Todos os domínios.
1. Na lista de exibição, especifique o número de resultados de pesquisa a serem exibidos por página e clique em Localizar.
1. Para adicionar usuários e grupos de Minhas políticas, marque a caixa de seleção de cada usuário e grupo a ser adicionado.
1. Clique em Adicionar e em OK.

Seus usuários e grupos selecionados agora têm permissão para criar políticas personalizadas.

### Remover a permissão para criar políticas personalizadas de um usuário ou grupo {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. Na página Segurança do documento, clique em Configuração > Minhas políticas.
1. Na página Minhas políticas, clique na guia Criar políticas. Os usuários e grupos com permissões para criar políticas personalizadas são exibidos.
1. Marque a caixa de seleção ao lado dos usuários e grupos a serem removidos dessa permissão.
1. Clique em Excluir e em OK.

### Especificar usuários e grupos que estão visíveis nas pesquisas {#specify-users-and-groups-that-are-visible-in-searches}

Quando os usuários gerenciam suas políticas personalizadas, eles podem procurar usuários e grupos para adicioná-las às suas políticas. Você deve especificar os domínios a partir dos quais os usuários e grupos estão visíveis nessas pesquisas.

1. Na página Segurança do documento, clique em Configuração > Minhas políticas.
1. Na página Minhas políticas, clique na guia Usuários e grupos visíveis.
1. Para tornar os usuários e grupos de um domínio visíveis, clique em Adicionar domínios, selecione os domínios e clique em Adicionar. Para remover um domínio, marque a caixa de seleção ao lado do nome do domínio e clique em Excluir.

## Editar manualmente o arquivo de configuração de segurança do documento {#manually-editing-the-document-security-configuration-file}

É possível importar e exportar as informações de configuração armazenadas no banco de dados de segurança do documento. Por exemplo, talvez você queira fazer uma cópia de backup das informações de configuração ao mover de uma preparação para um ambiente de produção, ou talvez deseje editar opções avançadas que só podem ser configuradas para editar esse arquivo.

É possível fazer as seguintes alterações usando o arquivo de configuração:

[Exibir permissões CATIA ao criar e editar políticas](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[Especificar um período de tempo limite para sincronização offline](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[Negar serviços de segurança de documento para aplicações específicas](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[Alterar os parâmetros de configuração da marca d&#39;água](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[Desativar links externos](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>A importação do arquivo de configuração reconfigura seu sistema com base nas informações do arquivo. As exceções são a configuração dinâmica de marca d&#39;água e informações de eventos personalizados, que não são salvas com o arquivo de configuração exportado. Você deve configurar essas informações manualmente no seu novo sistema. Somente um administrador do sistema ou um consultor de serviços profissionais familiarizado com a segurança do documento e o XML devem modificar o conteúdo de um arquivo de configuração, por exemplo, para reconfigurar uma configuração corrompida ou para ajustar os parâmetros de um determinado cenário de implantação corporativa.

**Exportar um arquivo de configuração**

1. No console de administração, clique em Serviços > Segurança do documento 11 > Configuração > Configuração manual.
1. Clique em Exportar e salve o arquivo de configuração em outro local. O nome de arquivo padrão é config.xml.
1. Clique em OK.
1. Antes de alterar o arquivo de configuração, faça uma cópia de backup caso precise reverter.

**Importar um arquivo de configuração**

1. No console de administração, clique em Serviços > Segurança do documento 11 > Configuração > Configuração manual.
1. Clique em Procurar para ir até o arquivo de configuração e clique em Importar. Não é possível digitar o caminho diretamente na caixa Nome do arquivo.
1. Clique em OK.

### Especificar um período de tempo limite para sincronização offline {#specify-a-timeout-period-for-offline-synchronization}

A segurança do Documento permite que os usuários abram e usem documentos protegidos quando não estiverem conectados ao servidor de segurança do documento. O aplicativo cliente do usuário deve sincronizar regularmente com o servidor para manter os documentos válidos para uso offline. Na primeira vez que os usuários abrem um documento protegido, será solicitado que eles saibam se o computador deve ser autorizado a executar a sincronização periódica do cliente.

Por padrão, a sincronização ocorre automaticamente a cada quatro horas e conforme necessário quando um usuário está conectado ao servidor de segurança do documento. Se o período offline de um documento expirar enquanto o usuário estiver offline, ele deverá se reconectar ao servidor para permitir que o aplicativo cliente sincronize com o servidor.

No arquivo de configuração de segurança do documento, você pode especificar a frequência padrão da sincronização automática em segundo plano. Essa configuração atua como o tempo limite padrão dos aplicativos clientes, a menos que o cliente defina explicitamente seu próprio valor de tempo limite.

1. Exporte o arquivo de configuração de segurança do documento. (Consulte Editar [manualmente o arquivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuração de segurança do documento.)
1. Abra o arquivo de configuração em um editor e localize o `PolicyServer` nó. Sob esse nó, localize o `ServerSettings` nó.
1. No `ServerSettings` nó, adicione esta entrada e salve o arquivo:

   `<entry key="BackgroundSyncFrequency" value="`*time *`"/>`

   onde *time* é o número de segundos entre sincronizações automáticas em segundo plano. Se você enviou esse valor para `0`, a sincronização sempre ocorre. O valor padrão é `14400` segundos (a cada quatro horas).

1. Importe o arquivo de configuração. (Consulte Editar [manualmente o arquivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuração de segurança do documento.)

### Negar serviços de segurança de documento para aplicações específicas {#denying-document-security-services-for-specific-applications}

Você pode configurar a segurança do documento para negar serviços a aplicativos que atendam a critérios específicos. Os critérios podem especificar um único atributo, como um nome de plataforma, ou podem especificar vários conjuntos de atributos. Este recurso pode ajudá-lo a controlar as solicitações que a segurança do documento deve tratar. Estes são alguns aplicativos deste recurso:

* **Proteção de receita:** Você pode negar acesso a qualquer aplicativo cliente que não suporte suas convenções de receita.
* **Compatibilidade do aplicativo:** Alguns aplicativos podem ser incompatíveis com as políticas ou o comportamento do servidor de segurança do documento.

Quando os aplicativos clientes tentam estabelecer um link com a segurança do documento, eles fornecem informações sobre aplicativos, versões e plataformas. A segurança do Documento compara essas informações com as configurações de Negação que ele obtém do arquivo de configuração de segurança do documento.

As configurações de Negações podem conter vários conjuntos de condições de negação. Se todos os atributos de um conjunto corresponderem, o aplicativo solicitante terá o acesso negado aos serviços de segurança do documento.

O recurso de negação de serviço exige que os aplicativos clientes usem o SDK de segurança do documento C++ Client versão 8.2 ou posterior. Os seguintes produtos da Adobe fornecem informações sobre o produto ao solicitar serviços de segurança do documento:

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard e posterior
* Adobe Reader 9.0 e posterior
* Extensões do Acrobat Reader DC para Microsoft Office 8.2 e posterior

Os aplicativos clientes usam a API Cliente do SDK de segurança do documento C++ Client para solicitar serviços de segurança do documento. As solicitações da API do cliente incluem informações da plataforma e da versão do SDK (pré-compiladas na API do cliente) e informações do produto obtidas do aplicativo cliente.

Os aplicativos ou plug-ins do cliente fornecem informações sobre o produto na implementação de uma função de retorno de chamada. O aplicativo fornece as seguintes informações:

* Nome do integrador
* Versão do integrador
* Família de aplicativos
* Nome do aplicativo
* Versão do aplicativo

Se alguma informação não for aplicável, o aplicativo cliente deixará o campo correspondente em branco.

Vários aplicativos da Adobe incluem informações do produto ao solicitar serviços de segurança do documento, incluindo extensões do Acrobat, Adobe Reader e Acrobat Reader DC para Microsoft Office.

**Acrobat e Adobe Reader**

Quando o Acrobat ou o Adobe Reader solicitam um serviço da segurança do documento, ele fornece as seguintes informações do produto:

* **Integrador:** Adobe Systems, Inc.
* **Versão do integrador:** 1,0
* **Família de aplicativos:** Acrobat
* **Nome do aplicativo:** Acrobat
* **Versão do aplicativo:** 9.0.0

**Extensões do Acrobat Reader DC para Microsoft Office**

O Acrobat Reader DC Extension for Microsoft Office é um plug-in usado com os produtos Microsoft Office Microsoft Word, Microsoft Excel e Microsoft PowerPoint. Quando solicita um serviço, ele fornece as seguintes informações:

* **Integrador:** Adobe Systems Incorporated
* **Versão do integrador:** 8,2
* **Família de aplicativos:** Extensões do Acrobat Reader DC para Microsoft Office
* **Nome do aplicativo:** Microsoft Word, Microsoft Excel ou Microsoft PowerPoint
* **Versão do aplicativo:** 2003 ou 2007

**Configurar a segurança do documento para negar serviços para aplicativos específicos**

1. Exporte o arquivo de configuração de segurança do documento. (Consulte Editar [manualmente o arquivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuração de segurança do documento.)
1. Abra o arquivo de configuração em um editor e localize o `PolicyServer` nó. Adicione um `ClientVersionRules` nó como um filho imediato do `PolicyServer` nó, se ele não existir:

   ```java
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

   `AppName`especifica o nome do aplicativo cliente. As vírgulas são usadas como separadores de nome. Para incluir uma vírgula em um nome, escape-a com um caractere de barra invertida (\). Por exemplo, *&quot;Adobe Systems\, Inc.&quot;*.

   `AppVersions` especifica a versão do aplicativo cliente.

   `Integrators` especifica o nome da empresa ou grupo que desenvolveu o plug-in ou o aplicativo integrado.

   `IntegratorVersions` é a versão do plug-in ou do aplicativo integrado.

1. Para cada conjunto adicional de dados de negação, adicione outro elemento *MyEntryName* .
1. Salve o arquivo de configuração.
1. Importe o arquivo de configuração. (Consulte Editar [manualmente o arquivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuração de segurança do documento.)

**Exemplos**

Neste exemplo, o acesso a todos os clientes Windows é negado.

```java
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

Neste exemplo, acesso negado a My Application versão 3.0 e My Other Application versão 2.0. O mesmo URL de informações de negação é usado independentemente do motivo da negação.

```java
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

Neste exemplo, todas as solicitações de uma instalação do Microsoft PowerPoint 2007 ou Microsoft PowerPoint 2010 de extensões do Acrobat Reader DC para Microsoft Office são negadas.

```java
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

Por padrão, você pode especificar um máximo de cinco elementos em uma marca d&#39;água. Além disso, o tamanho máximo de arquivo do documento PDF que você deseja usar como marca d&#39;água é limitado a 100 KB. Você pode alterar esses parâmetros no arquivo config.xml.

***observação **: Você deve alterar esses parâmetros com cautela.*

1. Exporte o arquivo de configuração de segurança do documento. (Consulte Editar [manualmente o arquivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuração de segurança do documento.)
1. Abra o arquivo de configuração em um editor e localize o `ServerSettings` nó.
1. No `ServerSettings` nó, adicione as seguintes entradas e salve o arquivo: `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   A primeira entrada, tamanho ** máximo do arquivo, é o tamanho máximo do arquivo (em KB) permitido para um elemento de marca d&#39;água PDF. O padrão é 100 KB.

   A segunda entrada, *max elements* é o número máximo de elementos permitidos em uma marca d&#39;água. O padrão é 5.

   ```java
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. Importe o arquivo de configuração. (Consulte Editar [manualmente o arquivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuração de segurança do documento.)

### Desativar links externos {#disabling-external-links}

Muitos usuários de segurança do documento não têm acesso a links externos, como **www.adobe.com** , enquanto usam interfaces de usuário do Rights Management:

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`.

As seguintes alterações no config.xml desabilitam todos os links externos das interfaces de usuário do Rights Management.

1. Exporte o arquivo de configuração de segurança do documento. (Consulte Editar [manualmente o arquivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuração de segurança do documento.)
1. Abra o arquivo de configuração em um editor e localize o `DisplaySettings` nó.
1. Para desativar todos os links externos, no `DisplaySettings` nó, adicione a seguinte entrada e salve o arquivo: `<entry key="ExternalLinksAllowed" value="false"/>`

   ```java
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. Importe o arquivo de configuração. (Consulte Editar [manualmente o arquivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuração de segurança do documento.)

### Configuração para habilitar o SMTP para o Transport Layer Security (TLS) {#configuration-to-enable-smtp-for-transport-layer-security-tls}

As seguintes alterações no config.xml habilitam o suporte TLS para o recurso de Registro de usuário convidado.

1. Exporte o arquivo de configuração de segurança do documento. (Consulte Editar [manualmente o arquivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuração de segurança do documento.)
1. Abra o arquivo de configuração em um editor e localize o `DisplaySettings` nó.
1. Localize o seguinte nó: `<node name="ExternalUser">`

   ```java
   <node name="ExternalUser">
   ```

1. Defina o valor da `SmtpUseTls` chave no `ExternalUser` nó como **true**.
1. Defina o valor da `SmtpUseSsl` chave no `ExternalUser` nó como **false**.
1. Salve o `config.xml`.
1. Importe o arquivo de configuração. (Consulte Editar [manualmente o arquivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuração de segurança do documento.)

### Desabilitar pontos de extremidade SOAP para documentos de segurança do Documento {#disable-soap-endpoints-for-document-security-documents}

As seguintes alterações no config.xml para desativar os pontos de extremidade SOAP para documentos de segurança do documento.

1. Exporte o arquivo de configuração de segurança do documento. (Consulte Editar [manualmente o arquivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuração de segurança do documento.)
1. Abra o arquivo de configuração em um editor e localize o seguinte nó: `<node name="DRM">`

   ```java
   <node name="DRM">
   ```

1. No nó DRM, localize o `entry` nó:

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. Para desativar pontos de extremidade SOAP para documentos de segurança de documento, defina o atributo value como **false**.

   ```java
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. Salve o `config.xml`.
1. Importe o arquivo de configuração. (Consulte Editar [manualmente o arquivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuração de segurança do documento.)

### Aumento da escalabilidade do servidor de segurança do documento {#increasingscalability}

Por padrão, ao sincronizar um documento para uso offline, juntamente com as informações do documento atual, os clientes de segurança do documento buscam informações de políticas, marcas d&#39;água, licenças e atualizações de revogação para todos os outros documentos aos quais o usuário tem acesso. Se essas atualizações e informações não forem sincronizadas com o cliente, um documento aberto no modo offline ainda poderá ser aberto com informações mais antigas de política, marca d&#39;água e revogação.

Você pode aumentar a escalabilidade do servidor de segurança do documento limitando as informações enviadas ao cliente. A redução na quantidade de informações enviadas ao cliente resulta em maior escalabilidade, menor tempo de resposta e melhor desempenho do servidor. Execute as seguintes etapas para aumentar a escalabilidade:

1. Exporte o arquivo de configuração de segurança do documento. (Consulte Editar [manualmente o arquivo](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuração de segurança do documento.)
1. Abra o arquivo de configuração em um editor e localize o nó ServerSettings.
1. No nó ServerSettings, defina o valor da `DisableGlobalOfflineSynchronizationData`propriedade como `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   Quando definido como true, o servidor de segurança do documento envia informações somente para o documento atual e as informações para o restante dos documentos (os outros documentos aos quais o usuário tem acesso) não são enviadas para o cliente.

   >[!NOTE]
   >
   >Por padrão, o valor da `DisableGlobalOfflineSynchronizationData`chave está definido como `false`.

1. Salve e importe o arquivo de configuração. (Consulte Editar [manualmente o arquivo](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)de configuração de segurança do documento.)

