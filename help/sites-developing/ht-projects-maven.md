---
title: Como criar projetos do AEM usando o Apache Maven
seo-title: Como criar projetos do AEM usando o Apache Maven
description: Este documento descreve como configurar um projeto do AEM com base no Apache Maven
seo-description: Este documento descreve como configurar um projeto do AEM com base no Apache Maven
uuid: 5db68639-7393-48b7-9d81-5b19b596ff21
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 3ebc1d22-a7a2-4375-9aa5-a18a7ceb446a
docset: aem65
translation-type: tm+mt
source-git-commit: 9d42526ff4c7b7d8a31690ebfb8b45d0e951ebac

---


# Como criar projetos do AEM usando o Apache Maven{#how-to-build-aem-projects-using-apache-maven}

## Visão geral {#overview}

Este documento descreve como configurar um projeto do AEM com base no [Apache Maven](https://maven.apache.org/).

O Apache Maven é uma ferramenta de código aberto para gerenciar projetos de software, automatizando construções e fornecendo informações de qualidade sobre projetos. É a ferramenta de gerenciamento de compilação recomendada para projetos do AEM.

A criação do projeto AEM com base no Maven oferece vários benefícios:

* Um ambiente de desenvolvimento agnóstico IDE
* Uso de arquétipos e artefatos Maven fornecidos pela Adobe
* Uso de conjuntos de ferramentas Apache Sling e Apache Felix para configurações de desenvolvimento baseadas em Maven
* Facilidade de importação para um IDE; por exemplo, Eclipse e/ou IntelliJ
* Integração fácil com sistemas de integração contínua

### Arquétipos de projeto do Maven {#maven-project-archetypes}

A Adobe fornece dois arquétipos Maven que podem servir como linha de base para seus projetos do AEM. Veja mais detalhes nos links abaixo:

* [Arquivo de projeto do AEM](https://github.com/adobe/aem-project-archetype)
* [Arquétipo Maven para o Kit inicial de aplicativos de página única](https://github.com/adobe/aem-spa-project-archetype)

## Dependências da API do Experience Manager {#experience-manager-api-dependencies}

### O que é o UberJar? {#what-is-the-uberjar}

O &quot;UberJar&quot; é o nome informal dado ao arquivo JAR (Java Archives) especial fornecido pela Adobe. Esses arquivos JAR contêm todas as APIs Java públicas expostas pelo Adobe Experience Manager. Também incluem bibliotecas externas limitadas, especificamente todas as APIs públicas disponíveis no AEM que vêm da biblioteca do Apache Sling, Apache Jackrabbit, Apache Lucene, Google Guava e duas bibliotecas usadas para processamento de imagens (Biblioteca do CYMK JPEG ImageIO de Werner Randelshofer e Biblioteca de imagens do TwelveMonkeys). O UberJars contém somente interfaces e classes de API, o que significa que eles contêm somente interfaces e classes que são exportadas por um pacote OSGi no AEM. Eles também contêm um arquivo *MANIFEST.MF* contendo as versões corretas de exportação do pacote para todos esses pacotes exportados, garantindo, assim, que os projetos criados contra o UberJar tenham os intervalos de importação do pacote corretos.

### Por que a Adobe criou o UberJars? {#why-did-adobe-create-the-uberjars}

No passado, os desenvolvedores tinham que gerenciar um número relativamente grande de dependências individuais para diferentes bibliotecas do AEM e quando cada nova API era usada, uma ou mais dependências individuais tinham que ser adicionadas ao projeto. Em um projeto, a introdução do UberJar resultou na remoção de 30 dependências distintas do projeto.

A partir do AEM 6.5, a Adobe fornece dois UberJars: uma que inclui interfaces obsoletas e outra que remove essas interfaces obsoletas. Ao referenciar um explicitamente no momento da criação, os clientes certamente entenderão se eles têm uma dependência do código obsoleto.

O segundo Uber Jar elimina quaisquer classes, métodos e propriedades obsoletos, de modo que os clientes possam compilar e compreender se o código personalizado é uma prova futura.

### Qual UberJar usar? {#which-uberjar-to-use}

O AEM 6.5 tem dois sabores do Uber Jar:

1. Uber Jar - Inclui apenas as interfaces públicas que não estão marcadas para desaprovação. Esse é o **recomendado** UberJar para usar, pois ajuda a que a base de códigos seja atualizada e não confie em APIs obsoletas.
1. Uber Jar com APIs obsoletas: inclui todas as interfaces públicas, incluindo as marcadas para desaprovação em uma versão futura do AEM.

### Como usar o UberJars? {#how-to-i-use-the-uberjars}

Se você estiver usando o Apache Maven como um sistema de compilação (que é o caso da maioria dos projetos Java AEM), precisará adicionar um ou dois elementos ao arquivo *pom.xml* . O primeiro é um elemento de *dependência* que adiciona a dependência real ao seu projeto:

**Dependência Uber Jar *(sem APIs obsoletas)***

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

**Dependência Uber Jar com APIs obsoletas**

>[!CAUTION]
>
>A Adobe recomenda implantar no Uber Jar que ***não* **contém as APIs obsoletas para garantir que seus aplicativos sejam executados corretamente em versões futuras do AEM.
>
>Use o Uber Jar com suporte à API obsoleto somente se o código que depende das APIs obsoletas não puder ser modificado para acomodar as alterações.

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis-with-deprecations</classifier>
    <scope>provided</scope>
</dependency>
```

Se sua empresa já estiver usando um Gerenciador de repositório Maven, como Sonatype Nexus, Apache Archiva ou JFrog Artifatory, adicione a configuração apropriada ao seu projeto para fazer referência a esse gerenciador de repositório e adicione o repositório Maven da Adobe ([https://repo.adobe.com/nexus/content/groups/public/](https://repo.adobe.com/nexus/content/groups/public/)) ao seu gerenciador de repositório.

Se você não estiver usando um gerenciador de repositório, será necessário adicionar um elemento de *repositório* ao arquivo *pom.xml* :

```xml
<repositories>
    <repository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.adobe.com/nexus/content/groups/public/</url>
        <layout>default</layout>
    </repository>
</repositories>
<pluginRepositories>
    <pluginRepository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.adobe.com/nexus/content/groups/public/</url>
        <layout>default</layout>
    </pluginRepository>
</pluginRepositories>
```

### O que posso fazer com o UberJar? {#what-can-i-do-with-the-uberjar}

Com o UberJar, é possível compilar o código do projeto que depende das APIs do AEM (e das APIs usadas pelos projetos mencionados acima). Você também pode gerar informações sobre o Serviço de componentes OSGi Runtime (SCR) e OSGi Metatype. Com algumas limitações, você também pode gravar e executar testes de unidade.

### O que não posso fazer com o UberJar? {#what-can-t-i-do-with-the-uberjar}

Como o UberJar contém **somente** APIs, ele não é executável e não pode ser usado para **executar** o Adobe Experience Manager. Para executar o AEM, você precisa do formulário Início rápido do AEM, independente ou Arquivo de aplicativos da Web (WAR).

### O senhor mencionou limitações nos testes de unidade. Por favor, explique mais. {#you-mentioned-limitations-on-unit-tests-please-explain-further}

Os testes de unidade geralmente interagem com APIs de produtos de três maneiras diferentes, sendo cada uma impactada de forma ligeiramente diferente pelo UberJar.

#### Caso de uso nº 1 - Código personalizado que chama uma interface de API {#use-case-custom-code-which-calls-a-api-interface}

Esse caso, que é o mais comum, envolve algum código personalizado que executa métodos em uma interface Java definida pela API do AEM. A implementação desta interface pode ser fornecida diretamente ou injetada utilizando o padrão de Injeção de Dependência. **Esse caso de uso pode ser tratado com o UberJar.**

Um exemplo da primeira seria:

```java
public class ClassWhichHasAEMInterfacePassedIn {
    /**
     * Get the first length characters of the page title.
     */
    public String getTrimmedTitle(Page page, int length) {
         String title = page.getTitle();
         return StringUtils.left(title, length);
    }
}
```

Um exemplo deste último seria:

```java
@Component
@Service
public class ComponentWhichHasAEMInterfaceInjected implements TitleTrimmer {
    @Reference
    private PageManagerFactory pageManagerFactory;

    /**
     * Get the first length characters of the title of the page containing the provided Resource.
     */
    public String getTrimmedTitle(Resource resource, int length) {
        PageManager pageManager = pageManagerFactory.getPageManager(resource.getResourceResolver());
        Page page = pageManager.getContainingPage(resource);
        if (page == null) {
           return null;
        }
        String title = page.getTitle();
        return StringUtils.left(title, length);
    }
}
```

Para testar em unidade qualquer um desses métodos, um desenvolvedor usaria uma estrutura de zombaria como [JMockit](http://jmockit.github.io), [Mockito](https://mockito.org/), [JMock](https://www.jmock.org/)ou [Easymock](https://easymock.org/) para criar um objeto de zombaria para a API AEM referenciada. Essas amostras usam o JMockit, mas para esse caso de uso específico, a diferença entre essas estruturas é em grande parte sintática.

```java
@RunWith(JMockit.class)
public class ClassWhichHasAEMInterfacePassedInTest {

    @Tested
    private ClassWhichHasAEMInterfacePassedIn instance;

    @Mocked
    private Page page;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(page, 8));
    }
}
```

```java
@RunWith(JMockit.class)
public class ComponentWhichHasAEMInterfaceInjectedTest {

    @Tested
    private ComponentWhichHasAEMInterfaceInjected instance;

    @Mocked
    private Page page;

    @Mocked
    private PageManager pageManager;

    @Injectable
    private PageManagerFactory pageManagerFactory;

    @Mocked
    private Resource resource;

    @Mocked
    private ResourceResolver resourceResolver;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            resource.getResourceResolver();
            result = resourceResolver;
            pageManagerFactory.getPageManager(resourceResolver);
            result = pageManager;
            pageManager.getContainingPage(resource);
            result = page;
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(resource, 8));
    }
}
```

#### Caso de uso nº 2 - Código personalizado que chama uma classe de implementação de API {#use-case-custom-code-which-calls-an-api-implementation-class}

Esse caso de uso envolve chamar um método estático ou de instância de uma classe na API AEM, na qual você está fazendo referência a uma classe concreta, em vez de uma interface, como no Caso de uso nº 1.

```java
public class ClassWhichUsesAStaticMethodFromAPI {

    /**
     * Get a map of asset titles to asset objects.
     *
     * @param resource either an asset resource or a folder containing assets.
     * @return an map of titles to assets. if an asset doesn't have a title, the name is used instead.
     */
    public Map<String, Asset> getAssetTitles(Resource resource) {
        Iterator<Asset> assets = DamUtil.getAssets(resource);
        Map<String, Asset> result = new HashMap<String, Asset>();
        while (assets.hasNext()) {
            Asset asset = assets.next();
            String title = asset.getMetadataValue(DamConstants.DC_TITLE);
            if (title == null) {
                title = asset.getName();
            }
            result.put(title, asset);
        }
        return result;
    }
}
```

```java
public class ClassWhichUsesAnInstanceMethodFromAPI {

    /**
     * Count the number of paragraphs in a parsys.
     *
     * @param resource the parsys resource
     * @return the count
     */
    public int countParagraphs(Resource resource) {
        return new ParagraphSystem(resource).paragraphs().size();
    }
}
```

**Esse caso de uso pode ser tratado com o UberJar**. No entanto, ainda é recomendável zombar da API, onde possível, para testes executados.

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAStaticMethodFromAPITest {

    @Tested
    private ClassWhichUsesAStaticMethodFromAPI instance;

    @Mocked(stubOutClassInitialization = true)
    private DamUtil unusedDamUtil = null;

    @Mocked
    private Resource resource;

    @Test
    public void test_that_empty_iterator_produces_empty_map() {
        new Expectations() {
            {
                DamUtil.getAssets(resource);
                result = Collections.<Asset> emptySet().iterator();
            }
        };
        Map<String, Asset> result = new ClassWhichUsesAStaticMethodFromAPI().getAssetTitles(resource);
        assertNotNull(result);
        assertEquals(0, result.size());
    }
    @Test
    public void test_with_reference_search() {
        assertTrue(true);
    }
}
```

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAnInstanceMethodFromAPITest {

    @Tested
    private ClassWhichUsesAnInstanceMethodFromAPI instance;

    @Mocked
    private Resource parsys;

    @Mocked
    private Paragraph firstPar;

    @Mocked
    private Paragraph secondPar;

    @Test
    public void test_empty_parsys_returns_zero() {
        new MockUp<ParagraphSystem>() {
            @Mock
            public void $init(Resource resource) {
                assertEquals(parsys, resource);
            }
            @Mock
            public List<Paragraph> paragraphs() {
                return Collections.<Paragraph> emptyList();
            }
        };
        assertEquals(0, instance.countParagraphs(parsys));
    }
}
```

#### Caso de uso #3 - Código personalizado que estende uma classe base da API {#use-case-custom-code-which-extends-a-base-class-from-the-api}

Assim como com a geração SCR, se o código estende uma classe base (abstrato ou concreto) da API AEM, você **deve** usar o UberJar para testá-lo.

## Tarefas Comuns de Desenvolvimento com Maven {#common-development-tasks-with-maven}

### Como adicionar caminhos ao módulo de conteúdo {#how-to-add-paths-to-the-content-module}

O módulo de conteúdo contém um arquivo src/main/content/META-INF/vault/filter.xml que define os filtros para o pacote AEM criado pelo Maven. O arquivo criado pelo arquétipo Maven tem a seguinte aparência:

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

Esse arquivo é usado de várias maneiras diferentes:

* para determinar qual conteúdo deve ser incluído no pacote `content-package-maven-plugin`
* pela ferramenta VLT para determinar quais caminhos devem ser considerados
* se o pacote for recriado no Gerenciador de pacotes AEM, isso também definirá quais caminhos incluir

Dependendo dos requisitos do aplicativo, você pode adicionar a esses caminhos para incluir mais conteúdo, como:

* Configurações de implementação
* Blueprints
* Modelos do fluxo de trabalho
* Páginas de design
* Conteúdo de amostra

Para adicionar aos caminhos, adicione mais `<filter>` elementos:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
    <filter root="/etc/msm/rolloutconfigs/myrolloutconfig"/>
    <filter root="/etc/blueprints/mysite/globalsite"/>
    <filter root="/etc/workflow/models/myproject"/>
    <filter root="/etc/designs/myproject"/>
    <filter root="/content/myproject/sample-content"/>
</workspaceFilter>
```

#### Adicionar caminhos ao pacote sem sincronizá-los {#adding-paths-to-the-package-without-syncing-them}

Se você tiver arquivos que devem ser adicionados ao pacote criado pelo plug-in content-package-maven-maven, mas que não devem ser sincronizados entre o sistema de arquivos e o repositório, poderá usar `.vltignore` arquivos. Esses arquivos têm a mesma sintaxe dos arquivos [.gitignore](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html) .

Por exemplo, o arquétipo usa um `.vltignore` arquivo para impedir que o arquivo JAR instalado como parte do conjunto seja sincronizado de volta ao sistema de arquivos:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore}

```xml
*.jar
```

#### Sincronizando caminhos sem adicioná-los ao pacote {#syncing-paths-without-adding-them-to-the-package}

Em alguns casos, é possível manter caminhos específicos sincronizados entre o sistema de arquivos e o repositório, mas não incluí-los no pacote que foi criado para ser instalado no AEM.

Um caso típico é o `/libs/foundation` caminho. Para fins de desenvolvimento, talvez você queira ter o conteúdo desse caminho disponível no seu sistema de arquivos, para que seu IDE possa resolver inclusões JSP que incluam JSPs em `/libs`. No entanto, você não deseja incluir essa parte no pacote que você criou, pois a `/libs` parte contém o código do produto que não deve ser modificado pelas implementações personalizadas.

Para isso, você pode fornecer um arquivo `src/main/content/META-INF/vault/filter-vlt.xml`. Se esse arquivo existir, ele será usado pela ferramenta VLT, por exemplo, quando você executar `vlt up` e `vlt ci`ou quando tiver configurado a `vlt sync` configuração. O content-package-maven-plugin continuará a usar o arquivo `src/main/content/META-INF/vault/filter.xml` ao criar o pacote.

Por exemplo, para disponibilizar `/libs/foundation` localmente para desenvolvimento, mas incluir apenas `/apps/myproject` no pacote, use os dois arquivos a seguir.

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml-1}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

#### src/main/content/META-INF/vault/filter-vlt.xml {#src-main-content-meta-inf-vault-filter-vlt-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/libs/foundation"/>
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

Você também precisará reconfigurar o plug-in maven-resources para não incluir esses arquivos no pacote: o arquivo filter.xml não é aplicado quando o pacote é instalado, mas somente quando o pacote é criado novamente usando o gerenciador de pacotes.

Altere a `<resources>` seção no pom de conteúdo da seguinte forma:

#### src/main/content/pom.xml {#src-main-content-pom-xml}

```xml
<!-- ... -->
<resources>
 <resource>
  <directory>src/main/content/jcr_root</directory>
  <filtering>false</filtering>
  <excludes>
   <exclude>**/.vlt</exclude>
   <exclude>**/.vltignore</exclude>
   <exclude>libs/</exclude>
  </excludes>
 </resource>
</resources>
<!-- ... -->
```

### How to Work with JSPs {#how-to-work-with-jsps}

A configuração do Maven descrita até agora cria um pacote de conteúdo que também pode incluir componentes e seus correspondentes JSPs. No entanto, Maven os trata como qualquer outro arquivo que faz parte do pacote de conteúdo e nem mesmo os reconhece como JSPs.

Os componentes resultantes funcionam no AEM, mas tornar Maven ciente dos JSPs tem dois benefícios principais

* permite que o Maven falhe se os JSPs contiverem erros, de modo que eles sejam revelados no momento da criação e não quando forem compilados pela primeira vez no AEM
* Para IDEs que podem importar projetos Maven, isso também permite a conclusão de código e o suporte à biblioteca de tags nos JSPs

São necessários dois itens para habilitar esta configuração:

1. adicionar dependências da biblioteca de tags
1. compilar os PEC como parte do processo de compilação Maven

#### Adicionar dependências da biblioteca de tags {#adding-tag-library-dependencies}

As dependências abaixo precisam ser adicionadas ao POM dos `content` módulos.

>[!NOTE]
>
>A menos que você esteja importando as dependências do produto conforme descrito em [Importando dependências](#importingaemproductdependencies) do produto AEM acima, elas também precisam ser adicionadas ao POM pai juntamente com a versão correspondente à configuração do AEM, conforme descrito em [Adicionar dependências](#addingdependencies) acima. Os comentários em cada entrada abaixo mostram o pacote a ser pesquisado no Localizador de Dependência.

>[!NOTE]
>
>O `com.adobe.granite.xssprotection` artefato não está incluído no POM cq-quickstart-product-dependencies e requer coordenadas completas de Maven, conforme obtido do Localizador de Dependência.

#### Compilação de JSPs como parte da fase de compilação Maven {#compiling-jsps-as-part-of-the-maven-compile-phase}

Para compilar JSPs na fase de Maven, `compile` usamos o plug-in [Maven JspC do Apache Sling](https://sling.apache.org/documentation/development/jspc.html) , como mostrado abaixo:

* configuramos uma execução para a `jspc` meta (que por padrão se vincula à `compile` fase, de modo que não precisamos especificar a fase explicitamente)

* mandamos compilar quaisquer JSPs em `${project.build.directory}/jsps-to-compile`
* e exibir o resultado para `${project.build.directory}/ignoredjspc` (o que significa `myproject/content/target/ignoredjspc`)

* configuramos maven-resources-plugin para copiar os JSPs para `${project.build.directory}/jsps-to-compile` na fase de geração-fontes e configurá-lo para não copiar a `libs/` pasta (pois esse é o código do produto AEM e não queremos incorrer nas dependências para compilação do nosso projeto, nem precisamos validar a compilação.

Nosso objetivo principal, como mencionado acima, é validar os JSPs e garantir que o processo de compilação falhe se eles contiverem erros. É por isso que os compilamos em um diretório separado que é ignorado (e na verdade imediatamente excluído depois, como você verá em um minuto).

O resultado do Plug-in Maven JspC também pode ser fornecido e implantado como parte de um pacote OSGi, mas isso tem outras implicações e efeitos colaterais e vai além da nossa meta de validação dos JSPs.

Para obter a exclusão das classes compiladas dos JSPs, configuramos o plug-in Maven Clean, como mostrado abaixo. Se você quiser inspecionar o resultado do Plug-in Maven JspC, execute `mvn compile` em `myproject/content` — depois disso, você encontrará o resultado `myproject/content/target/ignoredjspc`).

#### myproject/content/pom.xml {#myproject-content-pom-xml}

```xml
<build>
  <!-- ... -->
  <plugins>
    <!-- ... -->
    <plugin>
      <artifactId>maven-resources-plugin</artifactId>
      <executions>
        <execution>
          <id>copy-resources</id>
          <phase>generate-sources</phase>
          <goals>
            <goal>copy-resources</goal>
          </goals>
          <configuration>
            <outputDirectory>${project.build.directory}/jsps-to-compile</outputDirectory>
            <resources>
              <resource>
                <directory>src/main/content/jcr_root</directory>
                <excludes>
                  <exclude>libs/**</exclude>
                </excludes>
              </resource>
            </resources>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <groupId>org.apache.sling</groupId>
      <artifactId>maven-jspc-plugin</artifactId>
      <version>2.0.6</version>
      <executions>
        <execution>
          <id>compile-jsp</id>
          <goals>
            <goal>jspc</goal>
          </goals>
          <configuration>
            <jasperClassDebugInfo>false</jasperClassDebugInfo>
            <sourceDirectory>${project.build.directory}/jsps-to-compile</sourceDirectory>
            <outputDirectory>${project.build.directory}/ignoredjspc</outputDirectory>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <artifactId>maven-clean-plugin</artifactId>
      <executions>
        <execution>
          <id>remove-compiled-jsps</id>
          <goals>
            <goal>clean</goal>
          </goals>
          <phase>process-classes</phase>
          <configuration>
            <excludeDefaultDirectories>true</excludeDefaultDirectories>
            <filesets>
              <fileset>
                <directory>${project.build.directory}/jsps-to-compile</directory>
                <directory>${project.build.directory}/ignoredjspc</directory>
              </fileset>
            </filesets>
          </configuration>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

>[!NOTE]
>
>Dependendo de você realmente usar o código JSP em `/libs` (isto é, incluir JSPs de lá), será necessário refinar quais JSPs são copiados para compilação.
>
>Por exemplo, se você incluir `/libs/foundation/global.jsp`, poderá usar a seguinte configuração para a configuração `maven-resources-plugin` em vez da configuração acima, que ignora completamente `/libs`.
>
>
```
> <resource>  
>           <directory>src/main/content/jcr_root</directory>  
>           <includes>  
>                   <include>apps/**</include>  
>                   <include>libs/foundation/global.jsp</include>
>       </includes>  
>   </resource>  
>```

### Como trabalhar com sistemas SCM {#how-to-work-with-scm-systems}

Ao trabalhar com o Gerenciamento de configuração de origem (SCM), verifique se

* O VCS ignora artefatos que não são de origem no sistema de arquivos
* O VLT ignora artefatos do VCS e não os faz check-in no repositório

>[!NOTE]
>
>Esta descrição não aborda como configurar o Maven para trabalhar com seu SCM, descrito exaustivamente na referência [Maven POM e na documentação](https://maven.apache.org/pom.html#SCM) do [](https://maven.apache.org/scm/)Maven SCM Plugin.

#### Padrões para excluir do SCM {#patterns-to-exclude-from-scm}

A seguir está uma lista típica de padrões a serem incluídos no SCM. Por exemplo, se você estiver usando git, poderá adicioná-los ao arquivo do seu projeto `.gitignore` .

#### exemplo .gitignore {#sample-gitignore}

```shell
# Ignore VLT files
.vlt
.vlt-sync.log
.vlt-sync-config.properties

# Ignore Quickstart launches in the source tree
license.properties
crx-quickstart

# Ignore compilation results
target

# Ignore IDE and Operating System artifacts
.idea
.classpath
.metadata
.project
.settings
maven-eclipse.xml
*.iml
*.ipr
*.iws
.DS_Store
```

#### Ignorando arquivos de controle SCM no VLT {#ignoring-scm-control-files-in-vlt}

Em alguns casos, você pode ter arquivos de controle SCM na árvore de origem de conteúdo nos quais não deseja fazer check-in no repositório.

Pense na seguinte situação:

O arquetype já criou um arquivo .vltignore para impedir que o arquivo jar do pacote instalado seja sincronizado de volta ao sistema de arquivos:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-1}

```shell
*.jar
```

Obviamente, você também não quer esse arquivo no SCM, portanto, se você estiver usando git, adicione um arquivo correspondente. `gitignore` arquivo:

#### src/main/content/jcr_root/apps/myproject/install/.gitignore {#src-main-content-jcr-root-apps-myproject-install-gitignore}

```shell
*.jar
```

Como o . `gitignore` o arquivo também não deve entrar no repositório, o . `vltignore` é necessário estender o arquivo para incluir o . `gitignore` arquivo:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-2}

```shell
*.jar
.gitignore
```

### Como trabalhar com perfis de implantação {#how-to-work-with-deployment-profiles}

Se o processo de criação fizer parte de uma configuração maior de gerenciamento do ciclo de vida do desenvolvimento, como um processo de integração contínuo, você geralmente precisará implantar em outros computadores, além da instância local do desenvolvedor.

Para esses cenários, você pode adicionar facilmente novos Perfis [de construção de](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) Maven ao POM do projeto.

O exemplo abaixo adiciona um perfil `integrationServer`, que redefine os nomes de host e as portas das instâncias de autor e publicação. Você pode implantar nesses servidores executando o maven da raiz do projeto, como mostrado abaixo.

```shell
# install on integration test author
$ mvn -PautoInstallPackage -PintegrationServer install

# install on integration test publisher
$ mvn -PautoInstallPackagePublish -PintegrationServer install
```

#### myproject/pom.xml {#myproject-pom-xml}

```xml
<profiles>

    <!-- ... -->

    <profile>
        <id>integrationServer</id>
        <properties>
            <crx.host>dev-author.intranet</crx.host>
            <crx.port>5502</crx.port>
            <publish.crx.host>dev-publish.intranet</publish.crx.host>
            <publish.crx.port>5503</publish.crx.port>
        </properties>
    </profile>
</profiles>
```

### Como trabalhar com o AEM Communities {#how-to-work-with-aem-communities}

Quando licenciado para o recurso AEM Communities, é necessário um jar de API adicional.

Para obter detalhes, consulte [Uso do Maven para comunidades](/help/communities/maven.md)
