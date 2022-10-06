---
title: Acesso WebDAV
seo-title: WebDAV Access
description: Saiba mais sobre o acesso WebDAV no AEM.
seo-description: Learn about WebDAV access in AEM.
uuid: b0ecaa5d-5454-42df-8453-404ece734c32
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 1eaf7afe-a181-45df-8766-bd564b1ad22a
exl-id: 891ee66c-e49c-4561-8fef-e6e448a8aa1c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 0%

---

# Acesso WebDAV{#webdav-access}

Para se conectar ao AEM via WebDAV com o KDE:

AEM oferece suporte ao WebDAV, que permite exibir e editar o conteúdo do repositório. A conexão via WebDAV fornece acesso direto ao repositório de conteúdo por meio da área de trabalho. Os arquivos de texto e PDF adicionados ao repositório por meio da conexão WebDAV são automaticamente indexados por texto completo e podem ser pesquisados com as interfaces de pesquisa padrão e por meio das APIs Java padrão.

## Geral {#general}

[Instruções detalhadas por sistema operacional](/help/sites-administering/webdav-access.md#connecting-via-webdav) estão incluídos neste documento, mas, essencialmente, para se conectar ao seu repositório usando o protocolo WebDAV, você aponta seu cliente WebDAV para o seguinte local:

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

Esse URL, quando conectado a partir do nível do sistema operacional, fornece acesso WebDAV ao espaço de trabalho padrão ( `crx.default`). Embora seja mais simples para o usuário, ele não oferece a flexibilidade adicional de especificar nomes de espaço de trabalho, o que pode ser feito usando recursos adicionais [URLs do WebDAV](/help/sites-administering/webdav-access.md#webdav-urls).

AEM exibe o conteúdo do repositório da seguinte maneira:

* Um nó do tipo `nt:folder` é exibida como uma pasta. Nós abaixo do `nt:folder` são exibidos como conteúdo da pasta.

* Um nó do tipo `nt:file` é exibido como um arquivo. Nós abaixo do `nt:file` não são exibidos, mas formam o conteúdo do arquivo.

Quando você usa o WebDAV para criar e editar pastas e arquivos, AEM cria e edita as `nt:folder` e `nt:file` nós. Se você planeja usar o WebDAV para importar e exportar conteúdo, tente trabalhar com a `nt:file` e `nt:folder` O nó digita o máximo possível.

>[!NOTE]
>
>Antes de configurar o WebDAV, verifique o [Requisitos técnicos](/help/sites-deploying/technical-requirements.md#webdav-clients).

## URLs do WebDAV {#webdav-urls}

O URL do servidor WebDAV tem a seguinte estrutura:

<table>
 <colgroup>
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
 </colgroup>
 <tbody>
  <tr>
   <td>
    <code>
     <strong>URL Component</strong>
    </code></td>
   <td><code>https://&lt;host&gt;:&lt;port&gt;</code></td>
   <td><code>/&lt;crx-webapp-path&gt;</code></td>
   <td><code>/repository</code></td>
   <td><code>/&lt;workspace&gt;</code></td>
  </tr>
  <tr>
   <td>
    <code>
     <strong>Example</strong>
    </code></td>
   <td><code>http://localhost:4502</code></td>
   <td><code>/crx</code></td>
   <td><code>/repository</code></td>
   <td><code>/crx.default</code></td>
  </tr>
  <tr>
   <td><strong>Descrição</strong></td>
   <td>Host e porta em que AEM é executado</td>
   <td>Caminho para o webapp do repositório AEM</td>
   <td>Caminho para o qual o servlet WebDAV está mapeado</td>
   <td>Nome do espaço de trabalho</td>
  </tr>
 </tbody>
</table>

Ao alterar o elemento do espaço de trabalho no caminho, você pode mapear espaços de trabalho diferentes do padrão ( `crx.default`). Por exemplo, para mapear um espaço de trabalho chamado `staging`, use o seguinte URL:

```xml
http://localhost:4502/crx/repository/staging
```

## Conexão via WebDAV {#connecting-via-webdav}

[Tal como acima mencionado](/help/sites-administering/webdav-access.md#general), para se conectar ao seu repositório usando o protocolo WebDAV, você aponta seu cliente WebDAV para o local do seu repositório. No entanto, dependendo do sistema operacional, as etapas envolvidas para conectar seu cliente são diferentes e pode haver configuração do sistema operacional necessária.

São fornecidas instruções sobre como conectar os seguintes sistemas operacionais:

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

Para conectar com êxito um sistema Microsoft Windows 7 (e superior) a uma instância AEM que não esteja protegida com SSL, a opção para estabelecer a autenticação básica por uma rede não segura deve estar habilitada explicitamente no Windows. Isso requer uma alteração no Registro do Windows do WebClient.

Depois que o registro é atualizado, a instância de AEM pode ser mapeada como uma unidade.

#### Windows 7 e Configuração Superior {#windows-and-greater-configuration}

Para atualizar o registro para permitir a autenticação básica através de uma rede não segura:

1. Localize a seguinte subchave do Registro:

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. Defina as `BasicAuthLevel` subchave de entrada do registro para um valor de `2` ou maior.

   Se não estiver presente, adicione a subchave.

1. Você deve reiniciar o sistema para que a alteração no registro entre em vigor.

Consulte [Suporte Microsoft KB 841215](https://support.microsoft.com/default.aspx/kb/841215) para obter mais informações sobre esta alteração de registro.

Consulte [Suporte Microsoft KB 2445570](https://support.microsoft.com/kb/2445570) para obter informações sobre como melhorar a capacidade de resposta do WebDav Client no Windows.

>[!NOTE]
>
>O Adobe recomenda que você crie um usuário do Windows com as mesmas credenciais que o usuário do repositório; caso contrário, poderá encontrar conflitos de permissão.

#### Configuração do Windows 8 {#windows-configuration}

No Windows 8, também é necessário alterar a entrada do Registro [conforme descrito para o Windows 7 e posterior](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). No entanto, antes que você possa fazer isso, a Experiência do Desktop deve estar ativada para ver a entrada do Registro.

Para ativar a Experiência do desktop, abra **Gerenciador do servidor**, em seguida **Recursos**, em seguida **Adicionar recursos**, em seguida **Experiência desktop**.

Após a reinicialização, a entrada do Registro descrita para o Windows 7 e superior está disponível. Modifique-o conforme descrito para o Windows 7 e superior.

#### Conexão no Windows {#connecting-in-windows}

Para se conectar ao AEM via WebDAV em um ambiente Windows:

1. Abrir **Windows Explorer** ou **Explorador de arquivos** e clique em **Computador** ou **Este PC**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. Clique em **Mapear unidade de rede** para iniciar o assistente.
1. Insira os detalhes do mapeamento:

   * **Unidade**: Escolha qualquer letra disponível
   * **Pasta**: `http://localhost:4502`
   * Verificar **Conectar usando credenciais diferentes**

   Clique em Concluir

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >Se AEM estiver em outra porta, use esse número de porta em vez de 4502. Além disso, se você não estiver executando o repositório de conteúdo em sua máquina local, substitua `localhost` com o respectivo nome de servidor ou endereço IP.

1. Inserir nome de usuário `admin` e senha `admin`. O Adobe recomenda usar a conta de administrador pré-configurada para testes.

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. O assistente é fechado e a unidade recém-mapeada é aberta em uma janela do Windows Explorer ou do Explorador de Arquivos.

   ![chlimage_1-115](assets/chlimage_1-115a.png)

O Windows agora mapeou AEM como uma unidade via WebDAV e você pode usá-la como qualquer outra unidade.

### macOS {#macos}

Não há etapas de configuração necessárias para se conectar via WebDAV no macOS. Basta se conectar ao servidor WebDAV.

1. Navegue até qualquer **Localizador** e clique em **Ir** e **Conectar ao Servidor** ou pressione **Command+k**.
1. No **Conectar ao Servidor** , insira o local AEM:

   * `http://localhost:4502`
   >[!NOTE]
   >
   >Se AEM estiver em outra porta, use esse número de porta em vez de 4502. Além disso, se você não estiver executando o repositório de conteúdo em sua máquina local, substitua `localhost` com o respectivo nome de servidor ou endereço IP.

1. Quando for solicitado a autenticação, insira o nome de usuário `admin` e senha `admin`. O Adobe recomenda usar a conta de administrador pré-configurada para testes.

A macOS agora se conectou ao AEM via WebDAV e você pode usá-lo como qualquer outra pasta em seu Mac.

### Linux {#linux}

A conexão via WebDAV no Linux não requer configuração, mas envolve algumas etapas para fazer a conexão que variam de acordo com o ambiente de desktop.

#### NOME {#gnome}

Para se conectar ao AEM via WebDAV com GNOME:

1. Em Nautilus (explorador de arquivos), selecione **Places** e selecione **Conectar ao Servidor**.
1. No **Conectar ao Servidor** selecione WebDAV (HTTP) em Tipo de serviço.

1. Em **Servidor**, insira `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Se AEM estiver em outra porta, use esse número de porta em vez de 4502. Além disso, se você não estiver executando o repositório de conteúdo em sua máquina local, substitua `localhost` com o respectivo nome de servidor ou endereço IP.

1. Em **Pasta**, insira `/dav`
1. Insira o nome de usuário `admin`. O Adobe recomenda usar a conta de administrador pré-configurada para testes.
1. Deixe a porta em branco e insira qualquer nome para a conexão.
1. Clique em **Connect**. AEM solicita sua senha.
1. Digite a senha `admin` e clique em **Connect**.

O GNOME agora montou AEM como um volume e você pode usá-lo como qualquer outro volume.

#### KDE {#kde}

1. Abra o assistente de Pasta de rede.
1. Selecionar **WebFolder**(webdav) e clique em Avançar.
1. Em **Nome**, digite um nome de conexão.
1. Em **Usuário**, insira `admin.` O Adobe recomenda usar a conta de administrador pré-configurada.
1. Em **Servidor**, insira `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >Se AEM estiver em outra porta, use esse número de porta em vez de 4502. Além disso, se você não estiver executando o repositório de conteúdo em sua máquina local, substitua `localhost` com o respectivo nome de servidor ou endereço IP

1. Em **Pasta**, insira `dav`

1. Clique em **Salvar e conectar**.
1. Quando for solicitada sua senha, digite a senha `admin` e clique em **Connect**.

O KDE agora montou AEM como um volume e você pode usá-lo como qualquer outro volume.
