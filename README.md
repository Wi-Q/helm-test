# Helm testing

## Option 1: Use Helm dependency to have microservices extend a base application

Files for this option are stored within the 'several-applications-extend-base' directory and are just an example.

Within this folder there are two Helm Charts; 'common-php-app' and 'epos'. The 'common-php-app' is where all of the base configuration will live for a php application. For the purposes of this demonstration there is only a deployment.yaml file for the service, the same pattern would be used for each other k8s config.

The 'epos' application uses 'common-php-app' as a dependency, so the 'epos' application has access to all of the files within the 'common-php-app' application. As this is the case, the templates in the 'epos' application can call the base php application's version of the file, as seen in `several-applications-extend-base/epos/templates/deployment.yaml`. A benefit to this is that if a service doesn't require ingress, for example, then this file can just be left out of the application.

## Option 2: Use a single Helm application and pass in values

Files for this option are stored within the 'single-application-with-application-values'
