# github_conglomerate
Brings together details of github repos across organisations

[![Build Status](https://travis-ci.org/sanger-pathogens/GithubConglomerate.svg?branch=master)](https://travis-ci.org/sanger-pathogens/GithubConglomerate)   
[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-brightgreen.svg)](https://github.com/sanger-pathogens/GithubConglomerate/blob/master/LICENSE)

## Contents
  * [Introduction](#introduction)
  * [Running the tests](#running-the-tests)
  * [Usage](#usage)
    * [Example output](#example-output)
    * [Web App](#web-app)
  * [License](#license)
  * [Feedback/Issues](#feedbackissues)

## Introduction
Some organisations choose to give each team their own github organisation to simplify administration. This is a bit of a pain when trying to find interesting software to reuse. This tool creates a Heroku hostable web app which uses the Github API to get a list of repos for each 'Github organisation' and amalgamate them into one nice view. For example, you can see many of the [Wellcome Sanger Institute's](https://github-conglomerate.herokuapp.com/) here.

The script is outlined below which collected the required data and puts it into a json formatted file. This should then be made accessible via a URL which a simple web app will query on startup.

## Running the tests

`./run_tests.sh`

or
`python setup.py test`

## Usage
```
get-repo-data --orgs sanger-pathogens wtsi-hgi \
              --github <api-token> \
              --output example_output.json
```
### Example output
```
cat example_output.json | python -m json.tool
```
Gives:
```
  {
    "created_at": "2015-03-29T23:12:29.573859", 
    "repos": [
      {
        "created_at": "2014-04-30T09:44:21", 
        "description": "de novo virus assembler of Illumina paired reads", 
        "forks_count": 1, 
        "html_url": "https://github.com/sanger-pathogens/iva", 
        "last_released": "2015-03-27T11:36:49+00:00", 
        "latest_release": "v0.11.5", 
        "name": "iva", 
        "organisation": "sanger-pathogens", 
        "release_count": 19, 
        "stargazers_count": 2, 
        "updated_at": "2015-03-27T11:36:49"
      }, 
      {
        "created_at": "2015-03-25T11:16:25", 
        "description": "Takes a jinja2 template and some json and sends an email", 
        "forks_count": 1, 
        "html_url": "https://github.com/sanger-pathogens/json2email", 
        "last_released": "2015-03-28T16:58:12+00:00", 
        "latest_release": "release/0.0.6", 
        "name": "json2email", 
        "organisation": "sanger-pathogens", 
        "release_count": 2, 
        "stargazers_count": 1, 
        "updated_at": "2015-03-28T16:58:12"
      },
      {
        loads more
      }
    ]
  }
```

You can also load data from YAML config files as follows:
```
  ---
  github_token: <api_token>
  github_organisations:
  - sanger-pathogens
  - wtsi-hgi
```
### Web App

You can start the web app using the following command and view the results at http://localhost:8080.

`./scripts/web.py`

You can set a Google Analytics token by creating an environment variable called GA_TOKEN with a token. On Heroku you'd do this with the following:

`heroku config:set GA_TOKEN="<your token here>"`

You then want to redeploy the app so that the new config is picked up.

## License
GithubConglomerate is free software, licensed under [GPLv3](https://github.com/sanger-pathogens/GithubConglomerate/blob/master/LICENSE).

## Feedback/Issues
Please report any issues to  path-help@sanger.ac.uk.