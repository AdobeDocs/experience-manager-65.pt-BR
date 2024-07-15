---
title: Problema de instalação do pacote de serviços do AEM Forms JEE 6.5.15.0 no ambiente JBoss® Linux®
description: O pacote de serviços AEM Forms JEE 6.5.15.0 não está instalado corretamente no ambiente JBoss® Linux®. As alterações de patch não são aplicadas ao servidor de aplicativos. Adicione o arquivo "RUP_BOM.xml" ao diretório XML.
exl-id: 96ecbe58-a859-4432-a2d8-3d5dc0eaf989
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 1%

---

# Problema de instalação do AEM Forms 6.5.15.0 JEE Service Pack no ambiente JBoss® {#aem-forms-installation-issue-environment}

## Problema {#issue}

O pacote de serviços AEM Forms JEE 6.5.15.0 não está instalado corretamente no ambiente JBoss® Linux®. No arquivo `PatchInstallerProcessing[1-9*].log`, a entrada do log, `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing`, está registrada. Esta entrada indica que a instalação do AEM Forms JEE 6.5.15.0 service pack não foi bem-sucedida.

## Aplica-se a {#applies-to}

Esta solução aplica-se a:
* Ambiente JBoss® Linux®

>[!NOTE]
>
> Verifique se o service pack do AEM Forms JEE 6.5.15.0 está instalado no servidor de aplicativos pelo menos uma vez antes de executar as etapas de [adição do arquivo RUP_BOM.xml ao diretório XML](#solution-solution).

## Solução {#solution}

Para corrigir o problema de instalação do pacote de serviços AEM Forms JEE 6.5.15.0, adicione o arquivo `RUP_BOM.xml` ao diretório XML:
1. Navegue até a pasta onde você extraiu o patch `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. Navegue até o local `/CDROM_Installers/Linux/Disk1/InstData` e localize o arquivo `Resource1.zip`.
1. Copie o arquivo `Resource1.zip` em algum local diferente fora da pasta extraída e descompacte o arquivo `Resource1.zip`.
1. Navegue até `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` e copie o arquivo `RUP_BOM.xml`.
1. Cole o arquivo RUP_BOM.xml em `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. Reinstale o [AEM Forms JEE 6.5.15.0 service pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
