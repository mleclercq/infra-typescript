# Pulumi infra template

This repository is intended to be used as a pulumi template to initialize an
infrastructure-as-code folder in an application repository.

## Usage

Go in the application folder where you want to initialize the infra code, then
run:

```bash
mkdir infra && cd infra
pulumi new https://github.com/mleclercq/infra-typescript
```

You will be asked a couple of questions as follow:

```
This command will walk you through creating a new Pulumi project.

Enter a value or leave blank to accept the (default), and press <ENTER>.
Press ^C at any time to quit.

project name: (infra)                             <<<- ENTER THE NAME OF THE APPLICATION HERE
project description: (My application infra)       <<<- ENTER THE NAME OF THE APPLICATION HERE FOLLOWED BY dev
Created project 'YOUR APPLICATION'

Please enter your desired stack name.
To create a stack in an organization, use the format <org-name>/<stack-name> (e.g. `acmecorp/dev`).
stack name: (dev)                                 <<<- KEEP DEFAULT VALUE, PRESS ENTER
Created stack 'dev'

kubernetes:context: Do not change me: (this-is-not-the-cluster-you-re-looking-for) <<<- KEEP DEFAULT VALUE, PRESS ENTER
Saved config
```

> Note the `this-is-not-the-cluster-you-re-looking-for` kubernetes:context is a
> way to make sure you do not create kubernetes resources on the wrong cluster.
>
> All Kubernetes resources managed by Pulumi should specify directly (with a
> `{ provider: ... }` option) or indirectly (with a `{ parent: this }` option)
> on which Kubernetes cluster it should be deployed.
> With that setting, if you forget to specify one of these options, Pulumi will
> try to deploy the kubernetes resource on the cluster whose context name is
> `this-is-not-the-cluster-you-re-looking-for` (e.g. Pulumi will try to do
> something like
> `kubectl --context this-is-not-the-cluster-you-re-looking-for apply -f ...`)
> which will fail instead of creating a Kubernetes resource on whatever cluster
> your current kubernetes context points to.
