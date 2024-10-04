# OpenShift Plugin

## Introduction

This plugin packages other Jenkins plugins that define the Red Hat OpenShift Jenkins distribution.
It is only meant to be used within a container running Jenkins on top of an OpenShift cluster.

## Getting started

1. Build the container image using your container engine of choice, and push it to a container
   registry of your choice. `podman` and `quay.io` are used as examples below:

   ```sh
   podman build -t quay.io/<your-username>/openshift-jenkins:latest -f .konflux/Containerfile .
   podman push quay.io/<your-username>/openshift-jenkins:latest
   ```

2. If you have not done so already, create a Project in OpenShift to deploy your Jenkins instance.

   ```
   oc new-project jenkins
   ```

3. In `helm/values.yaml`, make the following changes:

   1. Update `controller.image` to point to the image you built above.
   2. Update `controller.jenkinsUrl` to match the expected ingress created by the `Route`. The
      default value here assumes deployment on OpenShift Local.

4. Apply the additional RBAC that will eventually be used by Jenkins:

   ```
   oc apply -f helm/00-rbac-sync-plugin.yaml
   ```

5. Follow the Jenkins [helm chart](https://github.com/jenkinsci/helm-charts) instructions to
   install the chart, using your `values.yaml` file

   ```sh
   helm install jenkins jenkins/jenkins -f helm/values.yaml

## Issues

TODO

## Contributing

For now, refer to the upstream [CONTRIBUTING](https://github.com/jenkinsci/.github/blob/master/CONTRIBUTING.md) guide.

## LICENSE

Licensed under Apache 2.0, see [LICENSE](LICENSE)

