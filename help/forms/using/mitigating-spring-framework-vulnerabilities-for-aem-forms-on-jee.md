---
title: Redução de vulnerabilidades do Spring Framework para AEM Forms no JEE
description: Redução de vulnerabilidades do Spring Framework para AEM Forms no JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 61cce7cd8290156bec6dcc351a59093f545a4ec7
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---


# Reduzindo vulnerabilidades do Spring Framework para AEM Forms no JEE

Este documento fornece orientação sobre como lidar com duas vulnerabilidades críticas do Spring Framework que afetam o AEM Forms no JEE:

- **[CVE-2024-38819](https://spring.io/security/cve-2024-38819)**: vulnerabilidade de passagem de caminho em estruturas Web funcionais
- **[CVE-2024-38820](https://spring.io/security/cve-2024-38820)**: exceção de correspondência sensível a maiúsculas e minúsculas do Spring Framework DataBinder

## Versões afetadas

- Adobe Experience Manager 6.5 Forms no JEE
- Versões AEM 6.5 Forms GA para 6.5.22.0

## Resolução

### Soluções específicas para versão

| Versão do AEM Forms | Ação necessária |
|-------------------|-----------------|
| 6.5.22.0 | 1. [Baixe o hotfix do seu ambiente](/help/release-notes/aem-forms-hotfix.md). </br> 2. Para instalar esta correção, siga as instruções para [instalar o Service Pack em um Formulário do AEM no JEE](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). |
| 6.5.17.0 - 6.5.21.0 | [Aplicar etapas de mitigação manual](#manual-mitigation-steps). |
| 6.5 - 6.5.16.0 | 1. [Instalar o service pack mais recente](/help/release-notes/release-notes.md)<br>2. [Implemente a solução apropriada](#version-specific-solutions) com base na sua versão atualizada. |

> **Observação**: a AEM Forms oferece suporte oficial apenas aos seis service packs mais recentes. Os usuários de versões mais antigas devem primeiro atualizar para o service pack mais recente e, em seguida, instalar o hotfix necessário.

## Considerações sobre implantação

### Para ambientes em cluster

Ao trabalhar com uma implantação em cluster:

- Aplicar substituições de arquivos JAR (Etapa #4) em **todos os nós** no cluster
- Manter a consistência usando versões idênticas do JAR em todos os servidores
- Conclua as atualizações em todos os nós antes de iniciar qualquer reinício de serviço
- Implementar uma estratégia coordenada de reinicialização para minimizar o tempo de inatividade do sistema

### Para ambientes de nó único

Ao trabalhar com uma implantação independente:

- Siga um processo simplificado, pois não há servidores localizadores para gerenciar
- Omitir etapas relacionadas à configuração ou à inicialização do servidor localizador
- Conclua todas as outras etapas conforme instruído, especialmente substituições de JAR e atualizações de manifesto
- Reinicie o servidor de aplicativos após implementar todas as alterações

## Etapas de mitigação manual

1. Interrompa os servidores de aplicativos.
1. Servidores de parada e de localizador.
1. Remover JARs de Mola do Core EAR:
   1. Vá até `[Adobe_Experience_Manager_Forms installation directory]/deploy`.
   1. Abra o arquivo `adobe-core-<appserver>.ear` usando uma ferramenta de gerenciador de arquivamento. Onde `<appserver>` pode ser JBoss, WebLogic ou WebSphere, dependendo do seu ambiente:
   - **Para JBoss:** Navegue até a pasta `ear/lib` e exclua os seguintes arquivos JAR:
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **Para WebLogic ou WebSphere:** exclua os seguintes arquivos JAR da raiz do EAR:
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **Para todos os servidores de aplicativos:** No nível raiz de `adobe-core-<appserver>.ear`, abra o arquivo `adobe-dscf.jar` e edite o arquivo `META-INF/MANIFEST.MF` para remover qualquer referência aos seguintes arquivos JAR:
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

1. Substituir arquivos JAR da distribuição do Geode:
   1. Navegue até `<Adobe_Experience_Manager_Forms>/lib/caching/lib`
   1. Substitua os arquivos JAR existentes pelas versões atualizadas:
   - `spring-context-<version>.jar` → `spring-context-6.1.14.jar`
   - `spring-beans-<version>.jar` → `spring-beans-6.1.14.jar`
   - `spring-core-<version>.jar` → `spring-core-6.1.14.jar`
   - `spring-jcl-<version>.jar` → `spring-jcl-6.1.14.jar`
   - `spring-web-<version>.jar` → `spring-web-6.1.14.jar`

   Para obter os arquivos JAR mais recentes, baixe o arquivo spring-6.1.14-jars.zip da [Distribuição de software da Adobe](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/spring-6.1.14-jars.zip) e extraia o arquivo ZIP para acessar os arquivos JAR atualizados do Spring framework.

   1. Atualize os arquivos MANIFEST.MF nos seguintes arquivos JAR:
   - `geode-server-all-<version>.jar`
   - `gfsh-dependencies.jar`

   Para cada JAR:
   - Abra o JAR usando uma ferramenta de gerenciador de arquivo
   - Localizar e extrair o arquivo `META-INF/MANIFEST.MF`
   - Editar o arquivo MANIFEST.MF em um editor de texto
   - Encontre a seção &quot;Class-Path&quot; e atualize todas as referências de estrutura Spring:
      - `spring-core-<version>.jar` a `spring-core-6.1.14.jar`
      - `spring-web-<version>.jar` a `spring-web-6.1.14.jar`
      - `spring-context-<version>.jar` a `spring-context-6.1.14.jar`
      - `spring-beans-<version>.jar` a `spring-beans-6.1.14.jar`
      - `spring-jcl-<version>.jar` a `spring-jcl-6.1.14.jar`
   - Salve o arquivo MANIFEST.MF modificado
   - Substitua o MANIFEST.MF original no JAR pela sua versão atualizada
   - Salve o arquivo JAR

   1. Problemas comuns a serem observados:
      - Verifique se não há entradas duplicadas no manifesto
      - Manter terminações de linha apropriadas
      - Verificar se todos os JARs referenciados existem nos locais especificados

   1. Etapas de verificação:
      - Verifique se o manifesto foi atualizado corretamente
      - Verifique se todas as dependências Spring estão referenciadas corretamente
      - Garantir que nenhuma referência de versão antiga permaneça
      - Teste o aplicativo para confirmar se não há problemas de carregamento de classe

1. Execute o Gerenciador de configurações.

1. Reiniciar servidores:
   - Iniciar os servidores localizadores usando o JDK 17
   - Inicie os Servidores de aplicativos usando a mesma versão do JDK (JDK 8 ou JDK 11) usada anteriormente.
