---
title: Problema de instalação do pacote de serviços do AEM Forms JEE 6.5.15.0 no ambiente JBoss® Linux®
description: O pacote de serviços AEM Forms JEE 6.5.15.0 não está instalado corretamente no ambiente JBoss® Linux®. As alterações de patch não são aplicadas ao servidor de aplicativos. Adicione o arquivo "RUP_BOM.xml" ao diretório XML.
source-git-commit: 76a3a87408ceb13023737379c20fb44ce5fb180a
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 1%

---


# Problema de instalação do AEM Forms 6.5.15.0 JEE Service Pack no ambiente JBoss® {#aem-forms-installation-issue-environment}

## Problema {#issue}

O pacote de serviços AEM Forms JEE 6.5.15.0 não está instalado corretamente no ambiente JBoss® Linux®. Entrada `PatchInstallerProcessing[1-9*].log` arquivar a entrada de log, `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component isn't in the installation. Skipping Processing`, está registrado. Esta entrada indica que a instalação do AEM Forms JEE 6.5.15.0 service pack não foi bem-sucedida.

## Aplica-se a {#applies-to}

Esta solução aplica-se a:
* Ambiente JBoss® Linux®

>[!NOTE]
>
> Verifique se o pacote de serviços do AEM Forms JEE 6.5.15.0 está instalado no servidor de aplicativos pelo menos uma vez antes de executar as etapas de [adicionando o arquivo RUP_BOM.xml ao diretório XML](#solution-solution).

## Solução {#solution}

Para corrigir o problema de instalação do pacote de serviços AEM Forms JEE 6.5.15.0, adicione o `RUP_BOM.xml` para o diretório XML:
1. Navegue até a pasta onde você extraiu o patch `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. Navegue até `/CDROM_Installers/Linux/Disk1/InstData` localização e localize o `Resource1.zip` arquivo.
1. Copie o `Resource1.zip` arquivo em algum local diferente fora da pasta extraída e descompacte `Resource1.zip` arquivo.
1. Navegue até `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` e copie o `RUP_BOM.xml` arquivo.
1. Cole o arquivo RUP_BOM.xml em `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. Reinstale o [Pacote de serviços do AEM Forms JEE 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).