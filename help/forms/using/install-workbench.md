---
title: Instalar workbench
seo-title: Instalar workbench
description: Instale o workbench.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '2246'
ht-degree: 0%

---


# Instalar o Workbench {#install-workbench}

Este documento fornece instruções para a instalação e configuração do AEM Forms Workbench. O programa de instalação também instala o Forms Designer.

## Who should read this document? {#who-should-read-this-doc}

Este documento destina-se a administradores ou desenvolvedores responsáveis pela instalação, configuração, administração ou implantação do Workbench. Também estão incluídas as informações necessárias para configurar seu sistema para suportar seus processos AEM Forms atualizados. As informações fornecidas baseiam-se no pressuposto de que qualquer pessoa que leia este documento está familiarizada com o sistema operacional Microsoft® Windows®.

## Informações adicionais {#additional-information}

Os recursos nesta tabela podem ajudá-lo a saber mais sobre isso e começar a usar o AEM Forms.
<table>
 <tbody>
  <tr>
   <td><p><strong>Para obter informações sobre</strong></p> </td>
   <td><p><strong>Consulte</strong></p> </td>
  </tr>
  <tr>
   <td><p>Informações processuais para o Workbench</p> </td>
   <td><p><a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Ajuda do Workbench</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Informações gerais sobre a AEM Forms e como ela se integra a outros produtos de Adobe</p> </td>
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65">Visão geral do AEM Forms</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Toda a documentação disponível para AEM Forms</p> </td>
   <td><p><a href="http://adobe.com/go/learn_aemforms_introduction_65">Documentação do AEM Forms</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Atualizações de patches, notas técnicas e informações adicionais sobre esta versão do produto</p> </td>
   <td><p>Entre em contato com o suporte empresarial Adobe</a><br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>O Flex Workspace está obsoleto para o AEM Forms. Ele está disponível para a versão AEM Forms.

## Before You Install {#before-you-install}

### Visão geral da instalação do Workbench {#workbench-installation-overview}

O Workbench é um ambiente de desenvolvimento integrado (IDE) que desenvolvedores e autores de formulários usam para criar formulários e processos comerciais automatizados. Ele também é usado para gerenciar os recursos e serviços que os processos e formulários usam.

A ilustração a seguir descreve a instalação do Workbench, incluindo:
* Processar design usando o Workbench
* Design de formulário usando o Designer

>[!NOTE]
>
>O servidor AEM Forms requer um programa de instalação separado. Para obter mais informações, consulte a documentação de instalação do AEM Forms sobre JEE.

![default-render-form](assets/installing-workbench.png)

## Pré-requisitos do sistema {#system-prerequisites}

Esta seção descreve os requisitos de hardware e software e as plataformas compatíveis.

### Requisitos mínimos de hardware e software {#minimum-hardware-software-requirements}

**Workbench**Os seguintes requisitos são recomendados como mínimo:
Espaço em disco para instalação:
* 680 MB apenas para Workbench.
* 2,15 GB em uma única unidade para uma instalação completa do Workbench, do Designer e do conjunto de amostras.
* 400 MB para diretórios de instalação temporários - 200 MB no diretório user \temp e 200 MB no diretório temporário do Windows.

>[!NOTE]
>
>Se todos esses locais residirem em uma única unidade, deve haver 1,5 GB de espaço disponível durante a instalação. Os arquivos copiados nos diretórios temporários são excluídos quando a instalação for concluída.

* Requisitos de hardware: Processador Intel® Pentium® 4 ou equivalente AMD de 1 GHz.
* O Java™ Runtime Ambiente (JRE) 7.0 atualiza 51 ou mais recente para 7.0.
* Resolução mínima do monitor de 1024 X 768 pixels ou superior com cor de 16 bits ou superior.
* Conexão de rede TCP/IPv4 ou TCP/IPv6 ao servidor AEM Forms.
* Instale o Visual C++ Redistributable Runtime Packages 2012 de 32 bits.
* Instale o Visual C++ Redistributable Runtime Packages 2013 de 32 bits.

>[!NOTE]
>
>Você deve ter privilégios Administrativos para instalar o Workbench. Se você estiver instalando usando uma conta que não seja de administrador, o instalador solicitará as credenciais de uma conta apropriada.

### Plataformas compatíveis {#supported-platforms}

Consulte a lista completa de plataformas compatíveis para Workbench em plataformas [suportadas pela](http://adobe.com/go/learn_aemforms_supportedplatforms_65)AEM Forms.

## Considerações sobre a instalação do Designer {#designer-installation-considerations}

Por padrão, a instalação do Workbench inclui uma versão correspondente somente em inglês do Designer. Se o aplicativo de instalação do Workbench detectar uma versão existente do Designer em seu computador, a instalação poderá ser encerrada e você deverá remover a versão atual do Designer antes de poder continuar.
A tabela abaixo tem uma lista completa de possíveis cenários de instalação do Designer que podem ser encontrados, bem como de quaisquer ações que devem ser tomadas ao instalar o Workbench.

<table>
 <tbody>
  <tr>
   <td><p><strong>Versão do Designer atualmente instalada</strong></p> </td>
   <td><p><strong>Ações necessárias</strong></p> </td>
  </tr>
  <tr>
   <td><p>Acrobat Pro ou Acrobat Pro Extended (inclui o Designer)</p> </td>
   <td><p>Nenhum.<br /> 
A instalação do Workbench detecta uma instância do Designer no computador que foi instalada com o Acrobat Pro ou o Acrobat Pro Extended.<br />
Diferentes versões do Designer podem coexistir no mesmo sistema, por exemplo, o Designer 6.4.x para Workbench 6.4 e o Designer 6.5.0.x para Workbench 6.5. Não é necessário desinstalar a versão do Designer instalada com o Acrobat 10 Pro ou Acrobat 10 Pro Extended ou superior.
<br /></p> </td>
  </tr>
  <tr>
   <td><p>Designer (independente)</p> </td>
   <td><p>Nenhum. <br />A versão do Designer incluída no Workbench é somente em inglês. <br />O instalador do Workbench não reinstalará uma nova versão do Designer. Em vez disso, uma versão atualizada, fornecida com o instalador do Workbench, será corrigida. Isso também permite que você use sua versão localizada do Designer no Workbench.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Para desinstalar o Designer (independente) no Windows 10 {#uninstall-designer-standalone-windows10}

1. Vá para **Painel de controle do Campaign > Programas > Programas e recursos**
1. Na lista programa Atualmente instalado, selecione **Adobe Designer**.
1. Clique em **Desinstalar** e em **Sim**.

## Instalação do Workbench {#installing-workbench}

Este capítulo descreve como instalar o Workbench.

### Instalação e execução do Workbench {#installing-and-running-workbench}

Antes de instalar o Workbench, é necessário certificar-se de que o ambiente inclui o software e o hardware necessários para executá-lo (consulte a seção: **Antes de instalar**).

**Para instalar e executar o Workbench:**

1. Execute uma destas tarefas:
   * Navegue até o diretório \workbench na mídia de instalação e clique no duplo run_windows_installer.bat.
   * Baixe e descompacte o Workbench no seu sistema de arquivos. Após o download, navegue até o diretório \workbench e o duplo clique no arquivo run_windows_installer.bat.

   >[!IMPORTANT]
   >
   >O instalador do Workbench só é executado a partir de uma unidade local. Não pode ser executado de um site remoto.

   >[!NOTE]
   >
   >Se você encontrar um erro &quot;Não foi possível criar a máquina virtual Java&quot;, crie uma variável de ambiente chamada _JAVA_OPTIONS com valor -Xmx512M e execute o instalador.

1. Na tela de Introdução, clique em Avançar.
1. Leia o Contrato de licença do produto, selecione Aceito os termos do Contrato de licença e clique em Avançar.
1. (Opcional) Selecione Instalar o Adobe Designer se você precisar dessa ferramenta para criar e modificar formulários.

   >[!NOTE]
   >
   >Você pode continuar usando o Designer instalado com o Acrobat 10, deixando essa opção desmarcada.

1. Aceite o diretório padrão como listado ou clique em Escolher e navegue até o diretório onde você instalará o Workbench e clique em Avançar.

   >[!NOTE]
   >
   >O caminho do diretório de instalação não deve conter caracteres # (pound) e $ (dólar).

1. Revise o resumo da pré-instalação e clique em Instalar. O programa de instalação exibe o progresso da instalação.
1. Revise o resumo da instalação. Selecione Start AEM Forms Workbench para iniciar o Workbench e clique em Avançar.
1. Revise as Notas de versão e clique em Concluído.
1. Os itens a seguir agora estão instalados no computador:
   * **Bancada**: Para executar o Workbench a partir do menu Start, selecione Todos os Programas > AEM Forms > Workbench, se você escolher armazenar a pasta de atalhos lá. Para obter informações, consulte a documentação <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Uso do Workbench</a> .
   * **Designer**: Você pode acessar o Designer de dentro do Workbench. Para obter informações, consulte o tópico Introdução na Ajuda <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf">do</a>Designer.
   * **AEM Forms SDK**: Para obter mais informações sobre como usar o SDK, consulte <a href="http://www.adobe.com/go/learn_aemforms_programming_65">Programação com o AEM Forms</a>.

## Atualização de processos {#upgrading-processes}

Os processos AEM Forms em JEE podem ser atualizados para aplicativos AEM Forms usando o Assistente de atualização. Consulte Atualização da documentação de artefatos herdados na Ajuda do Workbench para obter mais informações.

### Configuração e logon em um servidor {#configuring-and-logging-server}

Para usar o Workbench, é necessário ter uma instância do AEM Forms em execução, normalmente em um computador separado. É necessário ter um nome de usuário e senha para fazer logon no AEM Forms, bem como detalhes sobre a localização do servidor.

>[!NOTE]
>
>Se você configurou a AEM Forms para usar o provedor de repositório EMC Documentum ou IBM FileNet e quiser fazer logon em um repositório diferente do repositório configurado como padrão no console de administração de formulários AEM, forneça o nome de usuário como username@Repository.

### Definição das configurações de tempo limite {#configuring-timeout-settings}

Por padrão, o Workbench expira após duas horas, independentemente da atividade ou da inatividade. Para editar a configuração de tempo limite, consulte &quot;Configuração do Gerenciamento de usuários > Configurar atributos avançados do sistema&quot; na Ajuda <a href="https://docs.adobe.com/content/help/en/experience-manager-65/forms/administrator-help/configure-user-management/configure-advanced-system-attributes.html">do console de</a>administração.

### Configuração do Workbench para conexão por HTTPS {#configuring-workbench-to-connect-over-HTTPS}

Para conectar o Workbench a um servidor AEM Forms em HTTPS, é necessário garantir que a autoridade de certificação (CA) que emitiu a chave pública seja reconhecida como confiável pelo Workbench. Se o certificado não for reconhecido como vindo de uma fonte confiável, você deverá atualizar o arquivo de alerta localizado no diretório [Workbench_HOME]/workbench/jre/lib/security.

>[!NOTE]
>
>[Workbench_HOME] representa o diretório em que você instalou o Workbench. O local padrão é C:\Program Files (x86)\Adobe Experience Manager Forms Workbench.

Certifique-se de se conectar ao HTTPS usando o nome especificado no certificado. Normalmente, esse nome é o nome de host totalmente qualificado.

**Para atualizar o arquivo** de alerta:
1. Verifique se você tem uma cópia do certificado SSL (Secure Sockets Layer). Entre em contato com o administrador que configurou o servidor SSL ou exporte o certificado usando um navegador da Web.

   >[!NOTE]
   >
   >Para exportar o certificado, abra um navegador da Web e faça logon no console de administração, instale o certificado no navegador e, em seguida, exporte o certificado do navegador para um local de armazenamento temporário (ou diretamente para o diretório [Workbench_HOME]/workbench/jre/lib/security).

1. Copie o certificado para o diretório [Workbench_HOME]/workbench/jre/lib/security.

1. Abra uma janela de prompt de comando, navegue até [Workbench_HOME]/workbench/jre/bin e digite o seguinte comando:
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`
Em que:
   * change é a senha padrão para o armazenamento de chaves cacerts.
   * certname é o certificado selecionado na etapa 1.
   * exemplo é o alias escolhido para o certificado. Este valor pode ser alterado

1. Quando solicitado a confiar no certificado, digite Sim e pressione a tecla Enter. O keytool continua a importar o arquivo cacerts para o diretório [Workbench_HOME]/workbench/jre/lib/security.

1. Feche e reinicie o Workbench para aplicar alterações.

### Definição das configurações de cache para modelos gerados dinamicamente {#configuring-cache-settings-for-dynamically-generated-templates}

Os seguintes aspectos da operação de cache devem ser considerados se seu aplicativo gerar modelos exclusivos dinamicamente, atualizando automaticamente o conteúdo XFA. Na verdade, cada transação usa um modelo novo e único.

Quando o gerador ou a saída de formulários procura ou atualiza entradas no cache de um modelo de formulário específico, ele usa vários valores chave para localizar a entrada de cache específica que será acessada.

* **Nome** do arquivo de modelo: O local e o nome do arquivo do modelo usado como o identificador exclusivo primário do formulário em cache.
* **Carimbo de data e hora**: O arquivo de modelo contém um carimbo de data e hora usado para determinar a última hora de atualização do formulário.
* **UUID** do modelo: O Designer insere em cada modelo um identificador exclusivo (UUID) para o formulário e sua versão. Cada vez que o formulário é atualizado, a UUID incorporada é atualizada. Por exemplo, um modelo XDP pode mostrar o seguinte conteúdo:

   `<?xml version="1.0" encoding="UTF-8"?>`
   `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=http://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="http://www.xfa.org/schema/xfa-template/2.6/">`

* **Opções** de renderização: No cache de formulário renderizado, o conteúdo do cache é armazenado separadamente para cada conjunto de opções de renderização exclusivas.


O serviço Forms recebe modelos por referência ao nome do arquivo ou ao local do repositório, ou por valor como um objeto XML na memória.
* **Modelos passados por referência**: Usa a raiz do conteúdo e o nome do formulário. Se modelos exclusivos com nomes de arquivo diferentes forem transmitidos em cada solicitação usando esse método, o cache de disco crescerá infinitamente e nunca será reutilizado. Para evitar isso, modelos exclusivos devem ser passados com o mesmo nome de arquivo para garantir que o mesmo cache seja atualizado para todas as solicitações.
* **Modelos passados por valor**: Usa os bytes do modelo passados junto com os dados usando o parâmetro inDataDoc. Se os modelos exclusivos com UUID diferentes forem enviados usando esse método, o cache de disco crescerá infinitamente e nunca será reutilizado. Para evitar isso, o atributo UUID deve ser removido de todos os modelos para garantir que nenhum cache seja criado para o modelo. Como alternativa, passar o mesmo UUID não nulo permite que os objetos de cache sejam criados, mas garante que o mesmo cache seja atualizado com cada solicitação.

Para evitar que o cache cresça infinitamente, considere os seguintes fatores para renderizar modelos gerados dinamicamente usando as novas APIs do AEM Forms, que estão sendo renderizadosHTMLForm2 e renderizadosPDFForm2.

Ao usar as novas APIs, o modelo é passado como um objeto de documento, que é manipulado no serviço Forms com base no fato de ser ou não passivado.

Para documentos passivados nos quais o UUID e a raiz do conteúdo servem como chave de cache, considere os seguintes aspectos:
* O cache não é criado para modelos de entrada passiva sem UUID.
* Se mais de um modelo de entrada passivado com o mesmo UUID e raiz de conteúdo forem transmitidos, o mesmo cache será substituído.

Para documentos não passivados nos quais o nome do arquivo e a raiz do conteúdo servem como chave de cache, considere o seguinte aspecto:
* Para modelos de entrada não passivados, o armazenamento em cache depende da raiz do conteúdo e do nome do arquivo a partir do qual o documento foi gerado.
O mesmo cache será usado somente para solicitações com a mesma raiz de conteúdo e o mesmo nome de arquivo de modelo.
As práticas recomendadas a seguir garantirão que o cache não cresça infinitamente quando os modelos gerados dinamicamente forem passados para o serviço Forms:
   * Retire a UUID ou passe a mesma UUID em todos os modelos gerados dinamicamente.
   * Gere o documento a partir de bytes de modelo ou a partir do mesmo nome de arquivo no disco.

### Desinstalação do Workbench {#uninstalling-workbench}

Use a função Adicionar ou remover Programas no Painel de controle do Campaign para start do desinstalador. Os aplicativos Workbench e Designer têm programas de desinstalação separados.

## Configuração do AEM Forms XDC Editor {#configuring-aem-forms-xdc-editor}

Usando o Editor XDC, os administradores de impressoras de rede podem criar e modificar arquivos XML Forms Architecture Device Configuration (XDC). Os arquivos XDC descrevem os recursos das impressoras, como o idioma da impressora ou a correlação entre o tamanho do papel e o local da bandeja.

Antes de o administrador da impressora de rede usar o Editor XDC, localize os arquivos XDC de amostra e consulte Criar perfis de dispositivo usando o Editor XDC.

**Para obter os arquivos** XDC de amostra:
1. No servidor AEM Forms, localize a pasta XDC na raiz [\sdk\samples\Output\IVS]do AEM Forms.
1. Copie o conteúdo desta pasta em um diretório que esteja acessível do sistema Workbench ou Eclipse.

**Para obter a Ajuda** do Editor XDC:
1. Acesse o site de documentação da AEM Forms.
1. Clique na guia **Desenvolver** e navegue até Criar perfis de dispositivo usando o Editor XDC. Baixe o arquivo xdc_editor_help_web.zip e instale os arquivos de Ajuda seguindo as instruções fornecidas no arquivo Readme.

