---
title: Configurando diretórios
description: Saiba como adicionar, editar e excluir diretórios e configurar o gerenciamento de usuários para usar a exibição de lista virtual.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 30edcef2-e8fa-403a-9850-b8dfeeb9ac65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e9afc12af78140ae0ec12cc2ee95fc9e175f8d94
workflow-type: tm+mt
source-wordcount: '3241'
ht-degree: 0%

---


# Configurando diretórios {#configuring-directories}

Para cada domínio enterprise que você configurar, especifique os diretórios que o provedor de autenticação consultará para obter informações do usuário. Você pode configurar vários diretórios para um domínio.

## Adição de diretórios ou SPIs personalizadas {#adding-directories-or-custom-spis}

Para cada domínio enterprise que você configurar, especifique os diretórios que o provedor de autenticação consultará para obter informações do usuário. Você pode adicionar um diretório a um domínio enterprise existente ou a um novo domínio enterprise que está adicionando. Você pode configurar vários diretórios para um domínio. Você também pode configurar um domínio para usar uma SPI (Interface de provedor de serviços) personalizada para sincronização.

### Adicionar um diretório {#add-a-directory}

>[!NOTE]
>
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Clique em Novo Domínio Enterprise ou selecione um domínio enterprise existente.
1. Clique em Add Diretory (Adicionar diretório).
1. Na caixa Nome do perfil, digite um nome para diferenciar esse diretório e clique em Avançar.
1. Defina as definições do servidor de diretório. (Consulte [Configurações de diretório](configuring-directories.md#directory-settings).)
1. Para verificar se uma conexão pode ser estabelecida com o servidor LDAP, clique em Test. Se o teste falhar, revise a exceção no arquivo de log do Servidor de Aplicativos para determinar a causa raiz da falha. Clique em Fechar e em Avançar.
1. Selecione Configurações do usuário e defina as configurações conforme necessário. (Consulte [Configurações de diretório](configuring-directories.md#directory-settings).)
1. Para verificar se o DN de base e outros atributos configurados coletam o lote correto de usuários, clique em Testar. O LDAP tenta recuperar os primeiros 200 registros usando as configurações fornecidas (como DN de base, filtro de pesquisa e todos os atributos).

   Se os usuários forem retornados, os resultados mostrarão os valores atribuídos a cada campo de acordo com o conjunto de atributos. Se o teste falhar devido a um nome de servidor inexistente, informações de autorização incorretas ou atributos incorretos, a seguinte mensagem de erro será exibida: &quot;Os critérios de pesquisa especificados não retornaram nenhum resultado&quot;. Para determinar a causa raiz da falha, revise a exceção no arquivo de log do Servidor de Aplicativos. Clique em Fechar e em Avançar.

1. Selecione Group Settings e defina as configurações conforme necessário. (Consulte [Configurações de diretório](configuring-directories.md#directory-settings).)
1. Para verificar se o DN de base e outros atributos configurados coletam o lote correto de grupos, clique em Testar. Se os grupos forem retornados, os resultados mostrarão os valores atribuídos a cada campo de acordo com o conjunto de atributos. Clique em Fechar.

### Adicionar uma SPI personalizada {#add-a-custom-spi}

Para obter informações sobre como criar uma SPI personalizada, consulte &quot;Desenvolvendo SPIs para formulários AEM&quot; em [Programação com formulários AEM](https://www.adobe.com/go/learn_aemforms_programming_63). Para disponibilizar uma SPI personalizada recém-implantada para associação com o domínio, reinicie o servidor.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Clique em Novo Domínio Enterprise ou selecione um domínio enterprise existente.
1. Clique em Add Diretory (Adicionar diretório).
1. Digite um nome na caixa Nome do perfil, selecione Provedor SPI personalizado e clique em Avançar.
1. Selecione um provedor de usuários personalizado na lista e clique em Avançar.
1. Selecione um provedor de grupo personalizado na lista e clique em Concluir.

## Editar um diretório {#edit-a-directory}

Você pode editar os detalhes de um diretório configurado anteriormente.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Clique no domínio apropriado na lista e, na página exibida, selecione o diretório apropriado na lista.
1. Defina as configurações de diretório, usuário e grupo, conforme necessário. (Consulte [Configurações de diretório](configuring-directories.md#directory-settings).)
1. Clique em OK.

## Excluir um diretório {#delete-a-directory}

Quando você sincroniza seus domínios após excluir um diretório, todos os usuários e grupos nesse diretório são marcados como obsoletos no banco de dados. Eles não serão retornados em nenhuma pesquisa no Console de administração.

>[!NOTE]
>
>Os domínios Enterprise exigem pelo menos um provedor de autenticação e um provedor de diretório.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Clique no domínio apropriado na lista.
1. Marque a caixa de seleção do diretório apropriado e clique em Excluir.
1. Clique em OK na página de confirmação exibida e clique em OK novamente.

## Configurações do diretório {#directory-settings}

Ao adicionar um diretório a um domínio, especifique as configurações de diretório a seguir.

**Servidor:** (Obrigatório) FQDN (nome de domínio totalmente qualificado) do servidor de diretório. Por exemplo, para um computador chamado x na rede adobe.com, o FQDN é x.adobe.com. Um endereço IP pode ser usado no lugar do nome do servidor FQDN.

**Porta:** (obrigatória) a porta usada pelo servidor de diretório. Normalmente 389 ou 636 se o protocolo SSL for usado para enviar informações de autenticação pela rede.

**SSL:** (Obrigatório) Especifica se o servidor de diretório usa SSL ao enviar dados pela rede. O padrão é Não. Quando definido como Sim, o certificado do servidor LDAP correspondente deve ser confiável pelo Java™ runtime environment (JRE) do servidor de aplicativos.

**Associação** (Obrigatório) Especifica como acessar o diretório.

**Anônimo:** nenhum nome de usuário ou senha é necessário. Um usuário anônimo pode conseguir buscar apenas uma quantidade limitada de dados. Essa opção pode ser útil para o teste inicial.

**Usuário:** A autenticação é necessária. Na caixa Nome, especifique o nome do registro do usuário que pode acessar o diretório. É melhor inserir o nome distinto completo (DN) da conta de usuário, como cn=Jane Doe, ou=user, dc=can, dc=com. Na caixa Senha, especifique a senha associada. Essas configurações são necessárias ao selecionar Usuário como a opção de Vinculação.

**Nome:** Nome que pode ser usado para se conectar ao banco de dados LDAP quando o acesso anônimo não está habilitado. Para o Ative Diretory 2003, especifique `[domain name]\[userid]`. Para o Sun™ One, eDirectory ou IBM Tivoli Diretory Server, especifique o nome totalmente qualificado do usuário, como uid=lcuser,ou=it,o=company.com.

**Senha:** Senha que corresponde ao nome que você especificou para se conectar ao banco de dados LDAP quando o acesso anônimo não está habilitado.

**Preencher página com:** quando selecionado, preenche os atributos nas páginas de configurações de usuário e grupo com os valores LDAP padrão correspondentes.

**Recuperar DNs de Base:** Recupera os DNs de base e os exibe na lista suspensa. Essa configuração é útil quando você tem vários DNs de base e precisa selecionar um valor.

**Habilitar referência:** esta configuração é aplicável quando sua organização usa vários domínios do Ative Diretory organizados em uma estrutura hierárquica e você especificou configurações de diretório somente para o domínio pai. Nessa situação, ao selecionar essa opção, o Gerenciamento de usuários pode acessar os detalhes do usuário e do grupo nos domínios secundários.

>[!NOTE]
>
>Clique em Testar para verificar se uma conexão pode ser estabelecida com o servidor LDAP. Para determinar a causa raiz de qualquer falha, revise a exceção no arquivo de log do Servidor de Aplicativos.

### Configurações do usuário {#user-settings}

**Identificador Exclusivo:** (Obrigatório) Um atributo exclusivo e constante usado para identificar usuários. Use um atributo que não seja DN como identificador exclusivo porque o DN de um usuário poderá ser alterado se ele for movido para outra parte da organização. Esta configuração depende do servidor de diretório. O valor é objectGUID para o Ative Diretory 2003, nsuniqueID para o Sun™ One e guid para o eDirectory.

>[!NOTE]
>
>Certifique-se de informar um atributo que seja garantido como exclusivo em sua organização. Inserir um valor incorreto pode causar problemas graves no sistema.

**DN Base:** Definido como o ponto de partida para sincronizar usuários e grupos da hierarquia LDAP. É melhor especificar um DN base no nível mais baixo da hierarquia que abranja todos os usuários e grupos que precisam ser sincronizados para serviços.

Se você selecionou a opção Habilitar referência nas configurações de Diretório, defina a opção DN Base como a parte *dc* do DN. Para que a referência funcione, o intervalo de pesquisa deve incluir domínios pai e filho.

>[!NOTE]
>
>Não inclua o DN do usuário nessa configuração. Para sincronizar um usuário específico, use a configuração Filtro de pesquisa.

Embora o DN de base seja uma configuração obrigatória no console de administração, alguns servidores de diretório, como o IBM Domino Enterprise Server, podem exigir um BaseDN vazio. Para especificar um DN base vazio, exporte o arquivo config.xml, edite a configuração no arquivo config.xml e reimporte-o. (Consulte [Importar e exportar o arquivo de configuração](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**Filtro de Pesquisa:** (Obrigatório) O filtro de pesquisa a ser usado para localizar o registro associado ao usuário. Você pode executar uma pesquisa de um nível ou uma pesquisa de subnível. (Consulte Sintaxe de filtro de pesquisa ou RFC 2254.) Informações adicionais para o esquema do Microsoft AD, consulte Esquema do Ative Diretory.

**Descrição:** Atributo de esquema para a descrição do usuário

**Nome Completo:** (Obrigatório) Atributo de esquema para o nome completo do usuário

**ID de Logon:** (Obrigatório) Atributo de esquema para a ID de logon do usuário

**Sobrenome:** (Obrigatório) Atributo de esquema do sobrenome do usuário

**Nome Fornecido:** (Obrigatório) Atributo de esquema para o nome do usuário

**Iniciais:** Atributo de esquema para as iniciais do usuário

**Calendário Comercial:** permite mapear um calendário comercial para um usuário, com base no valor dessa configuração (a chave do calendário comercial). Os calendários comerciais definem dias úteis e não úteis. Os formulários AEM podem usar calendários comerciais ao calcular datas e horas futuras para eventos, como lembretes, prazos finais e escalonamentos. A forma como você atribui chaves do calendário de negócios aos usuários depende de você estar usando um domínio corporativo, local ou híbrido. (Consulte Configuração de Calendários de Negócios.)

Se você estiver usando um domínio enterprise, poderá mapear a definição Calendário de Negócios para um campo no diretório LDAP. Por exemplo, se cada registro de usuário no diretório contiver um campo *país* e você quiser atribuir calendários de negócios com base no país onde o usuário está localizado, especifique o nome do campo *país* como o valor para a configuração do Calendário de negócios. Em seguida, é possível mapear as chaves do calendário comercial (os valores definidos para o campo *país* no diretório LDAP) para os calendários comerciais no fluxo de trabalho de formulários.

A quantidade de espaço usada para exibir o nome da chave do calendário comercial nas páginas de fluxo de trabalho dos formulários é limitada. Limite o nome da chave do calendário comercial a menos de 53 caracteres para evitar que seja truncada nessas páginas.

**Modificar Carimbo de Data/Hora:** Para habilitar a sincronização do diretório delta, defina esse valor para modificar o Carimbo de Data/Hora. (Consulte Habilitar a sincronização de diretórios delta.)

**Organização:** atributo de esquema do nome da organização à qual o usuário pertence.

**Email Principal:** Atributo de esquema do endereço de email principal do usuário.

**Email Secundário:** atributo de esquema do endereço de email secundário do usuário.

**Telefone:** Atributo de esquema para o número de telefone do usuário.

**Endereço Postal:** Atributo de esquema para o endereço para correspondência do usuário.

**Localidade:** Atributo de esquema que contém as informações de localidade ISO. O valor é um código de idioma de duas letras ou um código de idioma e país.

**Fuso Horário:** Atributo de esquema que contém o fuso horário onde o usuário está localizado. O valor é uma string como Cidade/País.

**Habilitar o Controle VLV (Exibição de Lista Virtual):** um controle LDAP que permite aos formulários AEM recuperar dados em lotes do servidor de diretório. Se você estiver usando o Sun One como o diretório LDAP e o diretório contiver muitos usuários, a ativação do VLV criará um índice que o User Management poderá usar ao pesquisar usuários. Esse recurso é útil ao usar uma conta de usuário normal que pode sincronizar apenas uma quantidade limitada de dados. Você também pode ativar a VLV para grupos. Se você selecionar Ativar Controle de Exibição de Lista Virtual (VLV), especifique um nome na caixa Classificar Campo.

>[!NOTE]
>
>Para habilitar a VLV, configure o Sun One. Consulte [Configurar o Gerenciamento de Usuários para usar o VLV (Modo de Exibição de Lista Virtual)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Campo de Classificação:** Se você selecionou Habilitar Controle de Exibição de Lista Virtual (VLV), especifique o nome do atributo usado para classificar o índice. Esse nome de atributo (como uid) é o que você especificou quando criou um índice para VLV no servidor de diretório.

### Configurações de grupo {#group-settings}

**Identificador Exclusivo:** (Obrigatório) Um atributo exclusivo e constante usado para identificar grupos. Use um atributo não DN como identificador exclusivo. Esta configuração depende do servidor de diretório. O valor é objectGUID para o Ative Diretory 2003, nsuniqueID para o Sun One e guid para o eDirectory.

>[!NOTE]
>
>Certifique-se de informar um atributo que seja garantido como exclusivo em sua organização. Inserir um valor incorreto pode causar problemas graves no sistema.

**DN Base:** (Obrigatório) Nome distinto base do diretório.

Embora o DN de base seja uma configuração obrigatória no console de administração, alguns servidores de diretório, como o IBM Domino Enterprise Server, exigem um BaseDN vazio. Para especificar um DN base vazio, exporte o arquivo config.xml, edite a configuração no arquivo config.xml e reimporte-o. (Consulte [Importar e exportar o arquivo de configuração](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**Filtro de Pesquisa:** (Obrigatório) O filtro de pesquisa a ser usado para localizar o registro associado ao grupo. Você pode executar uma pesquisa de um nível ou uma pesquisa de subnível.

**Descrição:** Atributo de esquema para a descrição do grupo

**Nome Completo:** (Obrigatório) Atributo de esquema para o nome completo do grupo

**DN de Membro:** (Obrigatório) Atributo de esquema para o nome distinto dos membros em um grupo

**Identificador Exclusivo de Membro:** Identificador exclusivo de um usuário ou grupo que é membro do grupo selecionado. Esse valor depende do servidor de diretório. O valor é objectSID para AD2003, nsuniqueID para Sun One e guid para eDirectory.

Se o DN de Membro for especificado com um atributo não DN, o Gerenciamento de Usuários utilizará o Identificador Exclusivo de Membro para consultar o LDAP e coletar o DN do usuário, pois ele corresponde a um valor de identificador exclusivo.

Se o DN for especificado como um identificador exclusivo, não será necessário configurar o Identificador Exclusivo do Membro.

**Organização:** atributo de esquema do nome da organização à qual o grupo pertence

**Email Primário:** Atributo de esquema para o endereço de email primário do grupo

**Email Secundário:** atributo de esquema do endereço de email secundário do grupo

**Modificar Carimbo de Data/Hora:** Para habilitar a sincronização do diretório delta, defina esse valor para modificar o Carimbo de Data/Hora. (Consulte Habilitar a sincronização de diretórios delta.)

**Habilitar o Controle VLV (Exibição de Lista Virtual):** um controle LDAP que permite aos formulários AEM recuperar dados em lotes do servidor de diretório. Se você estiver usando o Sun One como o diretório LDAP e o diretório contiver muitos grupos, a ativação do VLV criará um índice que o User Management poderá usar ao pesquisar grupos. Esse recurso é útil ao usar uma conta de usuário normal que pode sincronizar apenas uma quantidade limitada de dados. Você também pode ativar a VLV para usuários. Se você selecionar Ativar Controle de Exibição de Lista Virtual (VLV), especifique um Nome de Campo de Classificação.

>[!NOTE]
>
>Para habilitar a VLV, configure o Sun One. Consulte [Configurar o Gerenciamento de Usuários para usar o VLV (Modo de Exibição de Lista Virtual)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Classificar Nome do Campo:** Se você selecionou Habilitar Controle de Exibição de Lista Virtual (VLV), especifique o nome de atributo usado para classificar o índice. Esse nome de atributo é o que você especificou quando criou um índice para VLV no servidor de diretório.

>[!NOTE]
>
>Clique em Testar para verificar se as definições de usuário e grupo são coletadas com base no DN de base e nos critérios de pesquisa.

Se usuários e grupos forem retornados, os resultados mostrarão os valores atribuídos a cada campo de acordo com o conjunto de atributos.

>[!NOTE]
>
>O Gerenciamento de usuários não oferece suporte a IDs de usuário duplicadas em um domínio; somente um usuário com a ID é sincronizado.

## Configurar o Gerenciamento de Usuários para usar o Modo de Exibição de Lista Virtual (VLV) {#configure-user-management-to-use-virtual-list-view-vlv}

A sincronização de diretórios é um requisito importante para o Gerenciamento de Usuários. Os usuários e grupos são sincronizados de um diretório corporativo para o banco de dados do AEM Forms para atribuir funções e permissões. O número de usuários varia de 100 a 100.000+, dependendo dos requisitos, e representa um desafio de engenharia para sincronizar dados com eficiência.

O protocolo LDAP fornece um mecanismo para consultar grandes conjuntos de dados de forma paginada usando controles de solicitação. Ao usar o Microsoft Ative Diretory, o LDAP para a sincronização de bancos de dados de formulários AEM usa PagedResultsControl para recuperar dados em lotes de um tamanho específico. O Sun ONE Diretory Server não oferece suporte a esse controle. Para concluir uma consulta paginada em relação ao Sun ONE Diretory Server, use o controle VLV (Exibição de Lista Virtual). Esse controle envolve a configuração do lado do servidor de diretórios e a implementação do lado do cliente.

>[!NOTE]
>
>Esta seção descreve o uso do controle VLV para o Sun ONE Diretory Server. No entanto, você pode usar este controle para qualquer servidor de diretório que suporte o controle VLV.

1. Ao configurar o diretório, selecione Ativar Controle de Exibição de Lista Virtual (VLV) nas páginas Definições do Usuário e Definições de Grupo. Ao marcar a caixa de seleção, você também deve especificar um nome de classificação na caixa Campo de classificação. O valor padrão é uid. (Consulte [Adicionar diretórios ou SPIs personalizados](configuring-directories.md#adding-directories-or-custom-spis) ou [Editar um diretório](configuring-directories.md#edit-a-directory).)
1. Use o console de administração Sun ONE ou um script de linha de comando para criar as entradas VLV LDAP para usuários e grupos. Se você usar um script de linha de comando, poderá usar os arquivos LDIF de exemplo de usuários e grupos. (Consulte [Configurando o Sun ONE Diretory Server para VLV](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv).)
1. Pare o servidor e crie o índice necessário. (Consulte [Criar o Índice de Servidor de Diretório para VLV](configuring-directories.md#create-the-directory-server-index-for-vlv).)

### Configurando o Sun ONE Diretory Server para VLV {#configuring-the-sun-one-directory-server-for-vlv}

A criação de um VLV requer um par de entradas que incluem as classes de objeto `vlvSearch` e `vlvIndex`. A entrada vlvSearch inclui uma base de pesquisa e o atributo `vlvFilter`, que especifica a classe de objeto que contém os atributos que você pretende classificar. A classe de objeto `vlvIndex` inclui o atributo `vlvSort`, que especifica um ou mais atributos para classificar e a ordem em que eles serão classificados. (Um sinal de menos (-) indica ordem alfabética inversa). O uso de formulários VLV com AEM requer entradas separadas para usuários e grupos.

>[!NOTE]
>
>As entradas Object podem ser criadas usando a interface gráfica de usuário (GUI) Sun ONE ou por meio de um script de linha de comando. Para obter instruções sobre como criar as entradas de Objeto usando a GUI, consulte a documentação do Sun ONE.

Este é um exemplo de script LDIF para entrada VLV para usuários:

```text
 dn: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 objectclass: top
 objectclass: vlvSearch
 cn: lcuser
 vlvBase: dc=corp,dc=adobe,dc=com
 vlvScope: 2
 vlvFilter: (&(objectclass=inetOrgPerson))
 aci: (target="ldap:///cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config")(targetattr="*")(version 3.0; acl "Config"
 ;allow(read,search,compare) userdn="ldap:///all"; )
 dn: cn=lcuser,cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 cn: lcuser
 vlvSort: cn
 objectclass: top
 objectclass: vlvIndex
```

**Criar as entradas do objeto usando um script**

1. O exemplo de script tem uma entrada LDAP denominada `lcuser`. Essa entrada é para configuração relacionada ao VLV para sincronização de usuários em formulários AEM. Modifique as seguintes propriedades de acordo:

   **Nome da entrada:** O nome da entrada neste exemplo é `lcuser`. Se `lcuser` for alterado, ele deverá ser alterado em todas as áreas do script de exemplo.

   **vlvBase:** O DN Base especificado na página Configurações do Usuário.

   **vlvFilter:** O Filtro de Pesquisa especificado na página Configurações do Usuário.

   **vlvSort:** O Campo de Classificação especificado na seção de configurações VLV da página Configurações do Usuário. Um controle VLV requer que você especifique um controle de classificação. Esse campo é usado como o parâmetro de classificação para o índice vlv criado.

   **aci:** O controle de acesso especificado no script de exemplo concede a qualquer usuário autenticado o direito de acessar os índices VLV para operações de leitura, pesquisa e comparação. O administrador pode restringir o acesso a um usuário de ligação, que é configurado na página Definições do Servidor de Diretórios especificada na interface do usuário de Gerenciamento de Usuários. Se as permissões não forem fornecidas, a pesquisa de usuários não poderá usar o VLV, e o servidor LDAP acionará uma exceção de permissão.

   >[!NOTE]
   >
   >Como convenção, o nome da entrada vlvIndex também é definido como `lcuser`, mas você pode dar a ele um nome diferente. Use o mesmo nome na ferramenta vlvindex. (Consulte [Criar o Índice de Servidor de Diretório para VLV ](configuring-directories.md#create-the-directory-server-index-for-vlv)*.)*

1. Usando a ferramenta `ldapmodify` fornecida com o Sun ONE Server, crie uma entrada semelhante para grupos usando o DN Base, o Filtro de Pesquisa e o Campo de Classificação do grupo, respectivamente:

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   Por exemplo, digite o seguinte texto:

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### Criar o Índice do Servidor de Diretórios para VLV {#create-the-directory-server-index-for-vlv}

Após definir as definições de diretório e criar as entradas VLV LDAP para usuários e grupos, pare o servidor e crie o índice necessário.

1. Depois de criar entradas de objeto, pare o Sun ONE Server.
1. Usando a ferramenta vlvindex, gere o índice digitando o seguinte texto:

   *instância do servidor de diretórios* `\vlvindex.bat -n userRoot -T lcuser`

   A seguinte saída é gerada:

   ```shell
    D:\tools\ldap\sun\shared\bin>..\..\slapd-chetanmeh-xp3\vlvindex.bat -n userRoot -T livecycle
    [21/Nov/2007:16:47:26 +051800] - userRoot: Indexing VLV: livecycle
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 1000 entries (5%).
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 2000 entries (9%).
    ...
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 20000 entries (94%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 21000 entries (99%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Finished indexing.
   ```

   A ferramenta vlvindex está presente no diretório da instância do servidor de diretórios. Se o Sun ONE Server tiver duas instâncias executando server1 e server2, a ferramenta vlvindex estará no diretório *Sun ONE server*\server1. O valor do parâmetro `-T` é o valor do atributo `cn` da entrada vlvindex criada anteriormente no LDIF de amostra. Nesse caso, é `lcuser`.

1. Se a VLV também estiver ativada para grupos, crie o índice correspondente para os grupos. Verifique se os índices foram criados executando o seguinte comando:

   *sun, um diretório de servidor* `\shared\bin>ldapsearch -h`*nome do host* `-p`*porta nº* `-s base -b "" objectclass=*`

   É gerada uma saída como os seguintes dados de amostra:

   ```shell
    D:\tools\ldap\sun\shared\bin>ldapsearch.exe -h localhost -p 55850 -s base -b "" objectclass=*
    ldapsearch.exe: started Tue Nov 27 16:34:20 2007
    version: 1
    dn:
    objectClass: top
    namingContexts: dc=corp,dc=adobe,dc=com
    supportedExtension: 2.16.840.1.113730.3.5.7
    ...
    vlvsearch: cn=MCC ou=testdata dc=corp dc=adobe dc=com, cn=userRoot,cn=ldbm dat
        abase,cn=plugins,cn=config
    vlvsearch: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
    vlvsearch: cn=Browsing ou=testdata,cn=userRoot,cn=ldbm database,cn=plugins,cn=
        config
    1 matches
   ```
