# Introduction

This is a demo of how Backstage can be used to visualize distributed system architecture.

This demo is using a static file configuration distributed across multiple repositories.

[Core .Net Libraries](https://github.com/gwilczura/dotnet-common)

[Products Domain](https://github.com/gwilczura/demo-domain-products)

[Backend For Frontend](https://github.com/gwilczura/demo-bff)

Those repositories conain code for system presented below:

![System Overview](/resources/system.png)

## Backstage Configuration

Backstage out of the box gives us a model to represent our systems:

[Backstage System Model](https://backstage.io/docs/features/software-catalog/system-model/)

This demo is based on configuration convention presented below.

![Backstage Configuration](/resources/backstage-config.png)

All repositories are public so not additional authentication-related configuration is needed.

Each repository has it's own `backstage` folder with `all.yaml` that points to other `location` files.

# How to Run

## backstage-gw
There is an already set-up backstage application that you can use.

It's named `backstage-gw`.

```
cd backstage-gw
corepack enable
yarn set version 4.4.1
yarn install
```

this gives use yarn 4.4 support and we can use .env.yarn

and then you can do

```
yarn dev
```

## How To Install new Backstage Instance

in main folder

```
nvm use 20.18.1
npm install concurrently
npm install isolated-vm --no-node-snapshot
corepack enable
yarn set version 4.4.1
# for windows
Set-ExecutionPolicy -Scope CurrentUser
npx @backstage/create-app@latest
```

name your app for example `backstage-demo`

new folder will be created named `backstage-demo`


## Accessing private repos in Azure DevOps

If you store your code in private repository you might need to set-up access to it.

Below is example for AzureDevops.

Create a PAT to your repository - in my case AzureDevops Repos

In `backstage-demo` create file

```
# for windows
New-Item .env.yarn -type file
```

inside add

```
AZDO_PAT: blablabla-your-pat-here-blablabla
```

Note: you can add any environmental variable in this file.

In backstage app `app-config.yml` add section

```
integrations:
  azure:
    - host: dev.azure.com
      credentials:
        - organizations:
            - your-org-name
          personalAccessToken: ${AZDO_PAT}
```

In terminal navigate to `backstage-demo` folder and run:
```
yarn dev
```
