## how the repo was set up

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

# Adding the repo via Argo CD
First you'll need to update the [./values.yaml](./values.yaml) host names to be your own host, or don't :P

Then, assuming you have argo CD up and running from the tutorial [here](https://github.com/jessebot/argo_vault_example), you can run:
```bash
argocd repo add https://github.com/jessebot/prometheus_argo_example
```
