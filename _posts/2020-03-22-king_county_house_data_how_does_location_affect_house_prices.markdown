---
layout: post
title:      "King County House Data:  How Does Location Affect House Prices?"
date:       2020-03-22 09:57:37 -0400
permalink:  king_county_house_data_how_does_location_affect_house_prices
---



King County house dataset contains house data which are sold during 2014 and 2015 at King County.  As a part of my project I had a chance to explore and work on this dataset.  'How Does Location Affect House Prices?'  is asked to explore which part of the county is most expensive , how location affect house prices. If there is enough correlation between house price and location data, location data can be used as a predictor for linear regression analysis.  

To answer the question , first  `groupby()` function  is used to group zipcodes and average price  calculated for each zipcode. The results are shown by a bar graph.  During grouping the prices by zip codes, the `mean ()` function is used instead of `sum ()` to reach unbiased results. 



```
fig, ax = plt.subplots(figsize=(20,15))
df.groupby('zipcode')['price'].mean().plot.bar()
plt.show()
```

<img src="https://github.com/esraguzel/dsc-mod-2-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-03-22%20at%2000.24.12.png?raw=true" width="100%">

The top 5 zip codes by average price are 98039, 98004, 98040, 98112 and 98102.

To visualize the most expensive areas of King county, longitude and latitude data used with a scatter plot. 


```
df.plot(kind="scatter", x="long", y="lat", figsize=(12, 10), c="price", 
             cmap="gist_heat_r", colorbar=True, sharex=False);
plt.show();
```

<img src="https://github.com/esraguzel/dsc-mod-2-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-03-22%20at%2012.05.12.png?raw=true" width="100%">


Here it can be observed that in general northern part of the county and the houses surrounding Lake Washington has higher prices.


To further analyze location's effect on house prices an open source data 'zipcode_king_county.geojson' is loaded to work with folium. It is aimed to create a heatmap with `Choropleth()` function showing average price for each zip code.
```
import json
# Calculating each zipcodes price mean
df_geo = df.groupby('zipcode')[['price']].mean().reset_index()
# changing zipcode data type to string to make it compatible with geojson file
df_geo['zipcode'] = df_geo['zipcode'].astype(str)

# loading the data
king_county_geo = 'zipcode_king_county.geojson'
with open(king_county_geo, 'r') as j:
    geo_data = json.load(j)
    
# Filtering the zip codes that exists in our dataset 
geozips = []
for i in range(len(geo_data['features'])):
    if geo_data['features'][i]['properties']['ZCTA5CE10'] in list(df_geo['zipcode'].unique()):
        geozips.append(geo_data['features'][i])
        
# Creating a new geojson dictionary with the filtered zip codes
new_json = dict.fromkeys(['type','features'])
new_json['type'] = 'FeatureCollection'
new_json['features'] = geozips

# Write content of dictionary with filtered zip codes to a json file
with open("king_county_new_geodata.json", "w") as new_file:
    new_file.write(json.dumps(
        new_json,
        sort_keys=True,
        indent=4, separators=(',', ': '),
    )
                  )
```


```
# Import folium library for map 
import folium

# Defining a start point view of the map
king_county = 'king_county_new_geodata.json'
m = folium.Map(
    location=[47.36, -121.89],
    zoom_start=10,
    detect_retina=True,
    control_scale=False,
)

# Creating a Choropleth with the help of follium 
folium.Choropleth(
    geo_data=king_county_geo,
    name='choropleth',
    data=df_geo,
    columns=['zipcode', 'price'],
    key_on='feature.properties.ZCTA5CE10',
    fill_color='YlOrRd',
    fill_opacity=0.7,
    line_opacity=0.2,
    legend_name='Average price'
).add_to(m)
folium.LayerControl().add_to(m)

m
```
<img src="https://github.com/esraguzel/dsc-mod-2-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-03-22%20at%2013.39.12.png?raw=true" width="100%">


It is observed that the Bellevue, Seattle and Mercer Island have the highest average house prices. Let's see whether the top 5 zip codes will match with the most expensive areas.

```
# Cerating a list of zipcodes, latitude and longitude belongong to the zipcodes
zipcode_list = [[47.6172, -122.230, 98039], [47.6312, -122.223, 98040], [47.5316, -122.233, 98040], [47.6440, -122.319, 98102], [47.6362, -122.302, 98112]]

for z in zipcode_list:
    lat = z[0]
    long = z[1]
    name = z[2]
    marker = folium.Marker(location=[lat, long], popup=name)
    marker.add_to(m)
m
```

<img src="https://github.com/esraguzel/dsc-mod-2-project-v2-1-onl01-dtsc-ft-012120/blob/master/images/Screenshot%202020-03-22%20at%2013.39.35.png?raw=true" width="100%">



As recognized from the above maps Northwest part of the county has higher average house prices  than the rest. In additon, some zip codes average house price are remarkably high compared to the rest.  It can be concluded that zipcodes can be effective predictors when performing multiple Regression Analysis on KC house data. 






