# WIFORCE public landing page

The content of the public landing page for the organisation [WIFORCE](https://github.com/WIFORCE) is in `profile/README.md`

## How to setup the GH actions

Reference info is available online on [GitHub actions](https://docs.github.com/en/actions)

1. Create a `.github/workflows` directory
2. Create a `yml` file for defining your workflow
3. Some step will require to use an authentication key. See the [section](#defining-a-secret) and [links](#links) below for the relevant documentation.
4. Enabling the GitHub Actions extension in VSCode is really useful for handling [actions](#triggering-an-action)

## Triggering an action

There are several triggers, right now, this one is set to manual (`workflow_dispatch:`) but it should ultimately be `schedule` (as there is no trigger for the addition of repos).

A manual trigger with the VSCode GitHub Actions extension is very easy, go to the icon for GH Actions in the left panel, refresh to see your available workflow, trigger the `play` icon, then click the `globe` to see the details online (the results will otherwise be displayed in the GH Actions side view).

## Defining a secret

This is a bit "cumbersome" for private organizations, but anyone as admin in an org can do it. With the free GitHub plan, secret can only be used with public repositories. Not a big issue, just some additional work-arounds.

1. As your GH user, go to `Settings`, then in the left menu, all the way down to `Developer Settings`.
2. Select `Personal Access Tokens` (PAT). Best is to create a `Fine-grained tokens` for added permission control.
3. Click generate a new token. For the purpose of actions at the organisational level, chose the organisation as owner, choose to give access to all repositories in the organisation and limit the permissions to `actions` and `metadata`. Save your PAT (copy-paste), as you will not be able to see its content past this step. Make sure to let the token expire for security reasons.
4. Go to your organization, `Settings`, then select `Secrets and variables` and `Actions`. Then add a `New organization secret` (any admin in the org can do that). Give it a memorable name and paste your PAT.
5. If all goes well, you can now use your memorable named secret as an env in your workflow, e.g. 
    ```yml
        env:
          GH_TOKEN: ${{ secrets.MEMORABLE_SECRET }}
    ```
6. And in your org `Settings`, you should see in the `Third Party Access` `Active tokens` section your newly created PAT.

## Links

* [Authenticate with GitHub Token](https://docs.github.com/en/actions/tutorials/authenticate-with-github_token)
* [Creating secrets for an organization](https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/use-secrets#creating-secrets-for-an-organization)
