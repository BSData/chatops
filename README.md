# chatops

Infrastructure supporting ChatOps across BSData repos.

To use the chatops commands in issue comments, add this workflow to a BSData repository:

```yml
# For details and description, see https://github.com/BSData/chatops
name: ChatOps
on:
  issue_comment:
    types: [created]
jobs:
  dispatch:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout ChatOps repo
        uses: actions/checkout@v2
        with:
          repository: BSData/chatops
          path: chatops
      - name: /command dispatch
        uses: peter-evans/slash-command-dispatch@v1
        with:
          token: ${{ secrets.SLASH_COMMAND_DISPATCH_TOKEN }}
          config-from-file: chatops/commands.json
```
