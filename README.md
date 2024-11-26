### Sidecar test (buildpack vs. cnb)

#### Buildpack app

```
cf push

curl $(cf curl "/v3/apps/$(cf app sidecar-test --guid)/routes" | jq -r ".resources[].url")

=> app is running

cf logs sidecar-test --recent | grep -o '\[.*/SIDECAR/.*'

=> [APP/PROC/WEB/SIDECAR/SIDECAR/0] OUT sidecar is running
```

#### CNB app

```
cf push -f manifest-cnb.yml

=> App does not start; logs indicate that the sidecar process also starts the 'web' process defined in the Procfile.

=> [APP/PROC/WEB/SIDECAR/SIDECAR/0] OUT * Serving Flask app 'app'
=> [APP/PROC/WEB/SIDECAR/SIDECAR/0] ERR Address already in use
```
