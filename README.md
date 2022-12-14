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
First you'll need to update the [./values.yaml](./values.yaml) host names to be your own host, or don't :shrug:

Then, assuming you have argo CD up and running from the tutorial [here](https://github.com/jessebot/argo-example), you can run:
```bash
argocd repo add https://github.com/jessebot/prometheus_example
```

Is the repo you have actually private? Try this (only with your private repo and not mine :P)
```bash
argocd repo add git@github.com:jessebot/prometheus_example.git --ssh-private-key-path ~/.ssh/id_rsa
```

# Creating an Argo CD app from this repo
```bash
argocd app create prometheus --repo git@github.com:jessebot/prometheus_example.git --dest-namespace monitoring --dest-server https://kubernetes.default.svc --path . --sync-policy auto --sync-option CreateNamespace=true
```
