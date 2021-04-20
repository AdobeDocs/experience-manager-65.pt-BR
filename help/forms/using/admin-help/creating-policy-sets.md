---
title: Criar e gerenciar conjuntos de políticas
seo-title: Criar e gerenciar conjuntos de políticas
description: Os conjuntos de políticas são usados para agrupar políticas que têm um objetivo comercial comum. Você pode criar, editar e excluir políticas em um conjunto de políticas.
seo-description: Os conjuntos de políticas são usados para agrupar políticas que têm um objetivo comercial comum. Você pode criar, editar e excluir políticas em um conjunto de políticas.
uuid: 11faf67c-b9b7-4394-8672-d43cace131ad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a4fb1a11-8fe3-4092-a036-1c079aea1250
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 0%

---


# Criar e gerenciar conjuntos de políticas {#creating-and-managing-policy-sets}

Os conjuntos de políticas são usados para agrupar políticas que têm um objetivo comercial comum. Os conjuntos de políticas podem ser disponibilizados a um subconjunto de usuários no sistema.

Cada conjunto de políticas tem pelo menos um coordenador de conjunto de políticas associado. O *coordenador do conjunto de políticas* é um administrador ou um usuário que tem permissões adicionais. O coordenador do conjunto de políticas é tipicamente um especialista na organização que pode criar melhor as políticas em um determinado conjunto de políticas.

Os coordenadores do conjunto de políticas podem executar estas tarefas:

* Criar novas políticas
* Editar e excluir qualquer política no conjunto de políticas
* Editar configurações do conjunto de políticas
* Adicionar e remover coordenadores para o conjunto de políticas
* Exibir eventos de política e documento para qualquer política ou documento dentro do conjunto de políticas
* Revogar acesso a documentos
* Alternar políticas para o documento

Os conjuntos de políticas são criados e excluídos na interface do administrador de segurança do documento por superusuários e coordenadores de conjuntos de políticas que têm permissão para isso.

Quando você exclui um conjunto de políticas, as políticas que faziam parte desse conjunto não podem ser aplicadas a novos documentos. No entanto, você pode exibir as informações da política no console de administração e nas páginas da Web do usuário final para as políticas que ainda estão em uso. Você pode exibir as informações da política na página de detalhes do documento para qualquer documento protegido pela política. As políticas ainda em uso podem ser editadas.

O superusuário ou coordenador de conjunto de políticas adiciona domínios criados no Gerenciamento de usuários ao usuário e grupo visíveis para cada conjunto de políticas. Essa lista é visível para o coordenador do conjunto de políticas e é usada para colocar limites em quais domínios o coordenador do conjunto de políticas pode navegar ao escolher usuários para adicionar às políticas.

Ao criar conjuntos de políticas, você atribui aos usuários a função de publicador de documentos. O *publicador de documento* é o usuário que protege o documento com uma política. Por padrão, esse usuário é sempre incluído em uma política com direitos de acesso totais, incluindo recursos de revogação e switching de política. No entanto, os administradores podem alterar os direitos de acesso do editor de documentos para políticas compartilhadas. Por exemplo, o administrador pode desabilitar o direito do publicador do documento de revogar o acesso ao documento ou alternar a política. Se um administrador mudar a política anexada ao documento, o Nome do Editor será atualizado para o nome do proprietário da política aplicada por último ao documento.

Após a instalação da segurança do documento, um conjunto de políticas padrão é criado chamado *Conjunto de Políticas Global*. Esse conjunto de políticas é gerenciado pelo administrador que instalou o software ou pelo coordenador do conjunto de políticas designado para esse conjunto de políticas.

## Criar um conjunto de políticas {#create-a-policy-set}

O Conjunto de Políticas Global é o único conjunto de políticas padrão criado na instalação. Você pode criar conjuntos de políticas adicionais e adicionar políticas, usuários, coordenadores de conjuntos de políticas e editores de documentos. Depois de criar um conjunto de políticas, você pode criar políticas dentro do conjunto.

Durante a criação do conjunto de políticas, é possível usar o botão Voltar para retornar à tela anterior e o botão Salvar para salvar o conjunto de políticas a qualquer momento.

1. Na página segurança do documento, clique em Políticas, clique na guia Conjuntos de políticas e, em seguida, clique em Novo.
1. Na caixa Nome, digite um nome para o conjunto de políticas, opcionalmente, digite uma Descrição e clique em Próximo. O nome não pode conter dois pontos **:**.

   >[!NOTE]
   >
   >É possível criar um nome de conjunto de políticas que contenha caracteres estendidos; no entanto, quando uma comparação é feita entre duas strings, caracteres acentuados e não acentuados, como &quot;e&quot; e &quot;é&quot; são considerados iguais. Quando alguém cria um conjunto de políticas, é feita uma comparação para verificar se um conjunto de políticas com o mesmo nome já existe. A comparação não pode distinguir entre nomes que são iguais, exceto caracteres acentuados. Pressupõe-se que o conjunto de políticas já esteja adicionado ao banco de dados e o novo não será adicionado.

1. (Opcional) Para definir os domínios que são visíveis para Editores de documentos quando eles adicionam usuários a uma política, clique em Adicionar domínios, selecione os domínios que podem ser pesquisados, clique em Adicionar e em OK.
1. Na página Adicionar usuários e grupos visíveis, clique em Avançar.
1. (Opcional) Para adicionar um coordenador de conjunto de políticas, clique em Adicionar Usuários e Grupos na página Adicionar Coordenadores do Conjunto de Políticas (Etapa 3 de 4) e execute estas tarefas:

   * Na caixa Localizar, digite o nome ou o endereço de email.
   * Na lista Uso, selecione a opção apropriada.
   * Na lista Tipo, selecione Usuário e, na lista Em, selecione um domínio para pesquisar.
   * Na lista Exibir, selecione o número de resultados a serem exibidos por página e clique em Localizar.
   * Marque a caixa de seleção do usuário ou grupo a ser adicionado e clique em Avançar.
   * Selecione as permissões do coordenador do conjunto de políticas e clique em Adicionar. As seguintes permissões podem ser definidas:

      * Exibir eventos
      * Gerenciar documentos (revogar e restabelecer o acesso a documentos e ativar políticas em documentos)
      * Gerenciar políticas (criar, editar e excluir políticas)
      * Gerenciar editores de documento (adicionar e remover editores de documento)
      * Delegar (adicionar e remover Coordenadores de conjunto de políticas)

1. Repita a etapa 5 para adicionar mais coordenadores de conjunto de políticas.
1. Revise as configurações do coordenador do conjunto de políticas e clique em Avançar.
1. Clique em Adicionar usuários e grupos para adicionar editores de documento que podem usar as políticas dentro do conjunto de políticas para proteger documentos.
1. Na página Adicionar Editores de Documento, execute estas tarefas:

   * Na caixa Localizar, digite o nome ou o endereço de email.
   * Na lista Uso, selecione a opção apropriada.
   * Na lista Tipo, selecione Usuário e, na lista Em, selecione um domínio para pesquisar.
   * Na lista Exibir, selecione o número de resultados a serem exibidos por página e clique em Localizar.
   * Marque as caixas de seleção dos usuários e grupos a serem adicionados, clique em Adicionar e em OK.

1. Clique em Salvar.

Agora é possível adicionar políticas ao seu conjunto de políticas. (Consulte [Criar e editar políticas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## Editar um conjunto de políticas {#edit-a-policy-set}

1. Na página segurança do documento, clique em Políticas, clique na guia Conjuntos de políticas e clique no conjunto de políticas para editar.
1. Clique na guia apropriada e edite conforme necessário:

   * **Detalhe:** edite o nome e a descrição do conjunto de políticas.
   * **Políticas:** crie, ative, edite e exclua políticas dentro do conjunto de políticas.
   * **Usuários e grupos visíveis:** adicione e remova usuários e grupos visíveis que possam ser incluídos em uma política.
   * **Coordenadores do conjunto de políticas:** adicione, remova e altere permissões para coordenadores.
   * **Editores de documento:** adicione e remova usuários que podem publicar documentos usando as políticas do conjunto.

1. Para excluir um usuário ou grupo visível, Coordenador do conjunto de políticas ou Editor de documentos, clique na guia apropriada, marque a caixa de seleção da entrada, clique em Excluir e em OK.
1. Para adicionar usuários ou grupos visíveis, um Coordenador de conjunto de políticas ou Editores de documentos, clique na guia apropriada, clique em Adicionar usuários ou grupos, procure o usuário ou grupo a ser adicionado, selecione a entrada, clique em Adicionar e em OK.
1. Na guia Políticas , procure por políticas para adicionar ao conjunto de políticas e criar novas políticas:

   * Para pesquisar uma política, selecione ID da política ou Nome da política, digite o valor correspondente, selecione o número de itens a serem exibidos e clique em Localizar.
   * Para obter detalhes sobre como criar uma nova política, consulte [Criar e editar políticas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).

## Excluir um conjunto de políticas {#delete-a-policy-set}

Quando você exclui um conjunto de políticas, as políticas que faziam parte desse conjunto não podem ser aplicadas a novos documentos. No entanto, você pode exibir as informações da política no console de administração e nas páginas da Web do usuário final para as políticas que ainda estão em uso. Você pode exibir as informações da política na página de detalhes do documento para qualquer documento protegido pela política. As políticas ainda em uso podem ser editadas.

1. Clique em Políticas e clique na guia Conjuntos de políticas .
1. Marque a caixa de seleção do conjunto de políticas a ser excluído.
1. Clique em Excluir e em OK.

