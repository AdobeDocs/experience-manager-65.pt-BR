---
title: Processar ativos usando manipuladores e fluxos de trabalho de mídia
description: Saiba mais sobre os manipuladores de mídia e como usar fluxos de trabalho para executar tarefas em seus ativos digitais.
mini-toc-levels: 1
contentOwner: AG
role: User
feature: Workflow,Renditions
exl-id: cfd6c981-1a35-4327-82d7-cf373d842cc3
solution: Experience Manager, Experience Manager Assets
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '2113'
ht-degree: 3%

---

# Processar ativos usando manipuladores e fluxos de trabalho de mídia {#processing-assets-using-media-handlers-and-workflows}

O [!DNL Adobe Experience Manager Assets] vem com um conjunto de fluxos de trabalho e manipuladores de mídia padrão para processar ativos. Um fluxo de trabalho define as tarefas a serem executadas nos ativos e delega as tarefas específicas aos manipuladores de mídia, por exemplo, geração de miniaturas ou extração de metadados.

Um workflow pode ser configurado para ser executado automaticamente quando um ativo de um tipo MIME específico é carregado. As etapas de processamento são definidas em termos de uma série de manipuladores de mídia [!DNL Assets]. [!DNL Experience Manager] fornece alguns [manipuladores internos](#default-media-handlers), e os extras podem ser [personalizados desenvolvidos](#creating-a-new-media-handler) ou definidos ao delegar o processo a uma [ferramenta de linha de comando](#command-line-based-media-handler).

Os manipuladores de mídia são serviços no [!DNL Assets] que executam ações específicas nos ativos. Por exemplo, quando um arquivo de áudio MP3 é carregado para [!DNL Experience Manager], um fluxo de trabalho aciona um manipulador MP3 que extrai os metadados e gera uma miniatura. Os manipuladores de mídia são usados com workflows. Há suporte para os tipos MIME mais comuns em [!DNL Experience Manager]. Tarefas específicas podem ser executadas em ativos estendendo ou criando fluxos de trabalho, estendendo ou criando manipuladores de mídia ou desativando e ativando manipuladores de mídia.

>[!NOTE]
>
>Consulte a página [Formatos de ativos com suporte](assets-formats.md) para obter uma descrição de todos os formatos com suporte no [!DNL Assets] e os recursos com suporte para cada formato.

## Manipuladores de mídia padrão {#default-media-handlers}

Os seguintes manipuladores de mídia estão disponíveis em [!DNL Assets] e tratam dos tipos MIME mais comuns:

<!-- TBD: Java versions should not be set to 1.5. Must be updated.
-->

| Nome do manipulador | Nome do serviço (no console do sistema) | Tipos MIME suportados |
|--------------|--------------------------------------|----------------------|
| [!UICONTROL ManipuladorTexto] | com.day.cq.dam.core.impl.handler.TextHandler | text/plain |
| [!UICONTROL PdfHandler] | com.day.cq.dam.handler.standard.pdf.PdfHandler | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | com.day.cq.dam.core.impl.handler.JpegHandler | image/jpeg |
| [!UICONTROL Mp3Handler] | com.day.cq.dam.handler.standard.mp3.Mp3Handler | audio/mpeg<br><b>Important</b> - Um arquivo MP3 carregado é [processado usando uma biblioteca de terceiros](https://www.zxdr.it/programmi/SistEvolBDD/LibJava/doc/de/vdheide/mp3/MP3File.html). A biblioteca calcula um comprimento aproximado não preciso se o MP3 tiver taxa de bits variável (VBR). |
| [!UICONTROL ZipHandler] | com.day.cq.dam.handler.standard.zip.ZipHandler | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | com.day.cq.dam.handler.standard.pict.PictHandler | image/pict |
| [!UICONTROL StandardImageHandler] | com.day.cq.dam.core.impl.handler.StandardImageHandler | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler | application/msword |
| [!UICONTROL MSPowerPointHandler] | com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | com.day.cq.dam.handler.standard.epub.EPubHandler | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | com.day.cq.dam.core.impl.handler.GenericAssetHandler | fallback caso nenhum outro manipulador seja encontrado para extrair dados de um ativo |

{style="table-layout:auto"}

Todos os manipuladores executam as seguintes tarefas:

* extrair todos os metadados disponíveis do ativo.
* criar uma imagem em miniatura de um ativo.

Para exibir os manipuladores de mídia ativos:

1. Em seu navegador, navegue até `https://localhost:4502/system/console/components`.
1. Clique em `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. Uma lista com todos os manipuladores de mídia ativos é exibida. Por exemplo:

![chlimage_1-437](assets/chlimage_1-437.png)

## Usar manipuladores de mídia em fluxos de trabalho para executar tarefas em ativos {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

Os manipuladores de mídia são serviços usados com fluxos de trabalho do.

[!DNL Experience Manager] tem alguns fluxos de trabalho padrão para processar ativos. Para visualizá-los, abra o console Fluxo de trabalho e clique na guia **[!UICONTROL Modelos]**: os títulos de fluxo de trabalho que começam com [!DNL Assets] são os títulos específicos dos ativos.

Os workflows existentes podem ser estendidos e novos podem ser criados para processar ativos de acordo com requisitos específicos.

O exemplo a seguir mostra como aprimorar o fluxo de trabalho de **[!UICONTROL Sincronização do AEM Assets]** para que os ativos secundários sejam gerados para todos os ativos, exceto documentos PDF.

### Desativar ou ativar um manipulador de mídia {#disabling-enabling-a-media-handler}

Os manipuladores de mídia podem ser desativados ou ativados por meio do console de gerenciamento Web do Apache Felix. Quando o manipulador de mídia está desativado, as tarefas não são executadas nos ativos.

Para ativar/desativar um manipulador de mídia:

1. Em seu navegador, navegue até `https://<host>:<port>/system/console/components`.
1. Clique em **[!UICONTROL Desabilitar]** ao lado do nome do manipulador de mídia. Por exemplo: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. Atualizar a página: um ícone é exibido ao lado do manipulador de mídia indicando que o recurso está desativado.
1. Para habilitar o manipulador de mídia, clique em **[!UICONTROL Habilitar]** ao lado do nome do manipulador de mídia.

### Criar um manipulador de mídia {#creating-a-new-media-handler}

Para suportar um novo tipo de mídia ou executar tarefas específicas em um ativo, é necessário criar um manipulador de mídia. Esta seção descreve como proceder.

#### Classes e interfaces importantes {#important-classes-and-interfaces}

A melhor maneira de iniciar uma implementação é herdar de uma implementação abstrata fornecida que cuida da maioria das coisas e fornece um comportamento padrão razoável: a classe `com.day.cq.dam.core.AbstractAssetHandler`.

Esta classe já fornece um descritor de serviço abstrato. Portanto, se você herdou desta classe e usou o maven-sling-plugin, certifique-se de definir o sinalizador de herança como `true`.

Implemente os seguintes métodos:

* `extractMetadata()`: extrai todos os metadados disponíveis.
* `getThumbnailImage()`: cria uma imagem em miniatura do ativo passado.
* `getMimeTypes()`: retorna os tipos MIME do ativo.

Este é um exemplo de template:

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

A interface e as classes incluem:

* Interface `com.day.cq.dam.api.handler.AssetHandler`: esta interface descreve o serviço que adiciona suporte para tipos MIME específicos. A adição de um tipo MIME requer a implementação dessa interface. A interface contém métodos para importar e exportar os documentos específicos, para criar miniaturas e extrair metadados.
* Classe `com.day.cq.dam.core.AbstractAssetHandler`: esta classe serve como base para todas as outras implementações do manipulador de ativos e fornece a funcionalidade comum usada.
* classe `com.day.cq.dam.core.AbstractSubAssetHandler`:
   * Essa classe serve como base para todas as outras implementações do manipulador de ativos e fornece a funcionalidade usada com frequência, além da funcionalidade usada com frequência para a extração de ativos secundários.
   * A melhor maneira de iniciar uma implementação é herdar de uma implementação abstrata fornecida que cuida da maioria das coisas e fornece o comportamento padrão razoável: a classe com.day.cq.dam.core.AbstractAssetHandler.
   * Esta classe já fornece um descritor de serviço abstrato. Portanto, se você herdou desta classe e usou o maven-sling-plugin, certifique-se de definir o sinalizador de herança como true.

Os seguintes métodos devem ser implementados:

* `extractMetadata()`: este método extrai todos os metadados disponíveis.
* `getThumbnailImage()`: este método cria uma imagem em miniatura do ativo passado.
* `getMimeTypes()`: este método retorna os tipos MIME do ativo.

Este é um exemplo de template:

empacotar my.own.stuff; /&ast;&ast; &ast; @scr.component inherit=&quot;true&quot; &ast; @scr.service &ast;/ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implementar as partes relevantes }

A interface e as classes incluem:

* Interface `com.day.cq.dam.api.handler.AssetHandler`: esta interface descreve o serviço que adiciona suporte para tipos MIME específicos. A adição de um tipo MIME requer a implementação dessa interface. A interface contém métodos para importar e exportar os documentos específicos, para criar miniaturas e extrair metadados.
* Classe `com.day.cq.dam.core.AbstractAssetHandler`: esta classe serve como base para todas as outras implementações do manipulador de ativos e fornece a funcionalidade comum usada.
* Classe `com.day.cq.dam.core.AbstractSubAssetHandler`: esta classe serve como base para todas as outras implementações do manipulador de ativos e fornece a funcionalidade usada com frequência, além da funcionalidade usada com frequência para a extração de subativos.

#### Exemplo: criar um manipulador de texto específico {#example-create-a-specific-text-handler}

Nesta seção, você cria um Manipulador de texto específico que gera miniaturas com uma marca d&#39;água.

Proceda da seguinte forma:

Consulte [Ferramentas de Desenvolvimento](../sites-developing/dev-tools.md) para instalar e configurar o Eclipse com um plug-in [!DNL Maven] e para configurar as dependências necessárias para o projeto [!DNL Maven].

Após executar o procedimento a seguir, ao fazer upload de um arquivo TXT no [!DNL Experience Manager], os metadados do arquivo são extraídos e duas miniaturas com uma marca d&#39;água são geradas.

1. No Eclipse, crie o projeto `myBundle` [!DNL Maven]:

   1. Na barra de menus, clique em **[!UICONTROL Arquivo]** > **[!UICONTROL Novo]** > **[!UICONTROL Outros]**.
   1. Na caixa de diálogo, expanda a pasta [!DNL Maven], selecione o projeto [!DNL Maven] e clique em **[!UICONTROL Avançar]**.
   1. Marque a caixa Criar um projeto simples e a caixa Usar local padrão do Workspace e clique em **[!UICONTROL Avançar]**.
   1. Defina um projeto [!DNL Maven]:

      * Id Do Grupo: `com.day.cq5.myhandler`.
      * ID do artefato: myBundle.
      * Nome: Meu pacote [!DNL Experience Manager].
      * Descrição: Este é meu pacote [!DNL Experience Manager].

   1. Clique em **[!UICONTROL Concluir]**.

1. Defina o compilador [!DNL Java™] para a versão 1.5:

   1. Clique com o botão direito do mouse no projeto `myBundle`, selecione [!UICONTROL Propriedades].
   1. Selecione [!UICONTROL Compilador Java™] e defina as seguintes propriedades como 1.5:

      * Nível de conformidade do compilador
      * Compatibilidade de arquivos .class gerados
      * Compatibilidade com o Source

   1. Clique em **[!UICONTROL OK]**. Na janela de diálogo, clique em **[!UICONTROL Sim]**.

1. Substitua o código no arquivo `pom.xml` pelo seguinte código:

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!-- ====================================================================== -->
    <!-- P A R E N T P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <parent>
     <groupId>com.day.cq.dam</groupId>
     <artifactId>dam</artifactId>
     <version>5.2.14</version>
     <relativePath>../parent</relativePath>
    </parent>
    <!-- ====================================================================== -->
    <!-- P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <groupId>com.day.cq5.myhandler</groupId>
    <artifactId>myBundle</artifactId>
    <name>My CQ5 bundle</name>
    <version>0.0.1-SNAPSHOT</version>
    <description>This is my CQ5 bundle</description>
    <packaging>bundle</packaging>
    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
     <plugins>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-scr-plugin</artifactId>
      </plugin>
      <plugin>
       <groupId>org.apache.sling</groupId>
       <artifactId>maven-sling-plugin</artifactId>
       <configuration>
        <slingUrlSuffix>/libs/dam/install/</slingUrlSuffix>
       </configuration>
      </plugin>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-bundle-plugin</artifactId>
       <extensions>true</extensions>
       <configuration>
        <instructions>
         <Bundle-Category>cq5</Bundle-Category>
         <Export-Package> com.day.cq5.myhandler </Export-Package>
        </instructions>
       </configuration>
      </plugin>
     </plugins>
    </build>
    <!-- ====================================================================== -->
    <!-- D E P E N D E N C I E S -->
    <!-- ====================================================================== -->
    <dependencies>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-api</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-core</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq</groupId>
      <artifactId>cq-commons</artifactId>
     </dependency>
     <dependency>
      <groupId>javax.jcr</groupId>
      <artifactId>jcr</artifactId>
     </dependency>
     <dependency>
      <groupId>org.apache.felix</groupId>
      <artifactId>org.osgi.compendium</artifactId>
     </dependency>
     <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-lang</groupId>
      <artifactId>commons-lang</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-gfx</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-text</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.workflow</groupId>
      <artifactId>cq-workflow-api</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.wcm</groupId>
      <artifactId>cq-wcm-foundation</artifactId>
      <version>5.2.22</version>
     </dependency>
    </dependencies>
   ```

1. Crie o pacote `com.day.cq5.myhandler` que contém as classes [!DNL Java™] em `myBundle/src/main/java`:

   1. Em myBundle, clique com o botão direito do mouse em `src/main/java`, selecione New e, em seguida, Package.
   1. Nomeie-o `com.day.cq5.myhandler` e clique em Concluir.

1. Criar a classe [!DNL Java™] `MyHandler`:

   1. Em [!DNL Eclipse], em `myBundle/src/main/java`, clique com o botão direito no pacote `com.day.cq5.myhandler`. Selecione [!UICONTROL Novo], depois [!UICONTROL Classe].
   1. Na janela de diálogo, nomeie a classe [!DNL Java™] `MyHandler` e clique em [!UICONTROL Concluir]. [!DNL Eclipse] cria e abre o arquivo `MyHandler.java`.
   1. Em `MyHandler.java`, substitua o código existente pelo seguinte e salve as alterações:

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;
   
   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/
   
   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }
   
    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/we-retail/en/products/apparel/gloves/Gloves.jpg");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two whitespaces in a row we do not want to double count.
     // The starting of the document is always a whitespace.
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a whitespace then we need to add one extra word.
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. Compilar a classe [!DNL Java™] e criar o pacote:

   1. Clique com o botão direito do mouse no projeto `myBundle`, selecione **[!UICONTROL Executar como]** e **[!UICONTROL Instalação de Maven]**.
   1. O pacote `myBundle-0.0.1-SNAPSHOT.jar` (contendo a classe compilada) foi criado em `myBundle/target`.

1. No CRX Explorer, crie um nó em `/apps/myApp`. Nome = `install`, Tipo = `nt:folder`.
1. Copie o pacote `myBundle-0.0.1-SNAPSHOT.jar` e armazene-o em `/apps/myApp/install` (por exemplo, com WebDAV). O novo manipulador de texto agora está ativo em [!DNL Experience Manager].
1. No navegador, abra o [!UICONTROL Console de Gerenciamento Web do Apache Felix]. Selecione a guia [!UICONTROL Componentes] e desabilite o manipulador de texto padrão `com.day.cq.dam.core.impl.handler.TextHandler`.

## Manipulador de mídia baseado em linha de comando {#command-line-based-media-handler}

O [!DNL Experience Manager] permite executar qualquer ferramenta de linha de comando em um fluxo de trabalho para converter ativos (como [!DNL ImageMagick]) e adicionar a nova representação ao ativo. Instale somente a ferramenta de linha de comando no disco que hospeda o servidor [!DNL Experience Manager] e para adicionar e configurar uma etapa do processo no fluxo de trabalho. O processo chamado, chamado `CommandLineProcess`, também filtra de acordo com tipos MIME específicos e cria várias miniaturas com base na nova representação.

As seguintes conversões podem ser executadas e armazenadas automaticamente em [!DNL Assets]:

* Transformação de EPS e IA usando [ImageMagick](https://www.imagemagick.org/script/index.php) e [Ghostscript](https://www.ghostscript.com/).
* Transcodificação de vídeo FLV usando [FFmpeg](https://ffmpeg.org/).
* Codificação de MP3 usando [LAME](https://lame.sourceforge.io/).
* Processamento de áudio usando [SOX](https://sourceforge.net/projects/sox/).

>[!NOTE]
>
>Em sistemas não Windows, a ferramenta FFmpeg retorna um erro ao gerar representações para um ativo de vídeo que tem uma aspa simples (&#39;) em seu nome de arquivo. Se o nome do arquivo de vídeo incluir aspas simples, remova-o antes de carregar para [!DNL Experience Manager].

O processo `CommandLineProcess` executa as seguintes operações na ordem listada:

* Filtra o arquivo de acordo com tipos MIME específicos, se especificado.
* Cria um diretório temporário no disco que hospeda o servidor [!DNL Experience Manager].
* Transfere o arquivo original para o diretório temporário.
* Executa o comando definido pelos argumentos da etapa. O comando está sendo executado no diretório temporário com as permissões do usuário que está executando [!DNL Experience Manager].
* Transfere o resultado de volta para a pasta de representação do servidor [!DNL Experience Manager].
* Exclui o diretório temporário.
* Cria miniaturas com base nessas representações, se especificado. O número e as dimensões das miniaturas são definidas pelos argumentos da etapa.

### Um exemplo usando [!DNL ImageMagick] {#an-example-using-imagemagick}

O exemplo a seguir mostra como configurar a etapa do processo da linha de comando para que, sempre que um ativo com o GIF ou TIFF miMIME e-type for adicionado a `/content/dam` no servidor [!DNL Experience Manager], uma imagem invertida do original será criada. Também são criadas mais três miniaturas: 140x100, 48x48 e 10x250.

Para fazer isso, use [!DNL ImageMagick]. [!DNL ImageMagick] é um software de linha de comando gratuito usado para criar, editar e compor imagens bitmap.

Instalar [!DNL ImageMagick] no disco que hospeda o servidor [!DNL Experience Manager]:

1. Instalar [!DNL ImageMagick]: consulte a [documentação do ImageMagick](https://www.imagemagick.org/script/download.php).
1. Configure a ferramenta de forma que uma linha de comando, você possa executar `convert`.
1. Para verificar se a ferramenta está instalada corretamente, execute o seguinte comando `convert -h` na linha de comando.

   Ele exibe uma tela de ajuda com todas as opções possíveis da ferramenta de conversão.

   >[!NOTE]
   >
   >Em algumas versões do Windows, o comando convert pode falhar ao ser executado por estar em conflito com o utilitário de conversão nativo que faz parte da instalação do [!DNL Windows]. Nesse caso, mencione o caminho completo do software [!DNL ImageMagick] usado para converter arquivos de imagem em miniaturas. Por exemplo, `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. Para ver se a ferramenta é executada corretamente, adicione uma imagem de JPG ao diretório de trabalho e execute o comando convert `<image-name>.jpg -flip <image-name>-flipped.jpg` na linha de comando. Uma imagem invertida é adicionada ao diretório. Em seguida, adicione a etapa do processo da linha de comando ao fluxo de trabalho **[!UICONTROL Atualizar ativo do DAM]**.
1. Vá para o console **[!UICONTROL Fluxo de trabalho]**.
1. Na guia **[!UICONTROL Modelos]**, edite o **[!UICONTROL modelo de Ativo de atualização DAM]**.
1. Altere os [!UICONTROL Argumentos] da etapa de **[!UICONTROL representação habilitada para a Web]** para: `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`.
1. Salve o workflow.

Para testar o fluxo de trabalho modificado, adicione um ativo a `/content/dam`.

1. No sistema de arquivos, obtenha uma imagem TIFF de sua escolha. Renomeie-o para `myImage.tiff` e copie-o para `/content/dam`, por exemplo, usando WebDAV.
1. Vá para o console do **[!UICONTROL CQ5 DAM]**, por exemplo, `https://localhost:4502/libs/wcm/core/content/damadmin.html`.
1. Abra o ativo **[!UICONTROL myImage.tiff]** e verifique se a imagem virada e as três miniaturas foram criadas.

#### Configurar a etapa do processo CommandLineProcess {#configuring-the-commandlineprocess-process-step}

Esta seção descreve como definir os [!UICONTROL Argumentos de processo] do [!UICONTROL CommandLineProcess].

Separe os valores dos [!UICONTROL Argumentos do processo] usando vírgula e não os inicie com um espaço em branco.

| Argument-Format | Descrição |
|---|---|
| mime:&lt;tipo- mime> | Argumento opcional. O processo é aplicado se o ativo tiver o mesmo tipo MIME que o do argumento. <br>Vários tipos MIME podem ser definidos. |
| tn:&lt;width>:&lt;height> | Argumento opcional. O processo cria uma miniatura com as dimensões definidas no argumento. <br>Várias miniaturas podem ser definidas. |
| cmd: &lt;comando> | Define o comando que é executado. A sintaxe depende da ferramenta de linha de comando. Somente um comando pode ser definido. <br>As variáveis a seguir podem ser usadas para criar o comando:<br>`${filename}`: nome do arquivo de entrada, por exemplo, original.jpg <br> `${file}`: nome completo do caminho do arquivo de entrada, por exemplo, `/tmp/cqdam0816.tmp/original.jpg` <br> `${directory}`: diretório do arquivo de entrada, por exemplo, `/tmp/cqdam0816.tmp` <br>`${basename}`: nome do arquivo de entrada sem sua extensão, por exemplo, original <br>`${extension}`: extensão do arquivo de entrada, por exemplo, JPG. |

Por exemplo, se [!DNL ImageMagick] estiver instalado no disco que hospeda o servidor [!DNL Experience Manager] e você criar uma etapa do processo usando [!UICONTROL CommandLineProcess] como Implementação e os seguintes valores como [!UICONTROL Argumentos de Processo]:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

Em seguida, quando o fluxo de trabalho é executado, a etapa se aplica somente aos ativos que têm `image/gif` ou `mime:image/tiff` como `mime-types`. Ele cria uma imagem invertida do original, converte-o em JPG e cria três miniaturas com as dimensões 140x100, 48x48 e 10x250.

Use os [!UICONTROL Argumentos de processo] a seguir para criar as três miniaturas padrão usando [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

Use os [!UICONTROL Argumentos do Processo] a seguir para criar a representação habilitada para a Web usando [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>A etapa [!UICONTROL CommandLineProcess] aplica-se somente a ativos (nós do tipo `dam:Asset`) ou descendentes de um ativo.

>[!MORELIKETHIS]
>
>* [Processar ativos](assets-workflow.md)
