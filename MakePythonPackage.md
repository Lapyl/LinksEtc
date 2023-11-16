## To make and release a Python package

Refer: https://packaging.python.org/en/latest/guides/distributing-packages-using-setuptools/

In your local GitHub folder, create <packagetopfolder> folder with the following content.

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

In Visual Studio Code (VSC), open <packagetopfolder> folder.

Make appropriate changes in various files.

In setup.py file, add:

    package_data = {'<packagesubfolder>'": ["<somestatics>/**/*",],}

Check that the code works in VSC.

In VSC, at command prompt, at <packagetopfolder>, run the following to generate dist/<packagesubfolder>-<versionnumber>.tar.gz .

    python -m build --sdist

In VSC, at command prompt, at <packagetopfolder>, run the following to generate dist/<packagesubfolder>-<versionnumber>-py3-none-any.whl .

    python -m build --wheel

In VSC, delete existing files in pypi folder, and copy the latest .tr.gz and .whl files from dist folder to pypi folder.

In VSC, at command prompt, at <packagetopfolder>, run the following to install <packagesubfolder> package in active Python installation.

    pip install pypi/<packagesubfolder>-<versionnumber>-py3-none-any.whl

Using Jupyter Notebook, verify that the installed package works as expected.

Make changes if and as necessary.

From GitHub desktop, upload this local repository to your remote GitHub account.

At PyPi.org, create your account, if not already done.

In VSC, at command prompt, at <packagetopfolder>, run the following to upload dist/\* to your PyPi.org account.

    twine upload pypi/\*

Verify the package got uploaded to PyPi.org .

Move files from dist folder to PyPi folder, to prevent errors during next upload.

On some other computer, pip install <packagesubfolder>, and verify that it works.
