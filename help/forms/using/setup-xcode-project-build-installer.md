---
title: Configurar o projeto Xcode e criar o aplicativo iOS
description: Explica como criar um aplicativo padrão do AEM Forms para iOS.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 78ce6107-8821-47d6-86ab-7ab968945e7c
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 2%

---

# Configurar o projeto Xcode e criar o aplicativo iOS{#set-up-the-xcode-project-and-build-the-ios-app}

O AEM Forms fornece o código-fonte completo do aplicativo AEM Forms. A origem contém todos os componentes para criar um aplicativo AEM Forms personalizado. O arquivo do código-fonte, `adobe-lc-mobileworkspace-src-<version>.zip` O faz parte da `adobe-aemfd-forms-app-src-pkg-<version>.zip` pacote na Distribuição de software.

Para obter a origem do aplicativo AEM Forms, execute as seguintes etapas:

1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
1. Selecionar **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. No **[!UICONTROL Filtros]** seção:
   1. Selecionar **[!UICONTROL Forms]** do **[!UICONTROL Solução]** lista suspensa.
   2. Selecione a versão e o tipo do pacote. Você também pode usar a variável **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Selecione o nome do pacote aplicável ao seu sistema operacional e **[!UICONTROL Aceitar termos do EULA]** e selecione **[!UICONTROL Baixar]**.
1. Abertura [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  e clique em **[!UICONTROL Fazer upload do pacote]** para carregar o pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

1. Para baixar o arquivo de código-fonte, abra `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` no navegador.
O pacote de origem é baixado no dispositivo.

A imagem a seguir exibe o conteúdo extraído do `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

A tabela a seguir detalha o conteúdo da variável `adobe-lc-mobileworkspace-src-[version]/ios` pasta.

<table>
 <tbody>
  <tr>
   <th><p>Diretório</p> </th>
   <th><p>Conteúdo</p> </th>
  </tr>
  <tr>
   <td><p><code>CordovaLib</code></p> </td>
   <td><p>PhoneGap SDK 6.4.0</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms</code></p> </td>
   <td><p>Recursos, plug-ins PhoneGap e módulo principal do aplicativo</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms.xcodeproj</code></p> </td>
   <td><p>Projeto Xcode para aplicativo AEM Forms</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>Arquivos HTML, CSS, imagens e JavaScript para o projeto de aplicativo do AEM Forms</p> </td>
  </tr>
 </tbody>
</table>

Para obter informações detalhadas sobre Assinatura de Código e adição de dispositivos ao Portal de Provisionamento do iOS, consulte [Configuração, processo e solução de problemas da assinatura do código do iOS](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

## Criar aplicativo AEM Forms padrão {#set-up-the-xcode-project}

1. Execute as seguintes etapas para configurar um projeto no Xcode e fornecer uma identidade de assinatura:

   Faça logon no computador Mac que tem o Xcode e o iOS SDK instalados e configurados.

1. Copie o `adobe-lc-mobileworkspace-src-<version>.zip` arquivar da pasta de downloads para `[User_Home]/Projects/`.
1. Extraia o arquivo no `[User_Home]/Projects/[your-project]`diretório.
1. Navegue até a ` [User_Home]/Projects/ `[seu-projeto]`/adobe-lc-mobileworkspace-src-[version]/ios` diretório.
1. Abra o `AEM Forms.xcodeproj` projeto no Xcode.
1. Clique em **AEM Forms**, em **METAS**, selecione **AEM Forms**. Selecione o **Configurações de build** localize o **Direito de assinatura de código** e, nos campos Depurar e Liberar, siga um destes procedimentos:

   * Deixe os campos não especificados para criar um aplicativo padrão do Mobile Workspace
   * Especifique os campos para conforme explicado em [Criação de um aplicativo AEM Forms seguro para o iOS](/help/forms/using/building-secure-mobile-workspace-app.md) para criar um aplicativo AEM Forms seguro.

1. No **Configurações de build** clique em **Todos** e clique em **Combinado**.
1. No **Configurações** listar, expandir **Assinatura de código**.
1. Para **Identidade de assinatura de código**, selecione a assinatura apropriada. Para obter informações detalhadas sobre como criar novas assinaturas, consulte [Criação e download de perfis de provisionamento de desenvolvimento](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html).
1. Certifique-se de que a mesma assinatura esteja selecionada para **Depurar**, **Versão**, e **Qualquer SDK do iOS**.
1. Substitua o seguinte código na `AEM Forms-info.plist` arquivo:

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   com o seguinte ao substituir `yourserver.com` com um nome de host apropriado para o seu servidor.

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSExceptionDomains</key>
   <dict>
   <key>yourserver.com</key>
   <dict>
   <!-Include to allow subdomains->
   <key>NSIncludesSubdomains</key>
   <true/>
   <!-Include to allow HTTP requests->
   <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
   <true/>
   <!-Include to support forward secrecy->
   <key>NSExceptionRequiresForwardSecrecy</key>
   <false/>
   <!-Include to specify minimum TLS version->
   <key>NSTemporaryExceptionMinimumTLSVersion</key>
   <string>TLSv1.1</string>
   </dict>
   </dict>
   </dict>
   ```

   >[!NOTE]
   >
   >Esta etapa é necessária somente se o aplicativo AEM Forms precisar se conectar a um servidor que não siga os requisitos do App Transport Security.

1. Em **PROJETO**, selecione **AEM Forms** e garantir que a assinatura apropriada seja selecionada para **Identidade de assinatura de código**, **Depurar**, **Versão** e **Qualquer SDK do iOS**.
1. Conectar um iPad provisionado a um computador Mac.
1. Selecione o dispositivo provisionado para o **AEM Forms** projeto.

   ![ipad](assets/ipad.png)

   Um dispositivo provisionado, iPad Air 2, é selecionado.

1. Selecionar **Produto** > **Limpar**.
1. Selecionar **Produto** > **Build**.

## Criar o instalador do aplicativo AEM Forms {#build-the-installer-for-the-mobile-workspace-app}

Você precisa arquivar o projeto Xcode para criar o instalador (um arquivo .ipa) e um arquivo de lista de propriedades (um arquivo .plist). O arquivo de lista de propriedades contém informações de configuração do aplicativo interno hospedado, como o nome e o local de hospedagem do aplicativo. Para obter mais informações sobre o arquivo de lista de propriedades, consulte [Sobre os Arquivos da Lista de Propriedades de Informações](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Conectar um iPad provisionado a um computador Mac. Para obter informações detalhadas sobre o provisionamento de uma iPad, consulte [Criação e download de perfis de provisionamento de desenvolvimento](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. Selecione o dispositivo provisionado para o **AEM Forms** projeto.

   ![ipad-1](assets/ipad-1.png)

   Um dispositivo provisionado, iPad Air 2, é selecionado.

1. Selecionar **Produto** > **Limpar**.
1. Selecionar **Produto** > **Build**.
1. Selecionar **Produto** > **Arquivar**.
1. No Organizer - Arquivos, selecione o arquivo mais recente do projeto e clique em **Distribuir**.
1. Selecionar **Salve para implantação corporativa ou ad-hoc** como o método de distribuição e clique em **Próxima**.
1. Selecione o apropriado **Identidade de assinatura de código** e clique em **Próxima**. Clique em **Permitir** para aplicar a assinatura.
1. Forneça o nome do aplicativo e selecione **Salvar para Distribuição Corporativa**.
1. Forneça o **URL do aplicativo** para o aplicativo. Por exemplo, para hospedar o aplicativo em um servidor CRX, forneça o URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. No **Título** especifique AEM Forms.
1. Clique em **Salvar** e feche o Xcode.

   Um arquivo do instalador, `AEM Forms.ipa`, e arquivo de lista de propriedades, `AEM Forms-info.plist`, são criados no local especificado.

1. Abra o `AEM Forms-info.plist` em um editor.
1. Substitua todos os espaços na URL do arquivo .ipa por %20.
1. Salve e feche o `AEM Forms-info.plist` arquivo.
