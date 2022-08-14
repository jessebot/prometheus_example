The exact commands I ran to create this repo:

```bash
# make sure the lock and tar files are ignored going forward
echo "charts/" > .gitignore

# create the chart yaml
helm show chart prometheus-community/kube-prometheus-stack > Chart.yaml

# show the values and based on that, edit up a values file
helm show values prometheus-community/kube-prometheus-stack
vim values.yml
```

Finally we run this to create the additional files we need:
```bash
helm dep update .
```
