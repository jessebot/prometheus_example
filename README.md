The exact commands I ran to create this repo:

```bash
# Create the directory to house everything
mkdir -p charts/prometheus

# make sure the lock and tar files are ignored going forward
echo "charts/" > charts/promtheus/.gitignore

# create the chart yaml
helm show chart prometheus-community/kube-prometheus-stack > charts/prometheus/Chart.yaml

# show the values and based on that, edit up a values file
helm show values prometheus-community/kube-prometheus-stack
vim charts/promtheus/values.yml
```

Finally we run this to create the additional files we need:
```bash
helm dep update charts/prometheus/
```
