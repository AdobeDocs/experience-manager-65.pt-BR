---
title: Configuração do cache para Forms
seo-title: Configuração do cache para Forms
description: Saiba como configurar as configurações de cache e como agrupar considerações para caches.
seo-description: Saiba como configurar as configurações de cache e como agrupar considerações para caches.
uuid: 70f36191-4163-410b-991a-e1481488aea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8a07dddf-1281-45ac-a55e-4333b860a261
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 0%

---


# Configuração do cache para Forms{#configuring-caching-for-forms}

O serviço Forms usa designs de formulário criados no Designer e os renderiza em vários formatos.

A página do Forms no console de administração contém configurações que controlam a maneira como o serviço Forms armazena itens em cache. Você pode ajustar essas configurações para otimizar o desempenho do serviço Forms.

O serviço Forms armazena em cache os seguintes itens:

* **designs de formulário:** O serviço Forms armazena em cache os designs de formulário recuperados do repositório ou de fontes HTTP. Esse armazenamento em cache melhora o desempenho, pois para solicitações de renderização subsequentes, o serviço Forms recupera o design de formulário do cache em vez de do repositório.
* **fragmentos e imagens:** O serviço Forms pode armazenar em cache fragmentos e imagens usados em designs de formulário. Quando o serviço Forms armazena esses objetos em cache, ele melhora o desempenho, pois os fragmentos e as imagens são lidos somente do repositório na primeira solicitação.
* **formulários:** o serviço Forms armazena em cache os formulários que renderiza. Esse tipo de armazenamento em cache melhora o desempenho, pois o serviço Forms não precisa resolver e renderizar o mesmo formulário em solicitações subsequentes.

A Forms armazena o cache em dois locais:

* **na memória:** os itens são armazenados na memória para acesso rápido. O cache da memória tem um tamanho limitado e é excluído quando você reiniciar o servidor.
* **no disco:** os itens são armazenados no sistema de arquivos do servidor. O cache de disco tem uma capacidade maior do que o cache na memória e é retido quando você reinicia o servidor. O local do cache de disco depende do servidor de aplicativos. Para obter informações sobre como alterar o local do cache de disco, consulte [Configuração de locais para Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).

## Especificação do modo de cache {#specifying-the-cache-mode}

A Forms suporta dois modos de armazenamento em cache:

* incondicional
* usando o ponto de verificação do cache

Se você alternar entre os modos de cache, reinicie o serviço Forms para que a alteração tenha efeito. Para reiniciar esse serviço, use o Workbench ou consulte [Start ou pare os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

A hora do ponto de verificação do cache é redefinida automaticamente quando você alterna entre os modos.

### Usando o cache incondicional {#using-unconditional-caching}

Nesse modo, quando o serviço Forms recebe uma solicitação, ele valida os recursos (design de formulários e quaisquer ativos relacionados, como fragmentos e imagens) necessários. O serviço Forms compara o carimbo de data e hora dos recursos no repositório ao carimbo de data e hora dos recursos no cache. Se o recurso no cache for mais antigo, o serviço Forms o atualizará.

Esse modo de cache garante que os recursos mais recentes sejam usados. No entanto, o desempenho é afetado porque o serviço Forms valida os itens em cache em relação ao repositório com cada solicitação. Esse modo de cache é adequado para ambientes de desenvolvimento e armazenamento temporário nos quais os recursos são atualizados com frequência e o desempenho não é uma preocupação principal.

**Especificar cache incondicional**

1. No console de administração, clique em Serviços > Forms.
1. Em Configurações de controle de cache da Forms, selecione Incondicionalmente e clique em Salvar.

### Usar o ponto de verificação de cache {#use-the-cache-check-point}

Nesse modo, o serviço Forms verifica apenas as versões mais recentes dos recursos do repositório quando o carimbo de data e hora do recurso em cache é mais antigo do que o tempo do ponto de verificação do cache. A última hora do ponto de verificação do cache é exibida na página do Forms no Console de administração.

Use esse modo de cache em ambientes de produção de alto desempenho onde o desempenho é uma preocupação e as alterações nos recursos são raras. Você pode redefinir o tempo do ponto de verificação do cache quando quiser implantar quaisquer alterações feitas nos recursos do repositório.

**Especificar o uso de um ponto de verificação de cache**

1. No Console de administração, clique em Serviços > Forms.
1. Em Configurações de controle de cache da Forms, selecione Somente se sua última validação foi feita antes do tempo do ponto de verificação da cache e clique em Salvar.

**Redefina o ponto de verificação do cache**

1. No console de administração, clique em Serviços > Forms.
1. Em Configurações de controle de cache da Forms, clique em Ponto de verificação de cache.

**Redefinir o conteúdo do cache**

Você pode limpar o conteúdo do cache a qualquer momento. Após uma redefinição de cache, a primeira solicitação para cada formulário é mais lenta porque o serviço Forms executa uma renderização completa e cria novo conteúdo de cache.

1. No console de administração, clique em Serviços > Forms.
1. Em Configurações de controle de cache da Forms, clique em Redefinir cache.

## Definição das configurações de cache {#configuring-cache-settings}

É possível especificar configurações que a Forms usa para armazenamento em cache, o que pode otimizar o desempenho do ambiente de formulários AEM.

Para acessar essas configurações, no console de administração, clique em Serviços > Forms.

>[!NOTE]
>
>Os requisitos de disco para o cache devem ser iguais ao repositório.

### Especificação de configurações de cache global {#specifying-global-cache-settings}

As configurações na área **Configurações de cache global** afetam todos os tipos de caches. Se você alterar qualquer uma dessas configurações, reinicie o serviço Forms para que a alteração tenha efeito. Para reiniciar esse serviço, use o Workbench ou consulte [Start ou pare os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

**Tamanho máximo do Documento do cache (KB):** O tamanho máximo, em quilobytes, de um design de formulário ou de outro recurso que pode ser armazenado em qualquer cache de memória. Esta é uma configuração global que se aplica a todos os caches de memória. Se um recurso for maior que esse valor, ele não será armazenado em cache na memória. O valor padrão é 1024 kilobytes. Essa configuração não afeta o cache de disco.

**Cache de renderização de formulário ativado:** por padrão, essa opção é selecionada, o que significa que os formulários renderizados são armazenados em cache para recuperação subsequente. Essa configuração melhora o desempenho, pois o serviço Forms só precisa renderizar um formulário específico uma vez e, em seguida, usa a versão em cache. Essa opção funciona com a propriedade de cache do design de formulário. Para obter informações sobre como configurar esse valor no design de formulário, consulte Ajuda do Designer.

### Armazenamento em cache de designs de formulário {#caching-form-designs}

Quando o serviço Forms recebe uma solicitação de renderização, ele recupera o design de formulário do repositório e o armazena em cache. Esse armazenamento em cache melhora o desempenho, pois para solicitações de renderização subsequentes, o serviço Forms recupera o design de formulário do cache em vez de do repositório.

O serviço Forms sempre armazena em cache designs de formulário em disco. Se os designs de formulário forem armazenados no servidor, esses arquivos serão considerados cache de disco. O serviço Forms também armazena em cache designs de formulário na memória, de acordo com a configuração na área **No Cache de Modelo de Memória**. Se você alterar qualquer uma dessas configurações, reinicie o serviço Forms para que a alteração tenha efeito. Para reiniciar esse serviço, use o Workbench ou consulte [Start ou pare os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

**Tamanho do Cache de Configuração do Modelo:** O número máximo de objetos de configuração do modelo a serem mantidos na memória. O valor padrão é 100. É recomendável definir esse valor maior ou igual ao valor Tamanho do Cache de Modelo. Essa configuração não afeta o cache de disco.

**Tamanho do Cache do Modelo:** O número máximo de objetos de conteúdo do modelo a serem mantidos na memória. O valor padrão é 100. Essa configuração não afeta o cache de disco.

**Ativado:** por padrão, essa caixa de seleção é selecionada, o que significa que os modelos de formulário são armazenados em cache na memória. Quando essa opção não está selecionada, os modelos de formulário são armazenados em cache somente em disco.

### Armazenamento de formulários renderizados em cache {#caching-rendered-forms}

O serviço Forms armazena formulários renderizados em cache para que não seja necessário resolver e renderizar o mesmo formulário em solicitações subsequentes. Os formulários renderizados são armazenados em cache tanto no disco quanto na memória.

Essas configurações estão localizadas na área **No Memory Form Rendering Cache**. Se você alterar qualquer uma dessas configurações, reinicie o serviço Forms para que a alteração tenha efeito. Para reiniciar esse serviço, use o Workbench ou consulte [Start ou pare os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

**Tamanho do cache:** especifica o número máximo de formulários renderizados que podem residir no cache da memória. O valor padrão é 100. Essa configuração não afeta o cache de disco.

**Ativado:** por padrão, essa opção é selecionada, o que significa que os formulários renderizados são armazenados em cache na memória. Quando essa opção não está selecionada, os formulários renderizados são armazenados em cache somente em disco.

### Armazenamento em cache de fragmentos e imagens {#caching-fragments-and-images}

O serviço Forms armazena em cache fragmentos e imagens usados em designs de formulário em disco. Isso melhora o desempenho, pois os fragmentos e imagens são lidos somente do repositório na primeira solicitação. Em seguida, nas solicitações subsequentes, o serviço Forms lê fragmentos e imagens do cache de disco. Fragmentos e imagens são armazenados em cache apenas em disco, e não na memória.

Você pode usar as seguintes configurações para controlar o armazenamento em cache de fragmentos e imagens em disco. Essas configurações estão localizadas na área **Configurações do Cache de Recursos de Modelo**:

**Cache** de recursosSelecione uma das seguintes opções da lista:

**Ativado para fragmentos e imagens:** o serviço Forms armazena em cache fragmentos e imagens. Esta é a opção padrão.

**Ativado para fragmentos:** o serviço Forms armazena em cache fragmentos, mas não imagens.

**Desativado:** o serviço Forms não armazena em cache fragmentos ou imagens.

**Intervalo de limpeza (segundos):** especifica a frequência com que o serviço Forms remove arquivos de cache antigos inválidos. O serviço Forms não remove arquivos de cache válidos. Se você alterar o intervalo de limpeza, reinicie o serviço Forms para que a alteração tenha efeito. Para reiniciar esse serviço, use o Workbench ou consulte Start ou pare os serviços associados aos módulos de formulários AEM para obter instruções. O valor padrão é 600 segundos.

## Considerações de cluster para caches {#clustering-considerations-for-caches}

Em um ambiente clusterizado, cada nó mantém seu próprio cache na memória e no disco. O conteúdo do cache em cada nó depende de quais formulários foram renderizados nesse nó.

O local do cache deve ser idêntico (mesmo disco e caminho) em cada nó do cluster. Não coloque o cache no armazenamento compartilhado.

Se você usar a página do Forms no console de administração para alterar as configurações de cache de um nó específico, as configurações de cache em outros nós serão atualizadas quando uma solicitação for para esse nó. Esse comportamento também se aplica ao botão Redefinir cache. Se você clicar no botão Redefinir cache para um nó, o cache será removido imediatamente desse nó. O cache em outros nós é limpo quando uma solicitação vai para esse nó.
