---
title: Configuração de armazenamento em cache para o Forms
description: Saiba como definir configurações de cache e como fazer considerações de cluster para caches.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6b57d00e-5ba0-41ee-8497-49ecfec5b9ed
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1611'
ht-degree: 0%

---

# Configuração de armazenamento em cache para o Forms{#configuring-caching-for-forms}

O serviço Forms pega designs de formulário que foram criados no Designer e os renderiza em vários formatos.

A página Forms no console de administração contém configurações que controlam a forma como o serviço do Forms armazena itens em cache. Você pode ajustar essas configurações para otimizar o desempenho do serviço Forms.

O serviço Forms armazena em cache os seguintes itens:

* **designs de formulário:** O serviço do Forms armazena em cache designs de formulário que ele recupera do repositório ou de fontes HTTP. Esse armazenamento em cache melhora o desempenho porque, para solicitações de renderização subsequentes, o serviço Forms recupera o design do formulário do cache, em vez do repositório.
* **fragmentos e imagens:** O serviço Forms pode armazenar em cache fragmentos e imagens usados em designs de formulário. Quando o serviço do Forms armazena esses objetos em cache, ele melhora o desempenho, pois os fragmentos e as imagens são lidos somente no repositório na primeira solicitação.
* **formulários:** O serviço Forms armazena em cache os formulários que renderiza. Esse tipo de armazenamento em cache melhora o desempenho porque o serviço Forms não precisa resolver e renderizar o mesmo formulário em solicitações subsequentes.

O Forms armazena o cache em dois locais:

* **na memória:** Os itens são armazenados na memória para acesso rápido. O cache de memória tem um tamanho limitado e é excluído quando você reinicia o servidor.
* **no disco:** Os itens são armazenados no sistema de arquivos do servidor. O cache de disco tem uma capacidade maior do que o cache na memória e é retido quando você reinicia o servidor. O local do cache de disco depende do servidor de aplicativos. Para obter informações sobre como alterar a localização do cache de disco, consulte [Configuração de locais para o Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).

## Especificação do modo de cache {#specifying-the-cache-mode}

O Forms oferece suporte a dois modos de armazenamento em cache:

* incondicional
* usando o ponto de verificação do cache

Se você alternar entre os modos de cache, reinicie o serviço Forms para que a alteração tenha efeito. Para reiniciar esse serviço, use o Workbench ou consulte [Iniciar ou parar os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

O tempo do ponto de verificação do cache é redefinido automaticamente quando você alterna entre os modos.

### Uso de cache incondicional {#using-unconditional-caching}

Nesse modo, quando o serviço do Forms recebe uma solicitação, ele valida os recursos (design de formulários e quaisquer ativos relacionados, como fragmentos e imagens) que são necessários. O serviço Forms compara o carimbo de data e hora dos recursos no repositório ao dos recursos no cache. Se o recurso no cache for mais antigo, o serviço Forms o atualizará.

Esse modo de cache garante que os recursos mais recentes sejam usados. No entanto, o desempenho é afetado porque o serviço do Forms valida os itens em cache em relação ao repositório com cada solicitação. Esse modo de cache é adequado para ambientes de desenvolvimento e preparo em que os recursos são atualizados com frequência e o desempenho não é uma preocupação principal.

**Especificar armazenamento em cache incondicional**

1. No console de administração, clique em Serviços > Forms.
1. Em Configurações de controle de cache do Forms, selecione Incondicionalmente e clique em Salvar.

### Usar o ponto de verificação do cache {#use-the-cache-check-point}

Nesse modo, o serviço do Forms só verifica o repositório em busca de versões mais recentes dos recursos quando o carimbo de data e hora do recurso em cache for anterior ao horário do ponto de verificação do cache. O último horário de ponto de verificação do cache é exibido na página do Forms no Console de administração.

Use esse modo de cache em ambientes de produção de alto desempenho, nos quais o desempenho é uma preocupação e as alterações nos recursos não são frequentes. Você pode redefinir o momento do ponto de verificação do cache quando quiser implantar quaisquer alterações feitas nos recursos do repositório.

**Especificar o uso de um ponto de verificação de cache**

1. No Console de Administração, clique em Serviços > Forms.
1. Em Configurações de controle de cache do Forms, selecione Somente se a última validação foi feita antes da hora do ponto de verificação do cache e clique em Salvar.

**Redefinir o ponto de verificação do cache**

1. No console de administração, clique em Serviços > Forms.
1. Em Configurações de controle de cache do Forms, clique em Ponto de verificação de cache.

**Redefinir o conteúdo do cache**

Você pode limpar o conteúdo do cache a qualquer momento. Após uma redefinição de cache, a primeira solicitação para cada formulário é mais lenta porque o serviço do Forms executa uma renderização completa e cria novo conteúdo de cache.

1. No console de administração, clique em Serviços > Forms.
1. Em Configurações de controle de cache do Forms, clique em Redefinir cache.

## Definição das configurações de cache {#configuring-cache-settings}

Você pode especificar as configurações que o Forms usa para armazenamento em cache, o que pode otimizar o desempenho do seu ambiente de formulários AEM.

Para acessar essas configurações, no console de administração, clique em Serviços > Forms.

>[!NOTE]
>
>Os requisitos de disco do cache devem ser iguais ao repositório.

### Especificando configurações globais de cache {#specifying-global-cache-settings}

As configurações no **Configurações de Cache Global** afetam todos os tipos de caches. Se você alterar qualquer uma dessas configurações, reinicie o serviço Forms para que a alteração tenha efeito. Para reiniciar esse serviço, use o Workbench ou consulte [Iniciar ou parar os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

**Tamanho Máximo do Documento de Cache (KB):** O tamanho máximo, em quilobytes, de um design de formulário ou outro recurso que pode ser armazenado em qualquer cache na memória. Essa é uma configuração global que se aplica a todos os caches em memória. Se um recurso for maior que esse valor, ele não será armazenado em cache na memória. O valor padrão é 1024 quilobytes. Essa configuração não afeta o cache de disco.

**Cache de renderização do formulário habilitado:** Por padrão, essa opção é selecionada, o que significa que os formulários renderizados são armazenados em cache para recuperação subsequente. Essa configuração melhora o desempenho porque o serviço Forms só precisa renderizar um formulário específico uma vez e, em seguida, usa a versão em cache. Essa opção funciona com a propriedade de cache do design do formulário. Para obter informações sobre como configurar esse valor no design do formulário, consulte a Ajuda do Designer.

### Armazenamento em cache de designs de formulário {#caching-form-designs}

Quando o serviço do Forms recebe uma solicitação de renderização, ele recupera o design do formulário do repositório e o armazena em cache. Esse armazenamento em cache melhora o desempenho porque, para solicitações de renderização subsequentes, o serviço Forms recupera o design do formulário do cache, em vez do repositório.

O serviço Forms sempre armazena em cache designs de formulário no disco. Se os designs de formulário forem armazenados no servidor, esses arquivos serão considerados cache de disco. O serviço Forms também armazena em cache designs de formulário na memória, de acordo com a configuração no **Cache de Modelos na Memória** área. Se você alterar qualquer uma dessas configurações, reinicie o serviço Forms para que a alteração tenha efeito. Para reiniciar esse serviço, use o Workbench ou consulte [Iniciar ou parar os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

**Tamanho do Cache de Configuração de Modelo:** O número máximo de objetos de configuração de modelo a serem mantidos na memória. O valor padrão é 100. É recomendável definir esse valor como maior ou igual ao valor Tamanho do Cache de Modelo. Essa configuração não afeta o cache de disco.

**Tamanho do Cache de Modelos:** O número máximo de objetos de conteúdo de modelo a serem mantidos na memória. O valor padrão é 100. Essa configuração não afeta o cache de disco.

**Ativado:** Por padrão, essa caixa de seleção está marcada, o que significa que os modelos de formulário são armazenados em cache na memória. Quando essa opção não está selecionada, os modelos de formulário são armazenados em cache somente no disco.

### Armazenamento em cache de formulários renderizados {#caching-rendered-forms}

O serviço do Forms armazena formulários renderizados em cache para que ele não precise resolver e renderizar o mesmo formulário em solicitações subsequentes. Os formulários renderizados são armazenados em cache no disco e na memória.

Essas configurações estão no **Cache de renderização do formulário de memória** área. Se você alterar qualquer uma dessas configurações, reinicie o serviço Forms para que a alteração tenha efeito. Para reiniciar esse serviço, use o Workbench ou consulte [Iniciar ou parar os serviços associados aos módulos de formulários AEM](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obter instruções.

**Tamanho do Cache:** Especifica o número máximo de formulários renderizados que podem residir no cache de memória. O valor padrão é 100. Essa configuração não afeta o cache de disco.

**Ativado:** Por padrão, essa opção é selecionada, o que significa que os formulários renderizados são armazenados em cache na memória. Quando essa opção não está selecionada, os formulários renderizados são armazenados em cache somente no disco.

### Armazenamento em cache de fragmentos e imagens {#caching-fragments-and-images}

O serviço do Forms armazena em cache fragmentos e imagens usadas em designs de formulário no disco. Isso melhora o desempenho porque os fragmentos e as imagens são lidos somente no repositório na primeira solicitação. Em seguida, em solicitações subsequentes, o serviço Forms lê fragmentos e imagens do cache de disco. Os fragmentos e as imagens são armazenados em cache somente no disco, e não na memória.

Você pode usar as configurações a seguir para controlar o armazenamento em cache de fragmentos e imagens no disco. Essas configurações estão no **Configurações do Cache de Recursos de Modelo** área:

**Armazenamento em cache de recursos** Selecione uma das seguintes opções na lista:

**Ativado para fragmentos e imagens:** O serviço do Forms armazena fragmentos e imagens em cache. Esta é a opção padrão.

**Ativado para fragmentos:** O serviço do Forms armazena fragmentos em cache, mas não imagens.

**Desabilitado:** O serviço Forms não armazena fragmentos ou imagens em cache.

**Intervalo de Limpeza (Segundos):** Especifica a frequência com que o serviço Forms remove arquivos de cache inválidos antigos. O serviço Forms não remove arquivos de cache válidos. Se você alterar o intervalo de limpeza, reinicie o serviço Forms para que a alteração tenha efeito. Para reiniciar esse serviço, use o Workbench ou consulte Iniciar ou parar os serviços associados aos módulos de formulários AEM para obter instruções. O valor padrão é de 600 segundos.

## Considerações de cluster para caches {#clustering-considerations-for-caches}

Em um ambiente em cluster, cada nó mantém seu próprio cache de disco e memória. O conteúdo do cache em cada nó depende de quais formulários foram renderizados nesse nó.

O local do cache deve ser idêntico (mesmo disco e caminho) em cada nó do cluster. Não coloque o cache no armazenamento compartilhado.

Se você usar a página Forms no console de administração para alterar as configurações de cache de um determinado nó, as configurações de cache em outros nós serão atualizadas quando uma solicitação for enviada para esse nó. Esse comportamento também se aplica ao botão Redefinir cache. Se você clicar no botão Redefinir cache para um nó, o cache será removido imediatamente desse nó. O cache em outros nós é limpo quando uma solicitação vai para esse nó.
