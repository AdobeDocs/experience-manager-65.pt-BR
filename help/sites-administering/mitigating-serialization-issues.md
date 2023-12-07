---
title: Redução de problemas de serialização no AEM
description: Saiba como atenuar problemas de serialização no AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# Redução de problemas de serialização no AEM{#mitigating-serialization-issues-in-aem}

## Visão geral {#overview}

A equipe de AEM da Adobe trabalhou em estreita colaboração com o projeto de código aberto [NotSoSerial](https://github.com/kantega/notsoserial) para ajudar a reduzir as vulnerabilidades descritas em **CVE-2015-7501**. NotSoSerial é licenciado sob o [Licença do Apache 2](https://www.apache.org/licenses/LICENSE-2.0) e inclui o código ASM licenciado sob sua própria licença [Licença do tipo BSD](https://asm.ow2.io/).

O jar do agente incluído neste pacote é a distribuição Adobe modificada de NotSoSerial.

NotSoSerial é uma solução de nível Java™ para um problema de nível Java™ e não é específico do AEM. Ele adiciona uma verificação de comprovação a uma tentativa de desserializar um objeto. Essa verificação testa um nome de classe em relação a uma inclui na lista de permissões de estilo de firewall, ou inclui na lista de bloqueios, ou ambos. Devido ao número limitado de classes no incluo na lista de bloqueios padrão, é improvável que esse teste afete seus sistemas ou códigos.

Por padrão, o agente executa uma verificação de inclui na lista de bloqueios em relação às classes vulneráveis conhecidas no momento. Essa inclui na lista de bloqueios destina-se a protegê-lo da lista atual de explorações que usam esse tipo de vulnerabilidade.

A inclui na lista de bloqueios e a inclui na lista de permissões podem ser configuradas seguindo as instruções em [Configurar o agente](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) seção deste artigo.

O agente deve ajudar a reduzir as classes vulneráveis conhecidas mais recentes. Se o seu projeto estiver desserializando dados não confiáveis, ele ainda poderá estar vulnerável a ataques de negação de serviço, ataques de memória insuficiente e explorações desconhecidas de desserialização futuras.

O Adobe oferece suporte oficial ao Java™ 6, 7 e 8. No entanto, o Adobe entende que o NotSoSerial também é compatível com o Java™ 5.

## Instalar o agente {#installing-the-agent}

>[!NOTE]
>
>Se você tiver instalado anteriormente o hotfix de serialização para AEM 6.1, remova os comandos agent start da sua linha de execução Java™.

1. Instale o **com.adobe.cq.cq-serialization-tester** pacote.

1. Acesse o Console da Web do pacote em `https://server:port/system/console/bundles`
1. Procure o pacote de serialização e inicie-o. Isso faz com que o carregue automaticamente o agente NotSoSerial.

## Instalando o Agente nos Servidores de Aplicações {#installing-the-agent-on-application-servers}

O agente NotSoSerial não está incluído na distribuição padrão do AEM para servidores de aplicativos. No entanto, você pode extraí-lo da distribuição AEM jar e usá-lo com a configuração do servidor de aplicativos:

1. Primeiro, baixe o arquivo AEM quickstart e extraia-o:

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Vá para o local do quickstart AEM recém-descompactado e copie o `crx-quickstart/opt/notsoserial/` pasta para a `crx-quickstart` pasta da instalação do servidor de aplicativos AEM.

1. Alterar a propriedade do `/opt` para o usuário que está executando o servidor:

   ```shell
   chown -R opt <user running the server>
   ```

1. Configure e verifique se o agente foi ativado corretamente, conforme mostrado nas seções a seguir deste artigo.

## Configurar o agente {#configuring-the-agent}

A configuração padrão é adequada para a maioria das instalações. Essa configuração inclui uma incluir na lista de bloqueios inclui na lista de permissões de classes vulneráveis de execução remota conhecida e um grupo de pacotes de em que a desserialização de dados confiáveis é segura.

A configuração do firewall é dinâmica e pode ser alterada a qualquer momento por:

1. Acessando o console da Web em `https://server:port/system/console/configMgr`
1. Pesquisando e clicando em **Configuração do firewall de desserialização.**

   >[!NOTE]
   >
   Você também pode acessar a página de configuração diretamente acessando o URL em:
   >
   * `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`

Essa configuração contém os registros incluir na lista de permissões, incluir na lista de bloqueios e desserializar.

**Permitir listagem**

Na seção lista de permissões, essas listagens são classes ou prefixos de pacote permitidos para desserialização. Se você estiver desserializando suas próprias classes, adicione as classes ou pacotes a este incluo na lista de permissões.

**Listagem de Blocos**

Na seção de listagem de blocos, há classes que nunca têm permissão para desserialização. O conjunto inicial dessas classes é limitado às classes que foram consideradas vulneráveis a ataques de execução remota. A inclui na lista de bloqueios ➡ é aplicada antes de qualquer entrada na lista de permissões.

**Log de Diagnóstico**

Na seção para logs de diagnóstico, você pode escolher várias opções para registrar quando a desserialização estiver ocorrendo. Essas opções só são registradas no primeiro uso e não são registradas novamente em usos subsequentes.

O padrão de **class-name-only** informa as classes que estão sendo desserializadas.

Você também pode definir a variável **pilha completa** opção que registra uma pilha de Java™ da primeira tentativa de desserialização para informar onde a desserialização está ocorrendo. Essa opção é útil para encontrar e remover a desserialização do seu uso.

## Verificando a ativação do agente {#verifying-the-agent-s-activation}

Você pode verificar a configuração do agente de desserialização navegando até o URL em:

* `https://server:port/system/console/healthcheck?tags=deserialization`

Após acessar o URL, uma lista de verificações de integridade relacionadas ao agente é exibida. Você pode determinar se o agente está ativado corretamente, verificando se as verificações de integridade estão sendo bem-sucedidas. Se eles estiverem falhando, você deve carregar o agente manualmente.

Para obter mais informações sobre solução de problemas com o agente, consulte [Tratamento De Erros Com O Carregamento Do Agente Dinâmico](#handling-errors-with-dynamic-agent-loading) abaixo.

>[!NOTE]
>
Se você adicionar `org.apache.commons.collections.functors` ao incluir na lista de permissões, a verificação de integridade sempre falha.

## Manipular erros com o carregamento dinâmico do agente {#handling-errors-with-dynamic-agent-loading}

Se erros forem expostos no registro ou se as etapas de verificação detectarem um problema ao carregar o agente, carregue o agente manualmente. Esse fluxo de trabalho também é recomendado se você usar um JRE (Java™ Runtime Environment) em vez de um JDK (Java™ Development Toolkit), porque as ferramentas para carregamento dinâmico não estão disponíveis.

Para carregar o agente manualmente, faça o seguinte:

1. Edite os parâmetros de inicialização da JVM do jar do CQ, adicionando a seguinte opção:

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   Exige que você use a opção -nofork CQ/AEM também, juntamente com as configurações de memória JVM apropriadas, pois o agente não está ativado em uma JVM bifurcada.

   >[!NOTE]
   >
   A distribuição de Adobe do jar do agente NotSoSerial pode ser encontrada no `crx-quickstart/opt/notsoserial/` pasta da sua instalação do AEM.

1. Interrompa e reinicie a JVM;

1. Verifique a ativação do agente novamente seguindo as etapas descritas acima em [Verificando a ativação do agente](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## Outras considerações {#other-considerations}

Se estiver executando em uma IBM® JVM, reveja a documentação sobre suporte para a API Java™ Attach em [este local](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=documentation-java-attach-api).
