---
title: Status do recurso da interface de toque
description: Notas de versão específicas da  [!DNL Adobe Experience Manager] Interface Habilitada para Toque.
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 15%

---

# Status do recurso da interface de toque {#touch-ui-feature-status}

Adobe Experience Manager (AEM) 6.4 em diante [A interface clássica está obsoleta](../release-notes/deprecated-removed-features.md). A Adobe não está fazendo mais aprimoramentos na interface clássica, e os usuários são incentivados a usar os novos recursos avançados disponíveis na interface habilitada para toque.

A partir da versão 6.0, o AEM apresentou uma nova interface chamada de &quot;interface habilitada para toque&quot; (chamada de &quot;interface de toque&quot;), alinhada ao [!DNL Adobe Experience Cloud] e às diretrizes gerais da interface de usuário do Adobe. Com paridade de recursos quase atingida, isso se tornou a interface padrão no AEM com a interface herdada, orientada para desktop, conhecida como &quot;interface clássica&quot;.

Embora a maioria dos recursos esteja presente na interface habilitada para toque, há recursos que ainda não estão completos e serão adicionados em versões futuras.

A lista a seguir mostra o status dos recursos conforme implementados no AEM 6.5.

Para obter recomendações para clientes que atualizam para AEM 6.5, consulte [Recomendações da interface de usuário para clientes](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Esta página só cobre a paridade de recursos com a interface clássica. Os recursos adicionados e exclusivos à interface habilitada para toque que não estão presentes na interface clássica não são listados.

>[!NOTE]
>
>Essa lista se esforça para ser completa, mas não é exaustiva.

## Legenda {#legend}

* **Concluído**: o recurso está totalmente disponível na interface habilitada para toque.
* **Principalmente**: o recurso está disponível na maioria das vezes na interface habilitada para toque.
* **Ausente**: o recurso não está presente na interface habilitada para toque; a interface clássica deve ser usada para executar esta ação.
* **Substituído**: o recurso foi substituído por uma nova implementação que funciona de forma diferente.
* **Removido**: o recurso não existe mais na interface habilitada para toque e não será substituído.

## Status do recurso: Administrador do Sites {#feature-status-sites-admin}

Esta é uma lista de recursos que o Administrador do Site da interface clássica (`/siteadmin`) possui e o status na interface habilitada para toque (`/sites.html`).

| Destaque | Status | Comentar |
|--- |--- |--- |
| Navegar pela Hierarquia do Site | Concluído | O AEM 6.4 apresentou uma [exibição da árvore de conteúdo](/help/sites-authoring/basic-handling.md#content-tree). |
| Iniciar fluxo de trabalho | Concluído |  |
| Criar nova página | Concluído |  |
| Criar novo site | Concluído |  |
| Criar novo lançamento | Concluído |  |
| Criar nova live copy | Concluído |  |
| Criar pasta | Concluído |  |
| Mostrar status da publicação | Concluído | A partir do AEM 6.5, o status do fluxo de trabalho será mostrado na exibição de lista. |
| Pesquisar | Concluído |  |
| Copiar e colar página (Duplicado) | Concluído |  |
| Mover páginas | Concluído |  |
| Páginas do Publish | Concluído |  |
| Páginas do Publish sem direitos de replicação | Concluído |  |
| Publicar mais tarde | Concluído |  |
| árvore do Publish | Concluído |  |
| Cancelar publicação de páginas | Concluído |  |
| Cancelar publicação de páginas sem direitos de replicação | Concluído |  |
| Desfazer a publicação mais tarde | Concluído |  |
| Excluir | Concluído |  |
| Bloquear/Desbloquear | Concluído |  |
| Visualizar/Editar propriedades | Concluído |  |
| Definir permissões em páginas | Concluído |  |
| Histórico da versão | Concluído |  |
| Restaurar versão | Concluído |  |
| Restaurar árvore e restaurar páginas excluídas | Ausente | Use a interface clássica. |
| Mostrar diferença entre a versão antiga e a atual | Concluído |  |
| Ações de Live Copy (implantação) | Concluído |  |
| Consulte cópias de idioma | Concluído |  |
| Localizar e substituir | Ausente | Use a interface clássica. |
| Caixa de entrada de notificações (eventos JCR) | Ausente | Use a interface clássica. Substituído por uma implementação diferente no futuro. |
| Referências | Concluído | Exibição de links de página de entrada adicionados ao AEM 6.5. |

## Status do recurso: editor de páginas {#feature-status-page-editor}

Esta é uma lista de recursos que o Editor de Páginas da interface clássica (`/cf#`) possui e o status na interface habilitada para toque (`/editor.html`).

| Destaque | Status | Comentar |
|--- |--- |--- |
| Editar páginas da Web | Concluído |  |
| Editar páginas da Web móveis | Concluído |  |
| Editar conteúdo importado via Importador de design | Concluído |  |
| Editar Emails | Concluído |  |
| Editar aplicativos híbridos para dispositivos móveis | Concluído |  |
| Editar Forms | Concluído |  |
| Editar ofertas | Concluído |  |
| Editar modelos de fluxos de trabalho | Concluído |  |
| Modo: Editar e Visualizar | Concluído |  |
| Visualização responsiva | Concluído |  |
| Modo: Editar design | Concluído |  |
| Modo: Andaime | Concluído |  |
| Modo: status da Live Copy | Concluído |  |
| Adicionar anotações | Concluído |  |
| Editar propriedades | Concluído |  |
| Página de implantação | Concluído |  |
| Iniciar e mostrar fluxo de trabalho | Concluído |  |
| Entrega do pacote de fluxo de trabalho | Principalmente | Acessível na interface habilitada para toque. Várias cargas de fluxo de trabalho ainda apresentadas na interface clássica. |
| Bloquear/desbloquear página | Concluído |  |
| Publicar página | Concluído |  |
| Desfazer a publicação da página | Concluído |  |
| Página de cópia | Removido | Use o Administrador do Site para [copiar páginas](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Mover página | Removido | Use o Administrador do Site para [mover páginas](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Excluir página | Removido | Use o Administrador do Site para [excluir páginas](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Mostrar referências | Removido | Use o Administrador do Site para ver a [lista detalhada de referências](/help/sites-authoring/author-environment-tools.md#references). |
| Log de auditoria | Removido | Use o Administrador do Site e [abra o painel de atividades](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Criar versão | Removido | Use o Administrador do Site para [criar novas versões](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Restaurar versão | Removido | Use o Administrador do Site para [restaurar versões](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Alternar lançamentos | Removido | Use o Administrador do Site para [alternar entre inicializações](/help/sites-authoring/launches-promoting.md). |
| Traduzir página | Removido | Use o Administrador do Site para [adicionar página a projetos de tradução](/help/sites-administering/tc-manage.md). |
| Timewarp (escolha a data/hora e navegue pelo site como ele era) | Concluído |  |
| Definir permissões | Concluído |  |
| Interface do usuário do Client Context | Substituído | Use a interface do [ContextHub](/help/sites-authoring/ch-previewing.md) a partir de agora. |
| Localizador de conteúdo para os vários tipos de mídia | Concluído |  |
| Lista de componentes | Concluído |  |
| Copiar e colar componentes | Concluído |  |
| Lista de componentes na área de transferência | Ausente |  |
| Desfazer / Refazer | Concluído |  |
| Arraste o conteúdo para o espaço reservado do componente | Concluído |  |
| Arraste o conteúdo diretamente para o espaço reservado parsys com a criação automática do componente | Concluído |  |

## Status do recurso: editores de texto, tabela e imagem {#feature-status-text-table-and-image-editors}

Esta é uma lista de recursos que o Texto da interface clássica, a Tabela e o Editor de imagens têm e o status na interface habilitada para toque.

| Destaque | Status | Comentar |
|--- |--- |--- |
| Editor de rich text | Concluído | Útil no local, na caixa de diálogo e em tela inteira. |
| Ativar/desativar plug-ins do RTE | Concluído | Isso pode ser feito usando o [Editor de modelos](/help/sites-authoring/templates.md). |
| Usar RTE para texto sem formatação | Concluído |  |
| Plug-in RTE: links e âncora | Concluído |  |
| Plug-in RTE: mapa de caracteres | Concluído |  |
| Plug-in RTE: Copiar/Colar | Concluído |  |
| Plug-in RTE: Colar do Microsoft® Word | Concluído |  |
| Plug-in RTE: localizar e substituir | Concluído |  |
| Plug-in RTE: Formatos de texto (negrito, ...) | Concluído |  |
| Plug-in RTE: Sub e sobrescrito | Concluído |  |
| Plug-in RTE: Justificar | Concluído |  |
| Plug-in RTE: listas (marcadores/números) | Concluído |  |
| Plug-in RTE: Formato de parágrafo | Concluído |  |
| Plug-in RTE: Estilos de texto | Concluído |  |
| Plug-in RTE: Editor de Source (Editar HTML) | Concluído | Disponível somente na caixa de diálogo e em tela cheia. |
| Plug-in RTE: verificador ortográfico | Concluído |  |
| Plug-in do RTE: Tabela (Editor de tabela incorporado) | Concluído |  |
| Plug-in RTE: Desfazer/Refazer | Concluído |  |
| Plug-in RTE: permitir imagens integradas | Concluído |  |
| Editor de tabela | Concluído | Útil no local, na caixa de diálogo e em tela inteira. |
| Arrastar imagem para a célula da tabela | Concluído | Utilizável em linha |
| Editor de imagem | Concluído | Útil no local, na caixa de diálogo e em tela inteira. |
| Ativar/desativar plug-ins do IPE | Concluído | O AEM 6.3 apresentou uma interface no [Editor de modelos](/help/sites-authoring/templates.md). |
| Plug-in do IPE: Cortar | Concluído |  |
| Plug-in IPE: Inverter | Concluído |  |
| Plug-in do IPE: Desfazer/Refazer | Concluído |  |
| Plug-in do IPE: Mapa de imagem | Concluído |  |
| Plug-in IPE: Girar | Concluído |  |
| Plug-in IPE: Zoom | Concluído |  |

## Status do recurso: Ferramentas {#feature-status-tools}

Esta é uma lista de várias ferramentas que a interface clássica tem e o status na interface habilitada para toque.

| Destaque | Status | Comentar |
|--- |--- |--- |
| Gerenciamento de tarefas | Substituído | O 6.0 apresentou Projetos e tarefas. |
| Caixa de entrada do fluxo de trabalho | Concluído |  |
| Fluxo de Trabalho para Configuração de Modelo de Página (`/etc/workflow/wcm/templates.html`) | Ausente | Use a interface clássica. |
| Interface do administrador de marcação | Concluído |  |
| Centro de controle do MSM/Blueprint | Concluído |  |
| Interface do usuário do gerenciador de blueprint | Concluído |  |
| Interface de implantação da configuração | Ausente | Use a interface clássica. |
| Interface do usuário de usuários, grupos e permissões | Quase Concluído | Para edição avançada de permissões, use a Interface clássica. |
| Limpar Versões (`/etc/versioning/purge.html`) | Ausente | Use a interface clássica. |
| Linkchecker Externo (`/etc/linkchecker.html`) | Ausente | Use a interface clássica. |
| Editor de itens em massa (`/etc/importers/bulkeditor.html`) | Ausente | Use a interface clássica. |
| Fazer upload de miniaturas para adicionar ou substituir as miniaturas | Ausente | Use a interface clássica. |
