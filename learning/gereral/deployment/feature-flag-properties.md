## Future flag changes 

You have to trigger a deployment in order to get the new feature flag values. (applies for all our services)
So create a PR in the config repo, changing the "deploymentControl" value in the environment specific value...yaml file

_Feature flags are not dynamically read._


Changing a feature flag value itself is not considered a change which would trigger a redeployment. There are only 4 ways to trigger a redeployment:
version change in the environment specific yaml file
deploymentControl change in the environment specific yaml file
a change in the shared generic values.yaml file (careful: all environments would be redeployed)
changes to the configmap.yaml  (careful: all environments would be redeployed)