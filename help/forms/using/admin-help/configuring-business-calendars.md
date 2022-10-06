---
title: Configurando Calendários Comerciais
seo-title: Configuring Business Calendars
description: Os calendários de negócios definem dias úteis e não úteis para sua organização. Saiba como configurar os calendários de negócios.
seo-description: Business calendars define business and non-business days for your organization. Learn how to configure the business calendars.
uuid: 0ba610b8-72a8-480c-8783-70d98cbe890a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7a85e13d-4800-47c4-812a-5c6e2355298a
exl-id: 4282718a-41f1-411a-9cd7-8c470005107d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 0%

---

# Configurando Calendários Comerciais {#configuring-business-calendars}

*Calendários de negócios* defina dias úteis e não úteis (por exemplo, feriados legais, finais de semana e dias de desligamento da empresa) para sua organização. Ao usar calendários de negócios, AEM formulários ignora dias que não são úteis ao executar determinados cálculos de data. No Workbench, você pode especificar se deseja usar calendários de negócios para eventos associados ao usuário, como lembretes de tarefas, prazos e escalonamentos, ou para ações não associadas aos usuários, como Eventos de Temporizador e o Serviço de Espera.

Por exemplo, um lembrete de tarefa é configurado para ocorrer três dias úteis depois que a tarefa é atribuída a um usuário. A tarefa é atribuída na quinta-feira. No entanto, os três dias seguintes não são dias úteis porque a sexta-feira é um feriado nacional e os dois dias seguintes são dias de fim de semana. O lembrete é enviado para quarta-feira da próxima semana.

>[!NOTE]
>
>Ao calcular datas e horas usando calendários de negócios, AEM formulários usa a data e a hora do servidor em que está em execução e não se ajusta para a diferença entre fusos horários. Por exemplo, se um lembrete de tarefa for agendado para ocorrer às 10:00 em um servidor em execução em Londres, mas o usuário que recebe o lembrete estiver localizado em Nova York, o usuário receberá o lembrete às 5:00, horário local.

## Usar o calendário de negócios padrão {#using-the-default-business-calendar}

AEM formulários fornece um calendário comercial padrão (nomeado como *Calendário incorporado*) que designa sábados e domingos como dias não úteis. Se todos os usuários em sua organização tiverem os mesmos dias que não sejam úteis, você poderá atualizar o calendário comercial padrão para adequá-lo à sua organização. Ao usar somente o calendário de negócios padrão, não é necessário ativar calendários de negócios no Gerenciamento de usuários ou fornecer qualquer mapeamento. Quando nenhum outro calendário de negócios é definido, AEM formulários usa o calendário de negócios padrão.

## Configurando vários calendários de negócios {#setting-up-multiple-business-calendars}

Se alguns dos usuários em sua organização tiverem dias diferentes que não sejam de negócios, você poderá definir vários calendários de negócios e configurar mapeamentos que permitam uma resolução de tempo de execução de um calendário de negócios para um usuário.

### Definir vários calendários de negócios {#define-multiple-business-calendars}

1. Decida como você associará o calendário de negócios apropriado a um usuário. Há duas maneiras de associar um calendário de negócios a um usuário:

   **Associação de grupo:** Você pode atribuir um calendário comercial a um usuário com base na associação de grupo do usuário. Nesse caso, cada usuário do grupo usará o mesmo calendário comercial.

   Se um usuário for membro de dois grupos diferentes e esses grupos forem mapeados para dois calendários comerciais diferentes, AEM formulários usarão o primeiro calendário encontrado em seus resultados de pesquisa. Nesse caso, considere usar chaves de calendário de negócios para associar usuários a calendários de negócios.

   **Chaves do calendário de negócios:** Você pode atribuir um calendário de negócios a um usuário com base em uma chave de calendário de negócios, que é uma configuração especificada no Gerenciamento de usuários. Em seguida, você mapeia a chave do calendário comercial para um calendário comercial no fluxo de trabalho de formulários.

   A forma como você atribui chaves do calendário de negócios aos usuários depende se você está usando um domínio corporativo, local ou híbrido. Para obter detalhes sobre como configurar domínios, consulte [Adição de domínios](/help/forms/using/admin-help/adding-domains.md#adding-domains).

   Se você estiver usando um domínio local ou híbrido, as informações sobre os usuários serão armazenadas somente no banco de dados do Gerenciamento de usuários . Para definir a chave do calendário de negócios para esses usuários, insira uma string no campo Chave do calendário de negócios ao adicionar ou editar um usuário no Gerenciamento de usuários. (Consulte [Adicionar e configurar usuários](/help/forms/using/admin-help/adding-configuring-users.md#adding-and-configuring-users).) Em seguida, você mapeia as chaves do calendário de negócios (as cadeias de caracteres) em calendários de negócios no fluxo de trabalho de formulários. (Consulte [Mapeamento de usuários e grupos para um calendário de negócios](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

   Se você estiver usando um domínio corporativo, as informações sobre os usuários ficarão em um sistema de armazenamento de terceiros, como um diretório LDAP, que é sincronizado pelo Gerenciamento de usuários com o banco de dados do Gerenciamento de usuários. Isso permite mapear uma chave do calendário de negócios para um campo no diretório LDAP. Por exemplo, se cada registro de usuário em seu diretório contiver um campo &quot;país&quot; e você quiser atribuir calendários de negócios com base no país onde o usuário está localizado, especifique o nome do campo &quot;país&quot; no campo Chave do calendário de negócios ao especificar as configurações de usuário para o diretório. (Consulte [Configuração de diretórios](/help/forms/using/admin-help/configuring-directories.md#configuring-directories).) Em seguida, você pode mapear as chaves do calendário de negócios (os valores definidos para o campo &quot;país&quot; no diretório LDAP) para calendários de negócios no fluxo de trabalho de formulários. (Consulte [Mapeamento de usuários e grupos para um calendário de negócios](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)

1. No fluxo de trabalho de formulários, defina um calendário para cada conjunto de usuários que compartilham os mesmos dias úteis. (Consulte [Criar ou atualizar um calendário de negócios](configuring-business-calendars.md#create-or-update-a-business-calendar).)
1. No fluxo de trabalho de formulários, mapeie as chaves do calendário comercial ou as associações de grupo para cada calendário. (Consulte [Mapeamento de usuários e grupos para um calendário de negócios](configuring-business-calendars.md#mapping-users-and-groups-to-a-business-calendar).)
1. No Workbench, o desenvolvedor do processo escolhe se deseja usar calendários de negócios para lembretes, prazos e escalonamentos. (Consulte [Ajuda do Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   Se o desenvolvedor do processo optar por usar calendários de negócios, AEM formulários selecionará dinamicamente o calendário de negócios apropriado com base na configuração Gerenciamento de usuários e nos mapeamentos do calendário de negócios definidos no Console de administração, ou, se não houver mapeamentos, usará o calendário padrão.

   Se o desenvolvedor do processo não usar calendários de negócios, o cálculo de data do evento será tratado todos os dias como um dia útil. Por exemplo, um prazo de tarefa é configurado para ocorrer três dias após a tarefa ser atribuída a um usuário. A tarefa é atribuída na quinta-feira. O prazo da tarefa ocorre no domingo, mesmo que seja um fim de semana.

## Criar ou atualizar um calendário de negócios {#create-or-update-a-business-calendar}

Se sua organização contém conjuntos diferentes de usuários que têm dias diferentes do dia útil, você pode definir vários calendários de negócios. Você também pode alterar calendários existentes, incluindo o calendário interno padrão fornecido com AEM formulários.

>[!NOTE]
>
>Se você não criar um novo calendário de negócios, então o calendário padrão será usado.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Calendários comerciais.
1. Para adicionar um novo calendário comercial, clique em ![bus_cal_plus](assets/bus_cal_plus.png). O texto *Novo calendário* é exibido na lista suspensa. Selecione o texto e digite outro nome para o calendário.

   Para editar um calendário empresarial existente, selecione-o na lista suspensa.

1. Em Dias não úteis padrão, selecione todos os dias não úteis semanais, como fins de semana.
1. [Opcional] Selecione Usar Horário Comercial e especifique os horários de início e término dos dias úteis.

   Se você selecionar esta opção, um evento que ocorre antes do intervalo de tempo especificado é movido para o início do intervalo de tempo e um evento que ocorre após o intervalo de tempo é movido para a hora de início do próximo dia útil.

   Por exemplo, considere uma situação em que um usuário recebe uma tarefa às 2:00 em uma terça-feira, e o lembrete dessa tarefa é definido para dois dias úteis. Sem horário comercial, o lembrete ocorreria às 2:00 da manhã de quinta-feira. Se o horário comercial estiver definido como das 8h às 17h, o lembrete será enviado para as 8h da quinta-feira. Sem horário comercial, se um evento de lembrete fosse criado às 18h da terça-feira, o lembrete ocorreria após o horário comercial da quinta-feira. Com o horário comercial definido como das 8h às 17h, o lembrete ocorreria às 8h da sexta-feira.

1. No calendário, à esquerda, clique duas vezes em quaisquer outros dias que não sejam úteis, como feriados. Não é possível selecionar dias no passado. Os dias que não são úteis selecionados aparecem em uma lista à direita, com a data aparecendo duas vezes em uma linha. Selecione a data à esquerda para digitar o nome ou a descrição do dia não útil.

   Para remover um dia que não seja útil da lista, clique em ![bus_cal_trash](assets/bus_cal_trash.png) ao lado do dia.

1. [Opcional] Se este calendário for o calendário padrão, selecione Calendário padrão. O calendário padrão é usado quando não existe outro mapeamento de calendário para eventos associados ao usuário ou nenhum calendário comercial é especificado para o Evento do Temporizador ou o Serviço de Espera. Não é possível excluir o calendário padrão.
1. Quando terminar de definir os dias que não são úteis, selecione Calendário ativado para torná-lo ativo e clique em Salvar.

   Se você estiver atualizando um calendário existente, a nova versão entrará em vigor imediatamente e será usada para todos os cálculos do calendário comercial, incluindo tarefas que já estão em execução.

   >[!NOTE]
   >
   >Se você não ativar o calendário, o calendário padrão será usado.

## Mapeamento de usuários e grupos para um calendário de negócios {#mapping-users-and-groups-to-a-business-calendar}

Há dois métodos que você pode usar para associar um calendário comercial a um usuário. Você pode atribuir calendários de negócios a usuários com base em uma chave de calendário de negócios ou com base no grupo de diretórios ao qual o usuário pertence. Use a guia Mapeamento para especificar o método que AEM formulários usarão e também para mapear as chaves e os grupos do calendário comercial para calendários de negócios. Para obter detalhes sobre como associar chaves de calendário de negócios com usuários, consulte [Configurando vários calendários de negócios](configuring-business-calendars.md#setting-up-multiple-business-calendars).

### Associar calendários de negócios com usuários com base em chaves de calendário de negócios {#associate-business-calendars-with-users-based-on-business-calendar-keys}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários > Calendários comerciais e, em seguida, clique na guia Mapeamento .
1. Na lista Sistema Usará, selecione Resolução de Chave do Calendário Comercial do Gerenciador de Usuários.
1. Selecione Exibir Chave de Calendário Comercial do Gerenciador de Usuários. Uma lista é exibida, contendo um conjunto exclusivo de chaves de calendário de negócios que foram definidas no Gerenciamento de usuários.

   Para domínios locais e híbridos, a lista exibe os valores inseridos no campo Chave do calendário comercial no Gerenciamento de usuários. Para domínios corporativos (LDAP), a lista exibe o conjunto exclusivo retornado do campo LDAP (por exemplo, &quot;país&quot;) que foi configurado nas configurações do domínio LDAP.

   Se o administrador do Gerenciamento de usuários não tiver definido nenhuma chave do calendário comercial, a lista ficará vazia.

1. Para cada item na lista Chave do Calendário Comercial do UM, selecione um Calendário.
1. Clique em Salvar.

### Associar calendários de negócios a usuários e grupos com base em grupos de serviços de diretório {#associate-business-calendars-with-users-and-groups-based-on-directory-service-groups}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários > Calendários comerciais e, em seguida, clique na guia Mapeamento .
1. Na lista Sistema Usará, selecione Grupos Definidos Pelo Servidor De Diretório.
1. Na guia Mapeamento , selecione Exibir grupos de serviço de diretório. Uma lista é exibida, contendo os grupos que foram definidos no Gerenciamento de usuários. (Consulte [Configurações do diretório](/help/forms/using/admin-help/configuring-directories.md#directory-settings).)

   >[!NOTE]
   >
   >No Workbench, se você configurou um serviço de Usuário para usar calendários de negócios e o serviço é atribuído a um grupo, AEM formulários usa os mapeamentos de grupo especificados aqui para resolver o calendário do grupo. AEM formulários sempre usa mapeamentos de grupos para resolver o calendário de grupos, mesmo quando você usa chaves de calendário de negócios para resolver o calendário para usuários. Se nenhum mapeamento de grupo for encontrado, o calendário comercial padrão será usado.

1. Para cada item na lista Grupo de Serviços de Diretório, selecione um Calendário.
1. Clique em Salvar.

## Exportar e importar calendários comerciais {#exporting-and-importing-business-calendars}

AEM formulários permite exportar e importar seus calendários comerciais como arquivos XML. Você pode usar esse recurso para mover calendários de um sistema de preparo para um sistema de produção.

>[!NOTE]
>
>Esse recurso exporta e importa todos os calendários de negócios definidos, incluindo o calendário de negócios padrão fornecido por formulários AEM. Um calendário comercial importado com o mesmo nome de um calendário existente substituirá o calendário existente.

### Exportar calendários de negócios {#export-business-calendars}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários > Calendários comerciais.
1. Clique em Exportar e salve o arquivo XML.

### Importar calendários de negócios {#import-business-calendars}

1. No console de administração, clique em Serviços > fluxo de trabalho de formulários > Calendários comerciais.
1. Clique em Importar.
1. Selecione o arquivo XML que contém os calendários de negócios exportados e clique em Abrir.

## Excluir um calendário de negócios {#delete-a-business-calendar}

Você pode remover os calendários de negócios que sua organização não requer mais. Se você excluir um calendário comercial que ainda esteja mapeado para usuários e grupos, o calendário padrão será usado.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Calendários comerciais.
1. Selecione o calendário.
1. Clique em Excluir.
