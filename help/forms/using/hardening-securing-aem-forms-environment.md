---
title: Como fortalecer e proteger formulários do AEM no ambiente OSGi
seo-title: Como fortalecer e proteger formulários do AEM no ambiente OSGi
description: Saiba mais sobre recomendações e práticas recomendadas para proteger o AEM Forms no servidor OSGi.
seo-description: Saiba mais sobre recomendações e práticas recomendadas para proteger o AEM Forms no servidor OSGi.
uuid: abca7e7c-38c3-44f5-8d8a-4615cfce26c6
topic-tags: Security
discoiquuid: b1bd04bf-0d6d-4e6b-8c7c-eafd1a24b5fe
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# Como fortalecer e proteger formulários do AEM no ambiente OSGi {#hardening-and-securing-aem-forms-on-osgi-environment}

Saiba mais sobre recomendações e práticas recomendadas para proteger o AEM Forms no servidor OSGi.

A segurança de um ambiente de servidor é de importância primordial para uma organização. Este artigo descreve as recomendações e práticas recomendadas para proteger servidores que executam o AEM Forms. Este não é um documento abrangente que endurece o host para seu sistema operacional. Em vez disso, este artigo descreve várias configurações de segurança que você deve implementar para melhorar a segurança do aplicativo implantado. Entretanto, para garantir que os servidores de aplicativos permaneçam protegidos, você também deve implementar procedimentos de monitoramento, detecção e resposta de segurança além das recomendações fornecidas neste artigo. O documento também contém as práticas recomendadas e diretrizes para proteger a PII (Informações de identificação pessoal).

O artigo destina-se a consultores, especialistas em segurança, arquitetos de sistemas e profissionais de TI responsáveis pelo planejamento de aplicativos ou desenvolvimento de infraestrutura e implantação do AEM Forms. Essas funções incluem as seguintes funções comuns:

* Engenheiros de TI e de operações que devem implantar aplicativos e servidores da Web seguros em organizações próprias ou de clientes.
* Arquitetos e planejadores responsáveis pelo planejamento dos esforços arquitetônicos dos clientes em suas organizações.
* Especialistas em segurança da TI que se concentram em fornecer segurança em todas as plataformas dentro de suas organizações.
* Consultores da Adobe e parceiros que exigem recursos detalhados para clientes e parceiros.

A imagem a seguir exibe componentes e protocolos usados em uma implantação típica do AEM Forms, incluindo a topologia de firewall apropriada:

![arquitetura típica](assets/typical-architecture.png)

O AEM Forms é altamente personalizável e pode funcionar em muitos ambientes diferentes. Algumas das recomendações podem não ser aplicáveis à sua organização.

## Camada de transporte segura {#secure-transport-layer}

As vulnerabilidades de segurança da camada de transporte estão entre as primeiras ameaças a qualquer servidor de aplicativos voltado para a Internet ou para a intranet. Esta seção descreve o processo de endurecimento de hosts na rede contra essas vulnerabilidades. Ele aborda a segmentação de rede, o endurecimento da pilha do protocolo de controle de transmissão/protocolo TCP/IP e o uso de firewalls para proteção de host.

### Limitar pontos de extremidade abertos {#limit-open-endpoints}

Uma organização pode ter um firewall externo para restringir o acesso entre um usuário final e o farm de publicação do AEM Forms. A organização também pode ter um firewall interno para limitar o acesso entre um farm de publicação e outros elementos dentro da organização (por exemplo, instância do autor, instância de processamento, bancos de dados). Permitir firewalls para permitir acesso a um número limitado de URLs de formulários AEM para usuários finais e dentro de elementos de organizações:

#### Configurar firewall externo {#configure-external-firewall}

Você pode configurar um firewall externo para permitir que certos URLs do AEM Forms acessem a Internet. O acesso a esses URLs é necessário para preencher ou enviar um formulário adaptável, HTML5, carta de gerenciamento de correspondência ou para fazer login em um servidor de formulários AEM:

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
     <li>/content/forms/formsets/profile/</li> 
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
   <td>Portal de formulários </td> 
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

#### Configurar firewall interno {#configure-internal-firewall}

Você pode configurar o firewall interno para permitir que determinados componentes do AEM Forms (por exemplo, instância do autor, instância de processamento, bancos de dados) se comuniquem com o farm de publicação e outros componentes internos mencionados no diagrama de topologia:

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
   <td>Servidor de complementos de fluxo de trabalho de formulários (AEM Forms no servidor JEE)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### Configurar permissões do repositório e ACLs (Access Control Lists, listas de controle de acesso) {#setup-repository-permissions-and-access-control-lists-acls}

Por padrão, os ativos disponíveis nos nós de publicação são acessíveis a todos. O acesso somente leitura está ativado para todos os ativos. É necessário ativar o acesso anônimo. Se você planeja restringir a exibição do formulário e enviar o acesso somente a usuários autenticados, use um grupo comum para permitir que somente usuários autenticados tenham acesso somente leitura aos ativos disponíveis nos nós de publicação. Os seguintes locais/diretórios contêm ativos de formulários que exigem proteção (acesso somente leitura para usuários autenticados):

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## Gerenciar dados de formulários com segurança {#securely-handle-forms-data}

O AEM Forms armazena dados em locais predefinidos e pastas temporárias. Você deve proteger os dados para evitar um uso não autorizado.

### Configurar limpeza periódica da pasta temporária {#setup-periodic-cleanup-of-temporary-folder}

Quando você configura formulários para anexos de arquivo, verifica ou visualiza componentes, os dados correspondentes são armazenados nos nós de publicação em /tmp/fd/. Os dados são apagados periodicamente. Você pode modificar o trabalho de expurgação de dados padrão para ser mais agressivo. Para modificar o trabalho programado para expurgar dados, abra o Console da Web do AEM, abra a Tarefa de limpeza temporária de armazenamento do AEM Forms e modifique a expressão Cron.

Nos cenários acima mencionados, os dados são salvos somente para usuários autenticados. Além disso, os dados são protegidos com ACLs (Access Control Lists, listas de controle de acesso). Portanto, modificar a limpeza de dados é uma etapa adicional para proteger as informações.

### Dados protegidos salvos pela ação de envio do portal de formulários {#secure-data-saved-by-forms-portal-submit-action}

Por padrão, a ação de envio de formulários adaptáveis pelo portal de formulários salva dados no repositório local do nó de publicação. Os dados são salvos em /content/forms/fp. **Não é recomendado armazenar dados na instância de publicação.**

Você pode configurar o serviço de armazenamento para enviar via rede para o cluster de processamento sem salvar nada localmente no nó de publicação. O cluster de processamento reside em uma zona segura atrás do firewall privado e os dados permanecem seguros.

Use as credenciais do servidor de processamento do serviço de configurações do AEM DS para postar dados do nó de publicação no servidor de processamento. É recomendável usar credenciais de um usuário não administrativo restrito com acesso de leitura e gravação ao repositório do servidor de processamento. Para obter mais informações, consulte [Configuração de serviços de armazenamento para rascunhos e envios](/help/forms/using/configuring-draft-submission-storage.md).

### Dados protegidos manipulados pelo FDM (form Data Model) {#secure-data-handled-by-form-data-model-fdm}

Use contas de usuário com privilégios mínimos obrigatórios para configurar fontes de dados para o FDM (form Data Model, modelo de dados de formulário). O uso de conta administrativa pode fornecer acesso aberto de metadados e entidades de esquema a usuários não autorizados.\
A integração de dados também fornece métodos para autorizar solicitações de serviço do FDM. Você pode inserir mecanismos de autorização de pré e pós execução para validar uma solicitação. As solicitações de serviço são geradas durante o preenchimento prévio de um formulário, o envio de um formulário e a chamada de serviços por meio de uma regra.

**** Autorização de pré-processamento: Você pode usar a autorização de pré-processamento para validar a autenticidade de uma solicitação antes de executá-la. Você pode usar entradas, serviço e detalhes da solicitação para permitir ou interromper a execução da solicitação. Você pode retornar uma exceção de integração de dados OPERATION_ACCESS_DENIED se a execução for interrompida. Você também pode modificar a solicitação do cliente antes de enviá-la para execução. Por exemplo, alterar a entrada e adicionar informações adicionais.

**** Autorização após o processo: Você pode usar a autorização pós-processo para validar e controlar os resultados antes de retornar os resultados ao solicitante. Você também pode filtrar, ameaçar e inserir dados adicionais aos resultados.

### Limitar o acesso do usuário {#limit-user-access}

Um conjunto diferente de personas do usuário é necessário para as instâncias de autor, publicação e processamento. Não execute nenhuma instância com credenciais de administrador.

**Em uma instância de publicação:**

* Somente usuários de grupos de usuários de formulários podem visualizar, criar rascunhos e enviar formulários.
* Somente os usuários de um grupo de agente-usuário cm podem visualizar as cartas de gerenciamento de correspondência.
* Desative todo o acesso anônimo não essencial.

**Em uma instância do autor:**

* Há um conjunto diferente de grupos predefinidos com privilégios específicos para cada persona. Atribuir usuários ao grupo.

   * Um usuário do grupo de usuários de formulários:

      * pode criar, preencher, publicar e enviar um formulário.
      * não é possível criar um formulário adaptável baseado em XDP.
      * não tem permissões para gravar scripts para formulários adaptáveis.
      * não é possível importar XDP ou qualquer pacote que contenha XDP
   * Um usuário de um grupo de usuários avançados para formulários cria, preenche, publica e envia todos os tipos de formulários, grava scripts para formulários adaptáveis, importa pacotes contendo XDP.
   * Um usuário de autores de modelo e usuários avançados de modelo pode visualizar e criar um modelo.
   * Um usuário de fdm-autores pode criar e modificar um modelo de dados de formulário.
   * Um usuário de um grupo de agente-usuário cm pode criar, visualizar e publicar cartas de gerenciamento de correspondência.
   * Um usuário de um grupo de editores de fluxo de trabalho pode criar um aplicativo de entrada e um modelo de fluxo de trabalho.


**Ao processar o autor:**

* Para salvar e enviar casos de uso remotos, crie um usuário com permissões de leitura, criação e modificação no caminho de conteúdo/formulário/fp do repositório crx.
* Adicione usuário ao grupo de usuários do fluxo de trabalho para permitir que um usuário use aplicativos da caixa de entrada do AEM.

## Elementos seguros da intranet de um ambiente do AEM Forms {#secure-intranet-elements-of-an-aem-forms-environment}

Em geral, os clusters de processamento e o complemento Forms Workflow (AEM Forms on JEE) são executados atrás de um firewall. Portanto, estes são considerados seguros. Você ainda pode executar algumas etapas para endurecer esses ambientes:

### Cluster de processamento seguro {#secure-processing-cluster}

Um cluster de processamento é executado no modo de autor, mas não o usa para atividades de desenvolvimento. Não permita que um usuário normal seja incluído em grupos de autores de conteúdo e usuários de formulário de um cluster de processamento.

### USAR as práticas recomendadas do AEM para proteger um ambiente AEM Forms {#use-aem-best-practices-to-secure-an-aem-forms-environment}

Este documento fornece instruções específicas para o ambiente do AEM Forms. Você deve tomar medidas para garantir que sua instalação subjacente do AEM esteja segura quando implantada. Para obter instruções detalhadas, consulte a documentação da Lista de verificação [de segurança do](/help/sites-administering/security-checklist.md) AEM.
