Puppet master Ansible role
==========================

This is an Ansible role for configuring a Puppet master. Most configuration is
actually done by Puppet and Ansible is simply used to bootstrap the
configuration process.

Usage
-----

Minimally, you will need to set a Git repository URL using
the puppet\_environments\_repo variable in e.g. host\_vars. This needs to point
to a Git repository that contains a so called control repository for Puppet.
This control repository contains:

  * manifests directory with site.pp and nodes.pp
  * hieradata directory containing Hiera data
  * Puppetfile for downloading Puppet modules using r10k

You will also need to set up your Hiera hierarchy as specified in the r10k.yaml
file under templates.

Caveats
-------

You **must** set the inventory hostname for the Puppet master to be the same as
the host's FQDN.
