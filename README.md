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