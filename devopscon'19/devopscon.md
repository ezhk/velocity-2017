# Deploy miscroservices like a Ninja with Istio service mesh
[Istio presentation](http://www.devopstrain.pro/istio/)  
[Register](bit.do/istio1), auth code: 5CPL  

Tiny running fix: microk8s.enable istio and answer «N».  

    $ kubectl describe pod -l=app=httpbin
    $ kubectl get pod httpbin-5c649bb49c-bfnvh -o yaml  

# Silos
3 ways of devops:

- flow
- feedback
- continious learning

Operations as mutual service.

# Shell Ninja
[Source](https://github.com/ro14nd-talks/shell-ninja)  
[Bash testing](https://github.com/sstephenson/bats)  

## Why?

 - shell is eveywhere.
 - it's least common denominator
 - fast turnaround

## History

* sh by Ken Thomson
* year: 1971
* CLI
* IO redirection
* no variable, no pipelines

## Bournee Shell by Stephen Bourne

* 1979
* inludes if, for
* variables, environments

## C-sh

* 1979
* aliases
* history
* ~
* job command

## Bash by Brian Fox

* 1989

```
#!/bin/bash

# fail on every and undefined vars
set -eu
        
# fail in a single failed command in a pipeline
set -o pipefail
        
# save global script args
args=("$@")

hasflag() {
    # - is default value in ${1:-}
    local flag=${1}
    for arg in "${ARGS[@}"; do
        # make check safe with using "
        if [ "$arg" == "$flag" ]; then
            echo "true"
            return
        fi
    done
    echo "false"
}

# here we call true or false command,
#   also possible to use return 1 or return 0
if $(hasflag --devops); then
    echo "Hello, Berlin!"
fi

loadmodules() {
    cmd=${ARGS[0]}
    for module in $(basedir)/modules/*; do
        if [ "$(basedir)/modules/$cmd" = "$module" ]; then
            source $(basedir)/modules/${module}
            # call function run() in module
            eval "${module}::run"
        fi
    done
}

debug() {
    if $(hasflag --verbose -v); then
        export PS4='+ ${BASH_SOURCE[0]} ${LINE_NO}'
        set -x
    fi
}

# replaca strong
check_error() {
    echo "${msg//ERROR}"
    # logic here
}
```

Bash testing:

```
@test "addition using dc" {
  result="$(echo 2 2+p | dc)"
  [ "$result" -eq 4 ]
}

@test "No image driven" {
    runldeploy $(PATH)/canary -- deployment=bla"

    echo $output
    [ $status -eq 1 ]
    asseert_regexp "No new image"
    asseert_regexp "--image"
    asseert_regexp "canary"
}
```

# kubectl hacking
[source](https://github.com/loodse/kubectl-hacking)

[bash-completion](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)  
[powerline go](https://github.com/justjanne/powerline-go)  