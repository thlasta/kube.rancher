# kube.rancher

echo "# kube.ipspeed.telefraf" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:thlasta/kube.rancher.git
git push -u origin main

Repo clonen
git clone git@github.com:thlasta/kube.rancher.git

# Repo auschecken/holen
git pull git@github.com:thlasta/kube.rancher.git

# Bei Änderungen:
git commit -m "Änderungsbeschreibung"
git push --all

# Namespace "cattle-system  " anlegen
kubectl create namespace cattle-system

# Jump one folder up, and apply to the whole folder:
kubectl apply -f rancher/


helm install rancher rancher-stable/rancher \
--namespace cattle-system \
--set hostname=192.168.0.144 \
--set bootstrapPassword=admin

helm install rancher-dashboard rancher-latest/rancher \
--namespace cattle-system \
--set hostname=rancher.hlasta.home \
--set bootstrapPassword=admin \
--set ingress.tls.source=secret


helm delete rancher rancher-stable/rancher

kubectl -n cattle-system rollout status deploy/rancher

kubectl -n cattle-system get deploy rancher

helm get values rancher-dashboard -n cattle-system

helm get values rancher-dashboard -n cattle-system -o yaml > values.yaml
