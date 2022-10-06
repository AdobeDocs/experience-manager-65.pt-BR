---
title: Extraindo strings para tradução
seo-title: Extracting Strings for Translating
description: Use xgettext-maven-plugin para extrair strings do código-fonte que precisam ser traduzidas
seo-description: Use xgettext-maven-plugin to extract strings from your source code that need translating
uuid: 2c586ecb-8494-4f8f-b31a-1ed73644d611
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 034f70f1-fbd2-4f6b-b07a-5758f0461a5b
exl-id: 4acc5f7f-0bcb-4b5a-8531-52e146cffeae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# Extraindo strings para tradução{#extracting-strings-for-translating}

Use xgettext-maven-plugin para extrair strings do código-fonte que precisam ser traduzidas. O plug-in Maven extrai cadeias de caracteres para um arquivo XLIFF que você envia para tradução. As cadeias de caracteres são extraídas dos seguintes locais:

* Arquivos de origem Java
* Arquivos de origem do JavaScript
* Representações XML de recursos SVN (nós JCR)

## Configuração da extração de cadeia de caracteres {#configuring-string-extraction}

Configure como a ferramenta xgettext-maven-plugin extrai strings para o seu projeto.

```xml
/filter { }
/parsers {
   /vaultxml { }
   /javascript { }
   /regexp {
      /files {
         /java { }
         /jsp { }
         /extjstemplate { }
      }
   }
}
/potentials { }
```

| Seção | Descrição |
|---|---|
| /filter | Identifica os arquivos que são analisados. |
| /parsers/vaultxml | Configura a análise de arquivos Vault. Identifica os nós do JCR que contêm strings externalizadas e dicas de localização. Também identifica nós JCR para ignorar. |
| /parsers/javascript | Identifica as funções do Javascript que externalizam cadeias de caracteres. Não é necessário alterar esta seção. |
| /parsers/regexp | Configura a análise de arquivos Java, JSP e Modelo ExtJS. Não é necessário alterar esta seção. |
| /potenciais | A fórmula para detectar cadeias de caracteres a serem internacionalizadas. |

### Identificação dos arquivos a serem analisados {#identifying-the-files-to-parse}

A seção /filter do arquivo i18n.any identifica os arquivos que a ferramenta xgettext-maven-plugin analisa. Adicione várias regras de inclusão e exclusão que identificam arquivos que são analisados e ignorados, respectivamente. Você deve incluir todos os arquivos e, em seguida, excluir os arquivos que não deseja analisar. Normalmente, você exclui tipos de arquivos que não contribuem para a interface do usuário ou arquivos que definem a interface do usuário, mas não estão sendo traduzidos. As regras de inclusão e exclusão têm o seguinte formato:

```
{ /include "pattern" }
{ /exclude "pattern" }
```

A parte do padrão de uma regra é usada para corresponder aos nomes dos arquivos a serem incluídos ou excluídos. O prefixo de padrão indica se você está correspondendo a um nó JCR (sua representação no Vault) ou ao sistema de arquivos.

| Prefixo | Efeito |
|---|---|
| / | Indica um caminho JCR. Portanto, esse prefixo corresponde arquivos abaixo do diretório jcr_root. |
| &amp;ast; | Indica um arquivo regular no sistema de arquivos. |
| nenhum | Nenhum prefixo ou padrão que começa com uma pasta ou nome de arquivo indica um arquivo normal no sistema de arquivos. |

Quando usado em um padrão, o caractere / indica um subdiretório e o &amp;último; corresponde a todos. A tabela a seguir lista vários exemplos de regras.

<table>
 <tbody>
  <tr>
   <th>Exemplo de regra</th>
   <th>Efeito</th>
  </tr>
  <tr>
   <td><code>{ /include "*" }</code></td>
   <td>Inclua todos os arquivos.</td>
  </tr>
  <tr>
   <td><code>{ /exclude "*.pdf" }</code></td>
   <td>Exclua todos os arquivos PDF.</td>
  </tr>
  <tr>
   <td><code> { /exclude "*/pom.xml" }</code></td>
   <td>Exclua arquivos POM.</td>
  </tr>
  <tr>
   <td><code class="code">{ /exclude "/content/*" }
      { /include "/content/catalogs/geometrixx/templatepages" }
      { /include "/content/catalogs/geometrixx/templatepages/*" }</code></td>
   <td><p>Exclua todos os arquivos abaixo do nó /content.</p> <p>Inclua o nó /content/catalogs/geometrixx/templatepages .</p> <p>Inclua todos os nós secundários de /content/catalogs/geometrixx/templatepages.</p> </td>
  </tr>
 </tbody>
</table>

### Extração das cadeias de caracteres  {#extracting-the-strings}

Sem POM:

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

Com POM: Adicione ao POM:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.adobe.granite.maven</groupId>
            <artifactId>xgettext-maven-plugin</artifactId>
            <version>1.1</version>
            <configuration>
                <rules>i18n.any</rules>
                <root>jcr_root</root>
                <xliff>cq.xliff</xliff>
                <verbose>true</verbose>
            </configuration>
        </plugin>
    </plugins>
</build>
```

o comando:

```shell
mvn xgettext:extract
```

### Arquivos de saída {#output-files}

* `raw.xliff`: strings extraídas
* `warn.log`: avisos (se houver), se `CQ.I18n.getMessage()` A API é usada incorretamente. Eles sempre precisam de uma correção e, em seguida, uma nova execução.

* `parserwarn.log`: avisos do analisador (se houver), por exemplo problemas do analisador js
* `potentials.xliff`: candidatos &quot;potenciais&quot; que não são extraídos, mas podem ser strings legíveis para humanos que precisam de tradução (podem ser ignorados, ainda produzem uma enorme quantidade de falsos positivos)
* `strings.xliff`: arquivo xliff nivelado, a ser importado para ALF
* `backrefs.txt`: permite pesquisa rápida de locais do código-fonte para uma determinada string
