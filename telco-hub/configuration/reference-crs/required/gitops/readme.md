# Installation instructions

1. Apply the manifests: `gitopsNS.yaml`, `gitopsOperGroup.yaml`, and `gitopsSubscription.yaml`.

2. Approve the created InstallPlan in the `openshift-gitops` namespace.

3. **[Optional]** Edit `argocd-ssh-known-hosts-cm.yaml` to add SSH known hosts (public keys) for the git repository you will connect.

   > **Important:** The ConfigMap already exists on the hub cluster. If you add your own known hosts, apply the YAML instead of creating it.

4. Depending on how you will connect to your git repository (SSH or HTTPS), modify `ztp-repo.yaml` and fill in the proper parameters and credentials.

5. Edit `ztp-installation/clusters-app.yaml` to set the connection to the git repository that contains the spoke/managed cluster information.

6. Edit `ztp-installation/policies-app.yaml` to set the connection to the git repository that contains the Policies for the spoke/managed clusters.

   > **Notice:** For both (5 and 6), you only need to modify `path`, `repoURL`, and `targetRevision`. For `repoURL`, use the credentials you created previously for HTTPS or SSL access.

7. Apply the patch to install ZTP inside Argo CD:

   ```bash
   oc patch argocd openshift-gitops -n openshift-gitops --type=merge --patch-file ztp-installation/argocd-openshift-gitops-patch.json
   ```

8. Apply the ZTP installation manifests:

   ```bash
   oc apply -k ztp-installation/
   ```
