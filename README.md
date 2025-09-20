name: Generate Pac-Man Contribution Graph

on:
  schedule:
    - cron: "0 0 * * *" # runs daily at midnight
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Generate Pac-Man Contribution Graph
        uses: yoshi389111/github-profile-3d-contrib@0.7.1
        with:
          user_name: zeyadlotfy
          theme: pacman

      - name: Commit and Push
        run: |
          git config --global user.name "github-actions[bot]"
          git config --global user.email "41898282+github-actions[bot]@users.noreply.github.com"
          git add output/
          git commit -m "Update Pac-Man contribution graph" || echo "No changes to commit"
          git push
