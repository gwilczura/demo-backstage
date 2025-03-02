# Introduction

This is a demo of how Backstage can be used to visualize distributed system architecture.

This demo is using a static file configuration distributed across multiple repositories.

[Core .Net Libraries](https://github.com/gwilczura/dotnet-common)

# How to Run

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

# How To Install new Backstage Instance

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

name your app for example backstage-demo

new folder will be created named `backstage-demo`


# Accessing repos in Azure DevOps

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
