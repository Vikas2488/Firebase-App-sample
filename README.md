# Implementing CI/CD For Android App Development

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

This repo contains the DevOps pipeline to implement CI/CD for Android app deployment.

#### Workflow
- Trigger the Jenkins pipeline on code push using Github webhook.
- Spinning up the Docker container for executing build
- Generating build for andorid using fastlane and notify on each stage over slack.
- Uploading the build on Firebase app distribution
- Triggering Slack notification on successful build.

## Tech
For implementing complete workflow, this pipeline uses a number of open source projects to work properly:
- *[Jenkins]* - Open source automation server.
- *[Fastlane]* - An open source platform aimed at simplifying Android and iOS deployment.
- *[Firebase]* - firebase distribution for distributing the Android builds.
- *[Slack]* - Communication platform for notification
- *[Docker]* - Its a platform as a service, that use OS-level virtualization to deliver software in packages called containers.

## Installation
Creating build of app using fastlane requires [ruby](https://www.ruby-lang.org/en/documentation/installation/) v2.7.0+ to run.

- Install the dependencies

    ```sh
    $ sudo apt-get install ruby-full
    $ ruby --version
    ruby 2.7.0p0 (2019-12-25 revision 647ee6f091) [x86_64-linux-gnu]
    ```
- Install Bundler by running 
    ```sh 
    gem install bundler
    ```
- Create a ./Gemfile in the root directory of your project with the content
    ```sh
    source "https://rubygems.org"
    gem "fastlane"
    ```
- Run ```bundle update``` and add both the ./Gemfile and the ./Gemfile.lock to version control
- Every time you run fastlane, use ```bundle exec fastlane [lane]```
- On your CI, add ```bundle install``` as your first build step
- To update fastlane, just run ```bundle update fastlane```

##### Setting up fastlane
Navigate your terminal to your project's directory and run
```sh 
fastlane init
```

##### Firebase app distribution setup
https://firebase.google.com/docs/app-distribution/android/distribute-fastlane

##### Setting up jenkins
Installation Guide
https://www.digitalocean.com/community/tutorials/how-to-install-jenkins-on-ubuntu-18-04
