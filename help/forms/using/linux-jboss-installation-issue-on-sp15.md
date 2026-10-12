---
title: Problema de instalação do pacote de serviços do AEM Forms JEE 6.5.15.0 no ambiente JBoss® Linux®
description: O pacote de serviços AEM Forms JEE 6.5.15.0 não está instalado corretamente no ambiente JBoss® Linux®. As alterações de patch não são aplicadas ao servidor de aplicativos. Adicione o arquivo "RUP_BOM.xml" ao diretório XML.
SEO Description: AEM Forms JEE 6.5.15.0 service pack  is not installed properly on the JBoss Linux environment.
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 1%
---
# Problema de instalação do AEM Forms 6.5.15.0 JEE Service Pack no ambiente JBoss® {#aem-forms-installation-issue-environment}

## Problema {#issue}

O AEM Forms JEE 6.5.15.0 service pack não está instalado corretamente no ambiente JBoss® Linux®. No arquivo `PatchInstallerProcessing[1-9*].log`, a entrada do log, `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing`, está registrada. Esta entrada indica que a instalação do AEM Forms JEE 6.5.15.0 service pack não foi bem-sucedida.

## Aplica-se a {#applies-to}

Esta solução aplica-se a:
* Ambiente JBoss® Linux®

>[!NOTE]
>
> Verifique se o service pack do AEM Forms JEE 6.5.15.0 está instalado no servidor de aplicativos pelo menos uma vez antes de executar as etapas de [adição do arquivo RUP_BOM.xml ao diretório XML](#solution-solution).

## Solução {#solution}

Para corrigir o problema de instalação do service pack do AEM Forms JEE 6.5.15.0, adicione o arquivo `RUP_BOM.xml` ao diretório XML:
1. Navegue até a pasta onde você extraiu o patch `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. Navegue até o local `/CDROM_Installers/Linux/Disk1/InstData` e localize o arquivo `Resource1.zip`.
1. Copie o arquivo `Resource1.zip` em algum local diferente fora da pasta extraída e descompacte o arquivo `Resource1.zip`.
1. Navegue até `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` e copie o arquivo `RUP_BOM.xml`.
1. Cole o arquivo RUP_BOM.xml em `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. Reinstale o [pacote de serviços do AEM Forms JEE 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
