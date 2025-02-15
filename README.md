# EEOB/BCB546 Spring 2024 Course Repository

This repository will be used throughout the semester to host the files and documents used in the course. It is expected that you will pull all new changes to this directory at the beginning of each class so that you can work with the data and script files for the in-class activities and homework assignments. Additionally, this repository will store the syllabus and other documents. 

For general information about the course, lecture slides, and to find descriptions of the weekly class activities please see the main course website:

[https://eeob-biodata.github.io/EEOB-BCB-546](https://eeob-biodata.github.io/EEOB-BCB-546/)

## Cloning this Repository for the First Time

Before cloning this repository, we recommend that you first have an account on [GitHub](https://github.com/). The following instructions assume that you have Git installed and are working in a Unix-based operating system.

First, navigate to the directory that you would like to store the course repository, for example, you might want to keep all of the material for this course in a folder called `BCB546_2024` on your desktop:

```
cd Desktop/BCB546_2024
```

Now, you can clone the repository:

```
git clone git@github.com:EEOB-BioData/BCB546_Spring2024.git
```

Or you can use the HTTPS URL:

```
git clone https://github.com/EEOB-BioData/BCB546_Spring2024.git
```

Now you have access to all of the files currently in the repository.

## Pulling Changes

This repository will be updated frequently throughout the semester. Thus, to have the most up-to-date files, you should pull the changes before you start any activity. To do this, simply use the `git pull` command to pull the changes from the `main` branch on the remote host.

```
git pull origin main
```

Now all your files should be up-to-date. If you happened to have modified a file that is already in the repository (not common), then you may be unable to pull the changes. To find out which file you modified, check the status of your repository:

```
git status
```

This will then list the files that you have changed along with any files you have created in the repository. Look for the file that is indicated as `modified`. If you want to save the changes in this file, simply rename the file and then use `git checkout` to get the version currently on the remote host. 

For example, if you accidentally modified the file called `data.txt`, copy this file to a new location:

```
cp data.txt data_modified.txt
```

And then check out the unmodified file:

```
git checkout data.txt
```

## More Advanced Git Challenges

You will learn how to work with git in more detail in the early part of the course. If you have any issues, please contact the course instructors via Slack!
