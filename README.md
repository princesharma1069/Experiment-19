# Aim: Real-World and Interactive Visualizations

## THEORY

This experiment focuses on Advanced and Interactive Data Visualization, specifically utilizing the Plotly library to create dynamic charts. Unlike static plots, interactive visualizations allow users to hover over data points for more detail, zoom in on specific regions,
and toggle data series on or off. This is particularly useful for complex datasets where hierarchical structures (Treemaps), geographical
distributions (Choropleth Maps), or multi-dimensional relationships (Radar Charts) need to be explored intuitively.

import plotly.express as px: Imports the Plotly Express module, a high-level interface for creating complex and interactive figures with simple code.

pd.DataFrame(): Organizes raw data into a tabular format that is compatible with Plotly’s plotting functions.

px.treemap(): Creates a hierarchical visualization where data is represented as nested rectangles, with sizes proportional to their values.

px.choropleth(): Generates a geographical map where regions are shaded or patterned in proportion to a statistical variable.

px.line_polar(): Creates a radar (or spider) chart used to display multivariate data on a two-dimensional chart of three or more quantitative variables.

line_close=True: A parameter within polar plots that connects the last data point back to the first to create a closed geometric shape.

fig.update_traces(): Allows for the modification of specific properties of the plot's data traces, such as fill color or marker opacity.

fig.update_layout(): Used to adjust the overall appearance of the chart, including margins, fonts, and background colors.

fig.show(): Renders the interactive figure directly within the Jupyter notebook or a web browser.
## CONCLUSION
Through this experiment, it is concluded that Interactive Visualizations significantly enhance data storytelling. By using libraries
like Plotly, we can move beyond static images to create tools that allow stakeholders to actively engage with data, making it easier
to identify outliers in geographical regions or understand budget allocations through hierarchical structures.
