# How to automate Release using GitHub Action as well.

```releases.yaml
name: Releases
on:
  workflow_dispatch:
    inputs:
      version:
        type: string
        required: true
        
jobs:
  release:
    name: Manual Version Up
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/create-release@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          tag_name: ${{ github.event.inputs.version }}
          release_name: ${{ github.event.inputs.version }}
          draft: false
          prerelease: false
```

## ❌ Resource not accessible by integration

The problem was solved by changing the `Settings > Actions > General > Workflow permissions` for the repository in question from `Read repository contents permission` to `Read and write permissions`

<img width="1193" alt="image" src="https://user-images.githubusercontent.com/28350464/223349671-07017ede-5131-47e8-ad0d-7a8f092ec696.png">
