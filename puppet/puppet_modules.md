# Puppet Module Creation & Deployment

## 1. Theory

### What is a Puppet Module?
A Puppet Module is a structured directory used to organize Puppet code, files, and templates for performing a specific configuration task. It allows you to reuse code, maintain cleaner structure, and scale your configuration efficiently.

### Why Puppet Modules?
- Helps manage large Puppet codebases
- Allows reuse of code across multiple nodes
- Provides a clean, organized folder structure
- Essential for production-level Puppet automation

### Module Directory Structure
A typical Puppet module looks like:
```
mymodule/
├── manifests/
│ └── init.pp
├── files/
├── templates/
└── metadata.json
```

### Key Components
#### `manifests/init.pp`
This is the main class file of the module where all logic is written.

Example:
```puppet
class mymodule {
  file { '/tmp/example.txt':
    ensure  => present,
    content => "Hello from Puppet Module!",
  }
}
```

#### `files/`

Contains static files that can be transferred directly to the agent machine using the source => 'puppet:///modules/mymodule/<file>' syntax.

#### `templates/`

Contains dynamic .erb templates (Ruby-based templates) used for generating configuration files based on variables or system facts.

### How Modules Work

A module is created inside the Puppet Master under:

```
/etc/puppetlabs/code/environments/production/modules/
```


The module contains:
```
Classes (inside manifests)

Static files

Templates

Metadata

site.pp decides which node uses which module.
```
When the agent runs:

```sh 
puppet agent -t 
```

It contacts the master, downloads the module, and applies the class.


**Machine :** Master
```sh
cd /etc/puppetlabs/code/environments/production/modules/
```

**Machine :** Master
```sh
sudo mkdir -p mymodule/manifests
sudo mkdir -p mymodule/files
sudo mkdir -p mymodule/templates
```

**Machine :** Master
```sh
sudo nano mymodule/manifests/init.pp
```

Paste the following:
```sh
class mymodule {

  file { '/tmp/module_test.txt':
    ensure  => present,
    content => "This file is created by Puppet Module!",
  }

  notify { "mymodule class has been applied on the agent": }
}
```

**Machine :** Master
```sh
sudo nano /etc/puppetlabs/code/environments/production/manifests/site.pp
```

Add the following:
```sh
node 'puppetagent' {
  include mymodule
}
```

**Machine :** Agent
```sh
sudo /opt/puppetlabs/bin/puppet agent -t
```
Expected Output:
```sh
Notice: mymodule class has been applied on the agent
Notice: File[/tmp/module_test.txt] created
```

**To verify file on agent**
```sh
cat /tmp/module_test.txt
```
Expected Outcome:
```
This file is created by Puppet Module!
```
