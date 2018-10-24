---
layout: default
---

##  FT_LAYOUTPLOT

Note that this reference documentation is identical to the help that is displayed in MATLAB when you type "help ft_layoutplot".

`<html>``<pre>`
    `<a href=/reference/ft_layoutplot>``<font color=green>`FT_LAYOUTPLOT`</font>``</a>` makes a figure with the 2-D layout of the channel positions
    for topoplotting and the individual channel axes (i.e. width and height
    of the subfigures) for multiplotting. A correct 2-D layout is a
    prerequisite  for plotting the topographical distribution of the
    potential or field distribution, or for plotting timecourses in a
    topographical arrangement.
 
    This function uses the same configuration options as prepare_layout and
    as the topoplotting and multiplotting functions. The difference is that
    this function plots the layout without any data, which facilitates
    the validation of your 2-D layout.
 
    Use as
    ft_layoutplot(cfg, data)
 
    There are several ways in which a 2-D layout can be made: it can be read
    directly from a *.lay file, it can be created based on 3-D electrode or
    gradiometer positions in the configuration or in the data, or it can be
    created based on the specification of an electrode of gradiometer file.
 
    You can specify either one of the following configuration options
    cfg.layout      = filename containg the layout
    cfg.rotate      = number, rotation around the z-axis in degrees (default = [], which means automatic)
    cfg.projection  = string, 2D projection method can be 'stereographic', 'ortographic', 'polar', 'gnomic' or 'inverse' (default = 'orthographic')
    cfg.elec        = structure with electrode definition
    cfg.grad        = structure with gradiometer definition
    cfg.elecfile    = filename containing electrode definition
    cfg.gradfile    = filename containing gradiometer definition
    cfg.output      = filename to which the layout will be written (default = [])
    cfg.montage     = 'no' or a montage structure (default = 'no')
    cfg.image       = filename, use an image to construct a layout (e.g. usefull for ECoG grids)
    cfg.visible     = string, 'yes' or 'no' whether figure will be visible (default = 'yes')
    cfg.box         = string, 'yes' or 'no' whether box should be plotted around electrode (default = 'yes')
    cfg.mask        = string, 'yes' or 'no' whether the mask should be plotted (default = 'yes')
 
    Alternatively the layout can be constructed from either
    data.elec     structure with electrode positions
    data.grad     structure with gradiometer definition
 
    Alternatively, you can specify
    cfg.layout = 'ordered'
    which will give you a 2-D ordered layout. Note that this is only suited
    for multiplotting and not for topoplotting.
 
    To facilitate data-handling and distributed computing you can use
    cfg.inputfile   =  ...
    If you specify this option the input data will be read from a *.mat
    file on disk. This mat files should contain only a single variable named 'data',
    corresponding to the input structure.
 
    See also `<a href=/reference/ft_prepare_layout>``<font color=green>`FT_PREPARE_LAYOUT`</font>``</a>`, `<a href=/reference/ft_topoplotER>``<font color=green>`FT_TOPOPLOTER`</font>``</a>`, `<a href=/reference/ft_topoplotTFR>``<font color=green>`FT_TOPOPLOTTFR`</font>``</a>`, `<a href=/reference/ft_multiplotER>``<font color=green>`FT_MULTIPLOTER`</font>``</a>`, `<a href=/reference/ft_multiplotTFR>``<font color=green>`FT_MULTIPLOTTFR`</font>``</a>`
`</pre>``</html>`
