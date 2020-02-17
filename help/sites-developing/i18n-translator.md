---
title: Uso do tradutor para gerenciar dicionários
seo-title: Uso do tradutor para gerenciar dicionários
description: O AEM fornece um console para gerenciar as várias traduções de textos usados na interface do usuário do componente
seo-description: O AEM fornece um console para gerenciar as várias traduções de textos usados na interface do usuário do componente
uuid: 4eea3110-e958-473e-8d22-c84fa435edbd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: adf3364c-11f1-45c6-b41d-2c7d48b626f9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Uso do tradutor para gerenciar dicionários{#using-translator-to-manage-dictionaries}

O AEM fornece um console para gerenciar as várias traduções de textos usados na interface do usuário do componente. Este console está disponível em

`https://<hostname>:<port-number>/libs/cq/i18n/translator.html`

Use a ferramenta tradutor para gerenciar strings em inglês e suas traduções. Os dicionários são criados no repositório, por exemplo /apps/myproject/i18n.

Observe que a ferramenta Tradutor e os dicionários que você gerencia são para apresentar a interface do usuário do componente em diferentes idiomas. Se desejar traduzir a página ou o conteúdo gerado pelo usuário, consulte [Traduzir conteúdo para sites](/help/sites-administering/translation.md) multilíngues e [Tradução de conteúdo](/help/communities/translate-ugc.md)gerado pelo usuário.

>[!CAUTION]
>
>Edite apenas os dicionários criados para seu projeto e que residem em `/apps`.
>
>Os dicionários do sistema AEM também estão disponíveis nesta ferramenta. Não altere os dicionários do sistema do AEM, pois isso pode causar problemas na interface do usuário do AEM. Além disso, as alterações podem ser perdidas após a atualização. Os dicionários do sistema AEM estão localizados em `/libs`.

>[!NOTE]
>
>Embora a ferramenta Tradutor tenha uma interface clássica da interface do usuário, ela é usada para a tradução de frases, independentemente da interface em que essas frases são encontradas.

O tradutor lista os textos usados no AEM com as várias traduções de idioma ao lado:

![chlimage_1-205](assets/chlimage_1-205.png)

Você pode pesquisar, filtrar e editar os textos em inglês e traduzidos. Você também pode exportar dicionários para o formato XLIFF para tradução e depois importar as traduções de volta para os dicionários.

Também é possível adicionar os dicionários i18n a um projeto de tradução desse console. Você pode criar um novo ou adicionar a um projeto existente.

1. Clique em **Traduzir dicionário**.

   ![chlimage_1-205](assets/chlimage_1-206.png)

1. Selecione a opção Criar ou Adicionar, dependendo de sua necessidade. Uma caixa de diálogo é aberta.

   ![chlimage_1-207](assets/chlimage_1-207.png)

1. Preencha os campos conforme necessário e clique em OK. ![chlimage_1-208](assets/chlimage_1-208.png)

1. Agora você pode clicar em **OK** ou ver o Dicionário de destino.

   >[!NOTE]
   >
   >Para obter mais informações sobre projetos de tradução, leia [Gerenciar projetos](/help/sites-administering/tc-manage.md)de tradução.

## Criação de um dicionário {#creating-a-dictionary}

Crie um dicionário para gerenciar suas strings de interface de usuário localizadas. Depois de criar um dicionário, você pode usar a ferramenta Tradução para gerenciá-lo.

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
   >Esta é a estrutura do módulo [](https://sling.apache.org/site/internationalization-support.html)Sling i18n.

1. Recarregue o tradutor e o caminho do dicionário (por exemplo, `/apps/myProject/i18n`) estará disponível no seletor suspenso na barra de ferramentas. Selecione esta opção para começar a adicionar strings e suas traduções.

   >[!NOTE]
   >
   >O tradutor só salvará traduções para línguas que estejam efetivamente presentes abaixo do caminho (por exemplo, `/apps/myProject/i18n`).
   >
   >Verifique se eles correspondem aos idiomas mostrados na grade.

## Gerenciamento de strings de dicionário {#managing-dictionary-strings}

Use a ferramenta Tradução para gerenciar as sequências de caracteres em seus dicionários. Você pode adicionar, modificar e remover strings em inglês e também fornecer strings traduzidas.

>[!CAUTION]
>
>Edite apenas os dicionários criados para seu projeto e que residem em `/apps`.
>
>Não altere os dicionários do sistema do AEM, pois isso pode causar problemas na interface do usuário do AEM. Além disso, as alterações podem ser perdidas após a atualização. Os dicionários do sistema AEM estão localizados em `/libs`.

### Adicionar, alterar e remover strings {#adding-changing-and-removing-strings}

Adicione strings em inglês a um dicionário que seu componente internacionalizou. Adicione somente strings que são internacionalizadas para que você não desperdice recursos ao traduzir strings que não são usadas.

As strings adicionadas a um dicionário devem corresponder exatamente à string especificada no código. Se a string em inglês padrão usada no código não corresponder à string em inglês em um dicionário, a string traduzida não aparecerá na interface do usuário quando necessário. As strings fazem distinção entre maiúsculas e minúsculas.

**Fornecer dicas de tradução**

Use a propriedade Comentário da string do dicionário para fornecer informações ao tradutor para esclarecer o significado da string. Normalmente, a interface do usuário auxilia os usuários a determinar o significado de palavras ambíguas. No entanto, o tradutor não vê a string no contexto da interface do usuário. A dica de tradução remove a ambiguidade. Por exemplo, um comentário ajuda o tradutor a entender que a palavra Inglês Solicitação é usada como um substantivo em vez de um verbo.

As dicas de tradução também distinguem strings que são idênticas e têm significados diferentes. Por exemplo, a palavra Pesquisar pode ser um substantivo ou um verbo, exigindo duas entradas &quot;Pesquisar&quot; no dicionário com duas dicas de tradução diferentes. O código que solicita a string também inclui a dica de conversão para que a string correta seja usada na interface do usuário.

**Incluindo variáveis indexadas**

Inclua variáveis na string localizada para criar significado contextual em uma sentença. Por exemplo, depois de fazer logon em um aplicativo da Web, a página inicial exibe a mensagem &quot;Bem-vindo ao administrador. Você tem duas mensagens na sua caixa de entrada.&quot; O contexto da página determina o nome do usuário e o número de mensagens.

Para incluir variáveis na string localizada, posicione os índices entre colchetes no local das variáveis no primeiro argumento do método get. Use a dica de localização para descrever os valores. O tradutor deve entender o significado das variáveis porque diferentes idiomas usam estruturas de frases diferentes.

Observe que [o código que solicita a string](/help/sites-developing/i18n-dev.md#including-variables-in-localized-sentences) traduzida fornece valores para as variáveis indexadas de acordo com o contexto.

Por exemplo, a seguinte string é exibida quando um usuário faz logon em um site e é incluída no dicionário:

`Welcome back {0}. You have {1} messages.`

O comentário a seguir descreve as variáveis:

`{0} = the user name, {1} = the number of items in the user's inbox`

**Modificação de strings**

Altere ou remova strings em inglês à medida que forem alteradas ou removidas no código. Quando você altera uma string, ela é persistente e uma nova string é feita que reflete a alteração. Antes de remover uma string, verifique se nenhum código a utiliza.

Use o procedimento a seguir para adicionar uma string.

1. No menu suspenso Dicionários, selecione o dicionário ao qual você está adicionando uma string. No menu suspenso, os dicionários são representados pelo caminho no repositório.
1. Acima da tabela Strings and Translations (Strings e traduções), clique em Add (Adicionar).

   ![chlimage_1-209](assets/chlimage_1-209.png)

1. Na caixa String da caixa de diálogo Adicionar string, digite a string em inglês. Na caixa Comentário, digite uma dica de tradução para o tradutor, se necessário.
1. Clique em OK.
1. Clique em Salvar.

   ![chlimage_1-210](assets/chlimage_1-210.png)

Use o procedimento a seguir para alterar uma string em um dicionário.

1. No menu suspenso Dicionários, selecione o dicionário que contém a string a ser alterada.
1. Clique duas vezes na string a ser alterada.
1. Na caixa de diálogo Editar string, selecione Modificar string ou comentário (Cria uma cópia).

   ![chlimage_1-211](assets/chlimage_1-211.png)

1. Modifique a string ou o comentário e clique em OK.
1. Clique em Salvar.

   ![chlimage_1-212](assets/chlimage_1-212.png)

Use o procedimento a seguir para remover uma string de um dicionário.

1. No menu suspenso Dicionários, selecione o dicionário do qual você está removendo uma string.
1. Clique em Remover.

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. Clique em Salvar.

   ![chlimage_1-214](assets/chlimage_1-214.png)

### Pesquisando strings {#searching-for-strings}

A barra de pesquisa na parte inferior da ferramenta Tradutor fornece opções de seleção de sequência:

* **** Filtrar por texto: Um padrão que corresponde à sequência, ao comentário ou às traduções em inglês. Somente os itens que correspondem a todo ou a parte do padrão aparecem na tabela.
* **** Alterações: Qualquer, Modificado, Novo, Excluído: Mostrar itens que foram alterados e não foram salvos.

   * Qualquer: Mostrar itens que foram modificados, adicionados ou removidos.
   * Modificado: Mostrar itens que foram alterados.
   * Novo: Mostrar itens adicionados.
   * Excluído: Mostrar itens a serem removidos.
   * Várias seleções: Mostrar itens com todas as propriedades selecionadas.

* **Tem Comentário**: Mostrar itens que têm comentários para tradutores.
* **** Traduções ausentes: Mostrar itens em que pelo menos um idioma não tenha uma tradução.

![chlimage_1-215](assets/chlimage_1-215.png)

1. Na barra de pesquisa, selecione as opções de filtragem.
1. Para filtrar usando as opções, clique em Filtrar.
1. Para remover os filtros e ver todos os itens no dicionário, clique em Limpar.

### Edição de strings traduzidas {#editing-translated-strings}

Depois de adicionar a string em inglês a um dicionário, você pode adicionar traduções da string. Você também pode [exportar o dicionário](/help/sites-developing/i18n-translator.md#exporting-a-dictionary) para que ele seja traduzido por terceiros.

1. Selecione [seu dicionário](#creating-a-dictionary) específico do projeto, pois ele especifica o caminho no repositório que contém as traduções. Por exemplo, selecione **Dicionários** como:

   `/apps/myProject/i18n`

   >[!CAUTION]
   >
   >Edite apenas os dicionários criados para seu projeto e que residem em `/apps`.
   >
   >Os dicionários do sistema AEM também estão disponíveis nesta ferramenta. Não altere os dicionários do sistema do AEM, pois isso pode causar problemas na interface do usuário do AEM. Além disso, as alterações podem ser perdidas após a atualização. Os dicionários do sistema AEM estão localizados em `/libs`.

1. Para editar os textos traduzidos de uma das strings, é possível:

   * Clique duas vezes no idioma apropriado para a string necessária para editar esse texto único:
   ![chlimage_1-216](assets/chlimage_1-216.png)

   * Clique duas vezes nos campos **String** ou **Comment** para obter a string desejada para abrir a caixa de diálogo **Editar string** , editar as traduções conforme necessário e clique em **OK** para fechar a caixa de diálogo:
   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Clique em **Salvar** na barra de ferramentas para confirmar suas alterações.

   >[!NOTE]
   >
   >Clicar em **Redefinir e atualizar** (em vez de **Salvar**) reverte quaisquer alterações nos textos anteriores.

## Uso de tradutores de terceiros {#using-third-party-translators}

Para suportar o uso de serviços de tradução de terceiros, a ferramenta Tradução permite exportar e importar dicionários.

### Exportar um dicionário {#exporting-a-dictionary}

Exporte um dicionário para um arquivo XLIFF para que um serviço de terceiros possa traduzir as strings de dicionário.

* Exporte um dicionário e inclua o inglês e os termos traduzidos para um idioma.
* Exporte algumas ou todas apenas as strings inglesas.

Ao exportar um arquivo XLIFF e incluir um idioma, a estrutura de nó do dicionário no repositório deve incluir esse idioma. Se o idioma não estiver incluído, ocorrerão erros. Por exemplo, para exportar o arquivo XLIFF francês, a pasta do dicionário deve incluir o nó `mix:language` filho chamado `fr`. (Consulte [Criação de um dicionário](/help/sites-developing/i18n-translator.md#creating-a-dictionary).)

Use o procedimento a seguir para exportar um arquivo XLIFF para um idioma específico.

1. Abrir a ferramenta Tradução `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Use o menu suspenso Dicionários para selecionar o dicionário a ser exportado.
1. Clique em Exportar > Exportar opções completas de *XX* Xliff, onde *XX* é o código de idioma de duas letras, como DE ou FR.

   O arquivo XLIFF é aberto em uma nova guia ou janela.

1. Use os comandos do navegador da Web para salvar a página como um arquivo no sistema de arquivos, como Arquivo > Salvar página como.

Use o procedimento a seguir para exportar todas ou algumas das strings em inglês.

1. Abra a ferramenta Tradução. `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Use o menu suspenso Dicionários para selecionar o dicionário a ser exportado.
1. Se você estiver exportando um subconjunto das strings, selecione os itens no dicionário a serem exportados. Selecionar nenhum item exporta todos os itens.
1. Clique em Exportar > Exportar seleção como Xliff (somente sequências de caracteres).
1. Na caixa de diálogo exibida, copie o texto e cole-o em um arquivo de texto.

### Importação de um dicionário {#importing-a-dictionary}

Importe um arquivo XLIFF em um dicionário para preencher o dicionário. Quando o dicionário inclui uma tradução para uma string em inglês e o arquivo XLIFF contém uma tradução diferente para a mesma string, a tradução do dicionário é substituída.

1. Abrir a ferramenta Tradução `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Clique em Importar > Traduções XLIFF.
1. Selecione o arquivo a ser importado e clique em OK.

## Gerenciamento de idiomas suportados {#managing-supported-lanuages}

Adicione ou remova idiomas compatíveis com a ferramenta de tradução e que sejam fornecidos aos usuários de suas páginas da Web.

### Alteração de idiomas listados na tabela de dicionários {#changing-languages-listed-in-the-dictionary-table}

A ferramenta Tradutor inclui os seguintes idiomas na tabela do dicionário:

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

1. Neste nó, crie uma propriedade:

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
   >O tradutor só salvará traduções para idiomas que estejam realmente [presentes no dicionário](#creating-a-dictionary) (isto é, abaixo do caminho do dicionário, como `/apps/myProject/i18n`).
   >
   >Verifique se eles correspondem aos idiomas mostrados na grade.

### Disponibilização de idiomas para autores {#making-languages-available-to-authors}

Depois de definir um dicionário para um idioma novo para sua instância do AEM, é necessário disponibilizá-lo para seleção pelos autores (por exemplo, para uso em **Preferências**):

1. Para alterar a lista de idiomas disponíveis em **Preferências** do console **Segurança** :

   1. Crie uma sobreposição no código do seu aplicativo para:

      ```
              /libs/cq/security/widgets/source/widgets/security/Preferences.js
       and update as required.
      ```

1. Para disponibilizar o idioma em **Preferências** no console **Sites** , é necessário fazer as seguintes alterações no aplicativo:

   1. Crie uma sobreposição para a estrutura em:

      `/libs/cq/security/content/tools/userProperties`

   1. Dentro da sobreposição, atualize a lista de idiomas em:

      `items/common/items /lang/options`

1. Salve tudo e recarregue o console apropriado.

### Alteração de nomes de idiomas e países padrão {#changing-language-names-and-default-countries}

Vários países utilizam a mesma língua, por exemplo, os EUA, o Reino Unido e a Austrália todos usam o inglês. Isso é indicado por um código que indica a língua e o país, como `en_US`, `en_GB` e `en_AU`.

Os países padrão são usados ao exibir sinalizadores (por exemplo, na caixa de diálogo de cópia de idioma), eles são usados para resolver o país para um código de idioma.

>[!NOTE]
>
>Para localizações como gerenciadas pelo tradutor acima, somente o idioma exato funciona. Se o menu suspenso de preferência de idioma usar `en_uk`, deverá haver um `en_uk` dicionário no repositório.

Para alterar as definições padrão:

1. Uma lista de idiomas é armazenada em:

   `/libs/wcm/core/resources/languages`

   Para sobrepor isso, copie-o para:

   `/apps/wcm/core/resources/languages`

   Em seguida, alterando ou estendendo a lista ali. A propriedade `defaultCountry` em um nó de idioma (por exemplo, `ja`) deve conter o código completo, como `ja_jp`, que seria definido `jp` como o país padrão para o idioma `ja`.

1. Atualize o Gerenciador **de Idiomas do** CQ WCM.

   * **Lista** de idiomas:

      O caminho para a lista de idiomas no repositório. Defina para o local usado para sobrepor:

      ```
             /apps/wcm/core/resources/languages
      ```
   Você pode fazer isso usando o Console Web OSGi:

   ```shell
   https://<hostname>:<port-number>/system/console/configMgr/com.day.cq.wcm.core.impl.LanguageManagerImpl
   ```

## Publicar dicionários {#publishing-dictionaries}

Incorpore seus dicionários ao processo de gerenciamento de versões de seus aplicativos AEM. Por exemplo, inclua o dicionário no pacote de conteúdo do aplicativo para implantação na instância de publicação. Essa estratégia oferece os seguintes benefícios:

* Os dicionários estão disponíveis para componentes em seu ambiente de publicação.
* As alterações nas strings de interface do usuário do componente são implantadas junto com as traduções atualizadas.

Da mesma forma, o teste de strings de dicionário deve ser executado como parte do ciclo de vida normal do desenvolvimento de software.

>[!NOTE]
>
>A funcionalidade de publicação regular, ou replicação, não deve ser usada para dicionários. Em vez disso, os dicionários devem ser tratados da mesma forma que o código e a configuração. Isso inclui o uso do controle de origem para rastrear alterações e o uso de pacotes de conteúdo para aplicar alterações ao autor e à publicação.

>[!NOTE]
>
>Ao usar o Dispatcher, é necessário [invalidar as páginas](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html) em cache para incluir novas strings de dicionário nas strings de componentes renderizados.

