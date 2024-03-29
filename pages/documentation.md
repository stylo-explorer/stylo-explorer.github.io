---
layout: page
title:
---

<h1><a id="TOC">Documentation</a></h1><br>
<h2>Table of Contents</h2>

<div style="text-indent:10px;"><a href="#Quickstart">1. Quickstart</a></div>

<div style="text-indent:10px;"><a href="#Explorer">2. Rolling Stylometry Explorer</a></div>

<div style="text-indent:22px;"><a href="#Minimap">2.1. Minimap</a></div>

<div style="text-indent:22px;"><a href="#Settings">2.2. Settings</a></div>

<div style="text-indent:22px;"><a href="#ColorLegend">2.3. Color Legend</a></div>

<div style="text-indent:22px;"><a href="#MFWSlider">2.4. MFW-Slider</a></div>

<div style="text-indent:22px;"><a href="#Tooltip">2.5. Tooltip</a></div>

<div style="text-indent:22px;"><a href="#Gradient">2.6. Gradient</a></div>

<div style="text-indent:10px;"><a href="#SideBySide">3. Side-by-Side</a></div>

<div style="text-indent:10px;"><a href="#Config">4. Config</a></div>

<br>
<hr>
<br>
The Rolling Stylometry Explorer is a web application to visualize rolling.classify results in the analyzed text. It was developed as a tool for use with the <a href="https://github.com/computationalstylistics/stylo">stylo R library</a> by the <a href="https://computationalstylistics.github.io/">Computational Stylistics Group</a>.
<br>
<h2><a id="Quickstart">1. Quickstart</a></h2>

<li>1. Download the Rolling Stylometry Explorer from github</li>
<li>2. Prepare your corpus</li>
<li>3. Open the <i>create_json_rolling.classify</i> file. If you want to delete the pronouns, set
<code>delete.pronouns</code> to <code>FALSE</code>. Under <code>corpus.lang</code> you can set the language. Then
insert the desired MFW-range under <code>mfw in seq(from=100, to=200, by=100)</code>. Adjust all further settings in
the <i>rolling.classify()</i> function. </li>
<b>Example</b><br>
<pre><code>delete.pronouns = FALSE
corpus.lang = "English.all"
for (mfw in seq(from=4000, to=5000, by=100)) {
result = rolling.classify(analyzed.features = "c", ngram.size = 3, mfw=mfw, slice.size = 5000, slice.overlap = 4500,
classification.method = "svm", delete.pronouns=delete.pronouns, corpus.lang=corpus.lang)</code></pre>

<li>4. Move the file into the folder with your
corpus and then run it with <code>Rscript --vanilla create_json_rolling.classify</code>. The analysis in Stylo is
performed and the JSON file is generated</li>
<li>5. Run the <i>json-consolidate.ts</i> file by executing <code>npx ts-node json-consolidate.ts
file_path_to_JSON_goes_here.ts
</code>. Add the file path to the JSON file(s). Follow the further instructions in the shell to provide information
about the configurations, the analyzed text and possible authors. <i>json-consolidate</i> will then generate a
<i>output.json</i> file.</li>
<li>6. Move the generated <i>output.json</i> file to <i>/rolling-classify-visualizer/src/assets</i>
<li>7. In the <i>explorer.html</i> file, pass the file path to the text to be analysed and to the JSON file. Implement
the Rolling Sylometry Explorer on your website using npm
(<code>
npm install rolling-classify-visualizer
</code>), import it in your Javascript
(<code>
import 'rolling-classify-visualizer';
</code>) and add the custom html-Tag to your website (see example below)
- or just try it out <a href="/pages/try-it.html">here</a>.
</li>

<b>Example</b><br>

<pre><code>
&lt;stylo-explorer
  book="/assets/analysis/book.txt"
  classification="/assets/analysis/output.json"
&gt;&lt;/stylo-explorer&gt;
&lt;script src="/assets/js/rolling-classify-visualizer.js"&gt;&lt;/script&gt;
</code></pre>

<br>
<p><img src="/assets/documentation/img/error-black-48dp.svg" alt="Note Icon"
style="float: left; margin: 0px 5px 10px 0px;" height="22px">

<b>Note</b>

<p>You can perform multiple analyses and pass multiple JSON files to the Explorer. Repeat step 3 for every analysis
you want to add to the Rolling Stylomentry Explorer. Add the file paths when you execute
<i>json-consolidate.ts</i></p>

<br>

<img src="/assets/documentation/img/warning-black-48dp.svg" alt="Warning Icon"
style="float: left; margin: 0px 5px 10px 0px;" height="22px">

<b>Warning</b>

<p>The Stylo Explorer has only been tested and optimised with the language settings English, English.contr and English.all.</p><br><br>

<a href="#TOC"><img src="/assets/documentation/img/baseline_keyboard_arrow_up_black_48dp.png" height="22px"></a>

<br>

<hr>
<br>

<h2><a id="Explorer">2. Rolling Stylometry Explorer</a></h2>
<p>The Rolling Stylometry Explorer is a web application to visualize rolling.classify results in the analyzed text.
It was developed as a tool for use with the <a href="https://github.com/computationalstylistics/stylo">stylo R
library</a> by the <a href="https://computationalstylistics.github.io/">Computational Stylistics
Group</a>.<br></p><br>
<b>Key Features</b>
<li>Display your rolling.classify results directly in the text
<li>Switch easily between different analyses and MFW values
<li>Use the Tooltip Feature to see the probabilities for each author and each text section
<li>Use the Gradient Feature and have the security of the authorship attribution displayed directly in the text
<li>Keep track of the configurations of the various analyses displayed in the Rolling Stylometry Explorer
</li>
<br><br>
<b>Stylo Explorer Overview</b>
<img src="/assets/documentation/img/Explorer_Interface.png" alt="Explorer Interface"><br>
<ul>
<li>1. <b>Explorer Tab</b>: Tab "Explorer" - you are here<br>
<li>2. <b>Config Tab</b>: Click on the Tab "Config" to switch to the Config-Site<br>
<li>3. <b>Side by Side Tab</b>: Click on the Tab "Side by Side" to switch to the Side by Side View<br>
<li>4. <b>Minimap</b>: Minimap based on the Stylo Plot. Shows current position in the text and assignment to
author<br>
<li>5. <b>Analyzed Text</b><br>

<li>6. <b>Settings</b>: Switch between different analyses by choosing a setting in the Drop-Down menu in the
toolbar

<li>7. <b>Color Legend</b>: Click to display the legend for the colors

<li>8. <b>MFW-Slider</b>: To change the MFW value and switch to another analysis, just move the MFW slider to
the desired MFW value

<li>9. <b>Gradient</b>: Switch the toggle switch to display the degree of confidence of the assignment in the text

<li> 10. <b>Tooltip</b>: Switch the toggle switch to show the probabilities for each author in each text section
(just hover over the text section)
<li>11. <b>Github Link</b>: Link to the projects Github page
</li><br>

<p><img src="/assets/documentation/img/emoji_objects-black-48dp.svg" alt="How it works Icon"
style="float: left; margin: 0px 5px 10px 0px;" height="22px">

<b>How it works</b>

<p>
Rolling.classify performs a windowing procedure and divides the text into short, overlapping sections.
Stylo uses a machine-learning algorithm to train a classifier to assign text sections to individual
authors in rolling.classify. The Rolling Stylometry Explorer divides the text into the same sections as
rolling.classify. The assignment made by rolling.classify is then made visible in the text by color
highlighting. Each author is assigned a color. The most probable author for the corresponding text
section is determined using the probabilities calculated by rolling.classify.</p>
<br><br>
<a href="#TOC"><img src="/assets/documentation/img/baseline_keyboard_arrow_up_black_48dp.png"
height="22px"></a>
<br>
<hr>
<br>

<h3><a id="Minimap">2.1. Minimap</a></h3>
<p>The Minimap is oriented in its presentation form to the plot generated by stylo for the respective
analysis. It can be read like the plot generated by stylo and shows the assignment in the course of the
text, thus providing an overview of the result of the analysis. The Minimap can also be used to navigate
through the text. By dragging to or clicking on a position in the Minimap the text navigates to the
corresponding position.</p><br><br>
<img src="/assets/documentation/img/emoji_objects-black-48dp.svg" alt="How it works Icon"
style="float: left; margin: 0px 5px 10px 0px;" height="22px">

<b>How it works</b>

<p>
To create the Minimap we divide the height of the Minimap, which is determined by the size of the
browser window by the number of text segments. We then insert bars into the Minimap, the dimensions of
which correspond to the result of the division. These bars represent the text segments and are coloured
according to the assignment to authors made by stylo. If the Minimap is clicked to navigate to the
corresponding position in the text, the system checks which position was clicked on as a percentage of
the Minimap. In the text, it jumps to this percentage position. This procedure also applies to dragging
within the Minimap.
</p>
<br><br>
<h4>Marker Minimap</h4>
<p>In Stylo you can use <i>xmilestone</i> to insert markers into the text, for example to show the beginning
of a chapter, which can be found later in the plot. If such markers have been inserted, they will also
be displayed in the Minimap.</p>
<br><br>

<a href="#TOC"><img src="/assets/documentation/img/baseline_keyboard_arrow_up_black_48dp.png"
height="22px"></a><br>

<hr>
<br>

<h3><a id="Settings">2.2. Settings</a></h3>
In the Rolling Stylometry Explorer you can view the analyses for different settings. For example, you can
switch between analyses that use different algorithms. A setting refers to all parameters set in Stylo R,
except the MFW value.
To switch to another analysis, simply click on <i>Settings</i> in the menu at the bottom of the page. Then
select the desired setting for the analysis from the drop-down menu. To change the MFW-Value see <a
href="#MFWSlider">MFW-Slider</a>.
<img src="/assets/documentation/img/Settings_menu.png">
<br><br>
<img src="/assets/documentation/img/emoji_objects-black-48dp.svg" alt="How it works Icon"
style="float: left; margin: 0px 5px 10px 0px;" height="22px">

<b>How it works</b>

<p>
The different settings are passed via the JSON file. From the information given to name the settings,
the displayed names for these settings are derived.
</p>
<br>

<a href="#TOC"><img src="/assets/documentation/img/baseline_keyboard_arrow_up_black_48dp.png"
height="22px"></a><br>

<hr>
<br>

<h3><a id="ColorLegend">2.3. Color Legend</a></h3>
Stylo R assigns a color to each author. This color is used in the plot. The Rolling Stylometry Explorer uses
the same colors as Stylo to display the authorship determined by Stylo in the text by color highlighting.
<br>
To display the legend for the colors just click on Color Legend in the menu at the bottom of the page.

<img src="/assets/documentation/img/color_legend_menu.png">
<br>
<br>
<img src="/assets/documentation/img/emoji_objects-black-48dp.svg" alt="How it works Icon"
style="float: left; margin: 0px 5px 10px 0px;" height="22px">

<b>How it works</b>

<p>
Stylo uses a fixed color palette in its default settings. This color palette has been adopted for the
Rolling Stylometry Explorer. Stylo assigns each author a color from this color palette. The Explorer
uses the same assignment procedure and can therefore always make the same assignment as Stylo.
</p><br><br>

<img src="/assets/documentation/img/warning-black-48dp.svg" alt="Warning Icon"
style="float: left; margin: 0px 5px 10px 0px;" height="22px">

<b>Warning</b>

<p> The Rolling Stylometry Explorer works with the color palette selected in the default settings of Stylo.
If the colours in Stylo R have been changed with the function assign.plot.colors, the Explorer will
still use the standard colour palette. In this case the color legend.</p><br>

<a href="#TOC"><img src="/assets/documentation/img/baseline_keyboard_arrow_up_black_48dp.png"
height="22px"></a><br>

<hr>
<br>

<h3><a id="MFWSlider">2.4. MFW-Slider</a></h3>

If several analyses with different MFW values were performed within a setting, it is possible to switch
between the analyses using the MFW slider. Simply move the MFW slider at the bottom of the screen to the
desired MFW value. This value is displayed in a thumb above the slider and next to the slider.

<img src="/assets/documentation/img/Slider_menu.png" alt="Slider Menu">
<br><br>
<img src="/assets/documentation/img/emoji_objects-black-48dp.svg" alt="How it works Icon"
style="float: left; margin: 0px 5px 10px 0px;" height="22px">

<b>How it works</b>

<p>
The analyses with the different MFW settings are transferred via the JSON file. Each position of the MFW
slider is assigned to a MFW value and thus to an analysis. If the slider is moved to a new value, the
corresponding analysis is loaded into the explorer.
</p><br><br>
<a href="#TOC"><img src="/assets/documentation/img/baseline_keyboard_arrow_up_black_48dp.png"
height="22px"></a>
<br>
<hr>
<br>

<h3><a id="Gradient">2.5. Gradient</a></h3>

The gradient feature allows you to display the degree of confidence of the assignment in the text.
To activate the function, switch the toggle switch in the settings menu at the bottom of the page.

<img src="/assets/documentation/img/Gradient_menu.png"><br><br>
<img src="/assets/documentation/img/emoji_objects-black-48dp.svg" alt="How it works Icon"
style="float: left; margin: 0px 5px 10px 0px;" height="22px">

<b>How it works</b>

<p>
Each author is assigned a color (see <a href="#ColorLegend">Color Legend</a>). According to the
probability calculated by stylo, the colors of the authors are mixed and the respective text section is
colored in the color thus created. The weighting of the colours is the average value of all available
results for the text section, which are then being normalized.</p>
<br>
<img src="/assets/documentation/img/warning-black-48dp.svg" alt="Warning Icon"
style="float: left; margin: 0px 5px 10px 0px;" height="22px">

<b>Warning</b>

<p>The gradient feature does not yet work reliably with SVM analyses. We are working on it :)</p><br><br>

<br>
<img src="/assets/documentation/img/Gradient_Text_Off_On.gif" alt="Gradient Demo"><br>
<br>
<a href="#TOC"><img src="/assets/documentation/img/baseline_keyboard_arrow_up_black_48dp.png"
height="22px"></a>
<br>
<hr>
<br>

<h3><a id="Tooltip">2.6. Tooltip</a></h3>
<p>With the tooltip feature you can display the probabilities output by stylo for the assignment of the authorship. Just activate the toggle switch "Tooltip" and hover with the mouse over a text section. A
window with the values for each author will appear. </p>

<p><img src="/assets/documentation/img/error-black-48dp.svg" alt="Note Icon"
style="float: left; margin: 0px 5px 10px 0px;" height="22px">

<b>Note</b>

<p>
The values displayed by the Explorer are not normalised.
</p>
<img src="/assets/documentation/img/Tooltip_menu.png"><br><br>
<img src="/assets/documentation/img/emoji_objects-black-48dp.svg" alt="How it works Icon"
style="float: left; margin: 0px 5px 10px 0px;" height="22px">

<b>How it works</b>

<p>You can make Stylo R save the calculated probabilities by storing the result of the analysis in a
variable. These values are saved in the JSON file and passed to the Explorer. The Explorer uses this
data to load the exact values for each text section. </p>
<img src="/assets/documentation/img/Tooltip_Text.png">
<br>

<a href="#TOC"><img src="/assets/documentation/img/baseline_keyboard_arrow_up_black_48dp.png"
    height="22px"></a>
<br>

<hr>
<br>

<h2><a id="SideBySide">3. Side-by-Side</a></h2>
<p>The side-by-side feature allows two analyses to be viewed and compared side by side. If you select the tab "Side-by-Side", you will see two analyses. You can select the settings for each analysis in the menu at the bottom of the page. The interface is structured analogous to the interface of the regular explorer.
The scrolling of the two windows is synchronised, which should make the comparison easier.<p>
<br>

<img src="/assets/documentation/img/Side_by_Side_Interface.png" alt="Config Interface">
<br>
<p><img src="/assets/documentation/img/emoji_objects-black-48dp.svg" alt="How it works Icon"
style="float: left; margin: 0px 5px 10px 0px;" height="22px">

<b>How it works</b>

<p>
For the side-by-side feature, two Rolling Stylometry Explorer are displayed next to each other. Both explorers access the same database and therefore contain the same book.txt file and the same JSON file. Otherwise, the explorers are independent of each other and separate settings can be made for each.</p>
<br>
<br>
<a href="#TOC"><img src="/assets/documentation/img/baseline_keyboard_arrow_up_black_48dp.png"
        height="22px"></a>

<br>
<br>
<hr>
<br>
<h2><a id="Config">4. Config</a></h2>
<p>During setup, you can provide information about the text, the authors and the different analyses.
This information can be viewed under Config. To get to the Config section, simply select the tab
<i>Config</i> in the menu at the top.
In the Config area you will find under <i>Author</i> the information you provided about the authors
and under <i>Analyzed Text</i> the information about the analyzed text. Additionally, there are
<i>tabs named after the individual analyses</i>. Here you can find the information about the
different implemented analyses.</p><br>

<img src="/assets/documentation/img/Config_Interface.png" alt="Config Interface">
<br>
<p><img src="/assets/documentation/img/emoji_objects-black-48dp.svg" alt="How it works Icon"
style="float: left; margin: 0px 5px 10px 0px;" height="22px">

<b>How it works</b>

<p>
    In the step in which you transfer your analyses to the Rolling Stylometry Explorer, you also can
    pass further information. You will be prompted to do so from the command line. The following
    input requests will appear:</p>

<li>Short name for JSON file?
    (Name of the analysis used in Settings and Config)</li>
<li>What settings have been used for "classification.json"? (This information is displayed under
    Config)
<li>What is the full name of the author?
    (This information is displayed under Config)</li>
<li>What is the title of the analyzed text / book?
    (This information is displayed under Config)</li>
<li>In which year was the text published?
    (This information is displayed under Config)</li>
<p>
    The passed information is transferred with the JSON file to the Explorer and used to name the
    analysis / to fill the Config page with information.
</p>
<br>
<br>
<a href="#TOC"><img src="/assets/documentation/img/baseline_keyboard_arrow_up_black_48dp.png"
        height="22px"></a>

<br>

<hr>
