---
title: "Using Atlas with Continuous Integration"
---
## Using Atlas with continuous integration
![How Atlas works](/help-images/how-atlas-works.png)

Continuous integration tools like Jenkins or CircleCI are simple to integrate into the Atlas application delivery pipeline between the Code and Build steps. Use the [Atlas Upload CLI](https://github.com/hashicorp/atlas-upload-cli) to push application code from the CI tool after a completed build to Atlas. Below is an example `.travis.yml` configuration that uses the Atlas Upload CLI to send code to Atlas:

	after_success:
	    - echo "Build Successful"
	    - sudo apt-get -y install golang
	    - mkdir -p $PROJECT_ROOT/mygo
	    - export GOPATH=$PROJECT_ROOT/mygo
	    - go get github.com/hashicorp/atlas-upload-cli
	    - cd $GOPATH/src/github.com/hashicorp/atlas-upload-cli/
	    - make
	    - ./bin/atlas-upload ATLAS_USERNAME/APP_NAME $PROJECT_ROOT/app

This builds the Atlas Upload CLI and then sends the application code to Atlas. Be sure to update `ATLAS_USERNAME` and `APP_NAME` with the respective values. This will create an application in your Atlas account. If you [link the application to a build configuration](https://atlas.hashicorp.com/help/getting-started/run-your-application), anytime a new application is pushed from your CI tool to Atlas, it will automatically start a build and output new deployable artifacts.

**Note:** For Travis CI, you need to encrypt your Atlas token and set it as an environment variable — [read here](https://github.com/hashicorp/atlas-examples/tree/master/TravisCI) for a full Travis/Atlas integration guide. 
