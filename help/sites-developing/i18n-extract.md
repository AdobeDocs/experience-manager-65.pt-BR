---
title: Extração de strings para tradução
seo-title: Extração de strings para tradução
description: Use xgettext-maven-plugin para extrair strings do código-fonte que precisam ser traduzidas
seo-description: Use xgettext-maven-plugin para extrair strings do código-fonte que precisam ser traduzidas
uuid: 2c586ecb-8494-4f8f-b31a-1ed73644d611
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 034f70f1-fbd2-4f6b-b07a-5758f0461a5b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---


# Extraindo strings para tradução{#extracting-strings-for-translating}

Use xgettext-maven-plugin para extrair strings do código-fonte que precisam ser traduzidas. O plug-in Maven extrai strings para um arquivo XLIFF que você envia para tradução. As strings são extraídas dos seguintes locais:

* Arquivos de origem Java
* Arquivos de origem JavaScript
* Representações XML de recursos SVN (nós JCR)

## Configurando a Extração de string {#configuring-string-extraction}

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
| /parsers/vaultxml | Configura a análise de arquivos Vault. Identifica os nós JCR que contêm sequências de caracteres externalizadas e dicas de localização. Também identifica nós JCR a serem ignorados. |
| /parsers/javascript | Identifica as funções do Javascript que externalizam strings. Não é necessário alterar esta seção. |
| /parsers/regexp | Configura a análise de arquivos Java, JSP e ExtJS Template. Não é necessário alterar esta seção. |
| /potenciais | A fórmula para detectar strings para internacionalizar. |

### Como identificar os arquivos a serem analisados {#identifying-the-files-to-parse}

A seção /filter do arquivo i18n.any identifica os arquivos que a ferramenta xgettext-maven-plugin analisa. Adicione várias regras de inclusão e exclusão que identificam arquivos que são analisados e ignorados, respectivamente. Você deve incluir todos os arquivos e excluir os arquivos que não deseja analisar. Normalmente, você exclui tipos de arquivos que não contribuem com a interface do usuário ou que definem a interface do usuário, mas que não estão sendo traduzidos. As regras de inclusão e exclusão têm o seguinte formato:

```
{ /include "pattern" }
{ /exclude "pattern" }
```

A parte do padrão de uma regra é usada para corresponder aos nomes dos arquivos a serem incluídos ou excluídos. O prefixo de padrão indica se você está correspondendo a um nó JCR (sua representação no Vault) ou ao sistema de arquivos.

| Prefixo | Efeito |
|---|---|
| / | Indica um caminho JCR. Portanto, esse prefixo corresponde arquivos abaixo do diretório jcr_root. |
| &amp;ast; | Indica um arquivo regular no sistema de arquivos. |
| nenhum | Nenhum prefixo, ou padrão que começa com um nome de pasta ou arquivo, indica um arquivo regular no sistema de arquivos. |

Quando usado em um padrão, o caractere / indica um subdiretório e o &amp;ast; corresponde a todos. A tabela a seguir lista várias regras de exemplo.

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
   <td>Excluir arquivos POM.</td>
  </tr>
  <tr>
   <td><code class="code">{ /exclude "/content/*" }
      { /include "/content/catalogs/geometrixx/templatepages" }
      { /include "/content/catalogs/geometrixx/templatepages/*" }</code></td>
   <td><p>Exclua todos os arquivos abaixo do nó /content.</p> <p>Inclua o nó /content/catalogs/geometrixx/templatepages.</p> <p>Inclua todos os nós filhos de /content/catalogs/geometrixx/templatepages.</p> </td>
  </tr>
 </tbody>
</table>

### Extração das strings {#extracting-the-strings}

sem POM:

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

Com POM: Adicione isso ao POM:

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
* `warn.log`: avisos (se houver), se a  `CQ.I18n.getMessage()` API for usada incorretamente. Eles sempre precisam de uma correção e depois de uma nova execução.

* `parserwarn.log`: avisos do analisador (se houver), por exemplo, problemas com o analisador js
* `potentials.xliff`: Candidatos &quot;potenciais&quot; que não são extraídos, mas podem ser strings legíveis para humanos que precisam de tradução (podem ser ignorados, ainda produzem uma enorme quantidade de falsos positivos)
* `strings.xliff`: arquivo xliff nivelado, a ser importado para ALF
* `backrefs.txt`: permite uma pesquisa rápida de locais de código-fonte para uma determinada string

