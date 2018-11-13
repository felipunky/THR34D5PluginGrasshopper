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

The grib files give us information so that we can reconstruct a grid of coordinates in latitudes and longitudes, not all the files have more than one band, but for those that do, I have developed a component called "Get variable names from file" so that we can select an index for the "Read information from grib file", that does have a band input as an integer index. The bands correspond to the variables of the file and the first band is index number 1.

An overview of the GH definition:

1.) Extract and project data:
The THR34D5Workshop plugin has two sub-folders:

-Extract Data:

The coordinates in latitudes and longitudes are all the same for the whole file, so we don't need to specify a band for the "Calculate coordinates from file component". We only need a path, please no double quotes or it won't work.

We can use the "Get variable names from file", with the same path as our previous step, to understand what info is contained in each of the bands.

The last component is called "Read information from grib file", it needs the path as the last two components and the band, we can pick the band from our "Get variable names from file".
![thr34d5one](https://user-images.githubusercontent.com/21000020/48444250-65c42f00-e761-11e8-9124-26fe8e15265b.JPG)
    
-Projections: 

We have three projections:

-WebMercator

-Cassini

-Spherical

Their inputs are the latitudes and longitudes from the "Calculate coordinates from file component".
![thr34d5two](https://user-images.githubusercontent.com/21000020/48444249-65c42f00-e761-11e8-8d16-0f33ef62516c.JPG)

2.) Remap our data set values:

For our visualization purposes we need to remap our values from the "Read information from grib file" "DataSet" output:

The first remap gets our data for a colour gradient and the second for our heightmap, so the target domains are different.
![thr34d5three](https://user-images.githubusercontent.com/21000020/48445373-6b6f4400-e764-11e8-894e-ee79c6a7569a.JPG)

3.) Visualize:

![thr34d5four](https://user-images.githubusercontent.com/21000020/48445668-1bdd4800-e765-11e8-8b54-429f7b25fc31.JPG)

We use the Tarsier plugin to create a point-cloud, the point-cloud data structure is based on a kd-tree https://en.wikipedia.org/wiki/K-d_tree so it's faster than the built-in 3D Point structure that Grasshopper offers and it also allows us to add colour to the points.
![thr34d5five](https://user-images.githubusercontent.com/21000020/48445927-d66d4a80-e765-11e8-947c-f94b035c4a6d.JPG)

We also translate the points from one of the projections in the Z-Vector so that we can create an interesting Heightmap.
![thr34d5six](https://user-images.githubusercontent.com/21000020/48445926-d66d4a80-e765-11e8-98d4-5575a83fccfc.JPG)
