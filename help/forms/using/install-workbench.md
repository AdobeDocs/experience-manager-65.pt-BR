---
title: Instalar o workbench
seo-title: Install workbench
description: Instale o workbench.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
role: Admin
exl-id: d530dbb9-f95e-4329-9665-37faf8f7931b
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '2244'
ht-degree: 0%

---

# Instalar o Workbench {#install-workbench}

Este documento fornece instruções para instalar e configurar o AEM Forms Workbench. O programa de instalação também instala o Forms Designer.

## Quem deve ler este documento? {#who-should-read-this-doc}

Este documento destina-se aos administradores ou desenvolvedores responsáveis pela instalação, configuração, administração ou implantação do Workbench. Também estão incluídas as informações necessárias para configurar seu sistema para suportar os processos atualizados do AEM Forms. As informações fornecidas baseiam-se no pressuposto de que qualquer pessoa que leia este documento está familiarizada com o sistema operacional Microsoft® Windows®.

## Informações adicionais {#additional-information}

Os recursos nesta tabela podem ajudá-lo a saber mais e começar a usar o AEM Forms.
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
   <td><p>Informações gerais sobre o AEM Forms e como ele se integra a outros produtos do Adobe</p> </td>
   <td><p><a href="https://adobe.com/go/learn_aemforms_introduction_65">Visão geral da AEM Forms</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Toda a documentação disponível para o AEM Forms</p> </td>
   <td><p><a href="https://adobe.com/go/learn_aemforms_introduction_65">Documentação do AEM Forms</a><br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Atualizações de patches, notas técnicas e informações adicionais sobre esta versão do produto</p> </td>
   <td><p>Entre em contato com o suporte empresarial Adobe</a><br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>O Flex Workspace está obsoleto para o AEM Forms. Ele está disponível para a versão do AEM Forms.

## Antes de instalar {#before-you-install}

### Visão geral da instalação do Workbench {#workbench-installation-overview}

O Workbench é um ambiente de desenvolvimento integrado (IDE) que os desenvolvedores e autores de formulários usam para criar formulários e processos comerciais automatizados. Ele também é usado para gerenciar os recursos e serviços que os processos e formulários usam.

A ilustração a seguir descreve a instalação do Workbench incluindo:
* Processar design usando o Workbench
* Design de formulário usando o Designer

>[!NOTE]
>
>O servidor AEM Forms requer um programa de instalação separado. Para obter mais informações, consulte a documentação de instalação do AEM Forms no JEE.

![formulário de renderização padrão](assets/installing-workbench.png)

## Pré-requisitos do sistema {#system-prerequisites}

Esta seção descreve os requisitos de hardware e software e as plataformas compatíveis.

### Requisitos mínimos de hardware e software {#minimum-hardware-software-requirements}

**Workbench**
Recomenda-se, no mínimo, os seguintes requisitos: Espaço em disco para instalação:
* 680 MB somente para Workbench.
* 2,15 GB em uma única unidade para uma instalação completa do Workbench, do Designer e do conjunto de amostras.
* 400 MB para diretórios de instalação temporários - 200 MB no diretório \temp do usuário e 200 MB no diretório temporário do Windows.

>[!NOTE]
>
>Se todos esses locais residirem em uma única unidade, deverá haver 1,5 GB de espaço disponível durante a instalação. Os arquivos copiados para os diretórios temporários são excluídos quando a instalação é concluída.

* Requisito de hardware: Processador Intel® Pentium® 4 ou AMD equivalente, 1 GHz.
* O Java™ Runtime Environment (JRE) 7.0 atualiza 51 ou atualizações posteriores para 7.0.
* Resolução mínima de monitor de 1024 X 768 pixels ou superior com cor de 16 bits ou superior.
* Conexão de rede TCP/IPv4 ou TCP/IPv6 ao servidor AEM Forms.
* Instale o Visual C++ Redistributable runtime Packages 2012 de 32 bits.
* Instale o Visual C++ Redistributable runtime Packages 2013 de 32 bits.

>[!NOTE]
>
>Você deve ter privilégios Administrativos para instalar o Workbench. Se você estiver instalando usando uma conta que não seja de administrador, o instalador solicitará as credenciais de uma conta apropriada.

### Plataformas compatíveis {#supported-platforms}

Consulte a lista completa de plataformas compatíveis para o Workbench em [Plataformas compatíveis com a AEM Forms](https://adobe.com/go/learn_aemforms_supportedplatforms_65).

## Considerações sobre a instalação do Designer {#designer-installation-considerations}

Por padrão, a instalação do Workbench inclui uma versão correspondente em inglês do Designer. Se o aplicativo de instalação do Workbench detectar uma versão existente do Designer em seu computador, a instalação poderá ser encerrada e você deverá remover a versão atual do Designer antes de continuar.
A tabela abaixo tem uma lista completa de possíveis cenários de instalação do Designer que podem ser encontrados, bem como quaisquer ações que devem ser tomadas ao instalar o Workbench.

<table>
 <tbody>
  <tr>
   <td><p><strong>Versão do Designer atualmente instalada</strong></p> </td>
   <td><p><strong>Ações necessárias</strong></p> </td>
  </tr>
  <tr>
   <td><p>Acrobat Pro ou Acrobat Pro Extended (inclui o Designer)</p> </td>
   <td><p>Nenhum.<br /> 
A instalação do Workbench detecta uma instância do Designer no seu computador que foi instalada com o Acrobat Pro ou o Acrobat Pro Extended.<br />
Diferentes versões do Designer podem coexistir no mesmo sistema, por exemplo, o Designer 6.4.x para Workbench 6.4 e o Designer 6.5.0.x para Workbench 6.5. Não é necessário desinstalar a versão do Designer instalada com o Acrobat 10 Pro ou Acrobat 10 Pro Extended ou superior.
<br /></p> </td>
  </tr>
  <tr>
   <td><p>Designer (independente)</p> </td>
   <td><p>Nenhum. <br />A versão do Designer incluída no Workbench é somente em inglês. <br />O instalador do Workbench não reinstalará uma nova versão do Designer. Em vez disso, uma versão atualizada, fornecida com o instalador do Workbench, será corrigida. Isso também permite usar sua versão localizada do Designer no Workbench.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Para desinstalar o Designer (independente) no Windows 10 {#uninstall-designer-standalone-windows10}

1. Ir para **Painel de controle do Campaign > Programas > Programas e recursos**
1. Na lista Programas instalados, selecione **Adobe Designer**.
1. Clique em **Desinstalar** e, em seguida, clique em **Sim**.

## Instalar o Workbench {#installing-workbench}

Este capítulo descreve como instalar o Workbench.

### Instalar e executar o Workbench {#installing-and-running-workbench}

Antes de instalar o Workbench, é necessário garantir que seu ambiente inclua o software e o hardware necessários para executá-lo (Consulte a seção : **Antes de instalar**).

**Para instalar e executar o Workbench:**

1. Execute uma destas tarefas:
   * Navegue até o diretório \workbench na mídia de instalação e clique duas vezes no arquivo run_windows_installer.bat.
   * Baixe e descompacte o Workbench no seu sistema de arquivos. Após o download, navegue até o diretório \workbench e clique duas vezes no arquivo run_windows_installer.bat.

   >[!IMPORTANT]
   >
   >O instalador do Workbench é executado somente a partir de uma unidade local. Ele não pode ser executado de um site remoto.

   >[!NOTE]
   >
   >Se encontrar um erro &quot;Não foi possível criar a máquina virtual do Java&quot;, crie uma variável de ambiente chamada _JAVA_OPTIONS com o valor -Xmx512M e execute o instalador.

1. Na tela Introdução, clique em Avançar.
1. Leia o Contrato de licença do produto, selecione Aceito os termos do Contrato de licença e clique em Avançar.
1. (Opcional) Selecione Instalar o Adobe Designer, se você precisar dessa ferramenta para criar e modificar formulários.

   >[!NOTE]
   >
   >Você pode continuar usando o Designer instalado com o Acrobat 10, deixando essa opção desmarcada.

1. Aceite o diretório padrão como listado ou clique em Escolher e navegue até o diretório onde você instalará o Workbench e clique em Avançar.

   >[!NOTE]
   >
   >O caminho do diretório de instalação não deve conter os caracteres # (libra) e $ (dólar).

1. Revise o resumo da pré-instalação e clique em Instalar. O programa de instalação exibe o progresso da instalação.
1. Revise o resumo da instalação. Selecione Iniciar o AEM Forms Workbench para iniciar o Workbench e clique em Próximo.
1. Revise as Notas de versão e clique em Concluído.
1. Os seguintes itens foram instalados no computador:
   * **Workbench**: Para executar o Workbench a partir do menu Iniciar, selecione Todos os programas > AEM Forms > Workbench, se optar por armazenar a pasta de atalho lá. Para obter informações, consulte o <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf">Uso do Workbench</a> documentação.
   * **Designer**: Você pode acessar o Designer no Workbench. Para obter informações, consulte o tópico Introdução em <a href="https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf">Ajuda do Designer</a>.
   * **AEM Forms SDK**: Para obter mais informações sobre como usar o SDK, consulte <a href="https://www.adobe.com/go/learn_aemforms_programming_65">Programação com o AEM Forms</a>.

## Atualização de processos {#upgrading-processes}

Os processos do AEM Forms em JEE podem ser atualizados para aplicativos AEM Forms usando o Assistente de atualização. Consulte Atualização da documentação de artefatos herdados na Ajuda do Workbench para obter mais informações.

### Configuração e logon em um servidor {#configuring-and-logging-server}

Para usar o Workbench, é necessário ter uma instância do AEM Forms em execução, normalmente em um computador separado. Você deve ter um nome de usuário e senha para fazer logon no AEM Forms, bem como detalhes sobre a localização do servidor.

>[!NOTE]
>
>Se você configurou o AEM Forms para usar o provedor de repositório EMC Documentum ou IBM FileNet e deseja fazer logon em um repositório diferente do repositório configurado como padrão no console de administração AEM formulários, forneça o nome de usuário como username@Repository.

### Definição das configurações de tempo limite {#configuring-timeout-settings}

Por padrão, o Workbench expira após duas horas, independentemente da atividade ou da inatividade. Para editar a configuração de tempo limite, consulte &quot;Configuração do gerenciamento de usuários > Configurar atributos avançados do sistema&quot; no <a href="https://docs.adobe.com/content/help/en/experience-manager-65/forms/administrator-help/configure-user-management/configure-advanced-system-attributes.html">ajuda do console de administração</a>.

### Configuração do Workbench para se conectar via HTTPS {#configuring-workbench-to-connect-over-HTTPS}

Para conectar o Workbench a um servidor AEM Forms por HTTPS, você deve garantir que a autoridade de certificação (CA) que emitiu a chave pública seja reconhecida como confiável pelo Workbench. Se o certificado não for reconhecido como proveniente de uma fonte confiável, você deverá atualizar o arquivo de alerta localizado na [Workbench_HOME]/workbench/jre/lib/security diretory.

>[!NOTE]
>
>[Workbench_HOME] representa o diretório onde você instalou o Workbench. O local padrão é C:\Program Files (x86)\Adobe Experience Manager forms Workbench.

Certifique-se de se conectar ao HTTPS usando o nome especificado no certificado. Normalmente, esse nome é o nome de host totalmente qualificado.

**Para atualizar o arquivo de alerta**:
1. Certifique-se de ter uma cópia do certificado SSL (Secure Sockets Layer). Entre em contato com o administrador que configurou o servidor SSL ou exporte o certificado usando um navegador da Web.

   >[!NOTE]
   >
   >Para exportar o certificado, abra um navegador da Web e faça logon no console de administração, instale o certificado no navegador e exporte o certificado do navegador para um local de armazenamento temporário (ou diretamente para o [Workbench_HOME]/workbench/jre/lib/diretory de segurança).

1. Copie o certificado para a [Workbench_HOME]/workbench/jre/lib/security diretory.

1. Abra uma janela de prompt de comando, navegue até [Workbench_HOME]/workbench/jre/bin e digite o seguinte comando:
   `keytool -import -storepass changeit -file [Workbench_HOME]\workbench\jre\lib\security\ssl_cert_for_certname.cer -keystore [Workbench_HOME]\workbench\jre\lib\security\cacerts -alias example`
Em que:
   * change é a senha padrão para o keystore acerts.
   * certname é o certificado selecionado na etapa 1.
   * exemplo é o alias escolhido para o certificado. Este valor pode ser alterado

1. Quando solicitado a confiar no certificado, digite Sim e pressione a tecla Enter. O keytool continua importando o arquivo de acerts para o [Workbench_HOME]/workbench/jre/lib/security diretory.

1. Feche e reinicie o Workbench para aplicar as alterações.

### Definição das configurações de cache para modelos gerados dinamicamente {#configuring-cache-settings-for-dynamically-generated-templates}

Os seguintes aspectos da operação de cache devem ser considerados se seu aplicativo gerar modelos exclusivos dinamicamente, atualizando automaticamente o conteúdo XFA. Na verdade, cada transação usa um novo modelo exclusivo.

Quando o gerador ou a saída do Forms procura ou atualiza entradas no cache de um modelo de formulário específico, ele usa vários valores principais para localizar a entrada de cache específica que será acessada.

* **Nome do arquivo de modelo**: O local e o nome do arquivo do modelo usado como o identificador exclusivo principal do formulário em cache.
* **Carimbo de data e hora**: O arquivo de modelo contém um carimbo de data e hora usado para determinar a hora da última atualização do formulário.
* **UUID do modelo**: O Designer insere em cada modelo um identificador exclusivo (UUID) para o formulário e sua versão. Cada vez que o formulário é atualizado, a UUID incorporada é atualizada. Por exemplo, um modelo XDP pode mostrar o seguinte conteúdo:

   `<?xml version="1.0" encoding="UTF-8"?>`
   `<?xfa generator="AdobeAEM formsDesignerES_V8.2" APIVersion="2.6.7185.0"?><xdp:xdp xmlns:xdp=https://ns.adobe.com/xdp/ timeStamp="2008-07-29T21:22:12Z" uuid="823e538f-ff6c-4961-b759-f7626978a223"><template xmlns="https://www.xfa.org/schema/xfa-template/2.6/">`

* **Opções de renderização**: No cache de formulário renderizado, o conteúdo do cache é armazenado separadamente para cada conjunto de opções de renderização exclusivas.


O serviço Forms recebe modelos por referência ao nome do arquivo ou local do repositório, ou pelo valor como um objeto XML na memória.
* **Modelos passados por referência**: Usa a raiz de conteúdo e o nome do formulário. Se modelos exclusivos com nomes de arquivo diferentes forem passados em cada solicitação usando este método, o cache de disco crescerá continuamente e nunca será reutilizado. Para evitar isso, os modelos exclusivos devem ser transmitidos com o mesmo nome de arquivo para garantir que o mesmo cache seja atualizado para todas as solicitações.
* **Modelos transmitidos por valor**: Usa bytes de modelo passados junto com os dados usando o parâmetro inDataDoc . Se modelos exclusivos com UUID diferentes forem passados usando esse método, o cache de disco crescerá continuamente e nunca será reutilizado. Para evitar isso, o atributo UUID deve ser removido de todos os modelos para garantir que nenhum cache seja criado para o modelo. Como alternativa, transmitir a mesma UUID não nula permite que os objetos de cache sejam criados, mas garante que o mesmo cache seja atualizado com cada solicitação.

Para evitar que o cache cresça infinitamente, considere os seguintes fatores para renderizar modelos gerados dinamicamente usando as novas APIs do AEM Forms, que estão sendo renderizadosHTMLForm2 e renderPDFForm2.

Ao usar as novas APIs, o modelo é passado como um objeto de documento, que é manipulado no serviço Forms com base no fato de ser passivo ou não.

Para documentos passivados nos quais o UUID e a raiz de conteúdo servem como chave de cache, considere os seguintes aspectos:
* O cache não é criado para modelos de entrada passiva sem UUID.
* Se mais de um template de entrada passivo com o mesmo UUID e a mesma raiz de conteúdo forem passadas, o mesmo cache será substituído.

Para documentos não passivos em que o nome do arquivo e a raiz do conteúdo servem como chave de cache, considere o seguinte aspecto:
* Para modelos de entrada não passivos, o armazenamento em cache depende da raiz de conteúdo e do nome do arquivo a partir do qual o documento foi gerado.
O mesmo cache será usado somente para solicitações com a mesma raiz de conteúdo e nome de arquivo de modelo.
As práticas recomendadas a seguir garantem que o cache não cresça infinitamente quando modelos gerados dinamicamente são passados para o serviço Forms:
   * Retire a UUID ou transmita a mesma UUID em todos os modelos gerados dinamicamente.
   * Gere o documento a partir de bytes de modelo ou do mesmo nome de arquivo no disco.

### Desinstalar o Workbench {#uninstalling-workbench}

Use a função Adicionar ou remover programas no Painel de controle do Campaign para iniciar o Desinstalador. Os aplicativos do Workbench e do Designer têm programas de desinstalação separados.

## Configuração do editor AEM Forms XDC {#configuring-aem-forms-xdc-editor}

Usando o XDC Editor, os administradores de impressoras de rede podem criar e modificar arquivos XML Forms Architecture Device Configuration (XDC). Os arquivos XDC descrevem os recursos das impressoras, como o idioma da impressora ou a correlação entre o tamanho do papel e o local da bandeja.

Antes de o administrador da impressora de rede usar o Editor XDC, localize os arquivos XDC de amostra e consulte Criar perfis de dispositivo usando o Editor XDC.

**Para obter os arquivos XDC de amostra**:
1. No servidor do AEM Forms, localize a pasta XDC em [Raiz do AEM Forms]\sdk\samples\Output\IVS.
1. Copie o conteúdo dessa pasta em um diretório acessível do sistema Workbench ou Eclipse.

**Para obter a Ajuda do XDC Editor**:
1. Acesse o site da documentação do AEM Forms.
1. Clique no botão **Desenvolver** e navegue até Criar perfis de dispositivo usando o XDC Editor. Baixe o arquivo xdc_editor_help_web.zip e instale os arquivos de Ajuda seguindo as instruções fornecidas no arquivo Readme.
