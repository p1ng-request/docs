---
description: Latest version 1.1.1
---

# 👍 Updates

## Version

### Get

the version number in your local machine

```python
import naas
naas.version()
```

### Are you at the last version?

```python
import naas

naas.up_to_date()
```

### Get remote version

the last version number in Github

```python
import naas
naas.get_last_version()
```

## To get the latest version 

### In Naas cloud

```python
import naas
naas.update()
```

### In your local machine

```python
!pip install --upgrade naas
```

## Changelog

### 0.17.1 \(2020-11-09\)

#### Fix

* auto\_update

### 0.17.0 \(2020-11-09\)

#### Feat

* build without naas\_driver image but package

### 0.16.2 \(2020-11-05\)

#### Fix

* proxy add function

### 0.16.1 \(2020-11-05\)

#### Fix

* notification and test

### 0.16.0 \(2020-11-05\)

#### Feat

* **notifications**: add auth in notif
* **domain**: add domain config proxy system

### 0.15.1 \(2020-11-04\)

#### Fix

* **runner**: allow form and json

### 0.15.0 \(2020-11-04\)

#### Feat

* **runner**: add form request

### 0.14.0 \(2020-11-02\)

#### Feat

* add post capability

### 0.13.0 \(2020-10-27\)

#### Feat

* add doc function

### 0.12.6 \(2020-10-27\)

#### Fix

* doc add publish

### 0.12.5 \(2020-10-27\)

#### Fix

* remove update description

### 0.12.4 \(2020-10-27\)

#### Fix

* workflow build

### 0.12.3 \(2020-10-25\)

#### Fix

* messange notif send

### 0.12.2 \(2020-10-22\)

#### Fix

* loggers tests

### 0.12.1 \(2020-10-22\)

#### Fix

* sort and on manager

### 0.12.0 \(2020-10-21\)

#### Feat

* add page system in manager

### 0.11.0 \(2020-10-21\)

#### Feat

* add update command

### 0.10.1 \(2020-10-20\)

#### Fix

* add user email in sentry

### 0.10.0 \(2020-10-20\)

#### Feat

* allow select sender email

### 0.9.0 \(2020-10-16\)

#### Feat

* **scheduler**: ✨ allow chaining scheduler

### 0.8.6 \(2020-10-16\)

#### Fix

* build version python 3.8

### 0.8.5 \(2020-10-15\)

#### Fix

* **manager**: 🐛 fis is production function

### 0.8.4 \(2020-10-14\)

#### Fix

* **manager**: ✨ add is\_production method

### 0.8.3 \(2020-10-13\)

#### Fix

* **binder**: 🐛 use new folder for binder

### 0.8.2 \(2020-10-12\)

#### Fix

* Licence switch to AGPL

### 0.8.1 \(2020-10-11\)

#### Fix

* **manager**: 📝 remove verbosity

### 0.8.0 \(2020-10-11\)

#### Feat

* **notification**: ✨ allow multi emails by list or string

#### Fix

* **notification**: 🐛 fix type of date json to data when file are send
* **notification**: 🐛 fix send file with email
* **api**: 🐛 fix respond image remove mimetype

### 0.7.0 \(2020-10-08\)

#### Feat

* **notification**: ✨ allow send file in notification

### 0.6.7 \(2020-10-08\)

#### Fix

* **runner**: 🐛 set feature in bs4 to remove warning

### 0.6.6 \(2020-10-08\)

#### Refactor

* **manager**: 🏗️ simplify way to get production assets

### 0.6.5 \(2020-10-07\)

#### Fix

* remove mimetype response image args

### 0.6.4 \(2020-10-07\)

#### Fix

* 🐛 add upgrade before install

### 0.6.3 \(2020-10-07\)

#### Fix

* 💚 add pr titlevalidation

### 0.6.2 \(2020-10-06\)

#### Fix

* 💚 use good ref to build

### 0.6.1 \(2020-10-05\)

### 0.6.0b3 \(2020-10-04\)

### 0.6.0b2 \(2020-10-04\)

#### Fix

* ci for master

### 0.6.0b1 \(2020-10-04\)

#### Fix

* try to trigger ci again

### 0.6.0b3 \(2020-10-04\)

### 0.6.0b2 \(2020-10-04\)

#### Fix

* ci for master

### 0.6.0b1 \(2020-10-04\)

#### Fix

* try to trigger ci again

### 0.6.0b2 \(2020-10-04\)

#### Fix

* ci for master

### 0.6.0b1 \(2020-10-04\)

#### Fix

* try to trigger ci again

### 0.6.0b1 \(2020-10-04\)

#### Fix

* try to trigger ci again
* ci version docker machine
* try to trigger ci again
* tag format
* ci error in tag name

### v6.0.0b0 \(2020-10-04\)

#### Fix

* ci use version who work really with pre release
* remove bump in dev

### 0.6.0b0 \(2020-10-04\)

### v6.0.0b0 \(2020-10-04\)

#### Fix

* ci use version who work really with pre release
* remove bump in dev

### 0.5.26 \(2020-10-03\)

#### Fix

* 🐛 remove old workflow ref in reademe

### 0.5.25 \(2020-10-02\)

#### Fix

* 🐛 change filepath

### 0.5.24 \(2020-10-02\)

#### Fix

* 🐛 fix test with new debug params

### 0.5.23 \(2020-10-02\)

#### Fix

* 🐛 fix add prod function

### 0.5.22 \(2020-10-01\)

#### Fix

* 📝 remove useless doc and ractor it

### 0.5.21 \(2020-10-01\)

#### Fix

* 🐛 remove useless code in binder

### 0.5.20 \(2020-10-01\)

#### Fix

* 🐛 fix binder clone

### 0.5.19 \(2020-10-01\)

#### Fix

* 🐛 add missing shebang on binder script

### 0.5.18 \(2020-10-01\)

#### Fix

* 🐛 fix binder boot

### 0.5.17 \(2020-10-01\)

#### Fix

* 🐛 fix sonar cloud error

### 0.5.16 \(2020-10-01\)

#### Fix

* 🐛 update code for sonar cloud + fix bugs

### 0.5.15 \(2020-10-01\)

#### Fix

* 🐛 improve assets test + fix error on delete

### 0.5.14 \(2020-10-01\)

#### Refactor

* ♻️ improve code with sonar cloud

### 0.5.13 \(2020-10-01\)

#### Fix

* 🐛 add missing attribute in html

### 0.5.12 \(2020-10-01\)

#### Fix

* 🐛 fix html error

### 0.5.11 \(2020-10-01\)

#### Fix

* 🐛 fix typo in test assets

### 0.5.10 \(2020-10-01\)

#### Fix

* 🐛 fix test in assets

### 0.5.9 \(2020-09-30\)

#### Fix

* 🐛 fix assets path allow set extension

### 0.5.8 \(2020-09-30\)

#### Fix

* 🐛 fix notif status icon url

### 0.5.7 \(2020-09-30\)

#### Fix

* 🐛 add alt image

### 0.5.6 \(2020-09-30\)

#### Fix

* 🐛 fix url in logo notification

### 0.5.5 \(2020-09-30\)

#### Fix

* 🐛 fix url on manager in notification

### 0.5.4 \(2020-09-30\)

#### Fix

* 🐛 fix in notebook render and notif

### 0.5.3 \(2020-09-30\)

#### Fix

* 🐛 typo on var name

### 0.5.2 \(2020-09-30\)

#### Fix

* 🐛 fix notification

### 0.5.1 \(2020-09-30\)

#### Fix

* 🐛 render notebook filepath

### 0.5.0 \(2020-09-30\)

#### Feat

* ✨ add feature to render result notebook !

### 0.4.25 \(2020-09-30\)

#### Fix

* 📝 add our first doc and fix some typo in print

### 0.4.24 \(2020-09-30\)

#### Refactor

* 🚚 rename send\_notif to send\_status

### 0.4.23 \(2020-09-30\)

#### Fix

* 🐛 fix delete job command

### 0.4.22 \(2020-09-30\)

#### Fix

* 🐛 add to home

### 0.4.21 \(2020-09-30\)

#### Fix

* 🐛 use good vars for emails notifications

### 0.4.20 \(2020-09-29\)

#### Fix

* 🐛 fix bug in df jobs

### 0.4.19 \(2020-09-29\)

#### Fix

* 🐛 change path of codecov

### 0.4.18 \(2020-09-29\)

#### Fix

* 🐛 fix syntax setup

### 0.4.17 \(2020-09-29\)

#### Fix

* 🐛 run test only on latest python for now

### 0.4.16 \(2020-09-29\)

#### Fix

* make all test pass

### 0.4.15 \(2020-09-29\)

#### Fix

* 🐛 fix pytest for runner

### 0.4.14 \(2020-09-29\)

#### Fix

* 🐛 use right var for update dockerdescription

### 0.4.13 \(2020-09-29\)

#### Fix

* 👷 use new pip version install

### 0.4.12 \(2020-09-29\)

#### Fix

* ci change wrong vars in workflow

### 0.4.11 \(2020-09-29\)

#### Fix

* ci auto publish docker

### 0.4.10 \(2020-09-29\)

#### Fix

* ci add qemu

### 0.4.9 \(2020-09-29\)

#### Fix

* ci add auto update description

### 0.4.8 \(2020-09-29\)

#### Fix

* ci for docker release

### 0.4.7 \(2020-09-29\)

#### Fix

* ci bump version

### 0.4.6 \(2020-09-29\)

#### Fix

* ci add deploy package step
* ci change token

### 0.4.5 \(2020-09-29\)

#### Fix

* ci add get\_version action

### 0.4.4 \(2020-09-29\)

#### Fix

* ci merge job for pypip deploy
* ci merge job for pypip deploy

### 0.4.3 \(2020-09-29\)

#### Fix

* ci make ci release on pypip

### 0.4.2 \(2020-09-29\)

#### Fix

* 🐛 when notebook notfound add missing key duration in error return

### 0.4.1 \(2020-09-28\)

#### Fix

* 🐛 remove duplicate job at boot and disable them

### 0.4.0 \(2020-09-28\)

#### Fix

* 🐛 add missing function for neg naas jobs
* ⚡ auto cleanup jobs at each restart
* 🐛 test
* 🐛 fix route name
* 🐛 fix error when empty dff
* 🐛 swtich to no deamon
* 🐛 switch back to python3
* 🐛 fix docker build
* 🐛 fix scheduler race function
* 🐛 rename static in assets
* 🐛 fix concurent call scheduler
* 🐛 fix scheduler functions
* 🐛 fix error in scheduler when check if notebook already run
* 🐛 use b64 font
* 🐛 add missing dep sentry
* 🐛 fix font in svg logo
* 🎨 alow more naas\_ statics
* 🐛 fix error handler
* 🎨 change how to call naas features
* 🐛 make scheduler work in async
* ✏️ change reccurence to recurrence
* 🐛 fix api call for csv

#### Refactor

* 🔥 remove redirect options since it's not necessary anymore

### 0.1.0 \(2020-09-23\)

#### Feat

* ✨ allow lab redirect from manager

### 0.0.24 \(2020-09-23\)

### 0.0.22 \(2020-09-23\)

#### Fix

* 🔧 fix version file

#### Refactor

* 💄 better loader naas manager

