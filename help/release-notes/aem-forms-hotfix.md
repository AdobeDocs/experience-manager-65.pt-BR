---
title: Hotfixes para o AEM Forms
description: Fornece informações sobre como baixar e instalar um hotfix do AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
source-git-commit: 276b0122fb3d88c584dd6b2b4c2c6f6eda9d0537
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 2%

---

# Hotfixes do Adobe Experience Manager Forms{#aem-form-hotfix}

Este artigo lista as correções críticas implementadas para resolver problemas conhecidos, melhorar a estabilidade do sistema e aprimorar o desempenho geral do AEM Forms.

## Hotfixes para o Adaptive Forms {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Data</strong></td>
    <td><strong>Link de download de Hotfix (link de Distribuição de software AEM)</strong></td>
    <td><strong>Problemas corrigidos</strong></td>
   </tr>
   <tr>
    <td>terça-feira, 20 de novembro de 2023</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Hotfix do AEM Service Pack 6.5.18.0 para Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Hotfix do AEM Service Pack 6.5.18.0 para Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Hotfix do AEM Service Pack 6.5.18.0 para SO Mac</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>A assinatura em linha para de funcionar, quando um URL de redirecionamento é definido no contêiner do guia de um Formulário adaptável. (FORMS-10493)</li>
    <li>Os modelos de Documento de registro (DoR) não são publicados para o Adaptive Forms localizado. (FORMS-10535)</li>
    <li>A comunicação interativa com imagens grandes em linha falha ao abrir no modo de edição. (FORMS-10578)</li>
    </ul>
    </td>    
    </tr>
    <tbody>
     </table>

## Baixar e instalar um Hotfix {#download-install-hotfix}

Execute as seguintes etapas para baixar e instalar o Hotfix:

1. Baixar [Hotfix](#hotfix-for-adaptive-forms) no link Distribuição de software.
1. Extraia o arquivo de Hotfix para obter um pacote de Experience Manager (.zip) e arquivos de pacote (.jar).
1. Carregue e instale o pacote (.zip) por meio do [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Abra os pacotes do gerenciador de configurações `https://server:host/system/console/bundles`, carregue e instale o pacote (.jar). O hotfix do está instalado.
