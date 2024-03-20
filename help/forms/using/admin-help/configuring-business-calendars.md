---
title: Configuração de calendários de negócios
description: Os calendários comerciais definem dias úteis e não úteis para sua organização. Saiba como configurar os calendários comerciais.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 4282718a-41f1-411a-9cd7-8c470005107d
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1889'
ht-degree: 0%

---

# Configuração de calendários de negócios {#configuring-business-calendars}

*Calendários comerciais* defina dias úteis e não-úteis (por exemplo, feriados legais, finais de semana e dias de desligamento da empresa) para sua organização. Ao usar calendários comerciais, os formulários AEM ignoram dias não úteis ao executar determinados cálculos de data. No Workbench, você pode especificar se usará calendários de negócios para eventos associados ao usuário, como lembretes de tarefa, prazos e escalonamentos, ou para ações não associadas a usuários, como Eventos de Timer e o Serviço de Espera.

Por exemplo, um lembrete de tarefa é configurado para ocorrer três dias úteis após a tarefa ser atribuída a um usuário. A tarefa é atribuída na quinta-feira. No entanto, os três dias seguintes não são dias úteis porque a sexta-feira é um feriado nacional e os próximos dois dias são dias de fim de semana. O lembrete é enviado na quarta-feira da semana seguinte.

>[!NOTE]
>
>Ao calcular datas e horas usando calendários comerciais, os formulários AEM usam a data e a hora do servidor em que estão sendo executados e não se ajustam para a diferença entre fusos horários. Por exemplo, se um lembrete de tarefa estiver programado para ocorrer às 10h em um servidor em execução em Londres, mas o usuário que recebe o lembrete estiver em Nova York, o usuário receberá o lembrete às 5h da hora local.

## Uso do calendário comercial padrão {#using-the-default-business-calendar}

Os formulários AEM fornecem um calendário comercial padrão (chamado de *Calendário interno*) que designa sábados e domingos como dias não úteis. Se todos os usuários da sua organização tiverem os mesmos dias não-úteis, você poderá atualizar o calendário padrão de negócios para se adequar à sua organização. Ao usar apenas o calendário de negócios padrão, não é necessário ativar os calendários de negócios no Gerenciamento de Usuários nem fornecer mapeamentos. Quando nenhum outro calendário comercial é definido, os formulários AEM usam o calendário comercial padrão.

## Configuração de vários calendários de negócios {#setting-up-multiple-business-calendars}

Se alguns usuários da organização tiverem dias não úteis diferentes, você poderá definir vários calendários comerciais e configurar mapeamentos que permitam uma resolução em tempo de execução de um calendário comercial para um usuário.

### Definir vários calendários comerciais {#define-multiple-business-calendars}

1. Decida como você associará o calendário de negócios apropriado a um usuário. Há duas maneiras de associar um calendário de negócios a um usuário:

   **Associação de grupo:** Você pode atribuir um calendário comercial a um usuário com base na associação de grupo do usuário. Nesse caso, cada usuário no grupo usará o mesmo calendário comercial.

   Se um usuário for membro de dois grupos diferentes e esses grupos forem mapeados para dois calendários comerciais diferentes, os formulários AEM usarão o primeiro calendário encontrado nos resultados da pesquisa. Nesse caso, considere o uso de chaves de calendário comercial para associar usuários a calendários comerciais.

   **Chaves do calendário comercial:** Você pode atribuir um calendário comercial a um usuário com base em uma chave de calendário comercial, que é uma definição especificada em Gerenciamento de usuários. Em seguida, mapeie a chave do calendário comercial para um calendário comercial no fluxo de trabalho de formulários.

   A forma como você atribui chaves do calendário de negócios aos usuários depende de você estar usando um domínio corporativo, local ou híbrido. Para obter detalhes sobre como configurar domínios, consulte [Adicionar domínios](/help/forms/using/admin-help/adding-domains.md#adding-domains).

   Se você estiver usando um domínio local ou híbrido, as informações sobre os usuários serão armazenadas somente no banco de dados do Gerenciamento de usuários. Para definir a chave do calendário comercial para esses usuários, informe uma string no campo Chave do Calendário Comercial ao adicionar ou editar um usuário no Gerenciamento de Usuários. (Consulte [Adicionar e configurar usuários](/help/forms/using/admin-help/adding-configuring-users.md#adding-and-configuring-users).) Em seguida, mapeie as chaves do calendário comercial (as cadeias de caracteres) para os calendários comerciais no fluxo de trabalho dos formulários. (Consulte [Mapeamento de usuários e grupos a um calendário comercial](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

   Se você estiver usando um domínio enterprise, as informações sobre usuários residirão em um sistema de armazenamento de terceiros, como um diretório LDAP, que o User Management sincroniza com o banco de dados do User Management. Isso permite mapear uma chave de calendário comercial para um campo no diretório LDAP. Por exemplo, se cada registro de usuário no diretório contiver um campo &quot;país&quot; e você quiser atribuir calendários de negócios com base no país onde o usuário está localizado, especifique o nome do campo &quot;país&quot; no campo Chave do Calendário de Negócios ao especificar as configurações de usuário para o diretório. (Consulte [Configurando diretórios](/help/forms/using/admin-help/configuring-directories.md#configuring-directories).) Em seguida, é possível mapear as chaves do calendário comercial (os valores definidos para o campo &quot;país&quot; no diretório LDAP) para calendários comerciais no fluxo de trabalho de formulários. (Consulte [Mapeamento de usuários e grupos a um calendário comercial](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

1. No workflow de formulários, defina um calendário para cada conjunto de usuários que compartilham os mesmos dias não úteis. (Consulte [Criar ou atualizar um calendário comercial](configuring-business-calendars.md#create-or-update-a-business-calendar).)
1. No workflow de formulários, mapeie as chaves do calendário comercial ou as associações de grupo para cada calendário. (Consulte [Mapeamento de usuários e grupos a um calendário comercial](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)
1. No Workbench, o desenvolvedor de processos escolhe se deseja usar calendários de negócios para lembretes, prazos e escalonamentos. (Consulte [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   Se o desenvolvedor de processos optar por usar calendários de negócios, os formulários AEM selecionarão dinamicamente o calendário de negócios apropriado com base na configuração Gerenciamento de usuários e nos mapeamentos do calendário de negócios definidos no Console de administração, ou, se não houver mapeamentos, usarão o calendário padrão.

   Se o desenvolvedor do processo não usar calendários comerciais, o cálculo de data para o evento tratará todos os dias como um dia útil. Por exemplo, um prazo de tarefa é configurado para ocorrer três dias após a tarefa ser atribuída a um usuário. A tarefa é atribuída na quinta-feira. O prazo da tarefa ocorre no domingo, mesmo sendo um fim de semana.

## Criar ou atualizar um calendário comercial {#create-or-update-a-business-calendar}

Se sua organização contiver diferentes conjuntos de usuários com diferentes dias não úteis, você poderá definir vários calendários comerciais. Você também pode alterar calendários existentes, incluindo o calendário interno padrão fornecido com formulários AEM.

>[!NOTE]
>
>Se você não criar um calendário comercial, será usado o calendário padrão.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Calendários de negócios.
1. Para adicionar um novo calendário comercial, clique em ![bus_cal_plus](assets/bus_cal_plus.png). O texto *Novo calendário* é exibida na lista suspensa. Selecione o texto e digite outro nome para o calendário.

   Para editar um calendário comercial existente, selecione-o na lista suspensa.

1. Em Dias não-úteis padrão, selecione quaisquer dias não-úteis semanais, como fins de semana.
1. [Opcional] Selecione Usar horário comercial e especifique as horas de início e término para os dias úteis.

   Se você selecionar essa opção, um evento que ocorre antes do intervalo de tempo especificado será movido para o início do intervalo de tempo, e um evento que ocorre após o intervalo de tempo será movido para a hora inicial do próximo dia útil.

   Por exemplo, considere uma situação em que um usuário recebe uma tarefa às 2h de uma terça-feira e o lembrete dessa tarefa é definido como dois dias úteis. Sem horário comercial, o lembrete ocorreria às 2:00 da manhã da quinta-feira. Se o horário comercial estiver definido como 8h às 17h, o lembrete será encaminhado para 8h na quinta-feira. Sem horário comercial, se um evento de lembrete fosse criado às 18h de terça-feira, o lembrete ocorreria depois do horário comercial de quinta-feira. Com o horário comercial definido para 8:00 às 17:00, o lembrete ocorreria às 8:00 na sexta-feira.

1. No calendário à esquerda, clique duas vezes em qualquer outro dia não útil, como feriados. Não é possível selecionar dias no passado. Os dias não-úteis selecionados são exibidos em uma lista à direita, com a data aparecendo duas vezes em uma linha. Selecione a data à esquerda para digitar o nome ou a descrição do dia não útil.

   Para remover um dia não útil da lista, clique em ![bus_cal_trash](assets/bus_cal_trash.png) ao lado do dia.

1. [Opcional] Se este calendário for o padrão, selecione Calendário padrão. O calendário padrão é usado quando nenhum outro mapeamento de calendário existe para eventos associados ao usuário ou nenhum calendário comercial é especificado para o Evento de Timer ou o Serviço de Espera. Não é possível excluir o calendário padrão.
1. Quando terminar de definir os dias não-úteis, selecione Calendário Ativado para ativá-lo e clique em Salvar.

   Se você estiver atualizando um calendário existente, a nova versão entrará em vigor imediatamente e será usada para todos os cálculos do calendário de negócios, inclusive para tarefas que já estão em execução.

   >[!NOTE]
   >
   >Se você não habilitar o calendário, será usado o calendário padrão.

## Mapeamento de usuários e grupos a um calendário comercial {#mapping-users-and-groups-to-a-business-calendar}

Há dois métodos que podem ser usados para associar um calendário comercial a um usuário. Você pode atribuir calendários de negócios a usuários com base em uma chave de calendário de negócios ou com base no grupo de diretórios ao qual o usuário pertence. Use a guia Mapeamento para especificar o método que os formulários AEM usarão e também para mapear as chaves e grupos do calendário comercial para calendários comerciais. Para obter detalhes sobre como associar chaves de calendário comercial a usuários, consulte [Configuração de vários calendários de negócios](configuring-business-calendars.md#setting-up-multiple-business-calendars).

### Associar calendários comerciais a usuários com base nas chaves do calendário comercial {#associate-business-calendars-with-users-based-on-business-calendar-keys}

1. No console de administração, clique em Serviços > Fluxo de trabalho de formulários > Calendários de negócios e, em seguida, clique na guia Mapeamento.
1. Na lista O Sistema Utilizará, selecione Resolução da Chave do Calendário Comercial do Gerenciador de Usuários.
1. Selecione Exibir Chave do Calendário Comercial do Gerenciador de Usuários. Uma lista é exibida, contendo um conjunto exclusivo de chaves do calendário de negócios que foram definidas no Gerenciamento de usuários.

   Para domínios locais e híbridos, a lista exibe os valores inseridos no campo Chave do calendário de negócios em Gerenciamento de usuários. Para domínios Enterprise (LDAP), a lista exibe o conjunto exclusivo retornado do campo LDAP (por exemplo, &quot;país&quot;) que foi configurado nas configurações de domínio LDAP.

   Se o administrador do Gerenciamento de usuários não tiver definido nenhuma chave de calendário comercial, a lista ficará vazia.

1. Para cada item na lista Chave do Calendário Comercial do UM, selecione um Calendário.
1. Clique em Salvar.

### Associar calendários de negócios a usuários e grupos com base em grupos de serviços de diretório {#associate-business-calendars-with-users-and-groups-based-on-directory-service-groups}

1. No console de administração, clique em Serviços > Fluxo de trabalho de formulários > Calendários de negócios e, em seguida, clique na guia Mapeamento.
1. Na lista O sistema utilizará, selecione Grupos definidos pelo servidor de diretório.
1. Na guia Mapeamento, selecione Exibir Grupos de Serviços de Diretório. Uma lista é exibida, contendo os grupos que foram definidos no Gerenciamento de usuários. (Consulte [Configurações do diretório](/help/forms/using/admin-help/configuring-directories.md#directory-settings).)

   >[!NOTE]
   >
   >No Workbench, se você tiver configurado um serviço de Usuário para usar calendários de negócios e o serviço estiver atribuído a um grupo, os formulários AEM usarão os mapeamentos de grupo especificados aqui para resolver o calendário do grupo. Os formulários AEM sempre usam mapeamentos de grupos para resolver o calendário de grupos, mesmo quando você usa as chaves do calendário comercial para resolver o calendário de usuários. Se nenhum mapeamento de grupo for encontrado, o calendário comercial padrão será usado.

1. Para cada item na lista Grupo de Serviços de Diretório, selecione um Calendário.
1. Clique em Salvar.

## Exportação e importação de calendários de negócios {#exporting-and-importing-business-calendars}

O AEM Forms permite exportar e importar seus calendários de negócios como arquivos XML. Você pode usar esse recurso para mover calendários de um sistema de preparo para um sistema de produção.

>[!NOTE]
>
>Esse recurso exporta e importa todos os calendários comerciais definidos, incluindo o calendário comercial padrão fornecido por formulários AEM. Um calendário comercial importado com o mesmo nome de um calendário existente substitui o calendário existente.

### Exportar calendários de negócios {#export-business-calendars}

1. No console de administração, clique em Serviços > Fluxo de trabalho de formulários > Calendários de negócios.
1. Clique em Exportar e salve o arquivo XML.

### Importar calendários de negócios {#import-business-calendars}

1. No console de administração, clique em Serviços > Fluxo de trabalho de formulários > Calendários de negócios.
1. Clique em Importar.
1. Selecione o arquivo XML que contém os calendários comerciais exportados e clique em Abrir.

## Excluir um calendário comercial {#delete-a-business-calendar}

Você pode remover qualquer calendário de negócios que sua organização não exija mais. Se você excluir um calendário comercial que ainda esteja mapeado a usuários e grupos, o calendário padrão será usado.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Calendários de negócios.
1. Selecione o calendário.
1. Clique em Excluir.
