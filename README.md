# Patches and Ansible Playbook to Prepare Ubuntu Boxes for CoreMedia

`coremedia-ubuntu-development`

The patches in this workspace are prepared to patch a 1710 CMS-9 workspaces
to be deployable as a single node configuration on a Ubuntu based host.

The playbook in this repository is intended for preparation of CI nodes and 
other hosts, which need to be able to build [CoreMedia][coremedia] workspaces 
for CoreMedia CMS 9 or LiveContext 3 without any other installation steps 
necessary.

Find mirrors of this repository at [gitlab][gitlab] and [github][github].


## Setup of the Environment

We rely on the roles `coremedia` for all coremedia hosts and `cmdev` for 
development hosts.

The role `coremedia` provides the (not supported but happily working) OpenJDK 
for users which do not want to include Oracle Java from the default CoreMedia 
chef node configuration.

The role `cmsdev` provides the needed development tools to build a workspace.


## Preparation

Install python on your node since otherwise ansible will not start.

The recipes in here also need a pre-installed ohai.

```
apt-get install python
apt-get install ohai
```

Configure relevant hosts in `inventory.properties` or your global ansible hosts 
file (if you haven't done so).


## Usage

Run with: 

```
ansible-playbook -i inventory.properties setup.yml
```


## Collection

This playbook provides:

* Java 8 
* mod_jk for Apache httpd

for hosts in role `coremedia`, and

* PhantomJS
* Maven
* [SenchaCMD][sencha]

for hosts in role `cmdev` .


## Deployment of the System to Ubuntu

To deploy CoreMedia CMS-9 to Ubuntu based systems, you will need to apply the
patches provided in this workspace to the chef scripts in your workspace.

### Known Issues Elsewhere

It might be, that you will need to use AJP not only for the Studio as indicated 
in the patches but also for the preview. This was not the case for the 1710
workspace but for a customized 1707 one.


## Feedback

Please use the [issues][issues] section of this repository at [github][github] 
for feedback. 

[issues]: https://github.com/provocon/coremedia-ubuntu-development/issues
[sencha]: https://www.sencha.com/products/extjs/cmd-download/
[coremedia]: https://www.coremedia.com/
[github]: https://github.com/provocon/coremedia-ubuntu-development
[gitlab]: https://gitlab.com/provocon/coremedia-ubuntu-development
