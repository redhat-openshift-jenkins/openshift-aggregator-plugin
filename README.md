# OpenShift Plugin

## Introduction

This plugin packages other Jenkins plugins that define the Red Hat OpenShift Jenkins distribution.
It is only meant to be used within a container running Jenkins on top of an OpenShift cluster.

## Getting started

1. If you have not done so already, create a Project in OpenShift to deploy your Jenkins instance.

   ```sh
   oc new-project jenkins
   ```

2. In `helm/values.yaml`, update `controller.jenkinsUrl` to match the expected ingress created by
   the `Route`. The default value assumes deployment on OpenShift Local.

3. Apply the additional RBAC that will eventually be used by Jenkins:

   ```sh
   oc apply -f helm/00-rbac-sync-plugin.yaml
   ```

4. Follow the Jenkins [helm chart](https://github.com/jenkinsci/helm-charts) instructions to
   install the chart, using your `values.yaml` file and the `values-*.yaml` files that configure
   each OpenShift plugin:

   ```sh
   helm install jenkins jenkins/jenkins -f helm/values.yaml -f helm/values-login.yaml -f helm/values-client.yaml
   ```

## Issues

TODO

## Contributing

For now, refer to the upstream [CONTRIBUTING](https://github.com/jenkinsci/.github/blob/master/CONTRIBUTING.md) guide.

## LICENSE

Licensed under Apache 2.0, see [LICENSE](LICENSE)

