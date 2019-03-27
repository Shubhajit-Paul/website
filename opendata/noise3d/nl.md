---
layout: page_noise3d
title: 3D Basisbestand Geluid
permalink: /opendata/noise3d/nl
is_dutch: true
---

![](/img/projects/noise3d_banner.jpg)

<div class="well"><b>Feedback Sessie op 11 April 2019</b><br/><br/>
Op 11 April 2019 organiseren we een feedback sessie bij het Kadaster in Rotterdam (10:00-12:00). In deze sessie zullen we toelichten hoe het versie 0.2 van het Basisbestand 3D Geluid tot stand is gekomen en staan we open voor feedback.

U kunt zich aanmelden met <a href="https://docs.google.com/forms/d/e/1FAIpQLSdlVlcyZ-vCFcH5KYUKeSWgd7MX7t0msp4dL3wnKpD0fiHAPg/viewform">dit formulier</a>.
</div>

- - -

* Table of Content
{:toc}

- - -
## Introduction

In a collaboration of Rijkswaterstaat, RIVM, Kadaster and the 3D geoinformation research group from TU Delft, we are investigating how 3D data on noise sources and the environment, as required in legally prescribed noise studies, can be automatically generated for the whole of the Netherlands from existing data such as the Key Register Addresses and Buildings (BAG), the Basic Register for Large-Scale Topography (BGT) and the airborne LiDAR point cloud covering the whole of The Netherlands (AHN). 

This is an ongoing project that was started in 2017. A more detailed project description can be found [here]({{ "/projects/noise3d/" | prepend: site.baseurl  }})

On this site we publish an example dataset that is generated using the current 0.2 version of our method. With this sample dataset interested parties have the possibility to review our results and send us feedback.

## Method and example data

Our method aims to achieve high detail and accuracy, while keeping the resulting files small and adhering to the requirements and limitations of the currently available noise simulation software on the market. With version 0.2 we deliver 3 input layers for 3D noise studies, namely

1. building models (gebouwen),
2. ground types with noise reflection/absorption factors (bodemvlakken), and
3. terrain (hoogtelijnen).

These three input layers were generated fully automatically from the public BAG, BGT and AHN3 datasets and are explained in more detail below. We also investigated noise barriers (geluidsschermen) and bridges (bruggen), however these are not part of the v0.2 example dataset.

The study area of the sample dataset spans the *37ez2*, *37fz1*, *37gn2*, and *37hn1* AHN tiles nearby the city of Rotterdam as illustrated below.

![Sample area v0.2]({{ "testarea_v02_extent.png" | prepend: site.baseurl }})


### Building models

In the current noise simulation practice each building, regardless of its roof shape, is modelled with a single height level. The resulting block-shaped building representation is called *LoD1.0*. Modelling a building with only a single height can lead to large errors in the modelled height in case the building in reality consists of different parts that each have a very different height. Therefore, we have investigated how to automatically create building models in which multiple height levels are possible, i.e. using the *LoD1.3* representation.

We offer three alternative data sets with building models, *LoD1.0*, *LoD1.3* and *LoD1.3 experimental* (see graphic below). 

1. In the *LoD1.0* data set each building is modelled with a single height value. 
2. In the *LoD1.3* data set the buildings with *only* horizontal roofparts are modelled with multiple heights. To achieve this the footprint is subdivided into several roofparts and each roofpart is assigned its own height. Buildings with slanted roofs are modelled with a single height.
3. In the *LoD1.3 experimental* dataset, also the buildings with slanted roofparts are modelled with multiple heights. These buildings are the most difficult to model in *LoD1.3*, and these results are merely indicative of the current status of our LoD1.3 building reconstruction method. We intend to further improve this method in the near future.

The height of each roofpart is computed by taking a percentile of the elevations points it contains. We offer both a 75th percentile and a 95th percentile variant.

![Sample area v0.2]({{ "building_lod.png" | prepend: site.baseurl }})

More details about our LoD1.3 reconstruction method can be found in the following slideshow.

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vTooIsoh8wN8nbd_xv4YOgo0blfdm7dSG4NSpIvgL5meQ4yz4YiL1n3TGjvdpJea20x1e6r-E0woeDc/embed?start=false&loop=false&delayms=3000" frameborder="0" width="480" height="299" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

### Downloads

For the sample area we prepared the following data sets:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;border:none;}
.tg td{padding:10px 5px;border-style:solid;border-width:0px;overflow:hidden;word-break:normal;}
.tg th{font-weight:normal;padding:10px 5px;border-style:solid;border-width:0px;overflow:hidden;word-break:normal;}
.tg .tg-fymr{font-weight:bold;border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-pcvp{border-color:inherit;text-align:left;vertical-align:top;background-color: #ecf0f1;}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-fymr">Feature</th>
    <th class="tg-fymr">Explanation</th>
    <th class="tg-fymr">File name</th>
    <th class="tg-fymr">Download</th>
  </tr>
  <tr>
    <td class="tg-pcvp">ground type</td>
    <td class="tg-pcvp">Ground types classified by their noise reflecting property. Objects that are smaller than 6 square meters are merged into their neighbour and obtain the neighbour's reflectance property.</td>
    <td class="tg-pcvp">&lt;tile id&gt;_bodemvlakken</td>
    <td class="tg-pcvp">
      <a href="{{ "bodemvlakken.zip" | prepend: "/download/noise3d/v02/" | prepend: site.baseurl }}">[ESRI Shapefile]</a><br/>
    </td>
  </tr>
  <tr>
    <td class="tg-0pky">terrain<br></td>
    <td class="tg-0pky">Terrain modelled with 3D lines (not contour lines and not breaklines)</td>
    <td class="tg-0pky">&lt;tile id&gt;_hoogtelijnen</td>
    <td class="tg-0pky">
      <a href="{{ "hoogtelijnen.zip" | prepend: "/download/noise3d/v02/" | prepend: site.baseurl }}">[ESRI Shapefile]</a><br/>
      </td>
  </tr>
  <tr>
    <td class="tg-pcvp">building in LoD1.0</td>
    <td class="tg-pcvp">Bulding footprints with a single height value per building. The height of the building model is computed as the 75th and 95th percentile of the points that are part of the roof.</td>
    <td class="tg-pcvp">&lt;tile id&gt;_lod10_&lt;percentile&gt;</td>
    <td class="tg-pcvp">
      <a href="{{ "lod10.zip" | prepend: "/download/noise3d/v02/" | prepend: site.baseurl }}">[ESRI Shapefile]</a><br/>
      </td>
  </tr>
  <tr>
    <td class="tg-0pky">building in LoD1.3</td>
    <td class="tg-0pky">Bulding footprints with a single height value per <em>building-part</em>. The height of the building model is computed as the 75th and 95th percentile of the points that are part of the roof. If the building has slanted roof surfaces (<code>dak_type</code> is <code>2</code>), then it is reconstructed in LoD1.0.</td>
    <td class="tg-0pky">&lt;tile id&gt;_lod13_&lt;percentile&gt;</td>
    <td class="tg-0pky">
      <a href="{{ "lod13.zip" | prepend: "/download/noise3d/v02/" | prepend: site.baseurl }}">[ESRI Shapefile]</a><br/>
      </td>
  </tr>
  <tr>
    <td class="tg-pcvp">building in LoD1.3 (experimental version)</td>
    <td class="tg-pcvp">Bulding footprints with a single height value per <em>building-part</em>. The height of the building model is computed as the 75th and 95th percentile of the points that are part of the roof. If the building has slanted roof surfaces (<code>dak_type</code> is <code>2</code>), then it is reconstructed in LoD1.3.</td>
    <td class="tg-pcvp">&lt;tile id&gt;_lod13_&lt;percentile&gt;_experimenteel</td>
    <td class="tg-pcvp">
      <a href="{{ "lod13_experimenteel.zip" | prepend: "/download/noise3d/v02" | prepend: site.baseurl }}">[ESRI Shapefile]</a><br/>
      </td>
  </tr>
</table>


### Attributes

The table below describes the attributes of the *buildings* and *ground types* data sets. The lines in the *terrain* data set do not have attributes.

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;border:none;}
.tg td{padding:10px 5px;border-style:solid;border-width:0px;overflow:hidden;word-break:normal;}
.tg th{font-weight:normal;padding:10px 5px;border-style:solid;border-width:0px;overflow:hidden;word-break:normal;}
.tg .tg-fymr{font-weight:bold;border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-pcvp{border-color:inherit;text-align:left;vertical-align:top;background-color: #ecf0f1;}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-fymr">Feature</th>
    <th class="tg-fymr">Attribute</th>
    <th class="tg-fymr">Explanation</th>
  </tr>
  <tr>
    <td class="tg-0pky">building</td>
    <td class="tg-0pky">bag_id</td>
    <td class="tg-0pky">the <code>identificatie</code> attribute from the BAG</td>
  </tr>
  <tr>
    <td class="tg-0pky"></td>
    <td class="tg-pcvp">dak_type</td>
    <td class="tg-pcvp">type of the roof of building<br>
      <code>2</code> – roof with at least one slanted surface<br>
      <code>1</code> – roof with multiple, only horizontal surfaces<br>
      <code>0</code> – roof with a single horizontal surface<br>
      <code>-1</code> – no AHN point was found for the building<br>
      <code>-2</code> – could not detect a roof surface, even though AHN points were found
      </td>
  </tr>
  <tr>
    <td class="tg-0pky"></td>
    <td class="tg-0pky">hoogte_abs</td>
    <td class="tg-0pky"><em>hoogte absolute</em> or absolute height of the building (height measure from NAP)</td>
  </tr>
  <tr>
    <td class="tg-0pky"></td>
    <td class="tg-pcvp">maaiveld_h</td>
    <td class="tg-pcvp"><em>maaiveld hoogte</em> or absolute ground height of the building</td>
  </tr>
  <tr>
    <td class="tg-0pky"></td>
    <td class="tg-0pky">maaiveld_p</td>
    <td class="tg-0pky"><em>aantal maaiveld punten</em> or number of AHN points that were used for calculating the ground height. Note that a value below 3 might indicate an unreliable value for <code>maaiveld_h</code></td>
  </tr>
  <tr>
    <td class="tg-0pky"></td>
    <td class="tg-pcvp">ahn_geldig</td>
    <td class="tg-pcvp">or valid height<br>
      <code>1</code> – building was built <em>before</em> the point cloud was collected for the tile<br>
      <code>0</code> – building was built <em>after</em> the point cloud was collected for the area
    </td>
  </tr>
  <tr>
    <td class="tg-0pky" style="border-bottom-width:0.5px"></td>
    <td class="tg-0pky" style="border-bottom-width:0.5px">ahn_datum</td>
    <td class="tg-0pky" style="border-bottom-width:0.5px">the date of the acquisition of the point cloud for the tile</td>
  </tr>
  <tr>
    <td class="tg-0pky">ground type</td>
    <td class="tg-0pky">uuid</td>
    <td class="tg-0pky">unique ID of the object</td>
  </tr>
  <tr>
    <td class="tg-0pky" style="border-bottom-width:0.5px"></td>
    <td class="tg-pcvp" style="border-bottom-width:0.5px">demping</td>
    <td class="tg-pcvp" style="border-bottom-width:0.5px">sound reflectance property of the ground<br>
      <code>hard</code> – reflecting<br>
      <code>zacht</code> – non-reflecting
    </td>
  </tr>
  <tr>
    <td class="tg-0pky">terrain</td>
    <td class="tg-0pky">-</td>
    <td class="tg-0pky">-</td>
  </tr>
</table>

## Feedback Form
In case of questions or comments about the data please fill out our [feedback form](https://docs.google.com/forms/d/e/1FAIpQLSfgWxv-5xdSWcEAxmmu6tnzwlc9fw6N-wHQuJLnnSNJv2NCtg/viewform).


- - -

# Project partners

{% include noise3d/partners.html %}