---
title: Fortalecimento e proteção de formulários AEM no ambiente OSGi
description: Saiba mais sobre as recomendações e práticas recomendadas para proteger o AEM Forms no servidor OSGi.
topic-tags: Security
role: Admin
exl-id: 5da3cc59-4243-4098-b1e0-438304fcd0c5
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 0%

---

# Fortalecimento e proteção de formulários AEM no ambiente OSGi {#hardening-and-securing-aem-forms-on-osgi-environment}

Saiba mais sobre as recomendações e práticas recomendadas para proteger o AEM Forms no servidor OSGi.

Proteger um ambiente de servidor é de suma importância para uma organização. Este artigo descreve recomendações e práticas recomendadas para proteger servidores que executam o AEM Forms. Este não é um documento abrangente de fortalecimento do host para o seu sistema operacional. Em vez disso, este artigo descreve várias configurações de proteção de segurança que você deve implementar para melhorar a segurança do aplicativo implantado. No entanto, para garantir que os servidores de aplicativos permaneçam seguros, você também deve implementar procedimentos de monitoramento de segurança, detecção e resposta, além das recomendações fornecidas neste artigo. O documento também contém práticas recomendadas e diretrizes para proteção de PII (Informações de identificação pessoal).

O artigo destina-se a consultores, especialistas em segurança, arquitetos de sistemas e profissionais de TI responsáveis por planejar o desenvolvimento e a implantação de aplicativos ou infraestruturas do AEM Forms. Essas funções incluem as seguintes funções comuns:

* Engenheiros de TI e de operações que precisam implantar aplicativos e servidores seguros para a Web em suas próprias organizações ou nas organizações dos clientes.
* Arquitetos e planejadores que são responsáveis por planejar os esforços de arquitetura para os clientes em suas organizações.
* Especialistas em segurança de TI que se concentram em fornecer segurança em todas as plataformas em suas organizações.
* Consultores da Adobe e parceiros que exigem recursos detalhados para clientes e parceiros.

A imagem a seguir exibe componentes e protocolos usados em uma implantação típica do AEM Forms, incluindo a topologia de firewall apropriada:

![arquitetura típica](assets/typical-architecture.png)

O AEM Forms é altamente personalizável e pode funcionar em vários ambientes diferentes. Algumas das recomendações podem não se aplicar à sua organização.

## Camada de transporte segura {#secure-transport-layer}

As vulnerabilidades de segurança da camada de transporte estão entre as primeiras ameaças a qualquer servidor de aplicativos voltado para a Internet ou para a intranet. Esta seção descreve o processo de proteção dos hosts na rede contra essas vulnerabilidades. Ele aborda a segmentação de rede, o fortalecimento da pilha do protocolo de controle de transmissão/protocolo de Internet (TCP/IP) e o uso de firewalls para proteção de host.

### Limitar pontos de extremidade abertos  {#limit-open-endpoints}

Uma organização pode ter um firewall externo para restringir o acesso entre um usuário final e o Farm de publicação do AEM Forms. A organização também pode ter um firewall interno para limitar o acesso entre um farm de publicação e outros elementos dentro da organização (por exemplo, instância do autor, instância de processamento, bancos de dados). Permitir que firewalls ativem o acesso a um número limitado de URLs do AEM Forms para usuários finais e elementos da organização:

#### Configurar firewall externo  {#configure-external-firewall}

Você pode configurar um firewall externo para permitir que determinados URLs da AEM Forms acessem a Internet. O acesso a esses URLs é necessário para preencher ou enviar um formulário adaptável, HTML5, uma carta de gerenciamento de correspondência ou fazer logon em um servidor AEM Forms:

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
   <td>formulários HTML5</td> 
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
   <td>Portal Forms </td> 
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
   <td>Publicar farm (publicar nós)</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>Servidor de processamento</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Servidor complementar do Forms Workflow (AEM Forms no servidor JEE)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### Configurar permissões de repositório e listas de controle de acesso (ACLs) {#setup-repository-permissions-and-access-control-lists-acls}

Por padrão, os ativos disponíveis nos nós de publicação estão acessíveis a todos. O acesso somente leitura está ativado para todos os ativos. É necessário para habilitar o acesso anônimo. Se você planeja restringir a visualização do formulário e enviar o acesso somente a usuários autenticados, use um grupo comum para permitir que somente usuários autenticados tenham acesso somente leitura aos ativos disponíveis nos nós de publicação. Os seguintes locais/diretórios contêm ativos de formulários que exigem proteção (acesso somente leitura para usuários autenticados):

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## Manipule com segurança os dados de formulários  {#securely-handle-forms-data}

O AEM Forms armazena dados em locais predefinidos e pastas temporárias. Você deve proteger os dados para impedir um uso não autorizado.

### Configurar limpeza periódica da pasta temporária {#setup-periodic-cleanup-of-temporary-folder}

Ao configurar formulários para anexos de arquivo, verificar ou visualizar componentes, os dados correspondentes são armazenados nos nós de publicação em /tmp/fd/. Os dados são removidos periodicamente. Você pode modificar o trabalho de limpeza de dados padrão para ser mais agressivo. Para modificar o trabalho agendado para limpar dados, abra o Console da Web do AEM, abra a Tarefa de limpeza de armazenamento temporário do AEM Forms e modifique a expressão Cron.

Nos cenários mencionados acima, os dados são salvos somente para usuários autenticados. Além disso, os dados são protegidos com listas de controle de acesso (ACLs). Portanto, a modificação da eliminação de dados é uma etapa adicional para proteger as informações.

### Dados seguros salvos pela ação enviar do portal de formulários {#secure-data-saved-by-forms-portal-submit-action}

Por padrão, a ação enviar do portal de formulários adaptáveis salva os dados no repositório local do nó de publicação. Os dados são salvos em /content/forms/fp. **Não é recomendável armazenar dados na instância de publicação.**

Você pode configurar o serviço de armazenamento para enviar pelo cabo ao cluster de processamento sem salvar nada localmente no nó de publicação. O cluster de processamento reside em uma zona segura atrás do firewall privado e os dados permanecem seguros.

Use as credenciais do servidor de processamento para o serviço de configurações do AEM DS para postar dados do nó de publicação no servidor de processamento. Use as credenciais de um usuário não administrativo restrito com acesso de leitura e gravação ao repositório do servidor de processamento. Para obter mais informações, consulte [Configuração de serviços de armazenamento para rascunhos e envios](/help/forms/using/configuring-draft-submission-storage.md).

### Dados seguros tratados pelo modelo de dados de formulário (FDM) {#secure-data-handled-by-form-data-model-fdm}

Use contas de usuário com os privilégios mínimos necessários para configurar fontes de dados para o modelo de dados de formulário (FDM). O uso da conta administrativa pode fornecer acesso aberto de metadados e entidades de esquema a usuários não autorizados.\
A integração de dados também fornece métodos para autorizar solicitações de serviço do FDM. Você pode inserir mecanismos de autorização de pré e pós-execução para validar uma solicitação. As solicitações de serviço são geradas ao preencher previamente um formulário, enviar um formulário e chamar serviços por meio de uma regra.

**Autorização de pré-processamento:** Você pode usar a autorização de pré-processamento para validar a autenticidade de uma solicitação antes de executá-la. Você pode usar entradas, serviço e detalhes da solicitação para permitir ou interromper a execução da solicitação. Você poderá retornar uma exceção de integração de dados OPERATION_ACCESS_DENIED se a execução for interrompida. Você também pode modificar a solicitação do cliente antes de enviá-la para execução. Por exemplo, alterar a entrada e adicionar outras informações.

**Autorização pós-processamento:** Você pode usar a autorização pós-processo para validar e controlar os resultados antes de retornar os resultados ao solicitante. Também é possível filtrar, remover e inserir dados adicionais nos resultados.

### Limitar o acesso do usuário {#limit-user-access}

Um conjunto diferente de personalidades de usuário é necessário para as instâncias de autor, publicação e processamento. Não execute nenhuma instância com credenciais de administrador.

**Em uma instância de publicação:**

* Somente usuários do grupo formulários-usuários podem visualizar, criar rascunhos e enviar formulários.
* Somente usuários do grupo cm-user-agent podem visualizar cartas de gerenciamento de correspondência.
* Desative todo o acesso anônimo não essencial.

**Em uma instância de autor:**

* Há um conjunto diferente de grupos predefinidos com privilégios específicos para cada persona. Atribuir usuários ao grupo.

   * Um usuário do grupo de usuários de formulários:

      * O pode criar, preencher, publicar e enviar um formulário.
      * O não pode criar um formulário adaptável baseado em XDP.
      * não têm permissões para gravar scripts para formulários adaptáveis.
      * não é possível importar XDP ou qualquer pacote que contenha XDP

   * Um usuário do grupo de usuários avançados de formulários cria, preenche, publica e envia todos os tipos de formulários, grava scripts para formulários adaptáveis e importa pacotes que contêm XDP.
   * Um usuário de autores de modelo e usuário avançado de modelo pode visualizar e criar um modelo.
   * Um usuário de autores do fdm pode criar e modificar um modelo de dados de formulário.
   * Um usuário do grupo cm-user-agent pode criar, pré-visualizar e publicar cartas de gerenciamento de correspondência.
   * Um usuário do grupo de editores de workflow pode criar um aplicativo de caixa de entrada e um modelo de workflow.

**No processamento do autor:**

* Para casos de uso de salvar e enviar remotamente, crie um usuário com permissões de leitura, criação e modificação no caminho content/form/fp do repositório crx.
* Adicione usuário ao grupo de usuários do fluxo de trabalho para permitir que um usuário use aplicativos da caixa de entrada do AEM.

## Elementos seguros da intranet de um ambiente do AEM Forms {#secure-intranet-elements-of-an-aem-forms-environment}

Em geral, os clusters de processamento e o complemento de Forms Workflow (AEM Forms no JEE) são executados atrás de um firewall. Então, eles são considerados seguros. Você ainda pode executar algumas etapas para fortalecer esses ambientes:

### Cluster de processamento seguro {#secure-processing-cluster}

Um cluster de processamento é executado no modo de autor, mas não o use para atividades de desenvolvimento. Não permita que um usuário normal seja incluído em grupos de autores de conteúdo e usuários de formulário de um cluster de processamento.

### USAR as práticas recomendadas de AEM para proteger um ambiente AEM Forms {#use-aem-best-practices-to-secure-an-aem-forms-environment}

Este documento fornece instruções específicas para o ambiente do AEM Forms. É necessário garantir que sua instalação subjacente do AEM esteja segura quando implantada. Para obter instruções detalhadas, consulte [Lista de verificação de segurança do AEM](/help/sites-administering/security-checklist.md) documentação.
