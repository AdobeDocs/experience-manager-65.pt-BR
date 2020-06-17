---
title: Como mitigar problemas de serialização no AEM
seo-title: Como mitigar problemas de serialização no AEM
description: Saiba como atenuar problemas de serialização no AEM.
seo-description: Saiba como atenuar problemas de serialização no AEM.
uuid: c3989dc6-c728-40fd-bc47-f8427ed71a49
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f3781d9a-421a-446e-8b49-40744b9ef58e
translation-type: tm+mt
source-git-commit: 3cbbad3ce9d93a353f48fc3206df989a8bf1991a
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# Como mitigar problemas de serialização no AEM{#mitigating-serialization-issues-in-aem}

## Visão geral {#overview}

A equipe do AEM na Adobe tem trabalhado em conjunto com o projeto de código aberto [NotSoSerial](https://github.com/kantega/notsoserial) para ajudar a atenuar as vulnerabilidades descritas em **CVE-2015-7501**. O NotSoSerial está licenciado sob a licença [do](https://www.apache.org/licenses/LICENSE-2.0) Apache 2 e inclui o código ASM licenciado sob sua própria licença [semelhante a](https://asm.ow2.org/license.html)BSD.

O jar do agente incluído neste pacote é a distribuição modificada pela Adobe de NotSoSerial.

NotSoSerial é uma solução de nível Java para um problema de nível Java e não é específica do AEM. Ela adiciona uma verificação de comprovação a uma tentativa de desserializar um objeto. Essa verificação testará um nome de classe em relação a uma lista de permissão do estilo firewall e/ou lista de blocos. Devido ao número limitado de classes na lista de blocos padrão, é improvável que isso tenha um impacto em seus sistemas ou códigos.

Por padrão, o agente fará uma verificação de lista de blocos em relação às classes vulneráveis conhecidas atuais. Essa lista de blocos tem o objetivo de protegê-lo da lista atual de explorações que usam esse tipo de vulnerabilidade.

A lista de blocos e a lista de permissões podem ser configuradas seguindo as instruções na seção [Configuração do agente](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent) deste artigo.

O agente deve ajudar a atenuar as classes vulneráveis mais recentes conhecidas. Se o seu projeto estiver desserializando dados não confiáveis, ele ainda poderá estar vulnerável a ataques de negação de serviço, ataques de memória esgotados e explorações de desserialização futuras desconhecidas.

A Adobe oferece suporte oficial ao Java 6, 7 e 8, no entanto nossa compreensão é que o NotSoSerial também oferece suporte ao Java 5.

## Instalação do agente {#installing-the-agent}

>[!NOTE]
>
>Se você instalou anteriormente a correção de serialização para o AEM 6.1, remova os comandos do start agente da linha de execução java.

1. Instale o pacote **com.adobe.cq.cq-serialization-tester** .

1. Vá para o console Web do pacote em `https://server:port/system/console/bundles`
1. Procure o pacote de serialização e start-o. Isso deve carregar automaticamente dinamicamente o agente NotSoSerial.

## Instalação do agente em servidores de aplicativos {#installing-the-agent-on-application-servers}

O agente NotSoSerial não está incluído na distribuição padrão do AEM para servidores de aplicativos. No entanto, você pode extraí-lo da distribuição do AEM jar e usá-lo com a configuração do servidor de aplicativos:

1. Primeiro, baixe o arquivo de início rápido do AEM e extraia-o:

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. Vá para o local da inicialização rápida do AEM recém-descompactado e copie a `crx-quickstart/opt/notsoserial/` pasta para a `crx-quickstart` pasta da instalação do servidor de aplicativos AEM.

1. Altere a propriedade de `/opt` para o usuário que está executando o servidor:

   ```shell
   chown -R opt <user running the server>
   ```

1. Configure e verifique se o agente foi ativado corretamente, como mostrado nas seções a seguir deste artigo.

## Configurar o agente {#configuring-the-agent}

A configuração padrão é adequada para a maioria das instalações. Isso inclui uma lista de blocos de classes vulneráveis de execução remota conhecida e uma lista de permissões de pacotes nos quais a desserialização de dados confiáveis deve ser relativamente segura.

A configuração do firewall é dinâmica e pode ser alterada a qualquer momento por:

1. Ir para o Web Console em `https://server:port/system/console/configMgr`
1. Procurando e clicando em Configuração do firewall de **desserialização.**

   >[!NOTE]
   >
   >Você também pode acessar a página de configuração diretamente acessando o URL em:
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`


Essa configuração contém a lista de permissões, a lista de blocos e o registro de desserialização.

**Permitir listagem**

Na seção de listagem de permissões, essas são classes ou prefixos de pacote que serão permitidos para desserialização. É importante estar ciente de que, se você estiver desserializando classes próprias, precisará adicionar as classes ou pacotes a essa lista de permissões.

**Lista de blocos**

Na seção de listagem de blocos, há classes que nunca são permitidas para desserialização. O conjunto inicial dessas classes está limitado a classes que foram consideradas vulneráveis a ataques de execução remota. A lista de blocos é aplicada antes de qualquer entrada listada permitida.

**Registro de diagnóstico**

Na seção para registro em log de diagnóstico, você pode escolher várias opções para registrar quando a desserialização estiver ocorrendo. Eles só são conectados na primeira utilização e não são registrados novamente em utilizações subsequentes.

O padrão de **class-name-only** informará as classes que estão sendo desserializadas.

Você também pode definir a opção de pilha **** completa que registrará uma pilha java da primeira tentativa de desserialização para informá-lo onde sua desserialização está ocorrendo. Isso pode ser útil para localizar e remover a desserialização de seu uso.

## Verificação da Ativação do agente {#verifying-the-agent-s-activation}

Você pode verificar a configuração do agente de desserialização navegando até o URL em:

* `https://server:port/system/console/healthcheck?tags=deserialization`

Após acessar o URL, uma lista de verificações de integridade relacionadas ao agente será exibida. Você pode determinar se o agente está ativado corretamente verificando se as verificações de integridade estão sendo bem-sucedidas. Se estiverem falhando, talvez seja necessário carregar o agente manualmente.

Para obter mais informações sobre como solucionar problemas com o agente, consulte [Manuseio de erros com carregamento](#handling-errors-with-dynamic-agent-loading) de agente dinâmico abaixo.

>[!NOTE]
>
>Se você adicionar `org.apache.commons.collections.functors` à lista de permissões, a verificação de integridade sempre falhará.

## Tratamento de erros com carregamento de agente dinâmico {#handling-errors-with-dynamic-agent-loading}

Se erros forem expostos no registro ou as etapas de verificação detectarem um problema ao carregar o agente, talvez seja necessário carregar o agente manualmente. Isso também é recomendável se você estiver usando um JRE (Ambiente Java Runtime) em vez de um JDK (Java Development Toolkit), já que as ferramentas para carregamento dinâmico não estão disponíveis.

Para carregar o agente manualmente, siga as instruções abaixo:

1. Modifique os parâmetros de inicialização JVM do jar CQ, adicionando a seguinte opção:

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >Isso requer o uso da opção -nofork CQ/AEM, juntamente com as configurações de memória JVM apropriadas, já que o agente não será ativado em uma JVM bifurcada.

   >[!NOTE]
   >
   >A distribuição da Adobe do jar do agente NotSoSerial pode ser encontrada na `crx-quickstart/opt/notsoserial/` pasta da instalação do AEM.

1. Parar e reiniciar a JVM;

1. Verifique a ativação do agente novamente seguindo as etapas descritas acima em [Verificando a Ativação](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation)do agente.

## Outras considerações {#other-considerations}

Se você estiver executando em uma IBM JVM, consulte a documentação sobre suporte para a API Java Attach [neste local](https://www.ibm.com/support/knowledgecenter/SSSTCZ_2.0.0/com.ibm.rt.doc.20/user/attachapi.html).
