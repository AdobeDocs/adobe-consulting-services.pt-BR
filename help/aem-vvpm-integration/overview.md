---
title: Visão geral da integração do Veeva Vault
description: Visão geral da integração do Veeva Vault
exl-id: 52cc7290-b7e1-4476-877f-48934e6daf68
source-git-commit: 005c738818ab622a342ddc3a94e94638e344d058
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Introdução ao Veeva Vault PromoMats e integração com o Adobe Experience Manager

Essa integração gerenciará seu conteúdo, aplicando direitos e conformidade e aproveitando a primeira experiência do setor.

Essa integração exige as seguintes versões mínimas de software:

* Adobe Experience Manager, 6.5.5+
* Veeva Vault PromoMats, 20R3.2+

>[!NOTE]
>
>Os usuários do serviço e as permissões apropriadas são necessários em ambos os sistemas para a integração.
>

>[!IMPORTANT]
>
>Esse recurso não está disponível para uso imediato como parte do produto. A implementação exige o contrato de manutenção da Adobe Consulting. Entre em contato com o representante da Adobe para obter mais informações.
>

## Princípios e recursos

Essa integração foi projetada para suportar dois casos de uso principais:

1. Aprovação de conteúdo - Quando um novo conteúdo for criado ou um conteúdo existente for editado no AEM, o conteúdo deverá ser aprovado para uso no VVPM, que dá suporte ao processo de aprovação médica, legal e regulamentar (MLR) para ciências biomédicas.

2. Gerenciamento de conteúdo - fornece visibilidade da utilização de ativos estabelecendo relações em PromoMats entre táticas digitais (por exemplo, email, apresentações, sites) e seus elementos (por exemplo, logotipos, fotografia, gráficos) criados em AEM para documentos originários do AEM.

Os benefícios incluem:

* Manutenção de uma única fonte da verdade para ativos e conteúdo sem duplicação em repositórios digitais.
* Aproveitar o Veeva Vault para gerenciamento de direitos e conformidade e o AEM para o melhor da categoria e criação/entrega de ativos e conteúdo.
* Ajuda a automatizar a movimentação de conteúdo e metadados entre AEM e Veeva Vault.
* Reduz o esforço manual no envio de conteúdo para Veeva para workflows de aprovação.
* Cada sistema é usado por seus pontos fortes e o conector auxilia na movimentação automática de conteúdo entre os sistemas para ajudar a acelerar o tempo de entrada no mercado.

O que a integração faz?

* Suporta o envio de páginas do site AEM, ativos, fragmentos de conteúdo e fragmentos de experiência para o VPM. Páginas AEM, Fragmentos de conteúdo e Fragmentos de experiência podem ser enviados como PDF ou imagens de captura de tela. Os binários do AEM Assets são enviados como estão.
* Oferece suporte à sincronização manual e automatizada de elementos de metadados selecionados que podem ser configurados de AEM para VPM.
* Oferece suporte à sincronização manual e automatizada de elementos de metadados selecionados que podem ser configurados de VPM para AEM.
* Oferece suporte a relacionamentos entre páginas do site AEM, ativos, fragmentos de conteúdo e fragmentos de experiência no VPM para automatizar os relacionamentos de conteúdo.
* Oferece suporte à geração de representação para vários tipos de dispositivos.

>[!NOTE]
>
>Consulte a documentação de uso da integração para obter mais detalhes sobre as opções de configuração.
>

O que o conector NÃO faz?

* Não reproduz processos e funcionalidades do AEM em Veeva ou vice-versa.
* Não faz a MLR por si só. Ele auxilia na automação do envio de conteúdo para Veeva para onde a MLR acontece.
* Não deve ser usado para criar uma configuração idêntica entre AEM e Veeva. Nem todo o conteúdo precisa se mover entre as duas plataformas.


>[!IMPORTANT]
>
>Essa integração considera atualmente o AEM como a fonte da verdade para a sincronização do conteúdo.
>

## Obter a integração

Para provisionar essa integração, é necessário seguir as etapas abaixo.

Siga os detalhes do fluxograma e do fluxograma abaixo para solicitar e configurar a integração.

![Solicitar acesso](assets/integration-request.png)

Detalhes do fluxograma (mapeia para as etapas acima):

* **Etapa 1** - Presume-se que você já tenha, ou esteja em processo de aquisição, uma licença para Veeva Vault PromoMats e para Adobe Experience Manager.
* **Etapa 2** - Uma nova ordem de venda (SO) que descreve um contrato de manutenção com a Adobe Consulting precisará ser assinada para aproveitar a integração.
* **Etapa 3** - Instalar, ativar e configurar o pacote de integração.

## Suporte

A seguir, é descrito como entrar em contato e registrar um problema com a equipe de suporte.

### Solicitação de integração ou suporte do Adobe Experience Manager

Os tíquetes de suporte podem ser registrados no Atendimento ao cliente do Adobe. O administrador do Adobe Experience Cloud precisará fazer logon no [Adobe Admin Console](https://adminconsole.adobe.com/), clique na guia suporte e crie um caso. Em caso de problemas de integração, inclua as seguintes informações:

* **Título do processo**: `AEM - Veeva Vault Integration`
* **Proprietário do processo**: `Data Engineering`
* **Descrição**: `Description of the issue`
* **Ponto de contato**: `The email address(es) for relavant AEM point of contacts for your organization.`
* **URL da instância do AEM**: `Place the Adobe Experience Manager instance url here.`
* **URL da instância Veeva**: `Place the Veeva Vault PromoMats instance url here.`

### Solicitação de suporte ao Veeva Vault PromoMats

Às vezes, o problema que está sendo experimentado é um problema com a operação da instância Veeva Vault PromoMats. Se esse for o caso, o administrador do Veeva Vault PromoMats pode ser direcionado para criar um tíquete de suporte com [Suporte a Veeva](http://support.veeva.com/). O status da instância do Veeva pode ser visualizado navegando até [Veeva Trust](http://trust.veeva.com/).

