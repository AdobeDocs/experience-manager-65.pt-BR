---
title: Importação e exportação de ativos para o AEM Forms
seo-title: Importação e exportação de ativos para o AEM Forms
description: É possível importar e exportar formulários e modelos adaptáveis de e para instâncias de AEM. Isso ajuda a migrar formulários ou movê-los pelos sistemas.
seo-description: É possível importar e exportar formulários e modelos adaptáveis de e para instâncias de AEM. Isso ajuda a migrar formulários ou movê-los pelos sistemas.
uuid: 937daedd-56f3-4e02-b695-b194b494d9bf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 69210727-dde3-495a-87b7-2e8173e6b664
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2549'
ht-degree: 1%

---


# Importação e exportação de ativos para o AEM Forms{#importing-and-exporting-assets-to-aem-forms}

É possível mover formulários e ativos relacionados, temas, dicionários de dados, fragmentos de documento e letras entre diferentes instâncias do AEM Forms. Esse movimento é necessário ao migrar sistemas ou mover formulários de um servidor de estágio para um servidor de produção. Para os ativos para os quais o upload e a importação por meio da interface do usuário do AEM Forms são compatíveis, usar a interface do usuário do Forms é a maneira recomendada para exportar ou importar. Não é recomendado usar o Gerenciador de pacotes AEM para exportar ou importar esses ativos.

>[!NOTE]
>
>* No AEM 6.4 Forms, a estrutura e os caminhos do repositório crx foram alterados. Se você importar ativos de uma versão anterior para o AEM 6.4 Forms e o formulário tiver algumas dependências na estrutura mais antiga, será necessário exportar manualmente as dependências. Para obter detalhes sobre alterações na estrutura e caminhos do repositório, consulte [Reestruturação do Repositório em AEM](/help/sites-deploying/repository-restructuring.md).

>



## Baixe ou faça upload dos ativos Forms e Documents {#download-or-upload-forms-amp-documents-assets}

A interface do usuário do AEM Forms permite exportar ativos de uma instância do AEM baixando-os como um pacote CRX ou arquivos binários AEM. Em seguida, você pode importar o pacote AEM CRX baixado ou o arquivo binário para outra instância AEM.

A exportação e a importação por meio da interface do usuário do AEM Forms são suportadas em todos os ativos, exceto nos modelos de formulário adaptável e nas políticas de conteúdo do formulário adaptável. Portanto, ao exportar um formulário adaptável da interface do usuário do AEM Forms, o modelo de formulário adaptável relacionado e as políticas de conteúdo não são exportados automaticamente como outros ativos relacionados.

Para esses tipos de ativos, você deve usar AEM Gerenciador de Pacotes para criar um pacote CRX no servidor de AEM de origem e instalar o pacote no servidor de destino. Para obter informações sobre como criar e instalar pacotes, consulte [Trabalhar com pacotes](/help/sites-administering/package-manager.md).

### Baixar ativos do Forms &amp; Documents {#download-forms-amp-documents-assets}

Para baixar os ativos Forms &amp; Documents :

1. Faça logon na instância do AEM Forms.
1. Toque no ícone Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > navegação ![ícone de bússola](assets/compass.png) > Forms > Forms &amp; Documents.
1. Selecione os ativos de formulários e toque no ícone **Download**.
1. Em Baixar ativo(s), escolha uma das opções a seguir e toque em **Baixar**.

   * **Baixar como pacote CRX:** use a opção para baixar e mover todos os ativos selecionados e dependências relacionadas de uma instância do AEM Forms para outra. Ele baixa todos os ativos e pastas como pacote crx. Qualquer ativo(s) de formulário, incluindo os formulários criados em AEM (formulários adaptáveis, Comunicações interativas e fragmentos de formulário adaptáveis), conjuntos de formulários, modelos de formulário, documentos PDF e recursos (XSDs, XFS, imagens) podem ser baixados como pacote da interface do usuário do AEM Forms.
A vantagem de baixar ativos como pacote é que ele também baixa ativos que foram usados pelo ativo selecionado para download. Por exemplo, se você tiver um formulário adaptável que use um modelo de formulário, XSD e uma imagem. Ao selecionar esse formulário adaptável e baixá-lo como pacote, o pacote baixado também contém o modelo de formulário, o XSD e a imagem. Todas as propriedades de metadados (incluindo propriedades personalizadas) associadas ao ativo também são baixadas.

   * **Baixar ativos como arquivos binários:** use a opção para baixar somente modelos de formulário (XDP), PDF forms (PDF), documento (PDF) e recursos (imagens, esquemas, folhas de estilos). É possível editar esses ativos com aplicativos externos. Ele baixa os ativos de formulários que têm binários, como XSDs, XDPs, imagens, PDFs e XDPs como um arquivo .zip.
Não é possível baixar formulários adaptáveis, Comunicações interativas, fragmentos de formulário adaptáveis, temas e conjuntos de formulários com a opção **Baixar ativos como arquivos binários**. Para baixar esses ativos, você deve usar a opção **Baixar como pacote CRX**.

   Os ativos selecionados são baixados como um arquivo morto (arquivo .zip).

   >[!NOTE]
   >
   >O pacote AEM e os arquivos binários são baixados como um arquivo (arquivo .zip). Os modelos para os ativos não são baixados junto com os ativos. É necessário exportar os modelos de ativos separadamente.

### Fazer upload dos ativos Forms e Documents {#upload-forms-amp-documents-assets}

Para fazer upload dos ativos Forms &amp; Documents :

>[!VIDEO](https://vimeo.com/)

1. Faça logon na instância do AEM Forms.
1. Toque no ícone Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > navegação ![ícone de bússola](assets/compass.png)> Forms> Forms &amp; Documents.
1. Toque em **Criar** >**Carregar arquivo**. Uma caixa de diálogo carregar formulários ou pacotes é exibida.
1. Na caixa de diálogo , navegue e selecione o pacote ou o arquivo a ser importado. Você também pode selecionar documentos PDF, XSDs, imagens, folhas de estilos e formulários XDP. Toque em **Abrir**. A pasta ou o nome de arquivo selecionado não deve incluir caracteres especiais.

   Na caixa de diálogo, verifique os detalhes dos ativos que estão sendo carregados e toque em **Upload**.

   Caso faça upload de um ativo de formulários existente, o ativo é atualizado.

   >[!NOTE]
   >
   >O upload de um pacote não substitui a hierarquia de pastas existente. Por exemplo, se você tiver um formulário adaptável chamado &quot;Treinamento&quot; no local /content/dam/formsanddocuments em um servidor. Você faz o download do formulário adaptável e faz o upload do formulário em outro servidor. O segundo servidor também tem uma pasta com o nome &#39;Treinamento&#39; no mesmo local /content/dam/formsanddocuments. O upload falha.

## Download ou upload de um tema {#downloading-or-uploading-a-theme}

Com o AEM Forms, você pode criar, baixar ou fazer upload de temas. Um tema é criado como outros ativos, como formulários, documentos e cartas. Você pode criar um tema, baixá-lo e carregá-lo em uma instância separada para reutilizá-lo. Para obter mais informações sobre temas, consulte [Temas no AEM Forms](../../forms/using/themes.md).

### Download de um tema {#downloading-a-theme}

É possível exportar temas no AEM Forms que você pode usar em outros projetos ou instâncias. AEM permite baixar o tema como um arquivo zip, que você pode fazer upload na instância.

Para baixar um tema:

1. Faça logon na instância do AEM Forms.
1. Toque no ícone Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > navegação ![ícone de bússola](assets/compass.png)> Forms> Temas.
1. Selecione o tema e toque em **Download**. O tema é baixado como um arquivo (arquivo .zip).

### Fazer upload de um tema {#uploading-a-theme}

É possível usar os temas criados com predefinições de estilização em seu projeto. Você pode importar pacotes de temas criados por outras pessoas, carregando-os no seu projeto.

Para fazer upload de um tema:

1. No Experience Manager, navegue até **Forms > Temas**.
1. Na página Temas , clique em **Criar > Upload de arquivo**.
1. No prompt Upload de arquivo, procure e selecione um pacote de temas no seu computador e clique em **Upload**.
O tema carregado está disponível na página de temas.

1. Faça logon na instância do AEM Forms.
1. Toque no ícone Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > navegação ![ícone de bússola](assets/compass.png)> Forms> Temas.
1. clique em **Criar** > **Upload de Arquivo**. No prompt Upload de arquivo, procure e selecione um pacote de temas no seu computador e clique em **Upload**. O tema é carregado.

## Importar e exportar ativos no Gerenciamento de correspondência {#import-and-export-assets-in-correspondence-management}

Para compartilhar ativos, como dicionários de dados, cartas e fragmentos de documento, entre duas implementações diferentes do Gerenciamento de correspondência, você pode criar e compartilhar arquivos .cmp. Um arquivo .cmp pode incluir um ou mais dicionários de dados, letras, fragmentos de documento e formulários.

### Exportar fragmentos de documento, letras e/ou dicionários de dados {#export-document-fragments-letters-and-or-data-dictionaries}

1. Nas letras, fragmentos de documento ou páginas de dicionário de dados, toque e selecione os ativos que deseja exportar para um único pacote e toque em Fila para download. Os ativos são alinhados para exportação.
1. Conforme necessário, repita a etapa acima para adicionar letras, fragmentos de documento e dicionários de dados.
1. Toque em **Baixar**.
1. O Gerenciamento de correspondência exibe a caixa de diálogo Baixar ativos com uma lista de ativos na lista de exportação.

   ![exportar](assets/export.png)

1. Para exibir as dependências exportadas, toque em Resolver. Ou pule para a próxima etapa. Mesmo que você não toque em resolver, as dependências ainda serão exportadas.
1. Para baixar o arquivo .cmp, toque em **OK**.
1. O Gerenciamento de correspondência baixa um arquivo .cmp em seu computador.

   O arquivo .cmp inclui os ativos exportados. Você pode compartilhar o arquivo .cmp com outras pessoas. Outros usuários podem importar o arquivo .cmp em um servidor diferente para obter todos os ativos no novo servidor.

### Exportar todos os ativos de Gerenciamento de correspondência como um pacote {#export-all-the-correspondence-management-assets-as-a-package}

Use essa opção para baixar todos os ativos de Gerenciamento de correspondência e dependências relacionadas como um pacote de uma instância de formulários AEM.

Por exemplo, se o Gerenciamento de correspondência tiver uma carta que usa uma imagem e texto, o pacote baixado também conterá a imagem e o texto relacionado à carta. Todas as propriedades de metadados (incluindo propriedades personalizadas) associadas ao ativo também são baixadas. Depois de baixar o pacote (.cmp), você poderá [importar o pacote para uma instância diferente do AEM Forms](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p).

Para baixar todos os ativos de Gerenciamento de correspondência e dependências relacionadas como um pacote, siga estas etapas:

1. Faça logon no AEM Forms Server como usuário de formulários.
1. Toque em **Adobe Experience Manager** na barra Navegação global.
1. Toque nas ferramentas ( ![ferramentas](assets/tools.png)) e toque em **Forms**.
1. Toque em **Exportar ativos de gerenciamento de correspondência**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   ( &quot;A página Exportar todos os ativos de gerenciamento de correspondência é exibida e exibe as informações sobre a última vez que o processo de exportação foi tentado e um link para baixar o último pacote exportado com êxito.

   ![export-last-run-details](assets/export-last-run-details.png)

1. Toque em **Exportar** e, na mensagem de confirmação, toque em **OK**.

   Após a conclusão de um processo em lote, os detalhes da última execução e o link para baixar o pacote são atualizados. Isso inclui informações como o login do Administrador e se o lote foi executado com êxito ou falhou. Os ativos são exportados para um pacote e o link Download do pacote exportado é exibido.

   >[!NOTE]
   >
   >O processo Exportar todos os ativos não pode ser cancelado uma vez iniciado. Além disso, enquanto a operação exportar todos estiver em andamento, não crie, exclua, modifique ou publique quaisquer ativos ou inicie o processo Publicar todos os ativos.a

1. Toque no link **Baixar pacote exportado** para baixar o arquivo do pacote.

   Para adicionar os ativos no pacote a outra instância do Correspondence Management, [importe o pacote para uma instância do AEM Forms](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p).

### Importar fragmentos de documento, letras e/ou dicionários de dados para o Gerenciamento de correspondência {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

Você pode importar ativos que são exportados para um arquivo .cmp . Um arquivo .cmp pode ter uma ou mais letras, dicionários de dados, fragmentos de documento e ativos dependentes.

>[!NOTE]
>
>Ao importar ativos antigos de Gerenciamento de correspondência para migração, faça logon usando uma conta de administrador. Para obter mais informações sobre Migração de ativos antigos do Gerenciamento de correspondência, consulte [Migrar ativos do Gerenciamento de correspondência para AEM formulários 6.1](/help/forms/using/migration-utility.md).

1. Na página de dicionário de dados, letras ou fragmentos de documento, toque em **Criar > Upload de arquivo** e selecione o arquivo .cmp.
1. O Gerenciamento de correspondência exibe a caixa de diálogo Importar ativos com a lista de ativos importados. Toque em **Importar**.

   Após importar os ativos, as seguintes propriedades dos ativos são atualizadas, enquanto as outras propriedades permanecem as mesmas:

   * Autor: Exibe a ID do usuário que importou o ativo para o servidor
   * Modificado: O momento em que o ativo foi importado para o servidor

   >[!NOTE]
   >
   >Para que você possa fazer upload de XDPs (como parte do arquivo cmp ou de outro modo), é necessário fazer parte do grupo forms-power-users . Para obter direitos de acesso, entre em contato com o administrador.

## Exportar um aplicativo de workflow {#export-a-workflow-application}

Você pode usar AEM gerenciador de pacotes para exportar aplicativos de fluxo de trabalho. O procedimento está listado abaixo:

1. Abra o gerenciador de pacotes do AEM Forms. O URL do gerenciador de pacotes é https://&lt;server>:&lt;port>/crx/packmgr.
1. Clique em **[!UICONTROL Criar pacote]**. A caixa de diálogo **[!UICONTROL Novo pacote]** é exibida.
1. Especifique o nome, a versão e o grupo do pacote. Clique em **[!UICONTROL OK]**.
1. Clique em **[!UICONTROL Editar]** e abra a guia **[!UICONTROL Filtros]**. Clique em **[!UICONTROL Adicionar filtro]**. Especifique o caminho do aplicativo de fluxo de trabalho. Por exemplo, /etc/fd/dashboard/startpoints/homemortgauge. Clique em **[!UICONTROL Adicionar regra]**.

1. Abra a guia **[!UICONTROL Avançado.]** Selecione **[!UICONTROL Merge]** ou **[!UICONTROL Overwrite]** no campo Manuseio de ACL. Clique em **[!UICONTROL Salvar]**.
1. Clique em **[!UICONTROL Build]** para criar o pacote.

   Após a criação do pacote, é possível baixá-lo e importá-lo para o outro servidor. O aplicativo de workflow aparece no servidor onde o pacote é carregado.

   >[!NOTE]
   >
   >Para que o aplicativo de fluxo de trabalho funcione corretamente, exporte também o formulário adaptável correspondente e o modelo de fluxo de trabalho com o aplicativo de trabalho.

## Pastas e organização de ativos {#folders-and-organizing-assets}

A interface do usuário do AEM Forms usa pastas para organizar ativos. Essas pastas são usadas para organizar ativos criados na interface do usuário do AEM Forms. É possível renomear, criar subpastas e armazenar ativos e documentos nessas pastas. Organizar documentos e ativos em uma pasta permite agrupar os arquivos para fácil gerenciamento. Você pode selecionar uma pasta e optar por baixá-la ou excluí-la.

Para criar uma pasta, conclua as seguintes etapas:

### Crie uma pasta {#create-a-folder}

1. Faça logon na interface do usuário do AEM Forms em `https://<server>:<port>/aem/forms.html`.
1. Navegue até o local em que deseja criar uma pasta.
1. Toque em Criar > Pasta.
1. Insira os seguintes detalhes:

   * **Título:** Exibir nome da pasta
   * **Nome:** *(Obrigatório)* O nome do nó no qual você deseja armazenar a pasta no repositório

   >[!NOTE]
   >
   >Por padrão, o valor do campo de nome é preenchido automaticamente a partir do título. O nome só pode conter caracteres alfanuméricos ou os caracteres especiais de hífen (-) e sublinhado (_). Quaisquer outros caracteres especiais inseridos no título serão substituídos automaticamente por um hífen e você será solicitado a confirmar o novo nome. Você pode optar por continuar com o nome sugerido ou editá-lo ainda mais.

1. Uma nova pasta com o título definido é exibida no local atual na lista de ativos.

   Se existir uma pasta com o nome especificado, o envio falhará com um erro. Você pode exibir a mensagem de erro passando o mouse sobre o ícone de erro ![aem6forms_error_alert](assets/aem6forms_error_alert.png) que aparece ao lado do campo de nome.

   Toque na pasta recém-criada para entrar na pasta e criar ativos ou pastas dentro dela. Além disso, você pode selecionar uma pasta e escolher colocá-la em fila para download, excluí-la ou editar seu nome.

   ![editdeletedownloadafolder](assets/editdeletedownloadafolder.png)

### Criar cópias de um ou mais ativos ou cartas {#create-copies-of-one-or-more-assets-or-letters}

Você pode usar ativos e cartas existentes para criar rapidamente ativos e cartas com propriedades, conteúdo e ativos herdados semelhantes. Você pode copiar e colar dicionários de dados, fragmentos de documento e letras.

Complete as etapas a seguir para criar cópias de ativos e cartas:

1. Na página Ativos ou Cartas relevante, selecione um ou mais ativos/cartas. A interface do usuário exibe o ícone Copiar .
1. Toque em Copiar. A interface do usuário exibe o ícone Colar. Você também pode optar por ir/navegar dentro de uma pasta antes de colar. Pastas diferentes podem conter ativos com os mesmos nomes. Para obter mais informações sobre pastas, consulte [Pastas e organização de ativos](#folders-and-organizing-assets).
1. Toque em Colar. A caixa de diálogo Colar é exibida. O sistema gera automaticamente nomes e títulos para as novas cópias de ativos/letras, mas você pode editar os títulos e os nomes dos ativos/letras.

   Se você estiver copiando e colando os ativos/letras no mesmo local, um sufixo &quot;-CopyXX&quot; será adicionado ao nome existente do ativo/letra. Se não existir um título para o ativo/carta copiada, o campo de título gerado automaticamente permanecerá em branco.

1. Se necessário, edite o Título e o Nome com os quais deseja salvar a cópia do ativo/carta.
1. Toque em Colar. Novas cópias dos ativos copiados são criadas.

## Pesquisar {#search-forms}

A interface do usuário do AEM Forms permite pesquisar seu conteúdo. Usando a barra superior, você pode tocar em Pesquisar **[A]** para pesquisar seu conteúdo em busca de recursos, como ativos e documentos.

Ao pesquisar ativos, o AEM Forms exibe o painel lateral. Você também pode tocar em ![assets-browser-content-only](assets/assets-browser-content-only.png) > Filtrar **[B]** para chamar o painel lateral. Usando os vários filtros no painel lateral, você pode limitar a pesquisa. O painel lateral também permite salvar suas pesquisas.

![search_topbar](assets/search_topbar.png)

**A.** Pesquisar  **B.** Filtro

![Painel lateral - Filtros](assets/search_sidepanel.png)

Painel lateral - Filtros

No painel lateral, você pode usar o seguinte para limitar os resultados da pesquisa:

* Diretório de pesquisa
* Tags
* Critérios de pesquisa; por exemplo, datas modificadas, status de publicação, status da Live Copy. 

O painel lateral também permite salvar suas configurações de pesquisa com nomes de sua escolha.

Para obter mais informações e instruções sobre como usar pesquisa, filtros, pesquisa salva e painel lateral, consulte [Pesquisar](/help/sites-authoring/search.md).
