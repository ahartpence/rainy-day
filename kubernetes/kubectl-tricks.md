# 'Scale Down' a daemonset
`kubectl -n monitoring patch daemonset datadog-agent -p '{"spec": {"template": {"spec": {"nodeSelector": {"non-existing": "true"}}}}}'`

# 'Scale Up' a daemonset
`kubectl -n default patch daemonset datadog-agent --type json -p='[{"op": "remove", "path": "/spec/template/spec/nodeSelector/non-existing"}]'`

# Grab all deploys in the current namespace with more than 1 replica
`for i in `kubectl get deploy | awk '{print $1}'`; do if ((`kubectl get deploy ${i} -o jsonpath='{.spec.replicas}'` > 0)); then echo ${i}; fi;done`

# Delete all evicted pods
`kubectl get pod | grep Evicted | awk '{print $1}' | xargs kubectl delete pod `
