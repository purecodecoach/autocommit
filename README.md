# auto-commit

🌳 Making green your Github stats, powered by [Github Actions](https://github.com/features/actions)

[![Auto commit](https://github.com/expressd3v/autocommit/workflows/Auto%20commit/badge.svg)](https://github.com/expressd3v/autocommit/actions?query=workflow%3A%22Auto+commit%22)

Worflow

```
name: Auto commit

on:

  push:
    branches:
      - master
      
  schedule:
  - cron: "<CRON>" // ex: "0 7,9,11 * * 1,3" refer https://crontab.guru/#0_7,9,11_*_*_1,3

jobs:
  auto_commit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3      
        with:
         persist-credentials: false
         fetch-depth: 0

      - name: Modify last update
        run: |
          d=`date '+%Y-%m-%dT%H:%M:%SZ'`
          echo $d > LAST_UPDATED
          
      - name: Commit changes
        run: |
          git config --local user.email "<YOUR GIT EMAIL>"
          git config --local user.name "<YOUR GIT USERNAME>"
          git add -A
          
          arr[0]="chore(bot): 😂 auto commit"
          arr[1]="chore(bot): 😱 auto commit"
          arr[2]="chore(bot): 👿 auto commit"
          arr[3]="chore(bot): 💩 auto commit"
          arr[4]="chore(bot): 🙏 auto commit"
          arr[5]="chore(bot): 🙈 auto commit"
          arr[6]="chore(bot): 🐐 auto commit"
          arr[7]="chore(bot): 🤖 auto commit"
          arr[8]="chore(bot): 🟩 auto commit"
          arr[9]="chore(bot): 👻 auto commit"
          
          rand=$[$RANDOM % ${#arr[@]}]
          
          git commit -m "${arr[$rand]}"
          
      - name: GitHub Push
        uses: ad-m/github-push-action@v0.6.0
        with:
          directory: "."
          branch: "master"
          github_token: ${{ secrets.GITHUB_TOKEN }}
```


## Make it your own

- Create your own repo with click "**Use this template**" button (forked repo will not work)

Or just do in the manual way:

- Create your own repo
- Copy file `.github/workflows/autocommit.yml` and `LAST_UPDATED` to your repo
- Change the `email` and `name` information on file [autocommit.yml, line 29 and 30](https://github.com/expressd3v/autocommit/blob/master/.github/workflows/autocommit.yml#L29)
- Change the scheduling time on file [autocommit.yml, line 10](https://github.com/expressd3v/autocommit/blob/master/.github/workflows/autocommit.yml#L10). You can use [crontab.guru](https://crontab.guru/) if you are not familiar with the cron schedule string. For first time, you can try to run it in every hour with string `1 * * * *` .
- You should update repository setting `Setting -> Actions -> General -> Workflow permissions -> Reac and Write Permission`
- Consider to support me, at least click the 🌟 button


© 2020 Crafted by [Nicholi Jin](https://nicholijin.com/)
