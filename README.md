# Interactive Visualization Using HTML

by Chengping Chai, Charles J. Ammon, Monica Meceria and Robert B. Herrmann

This package contains source code and data for several examples of plotting 3D seismic models using HTML. We are using Python 2.7 for this package. In two examples, we use a dispersion model from Herrmann et al. (2013, http://www.eas.slu.edu/eqc/eqc_research/NATOMO/) and a 3D shear velocity model from Chai et al. ([GRL](http://onlinelibrary.wiley.com/doi/10.1002/2015GL063733/full), 2015, also at http://eqseis.geosc.psu.edu/~cchai/01research/01westernUS.html). The dispersion data and velocity model are included in the folders RAYLU and WUS-CAMH-2015, respectively. Another example plot waveform using SAC files (data can be found in the folder WaveformData). Our plots also use political boundaries and coastlines data that are prepared with GMT (http://gmt.soest.hawaii.edu/). The boundary data for U.S. region are provided in the utility folder.

The python script plot_dispersion_as_html.py can be used to generate an interactive plot like WUS_dispersion_viewer.html in the Results folder. The python script plot_3D_model_as_html.py was used to generate a dynamic figure like WUS_model_viewer.html (in the Results folder). The script plot_waveform_as_html.py will plot seismograms from one event that are recorded on multiple three-component stations. The utility.py contains some Python functions used by the above scripts.

## Install Required Packages

The following python packages are required to generate interactive plots using our codes.

* numpy (version 1.10.4 or above)
* scipy (version 0.17.0 or above)
* bokeh (version 0.12.9 or above)
* obspy (version 1.0.3 or above)

Installation through Anaconda (or Miniconda) is highly recommended. You can find instructions on how to install Anaconda at https://docs.continuum.io/anaconda/install.

Once you have Anaconda installed, the required packages can be installed using these commands in the terminal.

```bash
conda install numpy
conda install scipy
conda install bokeh
conda config --add channels conda-forge
conda install obspy
```

## Run

To generate the HTML file with map views and dispersion curves for the dispersion model, type the following command in your terminal.

```bash
python plot_dispersion_as_html.py
```

The HTML file with map views and profile plots for the 3D velocity model can be generated by the command below.

```bash
python plot_3D_model_as_html.py
```

The HTML file with map views and cross-sections for the velocity model can be generated by the command below.

```bash
python plot_cross_sections_as_html.py
```

The command below can be used to generate the HTML file to show three-component seismograms and station locations.

```bash
python plot_waveforms_as_html.py
```


## Details on Velocity Model Viewer

The Python script plot_3D_model_as_html.py reads in the 3D velocity model from a text file, plots the velocity model using the Bokeh package and save the model parameters as well as visulization in a HTML file. 

### Work Flow

The following figure shows a flow-chats on how we design the script.   


### Format of the Text File (2015GL063733-ds02.txt)

The text file contains 900 1D velocity profles for 1-degree-by-1-degree cells. The cell starts from upper left corner of the study area and then across and down (like a book). Code oc and co are used to label ocean and continent, respectively. Each profile starts with a line looks like the following.

```bash
# Earth model for cell 001 (r,c) = (001,001) Lat: 54.500 Lon: -126.500 Code: co
```

For each profile, the first line is number of layers. In our example, the number of layers is 99. The lines followint the first line are model parameters for each layer. The first column is layer number. The second column is Vp in km/s. The third column is Vs in km/s. The 4th column is density in g/cm^3. The 5th column is layer thickness in km. The last column is depth from surface to the layer top in km. Other columns are not used.

![image](https://github.com/ccp137/DynamicViz/blob/master/Figures/Model_viewer.png)


### Available Options

In the Python script (plot_3D_model_as_html.py), we provide many customizable options in case you want to use this script for your own models. These options are saved as a Python dictionary (style_parameter) and can be changed in the main function. The following table lists these options. These options can be changed by editing the script. Optimal values of some parameters can be found by trying different values.

| Parameters of style_parameter | Functionality  |
| --- | ---|
| html_title | title of the HTML page tab |
| xlabel_fontsize | fontsize of x axis label |
| xtick_label_fontsize | fontsize of x axis ticks |
| title_font_size | fontsize of the figure title |
| annotating_text_font_size | fontsize of the annotating text |
| map_view_ndepth | number of depth (horizontal layers) |
| nlat | number of cells in latitude direction |
| nlon | number of cells in longitude direction |
| map_view_figure_lat_min | minimum latitude of the velocity map figure |
| map_view_figure_lat_max | maximum latitude of the velocity map figure |
| map_view_figure_lon_min | minimum longitude of the velocity map figure |
| map_view_figure_lon_max | maximum longitude of the velocity map figure |
| map_view_image_lat_min | minimum latitude of the velocity image |
| map_view_image_lat_max | maximum latitude of the velocity image |
| map_view_image_lon_min | minimum longitude of the velocity image |
| map_view_image_lon_max | maximum longitude of the velocity image |
| map_view_plot_width | width of the velocity map figure in pixel |
| map_view_plot_height | height of the velocity map figure in pixel |
| map_view_title | title of the velocity map figure |
| map_view_xlabel | x axis label of the velocity map figure |
| map_view_ylabel | y axis label fo the velocity map figure |
| map_view_tools | interactive tools used for the velocity map figure |
| map_view_default_index | depth index of the default (prior to clicking) velocity map |
| map_view_depth_label_lon | longitude to place the depth label |
| map_view_depth_label_lat | latitude to place the depth label |
| map_view_depth_box_lon | longitude of the background box beneath the depth label |
| map_view_depth_box_lat | latitude of the background box beneath the depth label |
| map_view_depth_box_width | width of the background box in pixel |
| map_view_depth_box_height | height of the background box in pixel |
| map_view_grid_width| width of the rectangles that represent the model grid |
| map_view_grid_height | height of the rectangles that represent the model grid | 
| spread_factor | a constant used to control the spread of color scale |
| min_vs_range | minimum spead allowed for the color scale |
| colorbar_title | title of the colorbar |
| colorbar_plot_height | height of the colorbar plot |
| profile_ndepth | number of layers used for the profile plot |
| profile_default_index | default index of the profile plot |
| profile_plot_width | width of the profile plot in pixel |
| profile_plot_height | height of the profile plot in pixel |
| profile_plot_xmin | minimum x of the profile plot |
| profile_plot_xmax | maximum x of the profile plot |
| profile_plot_ymin | minimum y of the profile plot |
| profile_plot_ymax | maximum y of the profile plot |
| profile_plot_tools | interactive tools used for the profile plot |
| profile_title | title of the profile plot |
| profile_lat_label_x | x of the latitiude label |
| profile_lat_label_y | y of the latitude label |
| profile_lon_label_x | x of the longitude label |
| profile_lon_label_y | y of the longitude label |
| profile_label_box_x | x of the background box for the latitude and longitude labels |
| profile_label_box_y | y of the background box for the latitude and longitude labels |
| profile_label_box_width | width of the background box in pixel |
| profile_label_box_height | width of the background box in pixel |
| depth_slider_title | title of the depth slider |
| profile_slider_title | title of the profile location slider |
| button_ndepth | number of depth allow for the text output |
| button_width | width of the data downloading buttons |
| simple_text_button_label | button label for the simple text button |
| model96_button_label | button label for the model96 button |
| annotation_plot_width | width of the annotating text at the bottom of the HTML page |
| annotation_plot_height | height of the annotating text at the bottom of the HTML page |
| annotating_html01 | content of the annotating text at the lower left corner |
| annotating_html02 | content of the annotating text at the lower right corner |
| left_column_width | width of the left part of the HTML page |
| right_column_width | width of the right part of the HTML page |
| library_source | include the Bokeh libraries in the HTML file (inline) or not (CDN) |
| vmodel_filename | filename of the 3D velocity model |
| html_filename | filename of the output HTML file |

### Known Limitations

* Map projections are not supported
* Slider value does not change with click

## Details on Dispersion Viewer



## Details on Waveform Viewer
