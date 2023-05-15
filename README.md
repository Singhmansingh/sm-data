# Git Submodule Test
This is a test repo for learning how git submodules work. The other repos in this project are:

- [sm-primary](https://github.com/singhmansingh/sm-primary) - First frontend built with plain HTML and jquery
- [sm-secondary](https://github.com/singhmansingh/sm-secondary) - Second frontend build with plain HTML and tailwind
- [sm-data](https://github.com/singhmansingh/sm-data) - data repo of 10 fun facts from [https://uselessfacts.jsph.pl/](https://uselessfacts.jsph.pl/) 

## Data
This repo is the data file for the front ends. It will act as the submodule in this example. each repo will be able to import the data to a `/data` folder, so that the final directory will be `/data/data.json`.

## Submodules
A submodule allows you to have a folder within your git repo that connects to another repo. This allows you to work on different applications, while sharing a certain amount of data between them. In this case, we have 2 different frontends, that share the same `data`. Instinctively, two things come to mind:

Incorrect methods:
1. "Duplicate the files. Whenever a change is made, just share the json"
   - this is bad because it is time confusing, and if working with others, getting them to work on the same file manually is alot of effort
2. "create a sub git repo, and just ignore it in the parent"
   - This can cause issues if not handled exactly correctly, and nesting gits is frowned upon. It's also needlessly complex.

To do this, we use **Submodules**, which are a supported function by git that will syncronize the folder nicely, as well as track the reference on github correctly.

## How to use them

I highly reccomend this video by Cameron McKenzie on YouTube [Add git submodules to GitHub example](https://www.youtube.com/watch?v=eJrh5IjWSGM).


### Creating a Submodule

To build a submodule, follow these steps:

Upload each of your working folders to their own repositors **Without the submodule folder**. This example we have created:

   - [sm-primary](https://github.com/singhmansingh/sm-primary) - First frontend built with plain HTML and jquery
   - [sm-secondary](https://github.com/singhmansingh/sm-secondary) - Second frontend build with plain HTML and tailwind

   Both make refence to a `data/data.json` file, that does not exist. **That is intentional**.

Upload your submodule to its own repository. This example we have created:
   - [sm-data](https://github.com/singhmansingh/sm-data) - data repo of 10 fun facts from [https://uselessfacts.jsph.pl/](https://uselessfacts.jsph.pl/) 


### Importing a Submodule

In your frontends, import the submodule with the following lines of code

```bash
# sm-primary
git submodule pull <GIT_LINK_TO_YOUR_SUBMODULE> <NAME_OF_LOCAL_FOLDER>
```
This will create 2 files in your project:
```shell
**your submodule**
.gitmodules
```
The `.gitmodules` is the key here. That file will tell git that the folder is not a normal folder. If you are using VSCode, you will see an <strong style="color:#66829b;">S</strong> next to the folder. That means it is working correctly.

Once that is complete, you can commit the changes, and push them to your repo.

```bash
# adding the submodule folder and pushing
git add .
git commit -m "added submodule folder"
git push origin master
```

On github, you will see a link to your submodule report, like:
```bash
# folderName @ recentcommit
data @ 04544b8
```

You are now setup to use the submodule!

### Updating a Submodule
When you make changes to the submodule repo (`sm-data`, for example), you can do your normal add and pushes
```bash
# in sm-data local folder
git add .
git commit -m "updated data.json"
git push origin master
```

Where the difference is, is you need to use the following command in your main folders, to update.
```bash
# in sm-primary/sm-secondary local folder 
git submodule update --remote
```
doing a normal `git submodule update` will only update the **reference and meta**, not the files. You need  to use the `--remote` flag to update the files.

Once that is done, you will have the newest version of your submodle. you can run a normal add/commit to update your remote repo.
```bash
# in sm-primary/sm-secondary local folder 
git add .
git commit -m "updated submodule"
git push origin master
```

You will see your commit ID change.

And that's it! your submodule is now connected and you are ready to share your files!

