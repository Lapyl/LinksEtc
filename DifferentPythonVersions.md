# Using different versions of Python

On my Windows computer, I had Python 3.9.7 installed, with lots of Python packages installed during the last several years. Even though I knew about Python virtual environment, I had avoided using it, and relied solely on the main Python installation. Recently, I needed to use a specialized Python package. I found that this package was not yet available for Python 3.9.7; it was available for only up to Python 3.7.x. I then felt the need for using Python virtual environment or some other way that can allow me to use Python 3.7.x, without disrupting my Python 3.9.7 installation. The following is a description of what I did. I do not claim this to be the best way of doing, but it did and does serve my purpose. I hope it helps someone.

From python.org website, I downloaded .msi or .exe files for installing 2.7.18, 3.0.1, 3.1.4, 3.2.5, 3.3.5, 3.4.4, 3.5.4, 3.6.8, 3.7.9, 3.8.10, 3.9.13, 3.10.11, 3.11.6, and 3.12.0 versions of Python. I then installed these versions in G:\Python_2.7.18, …, G:\Python_3.12.0 folders.

I started an Excel file called PyPacks.xlsm. I renamed its first sheet as Note. In cell A1, I wrote the following, based on Python packages I have found useful in my Python works:

    pandas matplotlib scikit-learn tensorflow asgiref audioread Babel beautifulsoup4 bokeh Cirq cmake contourpy coremltools datasets Django easygui ffmpeg Flask folium glob2 gpt-index gradio gradio_client h5py httpcore json5 jupyter jupyter-client jupyter-console jupyter-core jupyter-server jupyterlab keras Keras-Preprocessing langchain langchainplus-sdk llama-index matplotlib matplotlib-inline mysql mysql-connector mysqlclient notebook numpy oauthlib openai openapi-schema-pydantic opencv-python opencv-python-headless openpyxl pandas path pathlib2 pathspec pdfreader Pillow plotly protobuf py Pygments qiskit qiskit-aer qiskit-ibmq-provider qiskit-terra qiskit-textbook QtPy regex requests requests-mock requests-ntlm requests-oauthlib responses scikit-image scikit-learn-intelex scikit-video scipy seaborn setuptools spyder spyder-kernels sqlparse tensorboard tensorboard-data-server tensorboard-plugin-wit tensorboardX tensorflow tensorflow-addons tensorflow-estimator tensorflow-hub tensorflow-io-gcs-filesystem tensorflowjs tensorspacejs tqdm transformers wxPython

In this Excel file, I added a VBA module, and added the following code.

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

I ran the MacInstallPythonPackages macro from this Excel file. It prepared E:\Jupyter\Versions\V2.7.18.py, …, E:\Jupyter\Versions\V3.12.0.py files.

I opened Visual Studio Code. Therein, I opened E:\Jupyter\Versions folder.

I opened V2.7.18.py file in Visual Studio Code. It showed the following text in the editor.

    #!G:/Python_2.7.18/python.exe
    print("Stated version: 2.7.18")
    print("Stated folder: G:\Python_2.7.18")
    import os, sys, subprocess
    sRes = str(sys.version_info)
    print("Inferred version: " + sRes)
    sRes = os.path.dirname(sys.executable)
    print("Inferred folder: " +  sRes)
    subprocess.check_call([sys.executable, "-m", "pip", "install", "pandas"])
    …
    subprocess.check_call([sys.executable, "-m", "pip", "install", "wxPython”])

I clicked the gear button in the left bottom corned, and then clicked Command Palette. From the header pull-down menu, I clicked “Terminal: Run Active File in Active Terminal”. This installed pandas, …, wxPython packages in Python 2.7.18 version, in the G:\Python_2.7.18\Lib\site-packages folder.

Thereafter, I opened V3.0.1.py file, I repeated the above steps.

I repeated all the above steps for all other V*.py files.
