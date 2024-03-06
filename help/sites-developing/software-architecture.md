---
title: Arquitetura de software
description: Conheça algumas práticas recomendadas para a arquitetura do seu software para Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: cd4f3b4c-5488-4ca7-9c1e-b4c819fda8e8
source-git-commit: 0aa929021aa724e4ec18d49fea26f8c0b0538bdc
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Arquitetura de software{#software-architecture}

## Projeto para atualizações {#design-for-upgrades}

Ao estender comportamentos prontos para uso, é importante manter as atualizações em mente. Sempre aplique personalizações no diretório /apps e sobreponha a parte superior dos nós correspondentes no diretório /libs ou use sling:resourceSuperType para estender o comportamento pronto para uso. Embora algumas modificações possam ser necessárias para suportar uma nova versão do AEM, a nova versão não deve substituir suas personalizações se essa prática for seguida.

### Reutilizar modelo e componentes quando possível {#reuse-template-and-components-when-possible}

Isso permite que o site mantenha uma aparência mais consistente e simplifique a manutenção do código. Quando um novo modelo for necessário, estenda de um modelo base compartilhado para que os requisitos globais, como a inclusão da clientlib, possam ser codificados em um local. Quando um novo componente for necessário, procure oportunidades para estender de um componente existente.

### Designs de modelo de design {#design-template-designs}

Ao definir quais componentes podem ser incluídos em cada parsys na página, a consistência da aparência do site pode ser controlada. Restringindo o acesso ao design nas páginas, os &quot;superautores&quot; podem modificar os componentes permitidos por página sem a intervenção do desenvolvedor e, ao mesmo tempo, garantindo que os outros autores sigam os padrões corporativos.

### Desenvolver uma arquitetura SÓLIDA {#develop-a-solid-architecture}

SOLID é um acrônimo que descreve cinco princípios arquitetônicos que devem ser seguidos:

* **S** Princípio da responsabilidade única - cada módulo, classe, método e assim por diante devem ter apenas uma responsabilidade.
* **O** Princípio de Abertura/Fechamento - os módulos devem ser abertos para extensão e fechados para modificação.
* **L** Princípio de substituição iskov - os tipos devem ser substituíveis por seus subtipos.
* **I** Princípio de segmentação de interface - nenhum cliente deve ser forçado a depender de métodos que não usa.
* **D** Princípio da inversão de dependência - os módulos de alto nível não devem depender dos módulos de baixo nível. Ambos devem depender de abstrações. As abstrações não devem depender de detalhes. Os detalhes devem depender de abstrações.

O esforço para cumprir esses cinco princípios deve resultar em um sistema que tenha uma separação estrita de preocupações.

>[!TIP]
>
>SOLID é um conceito comumente usado em programação orientada a objetos e cada elemento é amplamente discutido na literatura da indústria.
>
>Essas informações são apenas um breve resumo apresentado para fins de conscientização e você é incentivado a se familiarizar com esses conceitos com mais profundidade.

### Siga o princípio de robustez {#follow-the-robustness-principle}

O Princípio de Robustez afirma que você deve ser conservador no que você envia, mas ser liberal no que você aceita. Em outras palavras, ao enviar mensagens para terceiros, você deve estar em total conformidade com as especificações. No entanto, ao receber mensagens de terceiros, você deve aceitar mensagens não conformes, desde que o significado da mensagem seja claro.

### Implementar picos em seus próprios módulos {#implement-spikes-in-their-own-modules}

Picos e código de teste fazem parte de qualquer implementação de software Agile. No entanto, você deve garantir que eles não cheguem à base de código de produção sem o nível apropriado de supervisão. Como resultado, é recomendável que os picos sejam criados em seu próprio módulo.

### Implementar scripts de migração de dados em seu próprio módulo {#implement-data-migration-scripts-in-their-own-module}

Os scripts de migração de dados, enquanto o código de produção, são executados apenas uma vez na primeira inicialização de um site. Portanto, quando o site está ativo, os scripts se tornam códigos inativos. Para garantir que você não crie um código de implementação que dependa dos scripts de migração, eles devem ser implementados em seu próprio módulo. Isso nos permite remover e desativar esse código imediatamente após o lançamento, eliminando o código inativo do sistema.

### Siga as convenções do Maven publicadas em arquivos POM {#follow-published-maven-conventions-in-pom-files}

O Apache publicou convenções de estilo em [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). É melhor seguir essas convenções porque facilita a rápida disponibilização de novos recursos.
