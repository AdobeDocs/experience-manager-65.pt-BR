---
title: Monitoramento de eventos
description: Quando o recurso de auditoria está ativado, a segurança de documentos permite monitorar determinados tipos de eventos. Pesquise e classifique facilmente a lista de eventos usando a segurança de documentos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 078b9ad1-16e2-40f4-92dc-e4093c0bb6ac
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# Monitoramento de eventos {#monitoring-events}

Quando o recurso de auditoria está ativado, a segurança de documentos permite monitorar determinados tipos de eventos. Os eventos que você pode ver dependem da sua função:

**Usuários:** podem exibir eventos auditados para seus documentos protegidos por política e para quaisquer documentos protegidos que recebam e usem.

**Coordenadores de definições de políticas:** pode exibir eventos auditados, incluindo eventos de documentos e políticas, para documentos protegidos por políticas de seus conjuntos de políticas.

**Administradores:** podem exibir eventos auditados relacionados a todos os documentos e usuários protegidos por política. Os administradores também podem rastrear outros tipos de eventos, incluindo eventos de usuário, documento, política e sistema.

>[!NOTE]
>
>Os eventos executados em uma cópia de um documento protegido por política também são rastreados como eventos no documento protegido original.

(Consulte [Opções de auditoria de evento](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).)

Um evento com falha é registrado se um usuário não autorizado tentar visualizar um documento ou tentar fazer logon usando um nome de usuário ou senha incorretos.

>[!NOTE]
>
>Eventos de acesso anônimo com falha para documentos podem ser registrados se uma política for editada para remover o acesso anônimo. Quando um recipient autorizado tenta acessar um documento protegido pela política editada, o acesso anônimo ainda é tentado, mas falhará.

Se uma política permitir o acesso anônimo do usuário, mas o administrador desativar posteriormente o acesso anônimo para segurança de documentos, o acesso anônimo falhará para documentos protegidos com a política e o evento não será registrado.

## Habilitar auditoria de eventos {#enable-event-auditing}

Esses requisitos de configuração devem ser atendidos para que a auditoria do evento ocorra:

* O sistema ou o administrador deve habilitar o recurso de auditoria para o servidor.

  (Consulte [Definindo configurações de privacidade e auditoria de eventos](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings).)

* A política usada para proteger o documento deve ter a auditoria habilitada. (Consulte [Criação e edição de políticas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## Pesquisar um evento {#search-for-an-event}

Você pode pesquisar a lista de eventos e visualizar descrições mais detalhadas sobre os eventos. As descrições detalhadas incluem informações como ID do evento, descrição, endereço IP, organização, usuário afetado, data e hora em que o evento ocorreu, atividades negadas e eventos off-line (quando os usuários tentam usar um documento quando não estão conectados à segurança de documentos).

Você pode pesquisar eventos na página Eventos usando uma combinação de critérios de pesquisa de eventos e as datas em que os eventos ocorreram. Os eventos que você pode pesquisar dependem da sua função:

**Usuários:** podem exibir eventos auditados para seus documentos protegidos por política e para quaisquer documentos protegidos que recebam e usem. Estas opções de pesquisa estão disponíveis:

**Eventos relacionados
para mim:** Os usuários podem encontrar eventos para qualquer documento protegido por política que tenham criado ou recebido. Por exemplo, se um usuário abrir, visualizar ou imprimir um documento que outra pessoa protegeu, ele verá apenas esses eventos para esse documento.

**Eventos relacionados aos meus documentos:** Os usuários podem encontrar todos os eventos relacionados a seus próprios documentos protegidos por política. Os usuários veem os eventos gerados por cada pessoa que manipulou seus documentos.

**Coordenadores de definições de políticas:** pode exibir eventos auditados, incluindo eventos de documentos e políticas, para documentos protegidos por políticas de seus conjuntos de políticas. Estas opções estão disponíveis:

**Documentar eventos onde
Sou um coordenador de conjunto de políticas:** Os coordenadores de conjuntos de políticas que têm permissão para exibir evento podem encontrar eventos relacionados a documentos protegidos por políticas de seus conjuntos de políticas.

**Eventos de política nos quais eu sou um coordenador de conjunto de políticas:** os coordenadores de conjuntos de políticas que têm permissão para exibir eventos podem encontrar eventos relacionados às políticas de seus conjuntos de políticas.

**Administradores:** podem exibir eventos auditados relacionados a todos os documentos e usuários protegidos por política. Os administradores também podem rastrear outros tipos. Além disso, os administradores podem subdividir ainda mais as pesquisas de eventos de acordo com o tipo de usuário:

**Usuários conhecidos:** Os usuários estão nos diretórios de origem ou estão registrados como usuários externos.

**Usuários anônimos:** usuários desconhecidos que acessam um documento protegido por uma política que permite acesso anônimo.

**Usuários do sistema:** eventos iniciados pelo servidor, como uma sincronização de diretório.

1. Na página Segurança de documentos, clique em Eventos.
1. Na lista Localizar, selecione os critérios de pesquisa que deseja usar. Dependendo da sua seleção na lista Localizar, uma segunda lista será exibida, fornecendo critérios de pesquisa adicionais. Se aplicável, na caixa de texto, digite os critérios de pesquisa.

   Para obter mais detalhes sobre os tipos de evento específicos, consulte [Opções de auditoria de evento](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).

1. Na lista Usuário, selecione o tipo de usuário que executou o evento:

   * Se você selecionar Usuário conhecido, uma segunda caixa de pesquisa será exibida, onde você deverá digitar o nome de usuário ou endereço de email do usuário.
   * Se você não souber esses valores, clique no ícone de pesquisa do Catálogo de endereços para procurar o usuário pelo nome ou pelo endereço de email.

1. Na lista Data, selecione uma opção de intervalo de datas. Se você selecionar Datas personalizadas, serão exibidas caixas, nas quais você digita a data no formato aaaa/mm/dd, ou poderá usar o Seletor de datas para especificar o intervalo de datas:

   * Clique no calendário para abrir o Seletor de datas.
   * Use as setas para localizar um ano e um mês.
   * Clique em um dia do mês no calendário.
   * Clique em OK para fechar o Seletor de datas.

1. Na lista Exibir, selecione o número de resultados de pesquisa a serem exibidos por página.
1. Clique em Localizar.

   Todos os eventos com falha são realçados na lista com um ícone de negado.

1. Para exibir detalhes sobre um evento, clique na descrição do evento na lista.

## Classificar a lista de eventos {#sort-the-event-list}

Você pode classificar a lista de eventos por cabeçalho de coluna para localizar os eventos mais facilmente. Os ícones de triângulo ao lado do cabeçalho da coluna indicam qual coluna é usada no momento para classificação. Um triângulo apontando para cima indica ordem crescente, enquanto um triângulo apontando para baixo indica ordem decrescente.

1. Clique no cabeçalho de coluna apropriado.
1. Para alterar a ordem de classificação, clique no cabeçalho da coluna novamente.
