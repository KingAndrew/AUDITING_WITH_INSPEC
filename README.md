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

### inspec.yml
Each profile must have an inspec.yml file that defines the following information:

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

### METADATA AND THE LOCK FILE
Candidates should understand:
- The purpose of the inspec.yml file.
- How an InSpec profile's name and version are defined.
- How to define profile dependencies.
- What it means to 'vendor' profiles.
- What the 'inspec.lock' file is.
- Updating the 'inspec.lock' file.
- Setting profile metadata.
- Managing updates from upstream profiles.
- Auditing with InSpec Page 3 v0.0.1

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
- Auditing with InSpec Page 4 v0.0.1
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
- Invoking InSpec to check a profile stored on a remote server via git.
- Invoking specific controls. 

### PACKAGING PROFILES
You can also package a profile as a compressed archive to make it easier to share. You can package profiles in tar.gz or zip format.  Before packaging your profiles check its validity with **inspec check**.  If it checks out package your profiles with the **inspec archive** PATH command.
```
>inspec archive auditd
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
[2018-09-09T14:44:38+00:00] WARN: Unrecognized content type: application/octet-stream. Assuming tar.gz

Profile: InSpec Profile (auditd)
Version: 0.1.0
Target:  local://

  System Package auditd
     ✔  should be installed

Test Summary: 1 successful, 0 failures, 0 skipped
```


- Using InSpec to scan a remote Linux system using a local profile.


- Using InSpec to scan a remote Linux system using a remote profile.
- Using basic authentication to authenticate with a target system over SSH.
- Using keys to authenticate with a target system over SSH.
- Executing InSpec on a remote Linux system from the command line
- Outputting InSpec scan results as JSON.

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
- Launching InSpec Shell
- Using InSpec Shell.
- How you would invoke InSpec shell on a target over SSH
- Loading core resources into InSpec Shell.
- Loading custom resources into InSpec Shell.
