---
title: Gerenciador de pacotes
description: Saiba mais sobre as noções básicas do gerenciamento de pacotes AEM com o Gerenciador de pacotes.
feature: Administering
role: Admin
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
docset: aem65
exl-id: e8929d7c-9920-4c02-95a9-6f7f7a365203
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '3565'
ht-degree: 1%

---


# Gerenciador de pacotes {#working-with-packages}

Os pacotes permitem importar e exportar conteúdo do repositório. Você pode usar pacotes para instalar novo conteúdo, instalar nova funcionalidade, transferir conteúdo entre instâncias e fazer backup do conteúdo do repositório.

Com o Gerenciador de pacotes, é possível transferir pacotes entre a instância do AEM e o sistema de arquivos local para fins de desenvolvimento.

## O que são pacotes? {#what-are-packages}

Um pacote é um arquivo zip que contém o conteúdo do repositório no formato de serialização de sistemas de arquivos, chamado de serialização do Vault, fornecendo uma representação fácil de usar e editar de arquivos e pastas. O conteúdo incluído no pacote é definido usando filtros.

Um pacote também contém informações meta do Vault, incluindo as definições de filtro e as informações de configuração de importação. As propriedades de conteúdo adicionais, que não são usadas para a extração de pacotes, podem ser incluídas no pacote, como uma descrição, uma imagem visual ou um ícone. Essas propriedades de conteúdo adicionais são apenas para o consumidor do pacote de conteúdo e para fins informativos.

>[!NOTE]
>
>Os pacotes representam a versão atual do conteúdo no momento em que o pacote é criado. Eles não incluem nenhuma versão anterior do conteúdo que o AEM mantém no repositório.

## Gerenciador de pacotes {#package-manager}

O Gerenciador de pacotes gerencia os pacotes na instalação do AEM. Depois de ter [foram atribuídas as permissões necessárias](#permissions-needed-for-using-the-package-manager) você pode usar o Gerenciador de pacotes para várias ações, incluindo configuração, criação, download e instalação de pacotes.

### Permissões necessárias {#required-permissions}

Para criar, modificar, fazer upload e instalar pacotes, os usuários devem ter as permissões apropriadas nos seguintes nós:

* Direitos totais, excluindo exclusão em `/etc/packages`
* O nó que contém o conteúdo do pacote

>[!CAUTION]
>
>A concessão de permissões para pacotes pode levar à divulgação de informações confidenciais e perda de dados.
>
>Para limitar esses riscos, é altamente recomendável conceder permissões de grupo específicas somente sobre subárvores dedicadas.

### Acessar o Gerenciador de pacotes {#accessing}

Você pode acessar o Gerenciador de pacotes de três maneiras:

1. No menu principal do AEM > **Ferramentas** > **Implantação** > **Pacotes**
1. De [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) usando a barra superior do alternador
1. Diretamente ao acessar `http://<host>:<port>/crx/packmgr/`

### Interface do usuário do Gerenciador de pacotes {#ui}

O Gerenciador de pacotes está dividido em quatro áreas funcionais principais:

* **Painel de navegação esquerdo** - Esse painel permite filtrar e classificar a lista de pacotes.
* **Lista de pacotes** - Esta é a lista de pacotes na sua instância filtrada e classificada de acordo com as seleções no Painel de navegação esquerdo.
* **Log de atividades** - Esse painel é minimizado no início e expande-se para detalhar a atividade do Gerenciador de pacotes, como quando um pacote é criado ou instalado. Há botões adicionais na guia Registro de atividades para:
   * **Limpar registro**
   * **Mostrar/Ocultar**
* **Barra de ferramentas** - A barra de ferramentas contém botões de atualização para o Painel de navegação esquerdo e a lista Pacote e botões para pesquisar, criar e fazer upload de pacotes.

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

Outras ações estão disponíveis abaixo de **Mais** botão.

* [Excluir](#deleting-packages)
* [Abrangência](#package-coverage)
* [Conteúdo](#viewing-package-contents-and-testing-installation)
* [Reajustar](#rewrapping-a-package)
* [Outras versões](#other-versions)
* [Desinstalar](#uninstalling-packages)
* [Testar instalação](#viewing-package-contents-and-testing-installation)
* [Validar](#validating-packages)
* [Replicar](#replicating-packages)

### Status do pacote {#package-status}

Cada entrada na lista de pacotes tem um indicador de status para informar rapidamente o status do pacote. Passar o mouse sobre o status revela uma dica de ferramenta com os detalhes do status.

![Status do pacote](assets/package-status.png)

Se o pacote tiver sido alterado ou nunca tiver sido criado, o status será apresentado como um link para executar uma ação rápida para recriar ou instalar o pacote.

## Configurações do pacote {#package-settings}

Um pacote é essencialmente um conjunto de filtros e os dados do repositório com base nesses filtros. Usando a interface do usuário do Gerenciador de pacotes, você pode clicar em um pacote e, em seguida, na **Editar** botão para exibir os detalhes de um pacote incluindo as configurações a seguir.

* [Configurações gerais](#general-settings)
* [Filtros do pacote](#package-filters)
* [Dependências de pacote](#package-dependencies)
* [Configurações avançadas](#advanced-settings)
* [Capturas de tela do pacote](#package-screenshots)

### Configurações gerais {#general-settings}

É possível editar uma variedade de configurações de pacote para definir informações como descrição do pacote, dependências e detalhes do provedor.

A variável **Configurações do pacote** está disponível por meio da **Editar** botão quando [criando](#creating-a-new-package) ou [edição](#viewing-and-editing-package-information) um pacote. Depois que as alterações forem feitas, clique em **Salvar**.

![Caixa de diálogo Editar pacote, configurações gerais](assets/general-settings.png)

| Texto | Descrição |
|---|---|
| Nome | O nome do pacote |
| Grupo | Para organizar pacotes, digite o nome de um novo grupo ou selecione um grupo existente |
| Versão | Texto a ser usado para a versão |
| Descrição | Uma breve descrição do pacote que permite a marcação HTML para formatação |
| Miniatura  | O ícone que aparece com a lista de pacotes |

#### Miniaturas do pacote {#thumbnails}

Uma miniatura fornece uma representação visual de referência rápida do que o pacote contém. Isso é mostrado na lista de pacotes e pode ajudar a identificar facilmente o pacote ou a classe do pacote.

A seguir estão exemplos de convenções usadas para pacotes oficiais:

Hotfix oficial

![Miniatura de hotfix oficial](assets/official-hotfix.png)

Instalação oficial do AEM de extensão

![Instalação oficial do AEM ou miniatura de extensão](assets/official-installation.png)

Service Pack Oficial

![Ícone oficial do service pack do AEM](assets/official-service-pack.png)

Use um ícone exclusivo para seu pacote. Não reutilize um ícone usado pelo Adobe.

### Filtros do pacote {#package-filters}

Os filtros identificam os nós de repositório a serem incluídos no pacote. A **Definição de filtro** especifica as seguintes informações:

* A variável **Caminho raiz** do conteúdo a ser incluído
* **Regras** que incluem ou excluem nós específicos abaixo do caminho raiz

Adicionar regras usando o **+** botão. Remover regras usando o **-** botão.

As regras são aplicadas de acordo com sua ordem, posicionando-as conforme necessário usando a **Para cima** e **Para baixo** botões de seta.

Os filtros podem incluir zero ou mais regras. Quando nenhuma regra é definida, o pacote contém todo o conteúdo abaixo do caminho raiz.

É possível definir uma ou mais definições de filtro para um pacote. Use mais de um filtro para incluir conteúdo de vários caminhos raiz.

![Guia Filtros](assets/edit-filter.png)

Ao criar filtros, você pode definir um caminho ou usar uma expressão regular para especificar todos os nós que deseja incluir ou excluir.

| Tipo de regra | Descrição |
|---|---|
| include | A inclusão de um diretório incluirá esse diretório e todos os arquivos e pastas nele (ou seja, toda a subárvore), mas **não** incluir outros arquivos ou pastas de sob o caminho raiz especificado. |
| excluir | Excluir um diretório excluirá esse diretório e todos os arquivos e pastas nesse diretório (ou seja, toda a subárvore). |

Os filtros de pacote são definidos com mais frequência quando você [crie o pacote.](#creating-a-new-package) No entanto, eles também podem ser editados posteriormente, após o que o pacote deve ser recriado para atualizar seu conteúdo com base nas novas definições de filtro.

>[!TIP]
>
>Um pacote pode conter várias definições de filtro, para que nós de locais diferentes possam ser facilmente combinados em um pacote.

### Dependências {#dependencies}

![Guia Dependências](assets/dependencies.png)

| Texto | Descrição | Exemplo/Detalhes |
|---|---|---|
| Testada com | O nome e a versão do produto com os quais este pacote é destinado ou compatível. | `6.5` |
| Problemas corrigidos | Um campo de texto que permite a listagem de detalhes de bugs corrigidos com este pacote, um bug por linha | - |
| Depende de | Lista outros pacotes necessários para que o pacote atual seja executado como esperado quando instalado | `groupId:name:version` |
| Substitui | Uma lista de pacotes obsoletos que este pacote substitui | `groupId:name:version` |

### Configurações avançadas {#advanced-settings}

![Guia Configurações avançadas](assets/advanced-settings.png)

| Texto | Descrição | Exemplo/Detalhes |
|---|---|---|
| Nome | O nome do provedor do pacote | `WKND Media Group` |
| URL | URL do provedor | `https://wknd.site` |
| Link | Link específico do pacote para uma página do provedor | `https://wknd.site/package/` |
| Exige | Define se há restrições ao instalar o pacote | **Admin** - O pacote só deve ser instalado com privilégios de administrador <br>**Restart** - O AEM deve ser reiniciado após a instalação do pacote |
| Reparação de AC | Especifica como as informações de controle de acesso definidas no pacote são tratadas quando o pacote é importado | **Ignorar** - Preservar ACLs no repositório <br>**Substituir** - Substituir ACLs no repositório <br>**Mesclar** - Mesclar ambos os conjuntos de ACLs <br>**MergePreserve** - Mesclar o controle de acesso no conteúdo com o fornecido com o pacote ao adicionar as entradas de controle de acesso de entidades principais não presentes no conteúdo <br>**Limpar** - Limpar ACLs |

### Capturas de tela do pacote {#package-screenshots}

Você pode anexar várias capturas de tela ao seu pacote para fornecer uma representação visual de como o conteúdo aparece.

![Guia Capturas de tela](assets/screenshots.png)

## Ações do pacote {#package-actions}

Há muitas ações que podem ser executadas em um pacote.

### Criação de um pacote {#creating-a-new-package}

1. [Acesse o Gerenciador de pacotes.](#accessing)

1. Clique em **Criar pacote**.

   >[!TIP]
   >
   >Se a instância tiver muitos pacotes, talvez haja uma estrutura de pastas em vigor. Nesses casos, é mais fácil navegar até a pasta de destino necessária antes de criar o novo pacote.

1. No **Novo pacote** insira os seguintes campos:

   ![Caixa de diálogo Novo pacote](assets/new-package-dialog.png)

   * **Nome do pacote** - Selecione um nome descritivo para ajudá-lo (e outros) a identificar facilmente o conteúdo do pacote.

   * **Versão** - Este é um campo textual para que você indique uma versão. Ele é anexado ao nome do pacote para formar o nome do arquivo zip.

   * **Grupo** - Este é o nome do grupo (ou pasta) de destino. Os grupos ajudam a organizar seus pacotes. Uma pasta é criada para o grupo se ele ainda não existir. Se você deixar o nome do grupo em branco, ele criará o pacote na lista de pacotes principal.

1. Clique em **OK** para criar o pacote.

1. O AEM lista o novo pacote no topo da lista de pacotes.

   ![Novo pacote](assets/new-package.png)

1. Clique em **Editar** para definir o [conteúdo do pacote.](#package-contents) Clique em **Salvar** após concluir a edição das configurações.

1. Agora você pode [Build](#building-a-package) seu pacote.

Não é obrigatório criar o pacote imediatamente após criá-lo. Um pacote não criado não tem conteúdo e consiste apenas nos dados de filtro e outros metadados do pacote.

### Criação de um pacote {#building-a-package}

Um pacote geralmente é criado ao mesmo tempo que você [criar o pacote](#creating-a-new-package), mas você pode retornar posteriormente para criar ou reconstruir o pacote. Isso pode ser útil se o conteúdo no repositório tiver sido alterado ou os filtros do pacote tiverem sido alterados.

1. [Acesse o Gerenciador de pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Clique em **Build**. Uma caixa de diálogo solicita a confirmação de que você deseja criar o pacote, pois qualquer conteúdo existente será substituído.

1. Clique em **OK**. O AEM cria o pacote, listando todo o conteúdo adicionado ao pacote como faz na lista de atividades. Quando concluído, o AEM exibe uma confirmação de que o pacote foi criado e (quando você fecha a caixa de diálogo) atualiza as informações da lista de pacotes.

### Editar um pacote {#edit-package}

Depois que um pacote for carregado para AEM, você poderá modificar suas configurações.

1. [Acesse o Gerenciador de pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Clique em **Editar** e atualize o **[Configurações do pacote](#package-settings)** conforme necessário.

1. Clique em **Salvar** para salvar.

Talvez seja necessário [recriar o pacote](#building-a-package) para atualizar seu conteúdo com base nas alterações feitas.

### Reencapsulamento de um pacote {#rewrapping-a-package}

Depois que um pacote é criado, ele pode ser empacotado novamente. Reajustar altera as informações do pacote sem alterar a miniatura, a descrição etc., sem alterar o conteúdo do pacote.

1. [Acesse o Gerenciador de pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Clique em **Editar** e atualize o **[Configurações do pacote](#package-settings)** conforme necessário.

1. Clique em **Salvar** para salvar.

1. Clique em **Mais** > **Reajustar** e uma caixa de diálogo solicitará confirmação.

### Exibindo Outras Versões do Pacote {#other-versions}

Como cada versão de um pacote aparece na lista como qualquer outro pacote, o Gerenciador de pacotes pode encontrar outras versões de um pacote selecionado.

1. [Acesse o Gerenciador de pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Clique em **Mais** > **Outras versões** e uma caixa de diálogo é aberta com uma lista de outras versões do mesmo pacote com informações de status.

### Visualizando o conteúdo do pacote e testando a instalação {#viewing-package-contents-and-testing-installation}

Depois que um pacote for criado, é possível visualizar o conteúdo.

1. [Acesse o Gerenciador de pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Para exibir o conteúdo, clique em **Mais** > **Conteúdo**, e o Gerenciador de pacotes lista todo o conteúdo do pacote no log de atividades.

   ![Conteúdo do pacote](assets/package-contents.png)

1. Para executar uma simulação da instalação, clique em **Mais** > **Testar instalação** O e o Gerenciador de pacotes relatam no registro de atividades os resultados como se a instalação tivesse sido executada.

   ![Testar instalação](assets/test-install.png)

### Fazendo download de pacotes para seu sistema de arquivos {#downloading-packages-to-your-file-system}

1. [Acesse o Gerenciador de pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Clique em **Baixar** ou o nome de arquivo vinculado do pacote na área de detalhes do pacote.

1. O AEM baixa o pacote para o computador.

### Compartilhamento de um pacote {#share}

O Package Share era um serviço público centralizado para distribuir pacotes de conteúdo. O Compartilhamento de pacotes foi substituído por [Distribuição de software](#software-distribution) e esse botão não funciona mais.

### Fazer upload de pacotes do seu sistema de arquivos {#uploading-packages-from-your-file-system}

1. [Acesse o Gerenciador de pacotes.](#accessing)

1. Selecione a pasta de grupo na qual deseja que o pacote seja carregado.

1. Clique em **Fazer upload do pacote** botão.

1. Forneça as informações necessárias sobre o pacote carregado.

   ![Caixa de diálogo de upload de pacote](assets/package-upload-dialog.png)

   * **Pacote** - Use o **Navegar...** botão para selecionar o pacote necessário do sistema de arquivos local.
   * **Forçar carregamento** - Se um pacote com esse nome já existir, essa opção forçará o upload e substituirá o pacote existente.

1. Clique em **OK** e o pacote selecionado é carregado e a lista de pacotes é atualizada adequadamente.

O conteúdo do pacote agora existe no AEM, mas para disponibilizar o conteúdo para uso, certifique-se de [instalar o pacote](#installing-packages).

### Validação de pacotes {#validating-packages}

Como os pacotes podem modificar o conteúdo existente, geralmente é útil validar essas alterações antes de instalar.

#### Opções de validação {#validation-options}

O Gerenciador de pacotes pode executar as seguintes validações:

* [Importações de pacote OSGi](#osgi-package-imports)
* [Sobreposições](#overlays)
* [ACLs](#acls)

##### Validar importações do pacote OSGi {#osgi-package-imports}

**O que está marcado**

Essa validação inspeciona o pacote para todos os arquivos JAR (pacotes OSGi), extrai seus `manifest.xml` (que contém as dependências versionadas nas quais o pacote OSGi se baseia) e verifica as exportações da instância AEM dessas dependências com as versões corretas.

**Como é relatado**

Todas as dependências com versão que não podem ser satisfeitas pela instância AEM são listadas no Log de atividades do Gerenciador de pacotes.

**Estados de erro**

Se as dependências não forem satisfeitas, os pacotes OSGi no pacote com essas dependências não serão iniciados. Isso resulta em uma implantação de aplicativo com falha, pois qualquer item que depende do pacote OSGi não iniciado não funcionará corretamente.

**Resolução de erro**

Para resolver erros devido a pacotes OSGi não satisfeitos, a versão de dependência no pacote com importações não satisfeitas deve ser ajustada.

##### Validar sobreposições {#overlays}

**O que está marcado**

Essa validação determina se o pacote que está sendo instalado contém um arquivo que já está sobreposto na instância AEM de destino.

Por exemplo, dada uma sobreposição existente em `/apps/sling/servlet/errorhandler/404.jsp`, um pacote que contém `/libs/sling/servlet/errorhandler/404.jsp`, de modo que altere o arquivo existente em `/libs/sling/servlet/errorhandler/404.jsp`.

**Como é exportado**

Essas sobreposições são descritas no Log de atividades do Gerenciador de pacotes.

**Estados de erro**

Um estado de erro significa que o pacote está tentando implantar um arquivo que já está sobreposto, portanto, as alterações no pacote serão substituídas (e, portanto, &quot;ocultas&quot;) pela sobreposição e não terão efeito.

**Resolução de erro**

Para resolver esse problema, o mantenedor do arquivo de sobreposição no `/apps` O deve revisar as alterações no arquivo sobreposto no `/libs` e incorpore as alterações conforme necessário na sobreposição ( `/apps`) e reimplante o arquivo sobreposto.

>[!NOTE]
>
>O mecanismo de validação não tem como reconciliar se o conteúdo sobreposto foi incorporado corretamente no arquivo de sobreposição. Portanto, essa validação continuará a relatar conflitos mesmo depois que as alterações necessárias forem feitas.

##### Validar ACLs {#acls}

**O que está marcado**

Essa validação verifica quais permissões estão sendo adicionadas, como elas serão tratadas (mesclar/substituir) e se as permissões atuais serão afetadas.

**Como é relatado**

As permissões são descritas no Log de atividades do Gerenciador de pacotes.

**Estados de erro**

Nenhum erro explícito pode ser fornecido. A validação simplesmente indica se qualquer nova permissão de ACL será adicionada ou afetada pela instalação do pacote.

**Resolução de erro**

Usando as informações fornecidas pela validação, os nós afetados podem ser revisados no CRXDE e as ACLs podem ser ajustadas no pacote conforme necessário.

>[!CAUTION]
>
>Como prática recomendada, os pacotes não devem afetar as ACLs fornecidas pelo AEM, pois isso pode resultar em um comportamento inesperado.

#### Executando validação {#performing-validation}

A validação de pacotes pode ser feita de duas maneiras diferentes:

* [Pela interface do usuário do Gerenciador de pacotes](#via-package-manager)
* [Por solicitação HTTP POST, como com cURL](#via-post-request)

A validação sempre deve ocorrer após o upload do pacote, mas antes de instalá-lo.

##### Validação De Pacote Via Gerenciador De Pacotes {#via-package-manager}

1. [Acesse o Gerenciador de pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Para validar o pacote, clique em **Mais** > **Validar**,

1. Na caixa de diálogo modal exibida, use as caixas de seleção para selecionar o(s) tipo(s) de validação e começar a validação clicando em **Validar**.

1. A(s) validação(s) escolhida(s) é/são executada(s) e os resultados são exibidos no Log de atividades do Gerenciador de pacotes.

##### Validação de pacote por meio de solicitação POST HTTP {#via-post-request}

A solicitação POST assume o seguinte formato.

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

A variável `type` pode ser qualquer lista não ordenada separada por vírgulas composta por:

* `osgiPackageImports`
* `overlays`
* `acls`

O valor de `type` toma como padrão `osgiPackageImports` se não for explicitamente aprovado.

Ao usar cURL, execute uma instrução semelhante à seguinte:

```shell
curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
```

Ao validar por meio da solicitação POST, a resposta é enviada de volta como um objeto JSON.

### Visualizando a cobertura do pacote {#package-coverage}

Os pacotes são definidos por seus filtros. O Gerenciador de pacotes pode aplicar filtros de um pacote ao conteúdo existente do repositório para mostrar qual conteúdo do repositório é coberto pela definição de filtro do pacote.

1. [Acesse o Gerenciador de pacotes.](#accessing)

1. Abra os detalhes do pacote na lista de pacotes clicando no nome do pacote.

1. Clique em **Mais** > **Cobertura**.

1. Os detalhes da cobertura estão listados no Log de atividades.

### Instalação de pacotes {#installing-packages}

Fazer upload de um pacote adiciona somente o conteúdo do pacote ao repositório, mas ele não está acessível. Instale o pacote carregado para usar o conteúdo do pacote.

>[!CAUTION]
>
>A instalação de um pacote pode substituir ou excluir conteúdo existente. Carregue um pacote somente se tiver certeza de que ele não exclui nem substitui o conteúdo necessário.

Antes da instalação do pacote, o Gerenciador de pacotes cria automaticamente um pacote de instantâneos que contém o conteúdo que será substituído. Este snapshot será reinstalado se você desinstalar o pacote.

>[!CAUTION]
>
>* Se estiver instalando ativos digitais, você deve:
>  Primeiro, desative o WorkflowLauncher.
>  Use a opção de menu Componentes do console OSGi para desativar
>  `com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl.`
>* Em seguida, quando a instalação estiver concluída, reative o WorkflowLauncher.
>
>A desativação do WorkflowLauncher garante que a estrutura do importador do Assets não manipule (involuntariamente) os ativos durante a instalação.

1. [Acesse o Gerenciador de pacotes.](#accessing)

1. Abra os detalhes do pacote que deseja instalar na lista de pacotes clicando no nome do pacote.

1. Clique no link **Instalar** nos detalhes do item ou no campo **Instalar** no status do pacote.

1. Uma caixa de diálogo solicitará confirmação e permitirá a especificação de opções adicionais.

   * **Somente extração** - Extraia o pacote somente para que nenhum instantâneo seja criado e, portanto, a desinstalação não será possível
   * **Salvar limite** - Número de nós transitórios até que o salvamento automático seja acionado (aumente se você encontrar exceções de modificação simultâneas)
   * **Extrair sub-pacotes** - Habilitar extração automática de pacotes secundários
   * **Manuseio do controle de acesso** - Especifica como as informações de controle de acesso definidas no pacote são tratadas quando o pacote é instalado (as opções são as mesmas do [configurações avançadas de pacote](#advanced-settings))
   * **Tratamento de dependências** - Especificar como as dependências são tratadas durante a instalação

1. Clique em **Instalar**.

1. O Registro de atividades detalha o progresso da instalação.

Quando a instalação for concluída e bem-sucedida, a lista de pacotes será atualizada e a palavra **Instalado** aparece no status do pacote.

### Reinstalação de pacotes {#reinstalling-packages}

A reinstalação de pacotes executa as mesmas etapas em um pacote já instalado que são processadas quando [instalando inicialmente o pacote.](#installing-packages)

### Upload e instalação baseados no sistema de arquivos {#file-system-based-upload-and-installation}

Você pode abandonar o Gerenciador de pacotes completamente ao instalar pacotes. O AEM pode detectar pacotes colocados em um local específico no sistema de arquivos local da máquina host, carregá-los e instalá-los automaticamente.

1. Na pasta de instalação do AEM, há uma `crx-quicksart` ao lado do jar e `license.properties` arquivo. Crie uma pasta chamada `install` em `crx-quickstart` resultando no caminho `<aem-home>/crx-quickstart/install`.

1. Nesta pasta, adicione seus pacotes. Eles serão carregados e instalados automaticamente na sua instância.

1. Quando o upload e a instalação estiverem concluídos, você poderá ver os pacotes no Gerenciador de pacotes como se tivesse usado a interface do usuário do Gerenciador de pacotes para instalá-los.

Se a instância estiver em execução, o upload e a instalação serão iniciados imediatamente quando você adicioná-los ao pacote do `install` pasta

Se a instância não estiver em execução, os pacotes serão colocados no `install` pastas são instaladas na inicialização em ordem alfabética.

### Desinstalando pacotes {#uninstalling-packages}

A desinstalação do pacote reverte o conteúdo do repositório para o instantâneo criado automaticamente pelo Gerenciador de Pacotes antes da instalação.

1. [Acesse o Gerenciador de pacotes.](#accessing)

1. Abra os detalhes do pacote que deseja desinstalar na lista de pacotes clicando no nome do pacote.

1. Clique em **Mais** > **Desinstalar**, para remover o conteúdo deste pacote do repositório.

1. Uma caixa de diálogo solicitará confirmação e listará todas as alterações que estão sendo feitas.

1. O pacote é removido e o instantâneo é aplicado. O progresso do processo é mostrado no Log de atividades.

### Exclusão de pacotes {#deleting-packages}

A exclusão de um pacote exclui somente seus detalhes do Gerenciador de pacotes. Se esse pacote já tiver sido instalado, o conteúdo instalado não será excluído.

1. [Acesse o Gerenciador de pacotes.](#accessing)

1. Abra os detalhes do pacote que deseja excluir na lista de pacotes clicando no nome do pacote.

1. O Gerenciador de pacotes solicita a confirmação de que você deseja excluir o pacote. Clique em **OK** para confirmar a exclusão.

1. As informações do pacote são excluídas e os detalhes são relatados no Log de atividades.

### Replicação de pacotes {#replicating-packages}

Replicar o conteúdo de um pacote para instalá-lo na instância de publicação.

1. [Acesse o Gerenciador de pacotes.](#accessing)

1. Abra os detalhes do pacote que deseja replicar na lista de pacotes clicando no nome do pacote.

1. Clique em **Mais** > **Replicar**.

1. O pacote é replicado e os detalhes são relatados no Registro de atividades.

## Distribuição de software {#software-distribution}

Os pacotes AEM podem ser usados para criar e compartilhar conteúdo em ambientes AEM.

[Distribuição de software](https://downloads.experiencecloud.adobe.com) O é um serviço centralizado projetado para simplificar a pesquisa e o download de pacotes AEM.

Para obter mais informações, consulte [Documentação de Distribuição de software.](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=pt-br)

>[!NOTE]
>
>No momento, o Gerenciador de Pacotes não está integrado à Distribuição de Software como estava com o antigo serviço de Compartilhamento de Pacotes. Portanto, os botões de compartilhamento e outros links para Compartilhamento de pacotes no Gerenciador de pacotes não funcionam mais. A solução é baixar pacotes no disco local.
