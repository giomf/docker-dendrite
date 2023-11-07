# docker-service


## ctl.sh
The ctl.sh script provides commands that are useful to control the services
### Usage
```
$ ./ctl.sh help
Control script for docker-compose services

Usage: ctl.sh <command>

Commands:
        start           Starts all services
        stop            Stops all services
        restart         Restart all services
        reset           Stops and Starts all services
        logs            Shows the docker logs
        status          Shows the services status
        init            Initializes the volumes and copies configuration files to the volumes.
                        This is only needed the first time!
        help            Shows this help page
```
### Init behavior

The behavior of the *init* command varies from service to service. This behavior must be adjusted in *ctl.sh* depending on the service. Otherwise, an error message appears when executing the init command. The use case for initializing is to create the volumes and copy configuration files from etc into them so that they can be edited afterwards.

## Service configuration values that need to be adjusted 
After executing the *init* command, the configuration files must be adjusted in most cases. This should only happen in the volumes folder and not in the etc folder. Otherwise, sensitive data may be pushed upstream.  
The following table gives an overview of which files must be adjusted.

| Value   | File    |
| ------- | ------- |
| EXAMPLE | EXAMPLE |

## Versioning of services and domain name settings
The versioning of the services as well as the domain name settings are done via an *.env* file which is automatically read by docker-compose. For this, the *env.example* should be copied and adapted. It should be noted that no secrets should end up in the *.env*.

## Environment variables
Environment variables are created via a service specific file in the *env* folder. They do not contain any secrets and can therefore be pushed upstream.

## Secrets
Secrets should be created in a file that contains only the secrets for the corresponding service
and grouped in the *secrets* folder. An example for this is *service.secrets.example*. Please note that the file permissions should be as restrictive as possible.

## Getting updates from template repo
```
git remote add template git@github.com:Giom-fm/docker-service.git
git pull template main --allow-unrelated-histories
```
