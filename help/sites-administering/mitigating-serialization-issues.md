---
title: Atenuando problemas de serialização no AEM
seo-title: Mitigating serialization issues in AEM
description: Saiba como atenuar problemas de serialização no AEM.
seo-description: Learn how to mitigate serialization issues in AEM.
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
exl-id: 01e9ab67-15e2-4bc4-9b8f-0c84bcd56862
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# Atenuando problemas de serialização no AEM{#mitigating-serialization-issues-in-aem}

## Visão geral {#overview}

A equipe de AEM do Adobe tem trabalhado em estreita colaboração com o projeto de código aberto [NotSoSerial](https://github.com/kantega/notsoserial) para ajudar a mitigar as vulnerabilidades descritas em **CVE-2015-7501**. O NotSoSerial está licenciado sob o [Licença Apache 2](https://www.apache.org/licenses/LICENSE-2.0) e inclui o código ASM licenciado sob sua própria licença [Licença tipo BSD](https://asm.ow2.org/license.html).

O agente incluído com este pacote é a distribuição do jar modificado do Adobe de NotSoSerial.

NotSoSerial é uma solução de nível Java para um problema de nível Java e não é AEM específico. Ele adiciona uma verificação de comprovação a uma tentativa de desserializar um objeto. Essa verificação testará um nome de classe em relação a uma lista de permissões e/ou lista de bloqueios no estilo firewall. Devido ao número limitado de classes na lista de bloqueios padrão, é improvável que isso afete seus sistemas ou códigos.

Por padrão, o agente executará uma verificação de lista de bloqueios em relação às classes vulneráveis conhecidas atuais. Essa lista de bloqueios tem como objetivo protegê-lo da lista atual de explorações que usam esse tipo de vulnerabilidade.

A lista de bloqueios e a lista de permissões podem ser configuradas seguindo as instruções em [Configurar o agente](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) seção deste artigo.

O agente tem como objetivo ajudar a mitigar as classes vulneráveis mais recentes conhecidas. Se seu projeto estiver desserializando dados não confiáveis, eles ainda poderão estar vulneráveis a ataques de negação de serviço, ataques de falta de memória e explorações desconhecidas de desserialização futuras.

O Adobe suporta oficialmente o Java 6, 7 e 8, no entanto, nossa compreensão é que o NotSoSerial também suporta o Java 5.

## Instalar o agente {#installing-the-agent}

>[!NOTE]
>
>Se você tiver instalado anteriormente o hotfix de serialização para AEM 6.1, remova os comandos de início do agente da linha de execução java.

1. Instale o **com.adobe.cq.cq-serialization-tester** pacote.

1. Vá para o Console da Web do Pacote em `https://server:port/system/console/bundles`
1. Procure o pacote de serialização e inicie-o. Isso deve carregar dinamicamente o agente NotSoSerial.

## Instalar o agente nos servidores de aplicativos {#installing-the-agent-on-application-servers}

O agente NotSoSerial não está incluído na distribuição padrão de AEM para servidores de aplicativos. No entanto, você pode extraí-lo da distribuição AEM jar e usá-lo com a configuração do servidor de aplicativos:

1. Primeiro, baixe o arquivo AEM quickstart e extraia-o:

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Vá para o local da inicialização rápida recém-descompactada AEM e copie a variável `crx-quickstart/opt/notsoserial/` para `crx-quickstart` pasta da instalação do servidor de aplicativos AEM.

1. Alterar a propriedade de `/opt` para o usuário que está executando o servidor:

   ```shell
   chown -R opt <user running the server>
   ```

1. Configure e verifique se o agente foi ativado corretamente, conforme mostrado nas seções a seguir deste artigo.

## Configurar o agente {#configuring-the-agent}

A configuração padrão é adequada para a maioria das instalações. Isso inclui uma lista de bloqueios de classes vulneráveis de execução remota conhecidas e uma lista de permissões de pacotes em que a desserialização de dados confiáveis deve ser relativamente segura.

A configuração do firewall é dinâmica e pode ser alterada a qualquer momento ao:

1. Ir para o Console da Web em `https://server:port/system/console/configMgr`
1. Como pesquisar e clicar em **Configuração do firewall de desserialização.**

   >[!NOTE]
   >
   >Você também pode acessar a página de configuração diretamente acessando o URL em:
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


Essa configuração contém o registro de lista de permissões, lista de bloqueios e desserialização.

**Permitir listagem**

Na seção de lista de permissões, essas são classes ou prefixos de pacote que serão permitidos para desserialização. É importante estar ciente de que, se você estiver desserializando classes próprias, precisará adicionar as classes ou pacotes a essa lista de permissões.

**Lista de bloqueios**

Na seção de listagem de blocos, há classes que nunca são permitidas para desserialização. O conjunto inicial dessas classes é limitado a classes que foram consideradas vulneráveis a ataques de execução remota. A lista de bloqueios é aplicada antes de qualquer entrada listada de permissão.

**Registro de diagnóstico**

Na seção para registro em log de diagnóstico, você pode escolher várias opções para registrar quando a desserialização estiver ocorrendo. Eles só estão conectados na primeira utilização e não são conectados novamente nos usos subsequentes.

O padrão de **class-name-only** informará sobre as classes que estão sendo desserializadas.

Também é possível definir a variável **pilha completa** que registrará uma pilha java da primeira tentativa de desserialização para informá-lo onde sua desserialização está acontecendo. Isso pode ser útil para localizar e remover a desserialização de seu uso.

## Verificando a ativação do agente {#verifying-the-agent-s-activation}

Você pode verificar a configuração do agente de desserialização navegando até o URL em:

* `https://server:port/system/console/healthcheck?tags=deserialization`

Depois de acessar o URL, uma lista de verificações de integridade relacionadas ao agente será exibida. Você pode determinar se o agente está ativado corretamente verificando se as verificações de integridade estão sendo transmitidas. Se estiverem falhando, talvez seja necessário carregar o agente manualmente.

Para obter mais informações sobre solução de problemas com o agente, consulte [Lidar com erros com o carregamento dinâmico de agentes](#handling-errors-with-dynamic-agent-loading) abaixo.

>[!NOTE]
>
>Se você adicionar `org.apache.commons.collections.functors` para a lista de permissões, a verificação de integridade sempre falhará.

## Lidar com erros com o carregamento do agente dinâmico {#handling-errors-with-dynamic-agent-loading}

Se erros forem expostos no registro ou se as etapas de verificação detectarem um problema ao carregar o agente, talvez seja necessário carregá-lo manualmente. Isso também é recomendado caso você esteja usando um JRE (Java Runtime Environment) em vez de um JDK (Java Development Toolkit), já que as ferramentas para carregamento dinâmico não estão disponíveis.

Para carregar o agente manualmente, siga as instruções abaixo:

1. Modifique os parâmetros de inicialização da JVM do jar CQ, adicionando a seguinte opção:

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Isso requer o uso da opção -nofork CQ/AEM, juntamente com as configurações apropriadas da memória JVM, já que o agente não será ativado em uma JVM bifurcada.

   >[!NOTE]
   >
   >A distribuição de Adobe do jar do agente NotSoSerial pode ser encontrada no `crx-quickstart/opt/notsoserial/` pasta da instalação do AEM.

1. Parar e reiniciar a JVM;

1. Verifique a ativação do agente novamente seguindo as etapas descritas acima em [Verificando a ativação do agente](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation).

## Outras considerações {#other-considerations}

Se você estiver executando uma JVM IBM, revise a documentação sobre suporte para a API de anexação Java em [esta localização](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html).
