<div align="center">
  <img src="https://github-readme-stats.vercel.app/api?hide_title=false&hide_rank=false&show_icons=true&include_all_commits=true&count_private=true&disable_animations=false&theme=dracula&locale=pt-br&hide_border=false&username=coelhos-gabi" height="150" alt="stats graph"  />
  <img src="https://github-readme-stats.vercel.app/api/top-langs?locale=pt-br&hide_title=false&layout=compact&card_width=320&langs_count=5&theme=dracula&hide_border=false&username=coelhos-gabi" height="150" alt="languages graph"  />
</div>

###
<img href="https://github.com/coelhos-gabi/coelhos-gabi/blob/output/snake.svg" alt="Snake animation" />

###

name: Generate snake animation

on:
  schedule: # execute every 12 hours
    - cron: "* */12 * * *"

  workflow_dispatch:

  push:
    branches:
    - master

  jobs:
    generate:
      runs-on: ubuntu-latest

      steps:
        - name: generate snake.svg
          uses: Platane/snk@master
          with:
            github_user_name: ${{ github.repository_owner }}
            outputs: dist/snake.svg


        - name: push snake.svg to the output branch
          uses: crazy-max/ghaction-github-pages@v2.6.0
          with:
            target_branch: output
            build_dir: dist
          env:
            GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
