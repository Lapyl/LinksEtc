## Different Python Versions

The following is a possible non-virtual-environment approach for having different Python versions.

Download .msi or .exe files for 2.7.18, 3.0.1, 3.1.4, 3.2.5, 3.3.5, 3.4.4, 3.5.4, 3.6.8, 3.7.9, 3.8.10, 3.9.13, 3.10.11, 3.11.6, and 3.12.0 versions of Python.

Install these versions in Python_2.7.18, …, Python_3.12.0 subfolders in <TopFolder> folder.

Prepare an Excel file named PyPacks.xlsm.

Rename the xlsm file's first sheet as Note.

In the xlsm file's A1 cell, write names of useful Python packages.

    pandas matplotlib scikit-learn tensorflow asgiref audioread Babel beautifulsoup4 bokeh Cirq cmake contourpy coremltools datasets Django easygui ffmpeg Flask folium glob2 gpt-index gradio gradio_client h5py httpcore json5 jupyter jupyter-client jupyter-console jupyter-core jupyter-server jupyterlab keras Keras-Preprocessing langchain langchainplus-sdk llama-index matplotlib matplotlib-inline mysql mysql-connector mysqlclient notebook numpy oauthlib openai openapi-schema-pydantic opencv-python opencv-python-headless openpyxl pandas path pathlib2 pathspec pdfreader Pillow plotly protobuf py Pygments qiskit qiskit-aer qiskit-ibmq-provider qiskit-terra qiskit-textbook QtPy regex requests requests-mock requests-ntlm requests-oauthlib responses scikit-image scikit-learn-intelex scikit-video scipy seaborn setuptools spyder spyder-kernels sqlparse tensorboard tensorboard-data-server tensorboard-plugin-wit tensorboardX tensorflow tensorflow-addons tensorflow-estimator tensorflow-hub tensorflow-io-gcs-filesystem tensorflowjs tensorspacejs tqdm transformers wxPython

In the xlsm file, add a VBA module with the following code.

    Option Explicit
    Sub MacInstallPythonPackages()
        Dim sPks As String, sDir As String
        Dim sVer As Variant, sPkg As Variant
        Dim oFso As New FileSystemObject
        Sheets("Note").Select
        sPks = Cells(1, 1)
        sDir = "E:/Jupyter/Versions"
        If oFso.FolderExists(sDir) Then oFso.DeleteFolder sDir
        oFso.CreateFolder sDir
        For Each sVer In Array("2.7.18", "3.0.1", "3.1.4", "3.10.11", "3.11.6", "3.12.0", "3.2.5", "3.3.5", "3.4.4", "3.5.4", "3.6.8", "3.7.9", "3.8.10", "3.9.13")
            Open sDir & "/V" & sVer & ".py" For Output As #1
            Print #1, "#!G:/Python_" & sVer & "/python.exe"
            Print #1, "print(""Stated version: " & sVer & """)"
            Print #1, "print(""Stated folder: G:\Python_" & sVer & """)"
            Print #1, "import os, sys, subprocess"
            Print #1, "sRes = str(sys.version_info)"
            Print #1, "print(""Inferred version: "" + sRes)"
            Print #1, "sRes = os.path.dirname(sys.executable)"
            Print #1, "print(""Inferred folder: "" +  sRes)"
            For Each sPkg In Split(sPks, " ")
                Print #1, "subprocess.check_call([sys.executable, ""-m"", ""pip"", ""install"", """ & sPkg & """])"
            Next
            Close #1
        Next
        Set oFso = Nothing
        MsgBox "Done"
    End Sub

Run the MacInstallPythonPackages macro from this xlsm file, to prepare E:\Jupyter\Versions\V2.7.18.py, …, E:\Jupyter\Versions\V3.12.0.py files.

In Visual Studio Code (VSC), open E:\Jupyter\Versions folder.

In VSC, open V2.7.18.py file, which will show the following.

    #!G:/Python_2.7.18/python.exe
    print("Stated version: 2.7.18")
    print("Stated folder: G:\Python_2.7.18")
    import os, sys, subprocess
    sRes = str(sys.version_info)
    print("Inferred version: " + sRes)
    sRes = os.path.dirname(sys.executable)
    print("Inferred folder: " + sRes)
    subprocess.check_call([sys.executable, "-m", "pip", "install", "pandas"])
    …
    subprocess.check_call([sys.executable, "-m", "pip", "install", "wxPython”])

In VSC's left bottom, click the gear button, and then click Command Palette. From the header pull-down menu, click “Terminal: Run Active File in Active Terminal”.

This will install pandas, …, wxPython packages in Python 2.7.18 version, in the G:\Python_2.7.18\Lib\site-packages folder.

Repeat the above steps for other Python versions.
