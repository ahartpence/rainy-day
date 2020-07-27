This exact command is for the Velero backup filestructure (resources/<k8s_object>/namespaces) and its expecting you to be in the namespaces folder, but could be edited to do whatever, i guess

The meat and potatoes are in the `do` block, but for future reference

```
for i in */*; do jq -M 'del(.metadata.generation)' $i > $i.tmp && mv $i.tmp $i ; done
```

```
for i in */*; do kubectl apply -f $i; done
```
