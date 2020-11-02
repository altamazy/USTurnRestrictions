# Introduction
-------------------
This data is freely available for download and use and contains 
1. 26,649 computer generated Turn Restrictions in the US based on NoLeft, NoRight and NoUTurn signs which are missing in OpenStreetMaps data drop form 10-29-2020. 
2. 9,296 computer generated Oneway Road Attributes in the US which are missing in OpenStreetMaps data drop form 10-29-2020.

# License
-------------------
This data is licensed by Microsoft under the [Open Data Commons Open Database License (ODbL)](https://opendatacommons.org/licenses/odbl/)

# FAQ
#### What does the data include?
1. 26,649 computer generated Turn Restrictions in the US based on NoLeft, NoRight and NoUTurn signs which are missing in OpenStreetMaps data drop form 10-29-2020. 
2. 9,296 computer generated Oneway Road Attributes in the US which are missing in OpenStreetMaps data drop form 10-29-2020.

#### What is the GeoJson format?
GeoJSON is a format for encoding a variety of geographic data structures. 
For Intensive Documentation and Tutorials, Refer to [GeoJson Blog](http://geojson.org/)

#### Creation Details:
The Turn Restriction generation is done in 150 steps:
1. Identifying OSM nodes which are potentially intersections.
2. Make pairs of incoming and outgoing streets at each intersection.
3. For each such pair select two street side images, one for capturing the view of the intersection from the incoming street and another one for capturing the outgoing streets.
4. Run Computer Vision Algorithm for detecting and turn restricting signs on those images, that is any "do not enter" signs in the latter image and any "no left", "no right", "no u turn" or "oneway" signs in the former image.
5. Make TR predictions based on the model's output.
6. Post processing, which includes conflation with existing Turn Restrictions in OSM and filtering out incorrect predictions.

### Scheme
![](/images/scheme.JPG)

#### CNN architecture
We train two models both with architectures based on [OverFeat] (https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Zhu_Traffic-Sign_Detection_and_CVPR_2016_paper.pdf) Network 
First model is trained on ~10000 images and detects the following signs in the images. 
![](/images/main_labels.JPG)
Secondary model is trained on additional ~1000 images and corrects the confusions with signs like
![](/images/secondary_labels.JPG)

#### Metrics
Precision and recall for pipeline's end-to-end performance are measured over an unbiased set of ~1500 intersections where traffic signs are detected. More accurate recall measurements are infeasible due to lack of ground true Turn Restrictions.
The overall metrics for the Turn Restriction generation pipeline are precision: 82.42%, recall: 97.40%, f1: 89.29%
The overall metrics for the Oneway Road Attributes generation pipeline are precision: 83.33%, recall: 78.94%, f1: 81.08%

#### Will there be more data coming for other geographies/other signs?
Yes, we are working on improving the measurements for Turn Restrictions based on "do not enter" signs. Traffic signs vary from country to country so model retraining is needed for obtaining predictions for a specific country. We have plans to do it for Australia.

#### Why is the data being released?
Microsoft has a continued interest in supporting a thriving OpenStreetMap ecosystem.

#### Number of Predictions for each US State

<table>
  <thead>
        <tr>
            <th>State</th> <th>Number of TR detections</th>  <th>Number of Oneway detections</th>
        </tr>
    </thead>
    <tbody>
<tr><td>Alabama</td> <td>110</td> <td>85</td></tr>
<tr><td>Arizona</td> <td>681</td> <td>97</td></tr>
<tr><td>Arkansas</td> <td>35</td> <td>40</td></tr>
<tr><td>Colorado</td> <td>442</td> <td>267</td></tr>
<tr><td>Connecticut</td> <td>244</td> <td>352</td></tr>
<tr><td>DC</td> <td>135</td> <td>25</td></tr>
<tr><td>Delaware</td> <td>109</td> <td>51</td></tr>
<tr><td>Florida</td> <td>2441</td> <td>490</td></tr>
<tr><td>Georgia</td> <td>343</td> <td>305</td></tr>
<tr><td>Idaho</td> <td>23</td> <td>45</td></tr>
<tr><td>Illinois</td> <td>755</td> <td>463</td></tr>
<tr><td>Indiana</td> <td>96</td> <td>107</td></tr>
<tr><td>Iowa</td> <td>85</td> <td>80</td></tr>
<tr><td>Kansas</td> <td>161</td> <td>123</td></tr>
<tr><td>Kentucky</td> <td>47</td> <td>35</td></tr>
<tr><td>Louisiana</td> <td>236</td> <td>131</td></tr>
<tr><td>Maine</td> <td>64</td> <td>34</td></tr>
<tr><td>Maryland</td> <td>443</td> <td>285</td></tr>
<tr><td>Massachusetts</td> <td>504</td> <td>340</td></tr>
<tr><td>Michigan</td> <td>859</td> <td>231</td></tr>
<tr><td>Minnesota</td> <td>383</td> <td>143</td></tr>
<tr><td>Mississippi</td> <td>19</td> <td>31</td></tr>
<tr><td>Missouri</td> <td>220</td> <td>123</td></tr>
<tr><td>Montana</td> <td>51</td> <td>145</td></tr>
<tr><td>Nebraska</td> <td>172</td> <td>91</td></tr>
<tr><td>Nevada</td> <td>255</td> <td>33</td></tr>
<tr><td>NewHampshire</td> <td>88</td> <td>62</td></tr>
<tr><td>NewJersey</td> <td>1095</td> <td>289</td></tr>
<tr><td>NewMexico</td> <td>102</td> <td>21</td></tr>
<tr><td>NewYork</td> <td>1874</td> <td>906</td></tr>
<tr><td>NorthernCalifornia</td> <td>3426</td> <td>372</td></tr>
<tr><td>NorthCarolina</td> <td>443</td> <td>309</td></tr>
<tr><td>NorthDakota</td> <td>60</td> <td>51</td></tr>
<tr><td>Ohio</td> <td>505</td> <td>518</td></tr>
<tr><td>Oklahoma</td> <td>82</td> <td>42</td></tr>
<tr><td>Oregon</td> <td>226</td> <td>107</td></tr>
<tr><td>Pennsylvania</td> <td>1259</td> <td>664</td></tr>
<tr><td>RhodeIsland</td> <td>59</td> <td>87</td></tr>
<tr><td>SouthernCalifornia</td> <td>5652</td> <td>327</td></tr>
<tr><td>SouthCarolina</td> <td>145</td> <td>210</td></tr>
<tr><td>SouthDakota</td> <td>6</td> <td>-</td></tr>
<tr><td>Tennessee</td> <td>145</td> <td>126</td></tr>
<tr><td>Texas</td> <td>895</td> <td>367</td></tr>
<tr><td>Utah</td> <td>114</td> <td>62</td></tr>
<tr><td>Vermont</td> <td>33</td> <td>46</td></tr>
<tr><td>Virginia</td> <td>763</td> <td>269</td></tr>
<tr><td>Washington</td> <td>461</td> <td>157</td></tr>
<tr><td>WestVirginia</td> <td>41</td> <td>61</td></tr>
<tr><td>Wisconsin</td> <td>254</td> <td>88</td></tr>
<tr><td>Wyoming</td> <td>9</td> <td>3</td></tr>
    </tbody>
</table>

# Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

# Legal Notices

Microsoft, Windows, Microsoft Azure and/or other Microsoft products and services referenced in the documentation
may be either trademarks or registered trademarks of Microsoft in the United States and/or other countries.
The licenses for this project do not grant you rights to use any Microsoft names, logos, or trademarks.
Microsoft's general trademark guidelines can be found at http://go.microsoft.com/fwlink/?LinkID=254653.

Privacy information can be found at https://privacy.microsoft.com/en-us/

Microsoft and any contributors reserve all other rights, whether under their respective copyrights, patents,
or trademarks, whether by implication, estoppel or otherwise.
