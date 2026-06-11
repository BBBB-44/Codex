---
---

#Next.js + infisical

## Install Docker

Install:
Docker Desktop

## Install infisical
```
npm install -g @infisical/cli
```

## Login infisical
```
infisical login
```

## Initialize project:
```
infisical init
```

## Add Dev Container
```
.devcontainer/devcontainer.json
```

## devcontainer.json
```json
{
  "name": "nextjs-infisical-dev",
  "image": "node:22",
  "workspaceFolder": "/app",
  "mounts": [
    "source=${localWorkspaceFolder},target=/app,type=bind"
  ],
  "forwardPorts": [3000],
  "remoteUser": "node",
  "postCreateCommand": "npm install"
"postStartCommand": "infisical run -- npm run dev"
}
```

## Open project in Cursor (inside container)
```
Ctrl + Shift + P → Dev Containers: Reopen in Container
```


## Run Next.js inside container with infisical
```
infisical run -- npm run dev
```

## Open browser
```
http://localhost:3000
```


# ASP.NET project

## Add Dev Container
```
.devcontainer/devcontainer.json
```

## devcontainer.json
```json
{
  "name": "aspnet-dev",
  "image": "mcr.microsoft.com/dotnet/sdk:8.0",
  "workspaceFolder": "/workspace",
  "mounts": [
    "source=${localWorkspaceFolder},target=/workspace,type=bind"
  ],
  "forwardPorts": [3000],
  "remoteUser": "root",
  "postCreateCommand": "dotnet restore"
"postStartCommand": "dotnet watch run --urls http://0.0.0.0:3000"
}
```

## Open project in Cursor (inside container)
```
Ctrl + Shift + P → Dev Containers: Reopen in Container
```

## Run ASP.NET inside container

Inside Cursor terminal:
```
dotnet run --urls http://0.0.0.0:3000
```

## Open browser
```
http://localhost:3000
```
