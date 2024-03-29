# HwameiStor Kubernetes Helm Charts

[![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/5685/badge)](https://bestpractices.coreinfrastructure.org/projects/5685) [![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/hwameistor)](https://artifacthub.io/packages/search?repo=hwameistor)


This functionality is in alpha and is subject to change. The code is provided as-is with no warranties. Alpha features are not subject to the support SLA of official GA features.

## Usage

### STEP 1: Install HwameiStor

[Helm](https://helm.sh) must be installed to use the charts.
Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

```console
$ git clone https://github.com/hwameistor/helm-charts.git
```

```console
$ cd helm-charts/charts
```

```console
$ helm install hwameistor -n hwameistor --create-namespace --generate-name
```

or:

```console
$ helm repo add hwameistor http://hwameistor.io/helm-charts
```

```console
$ helm install hwameistor/hwameistor -n hwameistor --create-namespace --generate-name
```

You can then run `helm search repo hwameistor` to see the charts.

### STEP 2: Enable HwameiStor On Node

Once the Helm charts was installed. You should enable HwameiStor on specific nodes as follows:

```console
$ kubectl label node <node-name> "lvm.hwameistor.io/enable=true"
```

### STEP 3: Claim Disk By Type On Node

Then claim disk for your local-storage by apply LocalDiskClaim CR:

```console
cat > ./local-disk-claim.yaml <<- EOF
apiVersion: hwameistor.io/v1alpha1
kind: LocalDiskClaim
metadata:
  name: <anyname>
  namespace: hwameistor
spec:
  nodeName: <node-name>
  description:
    diskType: <HDD or SSD or NVMe>
EOF
```

```console
$ kubectl apply -f ./local-disk-claim.yaml
```

**Congratulations! HwameiStor is now deployed on your cluster.**

## Next Step

To deploy stateful applications, please see [Deploy Applications With HwameiStor](https://github.com/hwameistor/local-storage#step-3-create-storageclass)

More infomation [HwameiStor](https://hwameistor.io)

## Contributing

We'd love to have you contribute!

## License

<!-- Keep full URL links to repo files because this README syncs from main to gh-pages.  -->
[Apache 2.0 License](https://github.com/hwameistor/helm-charts/blob/helm/LICENSE).

