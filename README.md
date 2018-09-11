# AUDITING WITH INSPEC BADGE TOPICS 
# A.K.A. InSpec Certification Study Guide
The Auditing With InSpec badge is awarded when someone proves that they understand the
core elements of InSpec. 

### An InSpec test is called a control. Controls are grouped into profiles.

Candidates must show:
1.  An understanding of installing InSpec.
2.  An understanding of InSpec profiles.
3.  An understanding of running inspec.
4.  An understanding of controls and metadata.
5.  An understanding of troubleshooting InSpec.

**Note:** I switched 2 and 3 from the official order for a better flow while learning.

## 1. INSTALLING INSPEC
### INSPEC INSTALLATION AND TARGET NODE

Candidates should understand:
- Software InSpec requires on a workstation so you can invoke an inspec command.
The workstation is your machine that you use on a daily basis.  Install inspec on it and you can keep your profiles locally or run remote profiles while targeting remote machines to inspect. 
- Software InSpec requires on a target.
  ```
  InSpec works over the SSH protocol when scanning Linux systems, 
  and the WinRM protocol when scanning Windows systems. 
  Therefore, InSpec requires no software to be installed on the target system.
  ```
- Installing inSpec on containers.
- How inSpec knows what command to run on a target for a particular resource.

### CHEFDK INSPEC OMNIBUS AND RUBYGEM
Candidates should understand:
- How to install InSpec software on a workstation.

- ChefDK vs. InSpec Omnibus vs. Ruby Gem.
InSpec requires Ruby ( >2.2 ).
### CHEFDK
Install the [Chef DK](https://downloads.chef.io/chefdk/). Choose this option if you're a Chef user or are interested in using Chef to correct compliance failures. The Chef DK includes InSpec.

### INSPEC
Install the [InSpec CLI](https://downloads.chef.io/inspec/). Choose this option if you're interested only in InSpec or have an existing way to correct compliance failures.
### Install as package

The InSpec package is available for MacOS, RedHat, Ubuntu and Windows. Download the latest package at [InSpec Downloads](https://downloads.chef.io/inspec) or install InSpec via script:

```
# RedHat, Ubuntu, and macOS
curl https://omnitruck.chef.io/install.sh | sudo bash -s -- -P inspec

# Windows
. { iwr -useb https://omnitruck.chef.io/install.ps1 } | iex; install -project inspec
```

### Install it via rubygems.org

When installing from source, gem dependencies may require ruby build tools to be installed.

For CentOS/RedHat/Fedora:

```bash
yum -y install ruby ruby-devel make gcc gcc-c++
```

For Ubuntu:

```bash
apt-get -y install ruby ruby-dev gcc g++ make
```

To install inspec from [rubygems](https://rubygems.org/):

```bash
gem install inspec
```


## 2. [INSPEC PROFILES](https://www.inspec.io/docs/reference/profiles/ "Inspec profile docs")

### Profile Structure
A profile should have the following structure:
```
   examples/profile   
    ├── README.md
    ├── controls
    │   ├── example.rb
    │   └── control_etc.rb
    ├── libraries
    │   └── extension.rb
    |── files
    │   └── extras.conf
    └── inspec.yml
    
where:
 - inspec.yml includes the profile description (required)
 - controls is the directory in which all tests are located (required)
 - libraries is the directory in which all InSpec resource extensions are located (optional)
 - files is the directory with additional files that a profile can access (optional)
 - README.md should be used to explain the profile, its scope, and usage
```

### METADATA AND THE LOCK FILE
Candidates should understand:
- The purpose of the inspec.yml file.
The purpose of the inspec.yml file is to provide metadata about the profile.
### inspec.yml
Each profile must have an inspec.yml file that defines the following metadata:

Use **name** to specify a unique name for the profile. **Required**.
```
name: ssh
```
Use **title** to specify a human-readable name for the profile.
```
title: Basic SSH
```
Use **maintainer** to specify the profile maintainer.
```
maintainer: Chef Software, Inc.
```
Use **copyright** to specify the copyright holder.
```
copyright: Chef Software, Inc.
```
Use **copyright_email** to specify support contact information for the profile, typically an email address.
```
copyright_email: support@chef.io
```
Use **license** to specify the license for the profile.
```
license: Proprietary, All rights reserved
```
Use **summary** to specify a *one line* summary for the profile.
```
summary: Verify that SSH Server and SSH Client are configured securely
```
Use **description** to specify a *multiple line* description of the profile.
```
description: Verify that SSH Server 
             and SSH Client are 
             configured securely
```
Use **version** to specify the profile version.
```
version: 1.0.0
```
Use **inspec_version** to place Semantic Versioning (SemVer) constraints on the version of InSpec that the profile can run under.
```
inspec_version: "~> 2.1"
```
Use **supports** to specify a list of supported platform targets.
```
supports:
  - os-family: linux
```
Use **depends** to define a list of profiles on which this profile depends.
```
depends:
  - name: profile
    path: ../path/to/profile
```
**name** is **required**; all other profile settings are optional.

For example:
```
name: ssh
title: Basic SSH
maintainer: Chef Software, Inc.
copyright: Chef Software, Inc.
copyright_email: support@chef.io
license: Proprietary, All rights reserved
summary: Verify that SSH Server and SSH Client are configured securely
version: 1.0.0
supports:
  - os-family: linux
depends:
  - name: profile
    path: ../path/to/profile
inspec_version: "~> 2.1"
```

- How an InSpec profile's name and version are defined.
- How to define profile dependencies.
- What it means to 'vendor' profiles.
- What the 'inspec.lock' file is.
- Updating the 'inspec.lock' file.
- Setting profile metadata.
See inspec.yml
- Managing updates from upstream profiles.

### PROFILE VERSION SEMVER AND CONSTRAINTS
Candidates should understand:
- The meaning of 'semver' versioning.
- How to set profile version.
- Setting version constraints.
- Setting profile dependencies.

### BASIC RESOURCE TYPES
Candidates should understand:
- Read and understand basic profiles.
- Identify core InSpec resources.
- How to use the common InSpec resources.
- How to find reference documentation on each resource.
- The matchers available for each resource, and when to use each.
- The correct syntax for describe statements.
- Matching on STDERR and STDOUT.
- Using the file resource to test directories.

### CREATING CUSTOM RESOURCES
Candidates should understand:
- Why you might want to write a custom InSpec resource.
- Where custom resource code resides.
- Using custom resources within a control.
- Identifying the Inspec.resource class.
- Understand the InSpec recourse DSL.

### PROFILES INHERITANCE TO OVERLAY CUSTOM CHANGES
Candidates should understand:
- Overlaying custom changes to profiles
- Inheriting only certain controls from another profile.
- Overwriting metadata in inherited controls.

### PROFILES INHERITANCE TO USE CUSTOM RESOURCES
Candidates should understand:
- Using custom resources.
- Using custom matchers.
- How to invoke a custom resource defined in a dependent profile.
- How to invoke a custom resource defined in a dependent resource pack.
- What happens if a custom resource is given the same name as a core resource.

### PROFILE ATTRIBUTES
- Candidates should understand:
- Attribute scope – within a control or within a profile.
- Why you would use attributes.
- How and where attribute values are defined.
- How to reference attributes within a control file.
- Where default values for profile attributes are defined.

### TESTING EITHER/OR CONFIGURATION CHECKS
Candidates should understand:
- When would you use a describe.one statement.
- When would you use an only_if statement.
- describe.one statement syntax.
- only_if statement syntax.
- When an only_if block returns true.

### SHARING OF PROFILES
Candidates should understand:
- How you use the Chef Supermarket.
- How you would share a custom resource with the community.
- How you would share a custom profile with the community.
- How you would run a profile directly from GitHub or the Supermarket.


## 3. RUNNING INSPEC
### RUNNING ON A LOCAL SYSTEM
Candidates should understand:
- What inspec commands are available.
```
>inspec help
Commands:
  inspec archive PATH                # archive a profile to tar.gz (default) or zip
  inspec artifact SUBCOMMAND ...     # Sign, verify and install artifacts
  inspec check PATH                  # verify all tests at the specified PATH
  inspec compliance SUBCOMMAND ...   # Chef Compliance commands
  inspec detect                      # detect the target OS
  inspec env                         # Output shell-appropriate completion configuration
  inspec exec PATHS                  # run all test files at the specified PATH.
  inspec habitat SUBCOMMAND ...      # Commands for InSpec + Habitat Integration
  inspec help [COMMAND]              # Describe available commands or one specific command
  inspec init TEMPLATE ...           # Scaffolds a new project
  inspec json PATH                   # read all tests in PATH and generate a JSON summary
  inspec shell                       # open an interactive debugging shell
  inspec supermarket SUBCOMMAND ...  # Supermarket commands
  inspec vendor PATH                 # Download all dependencies and generate a lockfile in a `vendor` directory
  inspec version                     # prints the version of this tool

Options:
  l, [--log-level=LOG_LEVEL]         # Set the log level: info (default), debug, warn, error
      [--log-location=LOG_LOCATION]  # Location to send diagnostic log messages to. (default: STDOUT or STDERR)
      [--diagnose], [--no-diagnose]  # Show diagnostics (versions, configurations)

```
- How to invoke inSpec locally.
```
inspec exec PATHS                  # run all test files at the specified PATH.
```
- Using Inspec detect locally.
```
>inspec detect

== Platform Details

Name:      ubuntu
Families:  debian, linux, unix
Release:   16.04
Arch:      x86_64
```
- Using inSpec to scan the local machine using a local profile.
An inSpec profile is identified by its pathname. So if we have the following profile:
```
./auditd
|-- README.md
|-- controls
|   `-- example.rb
|-- inspec.lock
`-- inspec.yml
```
- Invoking InSpec to check a profile contained on your local filesystem.
We can check to make sure the profile is valid.
```
>inspec check ./auditd
Location:    ./auditd
Profile:     auditd
Controls:    1
Timestamp:   2018-09-09T13:06:30+00:00
Valid:       true

No errors or warnings
```
Now we know that the profile is valid we can run the profile with inspec like so:
```
inspec exec ./auditd

Profile: InSpec Profile (auditd)
Version: 0.1.0
Target:  local://

  System Package auditd
     ✔  should be installed

Test Summary: 1 successful, 0 failures, 0 skipped
```
- Using InSpec to scan the local machine using a remote profile.
The Chef supermarket contains chef recipies as well as inspec profiles.  Here we execute a supermarket profile against the local machine.  
```
>inspec supermarket exec dev-sec/linux-baseline

Profile: DevSec Linux Security Baseline (linux-baseline)
Version: 2.2.2
Target:  local://

  ✔  os-01: Trusted hosts login
     ✔  File /etc/hosts.equiv should not exist
  ✔  os-02: Check owner and permissions for /etc/shadow
     ✔  File /etc/shadow should exist
     ✔  File /etc/shadow should be file
     ✔  File /etc/shadow should be owned by "root"
... -snip- ...
Profile Summary: 13 successful controls, 3 control failures, 38 controls skipped
Test Summary: 51 successful, 5 failures, 38 skipped
```
- Invoking InSpec to check a profile stored on a remote server via git.
```
>inspec check https://github.com/learn-chef/auditd/

Location:    https://github.com/learn-chef/auditd/
Profile:     auditd
Controls:    1
Timestamp:   2018-09-09T14:57:20+00:00
Valid:       true

No errors or warnings
```
- Invoking specific controls. 

### PACKAGING PROFILES
You can also package a profile as a compressed archive to make it easier to share. You can package profiles in tar.gz or zip format.  Before packaging your profiles check its validity with **inspec check**.  If it checks out package your profiles with the **inspec archive** PATH command.
```
>inspec archive ./auditd
I, [2018-09-09T14:37:57.195990 #206]  INFO -- : Checking profile in auditd
I, [2018-09-09T14:37:57.196243 #206]  INFO -- : Metadata OK.
I, [2018-09-09T14:37:57.198839 #206]  INFO -- : Found 1 controls.
I, [2018-09-09T14:37:57.198943 #206]  INFO -- : Control definitions OK.
I, [2018-09-09T14:37:57.199372 #206]  INFO -- : Generate archive /root/auditd-0.1.0.tar.gz.
I, [2018-09-09T14:37:57.208862 #206]  INFO -- : Finished archive generation.

#look to see if it worked
>ls | grep auditd
auditd
auditd-0.1.0.tar.gz
```

To run from the archive:
```
>inspec exec auditd-0.1.0.tar.gz

Profile: InSpec Profile (auditd)
Version: 0.1.0
Target:  local://

  System Package auditd
     ✔  should be installed

Test Summary: 1 successful, 0 failures, 0 skipped
```

### RUNNING ON A REMOTE SYSTEM
To run a profile remotely, you run **inspec exec** much like you do locally. However, you also specify the **-t** (target) argument to specify the URI of your target system.

### RUNNING ON A REMOTE SYSTEMS VIA SSH
Let's break down the target argument, ssh://root:password@target:
- ssh:// is the scheme. It specifies an SSH connection.
- root:password is the username and password for the account that permits SSH access. inspec exec also supports key-based authentication.
- target is the hostname of the target system. You could also specify a target system by its IP address.

Candidates should understand:

- Using inspec detect on a remote system.
- Using InSpec to scan a local Linux system using a remote (Github) profile.
```
inspec exec https://github.com/learn-chef/auditd/releases/download/v0.1.0/auditd-0.1.0.tar.gz

Profile: InSpec Profile (auditd)
Version: 0.1.0
Target:  local://

  System Package auditd
     ✔  should be installed

Test Summary: 1 successful, 0 failures, 0 skipped
```

- Using InSpec to scan a remote Linux system using a local profile.


- Using InSpec to scan a remote Linux system using a remote profile.
```
>inspec supermarket exec dev-sec/linux-baseline -t ssh://root:password@target

Profile: DevSec Linux Security Baseline (linux-baseline)
Version: 2.2.2
Target:  ssh://root@target:22

  ✔  os-01: Trusted hosts login
     ✔  File /etc/hosts.equiv should not exist
  ✔  os-02: Check owner and permissions for /etc/shadow
     ✔  File /etc/shadow should exist
     ✔  File /etc/shadow should be file
     ✔  File /etc/shadow should be owned by "root"
...-snip-...
Profile Summary: 14 successful controls, 2 control failures, 38 controls skipped
Test Summary: 52 successful, 4 failures, 38 skipped
```
- Using basic authentication to authenticate with a target system over SSH.
- Using keys to authenticate with a target system over SSH.
- Executing InSpec on a remote Linux system from the command line
- Outputting InSpec scan results as JSON.
The inspec exec command provides the --reporter argument, which transforms the output to a predefined format.

Run the following command to run the auditd profile on your target system and format the output as JSON. In this example, the output is piped to jq, which pretty-prints the output.
```
>inspec exec auditd --reporter=json | jq
{
  "platform": {
    "name": "ubuntu",
    "release": "16.04"
  },
  "profiles": [
    {
      "name": "auditd",
      "version": "0.1.0",
      "sha256": "9a0b08f182493acf3e4a89df6c4e20d65f6754cd3199285a5fa73352abd7b0bb",
      "title": "InSpec Profile",
      "maintainer": "The Authors",
      "summary": "An InSpec Compliance Profile",
      "license": "Apache-2.0",
      "copyright": "The Authors",
      "copyright_email": "you@example.com",
      "supports": [],
      "attributes": [],
      "groups": [
        {
          "id": "controls/example.rb",
          "controls": [
            "(generated from example.rb:1 a569767460cfcf7703e90eb97dbcc004)"
          ]
        }
      ],
      "controls": [
        {
          "id": "(generated from example.rb:1 a569767460cfcf7703e90eb97dbcc004)",
          "title": null,
          "desc": null,
          "impact": 0.5,
          "refs": [],
          "tags": {},
          "code": "",
          "source_location": {
            "line": 89,
            "ref": "/opt/inspec/embedded/lib/ruby/gems/2.4.0/gems/inspec-2.0.17/lib/inspec/control_eval_context.rb"
          },
          "results": [
            {
              "status": "passed",
              "code_desc": "System Package auditd should be installed",
              "run_time": 0.0211904,
              "start_time": "2018-09-10T09:49:16+00:00"
            }
          ]
        }
      ]
    }
  ],
  "statistics": {
    "duration": 0.0221925
  },
  "version": "2.0.17"
}

```

### RUNNING ON REMOTE SYSTEMS VIA WINRM
Candidates should understand:
- Using InSpec to scan a local Windows system using a local profile.
- Using InSpec to scan a local Windows system using a remote profile.
- Using InSpec to scan a remote Windows system using a local profile.
- Using InSpec to scan a remote Windows system using a remote profile.
- Authenticating with a target system over WinRM.

### RUNNING ON CONTAINERS
Candidates should understand:
- Using inSpec to scan a docker container using a local profile.
```
inspec exec auditd -t ssh://root:password@target

Profile: InSpec Profile (auditd)
Version: 0.1.0
Target:  ssh://root@target:22

  System Package auditd
     ×  should be installed
     expected that `System Package auditd` is installed

Test Summary: 0 successful, 1 failure, 0 skipped
```
- Using InSpec to scan a docker container using a remote profile.
- Authenticating with a docker container with InSpec.

### EXAMINING AN API ENDPOINT
Candidates should understand:
- The protocols you'd use to test a remote target
- What resource would you use to test URLs
- Implementing resource packs – e.g. AWS, Azure, VMWare.

### EXAMINING A DATABASE
Candidates should understand:
- What SQL database resources are available, and their matchers.
- How to execute an SQL query within a control.

## 4. CONTROLS AND METADATA
An InSpec control always contains at least one **describe block**. However, a control can contain _many describe blocks_.  

An InSpec test has two main components: _the subject to examine_ and the _subject's expected state_
Here's the format of a describe block.
```
describe <entity> do     # <entity> is the subject to examine. ex. a package name, service, file, or network port. 
  it { <expectation> }   # <expectation> specifies the expected state. ex. a port should be open or should not be open.
end
```

Default control created with **inspec init profile** PATH
```
>inspec init profile my_nginx
Create new profile at /root/my_nginx
 * Create directory controls
 * Create file controls/example.rb
 * Create file inspec.yml
 * Create directory libraries
 * Create file README.md
 
 >cat my_nginx/controls/example.rb
# encoding: utf-8
# copyright: 2018, The Authors

title 'sample section' 

# you can also use plain tests
describe file('/tmp') do                    
  it { should be_directory }                 
end

# you add 1 0r more controls here
control 'tmp-1.0' do                        # A unique ID for this control
  impact 0.7                                # The criticality, if this control fails.
  title 'Create /tmp directory'             # A human-readable title
  desc 'An optional description...'
  describe file('/tmp') do                  # The actual test
    it { should be_directory }
  end
end                                         # end of control 'tmp-1.0'
 
```
- **control** is followed by the control's name. Each control in a profile has a unique name- - .
- **impact** measures the relative importance of the test and must be a value between 0.0 an- d 1.0.
- **title** defines the control's purpose.
- **desc** provides a more complete description of what the control checks for.
- **describe** defines the test. Here, the test checks for the existence of the /tmp directory.
  - **file** is an InSpec resource.  The file resource provides the **be_directory** matcher.
  - **it** statement validates one of your resource's features
  - **should** asserts the condition that follows should be true.
  - **be_directory** is an example of a matcher. A matcher compares a resource's actual value to its expected value.
  
### Executing only specific controls
Use the **--controls** argument to run only certain controls.
For example in this case, the "package-09" control.

Run the **inspec exec** command again, this time specifying the **--controls package-09** argument.
```
inspec exec https://github.com/dev-sec/linux-baseline -t ssh://root:password@target --controls package-09

Profile: DevSec Linux Security Baseline (linux-baseline)
Version: 2.2.2
Target:  ssh://root@target:22

  ✔  package-09: CIS: Additional process hardening
     ✔  System Package prelink should not be installed


Profile Summary: 1 successful control, 0 control failures, 0 controls skipped
Test Summary: 1 successful, 0 failures, 0 skipped
```
You see only the results for the "package-09" control. As a bonus, the profile took less time to run.

### USING CONTROL METADATA
Candidates should understand:
- What a control's impact metadata defines.
- What a control's tag metadata defines.
- What a control's ref metadata defines.
- The format of a control's tag.
- If tag values are arbitrary or a closed set.
- If tags can be kay value pairs.
- Ranking the severity impact of each control using the impact metadata, i.e.
  - 0.7 - 1.0 Critical
  - 0.4 - <0.7 Major Issues
  - 0.1 - <0.4 Minor Issues
- Using refs to bridge the gap between documented compliance policies and executable code.

## 5. TROUBLESHOOTING
### USING THE INSPEC SHELL
Candidates should understand:
- What InSpec Shell is.
  - InSpec shell enables you to explore InSpec interactively
- Launching InSpec Shell
  - Run **inspec shell** to enter the interactive session.
```
>inspec shell
Welcome to the interactive InSpec Shell
To find out how to use it, type: help

You are currently running on:

    Name:      ubuntu
    Families:  debian, linux, unix
    Release:   16.04
    Arch:      x86_64

inspec>
```
- Using InSpec Shell.
Run **help** to see what commands are available
```
inspec> help
You are currently running on:

    Name:      ubuntu
    Families:  debian, linux, unix
    Release:   16.04
    Arch:      x86_64

Available commands:

    `[resource]` - run resource on target machine
    `help resources` - show all available resources that can be used as commands
    `help [resource]` - information about a specific resource
    `help matchers` - show information about common matchers
    `exit` - exit the InSpec shell

You can use resources in this environment to test the target machine. For example:

    command('uname -a').stdout
    file('/proc/cpuinfo').content => "value"
```
Run **help resources** to see which resources are available.
```
inspec> help resources
 - aide_conf
 - apache
 - apache_conf
 - apt
 - audit_policy
 - auditd
 - auditd_conf
 - aws_cloudtrail_trail
 - aws_cloudtrail_trails
 - aws_cloudwatch_alarm
 - aws_cloudwatch_log_metric_filter
 - aws_ec2_instance
 ...-snip-...
```
Run **help {resource]** for information about a specific resource
```
inspec> help aws_ec2_instance
Name: aws_ec2_instance

Description:

Verifies settings for an EC2 instance

Example:
    describe aws_ec2_instance('i-123456') do
  it { should be_running }
  it { should have_roles }
end
 describe aws_ec2_instance(name: 'my-instance') do
  it { should be_running }
  it { should have_roles }
end


Web Reference:

https://www.inspec.io/docs/reference/resources/aws_ec2_instance

```
- How you would invoke InSpec shell on a target over SSH
To invoke the InSpec shell on a target machine over ssh use the **-t** argument and the **ssh** scheme
```
>inspec shell -t ssh://root:password@target
Welcome to the interactive InSpec Shell
To find out how to use it, type: help

You are currently running on:

    Name:      ubuntu
    Families:  debian, linux, unix
    Release:   16.04
    Arch:      x86_64

inspec>
```

- Loading core resources into InSpec Shell.
- Loading custom resources into InSpec Shell.
