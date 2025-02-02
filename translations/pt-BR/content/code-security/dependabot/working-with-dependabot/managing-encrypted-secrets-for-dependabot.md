---
title: Gerenciar segredos criptografados para o Dependabot
intro: 'Você pode armazenar informações confidenciais como, por exemplo, senhas e tokens de acesso, como segredos criptografados e, em seguida, referenciá-los no arquivo de configuração do {% data variables.product.prodname_dependabot %}.'
redirect_from:
  - /github/administering-a-repository/managing-encrypted-secrets-for-dependabot
  - /code-security/supply-chain-security/managing-encrypted-secrets-for-dependabot
  - /code-security/supply-chain-security/keeping-your-dependencies-updated-automatically/managing-encrypted-secrets-for-dependabot
versions:
  fpt: '*'
  ghec: '*'
  ghes: '>3.2'
type: how_to
topics:
  - Dependabot
  - Version updates
  - Secret store
  - Repositories
  - Dependencies
shortTitle: Gerenciar segredos criptografados
---

{% data reusables.dependabot.beta-security-and-version-updates %}

## Sobre os segredos criptografados para {% data variables.product.prodname_dependabot %}

Os segredos de {% data variables.product.prodname_dependabot %} são credenciais criptografadas que você cria no nível de organização ou no nível do repositório.
Ao adicionar um segredo no nível da organização, é possível especificar quais repositórios podem acessar o segredo. Você pode usar segredos para permitir que {% data variables.product.prodname_dependabot %} atualize as dependências localizadas nos registros dos pacotes privados. Ao adicionar um segredo criptografado antes de atingir {% data variables.product.prodname_dotcom %} e que permanece criptografado até que seja usado por {% data variables.product.prodname_dependabot %} para acessar um registro de pacote privado.

Após adicionar um segredo de {% data variables.product.prodname_dependabot %}, você poderá referenciá-lo no arquivo de dependência _dependabot.yml_ dessa forma: {% raw %}`${{secrets.NAME}}`{% endraw %}, e m que "NAME" é o nome que você escolheu para o segredo. Por exemplo:

{% raw %}
```yaml
password: ${{secrets.MY_ARTIFACTORY_PASSWORD}}
```
{% endraw %}

For more information, see "[Configuration options for the dependabot.yml file](/github/administering-a-repository/configuration-options-for-dependency-updates#configuration-options-for-private-registries)."

### Nomear os seus segredos

O nome de um segredo de {% data variables.product.prodname_dependabot %}:
* Só pode conter caracteres alfanuméricos (`[A-Z]`, `[0-9]`) ou sublinhados (`_`). Não são permitidos espaços. Se você inserir letras minúsculas, elas serão alteradas para maiúsculas.
* Não precisa iniciar com o prefixo `GITHUB_`.
* Não precisa começar com um número.

## Adicionar um repositório secreto para {% data variables.product.prodname_dependabot %}

{% data reusables.actions.permissions-statement-secrets-repository %}

{% data reusables.repositories.navigate-to-repo %}
{% data reusables.repositories.sidebar-settings %}
{% data reusables.actions.sidebar-secret %}
{% data reusables.dependabot.dependabot-secrets-button %}
1. Clique em **Novo segredo do repositório**.
1. Digite um nome para o seu segredo na caixa de entrada **Nome**.
1. Insira o valor para o seu segredo.
1. Clique em **Add secret** (Adicionar segredo).

   O nome do segredo está listado na página de segredos do Dependabot. Você pode clicar em **Atualizar** para alterar o valor do segredo. Você pode clicar em **Remover** para excluir o segredo.

   ![Atualize ou remova um segredo do repositório](/assets/images/help/dependabot/update-remove-repo-secret.png)

## Adicionar um segredo de organização para {% data variables.product.prodname_dependabot %}

Ao criar um segredo em uma organização, você pode usar uma política para limitar quais repositórios podem acessar esse segredo. Por exemplo, você pode conceder acesso a todos os repositórios ou limitar o acesso a apenas repositórios privados ou a uma lista específica de repositórios.

{% data reusables.actions.permissions-statement-secrets-organization %}

{% data reusables.organizations.navigate-to-org %}
{% data reusables.organizations.org_settings %}
{% data reusables.actions.sidebar-secret %}
{% data reusables.dependabot.dependabot-secrets-button %}
1. Clique em **Novo segredo da organização**.
1. Digite um nome para o seu segredo na caixa de entrada **Nome**.
1. Insira o **Valor** para o seu segredo.
1. Na lista suspensa **Acesso do repositório**, escolha uma política de acesso.
1. Se você escolheu **repositórios selecionados**:

   * Clique em {% octicon "gear" aria-label="The Gear icon" %}.
   * Escolha os repositórios que podem acessar este segredo. ![Selecione repositórios para este segredo](/assets/images/help/dependabot/secret-repository-access.png)
   * Clique em **Atualizar seleção**.

1. Clique em **Add secret** (Adicionar segredo).

   O nome do segredo está listado na página de segredos do Dependabot. Você pode clicar em **Atualizar** para alterar o valor secreto ou sua política de acesso. Você pode clicar em **Remover** para excluir o segredo.

   ![Atualizar ou remover um segredo da organização](/assets/images/help/dependabot/update-remove-org-secret.png)

## Adicionar {% data variables.product.prodname_dependabot %} à sua lista de permissão de endereços IP

Se o seu registro privado estiver configurado com um IP de permissão de lista, você poderá encontrar o endereço IP que {% data variables.product.prodname_dependabot %} usa para acessar o registro no ponto de extermidade meta da API na chave do `dependabot`. Para obter mais informações, consulte "[Meta](/rest/reference/meta)".
