---
title: Instalar e configurar serviços de documento
seo-title: Installing and configuring document services
description: Instale os serviços de documento da AEM Forms para criar, montar, distribuir, arquivar documentos do PDF, adicionar assinaturas digitais para limitar o acesso a documentos e decodificar o Forms com códigos de barras.
seo-description: Install AEM Forms document services to create, assemble, distribute, archive PDF documents, add digital signatures to limit access to documents, and decode barcoded forms.
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
role: Admin
exl-id: 5d48e987-16c2-434b-8039-c82181d2e028
source-git-commit: 2d12f1652a3b8ec4e6ca9c737dc844d1f53f7d08
workflow-type: tm+mt
source-wordcount: '5365'
ht-degree: 1%

---

# Instalar e configurar serviços de documento {#installing-and-configuring-document-services}

A AEM Forms fornece um conjunto de serviços OSGi para realizar operações de nível de documento diferentes, por exemplo, serviços para criar, montar, distribuir e arquivar documentos do PDF, adicionar assinaturas digitais para limitar o acesso a documentos e decodificar o Forms com códigos de barras. Esses serviços estão incluídos no pacote complementar do AEM Forms. Coletivamente, esses serviços são conhecidos como serviços de documento. A lista de serviços de documento disponíveis e seus principais recursos é a seguinte:

* **Serviço de Assembler:** Permite combinar, reorganizar e aumentar documentos PDF e XDP e obter informações sobre documentos PDF. Também ajuda a converter e validar documentos PDF para o padrão PDF/A, transforma PDF forms, formulários XML e PDF forms para PDF/A-1b, PDF/A-2b e PDFA/A-3b. Para obter mais informações, consulte [Serviço de Assembler](/help/forms/using/assembler-service.md).

* **Serviço ConvertPDF:** Permite converter documentos do PDF em arquivos PostScript ou de imagem (JPEG, JPEG 2000, PNG e TIFF). Para obter mais informações, consulte [Serviço ConvertPDF](/help/forms/using/using-convertpdf-service.md).

* **Serviço Forms com código de barras:** Permite extrair dados de imagens eletrônicas de códigos de barras. O serviço aceita arquivos TIFF e PDF que incluem um ou mais códigos de barras como entrada e extrai os dados do código de barras. Para obter mais informações, consulte [Serviço Forms com código de barras](/help/forms/using/using-barcoded-forms-service.md).

* **Serviço DocAssurance:** Permite criptografar e descriptografar documentos, estender a funcionalidade do Adobe Reader com direitos de uso adicionais e adicionar assinaturas digitais aos documentos. O serviço de garantia de documentos contém três serviços: assinatura, criptografia e extensão do leitor. Para obter mais informações, consulte [Serviço DocAssurance](/help/forms/using/overview-aem-document-services.md).

* **Serviço de criptografia:** Permite criptografar e descriptografar documentos. Quando um documento é criptografado, seu conteúdo se torna ilegível. Um usuário autorizado pode descriptografar o documento para obter acesso a seu conteúdo. Para obter mais informações, consulte [Serviço de criptografia](/help/forms/using/overview-aem-document-services.md#encryption-service).

* **Serviço Forms:** Permite criar aplicativos clientes interativos de captura de dados que validam, processam, transformam e entregam formulários normalmente criados no Forms Designer. O serviço Forms renderiza qualquer design de formulário desenvolvido para documentos do PDF. Para obter mais informações, consulte [Serviço Forms](/help/forms/using/forms-service.md).

* **Serviço de saída:** Permite criar documentos em diferentes formatos, incluindo PDF, formatos de impressora laser e formatos de impressora de etiquetas. Os formatos de impressora a laser são PostScript e PCL (Printer Control Language). Para obter mais informações, consulte [Serviço de saída](/help/forms/using/output-service.md).

* **Serviço PDF Generator:** O serviço PDF Generator fornece APIs para converter formatos de arquivo nativos em PDF. Também converte o PDF em outros formatos de arquivo e otimiza o tamanho dos documentos do PDF. Para obter mais informações, consulte [Serviço PDF Generator](aem-document-services-programmatically.md#pdfgeneratorservice).

* **Serviço de extensão do Reader:** Permite que sua organização compartilhe facilmente documentos interativos do PDF, estendendo a funcionalidade do Adobe Reader com direitos de uso adicionais. O serviço ativa recursos que não estão disponíveis quando um documento do PDF é aberto usando o Adobe Reader, como adicionar comentários a um documento, preencher formulários e salvar o documento. Para obter mais informações, consulte [Serviço de extensão do Reader](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **Serviço de assinatura:** Permite que você trabalhe com assinaturas digitais e documentos no servidor AEM. Por exemplo, o serviço de assinatura é normalmente usado nas seguintes situações:

   * O servidor de AEM certifica um formulário antes de ele ser enviado a um usuário para ser aberto usando o Acrobat ou o Adobe Reader.
   * O servidor de AEM valida uma assinatura que foi adicionada a um formulário usando o Acrobat ou o Adobe Reader.
   * O servidor AEM assina um formulário em nome de um notário público.

   O serviço de assinatura acessa certificados e credenciais armazenadas no armazenamento de confiança. Para obter mais informações, consulte [Serviço de assinatura](/help/forms/using/aem-document-services-programmatically.md).

A AEM Forms é uma plataforma corporativa poderosa e os serviços de documento são apenas um dos recursos da AEM Forms. Para obter a lista completa de recursos, consulte [Introdução ao AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologia de implantação {#deployment-topology}

O pacote do complemento AEM Forms é um aplicativo implantado em AEM. Geralmente, é necessário apenas uma instância AEM (autor ou publicação) para executar os serviços de documento da AEM Forms. A topologia a seguir é recomendada para executar os serviços de documento da AEM Forms. Para obter informações detalhadas sobre topologias, consulte [Topologias de arquitetura e implantação do AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![Topologias de arquitetura e implantação do AEM Forms](do-not-localize/document-services.png)

>[!NOTE]
>
>Embora o AEM Forms permita configurar e executar todas as funcionalidades de um único servidor, você deve fazer o planejamento da capacidade, o balanceamento de carga e configurar servidores dedicados para recursos específicos em um ambiente de produção. Por exemplo, para um ambiente que usa o serviço Gerador de PDF para converter milhares de páginas por dia e vários formulários adaptáveis para capturar dados, configure servidores AEM Forms separados para o serviço Gerador de PDF e recursos de formulários adaptáveis. Ele ajuda a fornecer desempenho ideal e dimensionar os servidores independentemente uns dos outros.

## Requisitos do sistema {#system-requirements}

Antes de começar a instalar e configurar os serviços de documento da AEM Forms, verifique se:

* A infraestrutura de hardware e software está em vigor. Para obter uma lista detalhada de hardware e software suportados, consulte [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

* O caminho de instalação da instância de AEM não contém espaços em branco.
* Uma instância de AEM está em execução. Na terminologia AEM, uma &quot;instância&quot; é uma cópia do AEM em execução em um servidor no modo de criação ou publicação. Geralmente, é necessário apenas uma instância AEM (autor ou publicação) para executar os serviços de documento da AEM Forms:

   * **Autor**: Uma instância AEM usada para criar, carregar e editar conteúdo e administrar o site. Quando o conteúdo estiver pronto para entrar em funcionamento, ele será replicado para a instância de publicação.
   * **Publicar**: Uma instância de AEM que disponibiliza o conteúdo publicado ao público pela Internet ou por uma rede interna.

* Os requisitos de memória são cumpridos. O pacote do complemento AEM Forms requer:

   * 15 GB de espaço temporário para instalações baseadas no Microsoft® Windows.
   * 6 GB de espaço temporário para instalações baseadas em UNIX.

* O software cliente necessário para que o gerador de PDF execute a conversão no Microsoft® Windows e Linux® está instalado:

   * **Microsoft® Windows**: Instalar [Microsoft® Office](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p) ou [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux®**: Instalar [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* No Microsoft® Windows, o PDF Generator oferece suporte às rotas de conversão WebKit, Acrobat WebCapture e PhantomJS para converter arquivos HTML em documentos PDF.
>* Em sistemas operacionais baseados em UNIX, o PDF Generator oferece suporte a rotas de conversão WebKit e PhantomJS para converter arquivos HTML em documentos PDF.
>


### Requisitos adicionais para o sistema operacional baseado em UNIX {#extrarequirements}

Se você estiver usando o sistema operacional baseado em UNIX, instale os seguintes pacotes da mídia de instalação do respectivo sistema operacional:

<table>
 <tbody>
  <tr>
   <td>
    <ul>
     <li>expatriado</li>
    </ul> </td>
   <td>
    <ul>
     <li>libxcb</li>
    </ul> </td>
   <td>
    <ul>
     <li>freetype</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXau</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libSM</li>
    </ul> </td>
   <td>
    <ul>
     <li>zlib</li>
    </ul> </td>
   <td>
    <ul>
     <li>libICE</li>
    </ul> </td>
   <td>
    <ul>
     <li>libuuid</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>glibc</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXext</li>
    </ul> </td>
   <td>
    <ul>
     <li>nss-softokn-freebl</li>
    </ul> </td>
   <td>
    <ul>
     <li>fontconfig</li>
    </ul> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li>libX11</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrender</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXrandr</li>
    </ul> </td>
   <td>
    <ul>
     <li>libXinerama</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

* **(Somente PDF Generator**) Instale a versão de 32 bits das bibliotecas libcurl, libcrypto e libssl e crie os links simbólicos abaixo. Os links simbólicos apontam para a versão mais recente das respectivas bibliotecas:

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(Somente PDF Generator)** O serviço PDF Generator oferece suporte às rotas WebKit e PhantomJS para converter arquivos HTML para documentos PDF. Para habilitar a conversão para a rota PhantomJS, instale as bibliotecas de 64 bits listadas abaixo. Geralmente, essas bibliotecas já estão instaladas. Se alguma biblioteca estiver ausente, instale-a manualmente:

   * linux-gate.so.1
   * libz.so.1
   * libfontconfig.so.1
   * libfreetype.so.6
   * libdl.so.2
   * librt.so.1
   * libpthread.so.0
   * libstdc++.so.6
   * libm.so.6
   * libgcc_s.so.1
   * libc.so.6
   * ld-linux.so.2
   * libexpat.so.1

## Configurações de pré-instalação {#preinstallationconfigurations}

As configurações listadas na seção de configurações de pré-instalação são aplicáveis somente ao serviço PDF Generator. Se você não estiver configurando o serviço PDF Generator, ignore a seção de configuração de pré-instalação.

### Instalar o Adobe Acrobat e aplicativos de terceiros {#install-adobe-acrobat-and-third-party-applications}

Se você for usar o serviço PDF Generator para converter formatos de arquivo nativos, como Microsoft® Word, Microsoft® Excel, Microsoft® PowerPoint, OpenOffice, WordPerfect X7 e Adobe Acrobat em documentos PDF, certifique-se de que esses aplicativos estejam instalados no AEM Forms Server.

>[!NOTE]
>
>* Se o servidor AEM Forms estiver em um ambiente offline ou seguro e a Internet não estiver disponível para ativar o Adobe Acrobat, consulte [Ativação offline](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en) para obter instruções sobre como ativar essas instâncias do Adobe Acrobat.
>* Adobe Acrobat, Microsoft® Word, Excel e Powerpoint estão disponíveis apenas para Microsoft® Windows. Se você estiver usando o sistema operacional baseado em UNIX, instale o OpenOffice para converter arquivos de rich text e arquivos Microsoft® Office suportados em documentos PDF.
>* Ignore todas as caixas de diálogo exibidas após instalar o Adobe Acrobat e software de terceiros para todos os usuários configurados para usar o serviço Gerador de PDF.
>* Inicie todo o software instalado pelo menos uma vez. Descarte todas as caixas de diálogo para todos os usuários configurados para usar o serviço PDF Generator.
>* [Verifique a data de expiração dos números de série do Adobe Acrobat](https://helpx.adobe.com/enterprise/kb/volume-license-expiration-check.html) e defina uma data para atualizar a licença ou [migrar seu número de série](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) com base no prazo de validade.


Depois de instalar o Acrobat, abra o Microsoft® Word. No **Acrobat** clique em **Criar PDF** e converta um arquivo .doc ou .docx disponível em sua máquina em um documento do PDF. Se a conversão for bem-sucedida, o AEM Forms estará pronto para usar o Acrobat com o serviço PDF Generator.

### Configurar variáveis de ambiente {#setup-environment-variables}

Defina variáveis de ambiente para o Java Development Kit de 32 e 64 bits, aplicativos de terceiros e Adobe Acrobat. As variáveis de ambiente devem conter o caminho absoluto do executável usado para iniciar o aplicativo correspondente, por exemplo, a tabela abaixo lista as variáveis de ambiente para alguns aplicativos:

<table>
 <tbody>
  <tr>
   <td><p><strong>Aplicativo</strong></p> </td>
   <td><p><strong>Variável de ambiente</strong></p> </td>
   <td><p><strong>Exemplo</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>JDK (64 bits)</strong></p> </td>
   <td><p>JAVA_HOME</p> </td>
   <td><p>C:\Program Files\Java\jdk1.8.0_74</p> </td>
  </tr>
  <tr>
   <td><p><strong>Adobe Acrobat</strong></p> </td>
   <td><p>Acrobat_PATH</p> </td>
   <td><p>C:\Program Files (x86)\Adobe\Acrobat 2015\Acrobat\Acrobat.exe</p> </td>
  </tr>
  <tr>
   <td><p><strong>Bloco de notas</strong></p> </td>
   <td><p>Notepad_PATH</p> </td>
   <td><p>C:\WINDOWS\notepad.exe<br /> <strong></strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>OpenOffice</strong></p> </td>
   <td><p>OpenOffice_PATH</p> </td>
   <td><p>C:\Program Files (x86)\OpenOffice.org4</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Todas as variáveis de ambiente e os respectivos caminhos fazem distinção entre maiúsculas e minúsculas.
>* JAVA_HOME, JAVA_HOME_32 e Acrobat_PATH (somente Windows) são variáveis de ambiente obrigatórias.
>* A variável de ambiente OpenOffice_PATH é definida como a pasta de instalação em vez do caminho para o executável.
>* Não configure variáveis de ambiente para aplicativos do Microsoft® Office, como Word, PowerPoint, Excel e Projeto, ou para AutoCAD. Se esses aplicativos estiverem instalados no servidor, o serviço Gerar PDF inicia automaticamente esses aplicativos.
>* Em plataformas baseadas em UNIX, instale o OpenOffice como /root. Se o OpenOffice não estiver instalado como raiz, o serviço PDF Generator não converterá documentos OpenOffice em documentos PDF. Se for necessário instalar e executar o OpenOffice como um usuário não raiz, forneça direitos sudo ao usuário não raiz.
>* Se você estiver usando o OpenOffice em uma plataforma baseada em UNIX, execute o seguinte comando para definir a variável de caminho:
>
> `export OpenOffice_PATH=/opt/openoffice.org4`

### (Somente para IBM® WebSphere®) Configurar o provedor de soquete SSL IBM® {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

Execute as seguintes etapas para configurar o provedor de soquete SSL IBM®:

1. Crie uma cópia do arquivo java.security. O local padrão do arquivo é `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`.
1. Abra o arquivo java.security copiado para edição.
1. Altere as fábricas de soquete SSL padrão para usar as fábricas JSSE2 em vez das fábricas padrão IBM® WebSphere®:

   **Conteúdo padrão:**

   ```shell
   #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   #WebSphere socket factories (in cryptosf.jar)
   ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

   **Conteúdo modificado:**

   ```shell
   ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
   ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
   
   #WebSphere socket factories (in cryptosf.jar)
   #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
   #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
   ```

1. Para permitir que o AEM Forms Server use o arquivo java.security atualizado, enquanto inicia o servidor AEM Forms, adicione o seguinte argumento java:

   `-Djava.security.properties= [path of newly created Java.security file].`

### (Somente para Windows) Configurar o serviço Instalar Tinta e Manuscrito {#configure-install-ink-and-handwriting-service}

Se você estiver executando o Microsoft® Windows Server, configure o serviço de Tinta e Manuscrito. O serviço é necessário para abrir arquivos Microsoft® PowerPoint que usam recursos de vinculação do Microsoft® Office:

1. Abra o Gerenciador de Servidores. Clique no botão **[!UICONTROL Gerenciador do servidor]** ícone na bandeja do Quick Launch.
1. Clique em **[!UICONTROL Adicionar recursos]** no **[!UICONTROL Recursos]** menu. Selecione o **[!UICONTROL Serviços de escrita manual e de tinta]** caixa de seleção.
1. **[!UICONTROL Selecionar recursos]** caixa de diálogo com **[!UICONTROL Serviços de escrita manual e de tinta]** selecionado. Clique em **[!UICONTROL Instalar]** e o serviço está instalado.

### (Somente Windows) Definir as configurações de bloco de arquivos para o Microsoft® Office {#configure-the-file-block-settings-for-microsoft-office}

Altere as configurações do centro de confiança do Microsoft® Office para habilitar o serviço Gerador de PDF para converter arquivos criados com versões mais antigas do Microsoft® Office.

1. Abra um aplicativo do Microsoft® Office. Por exemplo, Microsoft® Word. Navegar para **[!UICONTROL Arquivo]**> **[!UICONTROL Opções]**. A caixa de diálogo opções é exibida.

1. Clique em **[!UICONTROL Central de confiança]** e clique em **[!UICONTROL Configurações da Central de Confiança]**.
1. No **[!UICONTROL Configurações do Centro de Confiança]**, clique em **[!UICONTROL Configurações de bloco de arquivo]**.
1. No **[!UICONTROL Tipo de arquivo]** lista, desmarque **[!UICONTROL Abrir]** para o tipo de arquivo que o serviço PDF Generator deve ter permissão para converter em documentos PDF.

### (Somente Windows) Conceder o privilégio Substituir um token de nível de processo {#grant-the-replace-a-process-level-token-privilege}

A conta de usuário usada para iniciar o servidor de aplicativos requer o **Substituir um token de nível de processo** privilégio. A conta do sistema local tem a variável **Substituir um token de nível de processo** privilégio por padrão. Para os servidores em execução com um usuário do grupo Administradores locais, o privilégio deve ser concedido explicitamente. Execute as seguintes etapas para conceder o privilégio:

1. Abra o Editor de políticas de grupo para Microsoft® Windows. Para abrir o Editor de Política de Grupo, clique em **[!UICONTROL Iniciar]**, tipo **gpedit.msc** na caixa Iniciar pesquisa e clique em **[!UICONTROL Editor de Política de Grupo]**.
1. Navegar para **[!UICONTROL Política de Computador Local]** > **[!UICONTROL Configuração do computador]** > **[!UICONTROL Configurações do Windows]** > **[!UICONTROL Configurações de segurança]** > **[!UICONTROL Políticas locais]** > **[!UICONTROL Atribuição de direitos de usuário]** e edite o **[!UICONTROL Substituir um token de nível de processo]** e inclua o grupo Administradores .
1. Adicione o usuário à entrada Substituir um token de nível de processo .

### (Somente Windows) Ativar o serviço PDF Generator para não administradores {#enable-the-pdf-generator-service-for-non-administrators}

Você pode ativar um usuário que não seja administrador para usar o serviço Gerador de PDF. Normalmente, somente os usuários com privilégios administrativos podem usar o serviço:

1. Crie uma variável de ambiente, PDFG_NON_ADMIN_ENABLED.
1. Defina o valor da variável de ambiente como TRUE.
1. Reinicie a instância do AEM Forms.

### (Somente Windows) Desativar Controle de Conta de Usuário (UAC) {#disable-user-account-control-uac}

1. Para acessar o Utilitário de configuração do sistema, acesse **[!UICONTROL Iniciar > Executar]** e então insira **[!UICONTROL MSCONFIG]**.
1. Clique no botão **[!UICONTROL Ferramentas]** e role para baixo e selecione **[!UICONTROL Alterar configurações de UAC]**. Clique em **[!UICONTROL Launch]** para executar o comando em uma nova janela.
1. Ajuste o controle deslizante para o nível Nunca notificar . Quando terminar, feche a janela de comando e feche a janela Configuração do sistema.
1. Verifique se a configuração do Registro para UAC está definida como 0 (zero). Execute as seguintes etapas para verificar:

   1. A Microsoft® recomenda fazer backup do registro antes de modificá-lo. Para obter etapas detalhadas, consulte [Como fazer backup e restaurar o registro no Windows](https://support.microsoft.com/en-us/help/322756).
   1. Abra o editor de Registro do Microsoft® Windows. Para abrir o editor do registro, vá para Iniciar > Executar, digite regedit e clique em OK.
   1. Vá até `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Verifique se o valor de EnableLUA está definido como 0 (zero).
   1. Garanta o valor de **EnableLUA** é definido como 0 (zero). Se o valor não for 0, altere o valor para 0. Feche o editor de Registro.

1. Reinicie o computador.

### (Somente Windows) Desativar o serviço de Relatório de Erros {#disable-error-reporting-service}

Ao converter um documento em PDF usando o serviço PDF Generator no Windows Server, ocasionalmente, o Windows Server relata que o executável encontrou um problema e deve fechar. No entanto, não afeta a conversão do PDF, pois continua em segundo plano.

Para evitar receber o erro, você pode desativar o relatório de erros do Windows. Para obter mais informações sobre como desativar o relatório de erros, consulte [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### (Somente Windows) Configurar conversão de HTML para PDF {#configure-html-to-pdf-conversion}

O serviço PDF Generator fornece rotas ou métodos WebKit, WebCapture e PhantomJS para converter arquivos HTML em documentos PDF. No Windows, para ativar a conversão para rotas WebKit e Acrobat WebCapture, copie a fonte Unicode para o diretório %windir%\fonts.

>[!NOTE]
>
>Sempre que instalar novas fontes na pasta de fontes, reinicie a instância do AEM Forms.

### (Somente plataformas baseadas em UNIX) Configurações adicionais para conversão de HTML para PDF  {#extra-configurations-for-html-to-pdf-conversion}

Em plataformas baseadas em UNIX, o serviço PDF Generator oferece suporte às rotas WebKit e PhantomJS para converter arquivos HTML em documentos PDF. Para habilitar a conversão de HTML para PDF, execute as seguintes configurações, aplicáveis à rota de conversão preferencial:

### (Somente plataformas baseadas em UNIX) Ativar suporte para fontes Unicode (somente WebKit) {#enable-support-for-unicode-fonts-webkit-only}

Copie a fonte Unicode em qualquer um dos seguintes diretórios, conforme apropriado para seu sistema:

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType (Solaris™)

>[!NOTE]
>
>* No Red Hat® Enterprise Linux® 6.x e posterior, as fontes da courier não estão disponíveis. Para instalar as fontes da courier, baixe o arquivo font-ibm-type1-1.0.3.zip. Extraia o arquivo em /usr/share/fonts. Crie um link simbólico de /usr/share/X11/fonts para /usr/share/fonts.
>* Exclua todos os arquivos de cache de fonte .list dos diretórios Html2PdfSvc/bin e /usr/share/fonts.
>* Verifique se os diretórios /usr/lib/X11/fonts e /usr/share/fonts existem. Se os diretórios não existirem, use o comando ln para criar um link simbólico de /usr/share/X11/fonts para /usr/lib/X11/fonts e outro link simbólico de /usr/share/fonts para /usr/share/X11/fonts. Além disso, verifique se as fontes da courier estão disponíveis em /usr/lib/X11/fonts.
>* Certifique-se de que todas as fontes (Unicode e não unicode) estejam disponíveis no diretório /usr/share/fonts ou /usr/share/X11/fonts.
>* Ao executar o serviço PDF Generator como um usuário não raiz, forneça ao usuário não raiz acesso de leitura e gravação a todos os diretórios de fonte.
>* Sempre que instalar novas fontes na pasta de fontes, reinicie a instância do AEM Forms.
>


## Instalar o pacote complementar do AEM Forms {#install-aem-forms-add-on-package}

O pacote do complemento AEM Forms é um aplicativo implantado em AEM. O pacote contém os Serviços de documento da AEM Forms e outros recursos da AEM Forms. Execute as seguintes etapas para instalar o pacote:

1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
1. Clique em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. No **[!UICONTROL Filtros]** seção:
   1. Selecionar **[!UICONTROL Forms]** do **[!UICONTROL Solução]** lista suspensa.
   2. Selecione a versão e o tipo do pacote. Também é possível usar a variável **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Toque no nome do pacote aplicável ao seu sistema operacional e selecione **[!UICONTROL Aceitar termos do EULA]** e toque em **[!UICONTROL Baixar]**.
1. Abra [Gerenciador de pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=pt-BR) e clique em **[!UICONTROL Fazer upload de pacote]** para fazer upload do pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

   Também é possível baixar o pacote por meio do link direto listado no [Versões do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) artigo 10. o

1. Depois que o pacote for instalado, você será solicitado a reiniciar a instância do AEM. **Não pare imediatamente o servidor.** Antes de parar o AEM Forms Server, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no `[AEM-Installation-Directory]/crx-quickstart/logs/error`Arquivo .log e o log é estável.

## Configurações pós-instalação {#post-installation-configurations}

### Configurar delegação de inicialização para bibliotecas RSA/BouncyCastle  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. Pare a instância de AEM. Navegue até o [AEM diretório de instalação]\crx-quickstart\conf\ folder. Abra o arquivo sling.properties para edição.

   Se você usar `[AEM installation directory]\crx-quickstart\bin\start.bat` para iniciar uma instância AEM, edite o sling.properties localizado em `[AEM_root]\crx-quickstart\`.

1. Adicione as seguintes propriedades ao arquivo sling.properties :

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. (Somente para AIX®) Adicione as seguintes propriedades ao arquivo sling.properties :

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. Salve e feche o arquivo.

### Configuração do serviço gerenciador de fontes  {#configuring-the-font-manager-service}

1. Faça logon em [Gerenciador de configuração de AEM](http://localhost:4502/system/console/configMgr) como administrador.
1. Localize e abra o **[!UICONTROL Gerentes de Fontes CQ-DAM-Handler-Gibson]** serviço. Especifique o caminho dos diretórios Fontes do sistema, Fontes do servidor do Adobe e Fontes do cliente. Clique em **[!UICONTROL Salvar]**.

   >[!NOTE]
   >
   >O seu direito de usar fontes fornecidas por outras partes que não o Adobe é regido pelos contratos de licença fornecidos por essas partes com essas fontes, e não é coberto pela licença de uso de software Adobe. O Adobe recomenda que você verifique e garanta que está em conformidade com todos os contratos de licença não-Adobe aplicáveis antes de usar fontes não-Adobe com o software Adobe, especialmente no que diz respeito ao uso de fontes em um ambiente de servidor.
   > Ao instalar novas fontes na pasta de fontes, reinicie a instância do AEM Forms.

### Configurar uma conta de usuário local para executar o serviço Gerador de PDF  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

Uma conta de usuário local é necessária para executar o serviço PDF Generator. Para obter etapas para criar um usuário local, consulte [Criar uma conta de usuário no Windows](https://support.microsoft.com/en-us/help/13951/windows-create-user-account) ou criar uma conta de usuário em plataformas baseadas em UNIX.

1. Abra o [Configuração do Gerador de PDF AEM Forms](http://localhost:4502/libs/fd/pdfg/config/ui.html) página.

1. No **[!UICONTROL Contas de usuário]** , forneça as credenciais de uma conta de usuário local e clique em **[!UICONTROL Enviar]**. Se o Microsoft® Windows for solicitado, permita acesso ao usuário. Quando adicionado com êxito, o usuário configurado é exibido sob a variável **[!UICONTROL Suas contas de usuário]** na seção **[!UICONTROL Contas de usuário]** guia .

### Definir as configurações de tempo limite {#configure-the-time-out-settings}

1. Em [Gerenciador de configuração de AEM](http://localhost:4502/system/console/configMgr), localize e abra o **[!UICONTROL Provedor Jacorb ORB]** serviço.

   Adicione o seguinte ao **[!UICONTROL Custom Properties.name]** e clique em **[!UICONTROL Salvar]**. Ele define o tempo limite de resposta pendente (também conhecido como tempo limite do cliente CORBA) como 600 segundos.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. Faça logon na instância do autor do AEM e navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Ferramentas]** > **[!UICONTROL Forms]** > **[!UICONTROL Configurar gerador de PDF]**. O URL padrão é <http://localhost:4502/libs/fd/pdfg/config/ui.html>.

   Abra o **[!UICONTROL Configuração geral]** e modifique o valor dos seguintes campos para seu ambiente:

<table>
 <tbody>
  <tr>
   <td>Texto</td>
   <td>Descrição</td>
   <td>Valor padrão</td>
  </tr>
  <tr>
   <td>Tempo limite da conversão do servidor</td>
   <td>Uma conversão de PDFG permanece ativa pelo número de segundos definido no tempo limite de conversão do servidor</td>
   <td>270 segundos<br /> </td>
  </tr>
  <tr>
   <td>Segundos para exploração de limpeza do PDFG</td>
   <td>O número de segundos necessários para executar operações pós-conversão.<br /> </td>
   <td>3600 segundos</td>
  </tr>
  <tr>
   <td>Segundos para expiração da tarefa</td>
   <td>Duração para a qual o serviço PDF Generator tem permissão para executar uma conversão. Verifique se o valor de Segundos da Expiração do Trabalho é maior que o valor de Segundos da Verificação de Limpeza de PDFG.</td>
   <td>7200 segundos</td>
  </tr>
 </tbody>
</table>

### (Somente Windows) Configurar o Acrobat para o serviço Gerador de PDF {#configure-acrobat-for-the-pdf-generator-service}

No Microsoft® Windows, o serviço Gerador de PDF usa o Adobe Acrobat para converter os formatos de arquivo suportados em um documento PDF. Execute as seguintes etapas para configurar o Adobe Acrobat para o serviço Gerador de PDF:

1. Abra o Acrobat e selecione **[!UICONTROL Editar]**> **[!UICONTROL Preferências]**> **[!UICONTROL Atualizador]**. Em Verificar atualizações, desmarque **[!UICONTROL Instalar atualizações automaticamente]** e clique em **[!UICONTROL OK]**. Feche o Acrobat.
1. Clique duas vezes em um documento PDF no seu sistema. Quando o Acrobat é iniciado pela primeira vez, as caixas de diálogo para Início de sessão, Tela de boas-vindas e EULA são exibidas. Descarte essas caixas de diálogo para todos os usuários configurados para usar o PDF Generator.
1. Execute o arquivo em lote do utilitário PDF Generator para configurar o Acrobat para o serviço PDF Generator:

   1. Abrir [Gerenciador de pacotes de AEM](http://localhost:4502/crx/packmgr/index.jsp) e faça o download do `adobe-aemfd-pdfg-common-pkg-[version].zip` do Gerenciador de Pacotes.
   1. Descompacte o arquivo .zip baixado. Abra o prompt de comando com privilégios administrativos.
   1. Navegue até o [arquivo zip extraído]`\jcr_root\etc\packages\day\cq60\fd\adobe-aemds-common-pkg-[version]\jcr_root\etc\packages\day\cq60\fd\adobe-aemfd-pdfg-common-pkg-[version]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]` diretório. Execute o seguinte arquivo em lote:

      `Acrobat_for_PDFG_Configuration.bat`

      O Acrobat está configurado para ser executado com o serviço Gerador de PDF.

1. Executar [Ferramenta de disponibilidade do sistema (SRT)](#SRT) para validar a instalação do Acrobat.

### (Somente Windows) Configurar a rota primária para conversão de HTML para PDF {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

O serviço PDF Generator fornece várias rotas para converter arquivos HTML para documentos PDF: Webkit, Acrobat WebCapture (somente Windows) e PhantomJS. O Adobe recomenda o uso da rota PhantomJS porque ela tem a capacidade de lidar com conteúdo dinâmico e não tem dependências em bibliotecas de 32 bits, JDK de 32 bits ou não requer fontes extras. Além disso, a rota PhantomJS não requer acesso sudo ou raiz para executar a conversão.

A rota principal padrão para conversão de HTML para PDF é o Webkit. Para alterar a rota de conversão:

1. Em AEM instância do autor, navegue até **[!UICONTROL Ferramentas]**> **[!UICONTROL Forms]**> **[!UICONTROL Configurar gerador de PDF]**.

1. No **[!UICONTROL Configuração geral]** selecione a rota de conversão preferencial na guia **[!UICONTROL Rota primária para conversões de HTML para PDF]** lista suspensa.

### Inicializar Armazenamento de Confiança Global {#intialize-global-trust-store}

Usando o Gerenciamento de armazenamento de confiança, você pode importar, editar e excluir certificados confiáveis no servidor para a validação de assinaturas digitais e autenticação de certificado. É possível importar e exportar qualquer número de certificados. Depois que um certificado é importado, você pode editar as configurações de confiança e o tipo de armazenamento de confiança. Execute as seguintes etapas para inicializar um armazenamento de confiança:

1. Faça logon na instância do AEM Forms como administrador.
1. Ir para  **[!UICONTROL Ferramentas]** >  **[!UICONTROL Segurança]** >  **[!UICONTROL Armazenamento de confiança]**.
1. Clique em  **[!UICONTROL Criar TrustStore]**. Definir senha e tocar **[!UICONTROL Salvar]**.

### Configurar certificados para extensão Reader e serviço de criptografia {#set-up-certificates-for-reader-extension-and-encryption-service}

O serviço DocAssurance pode aplicar direitos de utilização a documentos PDF. Para aplicar direitos de uso a documentos do PDF, configure os certificados.

Antes de configurar os certificados, verifique se você tem um:

* Arquivo de certificado (.pfx).

* Senha da chave privada fornecida com o certificado.

* Alias da chave de privacidade. Você pode executar o comando keytool do Java para exibir o Alias da chave privada:
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* Senha do arquivo de armazenamento de chaves. Se você estiver usando o certificado de extensões do Reader, a senha do arquivo de armazenamento de chaves será sempre a mesma da senha da chave privada.

Execute as seguintes etapas para configurar os certificados:

1. Faça logon na instância do AEM Author como administrador. Ir para **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.
1. Clique no botão **[!UICONTROL name]** do campo da conta do usuário. O **[!UICONTROL Editar configurações de usuário]** será aberta. Na instância do autor do AEM, os certificados residem em um KeyStore. Se você não criou um KeyStore anteriormente, clique em **[!UICONTROL Criar KeyStore]** e defina uma nova senha para o KeyStore. Se o servidor já tiver um KeyStore, pule esta etapa.  Se você estiver usando o certificado de extensões do Reader, a senha do arquivo de armazenamento de chaves será sempre a mesma da senha da chave privada.
1. No **[!UICONTROL Editar configurações de usuário]** selecione o **[!UICONTROL KeyStore]** guia . Expanda o **[!UICONTROL Adicionar chave privada do arquivo de armazenamento de chaves]** e forneça um alias. O alias é usado para executar a operação Reader Extensions .
1. Para fazer upload do arquivo de certificado, clique em **[!UICONTROL Selecionar arquivo de armazenamento de chaves]** e fazer upload de um &lt;filename>Arquivo .pfx.

   Adicione o **[!UICONTROL Senha do Armazenamento de Chaves]**, **[!UICONTROL Senha da chave privada]** e **[!UICONTROL Alias da chave privada]** que está associada ao certificado aos respectivos campos. Clique em **[!UICONTROL Enviar]**.

   >[!NOTE]
   >
   >No ambiente de produção, substitua suas credenciais de avaliação por credenciais de produção. Certifique-se de excluir suas credenciais antigas das extensões do Reader antes de atualizar uma credencial expirada ou de avaliações.

1. Clique em **[!UICONTROL Salvar e fechar]** no **[!UICONTROL Editar configurações de usuário]** página.

### Ativar AES-256 {#enable-aes}

Para usar a criptografia AES 256 para arquivos PDF, obtenha e instale os arquivos da Política de Competência de Força Ilimitada da Extensão de Criptografia Java (JCE). Substitua os arquivos local_policy.jar e US_export_policy.jar na pasta jre/lib/security. Por exemplo, se você estiver usando o Sun JDK, copie os arquivos baixados para o `[JAVA_HOME]/jre/lib/security` pasta.

O serviço Assembler depende do serviço Reader Extensions, do serviço Signature, do serviço Forms e do serviço Output. Execute as seguintes etapas para verificar se os serviços necessários estão funcionando:

1. Fazer logon no URL `https://'[server]:[port]'/system/console/bundles` como administrador.
1. Pesquise o seguinte serviço e verifique se os serviços estão ativos e em execução:

<table>
 <tbody>
  <tr>
   <th>Nome do serviço</th>
   <th>Nome do pacote</th>
  </tr>
  <tr>
   <td>Serviço de assinaturas</td>
   <td>adobe-aemfd-assinaturas</td>
  </tr>
  <tr>
   <td>Serviço de extensões do Reader</td>
   <td>com.adobe.aemfd.adobe-aemfd-readerextensions<br /> </td>
  </tr>
  <tr>
   <td>Serviço do Forms</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector<br /> </td>
  </tr>
  <tr>
   <td>Serviço de saída</td>
   <td>com.adobe.livecycle.adobe-lc-forms-bedrock-connector</td>
  </tr>
 </tbody>
</table>

## Problemas conhecidos e solução de problemas {#known-issues-and-troubleshooting}

* A conversão HTML para PDF falha se um arquivo de entrada zipado contiver arquivos HTML com caracteres de byte duplo em nomes de arquivo. Para evitar esse problema, não use caracteres de byte duplo ao nomear arquivos HTML.

* Em sistemas operacionais baseados em UNIX, faça o seguinte para encontrar as bibliotecas ausentes:

1. Vá até `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. Execute o seguinte comando para listar todas as bibliotecas necessárias para a conversão do PhantomJS em PDF.

   `ldd phantomjs`

   Execute o seguinte comando para listar bibliotecas ausentes.

   `ldd phantomjs | grep not`

1. Instale manualmente as bibliotecas ausentes.

## Ferramenta de disponibilidade do sistema (SRT) {#SRT}

A ferramenta System Readiness verifica se o computador está configurado corretamente para executar conversões PDF Generator. A ferramenta gera um relatório no caminho especificado. Para executar a ferramenta:

1. Abra o prompt de comando. Navegue até o `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools` pasta.

1. Execute o seguinte comando no prompt de comando:

   `java -jar forms-srt-[version].jar [Path_of_reports_folder] en`

   O comando gera o relatório e também cria o arquivo srt_config.yaml.

   >[!NOTE]
   >
   > * Se a Ferramenta de disponibilidade do sistema relatar que o arquivo pdfgen.api não está disponível na pasta de plug-ins do Acrobat, copie o arquivo pdfgen.api do `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]\plugins\x86_win32` para `[Acrobat_root]\Acrobat\plug_ins` diretório.
   >
   > * Você pode usar o arquivo srt_config.yaml para definir várias configurações de . O formato do arquivo é:


   ```
      # =================================================================
      # SRT Configuration
      # =================================================================
      #Note - follow correct format to avoid parsing failures
      #e.g. <param name>:<space><param value> 
      #locale: (mandatory field)Locale to be used for SRT. Supported locales [en/fr/de/ja].
      locale: en
   
      #aemTempDir: AEM Temp direcotry
      aemTempDir:
   
      #users: provide PDFG converting users list
      #users:
      # - user1
      # - user2
      users:
   
      #profile: select profile to run specific checks. Choose from [LCM], more will be added soon 
      profile:
   
      #outputDir: directory where output files will be saved
      outputDir:
   ```

1. Vá até `[Path_of_reports_folder]`. Abra o arquivo SystemReadinessTool.html . Verifique o relatório e corrija os problemas mencionados.

## Resolução de problemas

Se você enfrentar problemas mesmo depois de corrigir todos os problemas relatados pela ferramenta SRT, execute as seguintes verificações:

Antes de realizar as verificações a seguir, verifique se [Ferramenta de preparação do sistema](#SRT) não relata nenhum erro.

+++ Adobe Acrobat

* Garantir somente [versão compatível](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) do Microsoft® Office (32 bits) e o Adobe Acrobat está instalado e as caixas de diálogo de abertura são canceladas.
* Verifique se o Serviço de atualização do Adobe Acrobat está desativado.
* Certifique-se de que [Acrobat_for_PDFG_Configuration.bat](#configure-acrobat-for-the-pdf-generator-service) o arquivo em lote foi executado com privilégios de administrador.
* Verifique se um usuário PDF Generator foi adicionado na interface do usuário de configuração do PDF.
* Certifique-se de que [Substituir um token de nível de processo](#grant-the-replace-a-process-level-token-privilege) é adicionada para o usuário PDF Generator.
* Certifique-se de que o Suplemento Acrobat PDFMaker Office COM está ativado para aplicativos do Microsoft Office.

+++

+++Abrir Escritório

**Microsoft® Windows**

* Certifique-se de que [versão compatível](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) O do Microsoft Office está instalado e as caixas de diálogo de abertura são canceladas para todos os aplicativos.
* Verifique se um usuário PDF Generator foi adicionado na interface do usuário de configuração do PDF.
* Certifique-se de que o usuário Gerador de PDF é membro do grupo de administradores e do [Substituir um token de nível de processo](#grant-the-replace-a-process-level-token-privilege) privilégio é definido para o usuário.
* Certifique-se de que o usuário esteja configurado na interface do PDF Generator e execute as seguintes ações:
   1. Faça logon no Microsoft® Windows com o usuário PDF Generator.
   1. Abra os aplicativos Microsoft® Office ou Open Office e cancele todas as caixas de diálogo.
   1. Defina AdobePDF como impressora padrão.
   1. Defina o Acrobat como programa padrão para arquivos PDF.
   1. Execute a conversão manual usando as opções Arquivo > Imprimir e Acrobat em aplicativos do Microsoft Office e cancele todas as caixas de diálogo.
   1. Encerre todos os processos relacionados à conversão, como winword.exe, powerpoint.exe e excel.exe.
   1. Reinicie o servidor AEM Forms.

**Linux®**

* Certifique-se de que [versão compatível](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) Se o Open Office estiver instalado, as caixas de diálogo de abertura serão canceladas para todos os aplicativos e os aplicativos do Office serão iniciados com êxito.
* Criar uma variável de ambiente `OpenOffice_PATH` e defina-o para apontar para que a instalação do OpenOffice esteja definida no [console](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/) ou o perfil dt (Árvore do dispositivo).
* Se houver problemas na instalação do OpenOffice, verifique se [Bibliotecas de 32 bits](#extrarequirements) são necessários para a instalação do OpenOffice.

+++

+++HTML para problemas de conversão de PDF

* Certifique-se de que os diretórios de fontes sejam adicionados na interface do usuário de configuração do PDF Generator.

**Linux e Solaris (rota de conversão PhantomJS)**

* Certifique-se de que a biblioteca de 32 bits esteja disponível (libicudata.so.42) para conversão baseada em HTMLToPDF do Webkit e 64 bits (libicudata.so.42 libs) esteja disponível para conversão baseada em HTML baseada em PhantomJS.

* Execute o seguinte comando para listar bibliotecas ausentes para phantomjs:

   ```
   ldd phantomjs | grep not
   ```

* Certifique-se de que a variável de ambiente JAVA_HOME_32 aponte para o local correto.

**Linux® e Solaris™ (rota de conversão WebKit)**

* Certifique-se de que os diretórios `/usr/lib/X11/fonts` e `/usr/share/fonts` existe. Se os diretórios não existirem, crie um link simbólico de `/usr/share/X11/fonts` para `/usr/lib/X11/fonts` e outro link simbólico de `/usr/share/fonts` para `/usr/share/X11/fonts`.

   ```
   ln -s /usr/share/fonts /usr/share/X11/fonts
   
   ln -s /usr/share/X11/fonts /usr/lib/X11/fonts
   ```

* Certifique-se de que as fontes do IBM sejam copiadas em usr/share/fonts.
* Certifique-se de que a glibc da correção de vulnerabilidade de fantasma esteja disponível na máquina. Use seu gerenciador de pacotes padrão para atualizar para a versão mais recente do glibc. Inclui a correção de vulnerabilidade de fantasmas.
* Certifique-se de que as versões mais recentes das bibliotecas lib de 32 bits curl, libcrypto e libssl estejam instaladas no sistema. Criar também links simbólicos `/usr/lib/libcurl.so` (ou libcurl.a para AIX®), `/usr/lib/libcrypto.so` (ou libcrypto.a para AIX®) e `/usr/lib/libssl.so` (ou libssl.a para AIX®) apontando para as versões mais recentes (32 bits) das respectivas bibliotecas.

* Execute as seguintes etapas para o provedor de soquete SSL IBM®:
   1. Copie o arquivo java.security de `<WAS_Installed_JAVA>\jre\lib\security` para qualquer local no servidor do AEM Forms. O local padrão é Local padrão é = `<WAS_Installed>\Appserver\java_[version]\jre\lib\security`.

   1. Edite o arquivo java.security no local copiado e altere as fábricas padrão de soquete SSL com fábricas JSSE2 (Use fábricas JSSE2 em vez de WebSphere®).

      Altere as seguintes fábricas de soquete JSSE padrão:

      ```
      #ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      #ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

      com

      ```
      ssl.SocketFactory.provider=com.ibm.jsse2.SSLSocketFactoryImpl
      ssl.ServerSocketFactory.provider=com.ibm.jsse2.SSLServerSocketFactoryImpl
      WebSphere socket factories (in cryptosf.jar)
      #ssl.SocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLSocketFactory
      #ssl.ServerSocketFactory.provider=com.ibm.websphere.ssl.protocol.SSLServerSocketFactory
      ```

+++

+++ Não é possível adicionar um usuário do Gerador de PDF (PDFG)

* Verifique se o Microsoft® Visual C++ 2012 x86 e o Microsoft® Visual C++ 2013 x86 (32 bits) redistribuíveis estão instalados no Windows.

+++

+++Falhas no teste de automação

* Para o Microsoft® Office e o OpenOffice, execute pelo menos uma conversão manualmente (como cada usuário) para garantir que nenhuma caixa de diálogo apareça durante a conversão. Se alguma caixa de diálogo for exibida, descarte-a. Essa caixa de diálogo não deve aparecer durante a conversão automática.

* Antes de executar a automação em um ambiente AEM Forms em OSGi, verifique se o pacote de teste está instalado e ativo.

+++

+++Várias falhas de conversão de usuário

* Verifique os logs do servidor para verificar se a conversão está falhando para um usuário específico.(O Process Explorer pode ajudá-lo a verificar o processo de execução para usuários diferentes)

* Certifique-se de que o usuário configurado para PDF Generator tenha direitos de administrador local.

* Certifique-se de que o usuário do Gerador de PDF tenha permissões de leitura, gravação e execução em usuários temporários do LC e PDFG.

* Para o Microsoft® Office e o OpenOffice, execute pelo menos uma conversão manualmente (como cada usuário) para garantir que nenhuma caixa de diálogo apareça durante a conversão. Se alguma caixa de diálogo for exibida, descarte-a. Essa caixa de diálogo não deve aparecer durante a conversão automática.

* Execute uma conversão de amostra.

+++

+++A licença do Adobe Acrobat instalada no AEM Forms Server expira

* Se você tiver uma licença existente do Adobe Acrobat e ela tiver expirado, [Baixe a versão mais recente do Adobe Application Manager](https://helpx.adobe.com/in/creative-suite/kb/aam-troubleshoot-download-install.html)e migrando seu número de série. Antes [migrando seu número de série](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number).

   * Use os comandos a seguir para gerar vid.xml e serializar novamente a instalação existente usando o arquivo vid.xml em vez dos comandos fornecidos em [migrando seu número de série](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) artigo numérico.

          &quot;
          
          adobe_prtk —tool=VolumeSerialize —generate —serial=&lt;serialnum> [—leid=&lt;leid>] [—regsuppress=ss] [—eulasuppress] [—locales=lista limitada de localidades no formato xx_XX ou ALL>] [—provfile=&lt;absolute path=&quot;&quot; to=&quot;&quot; prov.xml=&quot;&quot;>]
          
          &quot;
      
   * Serialize o volume do pacote (serialize novamente a instalação existente usando o arquivo vid.xml e o novo serial): Execute o seguinte comando da pasta de instalação do PRTK como administrador para serializar e ativar os pacotes implantados em computadores clientes:

          &quot;
          adobe_prtk —tool=VolumeSerialize —provfile=C:\prov.xml -stream
          
          &quot;
      
* Para instalações de grande escala, use o [Customization Wizard Acrobat](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/index.html) para remover versões anteriores do Reader e do Acrobat. Personalize o instalador e implante-o em todos os computadores de sua organização.

+++

+++ O AEM Forms Server está em um ambiente offline ou seguro e a Internet não está disponível para ativar o Acrobat.

* Você pode ficar online dentro de 7 dias da primeira inicialização do produto Adobe para concluir uma ativação e registro online ou usar um dispositivo habilitado para Internet e o número de série do seu produto para concluir este processo. Para obter instruções detalhadas, consulte [Ativação offline](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en).

+++

## Próximas etapas {#next-steps}

Você tem um ambiente de serviços de documento da AEM Forms em funcionamento. Você pode usar serviços de documento por meio de:

* [Fluxos de trabalho centrados em formulários no OSGi](/help/forms/using/aem-forms-workflow.md)
* [Pastas monitoradas](/help/forms/using/watched-folder-in-aem-forms.md)
* [APIs de serviços de documento](/help/forms/using/aem-document-services-programmatically.md)
