The purpose of kud is to provide an opinionated pod deletion of one or many kubernetes pod(s).  Traditionally, if one wanted to delete a kubernetes pod, one had to `kubectl get pods --namespace foo`, visually identify the pod of interest, copy that pod to the buffer, and then `kubectl --namespace delete pod <paste_buffer>` to delete the pod.  This simple utility aims to provide a namespace-specific pod selector for quick execution.

# kud

```sh
kud(1)

NAME
    kud - Quick k8s pod deletion utility.

REQUIRES
    kubectl(1)

SYNOPSIS
    kud [OPTIONS]

DESCRIPTION
    ${SCRIPT} is a quick kubernetes (k8s) utility to delete 1+n pods. ${SCRIPT} prompts for:
      - <NAMESPACE> (defaults to current ns. See kubens(1))
      - <POD> (defaults to "1")
      - <CONFIRM> (defaults negatory)
    ENTER to use defaults.

OPTIONS
    -h, --help
        Show this help message
    -f, --force
        `kud -f` will delete the first pod in the namespace without further prompting.
    -a, --all
        Delete all pods in the namespace

SEE ALSO
    kubectx(1), kubens(1)
```

### USAGE

```sh
$ kud
Namespace? (default qux):
    1 qux
    2 quux
    3 quuz
    4 corge
    5 grault
    6 garply
    7 waldo
    8 fred
    9 plugh
    10 xyzzy
    11 thud
4
Pod number? (default 1):
    1 foo-drupal: running
    2 bar-mariadb: running
    3 baz-alpine: pending
2
Are you sure?
y

pod bar-mariadb deleted
```

With the `-a` or `--all` flag, all pods in the namespace will be deleted, without any further prompts.  When the `-f` or `--force` flag is invoked, the first, or only, pod in the namespace will be deleted, again without any further prompts.

_NOTE_: If your kubernetes pod object was created as a `POD`, and not a replicaset or deployment, self-healing may not occur (the pod won't restart of its own volition.)

## Installation

**For macOS:**

Use the [Homebrew](https://brew.sh/) package manager:
```sh
brew tap farmotive/k8s
brew install kud
```
**NOTE:** If using gcloud sdk to manage the installation and versioning of `kubectl`, install with the `--without-kubernetes-cli` flag to omit the brew dependency:
```sh
brew install kud --without-kubernetes-cli
```

See [farmotive homebrew k8s install section](https://github.com/farmotive/homebrew-k8s#install) for more options.

**Other platforms:**

- Download the `kud` script
- Add it somewhere in your PATH
- Make it executable (`chmod +x`)

-----

Thanks to [ahmetb](https://github.com/ahmetb) for the inspiration!
