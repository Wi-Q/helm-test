# Helm testing

## Option 1: Use Helm dependency to have microservice's Chart extend a base application Chart

Files for this option are stored within the 'several-applications-extend-base' directory and are just an example.

Within this folder there are two Helm Charts; 'common-php-app' and 'epos'. The 'common-php-app' is where all of the base configuration will live for a php application. For the purposes of this demonstration there is only a deployment.yaml file for the service (the same pattern could be used for each other k8s config).

The 'epos' Chart uses the 'common-php-app' Chart as a dependency therefore the 'epos' Chart has access to all of the files within the 'common-php-app' Chart. As this is the case, the templates in the 'epos' Chart can call the base php Chart's version of the file, as seen in `several-applications-extend-base/epos/templates/deployment.yaml`. A benefit to this is that if a service doesn't require ingress, for example, then this file can just be left out of the Chart or if it ends up requiring something completely custom then it can be added to the extended Chart.

To make changes to the extended Chart you can do so by editing it's directory.

To make changes to the base configuration you would need to:
- Edit the files in the 'common-php-app' Chart.
- Run `helm dependency upgrade` in the epos Chart.

You can test the rendering by running:

`cd several-applications-extend-base/epos`
`helm template ./ --debug`

## Option 2: Use a single Helm application and pass in values

Files for this option are stored within the 'single-application-with-application-values' and again, just an example.

I feel that this solution is a lot simpler overall with less files, but you don't have a clear separation of the wi-Q services. This would also mean putting a lot of context into the values.yaml files and having the templates have conditional rendering.

To test the templates you can run:

`cd php-application`
and then any of the following:
`helm template ./ --debug -f ../values/api/values.yaml`
`helm template ./ --debug -f ../values/epos/values.yaml`
`helm template ./ --debug -f ../values/payments/values.yaml`
