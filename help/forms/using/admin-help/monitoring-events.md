---
title: Monitoramento de eventos
seo-title: Monitoramento de eventos
description: Quando o recurso de auditoria está ativado, a segurança de documentos permite que você monitore determinados tipos de eventos. Você pode pesquisar e classificar facilmente a lista de eventos usando a segurança do documento.
seo-description: Quando o recurso de auditoria está ativado, a segurança de documentos permite que você monitore determinados tipos de eventos. Você pode pesquisar e classificar facilmente a lista de eventos usando a segurança do documento.
uuid: 22add6ff-536d-4cb9-8eac-b72cad5c3ecf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 379957bf-0634-4182-b269-1b010da4c90f
feature: Segurança de documentos
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 0%

---


# Monitorar eventos {#monitoring-events}

Quando o recurso de auditoria está ativado, a segurança de documentos permite que você monitore determinados tipos de eventos. Os eventos que você pode ver dependem da sua função:

**Usuários:** pode visualizar eventos auditados para seus documentos protegidos por políticas e para quaisquer documentos protegidos que eles recebam e usem.

**Coordenadores de conjunto de políticas:** pode visualizar eventos auditados, incluindo eventos de documento e de política, para documentos protegidos por políticas a partir de seus conjuntos de políticas.

**Administradores:** pode exibir eventos auditados relacionados a todos os documentos e usuários protegidos por políticas. Os administradores também podem rastrear outros tipos de eventos, incluindo eventos de usuário, documento, política e sistema.

>[!NOTE]
>
>Os eventos executados em uma cópia de um documento protegido por política também são rastreados como eventos no documento protegido original.

(Consulte [Opções de auditoria de eventos](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).)

Um evento com falha é registrado se um usuário não autorizado tentar visualizar um documento ou tentar fazer logon usando um nome de usuário ou senha incorretos.

>[!NOTE]
>
>Os eventos de acesso anônimo com falha para documentos podem ser registrados se uma política for editada para remover o acesso anônimo. Quando um recipient autorizado tenta acessar um documento que a política editada protege, o acesso anônimo ainda é tentado, mas falhará.

Se uma política permitir acesso anônimo de usuário, mas o administrador desativar posteriormente o acesso anônimo para segurança de documento, o acesso anônimo falhará para documentos protegidos com a política e o evento não será registrado.

## Habilitar auditoria de evento {#enable-event-auditing}

Esses requisitos de configuração devem ser atendidos para que a auditoria de eventos ocorra:

* O sistema ou o administrador deve ativar o recurso de auditoria para o servidor.

   (Consulte [Definição das configurações de privacidade e auditoria de eventos](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings).)

* A política usada para proteger o documento deve ter a auditoria ativada. (Consulte [Criar e editar políticas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## Procure por um evento {#search-for-an-event}

Você pode pesquisar a lista de eventos e exibir descrições mais detalhadas sobre os eventos. As descrições detalhadas incluem informações como ID do evento, descrição, endereço IP, organização, usuário afetado, data e hora em que o evento ocorreu, atividades negadas e eventos offline (quando os usuários tentam usar um documento quando não estão conectados à segurança do documento).

Você pode pesquisar eventos na página Eventos usando uma combinação de critérios de pesquisa de evento e as datas em que os eventos ocorreram. Os eventos que você pode pesquisar dependem da sua função:

**Usuários:** pode visualizar eventos auditados para seus documentos protegidos por políticas e para quaisquer documentos protegidos que eles recebam e usem. Essas opções de pesquisa estão disponíveis:

**Eventos relacionados a mim:** os usuários podem encontrar eventos para qualquer documento protegido por políticas que tenham criado ou recebido. Por exemplo, se um usuário abrir, exibir ou imprimir um documento protegido por outra pessoa, ele verá apenas esses eventos para esse documento.

**Eventos relacionados a meus documentos:** os usuários podem encontrar todos os eventos relacionados a seus próprios documentos protegidos por políticas. Os usuários veem os eventos gerados por cada pessoa que manipulou seus documentos.

**Coordenadores de conjunto de políticas:** pode visualizar eventos auditados, incluindo eventos de documento e de política, para documentos protegidos por políticas a partir de seus conjuntos de políticas. Estas opções estão disponíveis:

**Eventos de documento em que sou um coordenador de conjunto de políticas:** Os coordenadores de conjunto de políticas que têm permissão de exibição de evento podem encontrar eventos relacionados a documentos que as políticas de seus conjuntos de políticas protegem.

**Eventos de políticas em que sou coordenador de conjuntos de políticas:**  coordenadores de conjuntos de políticas que têm permissão de exibição de eventos podem encontrar eventos relacionados a políticas em seus conjuntos de políticas.

**Administradores:** pode exibir eventos auditados relacionados a todos os documentos e usuários protegidos por políticas. Os administradores também podem rastrear outros tipos. Além disso, os administradores podem subdividir as pesquisas de eventos de acordo com o tipo de usuário:

**Usuários conhecidos:** os usuários estão nos diretórios de origem ou são registrados como usuários externos.

**Usuários anônimos:** usuários desconhecidos que acessam um documento protegido por uma política que permite acesso anônimo.

**Usuários do sistema:** eventos iniciados pelo servidor, como uma sincronização de diretório.

1. Na página de segurança do documento, clique em Eventos.
1. Na lista Localizar, selecione os critérios de pesquisa que deseja usar. Dependendo da sua seleção na lista Localizar, é exibida uma segunda lista que fornece critérios de pesquisa adicionais. Se aplicável, na caixa de texto, digite os critérios de pesquisa.

   Para obter mais detalhes sobre os tipos de evento específicos, consulte [Opções de auditoria de evento](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).

1. Na lista Usuário, selecione o tipo de usuário que executou o evento:

   * Se você selecionar Usuário conhecido, uma segunda caixa de pesquisa será exibida, onde você deverá digitar o nome de usuário ou o endereço de email do usuário.
   * Se não souber esses valores, clique no ícone de pesquisa do Catálogo de endereços para procurar o usuário pelo nome de usuário ou pelo endereço de email.

1. Na lista Data, selecione uma opção de intervalo de datas. Se você selecionar Datas personalizadas, as caixas serão exibidas, onde você digita a data no formato aaaa/mm/dd, ou pode usar o Seletor de datas para especificar o intervalo de datas:

   * Clique no calendário para abrir o Seletor de datas.
   * Use as setas para encontrar um ano e mês.
   * Clique em um dia do mês no calendário.
   * Clique em OK para fechar o Seletor de datas.

1. Na lista Exibir, selecione o número de resultados de pesquisa a serem exibidos por página.
1. Clique em Localizar.

   Todos os eventos com falha são realçados na lista com um ícone negado.

1. Para exibir detalhes sobre um evento, clique na descrição do evento na lista.

## Classifique a lista de eventos {#sort-the-event-list}

Você pode classificar a lista de eventos por cabeçalho de coluna para encontrar eventos mais facilmente. Os ícones de triângulo ao lado do cabeçalho da coluna indicam qual coluna está sendo usada para classificar no momento. Um triângulo apontando para cima indica ordem crescente, enquanto um triângulo apontando para baixo indica ordem decrescente.

1. Clique no cabeçalho apropriado da coluna.
1. Para alterar a ordem de classificação, clique no cabeçalho da coluna novamente.

