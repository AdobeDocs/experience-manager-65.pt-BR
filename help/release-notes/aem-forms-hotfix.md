---
title: Hotfixes para o AEM Forms
description: Fornece informações sobre como baixar e instalar um hotfix do AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 5e2799505bc6d69cd5898445a9300ad162ef74fd
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 1%

---

# Hotfixes do Adobe Experience Manager Forms{#aem-form-hotfix}

Este artigo lista as correções críticas implementadas para resolver problemas conhecidos, melhorar a estabilidade do sistema e aprimorar o desempenho geral do AEM Forms.

>[!NOTE]
>
> Os hotfixes foram projetados para serem cumulativos, abrangendo todas as correções anteriores. Ao aplicar a correção mais recente a uma versão do, ele não apenas aborda o problema mais recente, mas também incorpora todas as correções de erros e aprimoramentos anteriores.

## Hotfixes para o Adaptive Forms {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Data</strong></td>
    <td><strong>Link de download de Hotfix (link de Distribuição de software AEM)</strong></td>
    <td><strong>Problemas corrigidos</strong></td>
  </tr>
  <tr>
    <td>sexta-feira, 16 de maio de 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1192-010.zip">Hotfix do AEM Service Pack 6.5.20.0 para Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1192-010.zip">Hotfix do AEM Service Pack 6.5.20.0 para Linux </a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1192-010.zip">Hotfix do AEM Service Pack 6.5.20.0 para Apple macOS</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>Em um Formulário adaptável baseado em um XDP com scripts incorporados em caixas de seleção, os scripts não são executados para elementos após essas caixas de seleção. Uma correção está disponível para esse problema. (FORMS-14244) </li>
     <li> As linhas no widget seletor de datas são truncadas ao percorrer meses no widget pop-up para campos com padrão Editar/Exibir. Uma correção está disponível para esse problema. (FORMS-13620) </li>
     <li>Os envios de formulários falham ao tentar usar o serviço DOR (Documento de registro) no back-end. A mensagem de erro encontrada é: "Não foi possível concluir a ação enviar porque o recurso de formulário não foi atribuído corretamente." (FORMS-13798) </li>
     <li>Quando um Formulário adaptável é enviado de uma instância de publicação do Adobe Experience Manager para um fluxo de trabalho do Adobe Experience Manager, o fluxo de trabalho não salva os anexos.  (FORMS-14209) </li>
     <li> Ao instalar o pacote AEM 6.5 Forms Service Pack 20 (pacote complementar do AEM Forms para SP20), a interface do usuário (UI) do AEM Sites exibe uma significativa degradação do desempenho.  (FORMS-13791) </li>
     <li>O serviço de preenchimento prévio falha com uma exceção de ponteiro nulo nas Comunicações interativas. (CQDOC-21355)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>terça-feira, 29 de janeiro de 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">Hotfix do AEM Service Pack 6.5.19.0 para Windows no servidor JEE</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>No AEM Forms no servidor JEE, o Forms HTML5 que usa o caminho de contexto não é renderizado. (FORMS-12485, FORMS-12691).</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>terça-feira, 29 de janeiro de 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">Hotfix do AEM Service Pack 6.5.18.0 para Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">Hotfix do AEM Service Pack 6.5.18.0 para Linux</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">Hotfix do AEM Service Pack 6.5.18.0 para Apple macOS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li> O componente de Assinatura escritas pronto para uso não é renderizado para uma visualização em um formulário adaptável. (FORMS-12073).</li>
    </ul>
    </td>    
   </tr>
   <tr>
    <td>terça-feira, 20 de novembro de 2023</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Hotfix do AEM Service Pack 6.5.18.0 para Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Hotfix do AEM Service Pack 6.5.18.0 para Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Hotfix do AEM Service Pack 6.5.18.0 para Apple macOS</a></li>
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
