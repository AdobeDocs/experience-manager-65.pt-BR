---
title: Reduzindo vulnerabilidades de XXE, configuração do modo de desenvolvimento Struts e execução remota de código para AEM Forms no JEE
description: Reduzindo vulnerabilidades de XXE, configuração e execução remota de código para AEM Forms no JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 9fade12f-a038-4fd6-8767-1c30966574c5
solution: Experience Manager, Experience Manager Forms
release-date: 2025-08-05T00:00:00Z
source-git-commit: f57b2e7874aae10dd2112e688f8db6a660f2cbb9
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 5%

---

# Redução de RCE (CVE-2025-49533), configuração do modo de desenvolvimento do Struts (CVE-2025-54253), XXE (CVE-2025-54254) e vulnerabilidades para AEM Forms no JEE {#mitigating-xxe-configuration-rce-vulnerabilities-aem-forms}

## Referência rápida

| **Nível de Impacto** | **Versões afetadas** | **Ação recomendada** |
|---|---|---|
| **Crítico** | AEM 6.5 Forms no JEE Service Pack 23 (6.5.23.0) | [Instalar hotfix mais recente](#option-1-for-users-on-version-65230-install-latest-hotfix) |
| **Crítico** | AEM 6.5 Forms no JEE Service Pack 18 a 22 (6.5.18.0 - 6.5.22.0) | [Instalar manualmente as correções](#option-2-for-users-on-65180---65220-manual-hotfix-installation) |
| **Crítico** | AEM 6.5 Forms no JEE Service Pack 17 (6.5.17.0) ou anterior | Atualize para uma versão com suporte do Service Pack e aplique as etapas de mitigação recomendadas para a nova versão |
| **Não Afetado** | AEM Forms no OSGi, Workbench, Cloud Service | Nenhuma ação necessária |

**Vulnerabilidades Endereçadas:**

- Execução de código remoto (CVE-2025-49533)
- Problemas de segurança da configuração (CVE-2025-54253)
- Processamento de Entidade Externa XML (XXE) (CVE-2025-54254)

## Visão geral

### O que foi afetado

| Vulnerabilidade | Impacto | Componentes afetados |
|---|---|---|
| **CVE-2025-49533**: Execução de Código Remoto | Execução de código não autenticado em GetDocumentServlet | AEM 6.5 Forms no JEE Service Pack 23 (6.5.23.0) e anterior |
| **CVE-2025-54253**: Problemas de Configuração | Modo de desenvolvimento Struts habilitado na interface do administrador | AEM 6.5 Forms no JEE Service Pack 23 (6.5.23.0) e anterior |
| **CVE-2025-54254**: XXE Processando | O módulo Segurança de documentos permite acesso não autorizado a arquivos | AEM 6.5 Forms no JEE Service Pack 23 (6.5.23.0) e anterior |


### O que não é afetado

- Experience Manager Forms Workbench (todas as versões)
- Experience Manager Forms no OSGi (todas as versões)
- Experience Manager Forms as a Cloud Service

## Opções de resolução


### Antes de começar

Antes de fazer qualquer alteração, faça um backup do arquivo EAR ou DSC que você está prestes a modificar ou atualizar:

- Localize o arquivo EAR ou DSC original no diretório de implantação.
- Copie o arquivo para um local de backup seguro fora do diretório de implantação.
- Certifique-se de que o backup esteja completo e acessível antes de prosseguir com qualquer atualização.

Essa precaução permite restaurar o estado original caso você encontre problemas durante o processo de atualização.

### Opção 1: (Para usuários na versão 6.5.23.0) Instalar Hotfix Mais Recente

1. [Baixe o hotfix para 6.5.23.0](/help/release-notes/aem-forms-hotfix.md).
1. Siga as [instruções de instalação de hotfix/patch padrão](/help/release-notes/jee-patch-installer-65.md)
1. Se você estiver usando a Segurança de documentos (antigo Rights Management) no IBM WebSphere ou no Oracle WebLogic, defina a seguinte propriedade do sistema Java (argumento JVM) antes de iniciar o servidor do AEM Forms:

   ```
   -Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
   ```

1. Reiniciar o servidor de aplicativos

### Opção 2: (Para usuários em 6.5.18.0 - 6.5.22.0) Instalação do Hotfix Manual

+++ Instalação manual de Hotfix do 6.5.18.0 - 6.5.22.0

**Etapa 1: baixar e extrair o pacote de Hotfix**

- Baixe o [hotfix de 6.5.18.0 - 6.5.22.](/help/release-notes/aem-forms-hotfix.md) do Portal de Distribuição de Software da Adobe
- Extrair localmente

**Etapa 2: Navegar até a Pasta de Versão Correta**

- Com base na versão do Service Pack instalada em seu ambiente, vá para a pasta correspondente.

  Exemplo para o Service Pack 20: a pasta é:

  ```
  <extracted-hotfix>/SP20/
  ```

**Etapa 3: Localizar o Diretório de Implantação**

- No AEM Forms no servidor JEE, acesse:

  ```
  [AEM installation directory]/deploy
  ```

  Exemplo: `adobe/adobe-experience-manager-forms/deploy`



**Etapa 4: atualizar e substituir os arquivos EAR**

>[!BEGINTABS]

>[!TAB JBoss]

1. Abrir `adobe-core-jboss.ear` e substituir `adminui.war` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adminui.war
   ```

   Por exemplo, `adobe-xxe-configuration-hotfix/SP20/jboss/adminui.war`

1. Dentro do `adobe-core-jboss.ear`, vá para a pasta `lib/` e substitua `adobe-uisupport.jar` por:

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   Por exemplo, `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. Salve o EAR. Verifique se as alterações foram salvas corretamente.


1. Substituir `adobe-edcserver-jboss.ear` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-edcserver-jboss.ear
   ```

   Por exemplo, `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-edcserver-jboss.ear`

1. Substituir `adobe-forms-jboss.ear` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/jboss/adobe-forms-jboss.ear
   ```

   Por exemplo, `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-forms-jboss.ear`



>[!TAB WebLogic]

1. Abrir `adobe-core-weblogic.ear` e substituir `adminui.war` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adminui.war
   ```

   Por exemplo, `adobe-xxe-configuration-hotfix/SP20/weblogic/adminui.war`

1. Dentro do `adobe-core-weblogic.ear`, substitua `adobe-uisupport.jar` por:

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   Por exemplo, `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. Salve o EAR. Verifique se as alterações foram salvas corretamente.


1. Substituir `adobe-edcserver-weblogic.ear` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-edcserver-weblogic.ear
   ```

   Por exemplo, `adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-edcserver-weblogic.ear`

1. Substituir `adobe-forms-weblogic.ear` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/weblogic/adobe-forms-weblogic.ear
   ```

   Por exemplo, `adobe-xxe-configuration-hotfix/SP20/weblogic/adobe-forms-weblogic.ear`

>[!TAB WebSphere]

1. Abrir `adobe-core-websphere.ear` e substituir `adminui.war` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adminui.war
   ```

   Por exemplo, `adobe-xxe-configuration-hotfix/SP20/websphere/adminui.war`

1. Dentro do `adobe-core-websphere.ear`, substitua `adobe-uisupport.jar` por:

   ```
   adobe-xxe-configuration-hotfix/SP[version]/adobe-uisupport.jar
   ```

   Por exemplo, `adobe-xxe-configuration-hotfix/SP20/adobe-uisupport.jar`

1. Salve o EAR. Verifique se as alterações foram salvas corretamente.


1. Substituir `adobe-edcserver-websphere.ear` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-edcserver-websphere.ear
   ```

   Por exemplo, `adobe-xxe-configuration-hotfix/SP20/websphere/adobe-edcserver-websphere.ear`

1. Substituir `adobe-forms-websphere.ear` por

   ```
   adobe-xxe-configuration-hotfix/SP[version]/websphere/adobe-forms-websphere.ear
   ```

   Por exemplo, `adobe-xxe-configuration-hotfix/SP20/websphere/adobe-forms-websphere.ear`

>[!ENDTABS]



**Etapa 5: atualizar `adobe-rightsmanagement-<appserver>-dsc.jar`arquivo com**

```
adobe-xxe-configuration-hotfix/SP[version]/<appserver>/adobe-rightsmanagement-<appserver>-dsc.jar
```

Por exemplo, `adobe-xxe-configuration-hotfix/SP20/jboss/adobe-rightsmanagement-jboss-dsc.jar`

**Etapa 6: Configuração Adicional para Segurança de Documentos no WebSphere e no WebLogic**:

Se você estiver usando a Segurança de documentos (antigo Rights Management), defina a seguinte propriedade do sistema Java (argumento JVM) antes de iniciar o servidor do AEM Forms:

```
-Dcom.adobe.forms.jee.services.allowDoctypeDeclaration=true
```


**Etapa 7: executar novamente o Gerenciador de Configurações**

- Inicie o Configuration Manager para reimplantar o EAR atualizado e aplicar o hotfix

+++

### Opção 3: (Para usuários em 6.5.17.0 e anterior) Caminho de Atualização

1. [Atualizar para uma versão compatível do Service Pack](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)
1. Siga a Opção 1 ou a Opção 2 acima com base em sua nova versão

## Referências

- [CWE-611: Restrição Inadequada de Referência de Entidade Externa XML](https://cwe.mitre.org/data/definitions/611.html)
- [CWE-16: Configuração](https://cwe.mitre.org/data/definitions/16.html)
- [Folha de características de prevenção do OWASP XXE](https://owasp.org/www-community/vulnerabilities/XML_External_Entity_XXE_Processing)
- [Práticas recomendadas de segurança da Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=pt-BR)
