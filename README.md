# Aim: Real-World and Interactive Visualizations

## THEORY

This experiment focuses on Advanced and Interactive Data Visualization, specifically utilizing the Plotly library to create dynamic charts. Unlike static plots, interactive visualizations allow users to hover over data points for more detail, zoom in on specific regions,
and toggle data series on or off. This is particularly useful for complex datasets where hierarchical structures (Treemaps), geographical
distributions (Choropleth Maps), or multi-dimensional relationships (Radar Charts) need to be explored intuitively.

A dendrogram is the output of hierarchical clustering. It is a tree-like diagram that shows the arrangement of clusters formed by progressively merging the most similar data points or groups. The y-axis (distance) indicates how similar two clusters are at the moment they are merged — lower merges indicate higher similarity; higher merges indicate groups that are more dissimilar. Dendrograms are used in bioinformatics (gene expression clustering), customer segmentation, document similarity analysis, and any domain requiring grouping without a pre-specified number of clusters. Dataset used: data = np.array([ [5, 3], [10, 15], [15, 12], [24, 10], [30, 30] ])

Dataset used:

df = pd.DataFrame({ 'Department': ['HR', 'IT', 'Sales', 'Marketing'], 'Budget': [20000, 50000, 40000, 30000] })

Commands:

import plotly.express as px: Imports the Plotly Express module, a high-level interface for creating complex and interactive figures with simple code.

pd.DataFrame(): Organizes raw data into a tabular format that is compatible with Plotly’s plotting functions.

px.treemap(): Creates a hierarchical visualization where data is represented as nested rectangles, with sizes proportional to their values.

px.choropleth(): Generates a geographical map where regions are shaded or patterned in proportion to a statistical variable.

linkage(data, method): Computes hierarchical clustering linkage matrix.

venn2([A, B], set_labels): Draws a two-circle Venn set diagram.

dendrogram(Z): Plots the hierarchical clustering tree.

px.line_polar(): Creates a radar (or spider) chart used to display multivariate data on a two-dimensional chart of three or more quantitative variables.

line_close=True: A parameter within polar plots that connects the last data point back to the first to create a closed geometric shape.

go.Figure(data=[...]): Creates an empty interactive Plotly figure.

go.Sankey(node, link): Plotly Sankey flow diagram trace.

px.scatter_3d(df, x, y, z, title): Interactive 3D scatter plot.

go.Scatterpolar(r, theta, fill, name): Polar (radar/spider) chart trace.

fig.add_trace(trace): Adds a trace to an existing Plotly figure.

fig.update_traces(): Allows for the modification of specific properties of the plot's data traces, such as fill color or marker opacity.

fig.update_layout(): Used to adjust the overall appearance of the chart, including margins, fonts, and background colors.

fig.show(): Renders the interactive figure directly within the Jupyter notebook or a web browser.

Matplotlib-based charts (dendrogram, Venn diagram) produce static PNG images embedded inline in the notebook. They cannot be interacted with after rendering.

Plotly-based charts (treemap, Sankey diagram, 3D scatter plot, radar chart) produce fully interactive HTML figures. Key interactive capabilities include:

Hover tooltips: Hovering over any element displays its label and value.
Zoom and pan: The figure can be zoomed into any region.
3D rotation: 3D scatter plots can be rotated freely by click-and-drag.
Legend toggling: Clicking a legend entry hides or shows the corresponding trace.

This interactivity makes Plotly figures particularly effective for presentations, dashboards, and exploratory analysis where the viewer needs to investigate specific data points rather than read a static summary.


## CONCLUSION
Through this experiment, it is concluded that Interactive Visualizations significantly enhance data storytelling. By using libraries
like Plotly, we can move beyond static images to create tools that allow stakeholders to actively engage with data, making it easier
to identify outliers in geographical regions or understand budget allocations through hierarchical structures.
