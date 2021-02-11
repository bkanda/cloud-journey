# Restart Deployments

This helm chart is to schedule a CronJob that will restart the deployments by the period defined in cron expression.
The CronJob executes ```kubectl rollout deploy/<DEPLOYMENT_NAME>```
Rollouts create new ReplicaSets, and wait for them to be up, before killing off old pods, and rerouting the traffic. Service will continue uninterrupted. That way if something goes wrong, the old pods will not be down or removed.

We can specify multiple deployments in the `values.yaml`, it will create a separate CronJob for each deployment. We can verify the job run and logs using following commands.

```bash
kubectl get cronjob
kubectl get job
kubectl logs $pods
```

# Install

```bash

# Using helm 3.0
helm3 install scheduled-deployment-restart \
    ./util/helm/scheduled-deployment-restart \
    --values=./util/helm/scheduled-deployment-restart/values/values_dev.yaml \
    --debug
```

# Uninstall

```bash
# Using helm 3.0
helm3 uninstall scheduled-deployment-restart
```