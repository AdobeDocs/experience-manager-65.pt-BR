---
title: Configuração de diretórios
seo-title: Configuring directories
description: Saiba como adicionar, editar e excluir diretórios e configurar o gerenciamento de usuários para usar a exibição de lista virtual.
seo-description: Learn how to add, edit and delete directories and configure user management to use virtual list view.
uuid: 0bf1a8a7-c917-4248-9937-d24e31c5ba17
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1f15f028-aa81-478e-97eb-f83a4dc0418c
exl-id: 30edcef2-e8fa-403a-9850-b8dfeeb9ac65
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '3227'
ht-degree: 0%

---

# Configuração de diretórios {#configuring-directories}

Para cada domínio empresarial configurado, especifique os diretórios que o provedor de autenticação consulta para informações do usuário. Você pode configurar vários diretórios para um domínio.

## Adicionar diretórios ou SPIs personalizados {#adding-directories-or-custom-spis}

Para cada domínio empresarial configurado, especifique os diretórios que o provedor de autenticação consulta para informações do usuário. Você pode adicionar um diretório a um domínio corporativo existente ou a um novo domínio corporativo que você está adicionando. Você pode configurar vários diretórios para um domínio. Você também pode configurar um domínio para usar uma Interface do Provedor de Serviços personalizada (SPI) para sincronização.

### Adicionar um diretório {#add-a-directory}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique em Novo domínio corporativo ou selecione um domínio corporativo existente.
1. Clique em Adicionar diretório.
1. Na caixa Nome do perfil, digite um nome para distinguir esse diretório e clique em Avançar.
1. Defina as configurações do servidor de diretório. (Consulte [Configurações do diretório](configuring-directories.md#directory-settings).)
1. Para verificar se uma conexão pode ser feita com o servidor LDAP, clique em Testar. Se o teste falhar, analise a exceção no arquivo de log do Servidor de Aplicativos para determinar a causa raiz da falha. Clique em Fechar e em Avançar.
1. Selecione Configurações do usuário e defina as configurações conforme necessário. (Consulte [Configurações do diretório](configuring-directories.md#directory-settings).)
1. Para verificar se o DN de base e outros atributos configurados coletam o lote correto de usuários, clique em Testar. O LDAP tenta recuperar os primeiros 200 registros usando as configurações fornecidas (como o DN de base, filtro de pesquisa e todos os atributos).

   Se os usuários forem retornados, os resultados mostrarão os valores atribuídos a cada campo de acordo com o conjunto de atributos. Se o teste falhar devido a um nome de servidor inexistente, informações de autorização incorretas ou atributos incorretos, a seguinte mensagem de erro será exibida: &quot;Os critérios de pesquisa especificados não retornaram nenhum resultado.&quot; Para determinar a causa raiz da falha, revise a exceção no arquivo de log do Servidor de Aplicativos . Clique em Fechar e em Avançar.

1. Selecione Configurações do grupo e defina as configurações conforme necessário. (Consulte [Configurações do diretório](configuring-directories.md#directory-settings).)
1. Para verificar se o DN de base e outros atributos configurados coletam o lote correto de grupos, clique em Testar. Se grupos forem retornados, os resultados mostrarão os valores atribuídos a cada campo de acordo com o conjunto de atributos. Clique em Fechar.

### Adicionar um SPI personalizado {#add-a-custom-spi}

Para obter informações sobre como criar um SPI personalizado, consulte &quot;Desenvolvimento de SPIs para formulários AEM&quot; em [Programação com formulários AEM](https://www.adobe.com/go/learn_aemforms_programming_63). Para disponibilizar um SPI personalizado recém-implantado para associação com o domínio, reinicie o servidor.

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique em Novo domínio corporativo ou selecione um domínio corporativo existente.
1. Clique em Adicionar diretório.
1. Digite um nome na caixa Nome do perfil, selecione Provedor de SPI personalizado e clique em Avançar.
1. Selecione um provedor de usuário personalizado na lista e clique em Avançar.
1. Selecione um provedor de grupo personalizado na lista e clique em Concluir.

## Editar um diretório {#edit-a-directory}

É possível editar os detalhes de um diretório que você configurou anteriormente.

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique no domínio apropriado na lista e, na página exibida, selecione o diretório apropriado na lista.
1. Configure o diretório, o usuário e o grupo, conforme necessário. (Consulte [Configurações do diretório](configuring-directories.md#directory-settings).)
1. Clique em OK.

## Excluir um diretório {#delete-a-directory}

Ao sincronizar seus domínios após excluir um diretório, todos os usuários e grupos nesse diretório serão marcados como obsoletos no banco de dados. Eles não serão retornados em nenhuma pesquisa pelo Console de administração.

>[!NOTE]
>
>Os domínios da empresa exigem pelo menos um provedor de autenticação e um provedor de diretório.

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique no domínio apropriado na lista.
1. Marque a caixa de seleção do diretório apropriado e clique em Excluir.
1. Clique em OK na página de confirmação que aparece e clique em OK novamente.

## Configurações do diretório {#directory-settings}

Ao adicionar um diretório a um domínio, especifique as seguintes configurações de diretório.

**Servidor:**  (Obrigatório) Nome de domínio totalmente qualificado (FQDN) do servidor de diretório. Por exemplo, para um computador chamado x na rede adobe.com, o FQDN é x.adobe.com. Um endereço IP pode ser usado no lugar do nome do servidor FQDN.

**Porta:** (Obrigatório) A porta que o servidor de diretório usa. Normalmente, 389 ou 636 se o protocolo SSL for usado para enviar informações de autenticação pela rede.

**SSL:** (Obrigatório) Especifica se o servidor de diretório usa SSL ao enviar dados pela rede. O padrão é Não. Quando definido como Sim, o certificado do servidor LDAP correspondente deve ser confiável pelo JRE (Java™ runtime environment) do servidor de aplicativos.

**Vínculo**  (Obrigatório) Especifica como acessar o diretório.

**Anônimo:** não é necessário nenhum nome de usuário ou senha. Um usuário anônimo pode ser capaz de buscar apenas uma quantidade limitada de dados. Essa opção pode ser útil para o teste inicial.

**Usuário:** a autenticação é necessária. Na caixa Nome, especifique o nome do registro do usuário que pode acessar o diretório. É melhor inserir o DN (nome distinto completo) da conta de usuário, como cn=Jane Doe, ou=user, dc=can, dc=com. Na caixa Senha, especifique a senha associada. Essas configurações são necessárias quando você seleciona Usuário como a opção Vínculo.

**Nome:** nome que pode ser usado para se conectar ao banco de dados LDAP quando o acesso anônimo não está habilitado. Para o Ative Diretory 2003, especifique `[domain name]\[userid]`. Para Sun™ One, eDirectory ou IBM Tivoli Diretory Server, especifique o nome totalmente qualificado do usuário, como uid=lcuser, ou=it, o=company.com.

**Senha:** senha que corresponde ao nome especificado para conexão com o banco de dados LDAP quando o acesso anônimo não está ativado.

**Preencher página com:** quando selecionado, preenche os atributos nas páginas de configurações do usuário e do grupo com os valores LDAP padrão correspondentes.

**Recuperar DNs de Base:**  Recupera os DNs de base e os exibe na lista suspensa. Essa configuração é útil quando você tem vários DNs de base e precisa selecionar um valor.

**Habilitar referência:** essa configuração é aplicável quando sua organização usa vários domínios do Ative Diretory organizados em uma estrutura hierárquica e você especificou configurações de diretório somente para o domínio pai. Nessa situação, ao selecionar essa opção, o Gerenciamento de usuários pode acessar detalhes do usuário e do grupo a partir dos domínios filhos.

>[!NOTE]
>
>Clique em Test para verificar se uma conexão pode ser feita com o servidor LDAP. Para determinar a causa raiz de qualquer falha, revise a exceção no arquivo de log do Servidor de Aplicativos .

### Configurações de usuário {#user-settings}

**Identificador exclusivo:**  (Obrigatório) Um atributo exclusivo e constante usado para identificar usuários. Use um atributo não-DN como o identificador exclusivo, pois o DN de um usuário pode ser alterado se mudar para outra parte da organização. Essa configuração depende do servidor de diretório. O valor é objectGUID para o Ative Diretory 2003, nsuniqueID para Sun™ One e guid para eDirectory.

>[!NOTE]
>
>Certifique-se de inserir um atributo que seja exclusivo em sua organização. Inserir um valor incorreto pode causar problemas graves no sistema.

**DN de base:** defina como o ponto de partida para sincronizar usuários e grupos da hierarquia LDAP. É melhor especificar um DN básico no nível mais baixo da hierarquia que abrange todos os usuários e grupos que precisam ser sincronizados para serviços.

Se você selecionou a opção Enable reference nas configurações do Diretório, defina a opção Base DN como a parte *dc* do DN. Para que a referência funcione, o período de pesquisa deve incluir domínios pai e filho.

>[!NOTE]
>
>Não inclua o DN do usuário nessa configuração. Para sincronizar um usuário específico, use a configuração Filtro de pesquisa .

Embora o DN de base seja uma configuração obrigatória no console de administração, alguns servidores de diretório, como o IBM Domino Enterprise Server, podem exigir um BaseDN vazio. Para especificar um DN de base vazio, exporte o arquivo config.xml, edite a configuração no arquivo config.xml e, em seguida, reimporte-o. (Consulte [Importar e exportar o arquivo de configuração](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**Filtro de pesquisa:** (Obrigatório) o filtro de pesquisa a ser usado para localizar o registro associado ao usuário. Você pode realizar uma pesquisa de um nível ou de subnível. (Consulte Sintaxe de filtro de pesquisa ou RFC 2254.) Informações adicionais sobre o esquema Microsoft AD, consulte Esquema do Ative Diretory.

**Descrição:** Atributo de esquema para a descrição do usuário

**Nome completo:** (Obrigatório) Atributo de esquema para o nome completo do usuário

**ID de logon:**  (Obrigatório) Atributo de esquema da ID de logon do usuário

**Sobrenome:**  (Obrigatório) Atributo de esquema do sobrenome do usuário

**Nome fornecido:** (Obrigatório) Atributo de esquema para o nome do usuário

**Iniciais:** atributo de esquema para as iniciais do usuário

**Calendário de negócios:** permite mapear um calendário de negócios para um usuário, com base no valor dessa configuração (a chave do calendário de negócios). Os calendários de negócios definem dias úteis e não úteis. AEM formulários podem usar calendários de negócios ao calcular datas e horários futuros para eventos como lembretes, prazos e escalonamentos. A maneira de atribuir chaves de calendário de negócios aos usuários depende se você está usando um domínio corporativo, local ou híbrido. (Consulte Configuração de Calendários Comerciais.)

Se você estiver usando um domínio corporativo, poderá mapear a configuração do Calendário corporativo para um campo no diretório LDAP. Por exemplo, se cada registro de usuário em seu diretório contiver um campo *country* e você quiser atribuir calendários de negócios com base no país onde o usuário está localizado, especifique o nome do campo *country* como o valor da configuração do Calendário de Negócios. Em seguida, você pode mapear as chaves do calendário de negócios (os valores definidos para o campo *country* no diretório LDAP) para calendários de negócios no fluxo de trabalho de formulários.

A quantidade de espaço usada para exibir o nome da chave do calendário comercial nas páginas do fluxo de trabalho de formulários é limitada. Limite o nome da chave do calendário de negócios a menos de 53 caracteres para evitar truncamento nessas páginas.

**Modificar carimbo de data e hora:** para ativar a sincronização do diretório delta, defina este valor para modificar o TimeStamp. (Consulte Ativar a sincronização de diretórios delta.)

**Organização:** atributo de esquema para o nome da organização à qual o usuário pertence.

**Email principal:** atributo de esquema do endereço de email principal do usuário.

**Email secundário:** atributo de esquema do endereço de email secundário do usuário.

**Telephone:** atributo de schema para o número de telefone do usuário.

**Endereço postal:** Atributo de schema do endereço de correspondência do usuário.

**Localidade:** Atributo de esquema que contém as informações de local ISO. O valor é um código de idioma de duas letras ou um código de idioma e país.

**Fuso horário:** atributo de esquema que contém o fuso horário em que o usuário está localizado. O valor é uma string, como Cidade/País.

**Habilitar controle de Exibição de lista virtual (VLV):**  um controle LDAP que permite que formulários AEM recuperem dados em lotes do servidor de diretório. Se você estiver usando o Sun One como seu diretório LDAP e o diretório contiver muitos usuários, a ativação do VLV criará um índice que o Gerenciamento de usuários poderá usar ao pesquisar usuários. Esse recurso é útil ao usar uma conta de usuário normal que pode sincronizar apenas uma quantidade limitada de dados. Você também pode ativar o VLV para grupos. Se você selecionar Ativar controle de exibição de lista virtual (VLV), especifique um nome na caixa Campo de classificação .

>[!NOTE]
>
>Para ativar o VLV, configure o Sun One. Consulte [Configurar Gerenciamento de Usuário para usar a Exibição de Lista Virtual (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Campo de classificação:** se tiver selecionado Ativar controle de exibição de lista virtual (VLV), especifique o nome do atributo usado para classificar o índice. Esse nome de atributo (como uid) é o especificado ao criar um índice para VLV no servidor de diretório.

### Configurações de grupo {#group-settings}

**Identificador exclusivo:**  (Obrigatório) Um atributo exclusivo e constante usado para identificar grupos. Use um atributo não DN como o identificador exclusivo. Essa configuração depende do servidor de diretório. O valor é objectGUID para o Ative Diretory 2003, nsuniqueID para Sun One e guid para eDirectory.

>[!NOTE]
>
>Certifique-se de inserir um atributo que seja exclusivo em sua organização. Inserir um valor incorreto pode causar problemas graves no sistema.

**DN Base:**  (Obrigatório) Nome distinto base do diretório.

Embora o DN de base seja uma configuração obrigatória no console de administração, alguns servidores de diretório, como o IBM Domino Enterprise Server, exigem um BaseDN vazio. Para especificar um DN de base vazio, exporte o arquivo config.xml, edite a configuração no arquivo config.xml e, em seguida, reimporte-o. (Consulte [Importar e exportar o arquivo de configuração](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**Filtro de pesquisa:** (Obrigatório) o filtro de pesquisa a ser usado para localizar o registro associado ao grupo. Você pode realizar uma pesquisa de um nível ou de subnível.

**Descrição:** Atributo de esquema para a descrição do grupo

**Nome completo:** (Obrigatório) Atributo de esquema para o nome completo do grupo

**DN do Membro:**  (Obrigatório) Atributo de esquema para o nome distinto dos membros de um grupo

**Identificador exclusivo do Membro:** Identificador exclusivo para um usuário ou grupo que é membro do grupo selecionado. Esse valor depende do servidor de diretório. O valor é objectSID para AD2003, nsuniqueID para Sun One e guid para eDirectory.

Se o DN do Membro for especificado com um atributo não DN, o Gerenciamento de Usuários usará o Identificador Exclusivo do Membro para consultar o LDAP para coletar o DN do usuário, pois ele corresponde a um valor de identificador exclusivo.

Se o DN for especificado como um identificador exclusivo, não será necessário configurar o Identificador Exclusivo do Membro.

**Organização:** atributo de esquema para o nome da organização à qual o grupo pertence

**Email principal:** atributo de esquema do endereço de email principal do grupo

**Email secundário:** atributo de esquema do endereço de email secundário do grupo

**Modificar carimbo de data e hora:** para ativar a sincronização do diretório delta, defina este valor para modificar o TimeStamp. (Consulte Ativar a sincronização de diretórios delta.)

**Habilitar controle de Exibição de lista virtual (VLV):**  um controle LDAP que permite que formulários AEM recuperem dados em lotes do servidor de diretório. Se você estiver usando o Sun One como seu diretório LDAP e o diretório contiver muitos grupos, a ativação do VLV criará um índice que o Gerenciamento de usuários poderá usar ao pesquisar grupos. Esse recurso é útil ao usar uma conta de usuário normal que pode sincronizar apenas uma quantidade limitada de dados. Você também pode ativar o VLV para usuários. Se você selecionar Habilitar Controle de Exibição de Lista Virtual (VLV), especifique um Nome do Campo de Classificação.

>[!NOTE]
>
>Para ativar o VLV, configure o Sun One. Consulte [Configurar Gerenciamento de Usuário para usar a Exibição de Lista Virtual (VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**Nome do campo de classificação:** se tiver selecionado Ativar controle de exibição de lista virtual (VLV), especifique o nome do atributo usado para classificar o índice. Esse é o nome de atributo que você especificou quando criou um índice para VLV no servidor de diretório.

>[!NOTE]
>
>Clique em Testar para verificar se as configurações do usuário e do grupo são coletadas com base no DN de base e nos critérios de pesquisa.

Se usuários e grupos forem retornados, os resultados mostrarão os valores atribuídos a cada campo de acordo com o conjunto de atributos.

>[!NOTE]
>
>O Gerenciamento de usuários não oferece suporte a IDs de usuário duplicadas em um domínio; somente um usuário com a ID de usuário é sincronizado.

## Configurar o Gerenciamento de Usuários para usar a Exibição de Lista Virtual (VLV) {#configure-user-management-to-use-virtual-list-view-vlv}

A sincronização de diretórios é um requisito importante para o Gerenciamento de usuários. Os usuários e grupos são sincronizados de um diretório corporativo para o banco de dados de formulários AEM para atribuição de funções e permissões. O número de usuários varia de 100 a 100000+, dependendo dos requisitos, e isso representa um desafio de engenharia para sincronizar os dados com eficiência.

O protocolo LDAP fornece um mecanismo para consultar grandes conjuntos de dados de uma maneira paginada usando controles de solicitação. Ao usar o Microsoft Ative Diretory, o LDAP para AEM a sincronização do banco de dados de formulários usa PagedResultsControl para recuperar dados em lotes de um tamanho específico. O servidor de diretório Sun ONE não suporta este controlo. Para concluir uma consulta paginada em relação ao Sun ONE Diretory Server, use o controle Virtual List View (VLV). Esse controle envolve a configuração do lado do servidor de diretórios e a implementação do lado do cliente.

>[!NOTE]
>
>Esta seção descreve o uso do controle VLV para o Sun ONE Diretory Server. No entanto, você pode usar esse controle para qualquer servidor de diretório que seja compatível com o controle VLV.

1. Ao configurar o diretório, selecione Ativar controle de exibição de lista virtual (VLV) na página Configurações do usuário e na página Configurações do grupo . Ao marcar a caixa de seleção, você também deve especificar um nome de classificação na caixa Campo de classificação . O valor padrão é uid. (Consulte [Adicionar diretórios ou SPIs personalizados](configuring-directories.md#adding-directories-or-custom-spis) ou [Editar um diretório](configuring-directories.md#edit-a-directory).)
1. Use o console de administração Sun ONE ou um script de linha de comando para criar as entradas de VLV LDAP para usuários e grupos. Se você usar um script de linha de comando, poderá usar a amostra de usuários e grupos de arquivos LDIF. (Consulte [Configuração do Sun ONE Diretory Server para VLV](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv).)
1. Pare o servidor e crie o índice necessário. (Consulte [Criar o Índice do Servidor de Diretórios para VLV](configuring-directories.md#create-the-directory-server-index-for-vlv).)

### Configurando o servidor de diretório Sun ONE para VLV {#configuring-the-sun-one-directory-server-for-vlv}

A criação de um VLV requer um par de entradas que incluem as classes de objeto `vlvSearch` e `vlvIndex` . A entrada vlvSearch inclui uma base de pesquisa e o atributo `vlvFilter`, que especifica a classe de objeto que contém os atributos que você pretende classificar. A classe de objeto `vlvIndex` inclui o atributo `vlvSort`, que especifica um ou mais atributos para classificar e a ordem para classificá-los. (Um sinal de menos (-) indica a ordem alfabética inversa). O uso de VLV com formulários de AEM requer entradas separadas para usuários e grupos.

>[!NOTE]
>
>As entradas Object podem ser criadas usando a interface gráfica (GUI) Sun ONE ou por meio de um script de linha de comando. Para obter instruções sobre como criar as entradas de Objeto usando a GUI, consulte a documentação do Sun ONE.

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

**Criar entradas de objeto usando um script**

1. O script de amostra tem uma entrada LDAP chamada `lcuser`. Essa entrada é para configuração relacionada ao VLV para sincronização de usuários em formulários AEM. Modifique as seguintes propriedades adequadamente:

   **Nome da entrada:** o nome da entrada nesta amostra é  `lcuser`. Se `lcuser` for alterado, ele deverá ser alterado em todas as áreas do script de amostra.

   **vlvBase:** O DN Base especificado na página Configurações do Usuário.

   **vlvFilter:** o Filtro de pesquisa especificado na página Configurações do usuário.

   **vlvSort:** O campo de classificação especificado na seção de configurações de VLV da página Configurações do usuário. Um controle VLV requer que você especifique um controle de classificação. Este campo é usado como parâmetro de classificação para o índice vlv criado.

   **aci:** O controle de acesso especificado no script de amostra concede a qualquer usuário autenticado o direito de acessar os índices VLV para operações de leitura, pesquisa e comparação. O administrador pode restringir o acesso a um usuário de vínculo, que é configurado na página Configurações do Servidor de Diretório especificada na interface do usuário Gerenciamento de Usuário. Se as permissões não forem fornecidas, a pesquisa do usuário não poderá usar o VLV e o servidor LDAP lançará uma exceção de permissão.

   >[!NOTE]
   >
   >Como uma convenção, o nome de entrada vlvIndex também é definido como `lcuser`, mas você pode dar a ele um nome diferente. Use o mesmo nome na ferramenta vlvindex. (Consulte [Criar o Índice de Servidor de Diretório para VLV ](configuring-directories.md#create-the-directory-server-index-for-vlv)*.)*

1. Usando a ferramenta `ldapmodify` fornecida com o Sun ONE Server, crie uma entrada semelhante para os grupos usando o DN de Base, o Filtro de Pesquisa e o Campo de Classificação do grupo, respectivamente:

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   Por exemplo, digite o seguinte texto:

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### Criar o Índice do Servidor de Diretórios para VLV {#create-the-directory-server-index-for-vlv}

Depois de definir as configurações do diretório e criar as entradas VLV LDAP para usuários e grupos, pare o servidor e crie o índice necessário.

1. Depois de criar entradas de objeto, pare o servidor Sun ONE.
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

   A ferramenta vlvindex está presente no diretório de instâncias do servidor de diretório. Se o Sun ONE Server tiver duas instâncias executando server1 e server2, a ferramenta vlvindex estará localizada no diretório *Sun ONE server diretory*\server1 . O valor do parâmetro `-T` é o valor do atributo `cn` da entrada vlvindex criada anteriormente no LDIF de amostra. Nesse caso, é `lcuser`.

1. Se o VLV também estiver ativado para grupos, crie o índice correspondente para os grupos. Verifique se os índices foram criados executando o seguinte comando:

   *sun one server diretoryhostnameport no* `\shared\bin>ldapsearch -h`** `-p`** `-s base -b "" objectclass=*`

   A saída, como os seguintes dados de exemplo, é gerada:

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
