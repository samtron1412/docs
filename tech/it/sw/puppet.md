[TOC]

# [Overview](https://www.digitalocean.com/community/tutorials/how-to-install-puppet-in-standalone-mode-on-centos-7)

# [Installation](http://docs.puppetlabs.com/pe/latest/install_basic.html)
## Decide on a Deployment Type
### Agent/Master
In agent/master Puppet, you run a central puppet master server (or servers) that hosts and compiles all of your configuration data. Other nodes run the puppet agent service, which periodically pulls their configurations from the master. Each agent will only get its own configuration, and will be unable to see how other nodes are configured.

### Standalone Puppet
In standalone Puppet, every node periodically uses the puppet apply command to compile and apply its own configuration, using a full set of Puppet **modules** and **manifests**.

# [Upgrading Puppet](http://docs.puppetlabs.com/pe/latest/install_upgrading.html)

# Architecture
Puppet usually uses an *agent/master* (client/server) architecture for configuring systems, using the *Puppet agent* and *Puppet master* applications. It can also run in a self-contained architecture with the *Puppet apply* application.

## Two stages for configuration management
1. Compile a catalog
2. Apply the catalog

**Catalog** is a document that describes the desired system state for on specific computer. It lists all of the resources that need to be managed, as well as any dependencies between those resources.

## The Agent/Master Architecture
Puppet agent -> (sent facts) -> Puppet master -> (send catalog) -> Puppet agent -> (apply catalog) -> (send report) -> Puppet master.


## The Stand-Alone Architecture
Puppet Apply application (replace for both agent and master)

## [Different](https://docs.puppetlabs.com/puppet/3.7/reference/architecture.html#note-differences-between-agentmaster-and-puppet-apply)




## Important Directories and Files
### Main config directory
By default, Puppet’s config files, manifest directory, primary module directory, and (sometimes) SSL directory all reside in the confdir.

#### Code and Data Directories

`modules` — the main directory for Puppet’s modules. (Master only.)
`manifests` — contains the main starting point for catalog compilation. (Master only.)
`environments` — contains alternate versions of the modules and manifests directories, to allow code changes to be tested on smaller sets of nodes before entering production. (Master only.)
`ssl` — contains each node’s certificate infrastructure. (All nodes.)

#### Config Files

`puppet.conf` — Puppet’s main config file. (All nodes.)
`auth.conf` — access control rules for the Puppet master’s network services. (Master only, unless listen is enabled.)
`autosign.conf` — a list of pre-approved certificate requests. (CA master only.)
`csr_attributes.yaml` — optional data to be inserted into new certificate requests. (All nodes.)
`device.conf` — configuration for network devices managed by the puppet device command. (All nodes.)
`fileserver.conf` — configuration for additional fileserver mount points. (Master only.)
`hiera.yaml` — configuration for the Hiera data lookup system. (Master only.)
`routes.yaml` — advanced configuration of indirector behavior. (Master only.)
`tagmail.conf` — instructions for mailing important Puppet events to administrators. (Master only.)

### The module path
Every directory in the modulepath should only contain valid Puppet modules.




# [Puppet's Commands](https://docs.puppetlabs.com/puppet/3.7/reference/services_commands.html)


# [Puppet's language](https://docs.puppetlabs.com/puppet/3.7/reference/lang_visual_index.html)
[Hello, World!](http://docs.puppetlabs.com/pe/latest/quick_start_helloworld.html)

You’ll write a very simple module that contains classes to manage your motd (message of the day) and create a Hello, World! notification on the command line.


# [Modules](http://docs.puppetlabs.com/puppet/3.7/reference/modules_fundamentals.html)
Modules are self-contained bundles of code and data. You can write your own modules or you can download pre-built modules from the [Puppet Forge](http://forge.puppetlabs.com/).

Modules are how Puppet finds the classes and types it can use.

## Installing Modules
`puppet module install <module name> --version 0.0.2`

`puppet module list`

`puppet module search <name>`

`puppet module uninstall <name>`

`puppet module upgrade <name>`


## Module Layout
On disk, a module is simply a directory tree with a specific, predictable structure:

    <MODULE NAME>
        manifests
        files
        templates
        lib
        facts.d
        tests
        spec

## Example

This example module, named “my_module”, shows the standard module layout in more detail:

- `my_module` — This outermost directory’s name matches the name of the module.
    + `manifests/` — Contains all of the manifests in the module.
        * `init.pp` — Contains a class definition. This class’s name must match the module’s name.
        * `other_class.pp` — Contains a class named `my_module::other_class`.
        * `my_defined_type.pp` — Contains a defined type named `my_module::my_defined_type`.
        * `implementation/` — This directory’s name affects the class names beneath it.
            - `foo.pp` — Contains a class named `my_module::implementation::foo`.
            - `bar.pp` — Contains a class named `my_module::implementation::bar`.
    + `files/` — Contains static files, which managed nodes can download.
        * `service.conf` — This file’s `source =>` URL would be `puppet:///modules/my_module/service.conf`. Its contents can also be accessed with the `file` function, like `content => file('my_module/service.conf')`.
    + `lib/` — Contains plugins, like *custom facts* and *custom resource types*. These will be used by both the Puppet master server and the Puppet agent service, and they’ll be synced to all agent nodes whenever they request their configurations. See “Using Plugins” for more details.
    + `facts.d/` — Contains *external facts*, which are an alternative to Ruby-based custom facts. These will be synced to all agent nodes, so they can submit values for those facts to the Puppet master. (Requires Facter 2.0.1 or later.)
    + `templates/` — Contains templates, which the module’s manifests can use. See “Templates” for more details.
        * `component.erb` — A manifest can render this template with `template('my_module/component.erb')`.
    + `tests/` — Contains examples showing how to declare the module’s classes and defined types.
        * `init.pp`
        * `other_class.pp` — Each class or type should have an example in the tests directory.
    + `spec/` — Contains spec tests for any plugins in the lib directory.

Each of the module’s subdirectories has a specific function, as follows.

## Manifests


## Allowed Module Names
Module names should only contain *lowercase letters*, *numbers*, and *underscores*, and should *begin with a lowercase letter*; that is, they should match the expression `[a-z][a-z0-9_]*`.

## Files


## Templates


## Writing Modules




# [Integrated with Vagrant](http://terrarum.net/blog/masterless-puppet-with-vagrant.html#vagrants-puppet-provisioners)


# Plugins in Modules
## Details
This page describes the deployment of custom **facts** and **types** for use by the client via modules.

Custom types and facts are stored in modules. These custom types and facts are then gathered together and distributed via a file mount on your Puppet master called plugins.

## Module structure
Plugins are stored in the lib directory of a module, using an internal directory structure that mirrors that of the Puppet code:

    {modulepath}
    └── {module}
        └── lib
            |── augeas
            │   └── lenses
            ├── facter
            └── puppet
                ├── parser
                │   └── functions
                ├── provider
                |   ├── exec
                |   ├── package
                |   └── etc... (any resource type)
                └── type

As the directory tree suggests, custom facts should go in `lib/facter/`, custom types should go in `lib/puppet/type/`, custom providers should go in `lib/puppet/provider/{type}/`, and custom functions should go in `lib/puppet/parser/functions/`.

For example:

A custom user provider:

    {modulepath}/{module}/lib/puppet/provider/user/custom_user.rb
A custom package provider:

    {modulepath}/{module}/lib/puppet/provider/package/custom_pkg.rb
A custom type for bare Git repositories:

    {modulepath}/{module}/lib/puppet/type/gitrepo.rb
A custom fact for the root of all home directories (that is, /home on Linux, /Users on Mac OS X, etc.):

    {modulepath}/{module}/lib/facter/homeroot.rb
A custom Augeas lens:

    {modulepath}/{module}/lib/augeas/lenses/custom.aug

# Hiera
Hiera is a key/value lookup tool for configuration data, built to make Puppet better and let you set node-specific data without repeating yourself.

## Why Hiera?
### Making Puppet Better

Hiera makes Puppet better by keeping *site-specific data out of your manifests*. Puppet classes can request whatever data they need, and your Hiera data will act like a site-wide config file.

This makes it:

- Easier to configure your own nodes: default data with multiple levels of overrides is finally easy.
- Easier to re-use public Puppet modules: don’t edit the code, just put the necessary data in Hiera.
- Easier to publish your own modules for collaboration: no need to worry about cleaning out your data before showing it around, and no more clashing variable names.

### Avoiding Repetition

With Hiera, you can:

- Write common data for most nodes
- Override some values for machines located at a particular facility…
- …and override some of those values for one or two unique nodes.

This way, you only have to write down the differences between nodes. When each node asks for a piece of data, it will get the specific value it needs.

To decide which data sources can override which, Hiera uses a **configurable hierarchy**. This ordered list can include both **static** data sources (with names like “common”) and **dynamic** ones (which can switch between data sources based on the node’s name, operating system, and more).

## Installation
        puppet resource package hiera ensure=installed
        gem install hiera

## Configuration and hiera.yaml
### Format
#### Example config file
```yaml
---
:backends:
  - yaml
  - json
:yaml:
  :datadir: /etc/puppet/hieradata
:json:
  :datadir: /etc/puppet/hieradata
:hierarchy:
  - "%{::clientcert}"
  - "%{::custom_location}"
  - common
```

#### Default Config Values
If the config file exists but has no data, the default settings will be equivalent to the following:

```yaml
---
:backends: yaml
:yaml:
  :datadir: /var/lib/hiera
:hierarchy: common
:logger: console
```

### Global settings
If absent, they will have default values.

#### :hierarchy
Must be a *string* or an *array of strings*, where each string is the *name of a static or dynamic data source*.

The data sources in the hierarchy are checked in order, top to bottom.

**Default value**: "common"

#### :backends
Must be a string or an array of strings, where each string is the *name of an available Hiera backend*. The built-in backends are `yaml` and `json`; an additional `puppet` backend is available.

    **Custom backends**: See “[Writing Custom Backends](http://docs.puppetlabs.com/hiera/1/custom_backends.html)” for details on writing new backend.

**Default value**: "yaml"

#### :logger
Must be the name of an available logger, as a string.

Loggers only control where warnings and debug messages are routed. You can use one of the built-in loggers, or write your own. The built-in loggers are:

- `console` (messages go directly to STDERR)
- `puppet` (messages go to Puppet’s logging system)
- `noop` (messages are silenced)

**Default value**: "console"; note that Puppet overrides this and sets it to "puppet", *regardless of what’s in the config file*.

### Backend-Specific Settings
`yaml` and `json`

#### :datadir
The directory in which to find data source files. This must be a string.

**Default value**: `/var/lib/hiera` on *nix, and `COMMON_APPDATA\PuppetLabs\Hiera\var` on Windows.



## [Hierarchies](http://docs.puppetlabs.com/hiera/1/hierarchy.html)
### Syntax
[Best Practice: Use Fully-Qualified Puppet Variables](http://docs.puppetlabs.com/hiera/1/variables.html)

