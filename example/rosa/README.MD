# Install crossplane ocp
helm install crossplane --namespace crossplane-system crossplane-stable/crossplane --set securityContextCrossplane.runAsUser=null --set securityContextCrossplane.runAsGroup=null --set securityContextRBACManager.runAsUser=null --set securityContextRBACManager.runAsGroup=null

## Install function 
oc apply -f ./functions.yaml

## update security context run as user (need to check template and update there)
oc edit deployment/<deployment-name>
update all references from 2000 to 1000790000

## create the definition
oc apply -f ./definition.yaml

## create xr
oc apply -f ./xr.yaml

## create the composition
oc apply -f ./composition.yaml

## verify execution
crossplane beta trace rosashell.openshift.io/rosa