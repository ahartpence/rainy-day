# 'Scale Down' a daemonset
`kubectl -n monitoring patch daemonset datadog-agent -p '{"spec": {"template": {"spec": {"nodeSelector": {"non-existing": "true"}}}}}'`

# 'Scale Up' a daemonset
`kubectl -n default patch daemonset datadog-agent --type json -p='[{"op": "remove", "path": "/spec/template/spec/nodeSelector/non-existing"}]'`

# Grab all deploys in the current namespace with more than 1 replica
``for i in `kubectl get deploy | awk '{print $1}'`; do if ((`kubectl get deploy ${i} -o jsonpath='{.spec.replicas}'` > 0)); then echo ${i}; fi;done``

# Delete all evicted pods
`kubectl get pod | grep Evicted | awk '{print $1}' | xargs kubectl delete pod `

# Decode certain field from secret
`kubectl get secret datadog-integration-files -n monitoring -o json | jq -r '.data."http_check.yaml"' | base64 --decode`

# Get cert from secret
`kubectl get secret svc-golf-ing-certs -o json | jq -r '.data."tls.crt"' | base64 --decode | openssl x509 -text -noout`

# Label all nodes a certain way

``for i in `kubectl get node | grep dedicated | awk '{print $1}'`; do kubectl label node $i kenna.io/data-dedicated=true; done``

``for i in `kubectl get node | grep dedicated | awk '{print $1}'`; do kubectl label node $i kenna.io/data-dedicated-size=small; done``

# Taint all nodes a certain way
``for i in `kubectl get node | grep dedicated | awk '{print $1}'`; do kubectl taint node $i kenna.io/data-dedicated=true:NoSchedule-; done``

``for i in `kubectl get node | grep dedicated | awk '{print $1}'`; do kubectl taint node $i kenna.io/data-dedicated-size=small:NoSchedule-; done``