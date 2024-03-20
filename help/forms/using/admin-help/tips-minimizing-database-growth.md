---
title: Dicas para minimizar o crescimento do banco de dados
description: Processos de longa duração armazenam dados de processo no banco de dados de formulários AEM. O crescimento do banco de dados de formulários AEM pode ser minimizado usando algumas estratégias fáceis de design de processo e configuração de produto.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f64efb06-815a-4608-ba1c-39e22f344ebb
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Dicas para minimizar o crescimento do banco de dados {#tips-for-minimizing-database-growth}

Processos de longa duração armazenam dados de processo no banco de dados de formulários AEM. O crescimento do banco de dados de formulários AEM pode ser minimizado usando algumas estratégias fáceis de design de processo e configuração de produto.

## Dicas de design de processos {#process-design-tips}

Use processos de vida curta sempre que possível. Processos de vida curta não armazenam dados de processo no banco de dados. A desvantagem de usar processos de vida curta é que seu status e estado não são rastreados no console de administração e não há histórico do processo.

Algumas operações de serviço, como a operação Atribuir tarefa (Serviço do usuário), exigem que sejam usadas em processos de longa duração. Nesse caso, você pode segmentar o processo em vários subprocessos e torná-los de vida curta, quando possível. Se você usar essa estratégia, os subprocessos de vida curta devem lidar com itens de dados grandes, como valores de documento.

Use variáveis com moderação. Ao usar processos de longa duração, para cada instância de processo, o espaço é alocado no banco de dados para cada variável no processo. O uso estratégico de variáveis pode economizar uma quantidade considerável de espaço. Por exemplo, você pode substituir valores variáveis quando os valores antigos não forem mais necessários no processo. E exclua todas as variáveis que você criou e que não está utilizando. Você pode validar o processo para encontrar variáveis não utilizadas.

Use tipos de variáveis simples (por exemplo, string ou int) e evite usar tipos de variáveis complexas quando possível. O espaço do banco de dados é alocado para variáveis mesmo quando elas não contêm um valor. As variáveis complexas normalmente exigem mais espaço do que as simples.

## Dicas de administração de produtos {#product-administration-tips}

Use o armazenamento global de documentos (GDS) com eficiência. O diretório GDS no Forms Server é usado para armazenar, entre outras coisas, arquivos que são passados para serviços que fazem parte de formulários AEM em processos. Para melhorar o desempenho, documentos menores são armazenados na memória e mantidos no banco de dados.

O console de administração expõe a propriedade Default Document Max Inline Size para configurar o tamanho máximo de documentos armazenados na memória e mantidos no banco de dados. (Consulte [Definir configurações gerais de formulários AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).) Se você definir essa propriedade com um valor baixo, a maioria dos documentos será mantida no diretório GDS em vez de no banco de dados. A vantagem é que você pode excluir mais facilmente os arquivos quando eles não são mais necessários quando eles são armazenados no diretório GDS.
