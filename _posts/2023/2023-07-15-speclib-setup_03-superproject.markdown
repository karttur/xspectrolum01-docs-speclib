---
layout: post
title: "Spectral system setup: 3. Super project structure"
categories: "xspectrolum-setup"
excerpt: "Setup of the xspectrolum spectral system; part 3: repository project structure, submoduls and super project"
tags:
  - GitHub
  - repo
  - submodules
  - super project
image: ts-mdsl-rntwi_RNTWI_id_2001-2016_AS
date: '2023-07-17 11:27'
modified: '2024-01-13 T17:17:25.000Z'
comments: true
share: true
---

## Introduction

The xspectrolum spectral processing system consists of approximately a dozen python packages linked together. To maintain and manage the structure, individual packages are stored as separate submodules (repos) on GitHub. They are then linked together in a super project. The principles for developing submodules as an umbrella super project is outlined in detail in my post on [GitHub Submodules with git](https://karttur.github.io/geoimagine03-docs-main/develop/develop-submodules-from-git/).

 If you want to dive deeper into submodules and super projects try out: [Using submodules in Git - Tutorial](https://www.vogella.com/tutorials/GitSubmodules/article.html), [Git Submodules basic explanation](https://gist.github.com/gitaarik/8735255), [Working with submodules](https://github.blog/2016-02-01-working-with-submodules/) or the youtube introduction [Git Tutorial: All About Submodules](https://www.youtube.com/watch?v=8Z4Cmhji_FQ).

## Prerequisites

To follow the instructions in this post you need a [GitHub](https://github.com) account.

To create a fully functional Spectral Processing System you must also have installed the the Apps covered in the [previous post](../speclib-setup-02appsetup/index.html).

## Python packages repositories

The first step is to create all the repositories for the individual python packages. The approach I use for that is to give all the repos with individual packages a double name:

xspectrolumXX-"package"

where the prefix is composed of two parts: the name _xspectrolum_ and then a version number (_XX_) then a hyphen ("-") followed by the name of the actual python package. In January 2023, the Processing System (version 01) is composed of the following packages/repos:

| package | repository |
| setup_db | xspectrolum01p-setup_db |
| setup_processes | xspectrolum01p-setup_processes |
| ancillary | xspectrolum01p-ancillary |
| campaign | xspectrolum01p-campaign |
| common | xspectrolum01p-common |
| importlight | xspectrolum01p-importlight |
| importmuzzlerefspectra | xspectrolum01p-importmuzzlerefspectra |
| importprobe | xspectrolum01p-importprobe |
| importprobedata | xspectrolum01p-importprobedata |
| importsensor | xspectrolum01p-importsensor |
| importspectra | xspectrolum01p-importspectra |
| importspectrometer | xspectrolum01p-importspectrometer |
| params | xspectrolum01p-params |
| plotspectra | xspectrolum01p-plotspectra |
| postgresdb | xspectrolum01p-postgresdb |
| project | xspectrolum01p-project |
| support | xspectrolum01p-support |
| userproj | xspectrolum01p-userproj |
| xspectplot | xspectrolum01p-xspectplot |



### Create repos

To create the repos listed above, open your [GtHub](https://github.com) account in your web-browser. Then manually create all the repos as outlined in the post on [git cheat sheet](https://karttur.github.io/git-vcs/git/blog-git-cheat-sheet/). You must also clone all the repos manually using the <span class='terminalapp'>git clone</span> command.

Each created repo will only contain two visible files: <span class='file'>README.md</span> and <span class='file'>LICENCE</span>. The next step is to add the python package code belonging to each repo. This can either be done by manual copy/paste from your locally developed IDE, or using the python module <span class='module'>submodule_stage-commit-push_script</span>. This module (or script) is part of the Framework itself, available in the <span class='package'>support</span> package. The script copies a list of python packages from one directory tree to another. If the target file already exist it is overwritten if the source file in more recent. The script also creates a predefined <span class='file'>.gitignore</span>. As the script is not dependent on any other part of the Framework, you can just copy and paste it from under the <span class='button'>Hide/Show</span> button.

<button id= "togglesrcipt" onclick="hiddencode('script')">Hide/Show submodule_stage-commit-push_script.py</button>

<div id="script" style="display:none">

{% capture text-capture %}
{% raw %}
```
'''
Created on 12 Feb 2021

@author: thomasgumbricht
'''

# Standard library imports

import os, shutil

import  time

import datetime

import csv

def CopyProject():
    ''' Copy project updates to local GitHub clone
    '''

    for item in submoduleL:

        submoduleGitHubDirName = '%s-%s' %(prefix,item)

        dstRootFP = os.path.join(gitHubFP,submoduleGitHubDirName)

        print ("copying updates for package", item)

        srcFP = os.path.join(srcProjectFP,item)

        for subdir, dirs, files in os.walk(srcFP, topdown=True):

            files = [f for f in files if not f.endswith('pyc')]

            for file in files:

                print ('file',file)

                srcFPN = os.path.join(subdir,file)

                if not os.path.isfile(srcFPN):

                    continue

                if file in ignoreL:

                    continue

                if file[0] == '.':

                    continue

                srcFPN = os.path.join(srcFP, subdir, file)

                print (srcFPN)

                print ('subdir',subdir)

                dstSubdir = os.path.split( subdir.replace(srcFP,'') )[1]

                print ('dstSubdir',dstSubdir)

                if len(dstSubdir) > 0:

                    dstFP =  os.path.join(dstRootFP,  dstSubdir)

                    if not os.path.isdir(dstFP):

                        print ('dstRootFP',dstRootFP)

                        print ('dstFP',dstFP)

                        os.makedirs(dstFP)

                else:

                    dstFP = dstRootFP

                dstFPN =  os.path.join(dstFP, file)

                print ('dstFPN',dstFPN)

                try:

                    srcTime = datetime.datetime.fromtimestamp( int(os.path.getmtime(srcFPN)) )

                    dstTime = datetime.datetime.fromtimestamp( int(os.path.getmtime(dstFPN)) )

                    if int( os.stat(srcFPN).st_mtime) <= int(os.stat(dstFPN).st_mtime):

                        continue

                except OSError:

                    pass

                    print ('error - target probably non-existing')

                print ('    copying', item, file, dstFPN)

                print ('')

                shutil.copy(srcFPN, dstFPN) #copying from source to destination

        # Create .gitignore if it does not exist, or overwrite is set to true       
        gitignoreFPN = os.path.join(dstRootFP,'.gitignore')

        if not os.path.isfile( gitignoreFPN ) or overwriteGitIgone:

            with open(gitignoreFPN, 'w', encoding='UTF8', newline='') as f:

                writer = csv.writer(f)

                # write multiple rows
                writer.writerows(gitignore)


def WriteScript():
    ''' Write script that loops over all the repos and stage, commit and push
    '''

    shF = open(scriptFPN, 'w')

    for item in submoduleL:

        submoduleGitHubDirName = '%s-%s' %(prefix,item)

        FP = os.path.join(gitHubFP,submoduleGitHubDirName)

        cdCmd = 'cd %s\n' %(FP)

        shF.write(cdCmd)

        shF.write('echo "${PWD}"\n')

        stageCmd = 'git add .\n'

        shF.write(stageCmd)

        commitCmd = 'git commit -m "%s"\n' %(commitMsg)

        shF.write(commitCmd)

        pushCmd = 'git push origin %s\n' %(branch)

        shF.write(pushCmd)

        shF.write('\n')

    shF.close()

    print ('Script file:', scriptFPN)

if __name__ == "__main__":

    copyProject = True

    overwriteGitIgone = True

    branch = 'main'

    commitMsg = 'updates oct 2021'

    ignoreL = ['__pycache__','.DS_Store','README.md']

    home = os.path.expanduser('~')

    scriptFPN = os.path.join(home, 'submodule_stage_commit_push.sh')

    srcProjectFP = '/Users/thomasgumbricht/eclipse-workspace/2020-03_geoimagine/karttur_v202003/geoimagine'

    gitHubFP = '/Users/thomasgumbricht/GitHub/'

    gitHubAccount = 'karttur'

    prefix = 'geoimagine03'

    gitignore = [['.DS_Store'],['__pycache__/']]

    submoduleL = ['ancillary','assets','basins','copernicus',
                  'dem','export','extract',
                  'gis','grace','grass','ktgdal',
                  'ktgrass','ktnumba',
                  'ktpandas','landsat','layout',
                  'modis','npproc',
                  'params','postgresdb','projects',
                  'region','sentinel',
                  'setup_db','setup_processes','smap','support',
                  'timeseries','updatedb','userproj',
                  'zipper']

    if copyProject:

        CopyProject()

    WriteScript()
```

{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

### Create the superproject repo

To create the superproject repo that will contain the python frame package, return to your online [GtHub](https://github.com) account and create another repo with only a <span class='file'>README.md</span> and a <span class='file'>LICENCE</span>. There is no need for a strict naming, in this example I named it _xspectrolum01superproj_, without any hyphen. To separate it from the submodules. Clone the superproject repo to your local machine with the command <span class='terminalapp'>git clone</span>.

#### Link the submodules to the superproject

The <span class='terminalapp'>git</span> command for linking other repos as submodules is [<span class='terminalapp'>git submodule add</span>](https://git-scm.com/book/en/v2/Git-Tools-Submodules). The command expects a url link to a repo; by default the name of the submodule will be identical to the original repo, but by adding a second variable the name can be customised. For the xspectrolum processing system, the name should be set to the actual name of the python package. Thus the command for using the repo _xspectrolum01p-setup_db_ as a submodule in the superproject becomes:

<span class='terminal'>$ git submodule add https://github.com/karttur/xspectrolum01p-setup_db setup_db</span>

Instead of writing the commands for adding all the individual package repos, the script _submodule_stage-commit-push_script.py_ (above) generates the shell script code for adding all. To execute the script, open a <span class='app'>Terminal</span> window and change directory <span class='terminal'>cd</span> to the superproject repo, for example:

<span class='terminal'>$ cd /Users/thomasgumbricht/GitHub/xspectrolum01superproj</span>

and execute the <span class='terminalapp'> git submodule add</span> script.

### Working with the superproject

The superproject and the linked modules can be managed using a set of specific git command., outlined in my post on [Managing superprojects](https://karttur.github.io/git-vcs/git/git-managing-superproject/).

### Cloning superproject into Eclipse

To clone the superproject and all its linked packages to Eclipse you can either use Eclipse builtin git commands or create an empty Eclipse project and clone the superproject using ordinary git commands.

#### Cloning a superproject from within Eclipse

See my post on [Git clone with Eclipse and no project](https://karttur.github.io/geoimagine03-docs-main/putinplace/putinplace-clone-eclipse-no-proj/).
