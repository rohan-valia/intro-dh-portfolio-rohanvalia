---
layout: page
title: Visualizing Data with Bokeh and Pandas
description: This lesson uses the Bokeh and Pandas libraries in Python to visualize the dataset regarding the bombing runs by the Allied powers during WWII.
---

## Source
[Charlie Harper, "Visualizing Data with Bokeh and Pandas," Programming Historian (2021)](https://programminghistorian.org/en/lessons/visualizing-with-bokeh)

## Reflection

The process of visualizing data requires the ability to first upload the dataset, sample the data, and then visually display the data in an effective manner. In this Programming Historian lesson, we are able to use the Bokeh and Pandas libraries in order to create visual models of the Allied powers bombing runs that took place in WWII. 

For the most part, I was able to follow the steps in plotting each visual model as they were each very methodical and logical in terms of attributing each component of the model. Through this process, learning about Bokeh was very interesting, including the interactive element of it within its visual model, which allows you to hover over data points to get more information on them. In the past, I have visualized data in Python using the matplotlib library, which creates more basic and one-dimensional forms of data models, so using Bokeh seemed much more advanced in terms of its data visualization in terms of its dynamic features. In regards to Pandas, I have worked with it in the past for reading and interpreting files and datasets, and I had seen a lot of the commands and functions that were called in plotting these models, but I learned a lot about how it can be used with Bokeh through this lesson. One other thing I learned was the importance of sampling when creating models for large datasets to produce more efficient visual models and in order to avoid a large amount of overlapping data points in a model. 

## Code

```python
# column_datasource.py

import pandas as pd
from bokeh.plotting import figure, output_file, show
from bokeh.models import ColumnDataSource
from bokeh.models.tools import HoverTool

output_file('columndatasource_example.html')

df = pd.read_csv('thor_wwii.csv')

sample = df.sample(50)
source = ColumnDataSource(sample)

p = figure()
p.circle(x='TOTAL_TONS', y='AC_ATTACKING',
         source=source,
         size=10, color='green')

p.title.text = 'Attacking Aircraft and Munitions Dropped'
p.xaxis.axis_label = 'Tons of Munitions Dropped'
p.yaxis.axis_label = 'Number of Attacking Aircraft'

hover = HoverTool()
hover.tooltips=[
    ('Attack Date', '@MSNDATE'),
    ('Attacking Aircraft', '@AC_ATTACKING'),
    ('Tons of Munitions', '@TOTAL_TONS'),
    ('Type of Aircraft', '@AIRCRAFT_NAME')
]

p.add_tools(hover)

show(p)
```


```python
# munitions_by_country.py

from bokeh.palettes import Spectral5
from bokeh.transform import factor_cmap
output_file('munitions_by_country.html')

df = pd.read_csv('thor_wwii.csv')

grouped = df.groupby('COUNTRY_FLYING_MISSION')[['TOTAL_TONS', 'TONS_HE', 'TONS_IC', 'TONS_FRAG']].sum()

print(grouped)
```

                            TOTAL_TONS     TONS_HE     TONS_IC  TONS_FRAG
    COUNTRY_FLYING_MISSION                                               
    AUSTRALIA                   479.89      453.90      13.600      18.64
    GREAT BRITAIN           1112598.95   868277.23  209036.158    1208.00
    NEW ZEALAND                2629.06     4263.70     166.500       0.00
    SOUTH AFRICA                 11.69       15.00       0.000       0.00
    USA                     1625487.68  1297955.65  205288.200  127655.98



```python
# munitions_by_country.py 

grouped = grouped / 1000

source = ColumnDataSource(grouped)
countries = source.data['COUNTRY_FLYING_MISSION'].tolist()
p = figure(x_range=countries)

color_map = factor_cmap(field_name='COUNTRY_FLYING_MISSION',
                    palette=Spectral5, factors=countries)

p.vbar(x='COUNTRY_FLYING_MISSION', top='TOTAL_TONS', source=source, width=0.70, color=color_map)

p.title.text ='Munitions Dropped by Allied Country'
p.xaxis.axis_label = 'Country'
p.yaxis.axis_label = 'Kilotons of Munitions'

hover = HoverTool()
hover.tooltips = [
    ("Totals", "@TONS_HE High Explosive / @TONS_IC Incendiary / @TONS_FRAG Fragmentation")]

hover.mode = 'vline'

p.add_tools(hover)

show(p)


```


```python
# munitions_by_country_stacked.py

from bokeh.palettes import Spectral3

output_file('types_of_munitions.html')

df = pd.read_csv('thor_wwii.csv')

filter = df['COUNTRY_FLYING_MISSION'].isin(('USA','GREAT BRITAIN'))
df = df[filter]

grouped = df.groupby('COUNTRY_FLYING_MISSION')['TONS_IC', 'TONS_FRAG', 'TONS_HE'].sum()

#convert tons to kilotons again
grouped = grouped / 1000

source = ColumnDataSource(grouped)
countries = source.data['COUNTRY_FLYING_MISSION'].tolist()
p = figure(x_range=countries)

p.vbar_stack(stackers=['TONS_HE', 'TONS_FRAG', 'TONS_IC'],
             x='COUNTRY_FLYING_MISSION', source=source,
             legend = ['High Explosive', 'Fragmentation', 'Incendiary'],
             width=0.5, color=Spectral3)

p.title.text ='Types of Munitions Dropped by Allied Country'
p.legend.location = 'top_left'

p.xaxis.axis_label = 'Country'
p.xgrid.grid_line_color = None	#remove the x grid lines

p.yaxis.axis_label = 'Kilotons of Munitions'

show(p)
```

    /var/folders/6z/x5gb0xfs2v513pyqk29flfxw0000gn/T/ipykernel_89936/2252052954.py:12: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      grouped = df.groupby('COUNTRY_FLYING_MISSION')['TONS_IC', 'TONS_FRAG', 'TONS_HE'].sum()
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead



```python
#my_first_timeseries.py

output_file('simple_timeseries_plot.html')

df = pd.read_csv('thor_wwii.csv')

#make sure MSNDATE is a datetime format
df['MSNDATE'] = pd.to_datetime(df['MSNDATE'], format='%m/%d/%Y')

# grouped = df.groupby('MSNDATE')['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
grouped = df.groupby(pd.Grouper(key='MSNDATE', freq='M'))['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
grouped = grouped/1000

source = ColumnDataSource(grouped)

p = figure(x_axis_type='datetime')

p.line(x='MSNDATE', y='TOTAL_TONS', line_width=2, source=source, legend='All Munitions')
p.line(x='MSNDATE', y='TONS_FRAG', line_width=2, source=source, color=Spectral3[1], legend='Fragmentation')
p.line(x='MSNDATE', y='TONS_IC', line_width=2, source=source, color=Spectral3[2], legend='Incendiary')

p.yaxis.axis_label = 'Kilotons of Munitions Dropped'

show(p)
```

    /var/folders/6z/x5gb0xfs2v513pyqk29flfxw0000gn/T/ipykernel_89936/2025397141.py:11: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      grouped = df.groupby(pd.Grouper(key='MSNDATE', freq='M'))['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead



```python
# annotating_trends.py

from bokeh.models import BoxAnnotation

output_file('eto_operations.html')

df = pd.read_csv('thor_wwii.csv')

#filter for the European Theater of Operations
filter = df['THEATER']=='ETO'
df = df[filter]

df['MSNDATE'] = pd.to_datetime(df['MSNDATE'], format='%m/%d/%Y')
group = df.groupby(pd.Grouper(key='MSNDATE', freq='M'))['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
group = group / 1000

source = ColumnDataSource(group)

p = figure(x_axis_type="datetime")

p.line(x='MSNDATE', y='TOTAL_TONS', line_width=2, source=source, legend='All Munitions')
p.line(x='MSNDATE', y='TONS_FRAG', line_width=2, source=source, color=Spectral3[1], legend='Fragmentation')
p.line(x='MSNDATE', y='TONS_IC', line_width=2, source=source, color=Spectral3[2], legend='Incendiary')

p.title.text = 'European Theater of Operations'

p.yaxis.axis_label = 'Kilotons of Munitions Dropped'

box_left = pd.to_datetime('6-6-1944')
box_right = pd.to_datetime('16-12-1944')

box = BoxAnnotation(left=box_left, right=box_right,
                    line_width=1, line_color='black', line_dash='dashed',
                    fill_alpha=0.2, fill_color='orange')

p.add_layout(box)

show(p)
```

    /var/folders/6z/x5gb0xfs2v513pyqk29flfxw0000gn/T/ipykernel_89936/2032927960.py:14: FutureWarning: Indexing with multiple keys (implicitly converted to a tuple of keys) will be deprecated, use a list instead.
      group = df.groupby(pd.Grouper(key='MSNDATE', freq='M'))['TOTAL_TONS', 'TONS_IC', 'TONS_FRAG'].sum()
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    BokehDeprecationWarning: 'legend' keyword is deprecated, use explicit 'legend_label', 'legend_field', or 'legend_group' keywords instead
    /var/folders/6z/x5gb0xfs2v513pyqk29flfxw0000gn/T/ipykernel_89936/2032927960.py:30: UserWarning: Parsing '16-12-1944' in DD/MM/YYYY format. Provide format or specify infer_datetime_format=True for consistent parsing.
      box_right = pd.to_datetime('16-12-1944')



```python
# target_locations.py

from bokeh.models import ColumnDataSource, Range1d
from bokeh.layouts import layout
from bokeh.tile_providers import get_provider
from pyproj import Transformer

output_file('mapping_targets.html')

df = pd.read_csv('thor_wwii.csv')

def LongLat_to_EN(long, lat):
    try:
        transformer = Transformer.from_crs('epsg:4326', 'epsg:3857')
        easting, northing = transformer.transform(long, lat)
        return easting, northing
    except:
        return None, None

df['E'], df['N'] = zip(
    *df.apply(lambda x: LongLat_to_EN(x['TGT_LONGITUDE'], x['TGT_LATITUDE']), axis=1))

grouped = df.groupby(['E', 'N'])[['TONS_IC', 'TONS_FRAG']].sum().reset_index()

filter = grouped['TONS_FRAG'] != 0
grouped = grouped[filter]

source = ColumnDataSource(grouped)

left = -2150000
right = 18000000
bottom = -5300000
top = 11000000

p = figure(x_range=Range1d(left, right), y_range=Range1d(bottom, top))

provider = get_provider('CARTODBPOSITRON')
p.add_tile(provider)

p.circle(x='E', y='N', source=source, line_color='grey', fill_color='yellow')

p.axis.visible = False

show(p)
```


```python

```