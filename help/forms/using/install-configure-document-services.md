---
title: Instalar e configurar serviços de documento
description: Instale os serviços de documento do AEM Forms para criar, montar, distribuir, arquivar documentos do PDF, adicionar assinaturas digitais para limitar o acesso a documentos e decodificar o Forms com código de barras.
topic-tags: installing
role: Admin, Developer
exl-id: 5d48e987-16c2-434b-8039-c82181d2e028
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
source-git-commit: c6d38c682dc45e3dcebef194b3b80510ab10f9e2
workflow-type: tm+mt
source-wordcount: '10086'
ht-degree: 1%

---

# Instalar e configurar serviços de documento {#installing-and-configuring-document-services}

A AEM Forms fornece um conjunto de serviços OSGi para realizar diferentes operações no nível do documento, por exemplo, serviços para criar, montar, distribuir e arquivar documentos PDF, adicionar assinaturas digitais para limitar o acesso a documentos e decodificar Forms com código de barras. Esses serviços estão incluídos no pacote complementar do AEM Forms. Coletivamente, esses serviços são conhecidos como serviços de documentos. A lista de serviços de documentos disponíveis e seus principais recursos são os seguintes:

* **Serviço do Assembler:** permite combinar, reorganizar e aumentar documentos PDF e XDP e obter informações sobre documentos PDF. Também ajuda a converter e validar documentos do PDF para o padrão PDF/A, transforma PDF forms, formulários XML e PDF forms para PDF/A-1b, PDF/A-2b e PDFA/A-3b. Para obter mais informações, consulte [Serviço de Assembler](/help/forms/using/assembler-service.md).

* **Serviço ConvertPDF:** permite converter documentos do PDF em arquivos PostScript ou de imagem (JPEG, JPEG 2000, PNG e TIFF). Para obter mais informações, consulte [Converter serviço PDF](/help/forms/using/using-convertpdf-service.md).

* **Serviço Forms com código de barras:** permite extrair dados de imagens eletrônicas de códigos de barras. O serviço aceita arquivos TIFF e PDF que incluem um ou mais códigos de barras como entrada e extrai os dados do código de barras. Para obter mais informações, consulte [Serviço Forms com código de barras](/help/forms/using/using-barcoded-forms-service.md).

* **Serviço DocAssurance:** permite criptografar e descriptografar documentos, estender a funcionalidade do Adobe Reader com direitos de uso adicionais e adicionar assinaturas digitais aos documentos. O serviço Doc Assurance contém três serviços: assinatura, criptografia e extensão do leitor. Para obter mais informações, consulte [DocAssurance Service](/help/forms/using/overview-aem-document-services.md).

* **Serviço de criptografia:** permite que você criptografe e descriptografe documentos. Quando um documento é criptografado, seu conteúdo fica ilegível. Um usuário autorizado pode descriptografar o documento para obter acesso ao conteúdo. Para obter mais informações, consulte [Serviço de criptografia](/help/forms/using/overview-aem-document-services.md#encryption-service).

* **Serviço Forms:** permite criar aplicativos cliente de captura de dados interativos que validam, processam, transformam e entregam formulários que normalmente são criados no Forms Designer. O serviço Forms renderiza qualquer design de formulário desenvolvido para documentos do PDF. Para obter mais informações, consulte [Forms Service](/help/forms/using/forms-service.md).

* **Serviço de saída:** permite que você crie documentos em diferentes formatos, incluindo PDF, formatos de impressora a laser e formatos de impressora de etiquetas. Os formatos de impressora a laser são PostScript e PCL (Printer Control Language). Para obter mais informações, consulte [Serviço de Saída](/help/forms/using/output-service.md).

* **Serviço PDF Generator:** o serviço PDF Generator fornece APIs para converter formatos de arquivo nativos em PDF. Também converte o PDF em outros formatos de arquivo e otimiza o tamanho dos documentos do PDF. Para obter mais informações, consulte [PDF Generator Service](aem-document-services-programmatically.md#pdfgeneratorservice).

* **Serviço de extensão do Reader:** permite que sua organização compartilhe facilmente documentos interativos do PDF, estendendo a funcionalidade do Adobe Reader com direitos de uso adicionais. O serviço ativa recursos que não estão disponíveis quando um documento do PDF é aberto usando o Adobe Reader, como adicionar comentários a um documento, preencher formulários e salvar o documento. Para obter mais informações, consulte [Reader Extension Service](/help/forms/using/overview-aem-document-services.md#reader-extension-service).

* **Serviço de assinatura:** permite trabalhar com assinaturas e documentos digitais no servidor do AEM. Por exemplo, o serviço de Assinatura é normalmente usado nas seguintes situações:

   * O servidor do AEM certifica um formulário antes que ele seja enviado a um usuário para ser aberto usando o Acrobat ou o Adobe Reader.
   * O servidor do AEM valida uma assinatura que foi adicionada a um formulário usando o Acrobat ou o Adobe Reader.
   * O servidor do AEM assina um formulário em nome de um notário público.

  O serviço de assinatura acessa certificados e credenciais armazenados no armazenamento de confiança. Para obter mais informações, consulte [Serviço de assinatura](/help/forms/using/aem-document-services-programmatically.md).

O AEM Forms é uma plataforma corporativa poderosa e os serviços de documentos são apenas um dos recursos do AEM Forms. Para obter a lista completa de recursos, consulte [Introdução ao AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologia de implantação {#deployment-topology}

O pacote complementar do AEM Forms é um aplicativo implantado no AEM. Geralmente, você precisa de apenas uma instância do AEM (autor ou publicação) para executar os serviços de documento do AEM Forms. A topologia a seguir é recomendada para executar serviços de documento do AEM Forms. Para obter informações detalhadas sobre topologias, consulte [Arquitetura e topologias de implantação para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![Arquitetura e topologias de implantação para o AEM Forms](do-not-localize/document-services.png)

>[!NOTE]
>
>Embora o AEM Forms permita configurar e executar todas as funcionalidades de um único servidor, você deve fazer o planejamento de capacidade, o balanceamento de carga e configurar servidores dedicados para recursos específicos em um ambiente de produção. Por exemplo, para um ambiente que usa o serviço PDF Generator para converter milhares de páginas por dia e vários formulários adaptáveis para capturar dados, configure servidores AEM Forms separados para o serviço PDF Generator e recursos de formulários adaptáveis. Ele ajuda a fornecer o melhor desempenho e a dimensionar os servidores independentemente uns dos outros.

## Requisitos do sistema {#system-requirements}

Antes de começar a instalar e configurar os serviços de documento do AEM Forms, verifique se:

* A infraestrutura de hardware e software está em vigor. Para obter uma lista detalhada de hardware e software com suporte, consulte [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

* O caminho de instalação da instância do AEM não contém espaços em branco.
* Uma instância do AEM está em execução. Na terminologia do AEM, uma &quot;instância&quot; é uma cópia do AEM executada em um servidor no modo de criação ou publicação. Geralmente, é necessário apenas uma instância do AEM (autor ou publicação) para executar os serviços de documento do AEM Forms:

   * **Autor**: uma instância do AEM usada para criar, carregar, editar conteúdo e administrar o site. Quando o conteúdo estiver pronto para entrar em funcionamento, ele será replicado para a instância de publicação.
   * **Publicar**: uma instância do AEM que serve o conteúdo publicado para o público através da Internet ou de uma rede interna.

* Os requisitos de memória são atendidos. O pacote complementar do AEM Forms exige:

   * 15 GB de espaço temporário para instalações baseadas no Microsoft® Windows.
   * 6 GB de espaço temporário para instalações baseadas em UNIX.

* O software cliente necessário para o gerador de PDF executar a conversão no Microsoft® Windows e Linux® está instalado:

   * **Microsoft® Windows**: instalar o [Microsoft® Office](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p) ou o [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator)
   * **Linux®**: instalar o [Apache OpenOffice](/help/forms/using/aem-forms-jee-supported-platforms.md#p-software-support-for-pdf-generator-p)

>[!NOTE]
>
>* No Microsoft® Windows, a PDF Generator suporta as rotas de conversão WebKit, Acrobat WebCapture e WebToPDF para converter arquivos HTML em documentos PDF.
>* Em sistemas operacionais baseados em UNIX, o PDF Generator suporta rotas de conversão WebKit e WebToPDF para converter arquivos HTML em documentos PDF.
>

### Requisitos adicionais para o sistema operacional baseado em UNIX {#extrarequirements}

Se você estiver usando um sistema operacional baseado em UNIX, instale os seguintes pacotes de 32 bits a partir da mídia de instalação do respectivo sistema operacional:
<table>
 <tbody>
  <tr>
   <td>
    <ul>
     <li>expat</li>
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
     <li>nss-softoken-freebl</li>
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

* **(PDF Generator somente**) Instale a versão de 32 bits das bibliotecas libcurl, libcrypto e libssl e crie os symlinks abaixo. Os symlinks apontam para a versão mais recente das respectivas bibliotecas:

   * /usr/lib/libcurl.so
   * /usr/lib/libcrypto.so
   * /usr/lib/libssl.so

* **(Somente PDF Generator)** O serviço PDF Generator oferece suporte às rotas WebKit e WebToPDF para converter arquivos HTML em documentos PDF. Para habilitar a conversão para a rota WebToPDF, instale as bibliotecas de 64 bits listadas abaixo. Geralmente, essas bibliotecas já estão instaladas. Se alguma biblioteca estiver ausente, instale-a manualmente:

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
* (Somente PDF Generator) Para habilitar a rota do WebKit nas configurações RHEL 8 ou RHEL 9, SLES15, a biblioteca `nspr` de 32 bits pode não estar disponível por padrão; instale-a se não estiver presente.

* (Somente no PDF Generator) Se a conversão WebToPDF falhar em um servidor Unix® com o seguinte erro:

  ```Auto configuration failed 4143511872:error:0E079065:configuration file routines:DEF_LOAD_BIO:missing equal sign:conf_def.c:362:line 57```
em seguida, defina a seguinte variável de ambiente e reinicie o servidor:
  `OPENSSL_CONF=/etc/ssl`

>[!NOTE]
>
> WebToPDF também é usado pelo recurso Gráfico em Comunicações Interativas. Portanto, todas as etapas de configuração mencionadas para WebToPDF acima são aplicáveis para garantir que o recurso de gráfico funcione corretamente.

## Configurações de pré-instalação {#preinstallationconfigurations}

As configurações listadas na seção de configurações de pré-instalação se aplicam somente ao serviço do PDF Generator. Se você não estiver configurando o serviço PDF Generator, ignore a seção de configuração de pré-instalação.

### Instalar o Adobe Acrobat e aplicativos de terceiros {#install-adobe-acrobat-and-third-party-applications}

Se você for usar o serviço PDF Generator para converter formatos de arquivo nativos, como Microsoft® Word, Microsoft® Excel, Microsoft® PowerPoint, OpenOffice e Adobe Acrobat em documentos PDF, verifique se esses aplicativos estão instalados no servidor AEM Forms.

>[!NOTE]
>
><!-- * If your AEM Forms Server is in an offline or secure environment and internet is not available to activate Adobe Acrobat, see [Offline Activation](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en) for instructions to activate such instances of Adobe Acrobat. -->
>* Adobe Acrobat, Microsoft® Word, Excel e Powerpoint estão disponíveis apenas para Microsoft® Windows. Se você estiver usando o sistema operacional baseado em UNIX, instale o OpenOffice para converter arquivos rich text e arquivos suportados do Microsoft® Office em documentos PDF.
>* Ignore todas as caixas de diálogo exibidas após a instalação do Adobe Acrobat e de softwares de terceiros para todos os usuários configurados para usar o serviço PDF Generator.
>* Inicie todos os softwares instalados pelo menos uma vez. Ignore todas as caixas de diálogo de todos os usuários configurados para usar o serviço PDF Generator.
>* [Verifique a data de expiração de seus números de série da Adobe Acrobat](https://helpx.adobe.com/enterprise/kb/volume-license-expiration-check.html) e defina uma data para atualizar a licença ou [migre seu número de série](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) com base na data de expiração.

### Instale o Adobe Acrobat Pro DC

#### Pré-requisitos

Antes de instalar o Acrobat, reveja esses requisitos essenciais. Você deve ter:

* Familiaridade com o [Adobe Admin Console](https://helpx.adobe.com/in/enterprise/admin-guide.html)
* Noções básicas sobre sua [arquitetura de implantação do AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md)
* Privilégios administrativos no Adobe Admin Console e no servidor que executa o AEM Forms.
* Um usuário com [acesso de administrador](https://helpx.adobe.com/in/enterprise/using/admin-roles.html) à Adobe [Admin Console](https://adminconsole.adobe.com). Geralmente, o administrador da organização já teria um usuário com acesso de administrador. Você pode assistir a este [vídeo instrutivo](https://www.youtube.com/watch?v=xO2T0I6SvsU&list=PLHRegP5ZOj7CpijZyD8pB9rIMJkvO6FnI&t=81s) sobre as etapas de adição de um administrador.
* Uma conta de usuário com a função de [Administrador de Implantação](https://helpx.adobe.com/in/enterprise/global-admin-console/manage-administrators.html) na Adobe Admin Console. O mesmo [vídeo de instrução](https://www.youtube.com/watch?v=xO2T0I6SvsU&list=PLHRegP5ZOj7CpijZyD8pB9rIMJkvO6FnI&t=81s) demonstra como adicionar um Administrador de Implantação.
* Privilégios de administrador local na máquina que executa o AEM Forms
* Sistema operacional Windows de 64 bits
* Conexão estável com a Internet para ativação de licença
<!-- Backup solution for existing Acrobat settings
 Supported version of Adobe Acrobat (see [Adobe documentation](https://helpx.adobe.com/acrobat/kb/acrobat-dc-compatibility-with-windows-macos.html) for details) -->


#### Fluxo de trabalho e linha do tempo da implementação

O processo completo normalmente leva de 1 a 2 horas, dependendo do seu ambiente:

| Etapa | Tempo estimado | Pré-requisitos |
|------|----------------|---------------|
| &#x200B;1. Criar pacote de FRL no Admin Console) | 15-20 minutos | [Acesso ao Admin Console](https://helpx.adobe.com/in/enterprise/admin-guide.html) |
| &#x200B;2. Conceder permissões de download | 5-10 minutos | [Acesso ao Admin Console](https://helpx.adobe.com/in/enterprise/global-admin-console/manage-administrators.html) |
| &#x200B;3. Desinstalar o Acrobat anterior | 10-15 minutos | Acesso de administrador do servidor |
| &#x200B;4. Baixe e instale o Adobe Acrobat Pro | 10-15 minutos | Acesso de administrador do servidor |
| &#x200B;5. Baixar e implantar o pacote de FRL | 20-30 minutos | Acesso de administrador do servidor |
| &#x200B;6. Verificar instalação | 5-10 minutos | Acesso ao servidor |

<!-- ![Workflow diagram showing the FRL implementation process](/help/forms/using/assets/frl.svg) -->

**Escolher Caminho de Instalação**

O processo de instalação do Adobe Acrobat Pro DC para instalação do Microsoft Office varia um pouco, dependendo do tipo de licença e do cenário de implantação. Para garantir que você siga as etapas corretas para seu ambiente específico, selecione a guia que corresponde à sua configuração:

* **Tipo de Licença**: Licença de Varejo ou Volume
* **Tipo de Implantação**: Um ou Vários Usuários

Cada guia contém instruções personalizadas otimizadas para sua configuração específica, ajudando você a evitar problemas de configuração e garantir a conformidade adequada com o licenciamento.

>[!VIDEO](https://video.tv.adobe.com/v/3469669)

>[!NOTE]
>
>O vídeo demonstra o processo de instalação de uma licença de varejo - configuração de usuário único. Para outros cenários de implantação (Varejo - Vários usuários, Licença por volume - Usuário único ou Licença por volume - Vários usuários), consulte as instruções específicas da etapa 9 nas guias correspondentes abaixo para garantir a inicialização correta do servidor e a ativação da licença para seu tipo de implantação.

>[!BEGINTABS]

>[!TAB Licença de Varejo - Único Usuário]

#### Configuração do FRL (Feature Restricted Licensing) para o Adobe Acrobat no servidor do AEM Forms

Essas etapas pressupõem que você tenha os privilégios administrativos necessários no Adobe Admin Console e no servidor que executa o AEM Forms.

##### Preparar o pacote de FRL (Adobe Admin Console)

Estas etapas devem ser executadas com acesso de *Administrador do Sistema* à Adobe Admin Console.

###### Etapa 1: fazer logon na Adobe Admin Console

1. Abra um navegador e navegue até a [Adobe Admin Console](https://adminconsole.adobe.com/)
1. Faça logon usando uma conta com privilégios de *Administrador do Sistema*.
1. (Opcional) Se sua organização tiver acesso a várias organizações IMS, use a opção de seleção de organização no canto superior direito do Admin Console para escolher a organização correta. Na maioria dos cenários de clientes, isso já estaria definido como o padrão de sua organização, pois os usuários normalmente têm acesso apenas à sua própria organização.

###### Etapa 2: criar o pacote FRL

1. No Admin Console, navegue até a guia &quot;Pacotes&quot;. Este é um pacote Adobe Admin Console, não um pacote AEM.
1. Selecione o cartão **Licença de Recurso Restrito** e clique no botão **Introdução**. Certifique-se de selecionar o tipo de licença correto.
1. Na tela **Criar um pacote**, defina as configurações do pacote:

   | Configuração | Valor recomendado | Notas |
   |---------|-------------------|-------|
   | Método de ativação | Offline | Opção recomendada |
   | Direito | Geração de PDF (PDFG) | Necessário para a funcionalidade do AEM Forms PDF Generator |
   | Configurar plataforma | Windows de 64 bits | O Apple macOS não é compatível no momento |
   | Ativar local | &quot;Usar idioma do SO&quot; | Configuração padrão |
   | Idioma | Seu idioma preferido | Para interface do Acrobat |
   | Escolher aplicativos - aplicativos disponíveis | Mantenha o Adobe Acrobat nos aplicativos disponíveis. Não Mover para o aplicativo selecionado | Você [baixaria o Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro) da página da Adobe Experience League na etapa 6. |
   | Escolher aplicativos - aplicativos selecionados | Manter apenas o arquivo de licença nos aplicativos selecionados | Configuração padrão para implantação de FRL |
   | Plug-ins | Não fazer alterações nesta tela | |
   | Opções | Não fazer alterações nesta tela | |
   | Finalizar | Nome do pacote: &quot;Acrobat FRL AEM Forms&quot; | Usar um nome descritivo |

1. Clique em **Criar** para criar o pacote.

###### Etapa 3: fornecer permissões de download a um usuário

É recomendável criar uma conta de serviço dedicada para gerenciar pacotes de FRL. Se você ainda não tiver uma conta dedicada, siga este [vídeo instrutivo](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s) para saber como adicionar um novo usuário à sua organização da Adobe.

Depois de ter a conta apropriada, siga estas etapas para conceder permissões de download:

1. Na Admin Console, navegue até a guia **Usuários**.
2. Localize ou crie uma conta de usuário para conceder permissões de download.
3. Clique no nome do usuário para abrir o perfil.
4. Clique no ícone ao lado do usuário **Editar Direitos de Administrador**.
5. Atribua a função de **Administrador de Implantação** ao usuário. Outras funções de administrador também podem funcionar, mas Administrador de implantação é a função recomendada. Clique em **Salvar**.


##### Implantar o pacote de FRL (AEM Forms Server)

As etapas a seguir são executadas no AEM Forms Server, com direitos de *administrador local* sobre a máquina.

###### Etapa 4: faça logon no servidor que executa o AEM Forms como administrador

Acesse o servidor que executa o AEM Forms usando o método apropriado. Verifique se você está usando uma conta com privilégios de administrador local para acessar o servidor.

###### Etapa 5: desinstalar a versão anterior do Acrobat (se houver)

**Crítico:** Faça backup de todas as configurações, perfis ou configurações personalizadas do Acrobat antes de desinstalar.

1. Abra o Painel de Controle do Windows.
2. Navegue até **Configurações** e abra **Aplicativos**.
3. Localize o **Adobe Acrobat** na lista de programas instalados
4. Selecione **Desinstalar** e siga as instruções para remover o aplicativo. Se solicitado, reinicie o servidor
5. Verifique se todas as versões Classic do programa estão desinstaladas. Use a [Ferramenta de Limpeza do Adobe Acrobat](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html) se necessário para concluir a remoção.

###### Etapa 6: baixar e instalar o Adobe Acrobat Pro

Após desinstalar a versão anterior, é necessário baixar e instalar uma versão compatível do Adobe Acrobat Pro:

1. Vá para a [página Downloads do Adobe Acrobat DC](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html).
2. Navegue até a seção **Instalador do Acrobat Pro**.
3. Para uso com o AEM Forms PDF Generator, baixe o instalador &quot;Para Windows (32 bits)&quot;, pois esta é a versão compatível com o AEM Forms PDF Generator.
4. Siga as instruções de instalação na página:
   * Extraia o arquivo zip baixado para uma pasta no seu computador
   * Navegue até o arquivo Setup.exe (não execute o arquivo Setup.exe a partir do arquivo zip)
   * Clique duas vezes em Setup.exe para iniciar a instalação
   * Siga as instruções na tela para concluir a instalação
5. Após a instalação, abra o Adobe Acrobat Pro e conclua a configuração inicial, descartando as caixas de diálogo de boas-vindas.
6. Verifique a instalação criando uma PDF simples.

###### Etapa 7: baixar o pacote FRL

1. Faça logon no [Adobe Admin Console](https://adminconsole.adobe.com/) usando a *conta de usuário* à qual você forneceu permissões de download na Etapa 3.
1. Navegue até a guia **Pacotes**.
1. Localize o pacote de FRL que você criou na Etapa 2 (chamado &quot;Acrobat FRL AEM Forms&quot; ou o nome do pacote personalizado).
1. Clique em **Baixar** para baixar o pacote no servidor.

###### Etapa 8: implantar o pacote

1. **Extrair o Pacote:** Extraia o conteúdo do arquivo ZIP baixado para um diretório no servidor (por exemplo, `C:\AcrobatFRL`). Certifique-se de que o diretório de extração seja facilmente acessível.

2. **Abrir Prompt de Comando como Administrador (Windows):** Clique com o botão direito no botão Iniciar e selecione &quot;Prompt de Comando (Admin)&quot; ou &quot;Windows PowerShell (Admin)&quot;

3. **Navegue até o diretório de extração:**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **Executar o Comando de Ativação:**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **Importante:**
   > * Substitua `<JSON_FILE_NAME>.json` pelo nome de arquivo *exato* do arquivo JSON no pacote extraído.
   > * O nome de arquivo JSON diferencia maiúsculas de minúsculas.
   > * Verifique se há erros de digitação no nome do arquivo.

   **Saída esperada:**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ️ **Observação:** o processo de ativação pode levar aproximadamente 30 segundos.

5. **Noções Básicas sobre os Parâmetros de Comando:**

   | Parâmetro | Descrição |
   |-----------|-------------|
   | `-p` | Especifica a plataforma (detecta automaticamente o sistema operacional) |
   | `-i` | Instrui a ferramenta a instalar e ativar a licença |
   | `-f` | Especifica o caminho para o arquivo de licença JSON |

###### Etapa 9: testar o serviço PDF Generator

Após concluir todos os processos, execute um teste de ação rápida para confirmar se a instalação é válida:

1. Abrir a interface do administrador do AEM Forms
2. Navegue até o serviço PDF Generator
3. Tente converter um documento simples do Microsoft Office para o PDF
4. Verifique se a conversão foi concluída com sucesso

#### Verificar versão do Acrobat após ativação de FRL

1. Abra o Adobe Acrobat Pro DC no servidor
2. Acesse Ajuda → Sobre o Adobe Acrobat Pro DC
3. Verifique se o número da versão corresponde à versão esperada
4. Confirmar se o status da licença é exibido como ativado

>[!TAB Licença de varejo - Vários usuários]

#### Configuração do FRL (Feature Restricted Licensing) para o Adobe Acrobat no servidor do AEM Forms

Essas etapas pressupõem que você tenha os privilégios administrativos necessários no Adobe Admin Console e no servidor que executa o AEM Forms.

##### Preparar o pacote de FRL (Adobe Admin Console)

Estas etapas devem ser executadas com acesso de *Administrador do Sistema* à Adobe Admin Console.

###### Etapa 1: fazer logon na Adobe Admin Console

1. Abra um navegador e navegue até a [Adobe Admin Console](https://adminconsole.adobe.com/)
1. Faça logon usando uma conta com privilégios de *Administrador do Sistema*.
1. (Opcional) Se sua organização tiver acesso a várias organizações IMS, use a opção de seleção de organização no canto superior direito do Admin Console para escolher a organização correta. Na maioria dos cenários de clientes, isso já estaria definido como o padrão de sua organização, pois os usuários normalmente têm acesso apenas à sua própria organização.

###### Etapa 2: criar o pacote FRL

1. No Admin Console, navegue até a guia &quot;Pacotes&quot;. Este é um pacote Adobe Admin Console, não um pacote AEM.
1. Selecione o cartão **Licença de Recurso Restrito** e clique no botão **Introdução**. Certifique-se de selecionar o tipo de licença correto.
1. Na tela **Criar um pacote**, defina as configurações do pacote:

   | Configuração | Valor recomendado | Notas |
   |---------|-------------------|-------|
   | Método de ativação | Offline | Opção recomendada |
   | Direito | Geração de PDF (PDFG) | Necessário para a funcionalidade do AEM Forms PDF Generator |
   | Configurar plataforma | Windows de 64 bits | O Apple macOS não é compatível no momento |
   | Ativar local | &quot;Usar idioma do SO&quot; | Configuração padrão |
   | Idioma | Seu idioma preferido | Para interface do Acrobat |
   | Escolher aplicativos - aplicativos disponíveis | Mantenha o Adobe Acrobat nos aplicativos disponíveis. Não Mover para o aplicativo selecionado | Você [baixaria o Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro) da página da Adobe Experience League na etapa 6. |
   | Escolher aplicativos - aplicativos selecionados | Manter apenas o arquivo de licença nos aplicativos selecionados | Configuração padrão para implantação de FRL |
   | Plug-ins | Não fazer alterações nesta tela | |
   | Opções | Não fazer alterações nesta tela | |
   | Finalizar | Nome do pacote: &quot;Acrobat FRL AEM Forms&quot; | Usar um nome descritivo |

1. Clique em **Criar** para criar o pacote.

###### Etapa 3: fornecer permissões de download a um usuário

É recomendável criar uma conta de serviço dedicada para gerenciar pacotes de FRL. Se você ainda não tiver uma conta dedicada, siga este [vídeo instrutivo](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s) para saber como adicionar um novo usuário à sua organização da Adobe.

Depois de ter a conta apropriada, siga estas etapas para conceder permissões de download:

1. Na Admin Console, navegue até a guia **Usuários**.
2. Localize ou crie uma conta de usuário para conceder permissões de download.
3. Clique no nome do usuário para abrir o perfil.
4. Clique no ícone ao lado do usuário **Editar Direitos de Administrador**.
5. Atribua a função de **Administrador de Implantação** ao usuário. Outras funções de administrador também podem funcionar, mas Administrador de implantação é a função recomendada. Clique em **Salvar**.


##### Implantar o pacote de FRL (AEM Forms Server)

As etapas a seguir são executadas no AEM Forms Server, com direitos de *administrador local* sobre a máquina.

###### Etapa 4: faça logon no servidor que executa o AEM Forms como administrador

Acesse o servidor que executa o AEM Forms usando o método apropriado. Verifique se você está usando uma conta com privilégios de administrador local para acessar o servidor.

###### Etapa 5: desinstalar a versão anterior do Acrobat (se houver)

**Crítico:** Faça backup de todas as configurações, perfis ou configurações personalizadas do Acrobat antes de desinstalar.

1. Abra o Painel de Controle do Windows.
2. Navegue até **Configurações** e abra **Aplicativos**.
3. Localize o **Adobe Acrobat** na lista de programas instalados
4. Selecione **Desinstalar** e siga as instruções para remover o aplicativo. Se solicitado, reinicie o servidor
5. Verifique se todas as versões Classic do programa estão desinstaladas. Use a [Ferramenta de Limpeza do Adobe Acrobat](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html) se necessário para concluir a remoção.

###### Etapa 6: baixar e instalar o Adobe Acrobat Pro

Após desinstalar a versão anterior, é necessário baixar e instalar uma versão compatível do Adobe Acrobat Pro:

1. Vá para a [página Downloads do Adobe Acrobat DC](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html).
2. Navegue até a seção **Instalador do Acrobat Pro**.
3. Para uso com o AEM Forms PDF Generator, baixe o instalador &quot;Para Windows (32 bits)&quot;, pois esta é a versão compatível com o AEM Forms PDF Generator.
4. Siga as instruções de instalação na página:
   * Extraia o arquivo zip baixado para uma pasta no seu computador
   * Navegue até o arquivo Setup.exe (não execute o arquivo Setup.exe a partir do arquivo zip)
   * Clique duas vezes em Setup.exe para iniciar a instalação
   * Siga as instruções na tela para concluir a instalação
5. Após a instalação, abra o Adobe Acrobat Pro e conclua a configuração inicial, descartando as caixas de diálogo de boas-vindas.
6. Verifique a instalação criando uma PDF simples.

###### Etapa 7: baixar o pacote FRL

1. Faça logon no [Adobe Admin Console](https://adminconsole.adobe.com/) usando a *conta de usuário* à qual você forneceu permissões de download na Etapa 3.
1. Navegue até a guia **Pacotes**.
1. Localize o pacote de FRL que você criou na Etapa 2 (chamado &quot;Acrobat FRL AEM Forms&quot; ou o nome do pacote personalizado).
1. Clique em **Baixar** para baixar o pacote no servidor.

###### Etapa 8: implantar o pacote

1. **Extrair o Pacote:** Extraia o conteúdo do arquivo ZIP baixado para um diretório no servidor (por exemplo, `C:\AcrobatFRL`). Certifique-se de que o diretório de extração seja facilmente acessível.

2. **Abrir Prompt de Comando como Administrador (Windows):** Clique com o botão direito no botão Iniciar e selecione &quot;Prompt de Comando (Admin)&quot; ou &quot;Windows PowerShell (Admin)&quot;

3. **Navegue até o diretório de extração:**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **Executar o Comando de Ativação:**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **Importante:**
   > * Substitua `<JSON_FILE_NAME>.json` pelo nome de arquivo *exato* do arquivo JSON no pacote extraído.
   > * O nome de arquivo JSON diferencia maiúsculas de minúsculas.
   > * Verifique se há erros de digitação no nome do arquivo.

   **Saída esperada:**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ️ **Observação:** o processo de ativação pode levar aproximadamente 30 segundos.

5. **Noções Básicas sobre os Parâmetros de Comando:**

   | Parâmetro | Descrição |
   |-----------|-------------|
   | `-p` | Especifica a plataforma (detecta automaticamente o sistema operacional) |
   | `-i` | Instrui a ferramenta a instalar e ativar a licença |
   | `-f` | Especifica o caminho para o arquivo de licença JSON |

###### Etapa 9: iniciar o servidor do AEM Forms

Após concluir todos os processos, execute um teste de ação rápida para confirmar se a instalação é válida:

1. Inicie o servidor do AEM Forms a partir de um console de linha de comando em uma sessão de usuário interativa. (Faça logon no servidor e inicie manualmente o AEM Forms a partir da linha de comando.)
2. Mantenha a sessão do usuário ativa após iniciar o servidor. Não saia do computador, pois isso encerra o processo do servidor. Você pode fechar com segurança a janela da Área de Trabalho Remota (RDP) sem fazer logoff; o servidor continua a ser executado enquanto a sessão permanecer ativa.
3. Para maior confiabilidade, configure uma tarefa de inicialização ou tarefa agendada para iniciar automaticamente o servidor do AEM Forms quando o usuário fizer logon.

###### Etapa 10 Testar serviço PDF Generator

1. Abrir a interface do administrador do AEM Forms
2. Navegue até o serviço PDF Generator
3. Tente converter um documento simples do Microsoft Office para o PDF
4. Verifique se a conversão foi concluída com sucesso

#### Verificar versão do Acrobat após ativação de FRL

1. Abra o Adobe Acrobat Pro DC no servidor
2. Acesse Ajuda → Sobre o Adobe Acrobat Pro DC
3. Verifique se o número da versão corresponde à versão esperada
4. Confirmar se o status da licença é exibido como ativado

>[!TAB Licença de Volume - Usuário Único]

#### Configuração do FRL (Feature Restricted Licensing) para o Adobe Acrobat no servidor do AEM Forms

Essas etapas pressupõem que você tenha os privilégios administrativos necessários no Adobe Admin Console e no servidor que executa o AEM Forms.

##### Preparar o pacote de FRL (Adobe Admin Console)

Estas etapas devem ser executadas com acesso de *Administrador do Sistema* à Adobe Admin Console.

###### Etapa 1: fazer logon na Adobe Admin Console

1. Abra um navegador e navegue até a [Adobe Admin Console](https://adminconsole.adobe.com/)
1. Faça logon usando uma conta com privilégios de *Administrador do Sistema*.
1. (Opcional) Se sua organização tiver acesso a várias organizações IMS, use a opção de seleção de organização no canto superior direito do Admin Console para escolher a organização correta. Na maioria dos cenários de clientes, isso já estaria definido como o padrão de sua organização, pois os usuários normalmente têm acesso apenas à sua própria organização.

###### Etapa 2: criar o pacote FRL

1. No Admin Console, navegue até a guia &quot;Pacotes&quot;. Este é um pacote Adobe Admin Console, não um pacote AEM.
1. Selecione o cartão **Licença de Recurso Restrito** e clique no botão **Introdução**. Certifique-se de selecionar o tipo de licença correto.
1. Na tela **Criar um pacote**, defina as configurações do pacote:

   | Configuração | Valor recomendado | Notas |
   |---------|-------------------|-------|
   | Método de ativação | Offline | Opção recomendada |
   | Direito | Geração de PDF (PDFG) | Necessário para a funcionalidade do AEM Forms PDF Generator |
   | Configurar plataforma | Windows de 64 bits | O Apple macOS não é compatível no momento |
   | Ativar local | &quot;Usar idioma do SO&quot; | Configuração padrão |
   | Idioma | Seu idioma preferido | Para interface do Acrobat |
   | Escolher aplicativos - aplicativos disponíveis | Mantenha o Adobe Acrobat nos aplicativos disponíveis. Não Mover para o aplicativo selecionado | Você [baixaria o Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro) da página da Adobe Experience League na etapa 6. |
   | Escolher aplicativos - aplicativos selecionados | Manter apenas o arquivo de licença nos aplicativos selecionados | Configuração padrão para implantação de FRL |
   | Plug-ins | Não fazer alterações nesta tela | |
   | Opções | Não fazer alterações nesta tela | |
   | Finalizar | Nome do pacote: &quot;Acrobat FRL AEM Forms&quot; | Usar um nome descritivo |

1. Clique em **Criar** para criar o pacote.

###### Etapa 3: fornecer permissões de download a um usuário

É recomendável criar uma conta de serviço dedicada para gerenciar pacotes de FRL. Se você ainda não tiver uma conta dedicada, siga este [vídeo instrutivo](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s) para saber como adicionar um novo usuário à sua organização da Adobe.

Depois de ter a conta apropriada, siga estas etapas para conceder permissões de download:

1. Na Admin Console, navegue até a guia **Usuários**.
2. Localize ou crie uma conta de usuário para conceder permissões de download.
3. Clique no nome do usuário para abrir o perfil.
4. Clique no ícone ao lado do usuário **Editar Direitos de Administrador**.
5. Atribua a função de **Administrador de Implantação** ao usuário. Outras funções de administrador também podem funcionar, mas Administrador de implantação é a função recomendada. Clique em **Salvar**.


##### Implantar o pacote de FRL (AEM Forms Server)

As etapas a seguir são executadas no AEM Forms Server, com direitos de *administrador local* sobre a máquina.

###### Etapa 4: faça logon no servidor que executa o AEM Forms como administrador

Acesse o servidor que executa o AEM Forms usando o método apropriado. Verifique se você está usando uma conta com privilégios de administrador local para acessar o servidor.

###### Etapa 5: desinstalar a versão anterior do Acrobat (se houver)

**Crítico:** Faça backup de todas as configurações, perfis ou configurações personalizadas do Acrobat antes de desinstalar.

1. Abra o Painel de Controle do Windows.
2. Navegue até **Configurações** e abra **Aplicativos**.
3. Localize o **Adobe Acrobat** na lista de programas instalados
4. Selecione **Desinstalar** e siga as instruções para remover o aplicativo. Se solicitado, reinicie o servidor
5. Verifique se todas as versões Classic do programa estão desinstaladas. Use a [Ferramenta de Limpeza do Adobe Acrobat](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html) se necessário para concluir a remoção.

###### Etapa 6: baixar e instalar o Adobe Acrobat Pro

Após desinstalar a versão anterior, é necessário baixar e instalar uma versão compatível do Adobe Acrobat Pro:

1. Vá para a [página Downloads do Adobe Acrobat DC](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html).
2. Navegue até a seção **Instalador do Acrobat Pro**.
3. Para uso com o AEM Forms PDF Generator, baixe o instalador &quot;Para Windows (32 bits)&quot;, pois esta é a versão compatível com o AEM Forms PDF Generator.
4. Siga as instruções de instalação na página:
   * Extraia o arquivo zip baixado para uma pasta no seu computador
   * Navegue até o arquivo Setup.exe (não execute o arquivo Setup.exe a partir do arquivo zip)
   * Clique duas vezes em Setup.exe para iniciar a instalação
   * Siga as instruções na tela para concluir a instalação
5. Após a instalação, abra o Adobe Acrobat Pro e conclua a configuração inicial, descartando as caixas de diálogo de boas-vindas.
6. Verifique a instalação criando uma PDF simples.

###### Etapa 7: baixar o pacote FRL

1. Faça logon no [Adobe Admin Console](https://adminconsole.adobe.com/) usando a *conta de usuário* à qual você forneceu permissões de download na Etapa 3.
1. Navegue até a guia **Pacotes**.
1. Localize o pacote de FRL que você criou na Etapa 2 (chamado &quot;Acrobat FRL AEM Forms&quot; ou o nome do pacote personalizado).
1. Clique em **Baixar** para baixar o pacote no servidor.

###### Etapa 8: implantar o pacote

1. **Extrair o Pacote:** Extraia o conteúdo do arquivo ZIP baixado para um diretório no servidor (por exemplo, `C:\AcrobatFRL`). Certifique-se de que o diretório de extração seja facilmente acessível.

2. **Abrir Prompt de Comando como Administrador (Windows):** Clique com o botão direito no botão Iniciar e selecione &quot;Prompt de Comando (Admin)&quot; ou &quot;Windows PowerShell (Admin)&quot;

3. **Navegue até o diretório de extração:**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **Executar o Comando de Ativação:**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **Importante:**
   > * Substitua `<JSON_FILE_NAME>.json` pelo nome de arquivo *exato* do arquivo JSON no pacote extraído.
   > * O nome de arquivo JSON diferencia maiúsculas de minúsculas.
   > * Verifique se há erros de digitação no nome do arquivo.

   **Saída esperada:**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ️ **Observação:** o processo de ativação pode levar aproximadamente 30 segundos.

5. **Noções Básicas sobre os Parâmetros de Comando:**

   | Parâmetro | Descrição |
   |-----------|-------------|
   | `-p` | Especifica a plataforma (detecta automaticamente o sistema operacional) |
   | `-i` | Instrui a ferramenta a instalar e ativar a licença |
   | `-f` | Especifica o caminho para o arquivo de licença JSON |

###### Etapa 9: iniciar o servidor do AEM Forms

Após concluir todos os processos, execute um teste de ação rápida para confirmar se a instalação é válida:

1. Use a Área de Trabalho Remota (RDP) para fazer logon no servidor e iniciar o servidor do AEM Forms usando serviços.
2. Depois que o servidor estiver em execução, não feche a janela do RDP. Em vez disso, saia normalmente fazendo logoff do usuário do — isso garante que a sessão termine sem problemas enquanto o serviço continua a ser executado em segundo plano.

###### Etapa 10: testar o serviço PDF Generator

Após concluir todos os processos, execute um teste de ação rápida para confirmar se a instalação é válida:

1. Abrir a interface do administrador do AEM Forms
2. Navegue até o serviço PDF Generator
3. Tente converter um documento simples do Microsoft Office para o PDF
4. Verifique se a conversão foi concluída com sucesso

###### Etapa 11: verificar a versão do Acrobat após a ativação de FRL

1. Abra o Adobe Acrobat Pro DC no servidor
2. Acesse Ajuda → Sobre o Adobe Acrobat Pro DC
3. Verifique se o número da versão corresponde à versão esperada
4. Confirmar se o status da licença é exibido como ativado

>[!TAB Licença de Volume - Vários Usuários]

#### Configuração do FRL (Feature Restricted Licensing) para o Adobe Acrobat no servidor do AEM Forms

Essas etapas pressupõem que você tenha os privilégios administrativos necessários no Adobe Admin Console e no servidor que executa o AEM Forms.

##### Preparar o pacote de FRL (Adobe Admin Console)

Estas etapas devem ser executadas com acesso de *Administrador do Sistema* à Adobe Admin Console.

###### Etapa 1: fazer logon na Adobe Admin Console

1. Abra um navegador e navegue até a [Adobe Admin Console](https://adminconsole.adobe.com/)
1. Faça logon usando uma conta com privilégios de *Administrador do Sistema*.
1. (Opcional) Se sua organização tiver acesso a várias organizações IMS, use a opção de seleção de organização no canto superior direito do Admin Console para escolher a organização correta. Na maioria dos cenários de clientes, isso já estaria definido como o padrão de sua organização, pois os usuários normalmente têm acesso apenas à sua própria organização.

###### Etapa 2: criar o pacote FRL

1. No Admin Console, navegue até a guia &quot;Pacotes&quot;. Este é um pacote Adobe Admin Console, não um pacote AEM.
1. Selecione o cartão **Licença de Recurso Restrito** e clique no botão **Introdução**. Certifique-se de selecionar o tipo de licença correto.
1. Na tela **Criar um pacote**, defina as configurações do pacote:

   | Configuração | Valor recomendado | Notas |
   |---------|-------------------|-------|
   | Método de ativação | Offline | Opção recomendada |
   | Direito | Geração de PDF (PDFG) | Necessário para a funcionalidade do AEM Forms PDF Generator |
   | Configurar plataforma | Windows de 64 bits | O Apple macOS não é compatível no momento |
   | Ativar local | &quot;Usar idioma do SO&quot; | Configuração padrão |
   | Idioma | Seu idioma preferido | Para interface do Acrobat |
   | Escolher aplicativos - aplicativos disponíveis | Mantenha o Adobe Acrobat nos aplicativos disponíveis. Não Mover para o aplicativo selecionado | Você [baixaria o Adobe Acrobat](#step-6-download-and-install-adobe-acrobat-pro) da página da Adobe Experience League na etapa 6. |
   | Escolher aplicativos - aplicativos selecionados | Manter apenas o arquivo de licença nos aplicativos selecionados | Configuração padrão para implantação de FRL |
   | Plug-ins | Não fazer alterações nesta tela | |
   | Opções | Não fazer alterações nesta tela | |
   | Finalizar | Nome do pacote: &quot;Acrobat FRL AEM Forms&quot; | Usar um nome descritivo |

1. Clique em **Criar** para criar o pacote.

###### Etapa 3: fornecer permissões de download a um usuário

É recomendável criar uma conta de serviço dedicada para gerenciar pacotes de FRL. Se você ainda não tiver uma conta dedicada, siga este [vídeo instrutivo](https://www.youtube.com/watch?v=w8b36YX2TEM&t=59s) para saber como adicionar um novo usuário à sua organização da Adobe.

Depois de ter a conta apropriada, siga estas etapas para conceder permissões de download:

1. Na Admin Console, navegue até a guia **Usuários**.
2. Localize ou crie uma conta de usuário para conceder permissões de download.
3. Clique no nome do usuário para abrir o perfil.
4. Clique no ícone ao lado do usuário **Editar Direitos de Administrador**.
5. Atribua a função de **Administrador de Implantação** ao usuário. Outras funções de administrador também podem funcionar, mas Administrador de implantação é a função recomendada. Clique em **Salvar**.


##### Implantar o pacote de FRL (AEM Forms Server)

As etapas a seguir são executadas no AEM Forms Server, com direitos de *administrador local* sobre a máquina.

###### Etapa 4: faça logon no servidor que executa o AEM Forms como administrador

Acesse o servidor que executa o AEM Forms usando o método apropriado. Verifique se você está usando uma conta com privilégios de administrador local para acessar o servidor.

###### Etapa 5: desinstalar a versão anterior do Acrobat (se houver)

**Crítico:** Faça backup de todas as configurações, perfis ou configurações personalizadas do Acrobat antes de desinstalar.

1. Abra o Painel de Controle do Windows.
2. Navegue até **Configurações** e abra **Aplicativos**.
3. Localize o **Adobe Acrobat** na lista de programas instalados
4. Selecione **Desinstalar** e siga as instruções para remover o aplicativo. Se solicitado, reinicie o servidor
5. Verifique se todas as versões Classic do programa estão desinstaladas. Use a [Ferramenta de Limpeza do Adobe Acrobat](https://helpx.adobe.com/acrobat/kb/remove-reader-dc-acrobat-dc.html) se necessário para concluir a remoção.

###### Etapa 6: baixar e instalar o Adobe Acrobat Pro

Após desinstalar a versão anterior, é necessário baixar e instalar uma versão compatível do Adobe Acrobat Pro:

1. Vá para a [página Downloads do Adobe Acrobat DC](https://helpx.adobe.com/in/acrobat/kb/acrobat-dc-downloads.html).
2. Navegue até a seção **Instalador do Acrobat Pro**.
3. Para uso com o AEM Forms PDF Generator, baixe o instalador &quot;Para Windows (32 bits)&quot;, pois esta é a versão compatível com o AEM Forms PDF Generator.
4. Siga as instruções de instalação na página:
   * Extraia o arquivo zip baixado para uma pasta no seu computador
   * Navegue até o arquivo Setup.exe (não execute o arquivo Setup.exe a partir do arquivo zip)
   * Clique duas vezes em Setup.exe para iniciar a instalação
   * Siga as instruções na tela para concluir a instalação
5. Após a instalação, abra o Adobe Acrobat Pro e conclua a configuração inicial, descartando as caixas de diálogo de boas-vindas.
6. Verifique a instalação criando uma PDF simples.

###### Etapa 7: baixar o pacote FRL

1. Faça logon no [Adobe Admin Console](https://adminconsole.adobe.com/) usando a *conta de usuário* à qual você forneceu permissões de download na Etapa 3.
1. Navegue até a guia **Pacotes**.
1. Localize o pacote de FRL que você criou na Etapa 2 (chamado &quot;Acrobat FRL AEM Forms&quot; ou o nome do pacote personalizado).
1. Clique em **Baixar** para baixar o pacote no servidor.

###### Etapa 8: implantar o pacote

1. **Extrair o Pacote:** Extraia o conteúdo do arquivo ZIP baixado para um diretório no servidor (por exemplo, `C:\AcrobatFRL`). Certifique-se de que o diretório de extração seja facilmente acessível.

2. **Abrir Prompt de Comando como Administrador (Windows):** Clique com o botão direito no botão Iniciar e selecione &quot;Prompt de Comando (Admin)&quot; ou &quot;Windows PowerShell (Admin)&quot;

3. **Navegue até o diretório de extração:**

   ```cmd
   cd C:\AcrobatFRL
   ```

4. **Executar o Comando de Ativação:**

   ```cmd
   # Command syntax
   adobe-licensing-toolkit.exe -p -i -f [JSON_FILE_NAME].json
   
   # Example with actual values
   adobe-licensing-toolkit.exe -p -i -f ngl-preconditioning-data.json
   ```

   > **Importante:**
   > * Substitua `<JSON_FILE_NAME>.json` pelo nome de arquivo *exato* do arquivo JSON no pacote extraído.
   > * O nome de arquivo JSON diferencia maiúsculas de minúsculas.
   > * Verifique se há erros de digitação no nome do arquivo.

   **Saída esperada:**

   ```
   Adobe Licensing Toolkit (1.1.0.130)
   Operation Successfully Completed
   ```

   > ℹ️ **Observação:** o processo de ativação pode levar aproximadamente 30 segundos.

5. **Noções Básicas sobre os Parâmetros de Comando:**

   | Parâmetro | Descrição |
   |-----------|-------------|
   | `-p` | Especifica a plataforma (detecta automaticamente o sistema operacional) |
   | `-i` | Instrui a ferramenta a instalar e ativar a licença |
   | `-f` | Especifica o caminho para o arquivo de licença JSON |

###### Etapa 9: iniciar o servidor do AEM Forms

Após concluir todos os processos, execute um teste de ação rápida para confirmar se a instalação é válida:

1. Inicie o servidor do AEM Forms a partir de um console de linha de comando em uma sessão de usuário interativa. (Faça logon no servidor e inicie manualmente o AEM Forms a partir da linha de comando.)
2. Mantenha a sessão do usuário ativa após iniciar o servidor. Não saia do computador, pois isso encerra o processo do servidor. Você pode fechar com segurança a janela da Área de Trabalho Remota (RDP) sem fazer logoff; o servidor continua a ser executado enquanto a sessão permanecer ativa.
3. Para maior confiabilidade, configure uma tarefa de inicialização ou tarefa agendada para iniciar automaticamente o servidor do AEM Forms quando o usuário fizer logon.

###### Etapa 10: testar o serviço PDF Generator

Após concluir todos os processos, execute um teste de ação rápida para confirmar se a instalação é válida:

1. Abrir a interface do administrador do AEM Forms
2. Navegue até o serviço PDF Generator
3. Tente converter um documento simples do Microsoft Office para o PDF
4. Verifique se a conversão foi concluída com sucesso

#### Verificar versão do Acrobat após ativação de FRL

1. Abra o Adobe Acrobat Pro DC no servidor
2. Acesse Ajuda → Sobre o Adobe Acrobat Pro DC
3. Verifique se o número da versão corresponde à versão esperada
4. Confirmar se o status da licença é exibido como ativado

>[!ENDTABS]



### Desative o modo protegido ao iniciar no Acrobat

Após ativar o FRL (Feature Restricted Licensing) e verificar a ativação do Acrobat, é recomendável desativar o &quot;Modo protegido na inicialização&quot; no Adobe Acrobat para garantir a compatibilidade com o AEM Forms PDF Generator.

Siga estas etapas:

1. Abra o **Adobe Acrobat Pro DC** no servidor.
2. Vá para **Menu** > **Preferências**.
3. Na janela Preferências, selecione **Segurança (aprimorada)** no painel esquerdo.
4. Na seção **Proteções de Sandbox**, **desmarque** a opção **&quot;Habilitar Modo Protegido na inicialização&quot;**.
5. Clique em **Sim** se for solicitada uma confirmação.
6. Clique em **OK** para salvar suas alterações e fechar a janela Preferências.
7. Reinicie o Adobe Acrobat Pro DC para que as alterações entrem em vigor.

>[!NOTE]
>
>A desativação do Modo protegido é necessária para cenários de automação do lado do servidor, como o AEM Forms PDF Generator. Essa configuração só deve ser alterada em ambientes de servidor dedicados, não em desktops de usuários finais.

Para obter mais informações, consulte [documentação do Adobe sobre Modo Protegido](https://helpx.adobe.com/acrobat/kb/protected-mode-troubleshooting-reader.html).



### Configurar variáveis de ambiente {#setup-environment-variables}

Defina variáveis de ambiente para o Java Development Kit de 64 bits, aplicativos de terceiros e Adobe Acrobat. As variáveis de ambiente devem conter o caminho absoluto do executável usado para iniciar o aplicativo correspondente. Por exemplo, a tabela abaixo lista as variáveis de ambiente para alguns aplicativos:

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
   <td><p>C:\Program Files\Java\jdk11</p> </td>
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
   <td><p>Arquivos C:\Program (x86)\OpenOffice 4</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Todas as variáveis de ambiente e os respectivos caminhos fazem distinção entre maiúsculas e minúsculas.
>* JAVA_HOME e Acrobat_PATH (somente Windows) são variáveis de ambiente obrigatórias.
>* A variável de ambiente OpenOffice_PATH está definida como a pasta de instalação em vez do caminho para o executável.
>* Não configure variáveis de ambiente para aplicativos do Microsoft® Office como Word, PowerPoint, Excel e Project, ou para AutoCAD. Se esses aplicativos estiverem instalados no servidor, o serviço Gerar PDF iniciará automaticamente esses aplicativos.
>* Em plataformas baseadas em UNIX, instale o OpenOffice como /root. Se o OpenOffice não estiver instalado como raiz, o serviço PDF Generator não converterá documentos OpenOffice em documentos PDF. Se você precisar instalar e executar o OpenOffice como um usuário não raiz, forneça direitos sudo ao usuário não raiz.
>* Se você estiver usando o OpenOffice em uma plataforma baseada em UNIX, execute o seguinte comando para definir a variável de caminho:\
> `export OpenOffice_PATH=/opt/openoffice.org4`
>* Em plataformas baseadas em SUSE® Linux® (SLES 15 SP6 ou posterior), siga as seguintes etapas para configurar o OpenOffice:
>     * Instale a última variante de 32 bits de `OpenOffice 4.1.x` disponível em um diretório como `/opt/openoffice4`.
>     * Defina a variável de ambiente `OpenOffice_PATH` para apontar para esse local. Por exemplo: `OpenOffice_PATH=/opt/openoffice4`.
>     * Verifique se a variável `OpenOffice_PATH` está definida globalmente (por exemplo, usando `/etc/profile` ou o equivalente específico do sistema) para que esteja disponível para todos os usuários no logon.

### (Somente para IBM® WebSphere®) Configurar o provedor de soquete SSL da IBM® {#only-for-ibm-websphere-configure-ibm-ssl-socket-provider}

Execute as seguintes etapas para configurar o provedor de soquete IBM® SSL:

1. Crie uma cópia do arquivo java.security. O local padrão do arquivo é `[WebSphere_installation_directory]\Appserver\java_[version]\jre\lib\security`.
1. Abra o arquivo java.security copiado para edição.
1. Altere as fábricas de soquetes SSL padrão para usar as fábricas JSSE2 em vez das fábricas IBM® WebSphere® padrão:

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

1. Para permitir que o AEM Forms Server use o arquivo java.security atualizado, ao iniciar o servidor do AEM Forms, adicione o seguinte argumento java:

   `-Djava.security.properties= [path of newly created Java.security file].`

### (Somente para Windows) Definir as configurações de bloco de arquivo do Microsoft® Office {#configure-the-file-block-settings-for-microsoft-office}

Altere as configurações da central de confiança do Microsoft® Office para habilitar o serviço PDF Generator para converter arquivos criados com versões mais antigas do Microsoft® Office.

1. Abra um aplicativo do Microsoft® Office. Por exemplo, Microsoft® Word. Navegue até **[!UICONTROL Arquivo]**> **[!UICONTROL Opções]**. A caixa de diálogo de opções é exibida.

1. Clique em **[!UICONTROL Central de Confiabilidade]** e em **[!UICONTROL Configurações da Central de Confiabilidade]**.
1. Nas **[!UICONTROL configurações da Central de Confiabilidade]**, clique em **[!UICONTROL Configurações de Bloqueio de Arquivo]**.
1. Na lista **[!UICONTROL Tipo de Arquivo]**, desmarque **[!UICONTROL Abrir]** para o tipo de arquivo que o serviço PDF Generator deve ter permissão para converter em documentos do PDF.

### (Somente Windows) Conceder o privilégio Substituir um token de nível de processo {#grant-the-replace-a-process-level-token-privilege}

A conta de usuário usada para iniciar o servidor de aplicativos requer o privilégio **Substituir um token de nível de processo**. Por padrão, a conta do sistema local tem o privilégio **Substituir um token de nível de processo**. Para os servidores executados com um usuário do grupo Administradores locais, o privilégio deve ser concedido explicitamente. Execute as seguintes etapas para conceder o privilégio:

1. Abra o Editor de Diretiva de Grupo para Microsoft® Windows. Para abrir o Editor de Diretiva de Grupo, clique em **[!UICONTROL Iniciar]**, digite **gpedit.msc** na caixa Iniciar Pesquisa e clique em **[!UICONTROL Editor de Diretiva de Grupo]**.
1. Navegue até **[!UICONTROL Política do Computador Local]** > **[!UICONTROL Configuração do Computador]** > **[!UICONTROL Configurações do Windows]** > **[!UICONTROL Configurações de Segurança]** > **[!UICONTROL Políticas Locais]** > **[!UICONTROL Atribuição de Direitos de Usuário]** e edite a política **[!UICONTROL Substituir um token de nível de processo]** e inclua o grupo Administradores.
1. Adicione o usuário à entrada Substituir um token no nível do processo.

>[!NOTE]
>
> Como implicado acima, se o servidor do AEM estiver sendo executado como um serviço na conta LocalSystem (LSA), não será necessário atribuir explicitamente esse privilégio a um usuário.

### (Somente para Windows) Habilitar o serviço PDF Generator para não administradores {#enable-the-pdf-generator-service-for-non-administrators}

Você pode permitir que um usuário não administrador use o serviço do PDF Generator. Normalmente, somente usuários com privilégios administrativos podem usar o serviço:

1. Crie uma variável de ambiente, PDFG_NON_ADMIN_ENABLED.
1. Defina o valor da variável de ambiente como TRUE.
1. Reinicie a instância do AEM Forms.

>[!NOTE]
>
> É recomendável usar o comando &#39;Ctrl + C&#39; para reiniciar o SDK. Reiniciar o AEM SDK usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

### (Somente para Windows) Desabilitar o UAC (Controle de Conta de Usuário) {#disable-user-account-control-uac}

1. Para acessar o Utilitário de Configuração do Sistema, vá para **[!UICONTROL Iniciar > Executar]** e digite **[!UICONTROL MSCONFIG]**.
1. Clique na guia **[!UICONTROL Ferramentas]**, role para baixo e selecione **[!UICONTROL Alterar Configurações de UAC]**. Clique em **[!UICONTROL Iniciar]** para executar o comando em uma nova janela.
1. Ajuste o controle deslizante para o nível Nunca notificar. Quando terminar, feche a janela de comando e a janela Configuração do sistema.
1. Verifique se a configuração do Registro para UAC está definida como 0 (zero). Execute as seguintes etapas para verificar:

   1. A Microsoft® recomenda fazer backup do registro antes de modificá-lo. Para obter etapas detalhadas, consulte [Como fazer backup e restaurar o Registro no Windows](https://support.microsoft.com/en-us/help/322756).
   1. Abra o editor de Registro do Microsoft® Windows. Para abrir o editor de registro, vá para Iniciar > Executar, digite regedit e clique em OK.
   1. Navegue até `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\`. Verifique se o valor de EnableLUA está definido como 0 (zero).
   1. Verifique se o valor de **EnableLUA** está definido como 0 (zero). Se o valor não for 0, altere o valor para 0. Feche o editor de Registro.

1. Reinicie o computador.

### (Somente para Windows) Desabilitar o Serviço de Relatório de Erros {#disable-error-reporting-service}

Ao converter um documento para o PDF usando o serviço PDF Generator no Windows Server, ocasionalmente, o Windows Server relata que o executável encontrou um problema e deve ser fechado. No entanto, isso não afeta a conversão do PDF, pois continua em segundo plano.

Para evitar o recebimento do erro, você pode desativar o relatório de erros do Windows. Para obter mais informações sobre como desativar o relatório de erros, consulte [https://technet.microsoft.com/en-us/library/cc754364.aspx](https://technet.microsoft.com/en-us/library/cc754364.aspx).

### (Somente para Windows) Configurar a conversão do HTML para o PDF {#configure-html-to-pdf-conversion}

O serviço PDF Generator fornece rotas ou métodos WebKit, WebCapture e WebToPDF para converter arquivos HTML em documentos PDF. No Windows, para habilitar a conversão para rotas WebKit e Acrobat WebCapture, copie a fonte Unicode para o diretório %windir%\fonts.

>[!NOTE]
>
>Sempre que você instalar novas fontes na pasta de fontes, reinicie a instância do AEM Forms.

### (Somente plataformas baseadas em UNIX) Configurações adicionais para conversão do HTML em PDF  {#extra-configurations-for-html-to-pdf-conversion}

Em plataformas baseadas em UNIX, o serviço PDF Generator oferece suporte a rotas WebKit e WebToPDF para conversão de arquivos HTML em documentos PDF. Para habilitar a conversão do HTML em PDF, execute as seguintes configurações, aplicáveis à rota de conversão de sua preferência:

### (Somente plataformas baseadas em UNIX) Habilitar suporte para fontes Unicode (somente WebKit) {#enable-support-for-unicode-fonts-webkit-only}

Copie a fonte Unicode para qualquer um dos seguintes diretórios, conforme apropriado para o seu sistema:

* /usr/lib/X11/fonts/TrueType
* /usr/share/fonts/default/TrueType
* /usr/X11R6/lib/X11/fonts/ttf
* /usr/X11R6/lib/X11/fonts/truetype
* /usr/X11R6/lib/X11/fonts/TrueType
* /usr/X11R6/lib/X11/fonts/TTF
* /usr/openwin/lib/X11/fonts/TrueType (Solaris™)

>[!NOTE]
>
>* No Red Hat® Enterprise Linux® 6.x e versões posteriores, as fontes courier não estão disponíveis. Para instalar as fontes do courier, baixe o arquivo font-ibm-type1-1.0.3.zip. Extraia o arquivo em /usr/share/fonts. Crie um link simbólico de /usr/share/X11/fonts para /usr/share/fonts.
>* Exclua todos os arquivos de cache de fontes .lst dos diretórios Html2PdfSvc/bin e /usr/share/fonts.
>* Verifique se os diretórios /usr/lib/X11/fonts e /usr/share/fonts existem. Se os diretórios não existirem, use o comando ln para criar um link simbólico de /usr/share/X11/fonts para /usr/lib/X11/fonts e outro link simbólico de /usr/share/fonts para /usr/share/X11/fonts. Verifique também se as fontes do courier estão disponíveis em /usr/lib/X11/fonts.
>* Verifique se todas as fontes (Unicode e não-unicode) estão disponíveis no diretório /usr/share/fonts ou /usr/share/X11/fonts.
>* Quando você executa o serviço PDF Generator como um usuário não-raiz, forneça a ele acesso de leitura e gravação a todos os diretórios de fontes.
>* Sempre que você instalar novas fontes na pasta de fontes, reinicie a instância do AEM Forms.
>

## Instalar pacote complementar do AEM Forms {#install-aem-forms-add-on-package}

O pacote complementar do AEM Forms é um aplicativo implantado no AEM. O pacote contém os Serviços de documento da AEM Forms e outros recursos do AEM Forms. Execute as seguintes etapas para instalar o pacote:

1. Abra a [Distribuição de softwares](https://experience.adobe.com/downloads). Você precisa de uma Adobe ID para fazer logon na Distribuição de softwares.
1. Selecione **[!UICONTROL Adobe Experience Manager]**, disponível no menu de cabeçalho.
1. Na seção **[!UICONTROL Filtros]**:
   1. Selecione **[!UICONTROL Forms]** na lista suspensa **[!UICONTROL Solução]**.
   2. Selecione a versão e o tipo do pacote. Você também pode usar a opção **[!UICONTROL Downloads de Pesquisa]** para filtrar os resultados.
1. Selecione o nome do pacote aplicável ao seu sistema operacional, selecione **[!UICONTROL Aceitar termos do EULA]** e selecione **[!UICONTROL Baixar]**.
1. Abra o [Gerenciador de Pacotes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html) e clique em **[!UICONTROL Carregar Pacote]** para carregar o pacote.
1. Selecione o pacote e clique em **[!UICONTROL Instalar]**.

   Você também pode baixar o pacote através do link direto listado no artigo [versões do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

1. Depois que o pacote for instalado, você será solicitado a reiniciar a instância do AEM. **Não interromper imediatamente o servidor.** Antes de parar o AEM Forms Server, aguarde até que as mensagens ServiceEvent REGISTERED e ServiceEvent UNREGISTERED parem de aparecer no arquivo `[AEM-Installation-Directory]/crx-quickstart/logs/error`.log e o log fique estável.

## Configurações pós-instalação {#post-installation-configurations}

### Configurar delegação de inicialização para bibliotecas RSA/BouncyCastle  {#configure-boot-delegation-for-rsa-bouncycastle-libraries}

1. Pare a instância do AEM. Navegue até a [pasta de instalação do AEM]\crx-quickstart\conf\. Abra o arquivo sling.properties para edição.

   Se você usar `[AEM installation directory]\crx-quickstart\bin\start.bat` para iniciar uma instância do AEM, edite o sling.properties localizado em `[AEM_root]\crx-quickstart\`.

1. Adicione as seguintes propriedades ao arquivo sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. (Somente no AIX®) Adicione as seguintes propriedades ao arquivo sling.properties:

   ```shell
   sling.bootdelegation.xerces=org.apache.xerces.*
   ```

1. Salvar e fechar o arquivo.

### Configurando o serviço gerenciador de fontes  {#configuring-the-font-manager-service}

1. Faça logon no [AEM Configuration Manager](http://localhost:4502/system/console/configMgr) como administrador.
1. Localize e abra o serviço **[!UICONTROL CQ-DAM-Handler-Gibson Font Managers]**. Especifique o caminho dos diretórios Fontes do sistema, Fontes do servidor do Adobe e Fontes do cliente. Clique em **[!UICONTROL Salvar]**.

   >[!NOTE]
   >
   >Seu direito de usar fontes fornecidas por terceiros que não sejam a Adobe é regido pelos contratos de licença fornecidos a você por esses terceiros com essas fontes e não está coberto pela sua licença para usar o software da Adobe. A Adobe recomenda que você revise e garanta que esteja em conformidade com todos os contratos de licença não-Adobe aplicáveis antes de usar fontes que não sejam da Adobe com o software da Adobe, especialmente no que diz respeito ao uso de fontes em um ambiente de servidor.
   >Ao instalar novas fontes na pasta fontes, reinicie a instância do AEM Forms.
   >

### Configurar uma conta de usuário local para executar o serviço PDF Generator  {#configure-a-local-user-account-to-run-the-pdf-generator-service}

Uma conta de usuário local é necessária para executar o serviço PDF Generator. Para obter as etapas para criar um usuário local, consulte [Criar uma conta de usuário no Windows](https://support.microsoft.com/en-us/help/13951/windows-create-user-account) ou criar uma conta de usuário em plataformas baseadas em UNIX.

1. Abra a página [Configuração do AEM Forms PDF Generator](http://localhost:4502/libs/fd/pdfg/config/ui.html).

1. Na guia **[!UICONTROL Contas de Usuário]**, forneça as credenciais de uma conta de usuário local e clique em **[!UICONTROL Enviar]**. Se o Microsoft® Windows solicitar, permita o acesso ao usuário. Quando adicionado com êxito, o usuário configurado é exibido na seção **[!UICONTROL Suas contas de usuário]** da guia **[!UICONTROL Contas de Usuário]**.

### Definir as configurações de tempo limite {#configure-the-time-out-settings}

1. No [AEM configuration manager](http://localhost:4502/system/console/configMgr), localize e abra o serviço **[!UICONTROL Provedor ORB Jacorb]**.

   Adicione o seguinte ao campo **[!UICONTROL Propriedades personalizadas.nome]** e clique em **[!UICONTROL Salvar]**. Ele define o tempo limite de resposta pendente (também conhecido como, tempo limite do cliente CORBA) como 600 segundos.

   `jacorb.connection.client.pending_reply_timeout=600000`

1. Faça logon na instância de autor do AEM e navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Ferramentas]** > **[!UICONTROL Forms]** > **[!UICONTROL Configurar PDF Generator]**. A URL padrão é <http://localhost:4502/libs/fd/pdfg/config/ui.html>.

   Abra a guia **[!UICONTROL Configuração Geral]** e modifique o valor dos seguintes campos para seu ambiente:

<table>
 <tbody>
  <tr>
   <td>Texto</td>
   <td>Descrição</td>
   <td>Valor padrão</td>
  </tr>
  <tr>
   <td>Tempo limite da conversão do servidor</td>
   <td>Uma conversão PDFG permanece ativa pelo número de segundos definidos no tempo limite de Conversão do servidor</td>
   <td>270 segundos<br /> </td>
  </tr>
  <tr>
   <td>Segundos para exploração de limpeza do PDFG</td>
   <td>O número de segundos necessários para executar operações pós-conversão.<br /> </td>
   <td>3600 segundos</td>
  </tr>
  <tr>
   <td>Segundos para expiração da tarefa</td>
   <td>Duração para a qual o serviço PDF Generator tem permissão para executar uma conversão. Verifique se o valor de Segundos para expiração da tarefa é maior que o valor de Segundos para varredura de limpeza do PDFG.</td>
   <td>7200 segundos</td>
  </tr>
 </tbody>
</table>

### (Somente para Windows) Configurar o Acrobat para o serviço PDF Generator {#configure-acrobat-for-the-pdf-generator-service}

No Microsoft® Windows, o serviço PDF Generator usa o Adobe Acrobat para converter formatos de arquivo suportados em um documento PDF. Execute as seguintes etapas para configurar o Adobe Acrobat para o serviço PDF Generator:

1. Abra o Acrobat e selecione **[!UICONTROL Editar]**> **[!UICONTROL Preferências]**> **[!UICONTROL Atualizador]**. Em Verificar atualizações, desmarque **[!UICONTROL Instalar atualizações automaticamente]** e clique em **[!UICONTROL OK]**. Feche o Acrobat.
1. Clique duas vezes em um documento do PDF no sistema. Quando o Acrobat é iniciado pela primeira vez, as caixas de diálogo para logon, tela de boas-vindas e EULA são exibidas. Ignore essas caixas de diálogo para todos os usuários configurados para usar o PDF Generator.
1. Execute o arquivo em lote do utilitário PDF Generator para configurar o Acrobat para o serviço PDF Generator:

   1. Abra o [Gerenciador de Pacotes do AEM](http://localhost:4502/crx/packmgr/index.jsp) e baixe o arquivo `adobe-aemfd-pdfg-common-pkg-[version].zip` do Gerenciador de Pacotes.
   1. Descompacte o arquivo .zip baixado. Abra o prompt de comando com privilégios administrativos.
   1. Navegue até `[extracted-zip-file]\jcr_root\etc\packages\day\cq60\fd\adobe-aemds-common-pkg-[version]\jcr_root\etc\packages\day\cq60\fd\`
   1. Descompacte o `adobe-aemfd-pdfg-common-pkg-[version]`.
   1. Navegue até o diretório `[downloaded-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]`. Execute o seguinte arquivo de lote:

      `Acrobat_for_PDFG_Configuration.bat`

      O Acrobat está configurado para ser executado com o serviço PDF Generator.

1. Execute a [Ferramenta de Preparação do Sistema (SRT)](#SRT) para validar a instalação do Acrobat.


### (Somente para Windows) Configurar a rota principal para conversão do HTML em PDF {#configure-primary-route-for-html-to-pdf-conversion-windows-only}

O serviço PDF Generator fornece várias rotas para converter arquivos HTML em documentos PDF: Webkit, Acrobat WebCapture (somente Windows) e WebToPDF. A Adobe recomenda usar a rota WebToPDF porque ela tem a capacidade de lidar com conteúdo dinâmico e não tem dependências em bibliotecas de 32 bits ou não requer fontes extras. Além disso, a rota WebToPDF não requer acesso sudo ou root para executar a conversão.

A rota principal padrão para a conversão do HTML para o PDF é o Webkit. Para alterar o roteiro de conversão:

1. Na instância do autor do AEM, navegue até **[!UICONTROL Ferramentas]**> **[!UICONTROL Forms]**> **[!UICONTROL Configurar PDF Generator]**.

1. Na guia **[!UICONTROL Configuração Geral]**, selecione a rota de conversão preferencial na lista suspensa **[!UICONTROL Rota Primária para conversões do HTML para o PDF]**.

### Inicializar armazenamento global de confiança {#intialize-global-trust-store}

Usando o Gerenciamento de Armazenamento Confiável, você pode importar, editar e excluir certificados confiáveis no servidor para validação de assinaturas digitais e autenticação de certificado. É possível importar e exportar qualquer número de certificados. Após importar um certificado, você poderá editar as configurações de confiança e o tipo de armazenamento de confiança. Execute as seguintes etapas para inicializar um armazenamento de confiança:

1. Faça logon na instância do AEM Forms como administrador.
1. Vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Armazenamento de Confiança]**.
1. Clique em **[!UICONTROL Criar TrustStore]**. Defina a senha e selecione **[!UICONTROL Salvar]**.

### Configurar certificados para o serviço de criptografia e extensão do Reader {#set-up-certificates-for-reader-extension-and-encryption-service}

O serviço DocAssurance pode aplicar direitos de uso a documentos do PDF. Para aplicar direitos de uso a documentos do PDF, configure os certificados.

Antes de configurar os certificados, verifique se você tem:

* Arquivo de certificado (.pfx).

* Senha da chave de privacidade fornecida com o certificado.

* Alias da chave de privacidade. Você pode executar o comando Java keytool para exibir o Alias da chave de privacidade:
  `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

* Senha do arquivo de armazenamento de chave. Se você estiver usando o certificado Reader Extensions da Adobe, a senha do arquivo do Keystore será sempre a mesma da senha da chave privada.

Execute as seguintes etapas para configurar os certificados:

1. Faça logon na instância do AEM Author como administrador. Vá para **[!UICONTROL Ferramentas]** > **[!UICONTROL Segurança]** > **[!UICONTROL Usuários]**.
1. Clique no campo **[!UICONTROL nome]** da conta de usuário. A página **[!UICONTROL Editar configurações do usuário]** é aberta. Na instância do autor do AEM, os certificados residem em um KeyStore. Se você não criou um KeyStore anteriormente, clique em **[!UICONTROL Criar KeyStore]** e defina uma nova senha para o KeyStore. Se o servidor já contiver um KeyStore, ignore esta etapa.  Se você estiver usando o certificado Reader Extensions da Adobe, a senha do arquivo do Keystore será sempre a mesma da senha da chave privada.
1. Na página **[!UICONTROL Editar Configurações de Usuário]**, selecione a guia **[!UICONTROL KeyStore]**. Expanda a opção **[!UICONTROL Adicionar Chave Privada do arquivo de Armazenamento de Chave]** e forneça um alias. O alias é usado para executar a operação de extensões do Reader.
1. Para carregar o arquivo de certificado, clique em **[!UICONTROL Selecionar Arquivo de Repositório de Chaves]** e carregue um arquivo &lt;filename>.pfx.

   Adicione a **[!UICONTROL Senha da Chave de Armazenamento]**, a **[!UICONTROL Senha da Chave Privada]** e o **[!UICONTROL Alias da Chave Privada]** associados ao certificado nos respectivos campos. Clique em **[!UICONTROL Enviar]**.

   >[!NOTE]
   >
   >No ambiente de produção, substitua suas credenciais de avaliação pelas credenciais de produção. Exclua suas credenciais antigas do Reader Extensions antes de atualizar uma credencial expirada ou de avaliações.

1. Clique em **[!UICONTROL Salvar e fechar]** na página **[!UICONTROL Editar configurações de usuário]**.

### Ativar AES-256 {#enable-aes}

Para usar a criptografia AES 256 para arquivos PDF, obtenha e instale os arquivos Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy. Substitua os arquivos local_policy.jar e US_export_policy.jar na pasta jre/lib/security. Por exemplo, se você estiver usando o Sun JDK, copie os arquivos baixados para a pasta `[JAVA_HOME]/jre/lib/security`.

O serviço do Assembler depende do serviço Reader Extensions, do serviço Signature, do serviço Forms e do serviço Output. Execute as seguintes etapas para verificar se os serviços necessários estão em execução:

1. Faça logon na URL `https://'[server]:[port]'/system/console/bundles` como administrador.
1. Pesquise no serviço a seguir e verifique se os serviços estão em funcionamento:

<table>
 <tbody>
  <tr>
   <th>Nome do serviço</th>
   <th>Nome do pacote</th>
  </tr>
  <tr>
   <td>Serviço de assinaturas</td>
   <td>adobe-aemfd-signatures</td>
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

### (Somente para Windows) Configure a entrada de registro para o Projeto Microsoft® {#configure-registry-entry-for-microsoft-project}

Depois de instalar o complemento AEM Forms e o Microsoft® Project na sua máquina, registre uma entrada para o Microsoft® Project no local de 64 bits. Ele facilita a execução de testes de conversões de Project para PDFG. Veja a seguir as etapas que descrevem o processo de entrada de registro:

1. Abra o editor do Registro do Microsoft® Windows (regedit). Para abrir o editor do Registro, vá para Iniciar > Executar, digite regedit e clique em OK.
1. Navegue até `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Adobe\Acrobat PDFMaker\<version>\Office\SupportedApp`, crie um novo Registro de **Valor Binário** e renomeie-o para **Projeto**.
1. Modifique o valor de dados do Registro binário criado para 01 e clique em OK.
1. Feche a entrada do Registro.


## Problemas conhecidos e solução de problemas {#known-issues-and-troubleshooting}

* A conversão de HTML para PDF falha se um arquivo de entrada compactado contiver arquivos HTML com caracteres de byte duplo em nomes de arquivo. Para evitar esse problema, não use caracteres de byte duplo ao nomear arquivos HTML.

* Em sistemas operacionais baseados em UNIX, faça o seguinte para localizar bibliotecas ausentes:

1. Vá até `[crx-repository]/bedrock/svcnative/HtmlToPdfSvc/bin/`.

1. Execute o comando a seguir para listar todas as bibliotecas que o WebToPDF requer para a conversão do HTML em PDF.

   `ldd phantomjs`

   Execute o seguinte comando para listar as bibliotecas ausentes.

   `ldd phantomjs | grep not`

1. Instale manualmente as bibliotecas ausentes.

## SRT (System Readiness Tool, ferramenta de preparação do sistema) {#SRT}

A [Ferramenta de Preparação do Sistema](#srt-configuration) verifica se o computador está configurado corretamente para executar conversões do PDF Generator. A ferramenta gera o relatório no caminho especificado. Para executar a ferramenta:

1. Abra o prompt de comando. Navegue até a pasta `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools`.

1. Execute o seguinte comando no prompt de comando:

   `java -jar forms-srt-[version].jar [Path_of_reports_folder] en`

   O comando gera o relatório e também cria o arquivo srt_config.yaml. Você pode usá-lo para configurar opções para a ferramenta SRT. É opcional configurar opções para a ferramenta SRT.

   >[!NOTE]
   >
   >* Se a Ferramenta de preparação do sistema relatar que o arquivo pdfgen.api não está disponível na pasta de plug-ins do Acrobat, copie o arquivo pdfgen.api do diretório `[extracted-adobe-aemfd-pdfg-common-pkg]\jcr_root\libs\fd\pdfg\tools\adobe-aemfd-pdfg-utilities-[version]\plugins\x86_win32` para o diretório `[Acrobat_root]\Acrobat\plug_ins`.

1. Navegue até `[Path_of_reports_folder]`. Abra o arquivo SystemReadinessTool.html. Verifique o relatório e corrija os problemas mencionados.

### Configuração de opções para a ferramenta SRT {#srt-configuration}

Você pode usar o arquivo srt_config.yaml para definir várias configurações para a ferramenta SRT. O formato do arquivo é:

```shell
   # =================================================================
   # SRT Configuration
   # =================================================================
   #Note - follow correct format to avoid parsing failures
   #for example, <param name>:<space><param value> 
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

* **Localidade:** É um parâmetro obrigatório. É compatível com inglês (en), alemão (de), francês (fr) e japonês (ja). O valor padrão é en. Isso não afeta os serviços do PDF Generator em execução no AEM Forms no OSGi.
* **aemTempDir:** é um parâmetro opcional. Especifica o local de armazenamento temporário do Adobe Experience Manager.
* **usuários:** é um parâmetro opcional. Você pode especificar um usuário para verificar se ele tem as permissões necessárias e o acesso de leitura/gravação nos diretórios necessários para executar o PDF Generator. Se nenhum usuário for especificado, as verificações específicas do usuário serão ignoradas e exibidas como falha no relatório.
* **outputDir:** especifique o local para salvar o relatório SRT. O local padrão é o diretório de trabalho atual da ferramenta SRT.

## Resolução de problemas

Se você enfrentar problemas mesmo depois de corrigir todos os problemas relatados pela ferramenta SRT, execute as seguintes verificações:

Antes de executar as seguintes verificações, verifique se a [Ferramenta de Preparação do Sistema](#SRT) não relata erros.

+++ Adobe Acrobat

* Verifique se apenas a [versão com suporte](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) do Microsoft® Office (32 bits) e do Adobe Acrobat está instalada e se as caixas de diálogo de abertura foram canceladas.
<!-- (Acrobat 2020 only) Ensure that Adobe Acrobat Update Service is disabled. -->
* Verifique se o arquivo de lote [Acrobat_for_PDFG_Configuration.bat](#configure-acrobat-for-the-pdf-generator-service) foi executado com privilégios de administrador.
* Verifique se um usuário do PDF Generator foi adicionado na interface de configuração do PDF.
* Verifique se a permissão [Substituir um token de nível de processo](#grant-the-replace-a-process-level-token-privilege) foi adicionada para o usuário do PDF Generator.
* Verifique se o suplemento Acrobat PDFMaker Office COM está ativado para os aplicativos do Microsoft Office.

+++

+++OpenOffice

**Microsoft® Windows**

* Verifique se a [versão com suporte](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) de 32 bits do Microsoft Office está instalada e se as caixas de diálogo de abertura foram canceladas para todos os aplicativos.
* Verifique se um usuário do PDF Generator foi adicionado na interface de configuração do PDF.
* Verifique se o usuário do PDF Generator é membro do grupo de administradores e se o privilégio [Substituir um token de nível de processo](#grant-the-replace-a-process-level-token-privilege) está definido para o usuário.
* Verifique se o usuário está configurado na interface do usuário do PDF Generator e execute as seguintes ações:
   1. Faça login no Microsoft® Windows com o usuário do PDF Generator.
   1. Abra os aplicativos do Microsoft® Office ou OpenOffice e cancele todas as caixas de diálogo.
   1. Defina Adobe PDF como impressora padrão.
   1. Defina o Acrobat como programa padrão para arquivos PDF.
   1. Execute a conversão manual usando as opções Arquivo > Imprimir e faixa de opções do Acrobat nos aplicativos do Microsoft Office e cancele todas as caixas de diálogo.
   1. Encerre todos os processos relacionados à conversão, como winword.exe, powerpoint.exe e excel.exe.
   1. Reinicie o servidor do AEM Forms.

**Linux®**

* Instale a [versão com suporte](aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator) do OpenOffice. O AEM Forms é compatível com versões de 32 e 64 bits. Após a instalação, abra todos os aplicativos OpenOffice, cancele todas as janelas de diálogo e feche os aplicativos. Reabra os aplicativos e verifique se nenhuma caixa de diálogo é exibida ao abrir um aplicativo OpenOffice.

* Crie uma variável de ambiente `OpenOffice_PATH` e defina-a para apontá-la para que a instalação do OpenOffice seja definida no [console](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/) ou no perfil dt (Árvore de Dispositivo).
* Se houver problemas na instalação do OpenOffice, verifique se as [bibliotecas de 32 bits](#extrarequirements) necessárias para a instalação do OpenOffice estão disponíveis.

+++

+++Problemas de conversão do HTML para o PDF

* Verifique se os diretórios de fontes foram adicionados na interface de configuração do PDF Generator.

**Linux e Solaris (rota de conversão WebToPDF)**

* Verifique se a biblioteca de 32 bits está disponível (libicudata.so.42) para conversão de HTMLToPDF baseada em Webkit e se as bibliotecas de 64 bits (libicudata.so.42 libs estão disponíveis para conversão de HTMLToPDF baseada em WebToPDF.

* Execute o seguinte comando para listar as bibliotecas ausentes para WebToPDF:

  ```
  ldd phantomjs | grep not
  ```

**Linux® e Solaris™ (rota de conversão do WebKit)**

* Verifique se os diretórios `/usr/lib/X11/fonts` e `/usr/share/fonts` existem. Se os diretórios não existirem, crie um link simbólico de `/usr/share/X11/fonts` a `/usr/lib/X11/fonts` e outro link simbólico de `/usr/share/fonts` a `/usr/share/X11/fonts`.

  ```
  ln -s /usr/share/fonts /usr/share/X11/fonts
  
  ln -s /usr/share/X11/fonts /usr/lib/X11/fonts
  ```

* Verifique se as fontes do IBM são copiadas em usr/share/fonts.
* Verifique se a correção de vulnerabilidade de fantasma glibc está disponível na máquina. Use seu gerenciador de pacotes padrão para atualizar para a versão mais recente do glibc. Ele inclui a correção de vulnerabilidade de fantasma.
* Verifique se as versões mais recentes das bibliotecas lib curl, libcrypto e libssl de 32 bits estão instaladas no sistema. Crie também symlinks `/usr/lib/libcurl.so` (ou libcurl.a para AIX®), `/usr/lib/libcrypto.so` (ou libcrypto.a para AIX®) e `/usr/lib/libssl.so` (ou libssl.a para AIX®) apontando para as versões mais recentes (32 bits) das respectivas bibliotecas.

* Execute as seguintes etapas para o Provedor de soquete IBM® SSL:
   1. Copie o arquivo java.security de `<WAS_Installed_JAVA>\jre\lib\security` para qualquer local no AEM Forms Server. O local padrão é Local Padrão = `<WAS_Installed>\Appserver\java_[version]\jre\lib\security`.

   1. Edite o arquivo java.security no local copiado e altere as fábricas padrão do SSL Socket com fábricas JSSE2 (use fábricas JSSE2 em vez do WebSphere®).

      Altere as seguintes fábricas de soquetes JSSE padrão:

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

<!-- +++ Unable to add a PDF Generator (PDFG) user

* (Acrobat 2020 only) Ensure Microsoft&reg; Visual C++ 2012 x86 and Microsoft&reg; Visual C++ 2013 x86 (32-bit) redistributable are installed on Windows.

+++
-->
+++Falhas no teste de automação

* Para o Microsoft® Office e OpenOffice, execute pelo menos uma conversão manualmente (como cada usuário) para garantir que nenhuma caixa de diálogo seja exibida durante a conversão. Se alguma caixa de diálogo for exibida, a descartará. Nenhuma caixa de diálogo deve aparecer durante a conversão automática.

* Antes de executar a automação em um ambiente AEM Forms no OSGi, verifique se o pacote de teste está instalado e ativo.

+++

<!-- +++ (Acrobat 2020 only) Multiple user conversion failures 

* Verify the server logs to check if the conversion is failing for a particular user.(Process Explorer can help you check running process for different users)

* Ensure that the user configured for PDF Generator has local admin rights.

* Ensure that PDF Generator user has read, write, and execute permissions on LC temp and PDFG temp users.

* For Microsoft&reg; Office and OpenOffice, perform at least one conversion manually (as each user) to ensure that no dialogue pops up during conversion. If any dialogue appears, dismissed it. No such dialogue should appear during automated conversion.

* Perform a sample conversion.

+++ -->

<!-- (Acrobat 2020 only) License of Adobe Acrobat installed on AEM Forms Server expires

* If you have an existing license of Adobe Acrobat and it has expired, [Download the latest version of Adobe Application Manager](https://helpx.adobe.com/in/creative-suite/kb/aam-troubleshoot-download-install.html), and migrating your serial number. Before [migrating your serial number](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number).

   * Use the following commands to generate prov.xml and reserialize the existing install using the prov.xml file instead of commands provided in [migrating your serial number](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/licensing.html#migrating-your-serial-number) number article.

      ```

         adobe_prtk --tool=VolumeSerialize --generate --serial=<serialnum> [--leid=<LEID>] [--regsuppress=ss] [--eulasuppress] [--locales=limited list of locales in xx_XX format or ALL>] [--provfile=<Absolute path to prov.xml>]

      ```

   * Volume serialize the package (Re-serialize the existing install using the prov.xml file and the new serial): Run the following command from the PRTK installation folder as an administrator to serialize and activate the deployed packages on client machines:

      ```
         adobe_prtk --tool=VolumeSerialize --provfile=C:\prov.xml –stream
         
      ```

* For large-scale installations, use the [Acrobat Customization Wizard](https://www.adobe.com/devnet-docs/acrobatetk/tools/Wizard/index.html) to remove previous versions of Reader and Acrobat. Customize the installer and deploy it to all the machines of your organization.

(Acrobat 2020 only) AEM Forms Server is in an offline or secure environment and internet is not available to activate Acrobat.

* You can go online within 7 days of the first launch of your Adobe product to complete an online activation and registration or use an internet-enabled device and your product's serial number to complete this process. For detailed instructions, see [Offline Activation](https://exception.licenses.adobe.com/aoes/aoes/v1/t1?locale=en).

+++ -->

+++ Não é possível converter o arquivo do Word ou Excel em PDF no Windows Server

Quando o usuário tenta converter arquivos do Word ou Excel para o PDF no Microsoft Windows Server, o seguinte erro é encontrado como:

*Mensagem de erro do conversor primário:
ALC-PDG-015-003-O sistema não pode abrir o arquivo de entrada. Envie seu arquivo novamente ou contate o administrador do sistema.*

Para resolver o problema, consulte [Não é possível converter o arquivo do Word ou Excel para o PDF no Windows Server](/help/forms/using/disable-uac-for-pdfgconfiguration.md).

+++

+++ Não é possível converter arquivos do Excel para PDF no Windows Server 2019

Ao converter o Microsoft Excel 2019 para PDF no Microsoft Windows Server 2019, você deve garantir o seguinte:

* Ao usar o serviço PDF Generator, o computador com Windows não deve ter nenhuma conexão remota ativa com o servidor do AEM (sessão do Windows RDP).
* A impressora padrão deve ser definida como Adobe PDF.

  >[!NOTE]
  >* Para o Apple macOS e o Ubuntu OS, não é necessário definir as configurações acima.

+++

+++ Não é possível converter arquivos XPS em PDFs

Para resolver o problema, [crie uma chave do Registro específica para o recurso no Windows](https://helpx.adobe.com/in/acrobat/kb/unable-convert-xps-to-pdfs.html).

+++


## Próximas etapas {#next-steps}

Você tem um ambiente de serviços de documento da AEM Forms em funcionamento. Você pode usar serviços de documento por meio de:

* [Fluxos de trabalho centrados em formulários no OSGi](/help/forms/using/aem-forms-workflow.md)
* [Pastas monitoradas](/help/forms/using/watched-folder-in-aem-forms.md)
* [APIs de serviços de documento](/help/forms/using/aem-document-services-programmatically.md)
