---
title: Usar o tradutor para gerenciar dicionários
seo-title: Using Translator to Manage Dictionaries
description: AEM fornece um console para gerenciar as várias traduções dos textos usados na interface do usuário do componente
seo-description: AEM provides a console for managing the various translations of texts used in component UI
uuid: 4eea3110-e958-473e-8d22-c84fa435edbd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: adf3364c-11f1-45c6-b41d-2c7d48b626f9
exl-id: a8d50c09-72d0-406e-874e-50a985227a56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2325'
ht-degree: 0%

---

# Usar o tradutor para gerenciar dicionários{#using-translator-to-manage-dictionaries}

O AEM fornece um console para gerenciar as várias traduções dos textos usados na interface do usuário do componente. Esse console está disponível em

`https://<hostname>:<port-number>/libs/cq/i18n/translator.html`

Use a ferramenta do tradutor para gerenciar cadeias de caracteres em inglês e suas traduções. Os dicionários são criados no repositório, por exemplo /apps/myproject/i18n.

Observe que a ferramenta Tradutor e os dicionários gerenciados são para apresentar a interface do usuário do componente em diferentes idiomas. Se quiser traduzir página ou conteúdo gerado pelo usuário, consulte [Tradução de conteúdo para sites multilíngues](/help/sites-administering/translation.md) e [Tradução do conteúdo gerado pelo usuário](/help/communities/translate-ugc.md).

>[!CAUTION]
>
>Somente edite os dicionários criados para o seu projeto e que estão em `/apps`.
>
>AEM dicionários do sistema também estão disponíveis nesta ferramenta. Não altere os dicionários do sistema de AEM, pois isso pode causar problemas na interface do usuário AEM. Além disso, as alterações podem ser perdidas na atualização. Os dicionários do sistema AEM estão localizados em `/libs`.

>[!NOTE]
>
>Embora a ferramenta Tradutor tenha uma interface clássica, ela é usada para tradução de frases, independentemente da interface em que essas frases são encontradas.

O tradutor apresenta uma lista dos textos utilizados em AEM com as várias traduções linguísticas ao lado de cada um:

![chlimage_1-205](assets/chlimage_1-205.png)

Você pode pesquisar, filtrar e editar o inglês e os textos traduzidos. Você também pode exportar dicionários para o formato XLIFF para tradução e depois importar as traduções de volta para os dicionários.

Também é possível adicionar os dicionários i18n a um projeto de tradução desse console. Você pode criar um novo ou adicionar a um projeto existente.

1. Clique em **Traduzir dicionário**.

   ![chlimage_1-206](assets/chlimage_1-206.png)

1. Selecione a opção Criar ou Adicionar , dependendo de sua necessidade. Uma caixa de diálogo é aberta.

   ![chlimage_1-207](assets/chlimage_1-207.png)

1. Preencha os campos conforme necessário e clique em OK. ![chlimage_1-208](assets/chlimage_1-208.png)

1. Agora você pode clicar em **OK** ou consulte o Dicionário de metas.

   >[!NOTE]
   >
   >Para obter mais informações sobre projetos de tradução, leia [Gerenciamento de projetos de tradução](/help/sites-administering/tc-manage.md).

## Criação de um dicionário {#creating-a-dictionary}

Crie um dicionário para gerenciar suas cadeias de caracteres de interface do usuário localizadas. Depois de criar um dicionário, você pode usar a ferramenta Tradução para gerenciá-lo.

1. Usando o CRXDE Lite, adicione o nó raiz ( `sling:Folder`) para seu novo dicionário como a estrutura para manter as definições de idioma:

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
   >Esta é a estrutura da variável [Módulo Sling i18n](https://sling.apache.org/site/internationalization-support.html).

1. Recarregue o tradutor e o caminho do dicionário (por exemplo, `/apps/myProject/i18n`) estará disponível no seletor suspenso na barra de ferramentas. Selecione essa opção para começar a adicionar cadeias de caracteres e suas traduções.

   >[!NOTE]
   >
   >O tradutor salvará somente traduções para idiomas que estão realmente presentes sob o caminho (por exemplo, `/apps/myProject/i18n`).
   >
   >Certifique-se de que eles correspondam aos idiomas mostrados na grade.

## Gerenciamento de sequências de dicionário {#managing-dictionary-strings}

Use a ferramenta Tradução para gerenciar as cadeias de caracteres em seus dicionários. Você pode adicionar, modificar e remover strings em inglês e também fornecer strings traduzidas.

>[!CAUTION]
>
>Somente edite os dicionários criados para o seu projeto e que estão em `/apps`.
>
>Não altere os dicionários do sistema de AEM, pois isso pode causar problemas na interface do usuário AEM. Além disso, as alterações podem ser perdidas na atualização. Os dicionários do sistema AEM estão localizados em `/libs`.

### Adicionar, alterar e remover cadeias de caracteres {#adding-changing-and-removing-strings}

Adicione strings em inglês a um dicionário que seu componente internacionalizou. Adicione somente strings que são internacionalizadas para que você não desperdice recursos traduzindo strings que não são usadas.

As cadeias de caracteres adicionadas a um dicionário devem corresponder exatamente à cadeia de caracteres especificada no código. Se a string padrão em inglês usada no código não corresponder à string em inglês em um dicionário, a string traduzida não aparecerá na interface do usuário quando necessário. As cadeias de caracteres fazem distinção entre maiúsculas e minúsculas.

**Fornecer dicas de tradução**

Use a propriedade Commenet da cadeia de caracteres do dicionário para fornecer informações ao tradutor e esclarecer o significado da cadeia de caracteres. Normalmente, a interface do usuário ajuda os usuários a determinar o significado de palavras ambíguas. No entanto, o tradutor não vê a string no contexto da interface do usuário. A dica de tradução remove a ambiguidade. Por exemplo, um comentário ajuda o tradutor a entender que a palavra em inglês Solicitação é usada como um substantivo em vez de um verbo.

Dicas de tradução também distinguem strings idênticas e com significados diferentes. Por exemplo, a palavra Pesquisar pode ser um substantivo ou um verbo, exigindo duas entradas &quot;Pesquisar&quot; no dicionário com duas dicas de tradução diferentes. O código que solicita a string também inclui a dica de tradução para que a string correta seja usada na interface do usuário.

**Incluindo variáveis indexadas**

Inclua variáveis na string localizada para criar significado contextual em uma frase. Por exemplo, depois de fazer logon em um aplicativo da Web, a página inicial exibe a mensagem &quot;Bem-vindo ao Administrador. Você tem 2 mensagens na sua caixa de entrada.&quot; O contexto da página determina o nome do usuário e o número de mensagens.

Para incluir variáveis na string localizada, coloque índices entre colchetes no local das variáveis no primeiro argumento do método get. Use a dica de localização para descrever os valores. O tradutor deve entender o significado das variáveis, pois idiomas diferentes usam estruturas de frases diferentes.

Observe que [o código que solicita a cadeia de caracteres traduzida](/help/sites-developing/i18n-dev.md#including-variables-in-localized-sentences) fornece valores para as variáveis indexadas de acordo com o contexto.

Por exemplo, a seguinte sequência de caracteres é exibida quando um usuário faz logon em um site e é incluída no dicionário:

`Welcome back {0}. You have {1} messages.`

O comentário a seguir descreve as variáveis:

`{0} = the user name, {1} = the number of items in the user's inbox`

**Modificação de cadeias de caracteres**

Altere ou remova as strings em inglês à medida que forem alteradas ou removidas no código. Quando você altera uma string, a string original é mantida e é feita uma nova string que reflete a alteração. Antes de remover uma string, verifique se nenhum código a usa.

Use o procedimento a seguir para adicionar uma string.

1. No menu suspenso Dicionários , selecione o dicionário ao qual você está adicionando uma string. No menu suspenso , os dicionários são representados pelo caminho no repositório.
1. Acima da tabela Strings and Translations, clique em Add.

   ![chlimage_1-209](assets/chlimage_1-209.png)

1. Na caixa String da caixa de diálogo Add String , digite a string em inglês. Na caixa Comentário, digite uma dica de tradução para o tradutor, se necessário.
1. Clique em OK.
1. Clique em Salvar.

   ![chlimage_1-210](assets/chlimage_1-210.png)

Use o procedimento a seguir para alterar uma string em um dicionário.

1. No menu suspenso Dicionários , selecione o dicionário que contém a string a ser alterada.
1. Clique duas vezes na string a ser alterada.
1. Na caixa de diálogo Editar cadeia de caracteres, selecione Modificar cadeia de caracteres ou Comentário (Cria uma cópia).

   ![chlimage_1-211](assets/chlimage_1-211.png)

1. Modifique a string ou o comentário e clique em OK.
1. Clique em Salvar.

   ![chlimage_1-212](assets/chlimage_1-212.png)

Use o procedimento a seguir para remover uma string de um dicionário.

1. No menu suspenso Dicionários , selecione o dicionário do qual você está removendo uma cadeia de caracteres.
1. Clique em Remover.

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. Clique em Salvar.

   ![chlimage_1-214](assets/chlimage_1-214.png)

### Pesquisar por cadeias de caracteres {#searching-for-strings}

A barra de pesquisa na parte inferior da ferramenta Tradutor fornece opções de seleção de sequência de caracteres:

* **Filtrar por texto:** Um padrão para corresponder com a sequência, o comentário ou as traduções em inglês. Somente os itens que correspondem a todo ou a parte do padrão aparecem na tabela.
* **Alterações: Qualquer, Modificado, Novo, Excluído:** Mostrar itens que foram alterados e que não foram salvos.

   * Qualquer: Mostrar itens que foram modificados, adicionados ou removidos.
   * Modificado: Mostrar itens que foram alterados.
   * Novo: Mostrar itens adicionados.
   * Excluído: Mostrar itens a serem removidos.
   * Várias seleções: Mostrar itens com todas as propriedades selecionadas.

* **Tem comentário**: Mostrar itens que têm comentários para tradutores.
* **Traduções ausentes:** Mostrar itens em que pelo menos um idioma não tenha uma tradução.

![chlimage_1-215](assets/chlimage_1-215.png)

1. Na barra de pesquisa, selecione as opções de filtragem.
1. Para filtrar usando as opções, clique em Filtro.
1. Para remover os filtros e ver todos os itens no dicionário, clique em Limpar.

### Edição de cadeias de caracteres traduzidas {#editing-translated-strings}

Após adicionar a string em inglês a um dicionário, é possível adicionar traduções dessa string. Você também pode [exportar o dicionário](/help/sites-developing/i18n-translator.md#exporting-a-dictionary) para que seja traduzido por um terceiro.

1. Selecionar [seu dicionário específico do projeto](#creating-a-dictionary) como especifica o caminho no repositório que contém as traduções. Por exemplo, selecione **Dicionários** como:

   `/apps/myProject/i18n`

   >[!CAUTION]
   >
   >Somente edite os dicionários criados para o seu projeto e que estão em `/apps`.
   >
   >AEM dicionários do sistema também estão disponíveis nesta ferramenta. Não altere os dicionários do sistema de AEM, pois isso pode causar problemas na interface do usuário AEM. Além disso, as alterações podem ser perdidas na atualização. Os dicionários do sistema AEM estão localizados em `/libs`.

1. Para editar os textos traduzidos para uma das strings, você pode:

   * Clique duas vezes no idioma apropriado para a sequência de caracteres necessária para editar esse texto único:

   ![chlimage_1-216](assets/chlimage_1-216.png)

   * Clique duas vezes na guia **String** ou **Comentário** campos para a cadeia de caracteres necessária para abrir o **Editar string** , edite as traduções conforme necessário e clique em **OK** para fechar a caixa de diálogo:

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Clique em **Salvar** na barra de ferramentas para confirmar as alterações.

   >[!NOTE]
   >
   >Clicando em **Redefinir e atualizar** (em vez de **Salvar**) reverte qualquer alteração nos textos anteriores.

## Uso de tradutores de terceiros {#using-third-party-translators}

Para suportar o uso de serviços de tradução de terceiros, a ferramenta Tradução permite exportar e importar dicionários.

### Exportar um dicionário {#exporting-a-dictionary}

Exporte um dicionário para um arquivo XLIFF para que um serviço de terceiros possa traduzir as cadeias de caracteres do dicionário.

* Exporte um dicionário e inclua o inglês e os termos traduzidos para um idioma.
* Exporte algumas ou todas apenas as strings em inglês.

Ao exportar um arquivo XLIFF e incluir um idioma, a estrutura de nó do dicionário no repositório deve incluir esse idioma. Se o idioma não for incluído, ocorrerão erros. Por exemplo, para exportar o arquivo XLIFF francês, a pasta do dicionário deve incluir o `mix:language` nó filho nomeado `fr`. (Consulte [Criação de um dicionário](/help/sites-developing/i18n-translator.md#creating-a-dictionary).)

Use o procedimento a seguir para exportar um arquivo XLIFF para um idioma específico.

1. Abra a ferramenta Tradução `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Use o menu suspenso Dicionários para selecionar o dicionário a ser exportado.
1. Clique em Exportar > Exportar completo *XX* Opções Xliff, onde *XX* é o código da linguagem de duas letras, como DE ou FR.

   O arquivo XLIFF é aberto em uma nova guia ou janela.

1. Use os comandos do navegador da Web para salvar a página como um arquivo em seu sistema de arquivos, como Arquivo > Salvar página como.

Use o procedimento a seguir para exportar todas ou algumas das strings somente em inglês.

1. Abra a ferramenta Tradução . `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Use o menu suspenso Dicionários para selecionar o dicionário a ser exportado.
1. Se o estiver exportando um subconjunto das cadeias de caracteres, selecione os itens no dicionário que serão exportados. Selecionar nenhum item exporta todos os itens.
1. Clique em Exportar > Exportar seleção como Xliff (somente strings).
1. Na caixa de diálogo exibida, copie o texto e o cole em um arquivo de texto.

### Importação de um dicionário {#importing-a-dictionary}

Importe um arquivo XLIFF em um dicionário para preencher o dicionário. Quando o dicionário inclui uma tradução para uma string em inglês e o arquivo XLIFF contém uma tradução diferente para a mesma string, a tradução do dicionário é substituída.

1. Abra a ferramenta Tradução `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Clique em Importar > Traduções XLIFF.
1. Selecione o arquivo a ser importado e clique em OK.

## Gerenciamento de idiomas suportados {#managing-supported-lanuages}

Adicione ou remova idiomas compatíveis com a ferramenta Tradução e fornecidos aos usuários de suas páginas da Web.

### Alteração de idiomas listados na tabela de dicionários {#changing-languages-listed-in-the-dictionary-table}

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

1. Usar o CRXDE Lite para criar um novo nó:

   `/etc/languages`

1. Nesse nó, crie uma propriedade:

   * **Nome**: `languages`
   * **Tipo**: `Multi-String`
   * **Valor**: a lista de idiomas que deseja exibir. Por exemplo:

      * fr
      * es

   >[!NOTE]
   >
   >Os códigos de idioma devem estar em minúsculas.

1. Clique em **Salvar tudo** no CRXDE Lite e recarregue o tradutor. A grade será atualizada para mostrar os idiomas definidos.

   >[!NOTE]
   >
   >O tradutor só salvará traduções para idiomas que sejam realmente [presente no dicionário](#creating-a-dictionary) (ou seja, sob o caminho do dicionário, como `/apps/myProject/i18n`).
   >
   >Certifique-se de que eles correspondam aos idiomas mostrados na grade.

### Disponibilizar idiomas para autores {#making-languages-available-to-authors}

Depois de definir um dicionário para um idioma novo em sua instância do AEM, é necessário disponibilizá-lo para seleção pelos autores (por exemplo, para uso em **Preferências**):

1. Para alterar a lista de idiomas disponíveis em **Preferências** do **Segurança** console:

   1. Crie uma sobreposição no código do aplicativo para:

      ```
              /libs/cq/security/widgets/source/widgets/security/Preferences.js
       and update as required.
      ```

1. Para disponibilizar o idioma em **Preferências** do **Sites** no console, é necessário fazer as seguintes alterações no aplicativo:

   1. Crie uma sobreposição para a estrutura em:

      `/libs/cq/security/content/tools/userProperties`

   1. Dentro da sobreposição, atualize a lista de idiomas em:

      `items/common/items /lang/options`

1. Salve tudo e recarregue o console apropriado.

### Alteração de nomes de idioma e países padrão {#changing-language-names-and-default-countries}

Vários países utilizam o mesmo idioma, por exemplo, os EUA, o Reino Unido e a Austrália usam o inglês. Isto é indicado por um código que indica a língua e o país, como `en_US`, `en_GB` e `en_AU`.

Os países padrão são usados ao exibir sinalizadores (por exemplo, na caixa de diálogo de cópia de idioma), eles são usados para resolver o país para um código de idioma.

>[!NOTE]
>
>Para localizações como gerenciadas pelo tradutor acima, somente o idioma exato funciona. Se o menu suspenso de preferência de idioma usar `en_uk`, deve haver um `en_uk` no repositório.

Para alterar as definições padrão:

1. Uma lista de idiomas é armazenada em:

   `/libs/wcm/core/resources/languages`

   Sobreponha isso copiando para:

   `/apps/wcm/core/resources/languages`

   Em seguida, alterando ou estendendo a lista ali. A propriedade `defaultCountry` em um nó de idioma (por exemplo, `ja`) deve conter o código completo, como `ja_jp`, que define `jp` como o país padrão para o idioma `ja`.

1. Atualize o **Gerenciador de Idioma do CQ WCM**.

   * **Lista de idiomas**:

      O caminho para a lista de idiomas no repositório. Defina para o local usado para sobrepor:

      ```
             /apps/wcm/core/resources/languages
      ```
   Você pode fazer isso usando o console da Web OSGi:

   ```shell
   https://<hostname>:<port-number>/system/console/configMgr/com.day.cq.wcm.core.impl.LanguageManagerImpl
   ```

## Publicação de dicionários {#publishing-dictionaries}

Incorpore seus dicionários ao processo de gerenciamento de versões dos aplicativos de AEM. Por exemplo, inclua o dicionário no pacote de conteúdo do aplicativo para implantação na instância de publicação. Essa estratégia oferece os seguintes benefícios:

* Os dicionários estão disponíveis para componentes em seu ambiente de publicação.
* As alterações nas cadeias de caracteres da interface do usuário do componente são implantadas junto com as traduções atualizadas.

Da mesma forma, o teste das strings de dicionário deve ser executado como parte do ciclo de vida normal do desenvolvimento de software.

>[!NOTE]
>
>A funcionalidade de publicação regular ou replicação não deve ser usada para dicionários. Em vez disso, os dicionários devem ser tratados da mesma forma que o código e a configuração. Isso inclui o uso do controle de origem para rastrear as alterações e o uso de pacotes de conteúdo para aplicar as alterações ao autor e à publicação.

>[!NOTE]
>
>Ao usar o Dispatcher, é necessário [invalidar páginas em cache](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html) para incluir novas strings dicacionistas em strings de componentes renderizados.
