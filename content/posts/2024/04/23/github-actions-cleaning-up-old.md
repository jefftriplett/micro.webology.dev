---
title: "🐳 GitHub Actions Cleaning up old Docker container images"
date: "2024-04-23T22:46:16-05:00"
url: "/2024/04/23/github-actions-cleaning-up-old/"
type: "post"
feed_id: "http://webology.micro.blog/2024/04/23/github-actions-cleaning-up-old/"
---

If you use GitHub Actions to build and deploy Docker container images, you quickly learn that deleting old container images you no longer need is a huge pain. I don't know why GitHub doesn't make this easier, but they have a reusable workflow we can use to help prune and clean up old container images. 

The [delete-package-versions](https://github.com/actions/delete-package-versions) will let you set a number to only keep the last x-known good images, with some other valuable options like deleting untagged container images. 

I prefer to write one [reusable workflow](https://docs.github.com/en/actions/using-workflows/reusing-workflows), which I can call from my standard CI build and deploy pipeline, along with a workflow_dispatch action we can call whenever we want. 

This workflow is a mouthful but wraps the `delete-package-versions` action and gives us a few configurable options to pass. Having a default value on `min_versions_to_keep` is nice because it is a default when calling this workflow from other locations. 

```yml
# .github/workflows/delete-container-versions.yml
name: Delete Untagged Container Versions

on:
  workflow_call:
    inputs:
      package_name:
        required: true
        type: string
      package_type:
        required: true
        type: string
      min_versions_to_keep:
        required: false
        type: number
        default: 30

jobs:
  delete_versions:
    runs-on: ubuntu-latest
    steps:
      - name: Delete all untagged container versions
        uses: actions/delete-package-versions@v5
        with:
          delete-only-untagged-versions: 'false'
          min-versions-to-keep: ${{ inputs.min_versions_to_keep }}
          package-name: ${{ inputs.package_name }}
          package-type: ${{ inputs.package_type }}
```

Our `cleanup.yml` is set up as a workflow_dispatch, allowing us to call our `delete-container-versions` job whenever we want. 

```yml
# .github/workflows/cleanup.yml
name: Delete Untagged Container Versions

on:
  workflow_dispatch:

jobs:
  delete-container-versions:
    uses: .github/workflows/delete-container-versions.yml
    with:
      package_name: 'your-docker-container-package-name'
      package_type: 'container'
```

I'm embarrassed to admit I had several repos with over 500 or more Docker container images. Deleting the oldest Docker images took less than a minute once I had the button set up. 

After successfully building and pushing a new container image to our registry, I also include this job as the last step. This will future-proof our build and deployment workflow so that it never gets out of control again. 

Also, I can count the number of times that I have needed to revert to one image on one hand and have never reverted to an image more than that. So saving the last 10, 20, or 30 images is peace of mind.
