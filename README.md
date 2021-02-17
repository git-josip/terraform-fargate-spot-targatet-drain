# terraform-fargate-spot-targatet-drain

Terraform scripts for deploying lambda for de-registering load balancer targets on FargateSpot interruption.

## How to

### Overview

All commands are defined in `MakeFile`.
You do not need to have installed `go` or `terraform` environments on your computer.
All commands are executed in inside docker image which needs to be build at the beginning.  

### Init - Build Docker image

At the very beginning we need to build image which will be used laetr for other commands.

Command: `make build` will build local `git-josip/aws-lambda-deregister-targets-fargate-spot` image. In that image we initialize terraform with our terraform configuration. 
Check `DOckerFile` for details.

### Source code compile

To compile your source code, run `make compile`. 
With this command executes `go build` command in docker Go env.
After this command we have new `build/` folder created containing compiled program.
All terrafrom tasks are depending on this one so we do not execute it when runnign `plan` or `apply`

### Terraform commands

`plan`, `apply` and `destroy` are supported terraform commands.
WIth `plan` we will just get output what resources will be created.

In order to run these commands we need to pass AWS acces,secret and region params to make. 

- `make awsDefaultRegion=eu-central-1  awsAccessKey=accessxxx   awsSecretKey=secretxxx plan`
- `make awsDefaultRegion=eu-central-1  awsAccessKey=accessxxx   awsSecretKey=secretxxx apply`
- `make awsDefaultRegion=eu-central-1  awsAccessKey=accessxxx   awsSecretKey=secretxxx destroy`