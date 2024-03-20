---
title: Reduzindo vulnerabilidades do Struts 2 para Experience Manager Forms no JEE
description: Reduzindo vulnerabilidades do Struts 2 para Experience Manager Forms no JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 73b5aff2-1320-4d9a-8972-54c4fdd3a2c2
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 1%

---

# Reduzindo vulnerabilidades do Struts 2 para Experience Manager Forms {#mitigatin-struts2-rce-vulnerabilities-for-aem-forms}

## Problema

Vulnerabilidades críticas de segurança foram relatadas para o Struts 2, uma estrutura de aplicativo Web popular e de código aberto para o desenvolvimento de aplicativos Web Java EE. As seguintes vulnerabilidades foram analisadas:

| Vulnerabilidade | O que foi impactado? | O que não é impactado? |
|---|---|---|
| [CVE-2023-50164](https://cve.mitre.org/cgi-bin/cvename.cgi?name=2023-50164) | Experience Manager 6.5 Forms no JEE (todas as versões de 6.5 GA para 6.5.19.0) | <ul><li> Experience Manager Forms Workbench (todas as versões)</li> <li> Experience Manager Forms no OSGi (todas as versões) </li> <li> Experience Manager Forms as a Cloud Service </li> <ul> |

## Resolução

A tabela a seguir lista a resolução de todas as versões afetadas:

| Versão | Versão atual | Ação do usuário |
|---|---|---|
| Experience Manager 6.5 Forms no JEE | 6.5.19.0 | [Instalar o pacote de serviços mais recente](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=en) |
| Experience Manager 6.5 Forms no JEE | 6.5.13.0 - 6.5.18.0 | Use um dos seguintes métodos: <ul><li>  <a href="https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=en"> Instalar o pacote de serviços mais recente </a> </li> <li> <a href ="#use-manual-mitigation-steps"> Usar etapas de mitigação manual </a> |
| Experience Manager 6.5 Forms no JEE | 6.5 - 6.5.12.0 | [Instalar o pacote de serviços mais recente](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=en)  </br> </br> **NOTA:** Atualmente, o AEM Forms é compatível com as versões 6.5.13.0 a 6.5.19.0. Se você estiver usando uma versão mais antiga, recomendamos atualizar para a versão 6.5.13.0 ou posterior. Para obter instruções sobre como instalar o AEM versão 6.5.13.0 ou posterior, consulte notas de versão. |

### Usar etapas de mitigação manual {#use-manual-mitigation-steps}

Você pode usar as etapas de mitigação manual para resolver o problema no Servidor de formulário AEM 6.5 que executa o Service Pack 13 para AEM 6.5 que executa o Service Pack 18 (6.5.13.0 - 6.5.18.0):

1. Baixe o [struts-core 2.5.33 jar](https://repo1.maven.org/maven2/org/apache/struts/struts2-core/2.5.33/struts2-core-2.5.33.jar) para uma pasta local. Por exemplo, C:\Users\labuser\Desktop\struts2-core-2.5.33.jar.
1. Baixe a Ferramenta de correção manual do AEM Forms no JEE em [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/patch_utility/archive-patcher-1.0.0.zip).
1. Descompacte o arquivo da ferramenta de correção manual. Por exemplo, extraia para a variável `/Users/labuser/Desktop/archive-patcher-1.0.0 folder`. Os seguintes arquivos são extraídos:
   * archive-patcher-1.0.0.jar
   * patch-archive.bat
   * patch-archive.sh

>[!BEGINTABS]

>[!TAB Windows]

1. Desative todas as instâncias e localizadores do servidor.

1. Abra a janela do terminal e navegue até a pasta que contém a Ferramenta de correção manual AEM Forms on JEE (arquivos extraídos).

1. Execute o seguinte comando para pesquisar todos os arquivos com bibliotecas struts2 mais antigas. Antes de executar o comando, substitua o caminho no comando pelo caminho do AEM Forms Server:


   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\configurationManager\export -pattern=.*struts2-core.*jar$
   ```

   >[!NOTE]
   >
   >
   >A ferramenta requer conectividade com a Internet, pois baixa dependências no tempo de execução. Portanto, antes de executar a ferramenta, verifique se você está conectado à Internet.

1. Execute os seguintes comandos na ordem listada para substituição recursiva no local. Antes de executar o comando, substitua o caminho no comando pelo caminho do AEM Forms Server e `struts2-core-2.5.33.jar` arquivo.



   ```
   patch-archive.bat -root=C:\Adobe\Adobe_Experience_Manager_Forms\configurationManager\export -pattern=.*struts2-core.*jar$ -action=replace C:\Users\labuser\Desktop\struts2-core-2.5.33.jar
   ```

   As etapas acima corrigem todos os arquivos ear com bibliotecas struts2 mais antigas.

1. Desimplante o EAR mais antigo e implante o arquivo EAR corrigido, disponível na pasta de exportação, no servidor de aplicativos.

1. Inicie o AEM Forms Server.

>[!TAB Linux]

1. Desative todas as instâncias e localizadores do servidor.

1. Abra a janela do terminal e navegue até a pasta que contém a Ferramenta de correção manual AEM Forms on JEE (arquivos extraídos).

1. Execute o seguinte comando para pesquisar todos os arquivos com bibliotecas struts2 mais antigas. Antes de executar o comando, substitua o caminho no comando pelo caminho do AEM Forms Server:


   ```
   ./patch-archive.sh -root=/opt/Adobe/Adobe_Experience_Manager_Forms/configurationManager/export/ -pattern=.*struts2-core.*jar$
   ```

   >[!NOTE]
   >
   >
   >A ferramenta requer conectividade com a Internet, pois baixa dependências no tempo de execução. Portanto, antes de executar a ferramenta, verifique se você está conectado à Internet.

1. Execute os seguintes comandos na ordem listada para substituição recursiva no local. Antes de executar o comando, substitua o caminho no comando pelo caminho do AEM Forms Server e `struts2-core-2.5.33.jar` arquivo.



   ```
   ./patch-archive.sh -root=/opt/Adobe/Adobe_Experience_Manager_Forms/configurationManager/export/ -pattern=.*struts2-core.*jar$ -action=replace /opt/struts2-core-2.5.33.jar
   ```

   As etapas acima corrigem todos os arquivos ear com bibliotecas struts2 mais antigas.

1. Desimplante o EAR mais antigo e implante o arquivo EAR corrigido, disponível na pasta de exportação, no servidor de aplicativos.

1. Inicie o AEM Forms Server.

>[!ENDTABS]




<!-- 
### Manual patching tool 


>[!BEGINTABS]

>[!TAB Windows]

    ```
    
    patch-archive.bat [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.

>[!TAB macOS]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  

>[!TAB Linux]

    ```
    
    patch-archive.sh [-root=dir-or-file] [-pattern=regex] [-action=list(default)|delete|replace <replacement-file>]

    ```

* **dir-or-file**: Specifies path of directory containing multiple archives to patch. The default path for AEM Forms on JEE is <>. 
* **regex**: Specifies regular expression identifying a file or an archive entry to patch. It is tested against each file's or archive entry's absolute path. For example, the pattern `.*struts2-core-2.5.30.jar$` search for all the lines that end with the exact string `struts2-core-2.5.30.jar`.
* **list**: Lists the matched files or archive entries. It recursively searches for and reports all instances of the supplied pattern matched in any entry present in any archive file (zip/jar/war/ear) inside the supplied root directory. No changes are made to any file. It is the default action of the tool, when no action is specified.
* **delete**: Deletes the matched files or archive entries. If the matched entity is an archive, deletion happens before traversing it. This prevents any potentially matching entries inside it from being reported.  
* **replace**: Substitutes the matched files or archive entries with the supplied replacement. If the matched entity is an archive, replacement happens before traversing it. This prevents any potentially matching entries inside it from being reported.  



>[!ENDTABS]









-->
