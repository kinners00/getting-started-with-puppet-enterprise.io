
   - [What is Bolt?](#what-is-bolt)
   - [What are the use cases for Bolt?](#what-are-the-use-cases-for-bolt)
   - [Sorry, I don't have time to learn another language right now](#sorry-i-dont-have-time-to-learn-another-language-right-now)
   - [Any language, surely you can't be serious?](#any-language-surely-you-cant-be-serious)
   - [What's the catch? Targets must need prequisities of some kind](#whats-the-catch-targets-must-need-prequisities-of-some-kind)
   - [Agentless Connectivity](#agentless-connectivity)
   - [What platforms does Bolt support?](#what-platforms-does-bolt-support)
   - [Lets get started!](#lets-get-started)


# bolt_sandbox

A sandbox-type project to aid learning around Bolt and it's various functionality enabling folks to hit the ground running when beginning to use Bolt and leverage pre-built automation from the forge. 

If you've never used bolt before, start your journey below!

<iframe width="560" height="315"
src="https://www.youtube.com/embed/MUQfKFzIOeU" 
frameborder="0" 
allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
allowfullscreen></iframe>


## What is Bolt?

Bolt is an **agentless** ad-hoc automation tool that allows you to run commands, scripts, tasks, plans and puppet code to simply achieve automation goals. If you're new to automation, bolt is a great place to start. 

## What are the use cases for Bolt?

Due to the ad-hoc nature of Bolt tasks, there are some use cases where these method is particularly appropriate such as:

- Patching
- Vulnerability management
- Network device management
- Maintenance tasks:
    - Rotate logs
    - Back ups
    - Restart system services

Bolt Plans allow you to create more complex workflows with multiple steps that need to be executed in sequential order. You can use plans for things like:

- Application Deployments
- COTS application upgrades
- Patching including pre/post patching tasks

## Sorry, I don't have time to learn another language right now

You don't have to! Bolt is language agnostic, so you can use whatever you're most comfortable with.

## Any language, surely you can't be serious?

![alt text](https://raw.githubusercontent.com/kinners00/files/main/DahUIvIU0AA_EbJ.jpeg)

 You can use Bolt with any scripting/programming language beit bash, powershell, python, ruby etc. Put simply, if your target can run it locally, Bolt can handle it.

![alt text](https://miro.medium.com/max/1474/0*lmMW87wdhzte-zAn.png)

 ## What's the catch? Targets must need prequisities of some kind

 No, nothing. Unlike other tools, Bolt is built to be easy to use and flexible so you can bring your skills to the table and begin reducing manual effort, today. No python packages needed, no puppet agent.

## Agentless Connectivity

Bolt is agentless by nature and as such connects to nodes via SSH or WinRM. Credential information can be provided via bolt command or stored in an inventory file, meaning you don't need to specify targets credentials each time you run a bolt command. 

## What platforms does Bolt support?

**Workstation**

Debian, Fedora, RHEL, SLES, Ubuntu, macOS and Windows - For details on which specific versions of each OS are supported check out [this link](https://puppet.com/docs/bolt/latest/bolt_installing.html)

**Targets**

Virtually everything - if you can connect to it via SSH/WinRM, you can most likely use it as a target with bolt. This includes things like network devices etc.

## Lets get started!

Begin your bolt journey below:

[**I'm ready!**](https://github.com/kinners00/bolt_sandbox/blob/master/docs/1_intro_to_bolt.md)


```json
{
     "description": "Displays first name/surname and age based on user input",
     "input_method": "environment"
   }

```

```bash
#!/bin/bash

# Validation of "firstname" and "surname" puppet task inputs
if [[ $PT_firstname ]] && [[ $PT_surname ]]; then
   echo "Full name:" $PT_firstname $PT_surname
else 
   echo "First name:" $PT_firstname
fi

# Validation of "age" input
if [[ $PT_age ]]; then
   echo "Age:" $PT_age
fi

```

```powershell
[CmdletBinding()]
Param(
 [Parameter(Mandatory)][string]$firstname,
 [string]$surname,
 [int]$age
 )

# Validation of "firstname" and "surname" puppet task inputs 
 if (($firstname) -and (($surname)))  {
    Write-Host "Full name: $firstname $surname"
    }  else {
    Write-Host "First name: $firstname"
}

# Validation of "age" input
 if ($age) {
    Write-Host "Age: $age"
}

```

```json
{
     "description": "Displays first name/surname and age based on user input",
     "input_method": "environment",
     "parameters": {
       "firstname": {
           "description": "Provide a first name of least 2 characters",
            "type": "String[2]"
       },
       "surname": {
           "description": "Provide a surname",
            "type": "Optional[String]"
       },
       "age": {
             "description": "Provide your age",
             "type": "Optional[Integer[18,100]]"
        }
     }
   }

```


```puppet
    service { 'ntpd':
	    ensure => 'running',
        enable => 'true',
    }

```

```yaml
---
version: 5

defaults:
  datadir: "data"

hierarchy:
  - name: 'Yaml backend'
    data_hash: yaml_data
    paths:
      - "nodes/%{trusted.certname}.yaml"
      - 'common.yaml'

```

```puppet
class profile::apache_web(
  String $doc_root,
  String $vhost_name,
  Integer $port,
  Boolean $default_vhost
) {

  class { 'apache':
    default_vhost => $default_vhost,
  }
  apache::vhost { '$vhost_name':
    port    => $port,
    docroot => '$doc_root',
  }
}
```



