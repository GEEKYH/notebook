> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [docs.github.com](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

> Use a personal access token in place of a password when authenticating to GitHub in the command line ......

Use a personal access token in place of a password when authenticating to GitHub in the command line or with the API.

[About personal access tokens](#about-personal-access-tokens)
-------------------------------------------------------------

Personal access tokens are an alternative to using passwords for authentication to GitHub when using the [GitHub API](https://docs.github.com/en/rest/overview/authenticating-to-the-rest-api) or the [command line](#using-a-personal-access-token-on-the-command-line).

Personal access tokens are intended to access GitHub resources on behalf of yourself. To access resources on behalf of an organization, or for long-lived integrations, you should use a GitHub App. For more information, see "[About creating GitHub Apps](https://docs.github.com/en/apps/creating-github-apps/setting-up-a-github-app/about-creating-github-apps)."

### [Types of personal access tokens](#types-of-personal-access-tokens)

GitHub currently supports two types of personal access tokens: fine-grained personal access tokens and personal access tokens (classic). GitHub recommends that you use fine-grained personal access tokens instead of personal access tokens (classic) whenever possible.

Organization owners can set a policy to restrict the access of personal access tokens (classic) to their organization. For more information, see "[Setting a personal access token policy for your organization](https://docs.github.com/en/organizations/managing-programmatic-access-to-your-organization/setting-a-personal-access-token-policy-for-your-organization#restricting-access-by-personal-access-tokens-classic)."

#### [Fine-grained personal access tokens](#fine-grained-personal-access-tokens)

Fine-grained personal access tokens have several security advantages over personal access tokens (classic):

*   Each token can only access resources owned by a single user or organization.
*   Each token can only access specific repositories.
*   Each token is granted specific permissions, which offer more control than the scopes granted to personal access tokens (classic).
*   Each token must have an expiration date.
*   Organization owners can require approval for any fine-grained personal access tokens that can access resources in the organization.

#### [Personal access tokens (classic)](#personal-access-tokens-classic)

Personal access tokens (classic) are less secure. However, some features currently will only work with personal access tokens (classic):

*   Only personal access tokens (classic) have write access for public repositories that are not owned by you or an organization that you are not a member of.
*   Outside collaborators can only use personal access tokens (classic) to access organization repositories that they are a collaborator on.
*   Some REST API operations are not available to fine-grained personal access tokens. For a list of REST API operations that are supported for fine-grained personal access tokens, see "[Endpoints available for fine-grained personal access tokens](https://docs.github.com/en/rest/overview/endpoints-available-for-fine-grained-personal-access-tokens)".

If you choose to use a personal access token (classic), keep in mind that it will grant access to all repositories within the organizations that you have access to, as well as all personal repositories in your personal account.

As a security precaution, GitHub automatically removes personal access tokens that haven't been used in a year. To provide additional security, we highly recommend adding an expiration to your personal access tokens.

### [Keeping your personal access tokens secure](#keeping-your-personal-access-tokens-secure)

Personal access tokens are like passwords, and they share the same inherent security risks. Before creating a new personal access token, consider if there is a more secure method of authentication available to you:

*   To access GitHub from the command line, you can use [GitHub CLI](https://docs.github.com/en/github-cli/github-cli/about-github-cli) or [Git Credential Manager](https://github.com/GitCredentialManager/git-credential-manager/blob/main/README.md) instead of creating a personal access token.
*   When using a personal access token in a GitHub Actions workflow, consider whether you can use the built-in `GITHUB_TOKEN` instead. For more information, see "[Automatic token authentication](https://docs.github.com/en/actions/security-guides/automatic-token-authentication)."

If these options are not possible, and you must create a personal access token, consider using another service such as the [1Password CLI](https://developer.1password.com/docs/cli/secret-references/) to store your token securely, or 1Password's [GitHub shell plugin](https://developer.1password.com/docs/cli/shell-plugins/github/) to securely authenticate to GitHub CLI.

When using a personal access token in a script, you can store your token as a secret and run your script through GitHub Actions. For more information, see "[Encrypted secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets)."You can also store your token as a Codespaces secret and run your script in Codespaces. For more information, see"[Managing encrypted secrets for your codespaces](https://docs.github.com/en/codespaces/managing-your-codespaces/managing-encrypted-secrets-for-your-codespaces)."

[Creating a fine-grained personal access token](#creating-a-fine-grained-personal-access-token)
-----------------------------------------------------------------------------------------------

**Note**: Fine-grained personal access token are currently in beta and subject to change. To leave feedback, see [the feedback discussion](https://github.com/community/community/discussions/36441).

1.  [Verify your email address](https://docs.github.com/en/get-started/signing-up-for-github/verifying-your-email-address), if it hasn't been verified yet.
    
2.  In the upper-right corner of any page, click your profile photo, then click **Settings**.
    
    ![](https://docs.github.com/assets/cb-65929/images/help/settings/userbar-account-settings.png)
    
3.  In the left sidebar, click **Developer settings**.
    
4.  In the left sidebar, under **Personal access tokens**, click **Fine-grained tokens**.
    
5.  Click **Generate new token**.
    
6.  Under **Token name**, enter a name for the token.
    
7.  Under **Expiration**, select an expiration for the token.
    
8.  Optionally, under **Description**, add a note to describe the purpose of the token.
    
9.  Under **Resource owner**, select a resource owner. The token will only be able to access resources owned by the selected resource owner. Organizations that you are a member of will not appear unless the organization opted in to fine-grained personal access tokens. For more information, see "[Setting a personal access token policy for your organization](https://docs.github.com/en/organizations/managing-programmatic-access-to-your-organization/setting-a-personal-access-token-policy-for-your-organization)."
    
10.  Optionally, if the resource owner is an organization that requires approval for fine-grained personal access tokens, below the resource owner, in the box, enter a justification for the request.
    
11.  Under **Repository access**, select which repositories you want the token to access. You should choose the minimal repository access that meets your needs. Tokens always include read-only access to all public repositories on GitHub.
    
12.  If you selected **Only select repositories** in the previous step, under the **Selected repositories** dropdown, select the repositories that you want the token to access.
    
13.  Under **Permissions**, select which permissions to grant the token. Depending on which resource owner and which repository access you specified, there are repository, organization, and account permissions. You should choose the minimal permissions necessary for your needs. For more information about what permissions are required for each REST API operation, see "[Permissions required for fine-grained personal access tokens](https://docs.github.com/en/rest/overview/permissions-required-for-fine-grained-personal-access-tokens)."
    
14.  Click **Generate token**.
    

If you selected an organization as the resource owner and the organization requires approval for fine-grained personal access tokens, then your token will be marked as `pending` until it is reviewed by an organization administrator. Your token will only be able to read public resources until it is approved. If you are an owner of the organization, your request is automatically approved. For more information, see "[Reviewing and revoking personal access tokens in your organization](https://docs.github.com/en/organizations/managing-programmatic-access-to-your-organization/reviewing-and-revoking-personal-access-tokens-in-your-organization)".

[Creating a personal access token (classic)](#creating-a-personal-access-token-classic)
---------------------------------------------------------------------------------------

**Note**: Organization owners can restrict the access of personal access token (classic) to their organization. If you try to use a personal access token (classic) to access resources in an organization that has disabled personal access token (classic) access, your request will fail with a 403 response. Instead, you must use a GitHub App, OAuth App, or fine-grained personal access token.

**Note**: Your personal access token (classic) can access every repository that you can access. GitHub recommends that you use fine-grained personal access tokens instead, which you can restrict to specific repositories. Fine-grained personal access tokens also enable you to specify fine-grained permissions instead of broad scopes.

1.  [Verify your email address](https://docs.github.com/en/get-started/signing-up-for-github/verifying-your-email-address), if it hasn't been verified yet.
    
2.  In the upper-right corner of any page, click your profile photo, then click **Settings**.
    
    ![](https://docs.github.com/assets/cb-65929/images/help/settings/userbar-account-settings.png)
    
3.  In the left sidebar, click **Developer settings**.
    
4.  In the left sidebar, under **Personal access tokens**, click **Tokens (classic)**.
    
5.  Select **Generate new token**, then click **Generate new token (classic)**.
    
6.  In the "Note" field, give your token a descriptive name.
    
7.  To give your token an expiration, select **Expiration**, then choose a default option or click **Custom** to enter a date.
    
8.  Select the scopes you'd like to grant this token. To use your token to access repositories from the command line, select **repo**. A token with no assigned scopes can only access public information. For more information, see "[Scopes for OAuth Apps](https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/scopes-for-oauth-apps#available-scopes)".
    
9.  Click **Generate token**.
    
10.  Optionally, to copy the new token to your clipboard, click .
    
    ![](https://docs.github.com/assets/cb-17251/images/help/settings/personal_access_tokens.png)
    
11.  To use your token to access resources owned by an organization that uses SAML single sign-on, authorize the token. For more information, see "[Authorizing a personal access token for use with SAML single sign-on](https://docs.github.com/en/enterprise-cloud@latest/authentication/authenticating-with-saml-single-sign-on/authorizing-a-personal-access-token-for-use-with-saml-single-sign-on)" in the GitHub Enterprise Cloud documentation.
    

[Using a personal access token on the command line](#using-a-personal-access-token-on-the-command-line)
-------------------------------------------------------------------------------------------------------

Once you have a token, you can enter it instead of your password when performing Git operations over HTTPS.

For example, on the command line you would enter the following:

```
$ git clone https://github.com/USERNAME/REPO.git
Username: YOUR_USERNAME
Password: YOUR_TOKEN

```

Personal access tokens can only be used for HTTPS Git operations. If your repository uses an SSH remote URL, you will need to [switch the remote from SSH to HTTPS](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories#switching-remote-urls-from-ssh-to-https).

If you are not prompted for your username and password, your credentials may be cached on your computer. You can [update your credentials in the Keychain](https://docs.github.com/en/get-started/getting-started-with-git/updating-credentials-from-the-macos-keychain) to replace your old password with the token.

Instead of manually entering your personal access token for every HTTPS Git operation, you can cache your personal access token with a Git client. Git will temporarily store your credentials in memory until an expiry interval has passed. You can also store the token in a plain text file that Git can read before every request. For more information, see "[Caching your GitHub credentials in Git](https://docs.github.com/en/get-started/getting-started-with-git/caching-your-github-credentials-in-git)."

[Further reading](#further-reading)
-----------------------------------

*   "[About authentication to GitHub](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/about-authentication-to-github)"
*   "[Token expiration and revocation](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/token-expiration-and-revocation)"