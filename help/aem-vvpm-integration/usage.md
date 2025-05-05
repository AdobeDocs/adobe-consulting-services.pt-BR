---
title: Uso da integração do Veeva Vault
description: Uso da integração do Veeva Vault
exl-id: efff7af1-eb25-4a1d-b7ef-52e3336970ff
source-git-commit: 19949a48cfee0c17481e52f286a460e9d81d7ff0
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 0%

---

# Uso da integração

## Apresentação

A apresentação de vídeo a seguir descreve o uso do conector:

>[!VIDEO](https://video.tv.adobe.com/v/332137/?quality=12&learn=on)

## Configurar

Este guia o guiará durante a colocação e o funcionamento do conector.

>[!IMPORTANT]
>
>Para cada sistema, essas etapas precisam ser executadas por um **administrador** para cada sistema.
>
>As etapas desta documentação guiarão você pela criação de integrações/registros que envolvem a atribuição de permissões e/ou acesso de administrador.  É sua responsabilidade garantir que essas etapas estejam em conformidade com as políticas de sua empresa antes de executar o, e executá-las com cuidado.
>

### Instalar pacote de integração

Você receberá acesso ao pacote de integração AEM. Há duas opções para instalar a integração:

1. **Instalação do Pacote** - Direta e menos envolvida.
2. **Instalação de POM** - Mais avançada, mas pode ser útil ao usar o AEM Cloud Manager e atualizar a integração.

#### Instalação do pacote

Para instalar o pacote, baixe-o com o link fornecido no email de integração. [Para obter instruções detalhadas sobre como instalar um pacote AEM, clique aqui.](https://experienceleague.adobe.com/docs/experience-manager-64/administering/contentmanagement/package-manager.html?lang=pt-BR&#installing-packages)

#### Instalação do POM

Para incluir o conector em seu POM, siga estas etapas. Substitua seu nome de usuário e senha pelos recebidos no email de integração.

1. Adicione o seguinte ao arquivo `.cloudmanager/maven/settings.xml` em seu projeto ou `~/.m2/settings.xml` em seu computador. Substitua `YOUR_USERNAME` pelo nome de usuário e `YOUR_PASSWORD` pela senha fornecida no email de integração.

   >[!IMPORTANT]
   >
   >Se estiver usando o Cloud Manager, a abordagem segura é seguir as etapas encontradas aqui para [repositórios Maven protegidos por senha](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/create-application-project/setting-up-project.html?lang=pt-BR#password-protected-maven-repositories).
   >

   ```
   <settings>
       ...
       <servers>
           ...
           <server>
               <id>repo.ea.adobe.net</id>
               <username>YOUR_USERNAME</username>
               <password>YOUR_PASSWORD</password>
               <filePermissions>BucketOwnerFullControl</filePermissions>
               <configuration>
                 <wagonProvider>s3</wagonProvider>
               </configuration>
           </server>
           ...
       </servers>
       ...
   </settings>
   ```

2. Adicione o seguinte ao arquivo `pom.xml` do projeto:

   ```
   <project>
       ...
       <build>
           ...
           <extensions>
               ...
               <extension>
                   <groupId>com.allogy.maven.wagon</groupId>
                   <artifactId>maven-s3-wagon</artifactId>
                   <version>1.2.0</version>
               </extension>
               ...
           </extensions>
           ...
       </build>
       ...
       <repositories>
           ...
           <repository>
               <id>repo.ea.adobe.net</id>
               <url>s3://repo.ea.adobe.net/release</url>
               <releases>
                   <enabled>true</enabled>
               </releases>
           </repository>
           ...
       </repositories>
       ...
   </project>
   ```

3. Adicione o seguinte ao arquivo `all/pom.xml` do projeto. Substitua `project.dependencies.dependency.version` pela versão apropriada e `project.build.plugins.plugin.configuration.embeddeds.embedded.target` pelo caminho correto.

   ```
   <project>
       ...
       <build>
           ...
           <plugins>
               ...
               <plugin>
                   <groupId>org.apache.jackrabbit</groupId>
                   <artifactId>filevault-package-maven-plugin</artifactId>
                   ...
                   <configuration>
                       ...
                       <embeddeds>
                           ...
                           <embedded>
                               <groupId>com.adobe.acs.aemveeva</groupId>
                               <artifactId>aem-veeva-connector.all</artifactId>
                               <type>zip</type>
                               <target>/apps/APP_NAME-packages/application/install</target>
                           </embedded>
                           ...
                       </embeddeds>
                   </configuration>
               </plugin>
               ...
           </plugins>
           ...
       </build>
       ...
       <dependencies>
           ...
           <dependency>
               <groupId>com.adobe.acs.aemveeva</groupId>
               <artifactId>aem-veeva-connector.all</artifactId>
               <version>1.0.5</version>
               <type>zip</type>
           </dependency>            
           ...
       </dependencies>
       ...
   </project>
   ```

### Configuração de nuvem

Essa integração é configurada criando uma configuração de nuvem na pasta em que o conector estará operando. Siga estas etapas para criar uma configuração na nuvem:

1. Navegue até a configuração de nuvem da Veeva.

   ![Navegar até a configuração da nuvem](assets/cloud-config-navigate.png)

2. Crie uma nova configuração da nuvem do Veeva na pasta apropriada e preencha o conforme descrito nas próximas seções.

   ![Criar configuração de nuvem](assets/cloud-config-create.png)

#### Guia Configuração

Preencha o seguinte na guia de configuração:

![Guia Configuração](assets/configuration-tab.png)

1. Obrigatório. Título para a configuração do conector do Veeva Vault. Isso pode ser um valor arbitrário. (ex.: `Veeva Vault Configuration`)
2. Obrigatório. O URL de domínio da instância Veeva (ex.: `https://my-instance.veevavault.com/`)
3. Obrigatório. ClientID necessária para chamar a API do Veeva Vault. Pode ser um valor arbitrário e é usado principalmente para depuração. (ex.: `adobe-aem-vvtechpartner`)
4. Obrigatório. Nome de usuário do Veeva Vault. Consulte [Criação de usuários do Veeva](#veeva-user-creation).
5. Obrigatório. Senha do Veeva Vault. Consulte [Criação de usuários do Veeva](#veeva-user-creation).

#### Guia Adobe IO

Se o projeto precisar gerar PDF ou imagens para páginas, esta guia será necessária. Preencha o seguinte na guia do adobe io:

![Guia E/S de Adobe](assets/adobe-io-tab.png)

1. Obrigatório. O endpoint de E/S de Adobe para criar imagens de PDF que foi fornecido no email de integração. (ex.: `https://my-namespace.adobeioruntime.net/api/v1/web/aem-veeva-serverless-0.0.2/trigger-action.json`)
2. Obrigatório. O nome da ação para a geração da imagem da página. Este valor deve ser `aem-veeva-integration/get-image-async`.
3. Obrigatório. O nome da ação para geração de imagem html. Este valor deve ser `aem-veeva-integration/get-pdf-async-new`.
4. Obrigatório. O endpoint de E/S Adobe para obter o estado da geração fornecida no email de integração.(ex.: `https://my-namespace.adobeioruntime.net/api/v1/web/aem-veeva-serverless-0.0.2/get-state-value`)
5. Obrigatório. Nome de usuário do AEM a ser usado pelo Adobe IO. Consulte [Criação de usuário do AEM](#aem-user-creation).
6. Obrigatório. Senha do AEM a ser usada pelo Adobe IO. Consulte [Criação de usuário do AEM](#aem-user-creation).
7. Opcional. O tempo limite padrão é permitir que a página responda até um tempo especificado após o qual o serviço AIO para de tentar obter uma resposta. O valor padrão é `30000`.
8. Opcional. O atraso ocorre depois que a página responde com 200 para atrasar a renderização de todas as imagens antes de capturar a tela. O valor padrão é `2000`.
9. Opcional. O URL gerado pela captura de tela/PDF expirará após o valor configurado em segundos.
10. Opcional. O serviço de geração de PDF/captura de tela de E/S de Adobe é assíncrono. O serviço AEM chama o endpoint de status AIO para obter captura de tela/PDF. Essa propriedade decidirá em milissegundos a pausa entre em cada chamada de status. O valor padrão é `10000`.
11. Opcional. Contagem máxima de tentativas para chamada de status para Adobe IO para obter captura de tela/PDF. O valor padrão é `10`.

#### Guia Avançado

Preencha o seguinte na guia avançado:

![Guia Avançado](assets/advanced-tab.png)

1. Necessário para geração de PDF/imagem. O padrão de nome de arquivo usado ao criar PDF/imagens. `{name}` pode ser modelado. (ex.: `{name}-screenshot`)
2. Opcional. Os tipos de dispositivo para os quais as capturas de tela das páginas são necessárias diferentes da Área de Trabalho. Os tipos válidos incluem `Tab (iPad)` e `Mobile (iPhone X)`.
3. Opcional. O valor do tipo de representação em Veeva que representa a representação acima. (ex.: `web_ready__c`)
4. Necessário para geração de PDF/imagem. Tipo de captura de tela a ser criada. `PDF` ou `Image`.
5. Necessário para geração de PDF/imagem. O tipo de PDF a ser gerado. `Print CSS Based PDF` ou `Pixel Perfect Screenshot PDF`.
6. Necessário para geração de PDF/imagem. O tipo de imagem a ser gerado. `PNG` ou `JPEG`.
7. Obrigatório. Fluxo de trabalho a ser executado depois que o acionador de Aprovação do Veeva Vault chegar.
8. Obrigatório. Valor da propriedade de status que representa Aprovado. (ex.: `Approved for Distribution`)
9. Obrigatório. Fluxo de trabalho a ser executado depois que o acionador de Rejeição do Veeva Vault tiver chegado.
10. Obrigatório. Valor da propriedade de status que representa Rejeitado/Não aprovado. (ex.: `Rejected`)
11. Opcional. Nome da propriedade para ID do documento no Veeva Vault. O valor padrão é `id`.
12. Opcional. Nome da propriedade para Status no Veeva Vault. O valor padrão é `status__v`.
13. Opcional. Nome da propriedade para Data de modificação do documento. O valor padrão é `version_modified_date__v`.
14. Opcional. Nome da propriedade do URL de recurso do documento. O valor padrão será `external_id__v`. Se esse campo já estiver em uso, crie um campo diferente em Veeva e preencha o nome do campo aqui. Esse campo será usado no Veeva para manter o caminho de recursos do AEM. Isso é necessário para a sincronização automatizada de metadados.
15. Opcional. Nome da propriedade para Número de Versão Principal no Veeva Vault. O valor padrão é `major_version_number__v`.
16. Opcional. Nome da propriedade para Número de Versão Secundária no Veeva Vault. O valor padrão é `minor_version_number__v`.
17. Opcional. Valor de tipo de relacionamento do Veeva Vault. Todos os ativos adicionados à página serão representados como relacionados com base nesse valor. O valor padrão é `supporting_document__c`.

#### Guia Página

Se estiver sincronizando páginas, preencha o seguinte na guia da página:

![Guia Página](assets/page-tab.png)

1. Obrigatório. Mapeie uma propriedade do AEM para Veeva.
a. Nome da propriedade AEM. Selecionável nas propriedades do AEM. (por exemplo, `jcr:title`) `{name}` pode ser modelado.
b. O nome da propriedade Veeva inserido exatamente em is existe em Veeva. (ex.: `name__v`)\
   c. Tipo de propriedade. `Text` ou `Multiline Text`.

2. Obrigatório. Mapeie uma propriedade de Veeva para AEM.
a. O nome da propriedade Veeva inserido exatamente em is existe em Veeva. (ex.: `name__v`)
b. Nome da propriedade AEM. Selecionável nas propriedades do AEM. (ex.: `jcr:title`)
c. Tipo de propriedade. `Text` ou `Multiline Text`.


#### Guia Ativo

Se estiver sincronizando ativos, preencha o seguinte na guia Ativo:

![Guia Ativo](assets/asset-tab.png)

1. Obrigatório. Mapeie uma propriedade do AEM para Veeva.
a. Nome da propriedade AEM. Selecionável nas propriedades do AEM. (por exemplo, `/jcr:content/metadata/jcr:title`) `{name}` pode ser modelado.
b. O nome da propriedade Veeva inserido exatamente em is existe em Veeva. (ex.: `name__v`)
c. Tipo de propriedade. `Text` ou `Multiline Text`.

2. Obrigatório. Mapeie uma propriedade de Veeva para AEM.
a. O nome da propriedade Veeva inserido exatamente em is existe em Veeva. (ex.: `name__v`)
b. Nome da propriedade AEM. Selecionável nas propriedades do AEM. (ex.: `/jcr:content/metadata/jcr:title`)
c. Tipo de propriedade. `Text` ou `Multiline Text`.

### Configuração adicional

#### Criação de usuários no AEM

Durante a geração de PDF/imagem, um usuário AEM precisa ser criado para obter páginas do AEM. Crie e forneça permissões somente leitura a um usuário seguindo estes links:

Se estiver usando o AEM 6.5.5+:

* [Criando um usuário no AEM](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/setup-organize-users/adding-configuring-users.html?lang=pt-BR&#create-a-user)
* [Adicionando permissões a um usuário no AEM](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html?lang=pt-BR&#permissions-in-aem)

Se estiver usando Cloud Service AEM:

* [Gerenciando usuários com AEM Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=pt-BR&#accessing)

As seguintes permissões são necessárias para o usuário do serviço AEM no conteúdo que será convertido em PDF/Imagem e enviado para a Veeva:

* Ler

>[!IMPORTANT]
>
> Essas ações devem ser executadas como administrador para cada sistema.
> Você deve estar em conformidade com os padrões de segurança de suas organizações ao criar usuários e definir permissões.
>

#### Criação de usuários Veeva

Para usar essa integração, um usuário precisa ser criado no Veeva Vault. Para criar um usuário, siga estas etapas:

1. Navegue até Admin -> Usuários e grupos -> Usuários do Vault -> Criar

   ![Navegar até o usuário Veeva](assets/veeva-user-navigate.png)

2. Preencha as entradas necessárias. A configuração mais simples é definir `License Type` como `Full User` e `Security Profile` como `Vault Owner`. Salvar ao concluir.

   ![Criar Usuário Veeva](assets/veeva-user-create.png)

As seguintes permissões são necessárias para os tipos de documentos Veeva específicos que estão sendo usados:

* Criar/Ler documentos
* Criar/Ler versões
* Criar/atualizar metadados
* Criar/atualizar representações

>[!IMPORTANT]
>
> Essas ações devem ser executadas como administrador para cada sistema.
> Você deve estar em conformidade com os padrões de segurança de suas organizações ao criar usuários e definir permissões.
>
