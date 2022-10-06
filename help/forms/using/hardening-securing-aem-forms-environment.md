---
title: Otimização e proteção de formulários AEM no ambiente OSGi
seo-title: Hardening and Securing AEM forms on OSGi environment
description: Saiba mais sobre as recomendações e as práticas recomendadas para proteger o AEM Forms no servidor OSGi.
seo-description: Learn recommendations and best practices for securing AEM Forms on OSGi server.
uuid: abca7e7c-38c3-44f5-8d8a-4615cfce26c6
topic-tags: Security
discoiquuid: b1bd04bf-0d6d-4e6b-8c7c-eafd1a24b5fe
role: Admin
exl-id: 5da3cc59-4243-4098-b1e0-438304fcd0c5
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 0%

---

# Otimização e proteção de formulários AEM no ambiente OSGi {#hardening-and-securing-aem-forms-on-osgi-environment}

Saiba mais sobre as recomendações e as práticas recomendadas para proteger o AEM Forms no servidor OSGi.

A proteção de um ambiente de servidor é de importância primordial para uma organização. Este artigo descreve recomendações e práticas recomendadas para proteger servidores que executam o AEM Forms. Este não é um documento abrangente de proteção de host para seu sistema operacional. Em vez disso, este artigo descreve várias configurações de proteção de segurança que você deve implementar para melhorar a segurança do aplicativo implantado. No entanto, para garantir que os servidores de aplicativos permaneçam seguros, você também deve implementar procedimentos de monitoramento, detecção e resposta de segurança, além das recomendações fornecidas neste artigo. O documento também contém práticas recomendadas e diretrizes para proteger a PII (Informações de identificação pessoal).

O artigo destina-se a consultores, especialistas em segurança, arquitetos de sistemas e profissionais de TI responsáveis pelo planejamento de aplicativos ou desenvolvimento de infraestrutura e implantação do AEM Forms. Essas funções incluem as seguintes funções comuns:

* Engenheiros de TI e de operações que devem implantar aplicativos e servidores da Web seguros em suas próprias organizações ou em organizações de clientes.
* Arquitetos e planejadores responsáveis pelo planejamento dos esforços arquitetônicos dos clientes em suas organizações.
* Especialistas em segurança de TI que se concentram em fornecer segurança em todas as plataformas em suas organizações.
* Consultores da Adobe e parceiros que exigem recursos detalhados para clientes e parceiros.

A imagem a seguir exibe componentes e protocolos que são usados em uma implantação típica do AEM Forms, incluindo a topologia de firewall apropriada:

![arquitetura típica](assets/typical-architecture.png)

O AEM Forms é altamente personalizável e pode funcionar em vários ambientes diferentes. Algumas das recomendações podem não se aplicar à sua organização.

## Camada de transporte segura {#secure-transport-layer}

As vulnerabilidades de segurança da camada de transporte estão entre as primeiras ameaças a qualquer servidor de aplicativos voltado para a Internet ou para a intranet. Esta seção descreve o processo de proteção de hosts na rede contra essas vulnerabilidades. Ele trata da segmentação de rede, da proteção de pilha do protocolo TCP/IP (Transmission Control Protocol/Internet Protocol) e do uso de firewalls para proteção de host.

### Limitar pontos de extremidade abertos  {#limit-open-endpoints}

Uma organização pode ter um firewall externo para restringir o acesso entre um usuário final e o AEM Forms publish Farm. A organização também pode ter um firewall interno para limitar o acesso entre um farm de publicação e outros elementos dentro da organização (por exemplo, instância de autor, instância de processamento, bancos de dados). Permita firewalls para permitir acesso a um número limitado de URLs do AEM Forms para usuários finais e dentro de elementos de organizações:

#### Configurar firewall externo  {#configure-external-firewall}

Você pode configurar um firewall externo para permitir que um determinado URL do AEM Forms acesse a Internet. O acesso a esses URLs é necessário para preencher ou enviar um formulário adaptável, HTML5, uma carta de gerenciamento de correspondência ou para fazer logon em um servidor AEM Forms:

<table> 
 <tbody>
  <tr>
   <td>Componente</td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>Formulários adaptáveis</td> 
   <td>
    <ul> 
     <li>/content/dam/formsanddocuments/AF_PATH/jcr:content</li> 
     <li>/etc/clientlibs/fd/</li> 
     <li>/content/forms/af/AF_PATH</li> 
     <li>/libs/granite/csrf/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Formulários HTML5</td> 
   <td>
    <ul> 
     <li>/content/forms/formsets/profiles/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Gerenciamento de correspondência </td> 
   <td>
    <ul> 
     <li>/aem/forms/createcorrespondence* </li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Portal do Forms </td> 
   <td>
    <ul> 
     <li>/content/forms/portal/</li> 
     <li>/libs/cq/ui/widgets*</li> 
     <li>/libs/cq/security/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td> Aplicativo AEM Forms</td> 
   <td>
    <ul> 
     <li>/j_security_check*</li> 
     <li>/soap/services/AuthenticationManagerService</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

#### Configurar firewall interno  {#configure-internal-firewall}

Você pode configurar o firewall interno para permitir que determinados componentes do AEM Forms (por exemplo, instância de autor, instância de processamento, bancos de dados) se comuniquem com o farm de publicação e outros componentes internos mencionados no diagrama de topologia:

<table> 
 <tbody>
  <tr>
   <td>Host<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>Publicar farm (nós de publicação)</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>Servidor de processamento</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Servidor do complemento Forms Workflow (AEM Forms no servidor JEE)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### Configurar permissões do repositório e listas de controle de acesso (ACLs) {#setup-repository-permissions-and-access-control-lists-acls}

Por padrão, os ativos disponíveis nos nós de publicação são acessíveis a todos. O acesso somente leitura é ativado para todos os ativos. É necessário ativar o acesso anônimo. Se você pretende restringir a visualização do formulário e enviar o acesso somente para usuários autenticados, use um grupo comum para permitir que somente usuários autenticados tenham acesso somente leitura aos ativos disponíveis nos nós de publicação. Os seguintes locais/diretórios contêm ativos de formulários que exigem proteção (acesso somente leitura para usuários autenticados):

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## Lidar com dados de formulários com segurança  {#securely-handle-forms-data}

O AEM Forms armazena dados em locais predefinidos e pastas temporárias. Você deve proteger os dados para evitar um uso não autorizado.

### Configurar limpeza periódica da pasta temporária {#setup-periodic-cleanup-of-temporary-folder}

Ao configurar formulários para anexos de arquivo, verificar ou visualizar componentes, os dados correspondentes são armazenados nos nós de publicação em /tmp/fd/. Os dados são removidos periodicamente. Você pode modificar o trabalho de limpeza de dados padrão para ser mais agressivo. Para modificar a tarefa agendada para limpar dados, abra AEM Console da Web, abra a Tarefa de Limpeza de Armazenamento Temporário AEM Forms e modifique a expressão Cron.

Nos cenários acima mencionados, os dados são salvos somente para usuários autenticados. Além disso, os dados são protegidos com ACLs (Access Control lists, listas de controle de acesso). Portanto, modificar a limpeza de dados é uma etapa adicional para proteger as informações.

### Dados seguros salvos pela ação de envio do portal de formulários {#secure-data-saved-by-forms-portal-submit-action}

Por padrão, a ação de envio do portal de formulários de formulários adaptáveis salva dados no repositório local do nó de publicação. Os dados são salvos em /content/forms/fp. **Não é recomendado armazenar dados na instância de publicação.**

Você pode configurar o serviço de armazenamento para enviar tudo pela rede para o cluster de processamento sem salvar localmente no nó de publicação. O cluster de processamento reside em uma zona segura atrás do firewall privado e os dados permanecem seguros.

Use as credenciais do servidor de processamento para AEM serviço de configurações do DS para publicar dados do nó de publicação no servidor de processamento. É recomendável usar credenciais de um usuário não administrativo restrito com acesso de leitura e gravação ao repositório do servidor de processamento. Para obter mais informações, consulte [Configuração de serviços de armazenamento para rascunhos e envios](/help/forms/using/configuring-draft-submission-storage.md).

### Dados seguros tratados pelo modelo de dados de formulário (FDM) {#secure-data-handled-by-form-data-model-fdm}

Use contas de usuário com os privilégios mínimos necessários para configurar as fontes de dados para o FDM (form Data Model, modelo de dados de formulário). O uso de contas administrativas pode fornecer acesso aberto de metadados e entidades de esquema para usuários não autorizados.\
A integração de dados também fornece métodos para autorizar solicitações de serviço do FDM. Você pode inserir mecanismos de autorização de pré e pós execução para validar uma solicitação. As solicitações de serviço são geradas durante o preenchimento prévio de um formulário, o envio de um formulário e a chamada de serviços por meio de uma regra.

**Autorização prévia ao processo:** Você pode usar a autorização de pré-processamento para validar a autenticidade de uma solicitação antes de executá-la. Você pode usar entradas, serviço e detalhes da solicitação para permitir ou parar a execução da solicitação. Você pode retornar uma exceção de integração de dados OPERATION_ACCESS_DENIED se a execução for interrompida. Você também pode modificar a solicitação do cliente antes de enviá-la para execução. Por exemplo, alterar a entrada e adicionar mais informações.

**Autorização pós-processo:** Você pode usar a autorização pós-processo para validar e controlar os resultados antes de retornar os resultados ao solicitante. Também é possível filtrar, remover e inserir dados adicionais aos resultados.

### Limitar o acesso do usuário {#limit-user-access}

Um conjunto diferente de personas de usuário é necessário para as instâncias de autor, publicação e processamento. Não execute nenhuma instância com credenciais de administrador.

**Em uma instância de publicação:**

* Somente usuários do grupo usuários de formulários podem visualizar, criar rascunho e enviar formulários.
* Somente usuários de um grupo cm-user-agent podem visualizar cartas de gerenciamento de correspondência.
* Desative todo o acesso anônimo não essencial.

**Em uma instância do autor:**

* Há um conjunto diferente de grupos predefinidos com privilégios específicos para cada persona. Atribuir usuários ao grupo.

   * Um usuário de um grupo de usuários de formulários:

      * podem criar, preencher, publicar e enviar um formulário.
      * O não pode criar um formulário adaptável baseado em XDP.
      * não tem permissões para gravar scripts para formulários adaptáveis.
      * não é possível importar XDP ou qualquer pacote que contenha XDP
   * Um usuário do grupo forms-power-user cria, preenche, publica e envia todos os tipos de formulários, grava scripts para formulários adaptáveis, importa pacotes contendo XDP.
   * Um usuário de autores de modelo e de usuários avançados de modelo pode visualizar e criar um modelo.
   * Um usuário de autores de fdm pode criar e modificar um modelo de dados de formulário.
   * Um usuário de um grupo cm-user-agent pode criar, visualizar e publicar cartas de gerenciamento de correspondência.
   * Um usuário de um grupo de editores de fluxo de trabalho pode criar um aplicativo de caixa de entrada e um modelo de fluxo de trabalho.


**No autor de processamento:**

* Para salvar e enviar casos de uso remotos, crie um usuário com permissões de leitura, criação e modificação no caminho content/form/fp do repositório crx.
* Adicione usuário ao grupo de usuários do fluxo de trabalho para permitir que um usuário use AEM aplicativos da caixa de entrada.

## Elementos seguros da intranet de um ambiente do AEM Forms {#secure-intranet-elements-of-an-aem-forms-environment}

Em geral, os clusters de processamento e o complemento Forms Workflow (AEM Forms no JEE) são executados atrás de um firewall. Portanto, são consideradas seguras. Você ainda pode executar algumas etapas para proteger esses ambientes:

### Cluster de processamento seguro {#secure-processing-cluster}

Um cluster de processamento é executado no modo de criação, mas não o usa para atividades de desenvolvimento. Não permita que um usuário normal seja incluído em grupos de autores de conteúdo e usuários de formulário de um cluster de processamento.

### USAR AEM práticas recomendadas para proteger um ambiente AEM Forms {#use-aem-best-practices-to-secure-an-aem-forms-environment}

Este documento fornece instruções específicas para o ambiente AEM Forms. Você deve tomar providências para garantir que a instalação AEM subjacente seja segura quando implantada. Para obter instruções detalhadas, consulte [Lista de verificação de segurança AEM](/help/sites-administering/security-checklist.md) documentação.
