---
title: Status do recurso da interface de toque
description: Notas de versão específicas para [!DNL Adobe Experience Manager] Interface habilitada para toque.
translation-type: tm+mt
source-git-commit: d938f52766154b68df2f6db2c8c49a0ad97e7e6d
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 14%

---


# Status do recurso da interface de toque {#touch-ui-feature-status}

A partir da AEM 6.4 [Interface clássica está obsoleta](../release-notes/deprecated-removed-features.md). O Adobe não fará mais aprimoramentos na interface clássica e os usuários são incentivados a aproveitar os novos recursos avançados disponíveis na interface habilitada para toque.

A partir da versão 6.0, AEM introduziu uma nova interface de usuário chamada de &quot;interface de usuário habilitada para toque&quot; (simplesmente chamada de &quot;Interface de usuário para toque&quot;) que está alinhada às [!DNL Adobe Experience Cloud] e às diretrizes gerais da interface de usuário do Adobe. Com quase a paridade de recursos alcançada, essa passou a ser a interface padrão em AEM com a interface legada orientada para desktop chamada de &quot;interface clássica&quot;.

Embora a maioria dos recursos esteja presente na interface habilitada para toque, há recursos que ainda não estão completos e serão adicionados em versões futuras.

A lista a seguir mostra o status atual dos recursos conforme implementado no AEM 6.5.

Para obter recomendações para clientes que atualizam para AEM 6.5, consulte [Recomendações da interface do usuário para clientes](/help/sites-deploying/ui-recommendations.md).

>[!NOTE]
>
>Esta página só cobre a paridade de recursos com a interface clássica. Os recursos adicionados e exclusivos à interface habilitada para toque que não estão presentes na interface clássica não são listados.

>[!NOTE]
>
>Essa lista tenta ser completa, mas não é exaustiva.

## Legenda {#legend}

* **Concluído**: O recurso está totalmente disponível na interface habilitada para toque.
* **Principalmente**: O recurso está disponível principalmente na interface habilitada para toque.
* **Ausente**: O recurso não está presente na interface habilitada para toque, a interface clássica deve ser usada para realizar essa ação.
* **Substituído**: O recurso foi substituído por uma nova implementação que funciona de forma diferente.
* **Removido**: O recurso não existe mais na interface habilitada para toque e não será substituído.

## Status do recurso: Administrador de sites {#feature-status-sites-admin}

Esta é uma lista de recursos que o Administrador do site da interface clássica (`/siteadmin`) tem e o status na interface habilitada para toque (`/sites.html`).

| Recurso | Status | Comentário |
|--- |--- |--- |
| Navegar pela Hierarquia do Site | Concluir | AEM 6.4 introduziu uma visualização de [árvore de conteúdo](/help/sites-authoring/basic-handling.md#content-tree). |
| Iniciar fluxo de trabalho | Concluir |  |
| Criar nova página | Concluir |  |
| Criar novo site | Concluir |  |
| Criar nova inicialização | Concluir |  |
| Criar nova live copy | Concluir |  |
| Criar pasta | Concluir |  |
| Mostrar status da publicação | Concluir | A partir AEM 6.5, o status do fluxo de trabalho é mostrado na visualização da lista. |
| Pesquisar   | Concluir |  |
| Copiar e colar página (Duplicado) | Concluir |  |
| Mover páginas | Concluir |  |
| Publicar páginas | Concluir |  |
| Publicar páginas sem direitos de replicação | Concluir |  |
| Publicar mais tarde | Concluir |  |
| Publicar árvore | Concluir |  |
| Desfazer a publicação de páginas | Concluir |  |
| Cancelar a publicação de páginas sem direitos de replicação | Concluir |  |
| Desfazer a publicação mais tarde | Concluir |  |
| Excluir | Concluir |  |
| Bloquear/Desbloquear | Concluir |  |
| Propriedades de visualização/edição | Concluir |  |
| Definir permissões nas páginas | Concluir |  |
| Histórico da versão | Concluir |  |
| Restaurar versão | Concluir |  |
| Restaurar árvore e restaurar páginas excluídas | Ausente | Use a interface clássica. |
| Mostrar diferença entre as versões antiga e atual | Concluir |  |
| Ações do Livecopy (implantação) | Concluir |  |
| Consulte cópias de idioma | Concluir |  |
| Localizar e substituir | Ausente | Use a interface clássica. |
| Caixa de entrada de notificação (eventos JCR) | Ausente | Use a interface clássica. Será substituído por uma implementação diferente. |
| Referências | Concluir | Exibição de links de página de entrada adicionados ao AEM 6.5. |

## Status do recurso: Editor de páginas {#feature-status-page-editor}

Esta é uma lista de recursos que o Editor de página da interface clássica (`/cf#`) tem e o status na interface habilitada para toque (`/editor.html`).

| Recurso | Status | Comentário |
|--- |--- |--- |
| Editar páginas da Web | Concluir |  |
| Editar páginas da Web móveis | Concluir |  |
| Editar conteúdo importado por meio do Importador de design | Concluir |  |
| Editar e-mails | Concluir |  |
| Editar aplicativos híbridos para dispositivos móveis | Concluir |  |
| Editar Forms | Concluir |  |
| Editar Ofertas | Concluir |  |
| Editar modelos de Workflows | Concluir |  |
| Modo: Editar e Pré-visualização | Concluir |  |
| Pré-visualização responsiva | Concluir |  |
| Modo: Editar design | Concluir |  |
| Modo: Andaime | Concluir |  |
| Modo: Status da Live Copy | Concluir |  |
| Adicionar anotações | Concluir |  |
| Editar propriedades | Concluir |  |
| Página de implantação | Concluir |  |
| Start e mostrar fluxo de trabalho | Concluir |  |
| Guia de pacotes de fluxo de trabalho | Principalmente | Completamente acessível na interface habilitada para toque. A carga de vários fluxos de trabalho ainda é apresentada na interface clássica. |
| Bloquear/desbloquear página | Concluir |  |
| Publicar página | Concluir |  |
| Desfazer a publicação da página | Concluir |  |
| Página de cópia | Removido | Use o Administrador do site para [copiar páginas](/help/sites-authoring/managing-pages.md#copying-and-pasting-a-page). |
| Mover página | Removido | Use o Administrador do site para [mover páginas](/help/sites-authoring/managing-pages.md#moving-or-renaming-a-page). |
| Excluir página | Removido | Use o Administrador do site para [excluir páginas](/help/sites-authoring/managing-pages.md#deleting-a-page). |
| Mostrar referências | Removido | Use o Administrador do site para ver a [lista de referência detalhada](/help/sites-authoring/author-environment-tools.md#references). |
| Log de auditoria | Removido | Use o Administrador do site e [abrir o painel de atividades](/help/sites-authoring/author-environment-tools.md#events-timeline). |
| Criar versão | Removido | Use o Administrador do site para [criar novas versões](/help/sites-authoring/working-with-page-versions.md#creating-a-new-version). |
| Restaurar versão | Removido | Use o Administrador do site para [restaurar versões](/help/sites-authoring/working-with-page-versions.md#reverting-to-a-page-version). |
| Interromper inicializações | Removido | Use o Administrador do site para alternar [entre inicializações](/help/sites-authoring/launches-promoting.md). |
| Traduzir página | Removido | Use o Administrador do site para [adicionar página a projetos de tradução](/help/sites-administering/tc-manage.md). |
| Timewarp (escolha a data/hora e navegue no site como ele parecia) | Concluir |  |
| Definir permissões | Concluir |  |
| Interface do usuário de contexto do cliente | Substituído | Use a interface do usuário [ContextHub](/help/sites-authoring/ch-previewing.md) para frente. |
| Localizador de conteúdo para os vários tipos de mídia | Concluir |  |
| Lista do componente | Concluir |  |
| Copiar e colar componentes | Concluir |  |
| Lista de componentes na área de transferência | Ausente |  |
| Desfazer / Refazer | Concluir |  |
| Arraste o conteúdo para o espaço reservado do componente | Concluir |  |
| Arraste o conteúdo diretamente para o espaço reservado parsys com a criação automática do componente | Concluir |  |

## Status do recurso: Editores de texto, tabela e imagem {#feature-status-text-table-and-image-editors}

Esta é uma lista de recursos que o Texto da interface clássica, a Tabela e o Editor de imagem têm e o status na interface habilitada para toque.

| Recurso | Status | Comentário |
|--- |--- |--- |
| Editor de Rich Text | Concluir | Usável no local, na caixa de diálogo e em tela cheia. |
| Ativar/desativar plug-ins RTE | Concluir | Pode ser feito usando o [Editor de modelos](/help/sites-authoring/templates.md). |
| Usar RTE para texto sem formatação | Concluir |  |
| Plug-in RTE: Links e âncora | Concluir |  |
| Plug-in RTE: Mapa de caracteres | Concluir |  |
| Plug-in RTE: Copiar/colar | Concluir |  |
| Plug-in RTE: Colar do Microsoft Word | Concluir |  |
| Plug-in RTE: Localizar e substituir | Concluir |  |
| Plug-in RTE: Formatos de texto (negrito, ...) | Concluir |  |
| Plug-in RTE: Sub e sobrescrito | Concluir |  |
| Plug-in RTE: Justificar | Concluir |  |
| Plug-in RTE: Listas (marcadores/números) | Concluir |  |
| Plug-in RTE: Formato de parágrafo | Concluir |  |
| Plug-in RTE: Estilos de texto | Concluir |  |
| Plug-in RTE: Editor de código-fonte (Editar HTML) | Concluir | Disponível apenas na caixa de diálogo e em tela cheia. |
| Plug-in RTE: Verificador ortográfico | Concluir |  |
| Plug-in RTE: Tabela (editor de tabela incorporado) | Concluir |  |
| Plug-in RTE: Desfazer/Refazer | Concluir |  |
| Plug-in RTE: Permitir imagens em linha | Concluir |  |
| Editor de tabela | Concluir | Usável no local, na caixa de diálogo e em tela cheia. |
| Arrastar imagem para a célula da tabela | Concluir | Usável em linha |
| Editor de imagem  | Concluir | Usável no local, na caixa de diálogo e em tela cheia. |
| Ativar/desativar plug-ins IPE | Concluir | AEM 6.3 introduziu uma interface no [Editor de modelos](/help/sites-authoring/templates.md). |
| Plug-in IPE: Recortar | Concluir |  |
| Plug-in IPE: Inverter | Concluir |  |
| Plug-in IPE: Desfazer/Refazer | Concluir |  |
| Plug-in IPE: Mapa de imagem | Concluir |  |
| Plug-in IPE: Girar | Concluir |  |
| Plug-in IPE: Zoom | Concluir |  |

## Status do recurso: Ferramentas {#feature-status-tools}

Esta é uma lista de várias ferramentas que a interface clássica tem e o status na interface habilitada para toque.

| Recurso | Status | Comentário |
|--- |--- |--- |
| Gerenciamento de tarefas | Substituído | 6.0 introduziu projetos e tarefas. |
| Caixa de entrada do fluxo de trabalho | Concluir |  |
| Configuração do fluxo de trabalho para modelo de página (`/etc/workflow/wcm/templates.html`) | Ausente | Use a interface clássica. |
| Marcação da interface do usuário do administrador | Concluir |  |
| Centro de controle MSM/Blueprint | Concluir |  |
| Interface do usuário do Gerenciador de Blueprint | Concluir |  |
| Interface do usuário de configuração de implantação | Ausente | Use a interface clássica. |
| Interface do usuário, grupos e permissões | Mais completo | Para a edição avançada de permissões, use a interface clássica. |
| Expurgar Versões (`/etc/versioning/purge.html`) | Ausente | Use a interface clássica. |
| Verificador de links externos (`/etc/linkchecker.html`) | Ausente | Use a interface clássica. |
| Editor em massa (`/etc/importers/bulkeditor.html`) | Ausente | Use a interface clássica. |
| Carregar miniaturas para adicioná-las ou substituí-las | Ausente | Use a interface clássica. |
