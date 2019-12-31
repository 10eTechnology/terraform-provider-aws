Rival's fork of terraform-provider-aws
==================
This is a fork we'll maintain, and bundle in our Terraform Docker image, in order to pull in various features and bug fixes that are useful or necessary.

Currently based off of: **v2.43.0**

With the following additions:

* https://github.com/terraform-providers/terraform-provider-aws/pull/11335 fix a bug where changing the name of a Route53 record does not delete the old record
    * `git merge --squash PR11335/jbergknoff/route53-delete-before-create`
* https://github.com/terraform-providers/terraform-provider-aws/pull/11211 publishing new Lambda versions after making config (non-code) updates
    * `git merge --squash PR11211/b-aws_lambda_function-publish-config-updates`
* https://github.com/terraform-providers/terraform-provider-aws/pull/10487 add Kinesis Stream Consumer resource
    * `git merge --squash PR10487/feature/kinesis-stream-consumer`
    * Also, added a patch to make it possible to import the resource.

```
$ git remote -v
PR10487 git@github.com:yomagroup/terraform-provider-aws (fetch)
PR10487 git@github.com:yomagroup/terraform-provider-aws (push)
PR11211 git@github.com:nemreid/terraform-provider-aws (fetch)
PR11211 git@github.com:nemreid/terraform-provider-aws (push)
PR11335 git@github.com:jbergknoff-rival/terraform-provider-aws (fetch)
PR11335 git@github.com:jbergknoff-rival/terraform-provider-aws (push)
origin  git@github.com:10etechnology/terraform-provider-aws (fetch)
origin  git@github.com:10etechnology/terraform-provider-aws (push)
upstream    git@github.com:terraform-providers/terraform-provider-aws (fetch)
upstream    git@github.com:terraform-providers/terraform-provider-aws (push)
```

Also consider pulling in:

* Let ECS task definition data source work gracefully if task definition doesn't exist.

Terraform Provider for AWS
==================

- Website: https://www.terraform.io
- [![Gitter chat](https://badges.gitter.im/hashicorp-terraform/Lobby.png)](https://gitter.im/hashicorp-terraform/Lobby)
- Mailing list: [Google Groups](http://groups.google.com/group/terraform-tool)

<img src="https://cdn.rawgit.com/hashicorp/terraform-website/master/content/source/assets/images/logo-hashicorp.svg" width="600px">

Requirements
------------

- [Terraform](https://www.terraform.io/downloads.html) 0.10+
- [Go](https://golang.org/doc/install) 1.13 (to build the provider plugin)

Developing the Provider
---------------------

If you wish to work on the provider, you'll first need [Go](http://www.golang.org) installed on your machine (please check the [requirements](https://github.com/terraform-providers/terraform-provider-aws#requirements) before proceeding).

*Note:* This project uses [Go Modules](https://blog.golang.org/using-go-modules) making it safe to work with it outside of your existing [GOPATH](http://golang.org/doc/code.html#GOPATH). The instructions that follow assume a directory in your home directory outside of the standard GOPATH (i.e `$HOME/development/terraform-providers/`).

Clone repository to: `$HOME/development/terraform-providers/`

```sh
$ mkdir -p $HOME/development/terraform-providers/; cd $HOME/development/terraform-providers/
$ git clone git@github.com:terraform-providers/terraform-provider-aws
...
```

Enter the provider directory and run `make tools`. This will install the needed tools for the provider.

```sh
$ make tools
```

To compile the provider, run `make build`. This will build the provider and put the provider binary in the `$GOPATH/bin` directory.

```sh
$ make build
...
$ $GOPATH/bin/terraform-provider-aws
...
```

Using the Provider
----------------------

To use a released provider in your Terraform environment, run [`terraform init`](https://www.terraform.io/docs/commands/init.html) and Terraform will automatically install the provider. To specify a particular provider version when installing released providers, see the [Terraform documentation on provider versioning](https://www.terraform.io/docs/configuration/providers.html#version-provider-versions).

To instead use a custom-built provider in your Terraform environment (e.g. the provider binary from the build instructions above), follow the instructions to [install it as a plugin.](https://www.terraform.io/docs/plugins/basics.html#installing-a-plugin) After placing it into your plugins directory,  run `terraform init` to initialize it.

For either installation method, documentation about the provider specific configuration options can be found on the [provider's website](https://www.terraform.io/docs/providers/aws/index.html).

Testing the Provider
---------------------------

In order to test the provider, you can run `make test`.

*Note:* Make sure no `AWS_ACCESS_KEY_ID` or `AWS_SECRET_ACCESS_KEY` variables are set, and there's no `[default]` section in the AWS credentials file `~/.aws/credentials`.

```sh
$ make test
```

In order to run the full suite of Acceptance tests, run `make testacc`.

*Note:* Acceptance tests create real resources, and often cost money to run. Please read [Running an Acceptance Test](https://github.com/terraform-providers/terraform-provider-aws/blob/master/.github/CONTRIBUTING.md#running-an-acceptance-test) in the contribution guidelines for more information on usage.

```sh
$ make testacc
```

Contributing
---------------------------

Terraform is the work of thousands of contributors. We appreciate your help!

To contribute, please read the contribution guidelines: [Contributing to Terraform - AWS Provider](.github/CONTRIBUTING.md)

Issues on GitHub are intended to be related to bugs or feature requests with provider codebase. See https://www.terraform.io/docs/extend/community/index.html for a list of community resources to ask questions about Terraform.

