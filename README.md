# kubectl_aliases

Shell functions and aliases to speed up your Kubernetes / kubectl troubleshooting workflow

## Setup instructions

Run the following command in your terminal to open your zsh env file and add the aliases and functions below

```
code ~/.zshrc 
```

- Add the shell function below to shorten the kubectl command for k 

```
autoload -Uz compinit
compinit

source <(kubectl completion zsh)

alias k=kubectl
```

- With the big "k" ready now let's add some aliases: 

```
##------ kubectl get
alias kg='k get'

##------ kubectl describe resources
alias kd='k describe'

##------ kubectl apply resources
alias ka='k apply'

##------ kubectl delete resources
alias kr='k delete'

##------ kubectl edit resources 
alias ke='k edit'

##------ kubectl apply
alias kx="k exec -it"
```

- With the big "k" and some aliases ready let's now and play around with a function to exec the agent

```

kag(){
       eval "k exec -it" $1 "-- agent" $2
    } 

```

- Save your .zshrc and restart (close and open) your terminal. 

## Use example

- Kubectl get 
```
kd pod my_app45372ba
# Describe pod

kg pods -n kube-system
# list of pods in kube-sytem namespace 
```
- Generate a status command for a Datadog agent deployment pod:

```
# Datadog agent pod name: datadog-agent-dxmm4

kag datadog-agent-dxmm4 status
# datadog-agent status output

kag check Openmetrics
# Openmetrics check output (if exists)

```
