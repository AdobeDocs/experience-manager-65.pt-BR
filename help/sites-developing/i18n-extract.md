---
title: Extraindo strings para tradução
description: Usar xgettext-maven-plugin para extrair strings do código-fonte que precisam ser traduzidas
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
exl-id: 4acc5f7f-0bcb-4b5a-8531-52e146cffeae
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---

# Extraindo strings para tradução{#extracting-strings-for-translating}

Use xgettext-maven-plugin para extrair strings do código-fonte que precisam ser traduzidas. O plug-in Maven extrai strings para um arquivo XLIFF que você envia para tradução. As cadeias de caracteres são extraídas dos seguintes locais:

* Arquivos de código-fonte Java
* Arquivos de origem do JavaScript
* Representações XML de recursos SVN (nós JCR)

## Configuração da extração de sequência de caracteres {#configuring-string-extraction}

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
| /filter | Identifica os arquivos analisados. |
| /parsers/vaultxml | Configura a análise dos arquivos do Vault. Identifica os nós JCR que contêm strings externalizadas e dicas de localização. Também identifica nós JCR a ignorar. |
| /parsers/javascript | Identifica as funções do JavaScript que externalizam cadeias de caracteres. Não é necessário alterar esta seção. |
| /parsers/regexp | Configura a análise de arquivos de modelo Java, JSP e ExtJS. Não é necessário alterar esta seção. |
| /potenciais | A fórmula para detectar strings a serem internacionalizadas. |

### Identificação dos arquivos a serem analisados {#identifying-the-files-to-parse}

A seção /filter do arquivo i18n.any identifica os arquivos que a ferramenta xgettext-maven-plugin analisa. Adicione várias regras de inclusão e exclusão que identificam os arquivos que são analisados e ignorados, respectivamente. Você deve incluir todos os arquivos e, em seguida, excluir os arquivos que não deseja analisar. Normalmente, você exclui tipos de arquivos que não contribuem para a interface do usuário ou arquivos que definem a interface do usuário, mas não estão sendo traduzidos. As regras de inclusão e exclusão têm o seguinte formato:

```
{ /include "pattern" }
{ /exclude "pattern" }
```

A parte padrão de uma regra é usada para corresponder aos nomes dos arquivos a serem incluídos ou excluídos. O prefixo do padrão indica se você está correspondendo a um nó JCR (sua representação no Vault) ou ao sistema de arquivos.

| Prefixo | Efeito |
|---|---|
| / | Indica um caminho JCR. Portanto, este prefixo corresponde a arquivos abaixo do diretório jcr_root. |
| &ast; | Indica um arquivo regular no sistema de arquivos. |
| nenhum | Nenhum prefixo ou padrão que comece com uma pasta ou nome de arquivo indica um arquivo regular no sistema de arquivos. |

Quando usado dentro de um padrão, o caractere / indica um subdiretório e o caractere &ast; corresponde a todos. A tabela a seguir lista várias regras de exemplo.

<table>
 <tbody>
  <tr>
   <th>Exemplo de regra</th>
   <th>Efeito</th>
  </tr>
  <tr>
   <td><code>{ /include "*" }</code></td>
   <td>Incluir todos os arquivos.</td>
  </tr>
  <tr>
   <td><code>{ /exclude "*.pdf" }</code></td>
   <td>Excluir todos os arquivos PDF.</td>
  </tr>
  <tr>
   <td><code> { /exclude "*/pom.xml" }</code></td>
   <td>Excluir arquivos POM.</td>
  </tr>
  <tr>
   <td><code class="code">{ /exclude "/content/*" }
      { /include "/content/catalogs/geometrixx/templatepages" }
      { /include "/content/catalogs/geometrixx/templatepages/*" }</code></td>
   <td><p>Exclua todos os arquivos abaixo do nó /content.</p> <p>Inclua o nó /content/catalogs/geometrixx/templatepages.</p> <p>Incluir todos os nós filhos de /content/catalogs/geometrixx/templatepages.</p> </td>
  </tr>
 </tbody>
</table>

### Extração de strings  {#extracting-the-strings}

sem POM:

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

Com POM: adicione isso ao POM:

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

* `raw.xliff`: cadeias de caracteres extraídas
* `warn.log`: avisos (se houver), se a API `CQ.I18n.getMessage()` for usada incorretamente. Eles sempre precisam de uma correção e, em seguida, uma reexecução.

* `parserwarn.log`: avisos do analisador (se houver), por exemplo, problemas do analisador js
* `potentials.xliff`: candidatos &quot;em potencial&quot; que não são extraídos, mas podem ser cadeias de caracteres legíveis por humanos que precisam de tradução (podem ser ignorados, ainda produzem uma grande quantidade de falsos positivos)
* `strings.xliff`: arquivo xliff nivelado, a ser importado para ALF
* `backrefs.txt`: permite pesquisa rápida de locais de código-fonte para uma determinada cadeia de caracteres
