---
title: Hotfix do AEM Form Service Pack
description: Fornece informações sobre como baixar e instalar o hotfix do AEM Forms Service Pack
source-git-commit: 169d407835098add0312b0d12c2c80035b525762
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---


# Hotfixes do Adobe Experience Manager{#aem-form-hotfix}

A instalação do mais recente [Pacote de serviços do AEM](/help/release-notes/release-notes.md) O é recomendado que inclua segurança, desempenho, estabilidade, e correções e aprimoramentos essenciais para o cliente lançados desde a disponibilização geral do Adobe Experience Manager 6.5.

## Hotfixes para o Adaptive Forms {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Data</strong></td>
    <td><strong>Nomes de Hotfix</strong></td>
    <td><strong>Correções</strong></td>
   </tr>
   <tr>
    <td>20 de novembro de 2023</td>
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

## Baixar e instalar o Hotfix {#download-install-hotfix}

Execute as seguintes etapas para baixar e instalar o Hotfix:

1. Baixar [Hotfix](#hotfix-for-adaptive-forms) no link SD.
1. Extraia o arquivo de Hotfix para obter um pacote de Experience Manager (.zip) e arquivos de pacote (.jar).
1. Faça upload e instale o pacote (.zip) por meio do Gerenciador de pacotes.
1. Abra os pacotes do gerenciador de configurações `https://server:host/system/console/bundles`, carregue e instale o pacote (.jar).
