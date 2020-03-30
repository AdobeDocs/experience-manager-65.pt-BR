---
title: Configure o projeto Xcode e crie o aplicativo iOS
seo-title: Configure o projeto Xcode e crie o aplicativo iOS
description: Explica como criar um aplicativo AEM Forms padrão para iOS.
seo-description: Explica como criar um aplicativo AEM Forms padrão para iOS.
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configure o projeto Xcode e crie o aplicativo iOS{#set-up-the-xcode-project-and-build-the-ios-app}

O AEM Forms fornece o código fonte completo do aplicativo AEM Forms. A fonte contém todos os componentes para criar um aplicativo AEM Forms personalizado. O arquivo de código-fonte `adobe-lc-mobileworkspace-src-<version>.zip` é parte do `adobe-aemfd-forms-app-src-pkg-<version>.zip` pacote em compartilhamento de pacote.

Para obter a fonte do aplicativo AEM Forms, execute as seguintes etapas:

1. Navegue até package shareURL: `https://<server>:<port>/crx/packageshare`.

1. Baixe o pacote de origem. Quando você baixa o pacote, ele é adicionado ao gerenciador de pacote do AEM Forms.
1. Após o download, navegue até: `https://<server>:<port>/crx/packmgr/index.jsp`e instale `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

1. Para baixar o arquivo de código fonte, abra `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` no navegador.
O pacote de origem é baixado em seu dispositivo.

A imagem a seguir exibe o conteúdo extraído do `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

A tabela a seguir detalha o conteúdo da `adobe-lc-mobileworkspace-src-[version]/ios` pasta.

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
   <td><p>Recursos, plug-ins PhoneGap e o módulo principal do aplicativo</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms.xcodeproj</code></p> </td>
   <td><p>Projeto Xcode para aplicativo AEM Forms</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>HTML, CSS, imagens e arquivos JavaScript para o projeto do aplicativo AEM Forms</p> </td>
  </tr>
 </tbody>
</table>

Para obter informações detalhadas sobre a assinatura de código e a adição de dispositivos ao portal de provisionamento do iOS, consulte Configuração, processo e solução de problemas [da assinatura de código do](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html)iOS.

## Criar aplicativo AEM Forms padrão {#set-up-the-xcode-project}

1. Execute as seguintes etapas para configurar um projeto no Xcode e fornecer uma identidade de assinatura:

   Faça logon em sua máquina Mac que tenha o Xcode e o SDK do iOS instalados e configurados.

1. Copie o `adobe-lc-mobileworkspace-src-<version>.zip` arquivo da pasta de downloads para `[User_Home]/Projects/`.
1. Extraia o arquivo no `[User_Home]/Projects/[your-project]`diretório.
1. Navegue até o diretório do ` [User_Home]/Projects/ `[seu projeto]`/adobe-lc-mobileworkspace-src-[version]/ios` .
1. Abra o `AEM Forms.xcodeproj` projeto no Xcode.
1. Clique em **AEM Forms**, em **PÚBLICOS ALVOS**, selecione **AEM Forms**. Selecione a **guia Build Settings **guia, localize a seção **Code Signing Entitlement (Direitos de assinatura de código)** e, nos campos Debug e Release, execute um dos seguintes procedimentos:

   * Deixe os campos não especificados para criar um aplicativo padrão do Mobile Workspace
   * Especifique os campos como explicado em [Criar um aplicativo AEM Forms seguro para iOS](/help/forms/using/building-secure-mobile-workspace-app.md) para criar um aplicativo AEM Forms seguro.

1. Na guia **Build Settings (Configurações** de criação), clique em **All (Todos** ) e, em seguida, clique em **Combinado**.
1. Na lista **Configurações** , expanda Assinatura **de código**.
1. Para Identidade **de assinatura de** código, selecione a assinatura apropriada. Para obter informações detalhadas sobre como criar novas assinaturas, consulte [Criação e Download de Perfis](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)de Provisionamento de Desenvolvimento.
1. Certifique-se de que a mesma assinatura esteja selecionada para **Depurar**, **Liberar** e **Qualquer SDK** do iOS.
1. Substitua o seguinte código no `AEM Forms-info.plist` arquivo:

   ```java
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   com o seguinte, ao substituir `yourserver.com` por um nome de host apropriado para seu servidor.

   ```java
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
   >Essa etapa é necessária somente se o aplicativo AEM Forms precisar se conectar a um servidor que não siga os requisitos de segurança do App Transport.

1. Em **PROJECT**, selecione **AEM Forms** e certifique-se de que a assinatura apropriada esteja selecionada para Identidade **de assinatura de** código, **Depuração**, **Liberação** **** e Qualquer SDK do iOS.
1. Conecte um iPad provisionado a uma máquina Mac.
1. Selecione o dispositivo provisionado para o projeto do **AEM Forms** .

   ![ipad](assets/ipad.png)

   Um dispositivo provisionado, iPad Air 2, está selecionado.

1. Selecione **Produto** > **Limpar**.
1. Selecione **Produto** > **Criar**.

## Criar o instalador para o aplicativo AEM Forms {#build-the-installer-for-the-mobile-workspace-app}

É necessário arquivar o projeto Xcode para criar o instalador (um arquivo .ipa) e um arquivo de lista de propriedade (um arquivo .plist). O arquivo de lista de propriedade contém informações de configuração do aplicativo interno hospedado, como o nome e o local de hospedagem do aplicativo. Para obter mais informações sobre o arquivo de lista de propriedade, consulte [Sobre arquivos](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)de Lista de propriedades de informações.

1. Conecte um iPad provisionado a uma máquina Mac. Para obter informações detalhadas sobre o provisionamento de um iPad, consulte [Criação e download de Perfis de provisionamento de desenvolvimento](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. Selecione o dispositivo provisionado para o projeto do **AEM Forms** .

   ![ipad-1](assets/ipad-1.png)

   Um dispositivo provisionado, iPad Air 2, está selecionado.

1. Selecione **Produto** > **Limpar**.
1. Selecione **Produto** > **Criar**.
1. Selecione **Produto** > **Arquivo**.
1. No Organizer - Arquivos, selecione o arquivo mais recente do seu projeto e clique em **Distribuir**.
1. Selecione **Salvar para implantação** corporativa ou ad-hoc como o método de distribuição e clique em **Avançar**.
1. Selecione a Identidade **de assinatura de** código apropriada e clique em **Avançar**. Clique em **Permitir** para aplicar a assinatura.
1. Forneça o nome do aplicativo e selecione **Salvar para distribuição** corporativa.
1. Forneça o URL **do** aplicativo. Por exemplo, para hospedar o aplicativo em um servidor CRX, forneça o URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. No campo **Título** , especifique Formulários AEM.
1. Clique em **Salvar** e feche o Xcode.

   Um arquivo instalador `AEM Forms.ipa`e um arquivo de lista de propriedade `AEM Forms-info.plist`são criados no local especificado.

1. Abra o `AEM Forms-info.plist` arquivo em um editor.
1. Substitua todos os espaços no URL do arquivo .ipa por %20.
1. Salve e feche o `AEM Forms-info.plist` arquivo.