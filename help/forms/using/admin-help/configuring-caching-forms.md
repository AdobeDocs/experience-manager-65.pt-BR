---
title: Configuração do armazenamento em cache para Forms
seo-title: Configuring caching for Forms
description: Saiba como definir configurações de cache e como agrupar considerações para caches.
seo-description: Learn how to configure cache settings and how to cluster considerations for caches.
uuid: 70f36191-4163-410b-991a-e1481488aea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8a07dddf-1281-45ac-a55e-4333b860a261
exl-id: 6b57d00e-5ba0-41ee-8497-49ecfec5b9ed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 0%

---

# Configuração do armazenamento em cache para Forms{#configuring-caching-for-forms}

O serviço Forms usa designs de formulário que foram criados no Designer e os renderiza em vários formatos.

A página Forms no console de administração contém configurações que controlam a maneira como o serviço Forms armazena itens em cache. É possível ajustar essas configurações para otimizar o desempenho do serviço Forms.

O serviço Forms armazena em cache os seguintes itens:

* **designs de formulário:** O serviço Forms armazena em cache designs de formulário que ele recupera do repositório ou de fontes HTTP. Esse armazenamento em cache melhora o desempenho, pois para solicitações de renderização subsequentes, o serviço Forms recupera o design de formulário do cache em vez do repositório.
* **fragmentos e imagens:** O serviço Forms pode armazenar em cache fragmentos e imagens usados em designs de formulário. Quando o serviço Forms armazena esses objetos em cache, ele melhora o desempenho, pois os fragmentos e imagens são lidos somente do repositório na primeira solicitação.
* **formulários:** O serviço Forms armazena em cache os formulários que renderiza. Esse tipo de armazenamento em cache melhora o desempenho, pois o serviço Forms não precisa resolver e renderizar o mesmo formulário em solicitações subsequentes.

O Forms armazena o cache em dois locais:

* **na memória:** Os itens são armazenados na memória para acesso rápido. O cache na memória tem um tamanho limitado e é excluído ao reiniciar o servidor.
* **no disco:** Os itens são armazenados no sistema de arquivos do servidor. O cache de disco tem uma capacidade maior do que o cache na memória e ele é retido quando você reinicia o servidor. A localização do cache de disco depende do servidor de aplicativos. Para obter informações sobre como alterar o local do cache de disco, consulte [Configuração de localizações para Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).

## Especificação do modo de cache {#specifying-the-cache-mode}

O Forms oferece suporte a dois modos de armazenamento em cache:

* incondicional
* uso do ponto de verificação do cache

Se você alternar entre os modos de cache, reinicie o serviço Forms para que a alteração entre em vigor. Para reiniciar este serviço, use o Workbench ou consulte [Iniciar ou parar os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

A hora do ponto de verificação do cache é redefinida automaticamente quando você alternar entre modos.

### Uso do armazenamento em cache incondicional {#using-unconditional-caching}

Nesse modo, quando o serviço Forms recebe uma solicitação, ele valida os recursos (design de formulários e quaisquer ativos relacionados, como fragmentos e imagens) necessários. O serviço Forms compara o carimbo de data e hora dos recursos no repositório ao carimbo de data e hora dos recursos no cache. Se o recurso no cache for mais antigo, o serviço Forms o atualizará.

Esse modo de cache garante que os recursos mais recentes sejam usados. No entanto, o desempenho é afetado porque o serviço Forms valida os itens em cache em relação ao repositório com cada solicitação. Esse modo de cache é adequado para ambientes de desenvolvimento e de preparo, onde os recursos são atualizados com frequência e o desempenho não é uma preocupação principal.

**Especificar cache incondicional**

1. No console de administração, clique em Serviços > Forms.
1. Em Configurações de Controle de Cache do Forms, selecione Incondicionalmente e clique em Salvar.

### Usar o ponto de verificação do cache {#use-the-cache-check-point}

Nesse modo, o serviço Forms só verifica o repositório para versões mais recentes dos recursos quando o carimbo de data e hora do recurso em cache é mais antigo que o tempo do ponto de verificação do cache. O último tempo do ponto de verificação do cache é exibido na página do Forms no Console de Administração.

Use esse modo de cache em ambientes de produção de alto desempenho, onde o desempenho é uma preocupação e as alterações nos recursos são pouco frequentes. Você pode redefinir o tempo do ponto de verificação do cache quando quiser implantar qualquer alteração feita nos recursos do repositório.

**Especificar o uso de um ponto de verificação de cache**

1. No Console de administração, clique em Serviços > Forms.
1. Em Configurações de Controle de Cache do Forms, selecione Somente se a última validação foi feita antes do tempo do ponto de verificação do cache e clique em Salvar.

**Redefinir o ponto de verificação do cache**

1. No console de administração, clique em Serviços > Forms.
1. Em Configurações de Controle de Cache do Forms, clique em Ponto de Verificação de Cache.

**Redefinir o conteúdo do cache**

Você pode limpar o conteúdo do cache a qualquer momento. Após uma redefinição de cache, a primeira solicitação para cada formulário é mais lenta porque o serviço Forms executa uma renderização completa e cria um novo conteúdo de cache.

1. No console de administração, clique em Serviços > Forms.
1. Em Configurações de Controle de Cache do Forms, clique em Redefinir Cache.

## Definição das configurações de cache {#configuring-cache-settings}

Você pode especificar configurações que o Forms usa para armazenamento em cache, o que pode otimizar o desempenho do seu ambiente de formulários AEM.

Para acessar essas configurações, no console de administração, clique em Serviços > Forms.

>[!NOTE]
>
>Os requisitos de disco para o cache devem ser iguais ao repositório.

### Especificação das configurações de cache global {#specifying-global-cache-settings}

As configurações no **Configurações de Cache Global** afetam todos os tipos de caches. Se você alterar qualquer uma dessas configurações, reinicie o serviço Forms para que a alteração entre em vigor. Para reiniciar este serviço, use o Workbench ou consulte [Iniciar ou parar os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

**Tamanho máximo do documento do cache (KB):** O tamanho máximo, em quilobytes, de um design de formulário ou de outro recurso que pode ser armazenado em qualquer cache na memória. Esta é uma configuração global que se aplica a todos os caches em memória. Se um recurso for maior que esse valor, ele não será armazenado em cache na memória. O valor padrão é 1024 kilobytes. Essa configuração não afeta o cache de disco.

**Cache de renderização de formulário ativado:** Por padrão, essa opção é selecionada, o que significa que os formulários renderizados são armazenados em cache para recuperação subsequente. Essa configuração melhora o desempenho, pois o serviço Forms só precisa renderizar um formulário específico uma vez e usa a versão em cache. Essa opção funciona com a propriedade de cache do design de formulário. Para obter informações sobre como configurar esse valor no design de formulário, consulte a Ajuda do Designer.

### Armazenamento de designs de formulário em cache {#caching-form-designs}

Quando o serviço Forms recebe uma solicitação de renderização, ele recupera o design de formulário do repositório e o armazena em cache. Esse armazenamento em cache melhora o desempenho, pois para solicitações de renderização subsequentes, o serviço Forms recupera o design de formulário do cache em vez do repositório.

O serviço Forms sempre armazena em cache designs de formulário em disco. Se os designs de formulário forem armazenados no servidor, esses arquivos serão considerados o cache de disco. O serviço Forms também armazena em cache designs de formulário na memória, de acordo com a configuração no **No Cache do Modelo de Memória** área. Se você alterar qualquer uma dessas configurações, reinicie o serviço Forms para que a alteração entre em vigor. Para reiniciar este serviço, use o Workbench ou consulte [Iniciar ou parar os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

**Tamanho do Cache de Configuração do Modelo:** O número máximo de objetos de configuração de modelo a serem mantidos na memória. O valor padrão é 100. É recomendável definir esse valor maior ou igual ao valor Tamanho do Cache do Modelo. Essa configuração não afeta o cache de disco.

**Tamanho do Cache do Modelo:** O número máximo de objetos de conteúdo de modelo a serem mantidos na memória. O valor padrão é 100. Essa configuração não afeta o cache de disco.

**Ativado:** Por padrão, essa caixa de seleção é selecionada, o que significa que os modelos de formulário são armazenados em cache na memória. Quando essa opção não está selecionada, os modelos de formulário são armazenados em cache somente no disco.

### Armazenamento de formulários renderizados em cache {#caching-rendered-forms}

O serviço Forms armazena formulários renderizados em cache para que não seja necessário resolver e renderizar o mesmo formulário em solicitações subsequentes. Os formulários renderizados são armazenados em cache no disco e na memória.

Essas configurações estão localizadas na variável **Cache de renderização do formulário de memória** área. Se você alterar qualquer uma dessas configurações, reinicie o serviço Forms para que a alteração entre em vigor. Para reiniciar este serviço, use o Workbench ou consulte [Iniciar ou parar os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

**Tamanho do Cache:** Especifica o número máximo de formulários renderizados que podem residir no cache na memória. O valor padrão é 100. Essa configuração não afeta o cache de disco.

**Ativado:** Por padrão, essa opção é selecionada, o que significa que os formulários renderizados são armazenados em cache na memória. Quando essa opção não está selecionada, os formulários renderizados são armazenados em cache somente no disco.

### Armazenamento em cache de fragmentos e imagens {#caching-fragments-and-images}

O serviço Forms armazena em cache fragmentos e imagens usados em designs de formulário no disco. Isso melhora o desempenho, pois os fragmentos e imagens são lidos somente do repositório na primeira solicitação. Em seguida, nas solicitações subsequentes, o serviço Forms lê fragmentos e imagens do cache de disco. Fragmentos e imagens são armazenados em cache somente em disco, e não na memória.

Você pode usar as seguintes configurações para controlar o armazenamento em cache de fragmentos e imagens no disco. Essas configurações estão localizadas na variável **Configurações do Cache de Recursos do Modelo** Área:

**Cache de recursos** Selecione uma das seguintes opções na lista:

**Ativado para fragmentos e imagens:** O serviço Forms armazena em cache fragmentos e imagens. Esta é a opção padrão.

**Ativado para fragmentos:** O serviço Forms armazena em cache fragmentos, mas não imagens.

**Desativado:** O serviço Forms não armazena fragmentos ou imagens em cache.

**Intervalo de Limpeza (Segundos):** Especifica a frequência com que o serviço Forms remove arquivos de cache inválidos antigos. O serviço Forms não remove arquivos de cache válidos. Se você alterar o intervalo de limpeza, reinicie o serviço Forms para que a alteração entre em vigor. Para reiniciar esse serviço, use o Workbench ou consulte Iniciar ou parar os serviços associados aos módulos de formulários AEM para obter instruções. O valor padrão é de 600 segundos.

## Considerações de cluster para caches {#clustering-considerations-for-caches}

Em um ambiente em cluster, cada nó mantém seu próprio cache na memória e no disco. O conteúdo do cache em cada nó depende de quais formulários foram renderizados nesse nó.

O local do cache deve ser idêntico (mesmo disco e caminho) em cada nó do cluster. Não coloque o cache no armazenamento compartilhado.

Se você usar a página do Forms no console de administração para alterar as configurações de cache de um determinado nó, as configurações de cache em outros nós serão atualizadas quando uma solicitação for para esse nó. Esse comportamento também se aplica ao botão Redefinir Cache. Se você clicar no botão Redefinir cache de um nó, o cache será imediatamente removido desse nó. O cache em outros nós é limpo quando uma solicitação vai para esse nó.
