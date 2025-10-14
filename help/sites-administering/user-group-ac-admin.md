---
title: Administração de direitos de usuário, grupo e acesso
description: Saiba mais sobre a administração de direitos de usuário, grupo e acesso no Adobe Experience Manager.
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 5808b8f9-9b37-4970-b5c1-4d33404d3a8b
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '3073'
ht-degree: 0%

---

# Administração de usuários, grupos e direitos de acesso{#user-group-and-access-rights-administration}

A habilitação do acesso a um repositório do CRX envolve vários tópicos:

* [Direitos de Acesso](#how-access-rights-are-evaluated) - os conceitos de como eles são definidos e avaliados
* [Administração de Usuários](#user-administration) - gerenciando as contas individuais usadas para acesso
* [Administração de Grupo](#group-administration) - simplifique o gerenciamento de usuários formando grupos
* [Gerenciamento de Direitos de Acesso](#access-right-management) - definindo políticas que controlam como esses usuários e grupos podem acessar recursos

Os elementos básicos são:

**Contas de Usuário** - O CRX autentica o acesso identificando e verificando um usuário (através da identificação de uma pessoa ou de outro aplicativo) de acordo com os detalhes mantidos na conta de usuário.

No CRX, cada conta de usuário é um nó no espaço de trabalho. Uma conta de usuário do CRX tem as seguintes propriedades:

* Ele representa um usuário do CRX.
* Ele contém um nome de usuário e uma senha.
* Aplicável para esse espaço de trabalho.
* Ele não pode ter subusuários. Para direitos de acesso hierárquicos, você deve usar grupos.

* Você pode especificar direitos de acesso para a conta de usuário.

  No entanto, para simplificar o gerenciamento, a Adobe recomenda que (na maioria dos casos) você atribua direitos de acesso a contas de grupo. A atribuição de direitos de acesso para cada usuário individual torna-se rapidamente difícil de gerenciar (as exceções são determinados usuários do sistema quando apenas uma ou duas instâncias existem).

**Contas de Grupo** - As contas de grupo são coleções de usuários e/ou outros grupos. Eles são usados para simplificar o gerenciamento, uma vez que os direitos de acesso atribuídos a um grupo são aplicados automaticamente a todos os usuários desse grupo. Um usuário não precisa pertencer a nenhum grupo, mas geralmente pertence a vários.

No CRX, um grupo tem as seguintes propriedades:

* Ele representa um grupo de usuários com direitos de acesso comuns. Por exemplo, autores ou desenvolvedores.
* Aplicável para esse espaço de trabalho.
* Ele pode ter membros; eles podem ser usuários individuais ou outros grupos.
* O agrupamento hierárquico pode ser obtido com relacionamentos de membros. Não é possível colocar um grupo diretamente abaixo de outro grupo no repositório.
* Você pode definir os direitos de acesso para todos os membros do grupo.

**Direitos de acesso** - O CRX usa Direitos de acesso para controlar o acesso a áreas específicas do repositório.

Isso é feito atribuindo privilégios para permitir ou negar acesso a um recurso (nó ou caminho) no repositório. Como vários privilégios podem ser atribuídos, eles devem ser avaliados para determinar qual combinação é aplicável para a solicitação atual.

O CRX permite configurar os direitos de acesso para contas de usuário e de grupo. Os mesmos princípios básicos de avaliação são então aplicados a ambos.

## Como os direitos de acesso são avaliados {#how-access-rights-are-evaluated}

>[!NOTE]
>
>O CRX implementa o controle de acesso [&#x200B; conforme definido pela JSR-283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).
>
>Uma instalação padrão de um repositório do CRX é configurada para usar listas de controle de acesso baseadas em recursos. Esta é uma possível implementação do controle de acesso JSR-283 e uma das implementações presentes com Jackrabbit.

### Assuntos e Principais {#subjects-and-principals}

O CRX usa dois conceitos principais ao avaliar direitos de acesso:

* **principal** é uma entidade que possui direitos de acesso. Os principais incluem:

   * Uma conta de usuário
   * Uma conta de grupo

     Se uma conta de usuário pertencer a um ou mais grupos, ela também será associada a cada uma dessas entidades de grupo.

* Um **assunto** é usado para representar a origem de uma solicitação.

  É usado para consolidar os direitos de acesso aplicáveis a essa solicitação. Elas são obtidas de:

   * O usuário principal

     Os direitos que você atribui diretamente à conta de usuário.

   * Todos os grupos principais associados a esse usuário

     Todos os direitos são atribuídos a qualquer um dos grupos aos quais o usuário pertence.

  O resultado é usado para permitir ou negar acesso ao recurso solicitado.

#### Compilando a lista de Direitos de Acesso para um Assunto {#compiling-the-list-of-access-rights-for-a-subject}

No CRX, o assunto depende de:

* o usuário principal
* todas as entidades de grupo associadas a esse usuário

A lista de direitos de acesso aplicáveis à entidade é construída a partir de:

* os direitos atribuídos diretamente à conta do usuário
* além de todos os direitos atribuídos a qualquer um dos grupos aos quais o usuário pertence

![chlimage_1-56](assets/chlimage_1-56.png)

>[!NOTE]
>
>* A CRX não considera nenhuma hierarquia de usuário ao compilar a lista.
>* O CRX usa uma hierarquia de grupo somente quando você inclui um grupo como membro de outro grupo. Não há herança automática de permissões de grupo.
>* A ordem em que você especifica os grupos não afeta os direitos de acesso.
>

### Resolução de solicitações e direitos de acesso {#resolving-request-and-access-rights}

Quando o CRX lida com a solicitação, ele compara a solicitação de acesso do assunto com a lista de controle de acesso no nó do repositório:

Portanto, se Linda solicitar a atualização do nó `/features` na seguinte estrutura do repositório:

![chlimage_1-57](assets/chlimage_1-57.png)

### Ordem de precedência {#order-of-precedence}

Os direitos de acesso no CRX são avaliados da seguinte maneira:

* As entidades do usuário sempre têm prioridade sobre as entidades do grupo, independentemente:

   * a ordem na lista de controle de acesso
   * sua posição na hierarquia do nó

* Para um determinado principal, existe (no máximo) uma negação e uma entrada de permissão em um determinado nó. A implementação sempre limpa as entradas redundantes e garante que o mesmo privilégio não seja listado nas entradas de permissão e negação.

>[!NOTE]
>
>Esse processo de avaliação é apropriado para o controle de acesso baseado em recursos de uma instalação padrão do CRX.

Tomando dois exemplos onde o usuário `aUser` é membro do grupo `aGroup`:

```xml
   + parentNode
     + acl
       + ace: aUser - deny - write
     + childNode
       + acl
         + ace: aGroup - allow - write
       + grandChildNode
```

No caso acima:

* `aUser` não recebeu permissão de gravação em `grandChildNode`.

```xml
   + parentNode
     + acl
       + ace: aUser - deny - write
     + childNode
       + acl
         + ace: aGroup - allow - write
         + ace: aUser - deny - write
       + grandChildNode
```

Neste caso:

* `aUser` não recebeu permissão de gravação em `grandChildNode`.
* A segunda ACE para `aUser` é redundante.

Os direitos de acesso de vários principais de grupo são avaliados com base em sua ordem, tanto na hierarquia quanto em uma única lista de controle de acesso.

### Práticas recomendadas {#best-practices}

A tabela a seguir lista algumas recomendações e práticas recomendadas:

<table>
 <tbody>
  <tr>
   <td>Recomendação...</td>
   <td>Motivo...</td>
  </tr>
  <tr>
   <td><i>Usar grupos</i></td>
   <td><p>Evite atribuir direitos de acesso a cada usuário. Há vários motivos para isso:</p>
    <ul>
     <li>Você tem muito mais usuários do que grupos, portanto, os grupos simplificam a estrutura.</li>
     <li>Os grupos ajudam a fornecer uma visão geral de todas as contas.</li>
     <li>A herança é mais simples com grupos.</li>
     <li>Os usuários vêm e vão. Os grupos são de longo prazo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><i>Ser positivo</i></td>
   <td><p>Sempre use as instruções Allow para especificar os direitos de acesso da entidade do grupo (sempre que possível). Evite usar uma instrução Deny.</p> <p>As entidades de grupo são avaliadas em ordem, tanto na hierarquia quanto na ordem em uma única lista de controle de acesso.</p> </td>
  </tr>
  <tr>
   <td><i>Mantenha a simplicidade</i></td>
   <td><p>Investir algum tempo e pensamento ao configurar uma nova instalação é bem pago.</p> <p>A aplicação de uma estrutura clara simplifica a manutenção e a administração contínuas, garantindo que seus colegas atuais e/ou futuros sucessores possam entender facilmente o que está sendo implementado.</p> </td>
  </tr>
  <tr>
   <td><i>Testar</i></td>
   <td>Use uma instalação de teste para praticar e garantir que você entenda os relacionamentos entre os vários usuários e grupos.</td>
  </tr>
  <tr>
   <td><i>Usuários/grupos padrão</i></td>
   <td>Sempre atualize os Usuários e grupos padrão imediatamente após a instalação para ajudar a evitar problemas de segurança.</td>
  </tr>
 </tbody>
</table>

## Administração de usuários {#user-administration}

Uma caixa de diálogo padrão é usada para **Administração de Usuário**.

Você deve estar conectado ao espaço de trabalho apropriado e, em seguida, acessar a caixa de diálogo de:

* o link **Administração de Usuário** no Console Principal do CRX
* o menu **Segurança** do CRX Explorer

![chlimage_1-58](assets/chlimage_1-58.png)

**Propriedades**

* **IDdoUsuário**

  O nome abreviado da conta é usado ao acessar o CRX.

* **Nome da Entidade**

  Um nome de texto completo para a conta.

* **Senha**

  Necessário ao acessar o CRX com esta conta.

* **ntlmhash**

  Atribuído automaticamente para cada nova conta e atualizado quando a senha é alterada.

* Você pode adicionar novas propriedades definindo um nome, tipo e valor. Clique em Salvar (símbolo de marca de verificação verde) para cada nova propriedade.

**Associação de Grupo**

Isso exibe todos os grupos aos quais a conta pertence. A coluna Herdado indica associação que foi herdada como resultado da associação de outro grupo.

Clicar em uma GroupID (quando disponível) abre a [Administração de Grupo](#group-administration) desse grupo.

**Representantes**

Com a funcionalidade Representar, um usuário pode trabalhar em nome de outro usuário.

Isso significa que uma conta de usuário pode especificar outras contas (usuário ou grupo) que podem operar com sua conta. Em outras palavras, se o usuário-B tiver permissão para representar o usuário-A, ele poderá agir usando os detalhes completos da conta do usuário-A (incluindo ID, nome e direitos de acesso).

Isso permite que as contas de personificação concluam tarefas como se estivessem usando a conta que estão representando; por exemplo, durante uma ausência ou para compartilhar uma carga excessiva a curto prazo.

Se uma conta representar outra, é difícil visualizar. Os arquivos de log não contêm informações sobre o fato de que a representação ocorreu nos eventos. Portanto, se o usuário-B estiver representando o usuário-A, todos os eventos poderão parecer como se fossem executados pelo usuário-A pessoalmente.

### Criar uma conta de usuário {#creating-a-user-account}

1. Abra a caixa de diálogo **Administração de Usuários**.
1. Clique em **Criar Usuário**.
1. Em seguida, você pode inserir as Propriedades:

   * **UserID** usado como o nome da conta.
   * **Senha** necessária ao fazer logon.
   * **Nome da Entidade** para fornecer um nome textual completo.
   * **Caminho Intermediário** que pode ser usado para formar uma estrutura de árvore.

1. Clique em Salvar (símbolo de marca de verificação verde).
1. A caixa de diálogo é expandida para que você possa fazer o seguinte:

   1. Configurar **Propriedades**.
   1. Consulte **Associação de Grupo**.
   1. Defina **Representantes**.

>[!NOTE]
>
>Às vezes, pode ocorrer uma perda de desempenho ao registrar novos usuários em instalações que têm um alto número de ambos:
>
>* usuários
>* grupos com muitos membros
>

### Atualizar uma conta de usuário {#updating-a-user-account}

1. Com a caixa de diálogo **Administração de Usuário**, abra a exibição de lista de todas as contas.
1. Navegue pela estrutura de árvore.
1. Clique na conta necessária para abri-la para edição.
1. Faça uma alteração e clique em Salvar (símbolo de marca de verificação verde) para essa entrada.
1. Clique em **Fechar** para concluir ou em **Lista...** para retornar à lista de todas as contas de usuário.

### Remover uma conta de usuário {#removing-a-user-account}

1. Com a caixa de diálogo **Administração de Usuário**, abra a exibição de lista de todas as contas.
1. Navegue pela estrutura de árvore.
1. Selecione a conta necessária e clique em **Remover Usuário**; a conta será excluída imediatamente.

>[!NOTE]
>
>Isso remove o nó dessa entidade do repositório.
>
>As entradas de direito de acesso não são removidas. Isso garante a integridade histórica.

### Definição de propriedades {#defining-properties}

Você pode definir **Propriedades** para contas novas ou existentes:

1. Abra a caixa de diálogo **Administração de Usuário** para a conta apropriada.
1. Defina um nome de **Propriedade**.
1. Selecione o **Tipo** na lista suspensa.
1. Defina o **Valor**.
1. Clique em Salvar (símbolo de clique verde) para a nova propriedade.

As propriedades existentes podem ser excluídas com o símbolo de lixeira.

Exceto pela Senha, as propriedades não podem ser editadas, elas devem ser excluídas e recriadas.

#### Alterar a senha {#changing-the-password}

A **Senha** é uma propriedade especial que pode ser alterada clicando no link **Alterar Senha**.

Você também pode alterar a senha da sua conta de usuário no menu **Segurança** do CRX Explorer.

### Definir um representante {#defining-an-impersonator}

É possível definir Representantes para contas novas ou existentes:

1. Abra a caixa de diálogo **Administração de Usuário** para a conta apropriada.
1. Especifique a conta que poderá representar essa conta.

   Você pode usar Procurar... para selecionar uma conta existente.

1. Clique em Salvar (símbolo de marca de verificação verde) para a nova propriedade.

## Administração de grupo {#group-administration}

Caixa de diálogo padrão usada para **Administração de Grupo**.

Você deve estar conectado ao espaço de trabalho apropriado e, em seguida, acessar a caixa de diálogo de:

* o link **Administração de Grupo** no Console Principal do CRX
* o menu **Segurança** do CRX Explorer

![chlimage_1-8](assets/chlimage_1-8.jpeg)

**Propriedades**

* **IDdoGrupo**

  Nome abreviado da conta de grupo.

* **Nome da Entidade**

  Um nome de texto completo para a conta de grupo.

* Você pode adicionar novas propriedades definindo um nome, tipo e valor. Clique em Salvar (símbolo de marca de verificação verde) para cada nova propriedade.

* **Membros**

  Você pode adicionar usuários ou outros grupos como membros deste grupo.

**Associação de Grupo**

Isso exibe todos os grupos aos quais a conta de grupo atual pertence. A coluna Herdado indica associação que foi herdada como resultado da associação de outro grupo.

Clicar em uma ID de grupo abre a caixa de diálogo desse grupo.

**Membros**

Lista todas as contas (usuários e/ou grupos) que são membros do grupo atual.

A coluna **Herdada** indica associação que foi herdada como resultado da associação de outro grupo.

>[!NOTE]
>
>Quando a função Proprietário, Editor ou Visualizador é atribuída a um usuário em qualquer pasta de Ativos, um novo grupo é criado. O nome do grupo tem o formato `mac-default-<foldername>` para cada pasta na qual as funções são definidas.

### Criar uma conta de grupo {#creating-a-group-account}

1. Abra a caixa de diálogo **Administração de Grupo**.
1. Clique em **Criar Grupo**.
1. Em seguida, você pode inserir as Propriedades:

   * **Nome da Entidade** para fornecer um nome textual completo.
   * **Caminho Intermediário** que pode ser usado para formar uma estrutura de árvore.

1. Clique em Salvar (símbolo de marca de verificação verde).
1. A caixa de diálogo é expandida para que você possa:

   1. Configurar **Propriedades**.
   1. Consulte **Associação de Grupo**.
   1. Gerenciar **Membros**.

### Atualizando uma conta de grupo {#updating-a-group-account}

1. Com a caixa de diálogo **Administração de Grupo**, abra a exibição de lista de todas as contas.
1. Navegue pela estrutura de árvore.
1. Clique na conta necessária para abri-la para edição.
1. Faça uma alteração e clique em Salvar (símbolo de marca de verificação verde) para essa entrada.
1. Clique em **Fechar** para concluir ou em **Lista...** para retornar à lista de todas as contas de grupo.

### Remover uma conta de grupo {#removing-a-group-account}

1. Com a caixa de diálogo **Administração de Grupo**, abra a exibição de lista de todas as contas.
1. Navegue pela estrutura de árvore.
1. Selecione a conta necessária e clique em **Remover Grupo**; a conta será excluída imediatamente.

>[!NOTE]
>
>Isso remove o nó dessa entidade do repositório.
>
>As entradas de direito de acesso não são removidas. Isso garante a integridade histórica.

### Definição de propriedades {#defining-properties-1}

Você pode definir Propriedades para contas novas ou existentes:

1. Abra a caixa de diálogo **Administração de Grupo** para a conta apropriada.
1. Defina um nome de **Propriedade**.
1. Selecione o **Tipo** na lista suspensa.
1. Defina o **Valor**.
1. Clique em Salvar (símbolo de marca de verificação verde) para a nova propriedade.

As propriedades existentes podem ser excluídas com o símbolo de lixeira.

### Membros {#members}

É possível adicionar membros ao grupo atual:

1. Abra a caixa de diálogo **Administração de Grupo** para a conta apropriada.
1. Ou:

   * Insira o nome do membro necessário (conta de usuário ou de grupo).
   * Ou use **Procurar...** para procurar e selecionar a entidade (conta de usuário ou de grupo) que deseja adicionar.

1. Clique em Salvar (símbolo de marca de verificação verde) para a nova propriedade.

Ou exclua um membro existente com o símbolo de lixeira.

## Gerenciamento de direitos de acesso {#access-right-management}

Com a guia **Controle de acesso** do CRXDE Lite, você pode definir as políticas de controle de acesso e atribuir os privilégios relacionados.

Por exemplo, para **Caminho Atual**, selecione o recurso desejado no painel esquerdo, a guia Controle de Acesso no painel inferior direito:

![crx_accesscontrol_tab](assets/crx_accesscontrol_tab.png)

As políticas são categorizadas de acordo com:

* **Políticas de Controle de Acesso Aplicáveis**

  Essas políticas podem ser aplicadas.

  Estas são as políticas disponíveis para criar uma política local. Quando você seleciona e adiciona uma política aplicável, ela se torna uma política local.

* **Políticas do Controle de Acesso Local**

  Estas são as políticas de controle de acesso que você aplicou. Em seguida, você pode atualizá-los, solicitá-los ou removê-los.

  Uma política local substitui todas as políticas herdadas do pai.

* **Políticas do controle de acesso efetivo**

  Estas são as políticas de controle de acesso que agora estão em vigor para qualquer solicitação de acesso. Eles mostram as políticas agregadas derivadas das políticas locais e de qualquer herdada do pai.

### Seleção de política {#policy-selection}

As políticas podem ser selecionadas para:

* **Caminho Atual**

  Como no exemplo acima, selecione um recurso no repositório. As políticas para esse &quot;caminho atual&quot; são mostradas.

* **Repositório**

  Seleciona o controle de acesso no nível do repositório. Por exemplo, ao definir o privilégio `jcr:namespaceManagement`, que é relevante somente para o repositório, não para um nó.

* **Entidade**

  Uma entidade registrada no repositório.

  Você pode digitar o nome da **Entidade de Segurança** ou clicar no ícone à direita do campo para abrir a caixa de diálogo **Selecionar Entidade de Segurança**.

  Isso permite **Pesquisar** por um **Usuário** ou **Grupo**. Selecione a entidade de segurança necessária na lista resultante e clique em **OK** para trazer o valor de volta para a caixa de diálogo anterior.

![crx_accesscontrol_selectprincipal](assets/crx_accesscontrol_selectprincipal.png)

>[!NOTE]
>
>Para simplificar o gerenciamento, o Adobe recomenda que você atribua direitos de acesso a contas de grupo, não a contas de usuário individuais.
>
>É mais fácil gerenciar alguns grupos do que muitas contas de usuário.

### Privilégios {#privileges}

Os seguintes privilégios estão disponíveis para seleção ao adicionar uma entrada de controle de acesso (consulte a [API de Segurança](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/security/Privilege.html) para obter detalhes completos):

<table>
 <tbody>
  <tr>
   <th><strong>Nome do privilégio</strong></th>
   <th><strong>Que controla o privilégio de...</strong></th>
  </tr>
  <tr>
   <td><code>jcr:read</code></td>
   <td>Recupere um nó e leia suas propriedades e seus valores.</td>
  </tr>
  <tr>
   <td><code>rep:write</code></td>
   <td>Este é um privilégio agregado específico do Jackrabbit de jcr:write e jcr:nodeTypeManagement.<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:all</code></td>
   <td>É um privilégio agregado que contém todos os outros privilégios predefinidos.</td>
  </tr>
  <tr>
   <td><strong>Avançado </strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>crx:replicate</code></td>
   <td>Executar replicação de um nó.</td>
  </tr>
  <tr>
   <td><code>jcr:addChildNodes</code></td>
   <td>Crie nós filhos de um nó.</td>
  </tr>
  <tr>
   <td><code>jcr:lifecycleManagement</code></td>
   <td>Executar operações de ciclo de vida em um nó.</td>
  </tr>
  <tr>
   <td><code>jcr:lockManagement</code></td>
   <td>Bloquear e desbloquear um nó; atualizar um bloqueio.</td>
  </tr>
  <tr>
   <td><code>jcr:modifyAccessControl</code></td>
   <td>Modifique as políticas de controle de acesso de um nó.</td>
  </tr>
  <tr>
   <td><code>jcr:modifyProperties</code></td>
   <td>Criar, modificar e remover as propriedades de um nó.</td>
  </tr>
  <tr>
   <td><code>jcr:namespaceManagement</code></td>
   <td>Registrar, cancelar registro e modificar definições de namespace.</td>
  </tr>
  <tr>
   <td><code>jcr:nodeTypeDefinitionManagement</code></td>
   <td>Importe definições de tipo de nó para o repositório.</td>
  </tr>
  <tr>
   <td><code>jcr:nodeTypeManagement</code></td>
   <td>Adicione e remova tipos de nó de mixin e altere o tipo de nó primário de um nó. Também inclui chamadas para Node.addNode e métodos de importação XML em que o mixin ou o tipo primário do novo nó é explicitamente especificado.</td>
  </tr>
  <tr>
   <td><code>jcr:readAccessControl</code></td>
   <td>Leia a política de controle de acesso de um nó.</td>
  </tr>
  <tr>
   <td><code>jcr:removeChildNodes</code></td>
   <td>Remova os nós filhos de um nó.</td>
  </tr>
  <tr>
   <td><code>jcr:removeNode</code></td>
   <td>Remover um nó.</td>
  </tr>
  <tr>
   <td><code>jcr:retentionManagement</code></td>
   <td>Executar operações de gerenciamento de retenção em um nó.</td>
  </tr>
  <tr>
   <td><code>jcr:versionManagement</code></td>
   <td>Executar operações de controle de versão em um nó.</td>
  </tr>
  <tr>
   <td><code>jcr:workspaceManagement</code></td>
   <td>A criação e a exclusão de espaços de trabalho por meio da API JCR.</td>
  </tr>
  <tr>
   <td><code>jcr:write</code></td>
   <td>Este é um privilégio agregado que contém:<br /> - jcr:modifyProperties<br /> - jcr:addChildNodes<br /> - jcr:removeNode<br /> - jcr:removeChildNodes</td>
  </tr>
  <tr>
   <td><code>rep:privilegeManagement</code></td>
   <td>Registre um novo privilégio.</td>
  </tr>
 </tbody>
</table>

### Registrando novos privilégios {#registering-new-privileges}

Você também pode registrar novos privilégios:

1. Na barra de ferramentas, selecione **Ferramentas** e **Privilégios** para exibir os privilégios registrados no momento.

   ![privilégios_ac](assets/ac_privileges.png)

1. Use o ícone **Registrar Privilégio** (**+**) para que você possa definir um privilégio:

   ![ac_privilegieregister](assets/ac_privilegeregister.png)

1. Clique em **OK** para salvar. O privilégio agora está disponível para seleção.

### Adicionando uma entrada de controle de acesso {#adding-an-access-control-entry}

1. Selecione seu recurso e abra a guia **Controle de acesso**.

1. Para adicionar uma nova **Política de Controle de Acesso Local**, clique no ícone **+** à direita da lista **Política de Controle de Acesso Aplicável**:

   ![crx_accesscontrol_applicable](assets/crx_accesscontrol_applicable.png)

1. Uma nova entrada aparece em **Políticas de Controle de Acesso Local:**

   ![crx_accesscontrol_newlocal](assets/crx_accesscontrol_newlocal.png)

1. Clique no ícone **+** para poder adicionar uma entrada:

   ![crx_accesscontrol_addentry](assets/crx_accesscontrol_addentry.png)

   >[!NOTE]
   >
   >No momento, é necessária uma solução alternativa para especificar uma cadeia de caracteres vazia.
   >
   >Para isso, você deve usar `""`.

1. Defina sua política de controle de acesso e clique em **OK** para salvar. Sua nova política é:

   * listado em **Política de Controle de Acesso Local**
   * as alterações são refletidas nas **Políticas do Controle de Acesso Efetivo**.

O CRX valida sua seleção; para um determinado principal, existe (no máximo) uma negação e uma entrada de permissão em um determinado nó. A implementação sempre limpa as entradas redundantes e garante que o mesmo privilégio não seja listado nas entradas de permissão e negação.

### Ordenação de Políticas do Controle de Acesso Local {#ordering-local-access-control-policies}

A ordem na lista indica a ordem em que as políticas são aplicadas.

1. Na tabela de **Políticas de Controle de Acesso Local**, selecione a entrada necessária e arraste-a para a nova posição na tabela.

   ![crx_accesscontrol_reorder](assets/crx_accesscontrol_reorder.png)

1. As alterações são mostradas nas tabelas do **Local** e das **Políticas do Controle de Acesso Efetivo**.

### Remover uma política de controle de acesso {#removing-an-access-control-policy}

1. Na tabela de **Políticas de Controle de Acesso Local**, clique no ícone vermelho (-) à direita da entrada.
1. A entrada foi removida das tabelas do **Local** e das **Políticas do Controle de Acesso Efetivo**.

### Teste de uma política de controle de acesso {#testing-an-access-control-policy}

1. Na barra de ferramentas do CRXDE Lite, selecione **Ferramentas**, em seguida **Testar Controle de Acesso...**.
1. Uma nova caixa de diálogo é aberta no painel superior direito. Selecione o **Caminho** e/ou a **Entidade** que deseja testar.
1. Clique em **Testar** para ver os resultados da sua seleção:

   ![crx_accesscontrol_test](assets/crx_accesscontrol_test.png)
