## To create an interactive Html on GitHub through Binder

Refer: https://www.nbinteract.com/tutorial/tutorial_github_setup.html

Go to your GitHub repositories.

Create a new repo, titled as InteractiveHtml or something, with readme or some starting content.

Go to mybinder.org .

Write "https://github.com/{GHusername}/{GHreponame}" for GitHub repository name.

Click Launch. This opens "https://hub.mybinder.org/user/{GHusername}-{GHreponame}-{somecode}/tree" in Jupyter notebook.

From the "tree notebook", click New and click Terminal. This opens "https://hub.mybinder.org/user/{GHusername}-{GHreponame}-{somecode}/terminals/1" in Jupyter notebook.

In the "terminal notebook", enter the following commands.

    pip install nbinteract
    nbinteract init
    ? [Y/n] ? Y
    git add -A
    git commit -m "Setup nbinteract"
    git config --global user.email "{GHaccountemail}"
    git config --global user.name "{GHaccountdisplayname}"
    git push origin master
    ? Username for 'https://github.com' ? {GHusername}
    ? Password ? {GHpassword}

This creates configuration files on Binder and pushes them to GH repo.

From the "tree notebook", click New and click Python3. This opens "https://hub.mybinder.org/user/{GHusername}-{GHreponame}-{somecode}/notebooks/Untitled.ipynb" in Jupyter notebook.

Save this "content notebook" as {SomeName}.ipynb.

In the "content notebook", add some content.

In the "content notebook", in the cell to import packages, write:

    from ipywidgets import interact

In the "content notebook", in a cell to add a function, write:

    def {SomeFunction} ({SomeArguments}):
        _ _ _
    return {SomeReturn}

In the "content notebook", in a cell to get an interactive widget, write:

    interact({SomeFunction}, {SomeArguments}={SomeValues})

In the "content notebook", run all the cells.

If you get ModuleNotFoundError wrror, in the "terminal notebook", enter the following commands.

    pip install {MissingModule}

In the "content notebook", confirm that all cells have run clearly.

In the "terminal notebook", enter the following commands.

    nbinteract {SomeName}.ipynb

This creates {SomeName}.html fils on Binder.

In the "terminal notebook", enter the following commands.

    git add -A
    git commit -m "Setup nbinteract"
    git push origin master
    ? Username for 'https://github.com' ? {GHusername}
    ? Password ? {GHpassword}

This creates additional fils on Binder and pushes them to GH repo.

In an Internet browser, go to:

    {GHusername}.github.io/{GHreponame}/{SomeName}.html
