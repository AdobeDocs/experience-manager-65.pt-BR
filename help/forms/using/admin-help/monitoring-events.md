---
title: Monitoramento de eventos
seo-title: Monitoramento de eventos
description: Quando o recurso de auditoria está ativado, a segurança do documento permite que você monitore determinados tipos de eventos. Você pode pesquisar e classificar facilmente a lista de eventos usando a segurança do documento.
seo-description: Quando o recurso de auditoria está ativado, a segurança do documento permite que você monitore determinados tipos de eventos. Você pode pesquisar e classificar facilmente a lista de eventos usando a segurança do documento.
uuid: 22add6ff-536d-4cb9-8eac-b72cad5c3ecf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 379957bf-0634-4182-b269-1b010da4c90f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Monitoramento de eventos {#monitoring-events}

Quando o recurso de auditoria está ativado, a segurança do documento permite que você monitore determinados tipos de eventos. Os eventos que você pode ver dependem de sua função:

**** Usuários: Pode exibir eventos auditados para seus documentos protegidos por política e para quaisquer documentos protegidos que eles recebam e usem.

**** Coordenadores de definição de políticas: Pode exibir eventos auditados, incluindo eventos de documento e política, para documentos protegidos por políticas de seus conjuntos de políticas.

**** Administradores: Pode exibir eventos auditados relacionados a todos os documentos protegidos por política e usuários. Os administradores também podem rastrear outros tipos de eventos, incluindo eventos de usuário, documento, política e sistema.

***Observação **: Os eventos executados em uma cópia de um documento protegido por política também são rastreados como eventos no documento protegido original.*

(Consulte Opções [de auditoria de](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options)eventos.)

Um evento com falha é registrado se um usuário não autorizado tentar exibir um documento ou tentar fazer logon usando um nome de usuário ou senha incorretos.

**Observação**: Os eventos de acesso anônimos *com falha para documentos podem ser registrados se uma política for editada para remover o acesso anônimo. Quando um destinatário autorizado tenta acessar um documento protegido pela política editada, o acesso anônimo ainda é tentado, mas falhará.*

Se uma política permitir o acesso anônimo do usuário, mas o administrador depois desativar o acesso anônimo para a segurança do documento, o acesso anônimo falhará para documentos protegidos com a política e o evento não será registrado.

## Habilitar auditoria de eventos {#enable-event-auditing}

Esses requisitos de configuração devem ser cumpridos para que a auditoria de eventos ocorra:

* O sistema ou o administrador deve ativar o recurso de auditoria do servidor.

   (Consulte [Configuração de auditoria de eventos e configurações](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings)de privacidade.)

* A política usada para proteger o documento deve ter a auditoria ativada. (Consulte [Criar e editar políticas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## Procurar um evento {#search-for-an-event}

Você pode pesquisar a lista de eventos e exibir descrições mais detalhadas sobre os eventos. As descrições detalhadas incluem informações como ID do evento, descrição, endereço IP, organização, usuário afetado, data e hora em que o evento ocorreu, atividades negadas e eventos offline (quando os usuários tentam usar um documento quando não estão conectados à segurança do documento).

Você pode pesquisar eventos na página Eventos usando uma combinação de critérios de pesquisa de eventos e as datas em que os eventos ocorreram. Os eventos que você pode pesquisar dependem da sua função:

**** Usuários: Pode exibir eventos auditados para seus documentos protegidos por política e para quaisquer documentos protegidos que eles recebam e usem. Essas opções de pesquisa estão disponíveis:

**** Eventos relacionados comigo: Os usuários podem encontrar eventos para qualquer documento protegido por política que tenham criado ou recebido. Por exemplo, se um usuário abrir, exibir ou imprimir um documento protegido por outra pessoa, ele verá apenas esses eventos para esse documento.

**** Eventos relacionados aos meus documentos: Os usuários podem encontrar todos os eventos relacionados a seus próprios documentos protegidos por política. Os usuários visualizam os eventos gerados por cada pessoa que manipulou seus documentos.

**** Coordenadores de definição de políticas: Pode exibir eventos auditados, incluindo eventos de documento e política, para documentos protegidos por políticas de seus conjuntos de políticas. Estas opções estão disponíveis:

**** Eventos de documento em que sou um coordenador de conjunto de políticas: Os coordenadores de definição de política que têm a permissão de exibição de evento podem encontrar eventos relacionados a documentos protegidos por políticas de seus conjuntos de políticas.

**** Eventos de política em que sou coordenador de conjunto de políticas: Os coordenadores de definição de política que têm permissão para exibir eventos podem encontrar eventos relacionados a políticas de seus conjuntos de políticas.

**** Administradores: Pode exibir eventos auditados relacionados a todos os documentos protegidos por política e usuários. Os administradores também podem rastrear outros tipos. Além disso, os administradores podem ainda subdividir as pesquisas de eventos de acordo com o tipo de usuário:

**** Usuários conhecidos: Os usuários estão nos diretórios de origem ou registrados como usuários externos.

**** Usuários anônimos: Usuários desconhecidos que acessam um documento protegido por uma política que permite acesso anônimo.

**** Usuários do sistema: Eventos iniciados pelo servidor, como uma sincronização de diretório.

1. Na página de segurança do documento, clique em Eventos.
1. Na lista Localizar, selecione os critérios de pesquisa que deseja usar. Dependendo da sua seleção na lista Localizar, uma segunda lista é exibida, fornecendo critérios de pesquisa adicionais. Se aplicável, na caixa de texto, digite os critérios de pesquisa.

   Para obter mais detalhes sobre os tipos de eventos específicos, consulte Opções [de auditoria de](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options)eventos.

1. Na lista Usuário, selecione o tipo de usuário que executou o evento:

   * Se você selecionar Usuário conhecido, uma segunda caixa de pesquisa será exibida, onde você deverá digitar o nome do usuário ou endereço de email do usuário.
   * Se você não souber esses valores, clique no ícone de pesquisa do Catálogo de endereços para procurar o usuário pelo nome de usuário ou pelo endereço de email.

1. Na lista Data, selecione uma opção de intervalo de datas. Se você selecionar Datas personalizadas, as caixas serão exibidas, onde você digita a data no formato aaaa/mm/dd, ou pode usar o Seletor de datas para especificar o intervalo de datas:

   * Clique no calendário para abrir o Seletor de datas.
   * Use as setas para encontrar um ano e um mês.
   * Clique em um dia do mês no calendário.
   * Clique em OK para fechar o Seletor de datas.

1. Na lista Exibir, selecione o número de resultados de pesquisa a serem exibidos por página.
1. Clique em Localizar.

   Todos os eventos com falha são realçados na lista com um ícone negado.

1. Para exibir detalhes sobre um evento, clique na descrição do evento na lista.

## Classificar a lista de eventos {#sort-the-event-list}

Você pode classificar a lista de eventos por cabeçalho de coluna para localizar eventos mais facilmente. Os ícones de triângulo ao lado do cabeçalho da coluna indicam qual coluna está sendo usada para classificar no momento. Um triângulo apontando para cima indica ordem crescente, enquanto um triângulo apontando para baixo indica ordem decrescente.

1. Clique no cabeçalho da coluna apropriada.
1. Para alterar a ordem de classificação, clique no cabeçalho da coluna novamente.

