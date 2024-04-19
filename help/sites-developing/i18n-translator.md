---
title: Usar o Translator para gerenciar dicionários
description: O AEM fornece um console para gerenciar as várias traduções de textos usados na interface do usuário do componente
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
exl-id: a8d50c09-72d0-406e-874e-50a985227a56
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '2318'
ht-degree: 0%

---

# Usar o Translator para gerenciar dicionários{#using-translator-to-manage-dictionaries}

O AEM fornece um console para gerenciar as várias traduções de textos usados na interface do usuário do componente. Este console está disponível em

`https://<hostname>:<port-number>/libs/cq/i18n/translator.html`

Use a ferramenta de tradução para gerenciar cadeias de caracteres em inglês e suas traduções. Os dicionários são criados no repositório, por exemplo, /apps/myproject/i18n.

A ferramenta Tradutor e os dicionários gerenciados são usados para apresentar a interface do usuário do componente em diferentes idiomas. Se quiser traduzir uma página ou conteúdo gerado pelo usuário, consulte [Tradução de conteúdo para sites multilíngues](/help/sites-administering/translation.md) e [Tradução de conteúdo gerado pelo usuário](/help/communities/translate-ugc.md).

>[!CAUTION]
>
>Edite somente os dicionários criados para o seu projeto e localizados em `/apps`.
>
>Dicionários do sistema AEM também estão disponíveis nesta ferramenta. Não altere os dicionários do sistema AEM, pois isso pode causar problemas com a interface AEM. Além disso, as alterações podem ser perdidas na atualização. Os dicionários do sistema AEM estão localizados em `/libs`.

>[!NOTE]
>
>Embora a ferramenta Translator tenha uma interface de interface clássica, ela é usada para tradução de frases, independentemente da interface em que essas frases são encontradas.

O tradutor relaciona os textos usados no AEM com as várias traduções de idiomas ao lado umas das outras:

![chlimage_1-205](assets/chlimage_1-205.png)

Você pode pesquisar, filtrar e editar os textos em inglês e traduzido. Você também pode exportar dicionários para o formato XLIFF para tradução e, em seguida, importar as traduções de volta para os dicionários.

Também é possível adicionar os dicionários i18n a um projeto de tradução a partir desse console. Você pode criar um ou adicionar a um projeto existente.

1. Clique em **Traduzir dicionário**.

   ![chlimage_1-206](assets/chlimage_1-206.png)

1. Selecione a opção Criar ou Adicionar dependendo da sua necessidade. Uma caixa de diálogo é aberta.

   ![chlimage_1-207](assets/chlimage_1-207.png)

1. Preencha os campos conforme necessário e clique em OK. ![chlimage_1-208](assets/chlimage_1-208.png)

1. Clique agora em **OK** ou consulte o Dicionário do Target.

   >[!NOTE]
   >
   >Para obter mais informações sobre projetos de tradução, leia [Gerenciamento de projetos de tradução](/help/sites-administering/tc-manage.md).

## Criando um dicionário {#creating-a-dictionary}

Crie um dicionário para gerenciar suas cadeias de caracteres localizadas da interface do usuário. Depois de criar um dicionário, você pode usar a ferramenta Tradução para gerenciá-lo.

1. Usando o CRXDE Lite, adicione o nó raiz ( `sling:Folder`) para o novo dicionário como a estrutura que armazena as definições de idioma:

   ` /apps/<projectName>/i18n`

   Por exemplo, `/apps/myProject/i18n`

1. Adicione a estrutura de idioma necessária nesta raiz. Por exemplo:

   ```shell
   /apps/myProject/i18n [sling:Folder]
       - de.json [nt:file] [mix:language]
           + jcr:language = de
       - fr.json [nt:file] [mix:language]
           + jcr:language = fr
   ```

   >[!NOTE]
   >
   >Esta é a estrutura do [Módulo Sling i18n](https://sling.apache.org/site/internationalization-support.html).

1. Recarregue o tradutor e o caminho do dicionário (por exemplo, `/apps/myProject/i18n`) estarão disponíveis no seletor suspenso na barra de ferramentas. Selecione essa opção para começar a adicionar strings e suas traduções.

   >[!NOTE]
   >
   >O tradutor só salvará traduções para idiomas que estejam realmente presentes abaixo do caminho (por exemplo, `/apps/myProject/i18n`).
   >
   >Verifique se eles correspondem aos idiomas mostrados na grade.

## Gerenciar strings de dicionário {#managing-dictionary-strings}

Use a ferramenta Tradução para gerenciar as cadeias de caracteres em seus dicionários. Você pode adicionar, modificar e remover cadeias de caracteres em inglês e também fornecer cadeias de caracteres traduzidas.

>[!CAUTION]
>
>Edite somente os dicionários criados para o seu projeto e localizados em `/apps`.
>
>Não altere os dicionários do sistema AEM, pois isso pode causar problemas com a interface AEM. Além disso, as alterações podem ser perdidas na atualização. Os dicionários do sistema AEM estão localizados em `/libs`.

### Adição, Alteração e Remoção de Strings {#adding-changing-and-removing-strings}

Adicione cadeias de caracteres em inglês a um dicionário internacionalizado por seu componente. Adicione somente strings internacionalizadas para não desperdiçar recursos traduzindo strings que não são usadas.

As cadeias de caracteres adicionadas a um dicionário devem corresponder exatamente à cadeia especificada no código. Se a cadeia de caracteres padrão em inglês que é usada no código não corresponder à cadeia de caracteres em inglês em um dicionário, a cadeia de caracteres traduzida não aparecerá na interface do usuário quando necessário. As cadeias de caracteres fazem distinção entre maiúsculas e minúsculas.

**Fornecer dicas de tradução**

Use a propriedade Comentário da string do dicionário para fornecer informações ao tradutor para esclarecer o significado da string. Normalmente, a interface auxilia os usuários a determinar o significado de palavras ambíguas. No entanto, o tradutor não vê a cadeia de caracteres no contexto da interface do usuário. A dica de tradução remove a ambiguidade. Por exemplo, um comentário ajuda o tradutor a entender que a palavra em inglês Request é usada como um substantivo em vez de um verbo.

As dicas de tradução também distinguem strings idênticas e com significados diferentes. Por exemplo, a palavra Pesquisa pode ser um substantivo ou um verbo, o que requer duas entradas de &quot;Pesquisa&quot; no dicionário com duas dicas de tradução diferentes. O código que solicita a cadeia de caracteres também inclui a dica de tradução para que a cadeia correta seja usada na interface do usuário.

**Inclusão de variáveis indexadas**

Inclua variáveis na string localizada para criar significado contextual em uma frase. Por exemplo, depois de fazer logon em um aplicativo web, a página inicial exibe a mensagem &quot;Bem-vindo de volta, Administrador. Você tem duas mensagens na sua caixa de entrada.&quot; O contexto da página determina o nome de usuário e o número de mensagens.

Para incluir variáveis na string localizada, coloque os índices entre colchetes no local das variáveis no primeiro argumento do método get. Use a dica de localização para descrever os valores. O tradutor deve entender o significado das variáveis porque línguas diferentes usam estruturas de frases diferentes.

Observe que [o código que solicita a cadeia de caracteres traduzida](/help/sites-developing/i18n-dev.md#including-variables-in-localized-sentences) O fornece valores para as variáveis indexadas de acordo com o contexto.

Por exemplo, a seguinte string é exibida quando um usuário faz logon em um site e é incluída no dicionário:

`Welcome back {0}. You have {1} messages.`

O Comentário a seguir descreve as variáveis:

`{0} = the user name, {1} = the number of items in the user's inbox`

**Modificação de strings**

Altere ou remova cadeias de caracteres em inglês à medida que são alteradas ou removidas no código. Quando você altera uma string, a string original é mantida e uma nova string é feita refletindo a alteração. Antes de remover uma string, verifique se nenhum código a usa.

Use o procedimento a seguir para adicionar uma string.

1. No menu suspenso Dicionários, selecione o dicionário ao qual está adicionando uma string. No menu suspenso, os dicionários são representados pelo caminho no repositório.
1. Acima da tabela Strings e traduções, clique em Adicionar.

   ![chlimage_1-209](assets/chlimage_1-209.png)

1. Na caixa String da caixa de diálogo Adicionar string, digite a string em inglês. Na caixa Comentário, digite uma dica de tradução para o tradutor, se necessário.
1. Clique em OK.
1. Clique em Salvar.

   ![chlimage_1-210](assets/chlimage_1-210.png)

Use o procedimento a seguir para alterar uma string em um dicionário.

1. No menu suspenso Dicionários, selecione o dicionário que contém a sequência de caracteres a ser alterada.
1. Clique duas vezes na sequência de caracteres a ser alterada.
1. Na caixa de diálogo Editar string, selecione Modificar string ou Comentário (Cria uma cópia).

   ![chlimage_1-211](assets/chlimage_1-211.png)

1. Modifique a cadeia de caracteres ou o comentário e clique em OK.
1. Clique em Salvar.

   ![chlimage_1-212](assets/chlimage_1-212.png)

Use o procedimento a seguir para remover uma string de um dicionário.

1. No menu suspenso Dicionários, selecione o dicionário do qual você está removendo uma string.
1. Clique em Remover.

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. Clique em Salvar.

   ![chlimage_1-214](assets/chlimage_1-214.png)

### Pesquisando Strings {#searching-for-strings}

A barra de pesquisa na parte inferior da ferramenta Tradutor fornece opções de seleção de strings:

* **Filtrar por texto:** Um padrão para corresponder à sequência de caracteres, ao comentário ou às traduções em inglês. Somente itens que correspondem a todo ou parte do padrão aparecem na tabela.
* **Alterações: Qualquer, Modificado, Novo, Excluído:** Mostrar itens que foram alterados e não foram salvos.

   * Qualquer um: mostra itens que foram modificados, adicionados ou removidos.
   * Modificado: mostra itens que foram alterados.
   * Novo: mostra itens que foram adicionados.
   * Excluído: mostra os itens que serão removidos.
   * Várias seleções: mostra itens que têm todas as propriedades selecionadas.

* **Tem comentário**: mostrar itens que tenham comentários para tradutores.
* **Traduções ausentes:** Mostrar itens em que pelo menos um idioma não tem uma tradução.

![chlimage_1-215](assets/chlimage_1-215.png)

1. Na barra de pesquisa, selecione as opções de filtro.
1. Para filtrar usando as opções, clique em Filtro.
1. Para remover os filtros e ver todos os itens no dicionário, clique em Limpar.

### Editar strings traduzidas {#editing-translated-strings}

Depois de adicionar a sequência de caracteres em inglês a um dicionário, você pode adicionar traduções da sequência de caracteres. Também é possível [exportar o dicionário](/help/sites-developing/i18n-translator.md#exporting-a-dictionary) para ser traduzido por um terceiro.

1. Selecionar [o dicionário específico do seu projeto](#creating-a-dictionary) como especifica o caminho no repositório que contém as traduções. Por exemplo, selecione **Dicionários** como:

   `/apps/myProject/i18n`

   >[!CAUTION]
   >
   >Edite somente os dicionários criados para o seu projeto e localizados em `/apps`.
   >
   >Dicionários do sistema AEM também estão disponíveis nesta ferramenta. Não altere os dicionários do sistema AEM, pois isso pode causar problemas com a interface AEM. Além disso, as alterações podem ser perdidas na atualização. Os dicionários do sistema AEM estão localizados em `/libs`.

1. Para editar os textos traduzidos de uma das cadeias de caracteres, é possível:

   * Clique duas vezes no idioma apropriado para a string necessária para editar esse texto único:

   ![chlimage_1-216](assets/chlimage_1-216.png)

   * Clique duas vezes no ícone **String** ou **Comentário** campos da cadeia de caracteres necessária para abrir a **Editar string** , edite as traduções conforme necessário e clique em **OK** para fechar a caixa de diálogo:

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Clique em **Salvar** na barra de ferramentas para confirmar as alterações.

   >[!NOTE]
   >
   >Clicando em **Redefinir e atualizar** (em vez de **Salvar**) reverte quaisquer alterações nos textos anteriores.

## Uso de tradutores de terceiros {#using-third-party-translators}

Para oferecer suporte ao uso de serviços de tradução de terceiros, a ferramenta de Tradução permite exportar e importar dicionários.

### Exportar um dicionário {#exporting-a-dictionary}

Exportar um dicionário para um arquivo XLIFF para que um serviço de terceiros possa traduzir as cadeias de caracteres do dicionário.

* Exporte um dicionário e inclua o inglês e os termos traduzidos de um idioma.
* Exporte algumas ou todas as cadeias de caracteres em inglês.

Quando você exporta um arquivo XLIFF e inclui um idioma, a estrutura do nó do dicionário no repositório deve incluir esse idioma. Se o idioma não for incluído, ocorrerão erros. Por exemplo, para exportar o arquivo XLIFF em francês, a pasta do dicionário deve incluir o `mix:language` nó filho chamado `fr`. (Consulte [Criando um dicionário](/help/sites-developing/i18n-translator.md#creating-a-dictionary).)

Use o procedimento a seguir para exportar um arquivo XLIFF para um idioma específico.

1. Abrir a ferramenta Tradução `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Use o menu suspenso Dicionários para selecionar o dicionário a ser exportado.
1. Clique em Exportar > Exportar completo *XX* Opções de Xliff, onde *XX* é o código de idioma de duas letras, como DE ou FR.

   O arquivo XLIFF é aberto em uma nova guia ou janela.

1. Use os comandos do navegador da Web para salvar a página como um arquivo em seu sistema de arquivos, como Arquivo > Salvar página como.

Use o procedimento a seguir para exportar todas ou algumas das strings em inglês.

1. Abra a ferramenta Tradução. `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Use o menu suspenso Dicionários para selecionar o dicionário a ser exportado.
1. Se você estiver exportando um subconjunto das cadeias de caracteres, selecione os itens do dicionário que serão exportados. Selecionar nenhum item exporta todos os itens.
1. Clique em Exportar > Exportar seleção como Xliff (somente strings).
1. Na caixa de diálogo exibida, copie o texto e cole-o em um arquivo de texto.

### Importando um dicionário {#importing-a-dictionary}

Importe um arquivo XLIFF em um dicionário para preencher o dicionário. Quando o dicionário inclui uma tradução para uma cadeia de caracteres em inglês e o arquivo XLIFF contém uma tradução diferente para a mesma cadeia de caracteres, a tradução do dicionário é substituída.

1. Abrir a ferramenta Tradução `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Clique em Importar > Traduções XLIFF.
1. Selecione o arquivo a ser importado e clique em OK.

## Gerenciamento de idiomas suportados {#managing-supported-lanuages}

Adicione ou remova idiomas compatíveis com a ferramenta Tradução e que são fornecidos aos usuários das suas páginas da Web.

### Alterando Idiomas Listados na Tabela de Dicionários {#changing-languages-listed-in-the-dictionary-table}

A ferramenta Tradutor inclui os seguintes idiomas na tabela de dicionários:

* de - Alemão
* fr - Francês
* it - Italiano
* es - Espanhol
* ja - Japonês
* pt-br - Português do Brasil
* zh-cn - Chinês simplificado
* zh-tw - Chinês tradicional (suporte limitado)
* ko-kr - Coreano

Use o procedimento a seguir para adicionar ou remover idiomas.

1. Usando o CRXDE Lite, crie um nó:

   `/etc/languages`

1. Neste nó, crie uma propriedade:

   * **Nome**: `languages`
   * **Tipo**: `Multi-String`
   * **Valor**: a lista de idiomas que você deseja exibir. Por exemplo:

      * fr
      * es

   >[!NOTE]
   >
   >Os códigos de idioma devem estar em minúsculas.

1. Clique em **Salvar tudo** no CRXDE Lite e recarregue o tradutor. A grade será atualizada para mostrar os idiomas definidos.

   >[!NOTE]
   >
   >O tradutor só salvará traduções para idiomas que são [presente no dicionário](#creating-a-dictionary) (ou seja, abaixo do caminho do dicionário, como `/apps/myProject/i18n`).
   >
   >Verifique se eles correspondem aos idiomas mostrados na grade.

### Disponibilização de idiomas para autores {#making-languages-available-to-authors}

Depois de definir um dicionário para um idioma novo na instância do AEM, é necessário disponibilizá-lo para seleção pelos autores (por exemplo, para uso no **Preferências**):

1. Para alterar a lista de idiomas disponíveis no **Preferências** do **Segurança** console:

   1. Crie uma sobreposição no código do aplicativo para:

      ```
              /libs/cq/security/widgets/source/widgets/security/Preferences.js
       and update as required.
      ```

1. Para disponibilizar o idioma no **Preferências** do **Sites** console, é necessário fazer as seguintes alterações no aplicativo:

   1. Crie uma sobreposição para a estrutura em:

      `/libs/cq/security/content/tools/userProperties`

   1. Na sobreposição, atualize a lista de idiomas em:

      `items/common/items /lang/options`

1. Salve tudo e recarregue o console apropriado.

### Alterando Nomes de Idiomas e Países Default {#changing-language-names-and-default-countries}

Vários países usam a mesma língua, por exemplo, os EUA, o Reino Unido e a Austrália usam o inglês. Isso é indicado por um código indicando o idioma e o país, como `en_US`, `en_GB` e `en_AU`.

Os países padrão são usados ao exibir sinalizadores (por exemplo, na caixa de diálogo de cópia de idioma), para resolver o país de um código de idioma.

>[!NOTE]
>
>Para localizações conforme gerenciado pelo tradutor acima, somente o idioma exato funciona. Se o menu suspenso de preferência de idioma usar `en_uk`, deve haver uma `en_uk` no repositório.

Para alterar as definições default:

1. Uma lista de idiomas é armazenada em:

   `/libs/wcm/core/resources/languages`

   Sobrepor copiando-o em:

   `/apps/wcm/core/resources/languages`

   Em seguida, altere ou estenda a lista lá. A propriedade `defaultCountry` em um nó de idioma (por exemplo, `ja`) deve conter o código completo, como `ja_jp`, que definiria `jp` como o país padrão do idioma `ja`.

1. Atualize o **Gerenciador de idiomas do WCM do CQ**.

   * **Lista de idiomas**:

     O caminho para a lista de idiomas no repositório. Defina isso no local usado para sobrepor:

     ```
            /apps/wcm/core/resources/languages
     ```

   Você pode fazer isso usando o Console da Web OSGi:

   ```shell
   https://<hostname>:<port-number>/system/console/configMgr/com.day.cq.wcm.core.impl.LanguageManagerImpl
   ```

## Dicionários de publicação {#publishing-dictionaries}

Incorpore seus dicionários no processo de gerenciamento de versões de seus aplicativos AEM. Por exemplo, inclua o dicionário no pacote de conteúdo do aplicativo para implantação na instância de publicação. Essa estratégia oferece os seguintes benefícios:

* Os dicionários estão disponíveis para componentes em seu ambiente de publicação.
* As alterações nas cadeias de caracteres da interface do usuário do componente são implantadas junto com as traduções atualizadas.

Da mesma forma, o teste de strings de dicionário deve ser executado como parte de seu ciclo de vida normal de desenvolvimento de software.

>[!NOTE]
>
>Não use a funcionalidade de publicação regular, ou replicação, para dicionários. Em vez disso, os dicionários devem ser tratados da mesma forma que o código e a configuração. Isso inclui usar o controle do código-fonte para rastrear alterações e usar pacotes de conteúdo para aplicar alterações ao autor e à publicação.

>[!NOTE]
>
>Ao usar o Dispatcher, é necessário [invalidar páginas em cache](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html) para incluir novas strings de dicionário em strings de componente renderizadas.
