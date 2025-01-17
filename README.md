# @sharmanikhil04/nexus-deployer

## Why this repo?

This repo is a fork of https://github.com/cthorne66/nexus-deployer.

It was forked to update dependencies and keep this upto date, especially prevent security issues due to dependencies of this repository.

> Nexus Artifact Deployer from grunt

[![Build Status](https://travis-ci.org/cthorne66/nexus-deployer.png)](https://travis-ci.org/cthorne66/nexus-deployer) 
[![npm version](https://badge.fury.io/js/nexus-deployer.svg)](http://badge.fury.io/js/nexus-deployer)
[![Dependency Status](https://david-dm.org/cthorne66/nexus-deployer.png)](https://david-dm.org/cthorne66/nexus-deployer)
## Getting Started

To install
```shell
npm install nexus-deployer --save-dev
```

From there, you have options

1. Run with Node
2. Run with Gulp
2. Run with Grunt

## Running with Node

```js
var deployer = require('nexus-deployer');

var release = {
    groupId: 'nexus-deployer',
    artifactId: 'nexus-deployer',
    version: '1.0',
    packaging: 'zip',
    auth: {
      username:'admin',
      password:'admin123'
    },
    pomDir: 'build/pom',
    url: 'http://localhost:8081/nexus/content/repositories/releases',
    artifact: 'build/nexus-deployer.zip',
    noproxy: 'localhost',
    cwd: ''
};


deployer.deploy(release, function(){
    // your async call back here
    // done();
});

```


## Running with Gulp

```js
var deployer = require('nexus-deployer');

// dont forget to create a task to actually generate the artifact as assumed
// here with the dependent 'artifacts:generate' task
gulp.task('deploy:artifacts', ['artifacts:generate'], function(callback) {
  
    var snapshot = {
        groupId: 'nexus-deployer',
        artifactId: 'nexus-deployer',
        version: '1.2-SNAPSHOT',
        packaging: 'zip',
        auth: {
            username:'admin',
            password:'admin123'
        },
        pomDir: 'build/pom',
        url: 'http://localhost:8081/nexus/content/repositories/snapshots',
        artifact: 'build/nexus-deployer.zip',
        noproxy: 'localhost',
        cwd: '',
        quiet: false,
        insecure: true
    };

    deployer.deploy(snapshot, callback);

});
```


## Running with Grunt
This plugin requires Grunt `~0.4.2`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:



Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('nexus-deployer');
```

## The "nexusDeployer" task

### Overview
In your project's Gruntfile, add a section named `nexusDeployer` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  nexusDeployer: {
    release: {
      options: {
		  groupId: "nexus-deployer",
		  artifactId: "nexus-deployer",
		  version: "1.0",
		  packaging: 'zip',
                  classifier: 'dev',
		  auth: {
			username:'admin',
			password:'admin123'
		  },
		  pomDir: 'build/pom',
		  url: 'http://localhost:9220/nexus/content/repositories/releases',
		  artifact: 'build/nexus-deployer.zip',
		  noproxy: 'localhost',
		  cwd: ''
		}
      }
    }
});
```

### Options

#### options.groupId
Type: `String`
Default value: `''`

The group owning the artifact.

#### options.artifactId
Type: `String`
Default value: `''`

The artifact id of the artifact.

#### options.packaging
Type: `String`
Default value: `''`

Type of artifact. eg zip, jar, pom, war etc.

#### options.classifier
Type: `String`
Defaut value: `''`

An optional classifier that can further distinguish between artifacts of the same group, id and version. eg dev, prod etc. (i.e. artifact-1.0-dev.zip, artifact-1.0-prod.zip)

#### options.version
Type: `String`
Default value: `''`

Version of the artifact being uploaded. Ensure you have your versions ending with -SNAPSHOT when an artifact is being uploaded to snapshot repository. Often artifact repositories
have that restriction.

#### options.auth.password
Type: `String`
Default value: `''`

Password to be used for authentication against nexus server


#### options.auth.username
Type: `String`
Default value: `''`

Username to be used for authentication against nexus server

#### options.insecure
Type: `boolean`
Default value: `false`

Accept Self-Signed certificates when connecting over https.

#### options.url
Type: `String`
Default value: `''`

Nexus repository url. Usually /nexus/content/repositories/snapshots or /nexus/content/repositories/releases


#### options.artifact
Type: `String`
Default value: `''`

Artifact to be uploaded. Must be a file.

#### options.noproxy
Type: `String`
Default value: `'127.0.0.1'`

list of comma separated addresses to exclude for which proxy is not applicable. This is a must when running proxy and HTTP_PROXY environment value is set.

#### options.cwd
Type: `String`
Default value: `''`

working directory from which deployer will deploy artifacts.


#### options.parallel
Type: `Boolean`
Default value: `'false'`

Whether to upload artifacts in parallel.


#### options.quiet
Type: `Boolean`
Default value: `'false'`

Chatty flag.

### Usage Examples
Deploy to release repository

```js
grunt.initConfig({
  nexusDeployer: {
    release: {
      options: {
		  groupId: "nexus-deployer",
		  artifactId: "nexus-deployer",
		  version: "1.0",
		  packaging: 'zip',
		  auth: {
			username:'admin',
			password:'admin123'
		  },
		  pomDir: 'build/pom',
		  url: 'http://localhost:8081/nexus/content/repositories/releases',
		  artifact: 'build/nexus-deployer.zip',
		  noproxy: 'localhost',
		  cwd: ''
		}
      }
    }
});
```

Deploy to snapshots repository

```js
grunt.initConfig({
  nexusDeployer: {
    release: {
      options: {
		  groupId: "nexus-deployer",
		  artifactId: "nexus-deployer",
		  version: "1.0-SNAPSHOT",
		  packaging: 'zip',
		  auth: {
			username:'admin',
			password:'admin123'
		  },
		  pomDir: 'build/pom',
		  url: 'http://localhost:8081/nexus/content/repositories/snapshots',
		  artifact: 'build/nexus-deployer.zip',
		  noproxy: 'localhost',
		  cwd: '',
		  parallel:false,
		  quiet: true
		}
      }
    }
});
```

To run
```
grunt nexusDeployer
```

## Release History