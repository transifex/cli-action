## Github Action for Transifex CLI

> [Transifex CLI homepage](https://github.com/transifex/cli)

Integrate the Transifex CLI within a Github action. Usage:

1. Make sure your repository has a Transifex CLI configuration. If not, set it
   up with:

   ```sh
   tx init
   tx add  # Complete the interactive wizard
   git add .tx
   git commit -m "Add Transifex CLI configuration"
   ```

2. Add a Transifex API token to your repository as a repository secret

3. Use this in your Github action workflow:

   ```yaml
   on: [push]
   jobs:
     Push-source-file:
       runs-on: ubuntu-latest
       steps:
         - name: Checkout
           uses: actions/checkout@v2
         - name: Push source file using transifex client
           uses: transifex/cli-action@v2
           with:
             token: ${{ secrets.TX_TOKEN }}
   ```

### Action options

**`token` (required)**: The Transifex API token to use for pushing

**`version` (default: latest)**: The Transifex CLI version to use

**`args` (default: push)**: Which arguments to pass to the tx command. By
default, the CLI will push the source files of all resources configured in
`.tx/config`.
