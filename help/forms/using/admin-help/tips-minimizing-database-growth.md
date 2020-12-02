---
title: Dicas para minimizar o crescimento do banco de dados
seo-title: Dicas para minimizar o crescimento do banco de dados
description: Processos de longa duração armazenam dados de processo no banco de dados de formulários AEM. O crescimento do banco de dados de formulários AEM pode ser minimizado usando algumas estratégias fáceis de design de processos e configuração de produtos.
seo-description: Processos de longa duração armazenam dados de processo no banco de dados de formulários AEM. O crescimento do banco de dados de formulários AEM pode ser minimizado usando algumas estratégias fáceis de design de processos e configuração de produtos.
uuid: 13f99d4f-848e-451e-90d9-55e202dc0bdb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89441336-babc-4d1f-9053-d1566cd42d22
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---


# Dicas para minimizar o crescimento do banco de dados {#tips-for-minimizing-database-growth}

Processos de longa duração armazenam dados de processo no banco de dados de formulários AEM. O crescimento do banco de dados de formulários AEM pode ser minimizado usando algumas estratégias fáceis de design de processos e configuração de produtos.

## Processar dicas de design {#process-design-tips}

Use processos de vida curta sempre que possível. Os processos de duração curta não armazenam dados de processo no banco de dados. A desvantagem de usar processos de vida curta é que seu status e estado não são rastreados no console de administração e não há histórico do processo.

Algumas operações de serviço, como a operação Atribuir Tarefa (serviço do usuário), exigem que elas sejam usadas em processos duradouros. Nesse caso, você pode segmentar o processo em vários subprocessos e torná-los de vida curta quando possível. Se você usar essa estratégia, os subprocessos de vida curta deverão lidar com itens de dados grandes, como valores de documento.

Use variáveis com moderação. Ao usar processos de longa duração, para cada instância do processo, o espaço é alocado no banco de dados para cada variável no processo. O uso estratégico de variáveis pode economizar uma quantidade considerável de espaço. Por exemplo, você pode substituir valores de variável quando valores antigos não são mais necessários no processo. E exclua quaisquer variáveis que você tenha criado e não esteja usando. Você pode validar o processo para localizar variáveis não usadas.

Use tipos de variável simples (por exemplo, string ou int) e evite usar tipos de variável complexos quando possível. O espaço do banco de dados é alocado para variáveis mesmo quando não contêm um valor. As variáveis complexas normalmente requerem mais espaço do que as simples.

## Dicas de administração do produto {#product-administration-tips}

Use o armazenamento global de documentos (GDS) com eficiência. O diretório GDS no servidor de formulários é usado para armazenar, entre outras coisas, arquivos enviados para serviços que fazem parte AEM formulários em processos. Para melhorar o desempenho, documentos menores são armazenados na memória e persistem no banco de dados.

o console de administração expõe a propriedade Tamanho máximo em linha do Documento padrão para configurar o tamanho máximo de documentos armazenados na memória e persistentes no banco de dados. (Consulte [Definir configurações gerais de formulários AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).) Se você definir essa propriedade como um valor baixo, a maioria dos documentos será mantida no diretório GDS em vez de no banco de dados. A vantagem é que você pode excluir mais facilmente os arquivos quando eles não são mais necessários quando eles são armazenados no diretório GDS.
