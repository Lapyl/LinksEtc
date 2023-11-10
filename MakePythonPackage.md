<<<<<<< HEAD
## Make Python Package

Refer: https://packaging.python.org/en/latest/guides/distributing-packages-using-setuptools/

- In your local GitHub folder, create <packagetopfolder> folder with the following content.

    <packagetopfolder>
        <packagesubfolder>
            __init__.py
            <otherreferencedfiles>
            <staticfilesfolder>
                __init__.py
                <staticfiles>
        LICENSE
        README.md
        setup.py
        <build>
        <dist>
        <pypi>

- In Visual Studio Code (VSC), open <packagetopfolder> folder.

- Make appropriate changes in various files.

- In setup.py file, add:

  package_data = {'<packagesubfolder>'": ["<somestatics>/**/*",],}

- Check that the code works in VSC.

- In VSC, at command prompt, at <packagetopfolder>, run the following to generate <packagesubfolder>-<versionnumber>.tar.gz and <packagesubfolder>-<versionnumber>-py3-none-any.whl files in dist folder.

  python -m build --sdist

  python -m build --wheel

- In VSC, at command prompt, at <packagetopfolder>, run the following to install <packagesubfolder> package in active Python installation.

  pip install dist/<packagesubfolder>-<versionnumber>-py3-none-any.whl

- Using Jupyter Notebook, verify that the installed package works as expected.

- Make changes if and as necessary.
=======
https://packaging.python.org/en/latest/guides/distributing-packages-using-setuptools/

- In your local GitHub folder, create <packagetopfolder> folder for <packagename>.

- In Visual Studio Code (VSC), open the <packagetopfolder> folder folder.

- In <packagetopfolder> folder, create <packagesubfolder> subfolder, and LICENSE, README.md, and setup.py files.

- In <packagesubfolder> subfolder, create __init__.py file, with the necessary code.

- If <packagesubfolder> subfolder contains <staticssubfolder> subfolder with some static files:
-- In <staticssubfolder> subfolder, create blank __init__.py file.
-- In setup.py file, add " package_data = {'<packagesubfolder>'": ["<somestatics>/**/*",],} ".

- Check that the code works in VSC.

- In VSC, at command prompt, run " python -m build --sdist ", to generate " dist/<packagename>-<versionnumber>.tar.gz " file.

- In VSC, at command prompt, run " python -m build --wheel ", to generate " dist/<packagename>-<versionnumber>-py3-none-any.whl " file.

- In VSC, at command prompt, run " pip install dist/<packagename>-<versionnumber>-py3-none-any.whl ", to install <packagename> package in your Python installation.

- Using Jupyter Notebook, verify that the installed package works as expected; and if necessary, make appropriate changes.
>>>>>>> c15c450480ced27c37a49138f1c2078abebfbaee

- From GitHub desktop, upload this local repository to your remote GitHub account.

- At PyPi.org, create your account, if not already done.

<<<<<<< HEAD
- In VSC, at command prompt, at <packagetopfolder>, run the following to upload dist/\* to your PyPi.org account.

  twine upload dist/\*

- Verify the package got uploaded to PyPi.org .

- Move files from dist folder to PyPi folder, to prevent errors during next upload.

- On some other computer, pip install <packagesubfolder>, and verify that it works.
=======
- In VSC, at command prompt, run " twine upload dist/* ", to upload the <package> to your PyPi.org account.

- Verify the package uploaded to PyPi.org .

- On some other computer, run " pip install <packagename ", and verify that it works.
-  
>>>>>>> c15c450480ced27c37a49138f1c2078abebfbaee
