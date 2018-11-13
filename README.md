# THR34D5PluginGrasshopper
Plugin for retrieving and visualizing data from the NCEP

# Install:
1.) Download the files in this repository as a zip to your computer, unzip it.

2.) Select all the unzipped files that end with a .dll and copy them. 

3.) Go to the location where Rhino.exe is, it should be on C:\Program Files\Rhinoceros 5.0 (64-bit)\System

4.) Paste all the dll's.

5.) Go to where you unzipped all the repository's files, copy all the files that end up in .gha

6.) Paste them in your Grasshopper's library's folder, it generally is at C:\Users\Felipe\AppData\Roaming\Grasshopper\Libraries note that in your case "Felipe" should be your user name.

7.) To test I normally use the "Get Variable Names From File", it should be in the THR34D5Workshop plugin tab:
    In the left input "PathToFile" connect a panel with the path to a grib2 file (Trick: on Windows click one time your file, then press    Shift and Right-Click, now you should see "Copy as path"), note: the path shouldn't have any double quotes.
    You should see something like this:
    ![ghwsplugin](https://user-images.githubusercontent.com/21000020/48441067-95226e00-e758-11e8-9ba3-fdc1668bedfa.JPG)

# Sample Definition:
In this repository there is a GH file: THR34D5.gh

It relies on only two plugins: THR34D5Workshop that is in this repository with its installation guide. And Tarsier that you can get from Food4Rhino: https://www.food4rhino.com/app/tarsier
