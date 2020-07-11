---
title: Instalação e configuração de serviços de documento
seo-title: Instalação e configuração de serviços de documento
description: Instale os serviços de documento do AEM Forms para criar, montar, distribuir, arquivar documentos PDF, adicionar assinaturas digitais para limitar o acesso a documentos e decodificar formulários com códigos de barras.
seo-description: Instale os serviços de documento do AEM Forms para criar, montar, distribuir, arquivar documentos PDF, adicionar assinaturas digitais para limitar o acesso a documentos e decodificar formulários com códigos de barras.
uuid: 908806a9-b0d4-42d3-9fe4-3eae44cf4326
topic-tags: installing
discoiquuid: b53eae8c-16ba-47e7-9421-7c33e141d268
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '4295'
ht-degree: 1%

---


# Instalação e configuração de serviços de documento {#installing-and-configuring-document-services}

O AEM Forms fornece um conjunto de serviços OSGi para realizar operações de nível de documento diferente, por exemplo, serviços para criar, montar, distribuir e arquivar documentos PDF, adicionar assinaturas digitais para limitar o acesso a documentos e decodificar formulários com códigos de barras. Esses serviços estão incluídos no pacote complementar AEM Forms. Coletivamente, esses serviços são conhecidos como serviços de documento. A lista dos serviços de documento disponíveis e seus principais recursos é a seguinte:

* **Serviço de montador:** Permite combinar, reorganizar e aumentar documentos PDF e XDP e obter informações sobre documentos PDF. Também ajuda a converter e validar documentos PDF em PDF/A padrão, transforma PDF forms, formulários XML e PDF forms em PDF/A-1b, PDF/A-2b e PDF/A-3b. Para obter mais informações, consulte Serviço [de Montagem](/help/forms/using/assembler-service.md).

* **Serviço ConvertPDF:** Permite converter documentos PDF em PostScript ou arquivos de imagem (JPEG, JPEG 2000, PNG e TIFF). Para obter mais informações, consulte Serviço [](/help/forms/using/using-convertpdf-service.md)ConvertPDF.

* **Serviço de formulários com códigos de barras:** Permite que você extraia dados de imagens eletrônicas de códigos de barras. O serviço aceita arquivos TIFF e PDF que incluem um ou mais códigos de barras como entrada e extrai os dados do código de barras. Para obter mais informações, consulte Serviço [](/help/forms/using/using-barcoded-forms-service.md)de formulários com códigos de barras.

* **Serviço DocAssurance:** Permite que você criptografe e descriptografe documentos, estenda a funcionalidade do Adobe Reader com direitos de uso adicionais e adicione assinaturas digitais aos seus documentos. O serviço de Garantia de Documento contém três serviços: assinatura, criptografia e extensão do leitor. Para obter mais informações, consulte Serviço [](/help/forms/using/overview-aem-document-services.md)DocAssurance.

* **Serviço de criptografia:** Permite que você criptografe e descriptografe documentos. Quando um documento é criptografado, seu conteúdo se torna ilegível. Um usuário autorizado pode descriptografar o documento para obter acesso ao seu conteúdo. Para obter mais informações, consulte Serviço [](/help/forms/using/overview-aem-document-services.md#encryption-service)de criptografia.

* **Serviço de formulários:** Permite criar aplicativos clientes de captura de dados interativos que validam, processam, transformam e entregam formulários normalmente criados no Forms Designer. O serviço Forms renderiza qualquer design de formulário desenvolvido para documentos PDF. Para obter mais informações, consulte Serviço [de](/help/forms/using/forms-service.md)formulários.

* **Serviço de saída:** Permite criar documentos em diferentes formatos, incluindo PDF, formatos de impressora laser e formatos de impressora de etiquetas. Os formatos de impressora a laser são PostScript e Printer Control Language (PCL). Para obter mais informações, consulte Serviço [de](/help/forms/using/output-service.md)saída.

* **Serviço Gerador de PDF:** O serviço Gerador de PDF fornece APIs para converter formatos de arquivo nativos em PDF. Também converte PDF em outros formatos de arquivo e otimiza o tamanho dos documentos PDF. Para obter mais informações, consulte Serviço [do Gerador de](aem-document-services-programmatically.md#pdfgeneratorservice)PDF.

* **Serviço de extensão do Reader:** Permite que sua organização compartilhe facilmente documentos PDF interativos estendendo a funcionalidade do Adobe Reader com direitos de uso adicionais. O serviço ativa recursos que não estão disponíveis quando um documento PDF é aberto usando o Adobe Reader, como adicionar comentários a um documento, preencher formulários e salvar o documento. Para obter mais informações, consulte [Reader Extension Service](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **Serviço de assinatura:** Permite trabalhar com assinaturas e documentos digitais no servidor AEM. Por exemplo, o serviço de assinatura é normalmente usado nas seguintes situações:

   * O servidor AEM certifica um formulário antes de ele ser enviado para um usuário abrir usando o Acrobat ou o Adobe Reader.
   * O servidor AEM valida uma assinatura que foi adicionada a um formulário usando o Acrobat ou o Adobe Reader.
   * O servidor AEM assina um formulário em nome de um notário público.

   O serviço de assinatura acessa certificados e credenciais armazenados no repositório de confiança. Para obter mais informações, consulte Serviço [de](/help/forms/using/aem-document-services-programmatically.md)assinatura.

A AEM Forms é uma plataforma poderosa de classe empresarial e os serviços de documento são apenas um dos recursos dos AEM Forms. Para obter a lista completa dos recursos, consulte [Introdução aos AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologia de implantação {#deployment-topology}

O pacote complementar do AEM Forms é um aplicativo implantado no AEM. Geralmente, é necessário apenas uma instância do AEM (autor ou publicação) para executar serviços de documento do AEM Forms. A topologia a seguir é recomendada para executar serviços de documento do AEM Forms. Para obter informações detalhadas sobre topologias, consulte [Arquitetura e topologias de implantação para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![Topologias de arquitetura e implantação para AEM Forms](do-not-localize/document-services.png)

>[!NOTE]
>
>Embora o AEM Forms permita configurar e executar todas as funcionalidades de um único servidor, você deve fazer planejamento de capacidade, balanceamento de carga e configurar servidores dedicados para recursos específicos em um ambiente de produção. Por exemplo, para um ambiente que usa o serviço Gerador de PDF para converter milhares de páginas por dia e vários formulários adaptáveis para capturar dados, configure servidores AEM Forms separados para o serviço Gerador de PDF e recursos de formulários adaptáveis. Ele ajuda a proporcionar um desempenho ótimo e dimensionar os servidores independentemente uns dos outros.

## Requisitos do sistema {#system-requirements}

Antes de começar a instalar e configurar os serviços de documento do AEM Forms, verifique se:

* A infraestrutura de hardware e software está em vigor. Para obter uma lista detalhada do hardware e software suportados, consulte os requisitos [](/help/sites-deploying/technical-requirements.md)técnicos.

* O caminho de instalação da instância do AEM não contém espaços em branco.
* Uma instância do AEM está ativa e em execução. Na terminologia do AEM, uma &quot;instância&quot; é uma cópia do AEM em execução em um servidor no modo de autor ou publicação. Geralmente, você precisa de apenas uma instância do AEM (autor ou publicação) para executar serviços de documento do AEM Forms:

   * **Autor**: Uma instância do AEM usada para criar, carregar e editar conteúdo e administrar o site. Depois que o conteúdo estiver pronto para entrar em funcionamento, ele será replicado para a instância de publicação.
   * **Publicar**: Uma instância do AEM que fornece o conteúdo publicado ao público pela Internet ou por uma rede interna.

* Os requisitos de memória são atendidos. O pacote suplementar de AEM Forms requer:

   * 15 GB de espaço temporário para instalações baseadas no Microsoft Windows.
   * 6 GB de espaço temporário para instalações baseadas em UNIX.

* O software cliente necessário para que o gerador de PDF execute a conversão no Microsoft Windows e no Linux está instalado:

   * **Microsoft Windows**: Instale o [Microsoft](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)Office ou o [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux**: Instalar o [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* No Microsoft Windows, o Gerador de PDF oferece suporte a rotas de conversão WebKit, Acrobat WebCapture e PhantomJS para converter arquivos HTML em documentos PDF.
>* Em sistemas operacionais baseados em UNIX, o Gerador de PDF suporta rotas de conversão WebKit e PhantomJS para converter arquivos HTML em documentos PDF.

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
     <li>libuídio</li> 
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

* **(Somente** para o Gerador de PDF) Instale a versão de 32 bits das bibliotecas libcurl, libcrypto e libssl e crie os links simbólicos abaixo. Os links simbólicos apontam para a versão mais recente das respectivas bibliotecas:

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(Somente gerador de PDF)** O serviço Gerador de PDF suporta rotas WebKit e PhantomJS para converter arquivos HTML em documentos PDF. Para ativar a conversão para a rota PhantomJS, instale as bibliotecas de 64 bits listadas abaixo. Geralmente, essas bibliotecas já estão instaladas. Se alguma biblioteca estiver faltando, instale-a manualmente:

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

As configurações listadas na seção de configurações de pré-instalação são aplicáveis somente ao serviço Gerador de PDF. Se você não estiver configurando o serviço Gerador de PDF, poderá ignorar a seção de configuração de pré-instalação.

### Instale o Adobe Acrobat e aplicativos de terceiros {#install-adobe-acrobat-and-third-party-applications}

Se você for usar o serviço Gerador de PDF para converter formatos de arquivo nativos, como Documentos Microsoft Word, Microsoft Excel, Microsoft PowerPoint, OpenOffice, WordPerfect X7 e Adobe Acrobat para PDF, verifique se esses aplicativos estão instalados no servidor AEM Forms.

>[!NOTE]
>
>* O Adobe Acrobat, o Microsoft Word, o Excel e o Powerpoint estão disponíveis somente para o Microsoft Windows. Se você estiver usando o sistema operacional baseado em UNIX, instale o OpenOffice para converter arquivos Rich Text e arquivos suportados do Microsoft Office em documentos PDF.
>* Descarte todas as caixas de diálogo exibidas após a instalação do Adobe Acrobat e de software de terceiros para todos os usuários configurados para usar o serviço Gerador de PDF.
>* Start todo o software instalado pelo menos uma vez. Descarte todas as caixas de diálogo para todos os usuários configurados para usar o serviço Gerador de PDF.

>



Depois de instalar o Acrobat, abra o Microsoft Word. Na **guia** Acrobat, clique **em Criar PDF** e converta um arquivo .doc ou .docx disponível em seu computador para um Documento PDF. Se a conversão for bem-sucedida, o AEM Forms estará pronto para usar o Acrobat com o serviço Gerador de PDF.

### Configurar variáveis de ambiente {#setup-environment-variables}

Defina variáveis de ambiente para o kit de desenvolvimento Java de 32 bits e 64 bits, aplicativos de terceiros e o Adobe Acrobat. As variáveis de ambiente devem conter o caminho absoluto do executável usado para start do aplicativo correspondente, por exemplo, a tabela abaixo das variáveis de ambiente do lista para alguns aplicativos:

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Aplicativo</strong></p> </td> 
   <td><p><strong>variável Ambiente</strong></p> </td> 
   <td><p><strong>Exemplo</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>JDK (64 bits)</strong></p> </td> 
   <td><p>JAVA_HOME</p> </td> 
   <td><p>C:\Program Files\Java\jdk1.8.0_74</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>JDK (32 bits)</strong></p> </td> 
   <td><p>JAVA_HOME_32</p> </td> 
   <td><p>C:\Program Files (x86)\Java\jdk1.8.0_74</p> </td> 
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
>* Todas as variáveis de ambiente e respectivos caminhos fazem distinção entre maiúsculas e minúsculas.
>* JAVA_HOME, JAVA_HOME_32 e Acrobat_PATH (somente Windows) são variáveis obrigatórias de ambiente.
>* A variável de ambiente OpenOffice_PATH é definida para a pasta de instalação em vez do caminho para o executável.
>* Não configure variáveis de ambiente para aplicativos do Microsoft Office, como Word, PowerPoint, Excel e Project, ou para AutoCAD. Se esses aplicativos estiverem instalados no servidor, o serviço Gerar PDF automaticamente start esses aplicativos.
>* Em plataformas baseadas em UNIX, instale o OpenOffice como /root. Se o OpenOffice não estiver instalado como raiz, o serviço Gerador de PDF não converterá documentos OpenOffice em documentos PDF. Se for necessário instalar e executar o OpenOffice como um usuário não raiz, forneça direitos sudo para o usuário não raiz.
>* Se você estiver usando o OpenOffice em uma plataforma baseada em UNIX, execute o seguinte comando para definir a variável de caminho:

>
>  
`export OpenOffice_PATH=/opt/openoffice.org4`

### (Somente para IBM WebSphere) Configurar o provedor de soquete IBM SSL {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

Execute as seguintes etapas para configurar o provedor de soquete IBM SSL:

1. Crie uma cópia do arquivo java.security. O local padrão do arquivo é `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`.
1. Abra o arquivo java.security copiado para edição.
1. Altere as fábricas padrão de soquetes SSL para usar as fábricas JSSE2 em vez das fábricas padrão IBM WebSphere:

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

1. Para permitir que o servidor AEM Forms use o arquivo java.security atualizado, ao iniciar o servidor AEM Forms, adicione o seguinte argumento java:

   `-Djava.security.properties= [path of newly created Java.security file].`

### (Somente para Windows) Configurar o serviço de instalação de escrita manual e tinta {#configure-install-ink-and-handwriting-service}

Se você estiver executando o Microsoft Windows Server, configure o serviço de Ink and Handwriting. O serviço é necessário para abrir arquivos do Microsoft PowerPoint que usam recursos de vinculação do Microsoft Office:

1. Abra o Server Manager. Clique no ícone **[!UICONTROL Server Manager]** na bandeja de Início rápido.
1. Clique em **[!UICONTROL Adicionar recursos]** no menu **[!UICONTROL Recursos]** . Marque a caixa de seleção **[!UICONTROL Ink and Handwriting Services]** (Serviços de tinta e escrita manual).
1. **[!UICONTROL Selecione a caixa de diálogo Recursos]** com Serviços **[!UICONTROL de]** Tinta e Escrita Manual selecionados. Clique em **[!UICONTROL Instalar]** e o serviço será instalado.

### (Somente Windows) Configure as configurações de bloco de arquivos para o Microsoft Office {#configure-the-file-block-settings-for-microsoft-office}

Altere as configurações do centro de confiança do Microsoft Office para permitir que o serviço Gerador de PDF converta arquivos criados com versões mais antigas do Microsoft Office.

1. Abra um aplicativo do Microsoft Office. Por exemplo, Microsoft Word. Navegue até **[!UICONTROL Arquivo]**> **[!UICONTROL Opções]**. A caixa de diálogo Opções é exibida.

1. Clique em Central de **[!UICONTROL confiança]** e clique em Configurações **[!UICONTROL da]** Central de confiança.
1. Nas configurações **[!UICONTROL da Central de]** Confiança, clique em Configurações **[!UICONTROL de bloco de]** arquivos.
1. Na lista Tipo **[!UICONTROL de]** arquivo, desmarque **[!UICONTROL Abrir]** para o tipo de arquivo que o serviço Gerador de PDF deve ter permissão para converter em documentos PDF.

### (Somente para Windows) Conceda ao privilégio Substituir token de nível de processo {#grant-the-replace-a-process-level-token-privilege}

A conta de usuário usada para start do servidor de aplicativos requer o privilégio **Substituir token** de nível de processo. Por padrão, a conta do sistema local tem o privilégio **Substituir um token** de nível de processo. Para os servidores que executam com um usuário do grupo Administradores locais, o privilégio deve ser concedido explicitamente. Execute as seguintes etapas para conceder o privilégio:

1. Abra o Editor de políticas de grupo para Microsoft Windows. Para abrir o Editor de políticas de grupo, clique em **[!UICONTROL Start]**, digite **gpedit.msc** na caixa Pesquisa de Start e clique em Editor **[!UICONTROL de políticas de]** grupo.
1. Navegue até Política **[!UICONTROL do computador]** local > Configuração **[!UICONTROL do]** computador > Configurações **[!UICONTROL do]** Windows > Configurações **[!UICONTROL de]** segurança > Políticas **** **** **** locais > Atribuição de direitos de usuário, edite a política do token de nível de processo de Substituição de e inclua o grupo Administradores.
1. Adicione o usuário à entrada Substituir um token de nível de processo.

### (Somente Windows) Ative o serviço Gerador de PDF para não administradores {#enable-the-pdf-generator-service-for-non-administrators}

Você pode habilitar um usuário que não seja administrador a usar o serviço Gerador de PDF. Normalmente, somente os usuários com privilégios administrativos podem usar o serviço:

1. Crie uma variável de ambiente, PDFG_NON_ADMIN_ENABLED.
1. Defina o valor da variável de ambiente como TRUE.
1. Reinicie a instância do AEM Forms.

### (Somente para Windows) Desativar Controle de Conta de Usuário (UAC) {#disable-user-account-control-uac}

1. Para acessar o Utilitário de configuração do sistema, vá até **[!UICONTROL Start > Executar]** e digite **[!UICONTROL MSCONFIG]**.
1. Clique na guia **[!UICONTROL Ferramentas]** e role para baixo e selecione **[!UICONTROL Alterar configurações]** UAC. Clique em **[!UICONTROL Iniciar]** para executar o comando em uma nova janela.
1. Ajuste o controle deslizante para o nível Nunca notificar. Quando terminar, feche a janela de comando e feche a janela Configuração do sistema.
1. Verifique se a configuração do Registro para UAC está definida como 0 (zero). Execute as seguintes etapas para verificar:

   1. A Microsoft recomenda fazer backup do registro antes de modificá-lo. Para obter etapas detalhadas, consulte [Como fazer backup e restaurar o registro no Windows](https://support.microsoft.com/en-us/help/322756).
   1. Abra o editor de Registro do Microsoft Windows. Para abrir o editor do Registro, vá até Start > Executar, digite regedit e clique em OK.
   1. Vá até `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Verifique se o valor de EnableLUA está definido como 0 (zero).
   1. Verifique se o valor de **EnableLUA** está definido como 0 (zero). Se o valor não for 0, altere o valor para 0. Feche o editor do Registro.

1. Reinicie o computador.

### (Somente para Windows) Desativar o serviço Relatórios de erros {#disable-error-reporting-service}

Ao converter um documento em PDF usando o serviço Gerador de PDF no Windows Server, ocasionalmente, o Windows Server informa que o executável encontrou um problema e precisa fechar. No entanto, isso não afeta a conversão do PDF à medida que continua em segundo plano.

Para evitar receber o erro, você pode desativar o relatórios de erro do Windows. Para obter mais informações sobre como desativar o relatórios de erro, consulte [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### (Somente para Windows) Configurar a conversão de HTML em PDF {#configure-html-to-pdf-conversion}

O serviço Gerador de PDF fornece rotas ou métodos WebKit, WebCapture e PhantomJS para converter arquivos HTML em documentos PDF. No Windows, para ativar a conversão para rotas WebKit e Acrobat WebCapture, copie a fonte Unicode para o diretório %windir%\fonts.

>[!NOTE]
>
>Sempre que instalar novas fontes na pasta de fontes, reinicie a instância do AEM Forms.

### (Somente plataformas baseadas em UNIX) Configurações extras para conversão de HTML em PDF  {#extra-configurations-for-html-to-pdf-conversion}

Em plataformas baseadas em UNIX, o serviço Gerador de PDF oferece suporte a rotas WebKit e PhantomJS para converter arquivos HTML em documentos PDF. Para ativar a conversão de HTML em PDF, execute as seguintes configurações, aplicáveis à sua rota de conversão preferida:

### (Somente plataformas baseadas em UNIX) Ativar suporte para fontes Unicode (somente WebKit) {#enable-support-for-unicode-fonts-webkit-only}

Copie a fonte Unicode para qualquer um dos seguintes diretórios, conforme apropriado para o seu sistema:

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType (Solaris)

>[!NOTE]
>
>* No RedHat Enterprise Linux 6.x e posterior, as fontes courier não estão disponíveis. Para instalar as fontes do correio, baixe o arquivo font-ibm-type1-1.0.3.zip. Extraia o arquivo em /usr/share/fonts. Crie um link simbólico de /usr/share/X11/fonts para /usr/share/fonts.
>* Exclua todos os arquivos de cache de fontes .lst dos diretórios Html2PdfSvc/bin e /usr/share/fonts.
>* Verifique se os diretórios /usr/lib/X11/fonts e /usr/share/fonts existem. Se os diretórios não existirem, use o comando ln para criar um link simbólico de /usr/share/X11/fonts para /usr/lib/X11/fonts e outro link simbólico de /usr/share/fonts para /usr/share/X11/fonts. Verifique também se as fontes courier estão disponíveis em /usr/lib/X11/fonts.
>* Verifique se todas as fontes (Unicode e não-unicode) estão disponíveis no diretório /usr/share/fonts ou /usr/share/X11/fonts.
>* Ao executar o serviço Gerador de PDF como um usuário não raiz, forneça ao usuário não raiz acesso de leitura e gravação a todos os diretórios de fonte.
>* Sempre que instalar novas fontes na pasta de fontes, reinicie a instância do AEM Forms.

>



## Install AEM Forms add-on package {#install-aem-forms-add-on-package}

O pacote complementar do AEM Forms é um aplicativo implantado no AEM. O pacote contém os Serviços de Documento do AEM Forms e outros recursos de AEM Forms. Execute as seguintes etapas para instalar o pacote:

1. Distribuição [de](https://experience.adobe.com/downloads)software aberta. Você precisa de um Adobe ID para fazer login na Software Distribution (Distribuição de software).
1. Toque em **[!UICONTROL Adobe Experience Manager]** disponível no menu de cabeçalho.
1. Na seção **[!UICONTROL Filtros]** :
   1. Selecione **[!UICONTROL Formulários]** na lista suspensa **[!UICONTROL Solução]** .
   2. Selecione a versão e o tipo do pacote. Você também pode usar a opção **[!UICONTROL Pesquisar downloads]** para filtrar os resultados.
1. Toque no nome do pacote aplicável ao seu sistema operacional, selecione **[!UICONTROL Aceitar termos]** do EULA e toque em **[!UICONTROL Download]**.
1. Abra o Gerenciador [de](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) pacotes e clique em **[!UICONTROL Carregar pacote]** para fazer upload do pacote.
1. Select the package and click **[!UICONTROL Install]**.

   Você também pode baixar o pacote por meio do link direto listado no artigo de versões [de](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) AEM Forms.

1. Depois que o pacote for instalado, você será solicitado a reiniciar a instância do AEM. **Não interrompa imediatamente o servidor.** Antes de parar o servidor de AEM Forms, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no arquivo `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log e o log esteja estável.

## Configurações pós-instalação {#post-installation-configurations}

### Configurar delegação de inicialização para bibliotecas RSA/BouncyCastle  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. Pare a instância do AEM. Navegue até o diretório [\crx-quickstart\conf\ folder de instalação do]AEM. Abra o arquivo sling.properties para edição.

   Se você usar `[AEM installation directory]\crx-quickstart\bin\start.bat` para start de uma instância do AEM, edite sling.properties localizado em `[AEM_root]\crx-quickstart\`.

1. Adicione as seguintes propriedades ao arquivo sling.properties:

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. (Somente para AIX) Adicione as seguintes propriedades ao arquivo sling.properties:

   ```
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. Salve e feche o arquivo.

### Configurar o serviço do gerenciador de fontes  {#configuring-the-font-manager-service}

1. Faça logon no [AEM Configuration Manager](http://localhost:4502/system/console/configMgr) como administrador.
1. Localize e abra o serviço **[!UICONTROL CQ-DAM-Handler-Gibson Font Managers]** . Especifique o caminho dos diretórios Fontes do sistema, Fontes do servidor Adobe e Fontes do cliente. Clique em **[!UICONTROL Salvar]**.

   >[!NOTE]
   >
   >O seu direito de usar fontes fornecidas por outras partes além da Adobe é regido pelos contratos de licença fornecidos por essas partes com essas fontes, e não está coberto pela sua licença para usar o software da Adobe. A Adobe recomenda que você analise e verifique se está em conformidade com todos os contratos de licença que não sejam da Adobe antes de usar fontes que não sejam da Adobe com o software da Adobe, especialmente no que diz respeito ao uso de fontes em um ambiente de servidor.
   > Quando você instalar novas fontes na pasta fonts, reinicie a instância do AEM Forms.

### Configurar uma conta de usuário local para executar o serviço Gerador de PDF  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

Uma conta de usuário local é necessária para executar o serviço Gerador de PDF. Para obter etapas para criar um usuário local, consulte [Criar uma conta de usuário no Windows](https://support.microsoft.com/en-us/help/13951/windows-create-user-account) ou [criar uma conta de usuário em plataformas](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/4/html/Step_by_Step_Guide/s1-starting-create-account.html)baseadas em UNIX.

1. Abra a página Configuração [do Gerador de PDF do](http://localhost:4502/libs/fd/pdfg/config/ui.html) AEM Forms.

1. Na guia Contas **[!UICONTROL de]** usuário, forneça as credenciais de uma conta de usuário local e clique em **[!UICONTROL Enviar]**. Se o Microsoft Windows solicitar, permita acesso ao usuário. Quando adicionado com êxito, o usuário configurado é exibido na seção **[!UICONTROL Suas contas]** de usuário na guia Contas **[!UICONTROL de]** usuário.

### Definir as configurações de tempo limite {#configure-the-time-out-settings}

1. No gerenciador [de configuração do](http://localhost:4502/system/console/configMgr)AEM, localize e abra o serviço Provedor **** Jacorb ORB.

   Adicione o seguinte ao campo Propriedades **[!UICONTROL personalizadas.name]** e clique em **[!UICONTROL Salvar]**. Ele define o tempo limite de resposta pendente (também conhecido como tempo limite do cliente CORBA) como 600 segundos.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. Faça logon na instância do autor do AEM e navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Ferramentas]** > **[!UICONTROL Formulários]** > **[!UICONTROL Configurar o Gerador]** de PDF. O URL padrão é http://localhost:4502/libs/fd/pdfg/config/ui.html.

   Abra a guia Configuração **** geral e modifique o valor dos seguintes campos para o seu ambiente:

<table> 
 <tbody> 
  <tr> 
   <td>Texto</td> 
   <td>Descrição</td> 
   <td>Valor padrão</td> 
  </tr> 
  <tr> 
   <td>Tempo limite da conversão do servidor</td> 
   <td>Uma conversão PDFG permanece ativa pelo número de segundos definido no tempo limite de conversão do servidor</td> 
   <td>270 seconds<br /> </td> 
  </tr> 
  <tr> 
   <td>Segundos para exploração de limpeza do PDFG</td> 
   <td>O número de segundos necessários para executar operações pós-conversão.<br /> </td> 
   <td>3600 segundos</td> 
  </tr> 
  <tr> 
   <td>Segundos para expiração da tarefa</td> 
   <td>Duração para a qual o serviço Gerador de PDF tem permissão para executar uma conversão. Verifique se o valor de Segundos de expiração do trabalho é maior que o valor de Segundos de verificação da limpeza PDFG.</td> 
   <td>7200 segundos</td> 
  </tr> 
 </tbody> 
</table>

### (Somente para Windows) Configurar o Acrobat para o serviço Gerador de PDF {#configure-acrobat-for-the-pdf-generator-service}

No Microsoft Windows, o serviço Gerador de PDF usa o Adobe Acrobat para converter os formatos de arquivo suportados em um documento PDF. Execute as seguintes etapas para configurar o Adobe Acrobat para o serviço Gerador de PDF:

1. Abra o Acrobat e selecione **[!UICONTROL Editar]**> **[!UICONTROL Preferências]**> **[!UICONTROL Atualizador]**. Em Verificar se há atualizações, desmarque Instalar atualizações **** automaticamente e clique em **[!UICONTROL OK]**. Feche o Acrobat.
1. Duplo clique em um documento PDF no seu sistema. Quando o Acrobat for start pela primeira vez, as caixas de diálogo para Logon, Tela de boas-vindas e EULA serão exibidas. Descarte essas caixas de diálogo para todos os usuários configurados para usar o Gerador de PDF.
1. Execute o arquivo em lote do utilitário Gerador de PDF para configurar o Acrobat para o serviço Gerador de PDF:

   1. Abra o Gerenciador [de pacotes do](http://localhost:4502/crx/packmgr/index.jsp) AEM e baixe o `adobe-aemfd-pdfg-common-pkg-[version].zip` arquivo do gerenciador de pacotes.
   1. Descompacte o arquivo .zip baixado. Abra o prompt de comando com privilégios administrativos.
   1. Navegue até o `[extracted-zip-file]\jcr_root\etc\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\scripts` diretório. Execute o seguinte arquivo de lote:

      `Acrobat_for_PDFG_Configuration.bat`

      O Acrobat está configurado para ser executado com o serviço Gerador de PDF.

1. Execute o System Readiness Tool (SRT) para validar a instalação do Acrobat. A ferramenta verifica se o computador está configurado corretamente para executar conversões do Gerador de PDF e gera um relatório no caminho especificado:

   1. Abra o prompt de comando. Navegue até a `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\etc\fd\ pdfg\tools\adobe-aemfd-pdfg-utilities-[version]-win.zip\srt` pasta. Execute o seguinte comando no prompt de comando:

      `cscript SystemReadinessTool.vbs [Path_of_reports_folder] en`

      >[!NOTE]
      >
      >Se a ferramenta System Readiness reportar que o arquivo pdfgen.api não está disponível na pasta plug-ins do acrobat, copie o arquivo pdfgen.api do `[extracted-adobe-aemfd-pdfg-common-pkg]\plugins\x86_win32` diretório para o `[Acrobat_root]\Acrobat\plug_ins` diretório.

   1. Vá até `[Path_of_reports_folder]`. Abra o arquivo SystemReadinessTool.html. Verifique o relatório e corrija os problemas mencionados.

### (Somente para Windows) Configurar a rota principal para conversão de HTML em PDF {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

O serviço Gerador de PDF fornece várias rotas para converter arquivos HTML em documentos PDF: Webkit, Acrobat WebCapture (somente Windows) e PhantomJS. A Adobe recomenda usar a rota PhantomJS porque ela tem a capacidade de lidar com conteúdo dinâmico e não tem dependências em bibliotecas de 32 bits, JDK de 32 bits ou não requer fontes extras. Além disso, a rota PhantomJS não requer acesso sudo ou raiz para executar a conversão.

A rota principal padrão para conversão HTML em PDF é Webkit. Para alterar a rota de conversão:

1. Na instância do autor de AEM, navegue até **[!UICONTROL Ferramentas]**> **[!UICONTROL Formulários]**> **[!UICONTROL Configurar o Gerador]** de PDF.

1. Na guia Configuração **** geral, selecione a rota de conversão preferencial no menu suspenso Rota **[!UICONTROL primária para conversões]** HTML em PDF.

### Inicializar armazenamento de confiança global {#intialize-global-trust-store}

Usando o Gerenciamento de armazenamento de confiança, você pode importar, editar e excluir certificados confiáveis no servidor para a validação de assinaturas digitais e autenticação de certificado. É possível importar e exportar qualquer número de certificados. Depois que um certificado é importado, você pode editar as configurações de confiança e o tipo de armazenamento de confiança. Execute as seguintes etapas para inicializar um armazenamento confiável:

1. Faça logon na instância do AEM Forms como administrador.
1. Vá até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Armazenamento]** de confiança.
1. Clique em **[!UICONTROL Criar TrustStore]**. Defina a senha e toque em **[!UICONTROL Salvar]**.

### Configurar certificados para o serviço de extensão e criptografia do Reader {#set-up-certificates-for-reader-extension-and-encryption-service}

O serviço DocAssurance pode aplicar direitos de uso a documentos PDF. Para aplicar direitos de uso a documentos PDF, configure os certificados.

Antes de configurar os certificados, verifique se você tem uma:

* Arquivo de certificado (.pfx).

* Senha da chave privada fornecida com o certificado.

* Alias da chave de privacidade. Você pode executar o comando keytool para visualização do Alias da chave privada:
   `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* Senha do arquivo de armazenamento de chaves. Se você estiver usando o certificado do Reader Extensions da Adobe, a senha do arquivo Keystore será sempre a mesma da chave privada.

Execute as seguintes etapas para configurar os certificados:

1. Faça logon na instância AEM Author como administrador. Vá até **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.
1. Clique no campo **[!UICONTROL name]** da conta de usuário. A página **[!UICONTROL Editar configurações]** do usuário é aberta. Na instância AEM Author, os certificados residem em um KeyStore. Se você não tiver criado um KeyStore antes, clique em **[!UICONTROL Criar KeyStore]** e defina uma nova senha para o KeyStore. Se o servidor já tiver um KeyStore, ignore esta etapa.  Se você estiver usando o certificado do Reader Extensions da Adobe, a senha do arquivo Keystore será sempre a mesma da chave privada.
1. Na página **[!UICONTROL Editar configurações]** do usuário, selecione a guia **[!UICONTROL KeyStore]** . Expanda a opção **[!UICONTROL Adicionar chave privada do arquivo]** de armazenamento de chave e forneça um alias. O alias é usado para executar a operação do Reader Extensions.
1. Para carregar o arquivo de certificado, clique em **[!UICONTROL Selecionar arquivo]** de armazenamento de chave e carregue um arquivo &lt;nome do arquivo>.pfx.

   Adicione a senha **[!UICONTROL do armazenamento de]** chave, a senha **[!UICONTROL da chave]** privada e o alias **[!UICONTROL da chave]** privada associados ao certificado aos respectivos campos. Clique em **[!UICONTROL Enviar]**.

   >[!NOTE]
   >
   >* No ambiente de produção, substitua suas credenciais de avaliação por credenciais de produção. Certifique-se de excluir suas credenciais antigas do Reader Extensions antes de atualizar uma credencial expirada ou de avaliações.


1. Clique em **[!UICONTROL Salvar e fechar]** na página **[!UICONTROL Editar configurações]** do usuário.

### Ativar AES-256 {#enable-aes}

Para usar a criptografia AES 256 para arquivos PDF, obtenha e instale os arquivos da política de jurisdição de força ilimitada do Java Cryptography Extension (JCE). Substitua os arquivos local_policy.jar e US_export_policy.jar na pasta jre/lib/security. Por exemplo, se você estiver usando o Sun JDK, copie os arquivos baixados para a `[JAVA_HOME]/jre/lib/security` pasta.

O serviço Assembler depende do serviço Reader Extensions, do serviço Signature, do serviço Forms e do serviço Output. Execute as seguintes etapas para verificar se os serviços necessários estão ativos e em execução:

1. Faça logon no URL `https://'[server]:[port]'/system/console/bundles` como administrador.
1. Pesquise o serviço a seguir e verifique se os serviços estão ativos e em execução:

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
   <td>Reader Extensions Service</td> 
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

* A conversão de HTML em PDF falhará se um arquivo de entrada compactado contiver arquivos HTML com caracteres de duplo byte em nomes de arquivos. Para evitar esse problema, não use caracteres de duplo byte ao nomear arquivos HTML.

* Em sistemas operacionais baseados em UNIX, faça o seguinte para localizar quaisquer bibliotecas ausentes:

1. Vá até `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. Execute o seguinte comando para lista de todas as bibliotecas exigidas pelo PhantomJS para conversão de HTML em PDF.

   `ldd phantomjs`

   Execute o seguinte comando para lista de bibliotecas ausentes.

   `ldd phantomjs | grep not`

1. Instale manualmente as bibliotecas ausentes.

## Próximos passos {#next-steps}

Você tem um ambiente de serviços de documento de AEM Forms funcionando. Você pode usar os serviços de documento por meio de:

* [workflows centrados em formulários no OSGi](/help/forms/using/aem-forms-workflow.md)
* [Pastas monitoradas](/help/forms/using/watched-folder-in-aem-forms.md)
* [APIs de serviços de Documento](/help/forms/using/aem-document-services-programmatically.md)

