
## kubectl Cheatsheet

### Help

```
alias k=kubectl                         
export do="--dry-run=client -o yaml"    # k get pod x $do
export now="--force --grace-period 0"   # k delete pod x $now
k explains pods --recursive       # get the documentation for pod manifests
```
### context and configuration
```
# use multiple kubeconfig files at the same time and view merged config
KUBECONFIG=~/.kube/config:~/.kube/kubconfig2 

k config view                 #Show Merged kubeconfig settings.
k config view \
  -o jsonpath='{. users [? (@. name == "e2e")]. user. password}'
k config view -o jsonpath='{. users[]. name}' # display the first user
k config view -o jsonpath='{. users [*]. name}' # get a list of users
k config view -o jsonpath="{.contexts[*].name}"

k config gets-contexts        #display list of contexts 
k config get-contexts -o name
k config current-context      #display the current-context
k config use-context <name>   #set the default context to my-cluster-name
k config set-context --current -n dev   
k config set-context test --user=admin -n foo
```

### Pod

```
k get pods
k get pods -l env=dev --no-headers

k run nginx --image=nginx
k run nginx --image=nginx $do #Generate POD Manifest YAML file

k delete pod <pod_name> -n <namespace> $now
```
