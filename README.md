# Docker repack template

Simply place a `Dockerfile` at the root of the repo e.g.:

```
FROM debian:bookworm-20240211

RUN apt-get update && apt-get install -y \
    fortune \
    cowsay \
    && rm -rf /var/lib/apt/lists/*
RUN echo '/usr/games/fortune | /usr/games/cowsay && echo -e "\n"' >> /etc/bash.bashrc
```

Is important **not** to use a `latest`, `stable` or any other tag that is not regulary updated. For debian these are the images with a date inside the tag.
This will autamtically build and release new debian images with a `cowsay` message of the day under the following name: `{DOCKER_HUB_USERNAME}/{REPO_NAME}:{BASE_IMAGE_TAG}` e.g.: `mietzen/debian-cowsay:bookworm-20240211` (The latest image also gets the `latest` tag)

Cowsay example: [https://github.com/mietzen/debian-cowsay](https://github.com/mietzen/debian-cowsay)

The worklow will build all platform listed in `platforms.json` and push them as multi-arch image. 

For the worklfow to run you need to create a GitHub-App to generate tokens, follow:

[https://github.com/actions/create-github-app-token](https://github.com/actions/create-github-app-token?tab=readme-ov-file#usage)

and add the following secrets as repository secrets in Actions **and** Dependabot:

- APP_ID
- APP_PRIVATE_KEY
