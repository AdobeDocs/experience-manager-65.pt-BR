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

AEM 6.4 em diante [A interface do usuário clássica está obsoleta](../release-notes/deprecated-removed-features.md). O Adobe não fará mais aprimoramentos na interface clássica e os usuários são incentivados a aproveitar os novos recursos avançados disponíveis na interface habilitada para toque.

A partir da versão 6.0, o AEM introduziu uma nova interface de usuário chamada de &quot;interface habilitada para toque&quot; (simplesmente chamada de &quot;interface de toque&quot;) que é alinhada ao [!DNL Adobe Experience Cloud] e às diretrizes gerais da interface do usuário do Adobe. Com quase a paridade de recursos alcançada, essa se tornou a interface padrão em AEM com a interface herdada orientada para desktop, chamada de &quot;interface clássica&quot;.

Embora a maioria dos recursos esteja presente na interface habilitada para toque, há recursos que ainda não foram concluídos e serão adicionados em versões futuras.

A lista a seguir mostra o status atual dos recursos conforme implementado no AEM 6.5.

Para obter recomendações para clientes que atualizaram para o AEM 6.5, consulte [Recomendações da interface do usuário para clientes](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Esta página aborda somente a paridade de recursos com a interface clássica. Os recursos adicionados e exclusivos à interface habilitada para toque que não estão presentes na interface clássica não são listados.

>[!NOTE]
>
>Essa lista se esforça para ser completa, mas não é exaustiva.

## Legenda {#legend}

* **Concluído**: O recurso está totalmente disponível na interface habilitada para toque.
* **Principalmente**: A maioria dos recursos está disponível na interface habilitada para toque.
* **Ausente**: O recurso não está presente na interface habilitada para toque, a interface clássica deve ser usada para fazer essa ação.
* **Substituído**: O recurso foi substituído por uma nova implementação que funciona de forma diferente.
* **Removido**: O recurso não existe mais na interface habilitada para toque e não será substituído.

## Status do recurso: Administrador de sites {#feature-status-sites-admin}

Esta é uma lista de recursos do Administrador do site da interface clássica (`/siteadmin`) tem e o status na interface habilitada para toque (`/sites.html`).

| Recurso | Status | Comentar |
|--- |--- |--- |
| Navegar pela Hierarquia do Site | Concluir | AEM 6.4 apresenta uma [exibição em árvore de conteúdo](/help/sites-authoring/basic-handling.md#content-tree). |
| Iniciar fluxo de trabalho | Concluir |  |
| Criar nova página | Concluir |  |
| Criar novo site | Concluir |  |
| Criar novo lançamento | Concluir |  |
| Criar nova cópia dinâmica | Concluir |  |
| Criar pasta | Concluir |  |
| Mostrar status da publicação | Concluir | A partir AEM 6.5, o status do workflow será mostrado na exibição em lista. |
| Pesquisar | Concluir |  |
| Copiar e colar página (Duplicar) | Concluir |  |
| Mover páginas | Concluir |  |
| Publicar páginas | Concluir |  |
| Publicar páginas sem direitos de replicação | Concluir |  |
| Publicar mais tarde | Concluir |  |
| Árvore de publicação | Concluir |  |
| Desfazer a publicação de páginas | Concluir |  |
| Cancelar a publicação de páginas sem direitos de replicação | Concluir |  |
| Desfazer a publicação mais tarde | Concluir |  |
| Excluir | Concluir |  |
| Bloquear/Desbloquear | Concluir |  |
| Exibir/editar propriedades | Concluir |  |
| Definir permissões na(s) página(s) | Concluir |  |
| Histórico da versão | Concluir |  |
| Restaurar versão | Concluir |  |
| Restaurar árvore e restaurar páginas excluídas | Ausente | Use a interface clássica. |
| Mostrar diferença entre a versão antiga e a atual | Concluir |  |
| Ações Livecopy (implantação) | Concluir |  |
| Ver cópias de idioma | Concluir |  |
| Localizar e substituir | Ausente | Use a interface clássica. |
| Caixa de entrada de notificações (eventos JCR) | Ausente | Use a interface clássica. Será substituída por uma implementação diferente. |
| Referências | Concluir | Exibição de links de página de entrada adicionados ao AEM 6.5. |

## Status do recurso: Editor de páginas {#feature-status-page-editor}

Esta é uma lista de recursos do Editor de página da interface clássica (`/cf#`) tem e o status na interface habilitada para toque (`/editor.html`).

| Recurso | Status | Comentar |
|--- |--- |--- |
| Editar páginas da Web | Concluir |  |
| Editar páginas da Web móveis | Concluir |  |
| Editar conteúdo importado pelo Importador de design | Concluir |  |
| Editar E-Mails | Concluir |  |
| Editar aplicativos móveis híbridos | Concluir |  |
| Editar Forms | Concluir |  |
| Editar ofertas | Concluir |  |
| Editar modelos de fluxos de trabalho | Concluir |  |
| Modo: Editar e visualizar | Concluir |  |
| Visualização responsiva | Concluir |  |
| Modo: Editar design | Concluir |  |
| Modo: Andaime | Concluir |  |
| Modo: Status da Live Copy | Concluir |  |
| Adicionar anotações | Concluir |  |
| Editar propriedades | Concluir |  |
| Página de implantação | Concluir |  |
| Iniciar e mostrar fluxo de trabalho | Concluir |  |
| Entrega do pacote de fluxo de trabalho | Principalmente | Completamente acessível na interface habilitada para toque. A carga de vários fluxos de trabalho ainda é apresentada na interface clássica. |
| Bloquear/desbloquear página | Concluir |  |
| Publicar página | Concluir |  |
| Desfazer a publicação da página | Concluir |  |
| Página de cópia | Removido | Use o administrador do site para [copiar páginas](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Mover página | Removido | Use o administrador do site para [mover páginas](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Excluir página | Removido | Use o administrador do site para [excluir páginas](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Mostrar referências | Removido | Use o Administrador do site para visualizar o [lista de referência detalhada](/help/sites-authoring/author-environment-tools.md#references). |
| Log de auditoria | Removido | Use o Administrador do site e [abrir o painel de atividades](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Criar versão | Removido | Use o administrador do site para [criar novas versões](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Restaurar versão | Removido | Use o administrador do site para [restaurar versões](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Alternar inicializações | Removido | Use o administrador do site para [alternar entre inicializações](/help/sites-authoring/launches-promoting.md). |
| Traduzir página | Removido | Use o administrador do site para [adicionar página a projetos de tradução](/help/sites-administering/tc-manage.md). |
| Timewarp (escolha data/hora e navegue pelo site como ele parecia) | Concluir |  |
| Definir permissões | Concluir |  |
| Interface do usuário de contexto do cliente | Substituído | Use o [ContextHub](/help/sites-authoring/ch-previewing.md) Interface do usuário do que está avançando. |
| Localizador de conteúdo para os vários tipos de mídia | Concluir |  |
| Lista de componentes | Concluir |  |
| Copiar e colar componentes | Concluir |  |
| Lista de componentes na área de transferência | Ausente |  |
| Desfazer / Refazer | Concluir |  |
| Arraste o conteúdo para o espaço reservado do componente | Concluir |  |
| Arraste o conteúdo diretamente para o espaço reservado do parsys com a criação automática do componente | Concluir |  |

## Status do recurso: Editores de texto, tabela e imagem {#feature-status-text-table-and-image-editors}

Esta é uma lista de recursos que a interface clássica Texto, Tabela e Editor de imagem têm e o status na interface habilitada para toque.

| Recurso | Status | Comentar |
|--- |--- |--- |
| Editor de rich text | Concluir | Usável no local, na caixa de diálogo e em tela cheia. |
| Ativar/desativar plug-ins do RTE | Concluir | Pode ser feito usando o [Editor de modelos](/help/sites-authoring/templates.md). |
| Usar RTE para texto sem formatação | Concluir |  |
| Plug-in do RTE: Links e âncora | Concluir |  |
| Plug-in do RTE: Mapa de caracteres | Concluir |  |
| Plug-in do RTE: Copiar/Colar | Concluir |  |
| Plug-in do RTE: Colar do Microsoft Word | Concluir |  |
| Plug-in do RTE: Localizar e substituir | Concluir |  |
| Plug-in do RTE: Formatos de texto (negrito, ...) | Concluir |  |
| Plug-in do RTE: Sub e sobrescrito | Concluir |  |
| Plug-in do RTE: Justificar | Concluir |  |
| Plug-in do RTE: Listas (marcador/números) | Concluir |  |
| Plug-in do RTE: Formato do parágrafo | Concluir |  |
| Plug-in do RTE: Estilos de texto | Concluir |  |
| Plug-in do RTE: Editor de código-fonte (HTML de edição) | Concluir | Disponível somente na caixa de diálogo e em tela cheia. |
| Plug-in do RTE: Verificador Ortográfico | Concluir |  |
| Plug-in do RTE: Tabela (Editor de tabela incorporado) | Concluir |  |
| Plug-in do RTE: Desfazer/Refazer | Concluir |  |
| Plug-in do RTE: Permitir imagens em linha | Concluir |  |
| Editor de tabela | Concluir | Usável no local, na caixa de diálogo e em tela cheia. |
| Arrastar imagem para a célula da tabela | Concluir | Utilizável em linha |
| Editor de imagem  | Concluir | Usável no local, na caixa de diálogo e em tela cheia. |
| Ativar/desativar plug-ins do IPE | Concluir | O AEM 6.3 apresentou uma interface do usuário no [Editor de modelos](/help/sites-authoring/templates.md). |
| Plug-in do IPE: Cortar | Concluir |  |
| Plug-in do IPE: Inverter | Concluir |  |
| Plug-in do IPE: Desfazer/Refazer | Concluir |  |
| Plug-in do IPE: Mapa de imagem | Concluir |  |
| Plug-in do IPE: Girar | Concluir |  |
| Plug-in do IPE: Zoom | Concluir |  |

## Status do recurso: Ferramentas {#feature-status-tools}

Esta é uma lista de várias ferramentas que a interface clássica tem e o status na interface habilitada para toque.

| Recurso | Status | Comentar |
|--- |--- |--- |
| Gerenciamento de tarefas | Substituído | 6.0 introduziu Projetos e tarefas. |
| Caixa de entrada do fluxo de trabalho | Concluir |  |
| Fluxo de trabalho para a configuração do modelo de página (`/etc/workflow/wcm/templates.html`) | Ausente | Use a interface clássica. |
| Marcação da interface do usuário do administrador | Concluir |  |
| Centro de Controle de MSM/Blueprint | Concluir |  |
| Interface do usuário do Gerenciador de Blueprint | Concluir |  |
| Interface do usuário de configuração de implementação | Ausente | Use a interface clássica. |
| Interface do usuário, grupos e permissões | Principalmente completo | Para editar permissões avançadas, use a interface clássica. |
| Limpar versões (`/etc/versioning/purge.html`) | Ausente | Use a interface clássica. |
| Verificador de links externos (`/etc/linkchecker.html`) | Ausente | Use a interface clássica. |
| Editor em massa (`/etc/importers/bulkeditor.html`) | Ausente | Use a interface clássica. |
| Fazer upload de miniaturas para adicioná-las ou substituí-las | Ausente | Use a interface clássica. |
