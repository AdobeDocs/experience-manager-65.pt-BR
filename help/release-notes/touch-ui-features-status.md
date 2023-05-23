---
title: Status do recurso da interface de toque
description: Notas de versão específicas do [!DNL Adobe Experience Manager] Interface habilitada para toque.
exl-id: 7b71e8db-e8c6-4470-bc22-db3d4600b7fc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 15%

---

# Status do recurso da interface de toque {#touch-ui-feature-status}

AEM 6.4 em diante [A interface clássica está obsoleta](../release-notes/deprecated-removed-features.md). O Adobe não fará mais aprimoramentos na interface clássica e os usuários são incentivados a aproveitar os novos recursos avançados disponíveis na interface habilitada para toque.

A partir da versão 6.0, o AEM apresentou uma nova interface de usuário chamada de &quot;interface habilitada para toque&quot; (simplesmente chamada de &quot;interface de toque&quot;), alinhada à [!DNL Adobe Experience Cloud] e as diretrizes gerais da interface do usuário do Adobe. Com paridade de recursos quase atingida, isso se tornou a interface padrão no AEM com a interface herdada, orientada para desktop, conhecida como &quot;interface clássica&quot;.

Embora a maioria dos recursos esteja presente na interface habilitada para toque, há recursos que ainda não estão completos e serão adicionados em versões futuras.

A lista a seguir mostra o status atual dos recursos conforme implementados no AEM 6.5.

Para obter recomendações para clientes que atualizam para AEM 6.5, consulte [Recomendações da interface do usuário para clientes](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Esta página só cobre a paridade de recursos com a interface clássica. Os recursos adicionados e exclusivos à interface habilitada para toque que não estão presentes na interface clássica não são listados.

>[!NOTE]
>
>Essa lista se esforça para ser completa, mas não é exaustiva.

## Legenda {#legend}

* **Concluído**: o recurso está totalmente disponível na interface habilitada para toque.
* **Principalmente**: o recurso está disponível principalmente na interface habilitada para toque.
* **Ausente**: o recurso não está presente na interface habilitada para toque, a interface clássica deve ser usada para executar essa ação.
* **Substituído**: o recurso foi substituído por uma nova implementação que funciona de forma diferente.
* **Removido**: o recurso não existe mais na interface habilitada para toque e não será substituído.

## Status do recurso: Administrador do Sites {#feature-status-sites-admin}

Esta é uma lista de recursos do administrador do site da interface clássica (`/siteadmin`) tem e o status na interface habilitada para toque (`/sites.html`).

| Destaque | Status | Comentar |
|--- |--- |--- |
| Navegar pela Hierarquia do Site | Concluir | O AEM 6.4 introduziu um [exibição de árvore de conteúdo](/help/sites-authoring/basic-handling.md#content-tree). |
| Iniciar fluxo de trabalho | Concluir |  |
| Criar nova página | Concluir |  |
| Criar novo site | Concluir |  |
| Criar novo lançamento | Concluir |  |
| Criar nova live copy | Concluir |  |
| Criar pasta | Concluir |  |
| Mostrar status da publicação | Concluir | A partir do AEM 6.5, o status do fluxo de trabalho será mostrado na exibição de lista. |
| Pesquisar | Concluir |  |
| Copiar e colar página (Duplicado) | Concluir |  |
| Mover página(s) | Concluir |  |
| Publicar página(s) | Concluir |  |
| Publicar página(s) sem direitos de replicação | Concluir |  |
| Publicar mais tarde | Concluir |  |
| Publicar árvore | Concluir |  |
| Cancelar publicação da página(s) | Concluir |  |
| Desfazer a publicação da página sem direitos de replicação | Concluir |  |
| Desfazer a publicação mais tarde | Concluir |  |
| Excluir | Concluir |  |
| Bloquear/Desbloquear | Concluir |  |
| Visualizar/Editar propriedades | Concluir |  |
| Definir permissões em página(s) | Concluir |  |
| Histórico de versão | Concluir |  |
| Restaurar versão | Concluir |  |
| Restaurar árvore e restaurar páginas excluídas | Ausente | Use a interface clássica. |
| Mostrar diferença entre a versão antiga e a atual | Concluir |  |
| Ações do Live Copy (implantação) | Concluir |  |
| Consulte cópias de idioma | Concluir |  |
| Localizar e substituir | Ausente | Use a interface clássica. |
| Caixa de entrada de notificações (eventos JCR) | Ausente | Use a interface clássica. Será substituída por uma implementação diferente. |
| Referências | Concluir | Exibição de links de página de entrada adicionados ao AEM 6.5. |

## Status do recurso: editor de páginas {#feature-status-page-editor}

Esta é uma lista de recursos do Editor de páginas da interface clássica (`/cf#`) tem e o status no campo habilitado para toque (`/editor.html`).

| Destaque | Status | Comentar |
|--- |--- |--- |
| Editar páginas da Web | Concluir |  |
| Editar páginas da Web móveis | Concluir |  |
| Editar conteúdo importado via Importador de design | Concluir |  |
| Editar Emails | Concluir |  |
| Editar aplicativos híbridos para dispositivos móveis | Concluir |  |
| Editar Forms | Concluir |  |
| Editar ofertas | Concluir |  |
| Editar modelos de fluxos de trabalho | Concluir |  |
| Modo: Editar e Visualizar | Concluir |  |
| Visualização responsiva | Concluir |  |
| Modo: Editar design | Concluir |  |
| Modo: Andaime | Concluir |  |
| Modo: status da Live Copy | Concluir |  |
| Adicionar anotações | Concluir |  |
| Editar propriedades | Concluir |  |
| Página de implantação | Concluir |  |
| Iniciar e mostrar fluxo de trabalho | Concluir |  |
| Entrega do pacote de fluxo de trabalho | Principalmente | Completamente acessível na interface habilitada para toque. Várias cargas de fluxo de trabalho ainda apresentadas na interface clássica. |
| Bloquear/desbloquear página | Concluir |  |
| Publicar página | Concluir |  |
| Desfazer a publicação da página | Concluir |  |
| Página de cópia | Removido | Use o administrador do site para [copiar páginas](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Mover página | Removido | Use o administrador do site para [mover páginas](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Excluir página | Removido | Use o administrador do site para [excluir páginas](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Mostrar referências | Removido | Use o Administrador do site para ver o [lista de referência detalhada](/help/sites-authoring/author-environment-tools.md#references). |
| Log de auditoria | Removido | Usar o administrador do site e [abrir painel de atividades](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Criar versão | Removido | Use o administrador do site para [criar novas versões](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Restaurar versão | Removido | Use o administrador do site para [restaurar versões](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Alternar lançamentos | Removido | Use o administrador do site para [alternar entre inicializações](/help/sites-authoring/launches-promoting.md). |
| Traduzir página | Removido | Use o administrador do site para [adicionar página a projetos de tradução](/help/sites-administering/tc-manage.md). |
| Timewarp (escolha data/hora e procure o site como ele parecia) | Concluir |  |
| Definir permissões | Concluir |  |
| Interface do usuário do Client Context | Substituído | Use o [ContextHub](/help/sites-authoring/ch-previewing.md) A interface do usuário do vai para frente. |
| Localizador de conteúdo para os vários tipos de mídia | Concluir |  |
| Lista de componentes | Concluir |  |
| Copiar e colar componentes | Concluir |  |
| Lista de componentes na área de transferência | Ausente |  |
| Desfazer / Refazer | Concluir |  |
| Arraste o conteúdo para o espaço reservado do componente | Concluir |  |
| Arraste o conteúdo diretamente para o espaço reservado parsys com a criação automática do componente | Concluir |  |

## Status do recurso: editores de texto, tabela e imagem {#feature-status-text-table-and-image-editors}

Esta é uma lista de recursos que o Texto da interface clássica, a Tabela e o Editor de imagens têm e o status na interface habilitada para toque.

| Destaque | Status | Comentar |
|--- |--- |--- |
| Editor de rich text | Concluir | Útil no local, na caixa de diálogo e em tela inteira. |
| Ativar/desativar plug-ins do RTE | Concluir | Pode ser feito usando o [Editor de modelo](/help/sites-authoring/templates.md). |
| Usar RTE para texto sem formatação | Concluir |  |
| Plug-in RTE: links e âncora | Concluir |  |
| Plug-in RTE: mapa de caracteres | Concluir |  |
| Plug-in RTE: Copiar/Colar | Concluir |  |
| Plug-in RTE: Colar do Microsoft Word | Concluir |  |
| Plug-in RTE: localizar e substituir | Concluir |  |
| Plug-in RTE: Formatos de texto (negrito, ...) | Concluir |  |
| Plug-in RTE: Sub e sobrescrito | Concluir |  |
| Plug-in RTE: Justificar | Concluir |  |
| Plug-in RTE: listas (marcadores/números) | Concluir |  |
| Plug-in RTE: Formato de parágrafo | Concluir |  |
| Plug-in RTE: Estilos de texto | Concluir |  |
| Plug-in RTE: Editor de código-fonte (Editar HTML) | Concluir | Disponível somente na caixa de diálogo e em tela cheia. |
| Plug-in RTE: verificador ortográfico | Concluir |  |
| Plug-in do RTE: Tabela (Editor de tabela incorporado) | Concluir |  |
| Plug-in RTE: Desfazer/Refazer | Concluir |  |
| Plug-in RTE: permitir imagens integradas | Concluir |  |
| Editor de tabela | Concluir | Útil no local, na caixa de diálogo e em tela inteira. |
| Arrastar imagem para a célula da tabela | Concluir | Utilizável em linha |
| Editor de imagem  | Concluir | Útil no local, na caixa de diálogo e em tela inteira. |
| Ativar/desativar plug-ins do IPE | Concluir | O AEM 6.3 introduziu uma interface no [Editor de modelo](/help/sites-authoring/templates.md). |
| Plug-in do IPE: Cortar | Concluir |  |
| Plug-in IPE: Inverter | Concluir |  |
| Plug-in do IPE: Desfazer/Refazer | Concluir |  |
| Plug-in do IPE: Mapa de imagem | Concluir |  |
| Plug-in IPE: Girar | Concluir |  |
| Plug-in IPE: Zoom | Concluir |  |

## Status do recurso: Ferramentas {#feature-status-tools}

Esta é uma lista de várias ferramentas que a interface clássica tem e o status na interface habilitada para toque.

| Destaque | Status | Comentar |
|--- |--- |--- |
| Gerenciamento de tarefas | Substituído | O 6.0 apresentou Projetos e tarefas. |
| Caixa de entrada do fluxo de trabalho | Concluir |  |
| Fluxo de trabalho para configuração de modelo de página (`/etc/workflow/wcm/templates.html`) | Ausente | Use a interface clássica. |
| Interface do administrador de marcação | Concluir |  |
| Centro de controle do MSM/Blueprint | Concluir |  |
| Interface do usuário do gerenciador de blueprint | Concluir |  |
| Interface de implantação da configuração | Ausente | Use a interface clássica. |
| Usuário, grupos e permissões UI | Quase Concluído | Para edição avançada de permissões, use a Interface clássica. |
| Limpar versões (`/etc/versioning/purge.html`) | Ausente | Use a interface clássica. |
| Verificador de links externos (`/etc/linkchecker.html`) | Ausente | Use a interface clássica. |
| Editor de itens em massa (`/etc/importers/bulkeditor.html`) | Ausente | Use a interface clássica. |
| Fazer upload de miniaturas para adicionar ou substituir as miniaturas | Ausente | Use a interface clássica. |
