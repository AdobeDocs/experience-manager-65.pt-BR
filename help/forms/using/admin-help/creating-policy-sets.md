---
title: Criação e gerenciamento de conjuntos de políticas
description: Os conjuntos de políticas são usados para agrupar políticas que têm um objetivo comercial comum. É possível criar, editar e excluir políticas em um conjunto de políticas.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 736926af-ae41-4da3-b181-444de72407bd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 0%

---

# Criação e gerenciamento de conjuntos de políticas {#creating-and-managing-policy-sets}

Os conjuntos de políticas são usados para agrupar políticas que têm um objetivo comercial comum. Os conjuntos de políticas podem ser disponibilizados para um subconjunto de usuários no sistema.

Cada conjunto de políticas tem pelo menos um coordenador de conjunto de políticas associado. A variável *coordenador de conjunto de políticas* é um administrador ou um usuário que tem permissões adicionais. O coordenador de conjunto de políticas normalmente é um especialista na organização que pode criar melhor as políticas em um determinado conjunto de políticas.

Os coordenadores de definições de políticas podem executar estas tarefas:

* Criar novas políticas
* Editar e excluir qualquer política no conjunto de políticas
* Editar configurações do conjunto de políticas
* Adicionar e remover coordenadores do conjunto de políticas
* Exibir eventos de política e documento para qualquer política ou documento no conjunto de políticas
* Revogar acesso a documentos
* Alternar políticas para o documento

Os conjuntos de políticas são criados e excluídos na interface do administrador da segurança de documentos por superusuários e coordenadores de definições de políticas que têm permissão para isso.

Quando você exclui um conjunto de políticas, as políticas que faziam parte do conjunto não podem ser aplicadas a novos documentos. No entanto, você pode exibir as informações de política no console de administração e nas páginas da Web do usuário final para políticas que ainda estão em uso. Você pode exibir as informações de política na página de detalhes do documento para qualquer documento protegido pela política. As políticas ainda em uso podem ser editadas.

O superusuário ou coordenador de conjunto de políticas adiciona domínios criados no Gerenciamento de usuários ao usuário e grupo visíveis para cada conjunto de políticas. Essa lista é visível para o coordenador de conjunto de políticas e é usada para colocar limites em quais domínios o coordenador de conjunto de políticas pode navegar ao escolher usuários para adicionar às políticas.

Ao criar conjuntos de políticas, você atribui aos usuários a função de editor de documentos. A variável *editor de documento* é o usuário que protege o documento com uma política. Esse usuário é, por padrão, sempre incluído em uma política com direitos de acesso totais, incluindo recursos de revogação e alternância de políticas. No entanto, os administradores podem alterar os direitos de acesso do editor do documento para políticas compartilhadas. Por exemplo, o administrador pode desativar o direito do editor de documentos de revogar o acesso aos documentos ou alternar a política. Se um administrador alternar a política anexada ao documento, o nome do Editor será atualizado para o nome do proprietário da política aplicada pela última vez ao documento.

Após a instalação da segurança de documentos, um conjunto de políticas padrão é criado chamado *Conjunto de Políticas Globais*. Esse conjunto de políticas é gerenciado pelo administrador que instalou o software ou pelo coordenador de conjuntos de políticas designado para esse conjunto de políticas.

## Criar um conjunto de políticas {#create-a-policy-set}

O Conjunto de Políticas Global é o único conjunto de políticas padrão criado na instalação. Você pode criar outros conjuntos de políticas e adicionar políticas, usuários, coordenadores de definições de políticas e editores de documentos. Depois de criar um conjunto de políticas, você pode criar políticas no conjunto.

Durante a criação do conjunto de políticas, você pode usar o botão Voltar para retornar à tela anterior e o botão Salvar para salvar o conjunto de políticas a qualquer momento.

1. Na página Segurança de documentos, clique em Políticas, clique na guia Conjuntos de políticas e, em seguida, clique em Novo.
1. Na caixa Nome, digite um nome para o conjunto de políticas, opcionalmente, digite uma Descrição e, em seguida, clique em Próximo. O nome não pode conter dois pontos **:**.

   >[!NOTE]
   >
   >É possível criar um nome de conjunto de políticas que contenha caracteres estendidos; no entanto, quando uma comparação é feita entre duas strings, caracteres acentuados e não acentuados, como &quot;e&quot; e &quot;é&quot;, são considerados iguais. Quando alguém cria um conjunto de políticas, uma comparação é feita para verificar se já existe um conjunto de políticas com o mesmo nome. A comparação não pode distinguir entre nomes que são iguais, exceto para caracteres acentuados. Pressupõe-se que o conjunto de políticas já esteja adicionado ao banco de dados e o novo não esteja adicionado.

1. (Opcional) Para definir os domínios que ficam visíveis para editores de documentos quando adicionam usuários a uma política, clique em Adicionar domínios, selecione os domínios que devem se tornar pesquisáveis, clique em Adicionar e, em seguida, clique em OK.
1. Na página Adicionar usuários e grupos visíveis, clique em Avançar.
1. (Opcional) Para adicionar um coordenador de conjunto de políticas, clique em Adicionar Usuários e Grupos na página Adicionar Coordenador(es) de Conjunto de Políticas (Etapa 3 de 4) e execute estas tarefas:

   * Na caixa Localizar, digite o nome ou o endereço de email.
   * Na lista Using, selecione a opção apropriada.
   * Na lista Tipo, selecione Usuário e, na lista Em, selecione um domínio a ser pesquisado.
   * Na lista Exibir, selecione o número de resultados a serem exibidos por página e clique em Localizar.
   * Marque a caixa de seleção do usuário ou grupo a ser adicionado e clique em Avançar.
   * Selecione as permissões do coordenador do conjunto de políticas e clique em Adicionar. As seguintes permissões podem ser definidas:

      * Exibir eventos
      * Gerenciar documentos (revogar e restabelecer o acesso aos documentos e alternar as políticas nos documentos)
      * Gerenciar políticas (criar, editar e excluir políticas)
      * Gerenciamento de editores de documentos (adicionar e remover editores de documentos)
      * Delegar (adicionar e remover Coordenadores de conjuntos de políticas)

1. Repita a etapa 5 para adicionar mais coordenadores de definições de políticas.
1. Revise as configurações do coordenador de conjunto de políticas e clique em Próximo.
1. Clique em Adicionar usuários e grupos para adicionar editores de documento que podem usar as políticas no conjunto de políticas para proteger documentos.
1. Na página Adicionar editores de documentos, execute estas tarefas:

   * Na caixa Localizar, digite o nome ou o endereço de email.
   * Na lista Using, selecione a opção apropriada.
   * Na lista Tipo, selecione Usuário e, na lista Em, selecione um domínio a ser pesquisado.
   * Na lista Exibir, selecione o número de resultados a serem exibidos por página e clique em Localizar.
   * Marque as caixas de seleção dos usuários e grupos a serem adicionados, clique em Adicionar e em OK.

1. Clique em Salvar.

Agora é possível adicionar políticas ao seu conjunto de políticas. (Consulte [Criação e edição de políticas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## Editar um conjunto de políticas {#edit-a-policy-set}

1. Na página Segurança de documentos, clique em Políticas, clique na guia Conjuntos de políticas e clique na política definida para editar.
1. Clique na guia apropriada e edite conforme necessário:

   * **Detalhe:** Edite o nome e a descrição do conjunto de políticas.
   * **Políticas:** Criar, ativar, editar e excluir políticas no conjunto de políticas.
   * **Usuários e grupos visíveis:** Adicione e remova usuários e grupos visíveis que possam ser incluídos em uma política.
   * **Coordenadores de conjuntos de políticas:** Adicionar, remover e alterar permissões para coordenadores.
   * **Editores de documentos:** Adicione e remova usuários que podem publicar documentos usando as políticas do conjunto.

1. Para excluir um usuário ou grupo visível, o Coordenador de conjuntos de políticas ou o Editor de documentos, clique na guia apropriada, marque a caixa de seleção da entrada, clique em Excluir e clique em OK.
1. Para adicionar usuários ou grupos visíveis, um Coordenador de conjuntos de políticas ou Editores de documentos, clique na guia apropriada, clique em Adicionar usuários ou grupos, procure o usuário ou grupo a ser adicionado, selecione a entrada, clique em Adicionar e, em seguida, clique em OK.
1. Na guia Políticas, procure por políticas a serem adicionadas ao conjunto de políticas e crie novas políticas:

   * Para pesquisar uma política, selecione ID da Política ou Nome da Política, digite o valor correspondente, selecione o número de itens a serem exibidos e clique em Localizar.
   * Para obter detalhes sobre como criar uma política, consulte [Criação e edição de políticas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).

## Excluir um conjunto de políticas {#delete-a-policy-set}

Quando você exclui um conjunto de políticas, as políticas que faziam parte do conjunto não podem ser aplicadas a novos documentos. No entanto, você pode exibir as informações de política no console de administração e nas páginas da Web do usuário final para políticas que ainda estão em uso. Você pode exibir as informações de política na página de detalhes do documento para qualquer documento protegido pela política. As políticas ainda em uso podem ser editadas.

1. Clique em Políticas e clique na guia Conjuntos de políticas.
1. Marque a caixa de seleção do conjunto de políticas a ser excluído.
1. Clique em Excluir e em OK.
