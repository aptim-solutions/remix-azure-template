# Azure Deployment Template

The below is based on the [https://github.com/aaronpowell/azure-remix-stack](azure remix stack)
We are constantly updating this template.

## Additional Files

The below files are in addition to the original remix template files

- `.dockerignore`
- `Dockerfile`
- `azure.yaml`
- `infra/`

## Deployment Preparation

### .dockerignore

There are no changes required to this file

### Dockerfile

1. May need to update the line with the version of node (may need version 20). The list of images can be found [here](https://hub.docker.com/_/node/)
2. If using prisma then uncomment the lines that install and run prisma

TODO:

- compare this to the `Dockerfile` in the epic-web template

### azure.yaml

1. update the name of the app

### infra/

1. main.bicep
   TODO: need to understand this file more as there are settings that could be useful

2. /core/\*
   TODO: need to understand these files. There doesn't appear to be anything that requires change (so far!)

3. /app/web.bicep

- update the environment variables in this file
  TODO: how do we get this file to look at the environment variables from either .env or from the environment itself? Doesn't feel right to have to hard-code into this file.

## Deployment Steps

1. `azd auth login` to make sure that you're logged in to the correct Azure environment
2. `azd init`
   1. This creates a folder with files in `.azure`. Can we update the environment variables here?
3. `azd provision`
   - This will then provision the resources. You'll be asked which subscription, which region etc.
4. Make sure that Docker is running on your machine
5. `azd deploy`
   - This will then (hopefully) show the url that has been deployed
   - a custom domain can then be pointed to the url

TODO:

- how do we change environment variables without having to provision again so that the custom domain doesn't get removed
- understand all the various settings that have been used and see how we update this
- how do we scale the settings when we need to (or reduce when we want a testing environment)
