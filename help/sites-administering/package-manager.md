---
title: Como trabalhar com pacotes
seo-title: Como trabalhar com pacotes
description: Saiba mais sobre as noções básicas de trabalhar com pacotes no AEM.
seo-description: Saiba mais sobre as noções básicas de trabalhar com pacotes no AEM.
uuid: cba76a5f-5d75-4d63-a0f4-44c13fa1baf2
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 6694a135-d1e1-4afb-9f5b-23991ee70eee
docset: aem65
translation-type: tm+mt
source-git-commit: 5e10ddb0e5cf24e1915d0840cd380520374e93ea

---


# How to Work With Packages{#how-to-work-with-packages}

Os pacotes permitem a importação e exportação de conteúdo do repositório. Por exemplo, você pode usar pacotes para instalar uma nova funcionalidade, transferir conteúdo entre instâncias e fazer backup do conteúdo do repositório.

Os pacotes podem ser acessados e/ou mantidos nas seguintes páginas:

* [Gerenciador](#package-manager)de pacotes, que você usa para gerenciar os pacotes na instância local do AEM.

* [Compartilhamento](#package-share)de pacotes, um servidor centralizado com pacotes disponíveis publicamente e privados para sua empresa. Os pacotes públicos podem conter hotfixes, nova funcionalidade, documentação etc.

Você pode transferir pacotes entre o Gerenciador de pacotes, o Compartilhamento de pacotes e seu sistema de arquivos.

## O que são os pacotes? {#what-are-packages}

Um pacote é um arquivo zip que contém o conteúdo do repositório na forma de uma serialização do sistema de arquivos (chamada de serialização &quot;vault&quot;). Isso proporciona uma representação fácil de usar e editar de arquivos e pastas.

Os pacotes incluem conteúdo, conteúdo de página e conteúdo relacionado ao projeto, selecionado usando filtros.

Um pacote também contém informações meta do cofre, incluindo as definições de filtro e as informações de configuração de importação. Propriedades de conteúdo adicionais (que não são usadas para extração de pacote) podem ser incluídas no pacote, como uma descrição, uma imagem visual ou um ícone; essas propriedades são para o consumidor do pacote de conteúdo e apenas para fins informativos.

>[!NOTE]
>
>Os pacotes representam a versão atual do conteúdo no momento em que o pacote é criado. Eles não incluem nenhuma versão anterior do conteúdo que o AEM mantém no repositório.

É possível executar as seguintes ações em ou com pacotes:

* Criar novos pacotes; definição das configurações e filtros do pacote conforme necessário
* Visualizar conteúdo do pacote (antes da criação)
* Criar pacotes
* Exibir informações do pacote
* Exibir conteúdo do pacote (após a criação)
* Modificar a definição de pacotes existentes
* Reconstruir pacotes existentes
* Revincular pacotes
* Baixar pacotes do AEM em seu sistema de arquivos
* Faça upload de pacotes do seu sistema de arquivos para a instância do AEM local
* Validar o conteúdo do pacote antes da instalação
* Execute uma instalação em funcionamento
* Instalar pacotes (o AEM não instala pacotes automaticamente após o upload)
* Excluir pacotes
* Baixar pacotes, como hotfixes, da biblioteca de compartilhamento de pacotes
* Carregar pacotes na seção interna da empresa da biblioteca Compartilhamento de pacotes

## Informações do pacote {#package-information}

Uma definição de pacote é composta de vários tipos de informações:

* [Configurações do pacote](#package-settings)
* [Filtros de pacote](#package-filters)
* [Capturas de tela do pacote](#package-screenshots)
* [Ícones de pacote](#package-icons)

### Configurações do pacote {#package-settings}

Você pode editar várias Configurações do pacote para definir aspectos como a descrição do pacote, bugs relacionados, dependências e informações do provedor.

A caixa de diálogo Configurações **do** pacote está disponível por meio do botão **Editar** ao [criar](#creating-a-new-package) ou [editar](#viewing-and-editing-package-information) um pacote e fornece três guias para configuração. Depois de fazer qualquer alteração, clique em **OK** para salvá-las.

![packagesedit](assets/packagesedit.png)

| **Texto** | **Descrição** |
|---|---|
| Nome | O nome do pacote. |
| Grupo | O nome do grupo ao qual o pacote será adicionado para organizar os pacotes. Digite o nome de um novo grupo ou selecione um grupo existente. |
| Versão | Texto a ser usado para a versão personalizada. |
| Descrição | Uma breve descrição do pacote. A marcação HTML pode ser usada para formatação. |
| Miniatura | O ícone que aparece com a lista de pacotes. Clique em Procurar para selecionar um arquivo local. |

![chlimage_1-108](assets/chlimage_1-108.png)

<table>
 <tbody>
  <tr>
   <th><strong>Texto</strong></th>
   <th><strong>Descrição</strong></th>
   <th><strong>Formato/Exemplo</strong></th>
  </tr>
  <tr>
   <td>Nome</td>
   <td>O nome do provedor.</td>
   <td><em>AEM Geometrixx<br /> </em></td>
  </tr>
  <tr>
   <td>URL</td>
   <td>URL do provedor.</td>
   <td><em>https://www.aem-geometrixx.com</em></td>
  </tr>
  <tr>
   <td>Link</td>
   <td>Link específico do pacote para uma página do provedor.</td>
   <td><em>https://www.aem-geometrixx.com/mypackage.html</em></td>
  </tr>
  <tr>
   <td>Exige<br /> </td>
   <td>
    <ul>
     <li>Administrador: Selecione quando o pacote só pode ser instalado por uma conta com privilégios de administrador.</li>
     <li>Reiniciar: Selecione quando o servidor precisa ser reiniciado após a instalação do pacote.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Reparação de AC</td>
   <td><p>Especifique como as informações de controle de acesso definidas no pacote são tratadas quando o pacote é importado:</p>
    <ul>
     <li><strong>Ignorar</strong></li>
     <li><strong>Substituir</strong></li>
     <li><strong>Mesclar</strong></li>
     <li><strong>Limpar</strong></li>
     <li><strong>MergePreserve</strong></li>
    </ul> <p>The default value is <strong>Ignore</strong>.</p> </td>
   <td>
    <ul>
     <li><strong>Ignorar</strong> - preservar ACLs no repositório</li>
     <li><strong>Substituir</strong> - substituir ACLs no repositório</li>
     <li><strong>Mesclar</strong> - mesclar ambos os conjuntos de ACLs</li>
     <li><strong>Limpar</strong> - limpar ACLs</li>
     <li><strong>MergePreserve</strong> - mesclar o controle de acesso no conteúdo com o fornecido com o pacote adicionando as entradas de controle de acesso de principais não presentes no conteúdo</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

![packagesdependencies](assets/packagesdependencies.png)

| **Texto** | **Descrição** | **Formato/Exemplo** |
|---|---|---|
| Testado com | O nome e a versão do produto para os quais este pacote está direcionado ou é compatível. | *AEM6* |
| Erros/problemas corrigidos | Um campo de texto que permite listar detalhes de erros corrigidos com este pacote. Liste cada bug em uma linha separada. | resumo bug-nr |
| Depende de | Lista as informações de dependência que precisam ser respeitadas sempre que outros pacotes forem necessários para permitir que o pacote atual seja executado como esperado. Esse campo é importante ao usar hotfixes. | groupId:name:version |
| Substitui | Uma lista de pacotes obsoletos que este pacote substitui. Antes de instalar, verifique se este pacote inclui todo o conteúdo necessário dos pacotes obsoletos para que nenhum conteúdo seja substituído. | groupId:name:version |

### Filtros de pacote {#package-filters}

Os filtros identificam os nós do repositório a serem incluídos no pacote. Uma Definição **de** filtro especifica as seguintes informações:

* O Caminho **** raiz do conteúdo a ser incluído.
* **Regras** que incluem ou excluem nós específicos abaixo do caminho raiz.

Os filtros podem incluir zero ou mais regras. Quando nenhuma regra é definida, o pacote contém todo o conteúdo abaixo do caminho raiz.

É possível definir uma ou mais definições de filtro para um pacote. Use mais de um filtro para incluir conteúdo de vários caminhos raiz.

![chlimage_1-109](assets/chlimage_1-109.png)

A tabela a seguir descreve essas regras e fornece exemplos:

<table>
 <tbody>
  <tr>
   <th> Tipo de regra</th>
   <th>Descrição </th>
   <th>Exemplo </th>
  </tr>
  <tr>
   <td> incluir</td>
   <td>Você pode definir um caminho ou usar uma expressão regular para especificar todos os nós que deseja incluir.<br /> <br /> A inclusão de um diretório:
    <ul>
     <li>incluir esse diretório <i>e todos os arquivos</i> e pastas desse diretório (ou seja, toda a subárvore)</li>
     <li><strong>não</strong> incluir outros arquivos ou pastas no caminho raiz especificado</li>
    </ul> </td>
   <td>/libs/sling/install(/.*)? </td>
  </tr>
  <tr>
   <td> excluir</td>
   <td>Você pode especificar um caminho ou usar uma expressão regular para especificar todos os nós que deseja excluir.<br /> A <br /> exclusão de um diretório excluirá esse diretório <i>e todos os arquivos</i> e pastas desse diretório (ou seja, toda a subárvore).<br /> </td>
   <td>/libs/wcm/fundação/componentes(/.*)?</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Um pacote pode conter várias definições de filtro, de modo que nós de diferentes locais possam ser facilmente combinados em um único pacote.

Os filtros de pacotes são definidos com mais frequência quando você [cria o pacote](#creating-a-new-package)pela primeira vez, mas também podem ser editados posteriormente (após o que o pacote deve ser recriado).

### Capturas de tela do pacote {#package-screenshots}

Você pode anexar capturas de tela ao seu pacote para fornecer uma representação visual da aparência do conteúdo; por exemplo, fornecendo capturas de tela de novas funcionalidades.

### Ícones de pacote {#package-icons}

Você também pode anexar um ícone ao seu pacote para fornecer uma representação visual de referência rápida do que o pacote contém. Isso é mostrado na lista de pacotes e pode ajudá-lo a identificar facilmente o pacote ou a classe do pacote.

Como um pacote pode conter um ícone, as seguintes convenções são usadas para pacotes oficiais:

>[!NOTE]
>
>Para evitar confusão, use um ícone descritivo para o pacote e não use um dos ícones oficiais.

Pacote de hotfix oficial:

![](do-not-localize/chlimage_1-28.png)

Instalação ou extensão oficial do AEM:

Pacotes de recursos oficiais:

![](do-not-localize/chlimage_1-29.png)

## Gerenciador de pacotes {#package-manager}

O Gerenciador de pacotes gerencia os pacotes na instalação local do AEM. Depois de [atribuir as permissões](#permissions-needed-for-using-the-package-manager) necessárias, você pode usar o Gerenciador de pacotes para várias ações, incluindo configuração, criação, download e instalação dos pacotes. Os principais elementos a serem configurados são:

* [Configurações do pacote](#package-settings)
* [Filtros de pacote](#package-filters)

### Permissões necessárias para usar o Gerenciador de pacotes {#permissions-needed-for-using-the-package-manager}

Para conceder aos usuários o direito de criar, modificar, carregar e instalar pacotes, você deve conceder a eles as permissões apropriadas nos seguintes locais:

* **/etc/packages** (direitos totais excluindo exclusão)
* o nó que contém o conteúdo do pacote

Consulte [Configuração de permissões](/help/sites-administering/security.md#setting-page-permissions) para obter instruções sobre como alterar permissões.

### Criação de um novo pacote {#creating-a-new-package}

Para criar uma nova definição de pacote:

1. Na tela de boas-vindas do AEM, clique em **Pacotes** (ou no console **Ferramentas** , clique duas vezes em **Pacotes**).

1. Em seguida, selecione **Gerenciador** de pacotes.
1. Clique em **Criar pacote**.

   >[!NOTE]
   >
   >Se sua instância tiver muitos pacotes, pode haver uma estrutura de pastas em vigor, portanto, você pode navegar até a pasta de destino desejada antes de criar o novo pacote.

1. Na caixa de diálogo:

   ![packagesnew](assets/packagesnew.png)

   Insira:

   * **Nome do grupo**

      O nome do grupo de destino (ou pasta). Os grupos devem ser usados para ajudar a organizar seus pacotes.

      Uma pasta será criada para o grupo se ainda não existir. Se você deixar o nome do grupo em branco, ele criará o pacote na lista principal de pacotes (Início > Pacotes).

   * **Nome do pacote**

      O nome do novo pacote. Selecione um nome descritivo para ajudá-lo (e outros) a identificar facilmente o conteúdo do pacote.

   * **Versão**

      Um campo textual para indicar uma versão. Isso será anexado ao nome do pacote para formar o nome do arquivo zip.
   Clique em **OK** para criar o pacote.

1. O AEM lista o novo pacote na pasta de grupo apropriada.

   ![packagesitem](assets/packagesitem.png)

   Clique no ícone ou no nome do pacote para abrir.

   ![packagesitemclicado](assets/packagesitemclicked.png)

   >[!NOTE]
   >
   >Você pode retornar a esta página em um estágio posterior, se necessário.

1. Clique em **Editar** para editar as configurações [](#package-settings)do pacote.

   Aqui, você pode adicionar informações e/ou definir certas configurações; por exemplo, eles incluem uma descrição, o [ícone](#package-icons), erros relacionados e detalhes do provedor.

   Clique em **OK** após terminar de editar as configurações.

1. Adicione **[capturas de tela](#package-screenshots)**ao pacote, conforme necessário. Uma instância está disponível quando o pacote é criado, adicione mais, se necessário, usando o **Package Screenshot**do sidekick.

   Adicione a imagem real clicando duas vezes no componente de imagem na área **Capturas de tela** , adicionando uma imagem e clicando em **OK**.

1. Defina os Filtros **[de](#package-filters)**pacote arrastando instâncias da Definição **de**filtro do sidekick e clicando duas vezes para abrir para edição:

   ![packagesfilter](assets/packagesfilter.png)

   Especificar:

   * **Caminho raiz** O conteúdo a ser embalado; essa pode ser a raiz de uma subárvore.
   * **As regras** são opcionais; para definições simples de pacote, não é necessário especificar regras de inclusão ou exclusão.

      Se necessário, é possível definir as regras [**Incluir **ou** Excluir **para](#package-filters)definir exatamente o conteúdo do pacote.

      Adicione regras usando o símbolo **+** e, como alternativa, remova regras usando o símbolo **-** . As regras são aplicadas de acordo com sua ordem para posicioná-las conforme necessário usando os botões **Para** cima e **Para baixo** .
   Em seguida, clique em **OK** para salvar o filtro.

   >[!NOTE]
   >
   >Você pode usar tantas definições de filtro quantas forem necessárias, embora seja necessário tomar cuidado para garantir que elas não entrem em conflito. Use a opção **Visualizar** para confirmar o conteúdo do pacote.

1. Para confirmar qual pacote contém, você pode usar a opção **Visualizar**. Isso executa uma execução seca do processo de criação e lista tudo o que será adicionado ao pacote quando ele for realmente criado.
1. Agora você pode [criar](#building-a-package) seu pacote.

   >[!NOTE]
   >
   >Não é obrigatório construir o pacote neste momento, pode ser feito posteriormente.

### Criação de um pacote {#building-a-package}

Geralmente, um pacote é criado ao mesmo tempo que você [cria a definição](#creating-a-new-package)do pacote, mas é possível retornar posteriormente para criar ou recriar o pacote. Isso pode ser útil se o conteúdo no repositório tiver sido alterado.

>[!NOTE]
>
>Antes de criar o pacote, pode ser útil visualizar o conteúdo do pacote. Para fazer isso, clique em **Visualizar**.

1. Abra a definição do pacote no Gerenciador **de** pacotes (clique no ícone ou no nome do pacote).

1. Clique em **Criar**. Uma caixa de diálogo solicita a confirmação de que você deseja criar o pacote.

   >[!NOTE]
   >
   >Isso é de especial importância quando você estiver reconstruindo um pacote, já que o conteúdo do pacote será substituído.

1. Clique em **OK**. O AEM criará o pacote, listando todo o conteúdo adicionado ao pacote conforme ele for criado. Quando o AEM concluído exibe uma confirmação de que o pacote foi criado e (quando você fecha a caixa de diálogo) atualiza as informações da lista de pacotes.

### Reenvolvimento de um pacote {#rewrapping-a-package}

Depois que um pacote é criado, ele pode ser reencapsulado, se necessário.

Revincular altera as informações do pacote - *sem* alterar o conteúdo do pacote. As informações do pacote são a miniatura, a descrição etc., ou seja, tudo o que você pode editar com a caixa de diálogo Configurações **do** pacote (para abrir, clique em **Editar**).

Um caso de uso importante para reenvolvimento é ao preparar um pacote para o compartilhamento do pacote. Por exemplo, você pode ter um pacote existente e decidir compartilhá-lo com outras pessoas. Para isso, adicione uma miniatura e uma descrição. Em vez de recriar o pacote inteiro com toda a sua funcionalidade (o que pode levar algum tempo e acarretar o risco de o pacote não ser mais idêntico ao original), você pode reembalá-lo e adicionar a miniatura e a descrição.

1. Abra a definição do pacote no Gerenciador **de** pacotes (clique no ícone ou no nome do pacote).

1. Clique em **Editar** e atualize as Configurações **[](#package-settings)**do pacote, conforme necessário. Clique em **OK**para salvar.

1. Clique em **Reenvolver**, uma caixa de diálogo solicitará confirmação.

### Visualizando e editando informações do pacote {#viewing-and-editing-package-information}

Para exibir ou editar informações sobre uma definição de pacote:

1. No Gerenciador de pacotes, navegue até o pacote que deseja exibir.
1. Clique no ícone de pacote do pacote que deseja exibir. Isso abrirá a página do pacote listando informações sobre a definição do pacote:

   ![packagesitemclicked-1](assets/packagesitemclicked-1.png)

   >[!NOTE]
   >
   >Também é possível editar e executar determinadas ações no pacote a partir desta página.
   >
   >Os botões disponíveis dependerão se o pacote já foi criado ou não.

1. Se o pacote já tiver sido criado, clique em **Conteúdo**, uma janela abrirá e listará todo o conteúdo do pacote:

### Exibição do conteúdo do pacote e teste da instalação {#viewing-package-contents-and-testing-installation}

Após a criação de um pacote, é possível exibir o conteúdo:

1. No Gerenciador de pacotes, navegue até o pacote que deseja exibir.
1. Clique no ícone de pacote do pacote que deseja exibir. Isso abrirá as informações de listagem da página do pacote sobre a definição do pacote.

1. Para exibir o conteúdo, clique em **Conteúdo**, uma janela abrirá e listará todo o conteúdo do pacote:

   ![conteúdo dos pacotes](assets/packgescontents.png)

1. Para executar uma execução seca da instalação, clique em **Testar instalação**. Após confirmar a ação, uma janela abrirá e listará os resultados como se a instalação tivesse sido executada:

   ![packagestestinstall](assets/packagestestinstall.png)

### Download de pacotes no seu sistema de arquivos {#downloading-packages-to-your-file-system}

Esta seção descreve como baixar um pacote do AEM para seu sistema de arquivos usando o **Package Manager**.

>[!NOTE]
>
>Consulte Compartilhamento [de](#package-share) pacotes para obter informações sobre como baixar hotfixes, pacotes de recursos e pacotes da área pública e da área interna de compartilhamento de pacotes da sua empresa.
>
>Em Compartilhamento de pacotes, você pode:
>
>* baixe os pacotes do Compartilhamento de [pacotes diretamente na instância](#downloading-and-installing-packages-from-package-share)local do AEM.
   >  Após o download, o pacote é importado para o repositório, depois disso, você pode instalá-lo imediatamente em sua instância local usando o Gerenciador de **pacotes**. Esses pacotes incluem hotfixes e outros pacotes compartilhados.
   >
   >
* baixe os pacotes do Compartilhamento de [pacotes no seu sistema](#downloading-packages-to-your-file-system-from-package-share)de arquivos.
>



1. Na tela de boas-vindas do AEM, clique em **Pacotes** e selecione **Gerenciador** de pacotes.
1. Navegue até o pacote que deseja baixar.

   ![download de pacotes](assets/packagesdownload.png)

1. Clique no link formado pelo nome do arquivo zip (sublinhado) do pacote que você deseja baixar; por exemplo `export-for-offline.zip`.

   O AEM baixa o pacote em seu computador (usando uma caixa de diálogo padrão de download do navegador).

### Carregando pacotes do seu sistema de arquivos {#uploading-packages-from-your-file-system}

O upload de um pacote permite que você carregue um pacote de seu sistema de arquivos no Gerenciador de pacotes AEM.

>[!NOTE]
>
>Consulte [Fazer upload de pacotes para o Compartilhamento](#uploading-packages-to-the-company-internal-package-share) de pacotes interno da empresa para fazer upload de um pacote para a área privada de Compartilhamento de pacotes da sua empresa.

Para carregar um pacote:

1. Navegue até o Gerenciador **de pacotes**. Em seguida, para a pasta do grupo na qual você deseja que o pacote seja carregado.

   ![packagesuploadbutton](assets/packagesuploadbutton.png)

1. Clique em **Carregar pacote**.

   ![packagesuploaddialog](assets/packagesuploaddialog.png)

   * **Arquivo**

      **Você pode digitar o nome do arquivo diretamente ou usar a opção** Procurar... para selecionar o pacote necessário do sistema de arquivos local (após a seleção, clique em **OK**).

   * **Forçar atualização**

      Se um pacote com esse nome já existir, clique nele para forçar o upload (e substituir o pacote existente).
   Clique em **OK** para que o novo pacote seja carregado e listado na lista Gerenciador de pacotes.

   >[!NOTE]
   >
   >Para disponibilizar o conteúdo para o AEM, [instale o pacote](#installing-packages).

### Validação de pacotes {#validating-packages}

Antes de instalar um pacote, verifique seu conteúdo. Como os pacotes podem modificar arquivos sobrepostos em `/apps` e/ou adicionar, modificar e remover ACLs, geralmente é útil validar essas alterações antes da instalação.

#### Opções de validação {#validation-options}

O mecanismo de validação pode verificar as seguintes características do pacote:

* Importações do pacote OSGi
* Sobreposições
* ACLs

Essas opções estão detalhadas abaixo.

* **Validar importações do pacote OSGi**

   **O que está marcado**

   Essa validação inspeciona o pacote para todos os arquivos JAR (pacotes OSGi), extrai suas dependências `manifest.xml` (que contêm as dependências com versão nas quais o pacote OSGi depende) e verifica as exportações da instância do AEM, ditas dependências, com as versões corretas.

   **Como é reportado**

   Todas as dependências com versão que não possam ser atendidas pela instância do AEM estão listadas no Log **de** atividade do Gerenciador de pacotes.

   **Estados de erro**

   Se as dependências não forem atendidas, os pacotes OSGi no pacote com essas dependências não serão iniciados. Isso resulta em uma implantação de aplicativo quebrada, pois qualquer coisa que dependa do pacote OSGi não iniciado não funcionará corretamente.

   **Resolução de erro**

   Para resolver erros devido a pacotes OSGi não satisfeitos, a versão de dependência no pacote com importações não satisfeitas precisa ser ajustada.

* **Validar sobreposições**

   **O que está marcado**

   Essa validação determina se o pacote que está sendo instalado contém um arquivo que já está sobreposto na instância de AEM de destino.

   Por exemplo, considerando uma sobreposição existente em `/apps/sling/servlet/errorhandler/404.jsp`, um pacote que contém `/libs/sling/servlet/errorhandler/404.jsp`, de modo que alterará o arquivo existente em `/libs/sling/servlet/errorhandler/404.jsp`.

   **Como é reportado**

   Essas sobreposições são descritas no Log **de** atividades do Gerenciador de pacotes.

   **Estados de erro**

   Um estado de erro significa que o pacote está tentando implantar um arquivo que já está sobreposto, portanto, as alterações no pacote serão substituídas (e, portanto, &quot;ocultas&quot;) pela sobreposição e não entrarão em vigor.

   **Resolução de erro**

   Para resolver esse problema, o responsável principal do arquivo de sobreposição em `/apps` deve revisar as alterações no arquivo sobreposto em `/libs` e incorporar as alterações conforme necessário na sobreposição ( `/apps`) e reimplantar o arquivo sobreposto.

   >[!NOTE]
   >
   >Observe que o mecanismo de validação não tem como reconciliar se o conteúdo sobreposto foi incorporado corretamente no arquivo de sobreposição. Por conseguinte, esta validação continuará a reportar sobre conflitos mesmo após as necessárias alterações.

* **Validar ACLs**

   **O que está marcado**

   Essa validação verifica quais permissões estão sendo adicionadas, como serão tratadas (mesclar/substituir) e se as permissões atuais serão afetadas.

   **Como é reportado**

   As permissões são descritas no Log **de** atividades do Gerenciador de pacotes.

   **Estados de erro**

   Não é possível fornecer erros explícitos. A validação simplesmente indica se novas permissões de ACL serão adicionadas ou afetadas pela instalação do pacote.

   **Resolução de erro**

   Usando as informações fornecidas pela validação, os nós afetados podem ser revisados no CRXDE e as ACLs podem ser ajustadas no pacote conforme necessário.

   >[!CAUTION]
   >
   >Como prática recomendada, os pacotes não devem afetar as ACLs fornecidas pelo AEM, pois isso pode resultar em comportamento inesperado do produto.

#### Executando Validação {#performing-validation}

A validação dos pacotes pode ser efetuada de duas formas diferentes:

* Por meio da interface do usuário do Gerenciador de pacotes
* Por meio de solicitação HTTP POST, como com cURL

>[!NOTE]
>
>A validação sempre deve ocorrer após o upload do pacote, mas antes da instalação.

**Validação do pacote por meio do Gerenciador de pacotes**

1. Abra o Gerenciador de pacotes em `https://<server>:<port>/crx/packmgr`
1. Selecione o pacote na lista e, em seguida, selecione o menu suspenso **Mais** no cabeçalho e, em seguida, **Validar** no menu suspenso.

   >[!NOTE]
   >
   >Isso deve ser feito após o upload do pacote de conteúdo, mas antes da instalação do pacote.

1. Na caixa de diálogo modal que é exibida, use as caixas de seleção para selecionar os tipos de validação e iniciar a validação clicando em **Validar**. Como alternativa, clique em **Cancelar**.

1. As validações escolhidas são executadas. Os resultados são exibidos no log de atividades do Gerenciador de pacotes.

**Validação de pacote por solicitação HTTP POST**

A solicitação POST assume o seguinte formulário.

```
https://<host>:<port>/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls
```

>[!NOTE]
>
>O `type` parâmetro pode ser qualquer lista não ordenada separada por vírgulas que consista em:
>
>* `osgiPackageImports`
>* `overlays`
>* `acls`
>
>
O valor padrão de `type` é `osgiPackageImports` se não for passado.

A seguir está um exemplo de uso de cURL para executar uma validação de pacote.

1. Se você estiver usando cURL, execute uma instrução semelhante a:

   ```shell
   curl -v -X POST --user admin:admin -F file=@/Users/SomeGuy/Desktop/core.wcm.components.all-1.1.0.zip 'http://localhost:4502/crx/packmgr/service.jsp?cmd=validate&type=osgiPackageImports,overlays,acls'
   ```

1. A validação solicitada é executada e a resposta é enviada de volta como um objeto JSON.

>[!NOTE]
>
>A resposta a uma solicitação HTTP POST de validação será um objeto JSON com os resultados da validação.

### Instalação de pacotes {#installing-packages}

Após carregar um pacote, é necessário instalar o conteúdo. Para ter o conteúdo do pacote instalado e funcional, ele precisa ser:

* carregado no AEM ( [carregado no sistema de arquivos](#uploading-packages-from-your-file-system) ou [baixado do compartilhamento](#downloading-and-installing-packages-from-package-share)de pacotes)

* instalados

>[!CAUTION]
>
>A instalação de um pacote pode substituir ou excluir o conteúdo existente. Carregue apenas um pacote se tiver certeza de que ele não exclui ou sobrescreve o conteúdo necessário.
>
>Para ver o conteúdo ou o impacto de um pacote, você pode:
>
>* Execute uma instalação de teste do pacote sem modificar qualquer conteúdo:
   >  Abra o pacote (clique no ícone ou nome do pacote) e clique em **Testar instalação**.
   >
   >
* Consulte uma lista de conteúdos do pacote:
   >  Abra o pacote e clique em **Conteúdo**.
>



>[!NOTE]
>
>Imediatamente antes da instalação do pacote, um pacote de snapshot é criado para conter o conteúdo que será substituído.
>
>Este instantâneo será reinstalado se/quando você desinstalar o pacote.

>[!CAUTION]
>
>Se você estiver instalando ativos digitais, deverá:
>
>* Primeiro, desative o WorkflowLauncher.
   >  Use a opção de menu Componentes do console OSGi para desativar `com.day.cq.workflow.launcher.impl.WorkflowLauncherImpl`.
   >
   >
* Em seguida, quando a instalação estiver concluída, reative o WorkflowLauncher.
>
>
Desativar o WorkflowLauncher garante que a estrutura do importador de Ativos não manipule (involuntariamente) os ativos na instalação.

1. No Gerenciador de pacotes, navegue até o pacote que deseja instalar.

   Um botão **Install (Instalar** ) é exibido na lateral de Packages que ainda não foram instalados.

   >[!NOTE]
   >
   >Como alternativa, você pode abrir o pacote clicando em seu ícone para acessar o botão **Instalar** .

1. Clique em **Instalar** para iniciar a instalação. Uma caixa de diálogo solicitará a confirmação e listará todas as alterações que estão sendo feitas. Quando terminar, clique em **Fechar** na caixa de diálogo.

   A palavra **Instalado** é exibida ao lado do pacote depois que ele é instalado.

### Upload e instalação baseados no sistema de arquivos {#file-system-based-upload-and-installation}

Há uma maneira alternativa de carregar e instalar pacotes na sua instância. Em seu sistema de arquivos, você tem uma `crx-quicksart` pasta junto com seu jar e `license.properties` arquivo. É necessário criar uma pasta com o nome `install` em `crx-quickstart`. Você terá algo assim: `<aem_home>/crx-quickstart/install`

Nesta instalação, pasta, você pode adicionar diretamente seus pacotes. Eles serão carregados e instalados automaticamente em sua instância. Quando terminar, você poderá ver os pacotes no Gerenciador de pacotes.

Se sua instância estiver sendo executada, a adição de um pacote à `install` pasta iniciará diretamente o upload e a instalação na instância. Se sua instância não estiver em execução, os pacotes que você colocar na `install` pasta serão instalados na inicialização, na ordem alfabética.

>[!NOTE]
>
>Você também pode fazer isso antes mesmo de iniciar a instância pela primeira vez. Para fazer isso, é necessário criar a `crx-quickstart` pasta manualmente, criar a `install` pasta abaixo dela e colocar os pacotes lá. Em seguida, quando você iniciar sua instância pela primeira vez, os pacotes serão instalados em ordem alfabética.

### Desinstalação de pacotes {#uninstalling-packages}

O AEM permite desinstalar pacotes. Essa ação reverte o conteúdo do repositório que é afetado ao snapshot feito imediatamente antes da instalação do pacote.

>[!NOTE]
>
>Durante a instalação, um pacote de snapshot é criado contendo o conteúdo que será substituído.
>
>Este pacote será reinstalado quando você desinstalar o pacote.

1. No Gerenciador de pacotes, navegue até o pacote que deseja desinstalar.
1. Clique no ícone de pacote do pacote que deseja desinstalar.
1. Clique em **Desinstalar** para remover o conteúdo deste pacote do repositório. Uma caixa de diálogo solicitará a confirmação e listará todas as alterações que estão sendo feitas. Quando terminar, clique em **Fechar** na caixa de diálogo.

### Excluindo pacotes {#deleting-packages}

Para excluir um pacote da(s) lista(s) do Gerenciador de pacotes:

>[!NOTE]
>
>Os arquivos/nós instalados do pacote **não** são excluídos.

1. No console **Ferramentas** , expanda a pasta **Pacotes** para mostrar seu pacote no painel direito.

1. Clique no pacote que deseja excluir para realçá-lo e depois:

   * Clique em **Excluir** no menu da barra de ferramentas.
   * Clique com o botão direito do mouse e selecione **Excluir**.
   ![packagesdelete](assets/packagesdelete.png)

1. O AEM solicita a confirmação de que você deseja excluir o pacote. Click **OK** to confirm the deletion.

>[!CAUTION]
>
>Se este pacote já tiver sido instalado, o conteúdo *instalado* **não** será excluído.

### Replicação de pacotes {#replicating-packages}

Replicar o conteúdo de um pacote para instalá-lo na instância de publicação:

1. No Gerenciador **de pacotes**, navegue até o pacote que você deseja replicar.

1. Clique no ícone ou no nome do pacote que deseja replicar para expandi-lo.
1. No menu suspenso **Mais** na barra de ferramentas, selecione **Replicar**.

## Compartilhamento de pacotes {#package-share}

O Compartilhamento de pacotes é um servidor centralizado disponibilizado publicamente para compartilhar Content-Packages.

Com o Compartilhamento de pacotes, você pode baixar esses pacotes, que podem incluir hotfixes oficiais, conjuntos de recursos, atualizações ou conteúdo de amostra gerado por outros usuários.

Você também pode carregar e compartilhar pacotes dentro da sua empresa.

### Acesso ao Compartilhamento de pacotes {#access-to-package-share}

Não há acesso anônimo ao Compartilhamento de pacotes; ou seja, somente usuários registrados podem exibir, baixar e carregar pacotes.

O acesso ao Compartilhamento de pacotes está disponível para nossos parceiros e clientes. Os dados de registro devem ser enviados para que os direitos de acesso sejam atribuídos.

Para obter acesso ao Compartilhamento de pacotes:

* Usar a página [Entrar](#signing-in-to-package-share)
* Na primeira vez que você usar a página de logon, será necessário:

   * [Registre-se em uma Adobe ID](#registering-for-package-share) e/ou [valide sua Adobe ID existente](#validating-your-adobe-id)
   * para que sua conta [de compartilhamento de](#package-share-account) pacotes possa ser criada

>[!NOTE]
>
>Qualquer usuário de Compartilhamento de pacotes que não tenha sido atribuído a um cliente deve ingressar em uma comunidade para ver esses recursos clicando em **Ingressar** ao lado do logon de compartilhamento de pacotes.

#### Fazer logon no compartilhamento de pacotes {#signing-in-to-package-share}

1. Na tela de boas-vindas do AEM, clique em **Ferramentas**.
1. Em seguida, selecione Compartilhamento **de pacotes**. Você deverá:

   * fazer logon com sua Adobe ID
   * [Criar uma Adobe ID](#registering-for-package-share)
   >[!NOTE]
   >
   >Na primeira vez que você fizer logon com sua Adobe ID, deverá concluir a [validação do seu endereço](#validating-your-adobe-id)de email.

   >[!NOTE]
   >
   >Se você esqueceu sua senha, use o link de páginas [de](https://enterprise-dev.adobe.com/content/edev/en/registration/account.html) Ajuda (também na caixa de diálogo de logon).

#### Validação da Adobe ID {#validating-your-adobe-id}

Na primeira vez que você entrar no Compartilhamento de pacotes com sua Adobe ID, seu endereço de email será validado.

1. Você receberá um email contendo um link.
1. Você precisa clicar neste link.
1. Uma página da Web será aberta.

   A ação de abrir esta página da Web é executada como validação.

1. O logon continuará.

1. Você receberá um email contendo um link.
1. Você precisa clicar neste link.
1. Uma página da Web será aberta. A ação de abrir esta página da Web é executada como validação.
1. O logon continuará.

#### Registrando-se no Compartilhamento de pacotes {#registering-for-package-share}

Se você precisar acessar o Compartilhamento de pacotes, será necessário se registrar para uma ID da Adobe:

* A página [de logon do Compartilhamento de](#signing-in-to-package-share) pacotes oferece um link para o registro de uma ID da Adobe.
* Você pode se registrar para uma Adobe ID de um certo software de desktop da Adobe.
* Como alternativa, você pode se registrar on-line na página [Logon da](https://www.adobe.com/cfusion/membership/index.cfm?nf=1&nl=1)Adobe.

Uma Adobe ID pode ser criada fornecendo:

* seu endereço de email
* uma senha de sua escolha
* algumas informações adicionais, como o seu nome e o país de residência

#### Conta de compartilhamento de pacotes {#package-share-account}

A validade do seu aplicativo será verificada antes de:

* Sua conta de usuário é criada com as permissões necessárias/permitidas.
* Sua conta é adicionada ao grupo de sua empresa.

>[!NOTE]
>
>Um usuário de uma de nossas empresas parceiras também pode ser membro de seus grupos de clientes.

#### Considerações de rede {#network-considerations}

**IPv6**

Você pode enfrentar problemas ao tentar acessar o Compartilhamento de pacotes a partir de um ambiente IPv6 puro.

Isso ocorre porque o compartilhamento de pacotes é um serviço hospedado em um servidor, o que significa que sua conexão é feita por meio de várias redes na Internet. Não é possível garantir que todas as redes de ligação suportem o IPv6; caso contrário, a conexão pode falhar.

Para evitar esse problema, você pode acessar o Compartilhamento de pacotes de uma rede IPv4, baixar o pacote e, em seguida, carregá-lo no ambiente IPv6.

**Proxy HTTP**

O Compartilhamento de pacotes não está disponível no momento se sua empresa executa um proxy http que requer autenticação.

O Compartilhamento de pacotes só está disponível quando o servidor AEM tem acesso à Internet sem necessidade de autenticação. Para configurar o proxy para todos os serviços que usam o cliente http (incluindo o compartilhamento de pacote), use a configuração [OSGi do pacote](/help/sites-deploying/osgi-configuration-settings.md)Day Commons HTTP Client 3.1.

### Compartilhamento de pacotes internos {#inside-package-share}

Em pacotes de Compartilhamento de pacotes estão organizados em subárvores de três:

* Pacotes da Adobe fornecidos pela Adobe.
* Pacotes compartilhados fornecidos por outras empresas e tornados públicos pela Adobe.
* Pacotes privados da sua empresa.

![chlimage_1-110](assets/chlimage_1-110.png)

### Como pesquisar e filtrar pacotes {#searching-and-filtering-packages}

O Compartilhamento de pacotes oferece uma barra de pesquisa que você pode usar para pesquisar palavras-chave ou tags específicas. As palavras-chave e tags são compatíveis com vários valores.

* Para procurar várias palavras-chave, é necessário separar cada palavra-chave por um espaço.
* Para pesquisar por várias tags, é necessário selecionar cada uma delas nas árvores do pacote.

Você também pode alterar o operador condicional de OU para E, no lado direito da barra de resumo do filtro.

### Download E Instalação De Pacotes Do Compartilhamento De Pacotes {#downloading-and-installing-packages-from-package-share}

Para baixar pacotes do Compartilhamento de pacotes e instalá-los em sua instância local, é mais fácil acessar o Compartilhamento de pacotes de sua instância do AEM. Isso fará o download do pacote e o registrará imediatamente no Gerenciador de pacotes, de onde ele pode ser instalado.

1. Na tela de Boas-vindas do AEM, clique em **Ferramentas** e selecione Compartilhamento **de** pacotes para abrir a página Compartilhamento de pacotes.
1. Usando os detalhes de sua conta, faça logon no Compartilhamento de pacotes. A página inicial é exibida, listando a pasta Adobe, a pasta Compartilhada e uma específica para a sua empresa.

   >[!NOTE]
   >
   >Antes de começar a baixar pacotes do Compartilhamento de pacotes, verifique se você tem o acesso [](#access-to-package-share)necessário.

1. Navegue até o pacote que deseja baixar e clique em **Download**.

1. Volte ou navegue até o Gerenciador **de** pacotes na sua instância do AEM. Em seguida, navegue até o pacote que você acabou de baixar.

   >[!NOTE]
   >
   >Para localizar o pacote baixado, siga o mesmo caminho do Compartilhamento de pacotes. Por exemplo, se você baixou um pacote do seguinte caminho no Compartilhamento de pacotes:
   >
   >**Pacotes** > **Público** > **Hotfixes**
   Em seguida, no Package Manager em sua instância local, o pacote também será exibido em:
   **Pacotes** > **Público** > **Hotfixes**

1. Clique em **Instalar** para instalar o pacote na instalação local do AEM.

   >[!NOTE]
   Se o pacote já tiver sido instalado em sua instância, o indicador **Instalado** será exibido ao lado do pacote em vez do botão **Instalar** .

   >[!CAUTION]
   A instalação de um pacote pode substituir o conteúdo existente no repositório. Portanto, recomendamos que você execute uma instalação **de** teste primeiro. Isso permite que você verifique se o conteúdo do pacote está em conflito com o conteúdo existente.

### Download de pacotes para seu sistema de arquivos do Compartilhamento de pacotes {#downloading-packages-to-your-file-system-from-package-share}

[Baixar e instalar](#downloading-and-installing-packages-from-package-share) é muito conveniente, mas, se necessário, você também pode baixar o pacote e salvá-lo no sistema de arquivos local:

1. Em Compartilhamento de pacotes, clique no ícone ou nome do pacote.
1. Click the **Assets** tab.
1. Clique em **Download para disco**.

### Carregar um pacote {#uploading-a-package}

Com o Compartilhamento de pacotes, você pode fazer upload de pacotes para a área interna de compartilhamento de pacotes da sua empresa. Isso os torna disponíveis para compartilhamento em sua empresa.

Esses pacotes *não* estão disponíveis para a comunidade geral do AEM, mas estão disponíveis para todos os usuários registrados em sua empresa.

Para fazer upload de pacotes, faça o compartilhamento de pacotes interno da empresa:

>[!CAUTION]
Para carregar um pacote no Compartilhamento de pacotes, primeiro é necessário criar uma pasta de grupo com o nome da empresa no Gerenciador de pacotes local. Por exemplo, geometrixx. Todos os pacotes a serem carregados para compartilhamento devem ser colocados nesta pasta de grupo.
Os pacotes na lista inicial do Gerenciador de pacotes ou em outras pastas não podem ser compartilhados.

1. Abra o Gerenciador **de pacotes** e navegue até o pacote que deseja carregar.

1. Clique no ícone do pacote para abri-lo.
1. Clique em **Compartilhar** para abrir a caixa de diálogo para fazer upload do pacote no Compartilhamento de pacotes.
1. Se ainda não estiver conectado ao Compartilhamento de pacotes, será necessário inserir suas credenciais de logon.

   Quando você estiver conectado, o AEM exibirá detalhes sobre o pacote a ser carregado:

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. Clique em **Compartilhar** para carregar o pacote no Compartilhamento de pacotes interno da sua empresa.

   O AEM exibe o status e indica quando o pacote terminou de ser carregado, depois disso você pode clicar no **x** (canto superior direito) para sair da janela **Compartilhar pacote** .

1. Após a conclusão do upload, você pode navegar até a pasta interna da sua empresa para ver o pacote que você acabou de compartilhar.

>[!NOTE]
Para modificar um pacote disponível em Compartilhamento de pacotes, é necessário baixá-lo, recriá-lo e carregá-lo novamente no Compartilhamento de pacotes.

### Excluindo Um Pacote {#deleting-a-package}

Você só pode excluir os pacotes que carregou por meio do procedimento a seguir:

1. Na árvore da empresa, verifique o grupo de pacotes que contém o pacote.
1. Clique no pacote.
1. Clique no botão Excluir.

   ![chlimage_1-18](do-not-localize/chlimage_1-30.png)

1. Clique em **Excluir** para confirmar que deseja excluir o pacote.

### Como tornar os pacotes semisprivados {#making-packages-semi-private}

Você pode compartilhar pacotes fora da sua organização, mas não publicamente. Estes pacotes seriam considerados semiprivados. Para compartilhar esses pacotes semiprivados, você precisará de ajuda do Suporte da Adobe. Para fazer isso, abra um ticket com o Suporte da Adobe solicitando que um pacote seja disponibilizado fora da organização. Eles solicitarão uma lista das IDs da Adobe que você deseja conceder acesso aos seus pacotes.

## Distribuição de software (Beta) {#software-distribution-beta}

[Distribuição](https://downloads.experiencecloud.adobe.com) de software é a nova interface do usuário projetada para simplificar a pesquisa e o download de pacotes AEM. Atualmente, ele está em status beta e só pode ser acessado pelos Adobe Managed Services e AEM como clientes do Cloud Service, bem como pelos funcionários da Adobe.

>[!NOTE]
* [O Compartilhamento](#package-share) de pacotes permanecerá em operações até que todos os clientes tenham acesso à Distribuição de software.
* Todos os pacotes estão disponíveis em Compartilhamento de pacotes e Distribuição de software.


>[!CAUTION]
O gerenciador de pacote AEM não pode ser usado com a Distribuição de software no momento, você pode baixar seus pacotes no disco local.

