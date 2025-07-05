# Deploy Blazium Game Action

Reusable Action that deploys a Blazium game. This action deploys a game already built using [blazium-engine/export-blazium-game](https://github.com/blazium-engine/export-blazium-game). The resulting build needs to be uploaded as an artifact.

## Usage

- Docker Deploy:

```yml
deploy-docker:
uses: blazium-engine/deploy-blazium-game/.github/workflows/deploy-docker.yml@master
with:
    artifact-name: Web-web
    docker-registry: registry.digitalocean.com
    registry-path: org-name/image-name
secrets:
    docker-username: username
    docker-token: password
```
