---
title: Visão Principal para Gerenciamento de Permissões
seo-title: Principal View for Permissions Management
description: Saiba mais sobre a nova interface da interface do usuário de toque que facilita o gerenciamento de permissões.
seo-description: Learn about the new Touch UI interface that facilitates permissions management.
uuid: 16c5889a-60dd-4b66-bbc4-74fbdb5fc32f
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: db8665fa-353f-45c2-8e37-169d5c1df873
docset: aem65
exl-id: 4ce19c95-32cb-4bb8-9d6f-a5bc08a3688d
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 1%

---

# Visão Principal para Gerenciamento de Permissões{#principal-view-for-permissions-management}

## Visão geral {#overview}

O AEM 6.5 apresenta o Gerenciamento de permissões para usuários e grupos. A funcionalidade principal permanece a mesma da interface clássica, mas é mais fácil de usar e eficiente.

## Como usar {#how-to-use}

### Acesso à interface do usuário {#accessing-the-ui}

O novo gerenciamento de permissões baseado na interface do usuário é acessado pelo cartão Permissões em Segurança, como mostrado abaixo:

![](assets/screen_shot_2019-03-17at63333pm.png)

A nova exibição facilita visualizar todo o conjunto de privilégios e restrições de um determinado principal em todos os caminhos em que as Permissões foram concedidas explicitamente. Isso remove a necessidade de acessar o

CRXDE para gerenciar privilégios e restrições avançados. Foi consolidado na mesma perspectiva. A exibição assume como padrão o Grupo &quot;todos&quot;.

![](assets/unu-1.png)

Existe um filtro que permite ao usuário selecionar o tipo de principals a serem observados **Usuários**, **Grupos** ou **Todos** e procurar qualquer principal **.**

![](assets/image2019-3-20_23-52-51.png)

### Exibindo Permissões para um Principal {#viewing-permissions-for-a-principal}

O quadro à esquerda permite que os usuários rolem para baixo para localizar qualquer principal ou pesquisar por um Grupo ou Usuário com base no filtro selecionado, conforme mostrado abaixo:

![](assets/doi-1.png)

Clicar no nome mostra as permissões atribuídas à direita. O painel de permissões mostra a lista de Entradas de Controle de Acesso em caminhos específicos junto com restrições configuradas.

![](assets/trei-1.png)

### Adicionando nova Entrada de Controle de Acesso para um Principal {#adding-new-access-control-entry-for-a-principal}

Novas permissões podem ser adicionadas adicionando uma nova Entrada de controle de acesso clicando no botão Adicionar ACE.

![](assets/patru.png)

Isso exibe a janela mostrada abaixo, a próxima etapa é escolher um caminho onde a permissão precisa ser configurada.

![](assets/cinci-1.png)

Aqui, selecionamos um caminho para o qual queremos configurar uma permissão **dam-users**:

![](assets/sase-1.png)

Depois que o caminho é selecionado, o fluxo de trabalho volta a essa tela, onde o usuário pode selecionar um ou mais privilégios dos namespaces disponíveis (como `jcr`, `rep` ou `crx`) conforme mostrado abaixo.

Os privilégios podem ser adicionados pesquisando-se usando o campo de texto e selecionando-o na lista.

>[!NOTE]
>
>Para obter uma lista completa de privilégios e descrições, consulte [esta página](/help/sites-administering/user-group-ac-admin.md#access-right-management).

![](assets/image2019-3-21_0-5-47.png) ![](assets/image2019-3-21_0-6-53.png)

Depois que a lista de privilégios for selecionada, o usuário poderá escolher o Tipo de permissão : Negar ou Permitir, conforme mostrado abaixo.

![](assets/screen_shot_2019-03-17at63938pm.png) ![](assets/screen_shot_2019-03-17at63947pm.png)

### Uso de restrições {#using-restrictions}

Além da lista de privilégios e do Tipo de permissão em um determinado caminho, essa tela também permite adicionar restrições ao controle de acesso de granularidade fina, conforme mostrado abaixo:

![](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>Para obter mais informações sobre o que cada restrição significa, consulte [Documentação do Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html).

As restrições podem ser adicionadas, conforme mostrado abaixo, escolhendo o tipo de restrição, inserindo o valor e pressionando o **+** ícone .

![](assets/sapte-1.png) ![](assets/opt-1.png)

A nova ACE é refletida na Lista de controle de acesso, como mostrado abaixo. Observe que `jcr:write` é um privilégio agregado que inclui `jcr:removeNode` que foi adicionado acima, mas não é mostrado abaixo, pois está coberto em `jcr:write`.

### Edição de ACEs {#editing-aces}

As Entradas de Controle de Acesso podem ser editadas selecionando um principal e escolhendo o ACE que deseja editar.

Por exemplo, aqui podemos editar a entrada abaixo para **dam-users** clicando no ícone de lápis à direita:

![Adicionar restrição](assets/image2019-3-21_0-35-39.png)

A tela de edição é mostrada com ACEs configuradas pré-selecionadas, elas podem ser excluídas clicando no ícone de cruz ao lado delas ou novos privilégios podem ser adicionados para o caminho especificado, conforme mostrado abaixo.

![Editar entrada](assets/noua-1.png)

Aqui, adicionamos a variável `addChildNodes` privilégio de **dam-users** no caminho determinado.

![](assets/image2019-3-21_0-45-35.png)

As alterações podem ser salvas clicando no botão **Salvar** no canto superior direito, e as alterações refletirão nas novas permissões para **dam-users **conforme mostrado abaixo:

![](assets/zece-1.png)

### Exclusão de ACEs {#deleting-aces}

As Entradas de Controle de Acesso podem ser excluídas para remover todas as permissões concedidas a um responsável principal em um caminho específico. O ícone X ao lado da ACE pode ser usado para excluí-lo, conforme mostrado abaixo:

![](assets/image2019-3-21_0-53-19.png) ![](assets/unspe.png)

### Combinações de privilégios da interface clássica {#classic-ui-privilege-combinations}

Observe que a nova interface de usuário de permissões usa explicitamente o conjunto básico de privilégios em vez de combinações predefinidas que não refletiram verdadeiramente os privilégios subjacentes exatos que foram concedidos.

Isso gerou confusão sobre o que exatamente está sendo configurado. A tabela a seguir lista o mapeamento entre as combinações de privilégios da interface clássica e os privilégios reais que as constituem:

<table>
 <tbody>
  <tr>
   <th>Combinações de privilégios da interface clássica</th>
   <th>Privilégio da interface do usuário de permissões</th>
  </tr>
  <tr>
   <td>Leitura</td>
   <td><code>jcr:read</code></td>
  </tr>
  <tr>
   <td>Modificar</td>
   <td><p><code>jcr:modifyProperties</code></p> <p><code>jcr:lockManagement</code></p> <p><code>jcr:versionManagement</code></p> </td>
  </tr>
  <tr>
   <td>Criar</td>
   <td><p><code>jcr:addChildNodes</code></p> <p><code>jcr:nodeTypeManagement</code></p> </td>
  </tr>
  <tr>
   <td>Excluir</td>
   <td><p><code>jcr:removeNode</code></p> <p><code>jcr:removeChildNodes</code></p> </td>
  </tr>
  <tr>
   <td>Ler ACL</td>
   <td><code>jcr:readAccessControl</code></td>
  </tr>
  <tr>
   <td>Editar ACL</td>
   <td><code>jcr:modifyAccessControl</code></td>
  </tr>
  <tr>
   <td>Replicar</td>
   <td><code>crx:replicate</code></td>
  </tr>
 </tbody>
</table>
