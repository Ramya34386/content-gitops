![la logo](https://user-images.githubusercontent.com/42839573/67322755-818e9400-f4df-11e9-97c1-388bf357353d.png)

## Hands-On GitOps

### This document contains a number of commands that may prove useful to the student.

This is the command to install fluxctl on an Ubuntu server.

```
$ sudo snap install fluxctl
```

This is the command to check the kubernetes cluster that is staged.

```
$ kubctl get nodes
```

This is the command to create a namespace called flux.

```
$ kubectl create namespace flux
```

The following is the fluxctl install command used to deploy the flux pods to a cluster within the flux namespace. This is the example used in the "Installing with GitHub Lab".

```
fluxctl install \
--git-user=${GHUSER} \
--git-email=${GHUSER}@users.noreply.github.com \
--git-url=git@github.com:${GHUSER}/content-gitops \
--git-path=namespaces,workloads \
--namespace=flux | kubectl apply -f -
```
The version of this command used in the "Installing with GitLab Lab" is:

```
    $ export GLUSER=[your GitLab username]
```    
Then input the command to run flux:
```
    $ fluxctl install \
    --git-user=${GLUSER} \
    --git-email=${GLUSER}@gmail.com \
    --git-url=git@gitlab.com:${GLUSER}/flux-sample \
    --git-path=namespaces,workloads \
    --namespace=flux | kubectl apply -f -
```

This is the command to check the status of the flux deployment.

```
kubectl -n flux rollout status deployment/flux
```

This is the command to interogate the RSA Key created by the flux install.

```
$ fluxctl identity --k8s-fwd-ns flux
```

This is the command to cause flux to sync with the repo.

```
$ fluxctl sync --k8s-fwd-ns flux
```

This is the command to set an environment variable to tell fluxctl the namespace that flux is running in.

```
$ export FLUX_FORWARD_NAMESPACE=flux
```

This is the command to list flux workloads

```
$ fluxctl list-workloads
```
and...
```
$ fluxctl list-workloads --all-namespaces
```
and...
```
$ fluxctl -n lasample list-workloads
```

This is the command to list images running as flux workloads
```
$ fluxctl list-images
```
and... (specify namespace and deployment name, such as lasample and hello)
```
$ fluxctl list-images --workload lasample:deployment/hello
```

This is the command to get pods.
```
$ kubectl -n lasample get pods
```

This is the command to describe a specific pod such as hello-75d7f49d9b-t8bpr
```
$ kubectl -n lasample describe pod/hello-75d7f49d9b-t8bpr
```