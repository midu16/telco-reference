# Installation instructions

1. Create the manifests: `acmNS.yaml`, `acmOperGroup.yaml`, and `acmSubscription.yaml`.

2. Approve the created InstallPlan in the `open-cluster-management` namespace.

3. Create the `acmMCH.yaml`.

4. Approve the created InstallPlan in the `multicluster-engine` namespace.

5. Apply the `acmProvisioning.yaml`.

6. Create the `acmAgentServiceConfig.yaml`.

7. The `multicluster-engine` enables the `cluster-proxy-addon` feature by default. To disable it, apply the following patch:

   ```bash
   oc patch multiclusterengines.multicluster.openshift.io multiclusterengine --type=merge --patch-file ./disable-cluster-proxy-addon.json
   ```

8. Create the `observatilityNS.yaml`.

9. Enable MultiClusterHub Observability. Check the [pre-requirements](./pre-requeriments.md) first.

10. Create the `observabilityMCO.yaml`.
