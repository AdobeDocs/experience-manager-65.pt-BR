---
title: Gerenciador de pacotes
description: Saiba mais sobre as noções básicas do gerenciamento de pacotes de AEM com o Gerenciador de Pacotes.
feature: Administering
role: Admin
uuid: cba76a5f-5d75-4d63-a0f4-44c13fa1baf2
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6694a135-d1e1-4afb-9f5b-23991ee70eee
docset: aem65
exl-id: e8929d7c-9920-4c02-95a9-6f7f7a365203
source-git-commit: d303a374fd4ab8e398fd909dec4ce6155a2163f5
workflow-type: tm+mt
source-wordcount: '3573'
ht-degree: 1%

---


# Gerenciador de pacotes {#working-with-packages}

Os pacotes permitem a importação e exportação de conteúdo do repositório. Você pode usar pacotes para instalar novo conteúdo, instalar nova funcionalidade, transferir conteúdo entre instâncias e fazer backup do conteúdo do repositório.

Com o Gerenciador de pacotes, você pode transferir pacotes entre a instância do AEM e o sistema de arquivos local para fins de desenvolvimento.

## O que são pacotes? {#what-are-packages}

Um pacote é um arquivo zip com conteúdo de repositório no formulário de serialização do sistema de arquivos, chamado serialização de cofre, fornecendo uma representação fácil de usar e de fácil edição de arquivos e pastas. O conteúdo incluído no pacote é definido usando filtros.

Um pacote também contém informações de metadados de cofre, incluindo as definições de filtro e informações de configuração de importação. Propriedades de conteúdo adicionais, que não são usadas para extração de pacote, podem ser incluídas no pacote, como uma descrição, uma imagem visual ou um ícone. Essas propriedades de conteúdo adicionais são para o consumidor do pacote de conteúdo e somente para fins informativos.

>[!NOTE]
>
>Os pacotes representam a versão atual do conteúdo no momento em que o pacote é criado. Eles não incluem versões anteriores do conteúdo que AEM mantém no repositório.

## Gerenciador de pacotes {#package-manager}

O Gerenciador de Pacotes gerencia os pacotes na instalação do AEM. Depois de [atribuiu as permissões necessárias](#permissions-needed-for-using-the-package-manager) você pode usar o Gerenciador de pacotes para várias ações, incluindo configuração, criação, download e instalação dos seus pacotes.

### Permissões necessárias {#required-permissions}

Para criar, modificar, carregar e instalar pacotes, os usuários devem ter as permissões apropriadas nos seguintes nós:

* Direitos completos excluindo exclusão em `/etc/packages`
* O nó que contém o conteúdo do pacote

>[!CAUTION]
>
>A concessão de permissões para pacotes pode levar à divulgação de informações confidenciais e à perda de dados.
>
>Para limitar esses riscos, é altamente recomendável conceder permissões de grupo específicas somente sobre subárvores dedicadas.

### Acessar o Gerenciador de Pacotes {#accessing}

Você pode acessar o Gerenciador de pacotes de três maneiras:

1. No menu principal AEM -> **Ferramentas** -> **Implantação** -> **Pacotes**
1. De [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) usando a barra do alternador superior
1. Diretamente acessando `http://<host>:<port>/crx/packmgr/`

### Interface do usuário do Gerenciador de pacotes {#ui}

O Gerenciador de pacotes é dividido em quatro áreas funcionais principais:

* **Painel Navegação Esquerdo** - Esse painel permite filtrar e classificar a lista de pacotes.
* **Lista de pacotes** - Esta é a lista de pacotes na sua instância filtrados e classificados por seleções no Painel de Navegação Esquerdo.
* **Log de atividades** - Esse painel é minimizado no início e é expandido para detalhar a atividade do Gerenciador de pacotes, como quando um pacote é criado ou instalado. Há botões adicionais na guia Log de atividades para:
   * **Limpar registro**
   * **Exibir / Ocultar**
* **Barra de ferramentas** - A barra de ferramentas contém botões de atualização para o Painel de navegação esquerdo e a lista Pacote, bem como botões para pesquisar, criar e carregar pacotes.

![Interface do usuário do Gerenciador de pacotes](assets/package-manager-ui.png)

Clicar em uma opção no Painel de navegação esquerdo filtra imediatamente a Lista de pacotes.

Clicar em um nome de pacote expande a entrada na Lista de pacotes para mostrar mais detalhes sobre o pacote.

![Detalhes do pacote expandido](assets/package-expand.png)

Há várias ações que podem ser executadas em um pacote por meio dos botões da barra de ferramentas disponíveis quando os detalhes do pacote são expandidos.

* [Editar](#edit-package)
* [Criar](#building-a-package)
* [Reinstalar](#reinstalling-packages)
* [Download](#downloading-packages-to-your-file-system)
* [Compartilhar](#share)

Outras ações estão disponíveis abaixo da variável **Mais** botão.

* [Excluir](#deleting-packages)
* [Cobertura](#package-coverage)
* [Conteúdo](#viewing-package-contents-and-testing-installation)
* [Reajustar](#rewrapping-a-package)
* [Outras versões](#other-versions)
* [Desinstalar](#uninstalling-packages)
* [Testar instalação](#viewing-package-contents-and-testing-installation)
* [Validar](#validating-packages)
* [Replicar](#replicating-packages)

### Status do pacote {#package-status}

Cada entrada na lista de pacotes tem um indicador de status para que você saiba rapidamente o status do pacote. Passar o mouse sobre o status revela uma dica de ferramenta com os detalhes do status.

![Status do pacote](assets/package-status.png)

Se o pacote tiver sido alterado ou não tiver sido criado, o status será apresentado como um link para tomar uma ação rápida para reconstruir ou instalar o pacote.

## Configurações do pacote {#package-settings}

Um pacote é essencialmente um conjunto de filtros e os dados do repositório com base nesses filtros. Usando a interface do usuário do Gerenciador de pacotes, você pode clicar em um pacote e, em seguida, na função **Editar** para visualizar os detalhes de um pacote, incluindo as configurações a seguir.

* [Configurações gerais](#general-settings)
* [Filtros do pacote](#package-filters)
* [Dependências do pacote](#package-dependencies)
* [Configurações avançadas](#advanced-settings)
* [Capturas de tela do pacote](#package-screenshots)

### Configurações gerais {#general-settings}

É possível editar várias configurações de pacote para definir informações, como descrição do pacote, dependências e detalhes do provedor.

O **Configurações do pacote** está disponível por meio do **Editar** botão quando [criação](#creating-a-new-package) ou [edição](#viewing-and-editing-package-information) um pacote. Depois de fazer qualquer alteração, clique em **Salvar**.

![Caixa de diálogo Editar pacote, configurações gerais](assets/general-settings.png)

| Texto | Descrição |
|---|---|
| Nome | O nome do pacote |
| Grupo | Para organizar pacotes, você pode digitar o nome de um novo grupo ou selecionar um grupo existente |
| Versão | Texto a ser usado para a versão |
| Descrição | Breve descrição do pacote que permite a marcação de HTML para formatação |
| Miniatura  | O ícone que aparece com a listagem de pacotes |

#### Miniaturas do pacote {#thumbnails}

Uma miniatura fornece uma representação visual de referência rápida do que o pacote contém. Isso é mostrado na lista de pacotes e pode ajudar a identificar facilmente o pacote ou a classe do pacote.

Os exemplos de convenções a seguir são usados para as embalagens oficiais:

Hotfix oficial

![Miniatura do hotfix oficial](assets/official-hotfix.png)

Instalação oficial AEM da extensão

![Miniatura da instalação ou extensão do AEM oficial](assets/official-installation.png)

Service Pack Oficial

![Ícone oficial AEM service pack](assets/official-service-pack.png)

Use um ícone exclusivo para o seu pacote. Não reutilize um ícone utilizado por Adobe.

### Filtros do pacote {#package-filters}

Os filtros identificam os nós do repositório a serem incluídos no pacote. A **Definição de filtro** especifica as seguintes informações:

* O **Caminho raiz** do conteúdo a ser incluído
* **Regras** que incluem ou excluem nós específicos abaixo do caminho raiz

Adicionar regras usando o **+** botão. Remova regras usando o **-** botão.

As regras são aplicadas de acordo com sua ordem, de forma que sejam posicionadas conforme necessário usando a variável **Up** e **Down** botões de seta.

Os filtros podem incluir zero ou mais regras. Quando nenhuma regra é definida, o pacote contém todo o conteúdo abaixo do caminho raiz.

É possível definir uma ou mais definições de filtro para um pacote. Use mais de um filtro para incluir conteúdo de vários caminhos raiz.

![Guia Filtros](assets/edit-filter.png)

Ao criar filtros, você pode definir um caminho ou usar uma expressão regular para especificar todos os nós que deseja incluir ou excluir.

| Tipo de regra | Descrição |
|---|---|
| include | A inclusão de um diretório incluirá esse diretório e todos os arquivos e pastas nesse diretório (ou seja, toda a subárvore), mas **não** inclua outros arquivos ou pastas de abaixo do caminho raiz especificado. |
| excluir | A exclusão de um diretório excluirá esse diretório e todos os arquivos e pastas nesse diretório (ou seja, toda a subárvore). |

Os filtros de pacote são definidos com mais frequência ao [crie o pacote.](#creating-a-new-package) No entanto, eles também podem ser editados posteriormente, depois disso, o pacote deve ser recriado para atualizar seu conteúdo com base nas novas definições de filtro.

>[!TIP]
>
>Um pacote pode conter várias definições de filtro para que nós de locais diferentes possam ser facilmente combinados em um pacote.

### Dependências {#dependencies}

![Guia Dependências](assets/dependencies.png)

| Texto | Descrição | Exemplo/Detalhes |
|---|---|---|
| Testada com | O nome e a versão do produto com os quais este pacote é direcionado ou compatível. | `6.5` |
| Problemas corrigidos | Um campo de texto que permite listar detalhes de bugs corrigidos com este pacote, um bug por linha | - |
| Depende de | Lista outros pacotes necessários para que o pacote atual seja executado como esperado quando instalado | `groupId:name:version` |
| Substitui | Uma lista de pacotes obsoletos que este pacote substitui | `groupId:name:version` |

### Configurações avançadas {#advanced-settings}

![Guia Configurações avançadas](assets/advanced-settings.png)

| Texto | Descrição | Exemplo/Detalhes |
|---|---|---|
| Nome | O nome do provedor do pacote | `WKND Media Group` |
| URL | URL do provedor | `https://wknd.site` |
| Link | Link específico do pacote para uma página de provedor | `https://wknd.site/package/` |
| Exige | Define se há restrições ao instalar o pacote | **Administrador** - O pacote só deve ser instalado com privilégios de administrador <br>**Reiniciar** - AEM deve ser reiniciado após a instalação do pacote |
| Reparação de AC | Especifica como as informações de controle de acesso definidas no pacote são tratadas quando o pacote é importado | **Ignorar** - Preservar ACLs no repositório <br>**Substituir** - Substituir ACLs no repositório <br>**Mesclar** - Mesclar ambos os conjuntos de ACLs <br>**MergePreserve** - Mesclar o controle de acesso no conteúdo com o fornecido com o pacote adicionando as entradas de controle de acesso de principais não presentes no conteúdo <br>**Limpar** - Limpar ACLs |

### Capturas de tela do pacote {#package-screenshots}

Você pode anexar várias capturas de tela ao seu pacote para fornecer uma representação visual de como o conteúdo é exibido.

![Guia Capturas de tela](assets/screenshots.png)

## Ações do pacote {#package-actions}

Há muitas ações que podem ser realizadas em um pacote.

### Criação de um pacote {#creating-a-new-package}

1. [Acesse o Gerenciador de Pacotes.](#accessing)

1. Clique em **Criar pacote**.

   >[!TIP]
   >
   >Se a instância tiver muitos pacotes, pode haver uma estrutura de pastas em vigor. Nesses casos, é mais fácil navegar para a pasta de destino necessária antes de criar o novo pacote.

1. No **Novo pacote** digite os seguintes campos:

   ![Caixa de diálogo Novo pacote](assets/new-package-dialog.png)

   * **Nome do pacote** - Selecione um nome descritivo para ajudá-lo (e outros) a identificar facilmente o conteúdo do pacote.

   * **Versão** - Este é um campo textual para que você indique uma versão. Isso é anexado ao nome do pacote para formar o nome do arquivo zip.

   * **Grupo** - Este é o nome do grupo de destino (ou pasta). Os grupos ajudam a organizar seus pacotes. Uma pasta é criada para o grupo se ele ainda não existir. Se deixar o nome do grupo em branco, ele criará o pacote na lista de pacotes principais.

1. Clique em **OK** para criar o pacote.

1. AEM lista o novo pacote na parte superior da lista de pacotes.

   ![Novo pacote](assets/new-package.png)

1. Clique em **Editar** para definir a variável [conteúdo do pacote.](#package-contents) Clique em **Salvar** depois que terminar de editar as configurações.

1. Agora você pode [Criar](#building-a-package) seu pacote.

Não é obrigatório construir imediatamente o pacote após a sua criação. Um pacote não criado não contém conteúdo e consiste apenas nos dados de filtro e outros metadados do pacote.

### Criação de um pacote {#building-a-package}

Geralmente, um pacote é criado ao mesmo tempo que você [criar o pacote](#creating-a-new-package), mas você pode retornar posteriormente para criar ou recriar o pacote. Isso pode ser útil se o conteúdo no repositório tiver sido alterado ou se os filtros do pacote tiverem sido alterados.

1. [Acesse o Gerenciador de Pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Clique em **Criar**. Uma caixa de diálogo solicita a confirmação de que você deseja criar o pacote, pois qualquer conteúdo existente do pacote será substituído.

1. Clique em **OK**. AEM cria o pacote, listando todo o conteúdo adicionado ao pacote da mesma forma que faz na lista de atividades. Ao concluir o AEM, você exibe uma confirmação de que o pacote foi criado e (ao fechar a caixa de diálogo) atualiza as informações da lista de pacotes.

### Editar um pacote {#edit-package}

Depois que um pacote é carregado para o AEM, você pode modificar suas configurações.

1. [Acesse o Gerenciador de Pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Clique em **Editar** e atualize o **[Configurações do pacote](#package-settings)** conforme necessário.

1. Clique em **Salvar** para salvar.

Pode ser necessário [recrie o pacote](#building-a-package) para atualizar seu conteúdo com base nas alterações feitas.

### Reembrulhar um pacote {#rewrapping-a-package}

Depois que um pacote é criado, ele pode ser reembutido. Rewrapping altera as informações do pacote sem precisar, como miniatura, descrição etc., sem alterar o conteúdo do pacote.

1. [Acesse o Gerenciador de Pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Clique em **Editar** e atualize o **[Configurações do pacote](#package-settings)** conforme necessário.

1. Clique em **Salvar** para salvar.

1. Clique em **Mais** -> **Reembrulhar** e uma caixa de diálogo pedirá confirmação.

### Exibição de outras versões de pacote {#other-versions}

Como cada versão de um pacote é exibida na lista como qualquer outro pacote, o Gerenciador de pacotes pode encontrar outras versões de um pacote selecionado.

1. [Acesse o Gerenciador de Pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Clique em **Mais** -> **Outras versões** e uma caixa de diálogo é aberta com uma lista de outras versões do mesmo pacote com informações de status.

### Visualização do conteúdo do pacote e teste da instalação {#viewing-package-contents-and-testing-installation}

Após a criação de um pacote, é possível visualizar o conteúdo.

1. [Acesse o Gerenciador de Pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Para exibir o conteúdo, clique em **Mais** -> **Conteúdo** e o Gerenciador de pacotes lista todo o conteúdo do pacote no log de atividades.

   ![Conteúdo do pacote](assets/package-contents.png)

1. Para executar uma simulação de instalação, clique em **Mais** -> **Instalar teste** O e o Gerenciador de pacotes informam no registro de atividades os resultados como se a instalação tivesse sido executada.

   ![Instalação de teste](assets/test-install.png)

### Fazendo download de pacotes no seu sistema de arquivos {#downloading-packages-to-your-file-system}

1. [Acesse o Gerenciador de Pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Clique no botão **Baixar** ou o nome do arquivo vinculado do pacote na área de detalhes do pacote.

1. AEM baixa o pacote no computador.

### Compartilhamento de um pacote {#share}

O Compartilhamento de pacotes era um serviço público centralizado para distribuir pacotes de conteúdo. O Compartilhamento de pacotes foi substituído por [Distribuição de software](#software-distribution) e esse botão não funciona mais.

### Fazer upload de pacotes do seu sistema de arquivos {#uploading-packages-from-your-file-system}

1. [Acesse o Gerenciador de Pacotes.](#accessing)

1. Selecione a pasta do grupo na qual deseja que o pacote seja carregado.

1. Clique no botão **Fazer upload do pacote** botão.

1. Forneça as informações necessárias sobre o pacote carregado.

   ![Caixa de diálogo de upload do pacote](assets/package-upload-dialog.png)

   * **Embalagem** - Use o **Procurar...** para selecionar o pacote necessário do sistema de arquivos local.
   * **Forçar upload** - Se um pacote com esse nome já existir, essa opção força o upload e substitui o pacote existente.

1. Clique em **OK** e o pacote selecionado é carregado e a lista de pacotes é atualizada adequadamente.

O conteúdo do pacote agora existe em AEM, mas para torná-lo disponível para uso, certifique-se de [instale o pacote](#installing-packages).

### Validação de pacotes {#validating-packages}

Como os pacotes podem modificar o conteúdo existente, geralmente é útil validar essas alterações antes de instalar.

#### Opções de validação {#validation-options}

O Gerenciador de pacotes pode executar as seguintes validações:

* [Importações de pacotes OSGi](#osgi-package-imports)
* [Sobreposições](#overlays)
* [ACLs](#acls)

##### Validar importações do pacote OSGi {#osgi-package-imports}

**O que está marcado**

Essa validação inspeciona o pacote de todos os arquivos JAR (pacotes OSGi), extrai seus `manifest.xml` (que contém as dependências com versão em que o pacote OSGi depende) e verifica as exportações da instância AEM feitas dependências com as versões corretas.

**Como é reportado**

Todas as dependências com versão que não possam ser atendidas pela instância de AEM são listadas no Log de atividades do Gerenciador de pacotes.

**Estados de erro**

Se as dependências não forem atendidas, os pacotes OSGi no pacote com essas dependências não serão iniciados. Isso resulta em uma implantação de aplicativo interrompida, pois qualquer coisa que dependa do pacote OSGi não iniciado, por sua vez, não funcionará corretamente.

**Resolução de Erro**

Para resolver erros devido a pacotes OSGi insatisfeitos, a versão de dependência no pacote com importações insatisfeitas deve ser ajustada.

##### Validar sobreposições {#overlays}

**O que está marcado**

Essa validação determina se o pacote que está sendo instalado contém um arquivo que já está sobreposto na instância de destino AEM.

Por exemplo, considerando uma sobreposição existente em `/apps/sling/servlet/errorhandler/404.jsp`, um pacote que contém `/libs/sling/servlet/errorhandler/404.jsp`, de forma que altere o arquivo existente em `/libs/sling/servlet/errorhandler/404.jsp`.

**Como é reportado**

Essas sobreposições são descritas no Log de atividades do Gerenciador de pacotes.

**Estados de erro**

Um estado de erro significa que o pacote está tentando implantar um arquivo que já está sobreposto, portanto, as alterações no pacote serão sobrepostas (e, portanto, &quot;ocultas&quot;) pela sobreposição e não terão efeito.

**Resolução de Erro**

Para resolver esse problema, o mantenedor do arquivo de sobreposição em `/apps` deve revisar as alterações no arquivo sobreposto em `/libs` e incorpore as alterações conforme necessário na sobreposição ( `/apps`) e reimplante o arquivo sobreposto.

>[!NOTE]
>
>O mecanismo de validação não tem como reconciliar se o conteúdo sobreposto foi incorporado corretamente no arquivo de sobreposição. Por conseguinte, esta validação continuará a apresentar relatórios sobre conflitos mesmo depois de terem sido efetuadas as alterações necessárias.

##### Validar ACLs {#acls}

**O que está marcado**

Essa validação verifica quais permissões estão sendo adicionadas, como serão tratadas (mesclar/substituir) e se as permissões atuais serão afetadas.

**Como é reportado**

As permissões são descritas no Log de atividades do Gerenciador de pacotes.

**Estados de erro**

Não é possível fornecer erros explícitos. A validação simplesmente indica se qualquer nova permissão ACL será adicionada ou afetada pela instalação do pacote.

**Resolução de Erro**

Usando as informações fornecidas pela validação, os nós afetados podem ser revisados no CRXDE e as ACLs podem estar ajustando no pacote conforme necessário.

>[!CAUTION]
>
>Como prática recomendada, é recomendável que os pacotes não afetem as ACLs fornecidas AEM, pois isso pode resultar em comportamento inesperado.

#### Executando validação {#performing-validation}

A validação dos pacotes pode ser feita de duas maneiras diferentes:

* [Por meio da interface do usuário do Gerenciador de pacotes](#via-package-manager)
* [Por meio de solicitação HTTP POST, como com cURL](#via-post-request)

A validação deve sempre ocorrer após o upload do pacote, mas antes da instalação.

##### Validação de Pacote Via Gerenciador de Pacotes {#via-package-manager}

1. [Acesse o Gerenciador de Pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Para validar o pacote, clique em **Mais** -> **Validar**,

1. Na caixa de diálogo modal que aparece, use as caixas de seleção para selecionar os tipos de validação e iniciar a validação clicando em **Validar**.

1. As validações escolhidas são executadas e os resultados são exibidos no Log de atividades do Gerenciador de pacotes.

##### Validação de pacote por solicitação POST HTTP {#via-post-request}

A solicitação POST assume o seguinte formulário.

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

O `type` pode ser qualquer lista desordenada, separada por vírgulas, consistindo em:

* `osgiPackageImports`
* `overlays`
* `acls`

O valor de `type` o padrão é `osgiPackageImports` se não tiver sido transmitido explicitamente.

Ao usar cURL, execute uma instrução semelhante ao seguinte:

```shell
curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
```

Ao validar por meio da solicitação POST, a resposta é enviada de volta como um objeto JSON.

### Visualização da cobertura do pacote {#package-coverage}

Os pacotes são definidos por seus filtros. Você pode fazer com que o Gerenciador de pacotes aplique filtros de um pacote ao seu conteúdo de repositório existente para mostrar qual conteúdo do repositório é coberto pela definição de filtro do pacote.

1. [Acesse o Gerenciador de Pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Clique em **Mais** -> **Cobertura**.

1. Os detalhes de cobertura estão listados no Log de atividades.

### Instalação de pacotes {#installing-packages}

Fazer upload de um pacote apenas adiciona o conteúdo do pacote ao repositório, mas ele não está acessível. Você deve instalar o pacote carregado para usar o conteúdo do pacote.

>[!CAUTION]
>
>A instalação de um pacote pode substituir ou excluir o conteúdo existente. Faça upload de um pacote somente se tiver certeza de que ele não exclui ou substitui o conteúdo necessário.

Antes da instalação do seu pacote, o Gerenciador de pacotes cria automaticamente um pacote de instantâneos que contém o conteúdo que será substituído. Esse instantâneo será reinstalado se você desinstalar o pacote.

1. [Acesse o Gerenciador de Pacotes.](#accessing)

1. Abra os detalhes do pacote que deseja instalar na lista de pacotes clicando no nome do pacote.

1. Clique no botão **Instalar** nos detalhes do item ou na variável **Instalar** no status do pacote.

1. Uma caixa de diálogo solicitará a confirmação e permitirá que outras opções sejam especificadas.

   * **Extrair somente** - Extraia o pacote somente para que nenhum instantâneo seja criado e, portanto, a desinstalação não será possível
   * **Salvar limite** - Número de nós transitórios até que o salvamento automático seja acionado (aumente se você encontrar exceções de modificação simultâneas)
   * **Extrair Subpacotes** - Habilitar a extração automática de subpacotes
   * **Manuseio de Controle de Acesso** - Especifica como as informações de controle de acesso definidas no pacote são tratadas quando o pacote é instalado (as opções são as mesmas do pacote [configurações avançadas do pacote](#advanced-settings))
   * **Manuseio de Dependências** - Especificar como as dependências são tratadas durante a instalação

1. Clique em **Instalar**.

1. O registro de atividades detalha o progresso da instalação.

>[!CAUTION]
>
>* Se você estiver instalando ativos digitais, deverá:
   >  Primeiro, desative o WorkflowLauncher.
   >  Use a opção de menu Componentes do console OSGi para desativar
   >  `com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl.`
>* Em seguida, quando a instalação for concluída, reative o WorkflowLauncher.
>
>Desativar o WorkflowLauncher garante que a estrutura do importador de Ativos não manipule (involuntariamente) os ativos na instalação.

Quando a instalação for concluída e bem-sucedida, a lista de pacotes será atualizada e a palavra **Instalado** aparece no status do pacote.

### Reinstalar pacotes {#reinstalling-packages}

A reinstalação de pacotes executa as mesmas etapas em um pacote já instalado que são processadas ao [instalando inicialmente o pacote.](#installing-packages)

### Upload e instalação baseados no sistema de arquivos {#file-system-based-upload-and-installation}

Você pode abandonar completamente o Gerenciador de pacotes ao instalar os pacotes. AEM pode detectar pacotes colocados em um local específico no sistema de arquivos local do computador host e fazer upload e instalação automaticamente.

1. Na pasta de instalação do AEM, há um `crx-quicksart` ao lado do jar e `license.properties` arquivo. Crie uma pasta chamada `install` under `crx-quickstart` resultando no caminho `<aem-home>/crx-quickstart/install`.

1. Nesta pasta, adicione seus pacotes. Eles serão carregados e instalados automaticamente na sua instância.

1. Quando o upload e a instalação estiverem concluídos, você poderá ver os pacotes no Gerenciador de pacotes como se tivesse usado a interface do usuário do Gerenciador de Pacotes para instalá-los.

Se a instância estiver em execução, o upload e a instalação começarão imediatamente quando você adicioná-los ao pacote na `install` pasta

Se a instância não estiver em execução, os pacotes serão colocados no `install` são instaladas na inicialização em ordem alfabética.

### Desinstalação de pacotes {#uninstalling-packages}

A desinstalação do pacote reverte o conteúdo do repositório para o instantâneo feito automaticamente pelo Gerenciador de pacotes antes da instalação.

1. [Acesse o Gerenciador de Pacotes.](#accessing)

1. Abra os detalhes do pacote que deseja desinstalar na lista de pacotes clicando no nome do pacote.

1. Clique em **Mais** -> **Desinstalar**, para remover o conteúdo deste pacote do repositório.

1. Uma caixa de diálogo solicitará a confirmação e listará todas as alterações feitas.

1. O pacote é removido e o instantâneo é aplicado. O andamento do processo é mostrado no Log de atividades.

### Exclusão de pacotes {#deleting-packages}

A exclusão de um pacote exclui somente seus detalhes do Gerenciador de Pacotes. Se este pacote já tiver sido instalado, o conteúdo instalado não será excluído.

1. [Acesse o Gerenciador de Pacotes.](#accessing)

1. Abra os detalhes do pacote que deseja excluir da lista de pacotes clicando no nome do pacote.

1. O Gerenciador de pacotes solicita a confirmação de que você deseja excluir o pacote. Clique em **OK** para confirmar a exclusão.

1. As informações do pacote são excluídas e os detalhes são relatados no Log de atividades.

### Replicação de pacotes {#replicating-packages}

Replicar o conteúdo de um pacote para instalá-lo na instância de publicação.

1. [Acesse o Gerenciador de Pacotes.](#accessing)

1. Abra os detalhes do pacote que deseja replicar da lista de pacotes clicando no nome do pacote.

1. Clique em **Mais** -> **Replicar**.

1. O pacote é replicado e os detalhes são relatados no Log de atividades.

## Distribuição de software {#software-distribution}

AEM Pacotes podem ser usados para criar e compartilhar conteúdo em ambientes AEM.

[Distribuição de software](https://downloads.experiencecloud.adobe.com) O é um serviço centralizado projetado para simplificar a pesquisa e o download de pacotes de AEM.

Para obter mais informações, consulte o [Documentação de distribuição de software.](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html)

>[!NOTE]
>
>No momento, o Gerenciador de pacotes não está integrado à Distribuição de software, como estava no antigo serviço Compartilhamento de pacotes. Portanto, os botões de compartilhamento e outros links para o Compartilhamento de pacotes no Gerenciador de pacotes não funcionam mais. A solução é baixar pacotes no disco local.
