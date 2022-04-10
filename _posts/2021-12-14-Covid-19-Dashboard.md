---
title: "Covid-19 Dashboard"
excerpt: "Number of cases and deaths resulted from Covid-19 by country or region for 2020-2021"
last_modified_at: 2022-04-09
author_profile: true
thumbnail: /assets/images/COVID-19 DASHBOARD.png
header:
  image: "/assets/images/COVID-19 DASHBOARD.png"
  teaser: /assets/images/COVID-19 DASHBOARD-Thumbnail.png
tags: 
  - Covid
  - MATLAB
  - GUI
  - App
---
  
During the few months of lockdown in the recent Covid-19 pandemic, I decided to put my MATLAB skills to test and build a dashboard to both visualize the daily and cumulative numbers better and to refresh my app building knowledge. After all, if you don't use your skills, you will lose them.

I started by creating an object oriented class structure for different countries, regions, and states. This was challenging as some countries had regions and some countries had states and some had none or both.

```matlab
% Class definition to be able to store global, country, and state data
    
classdef Places < handle
    properties (Access = public)
        Country
        Region
        CovidCases
        DeathCases
    end

methods
    function obj = Places(count,region,cases)
        % setting country or state name to string
        if nargin < 3, cases = []; end
        obj.Country = string(count);
        obj.Region = string(region);
        obj.Region(obj.Region == "") = "All";
% and so on ...
```
Once I had a solid base for my data I could use them and build my app structure efficiently and however I wanted. I defined a few useful properties and functions to be able to manipulate the data for better visualization. I added features to take average over a few days, see cumulative or daily cases and deaths on one graph for comparison, and most importantly choose countries and regions right on the app for convenience.

```matlab
% Example of a few properties that correspond to app components
        
    properties (Access = public)
        UIFigure               matlab.ui.Figure
        OptionButtonGroup      matlab.ui.container.ButtonGroup
        DailyButton            matlab.ui.control.RadioButton

% Example of a function for app usability        

function computeData(app)
            app.titleCountry = app.Country{app.country_index+app.region_index-1}.Country;
            app.titleRegion = app.Country{app.country_index+app.region_index-1}.Region;
            b = length(app.Country{app.country_index+app.region_index-1}.CovidCases);

% Startup function to display something when the app starts up.

function setDefaults(app)
        % Setting up initial values for widgets
        app.CountryListBox.Items = ["Global" ; app.Global.Country];
        app.CountryListBox.Value = app.CountryListBox.Items(1);
        app.StateorRegionListBox.Items = app.Global.Region(1);
```
The final results are what you see at the top of the page. A pretty looking user-friendly app that helps you visualize what is going on in the world and how serious this virus is.

<figure style="width: 600px" class="align-center">
    <a href="/assets/images/COVID-19 DASHBOARD.png"><img src="/assets/images/COVID-19 DASHBOARD.png"></a>
</figure>
