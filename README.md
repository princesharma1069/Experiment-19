# Aim: Real-World and Interactive Visualizations

## THEORY

Introduction to Real-World and Interactive Visualizations
Basic and statistical charts cover most exploratory data analysis needs. However, certain analytical scenarios require specialized or interactive visualization types that reveal structure not visible in flat 2D charts — hierarchical composition, cluster groupings, set overlaps, flow quantities between entities, three-dimensional relationships, and multi-variable profile comparisons. Python's Plotly, SciPy, and Matplotlib ecosystem provides these advanced visualization capabilities.

Libraries imported for this experiment: import plotly.express as px import plotly.graph_objects as go import matplotlib.pyplot as plt import numpy as np import pandas as pd from scipy.cluster.hierarchy import dendrogram, linkage from matplotlib_venn import venn2

Plotly produces fully interactive figures (hover tooltips, zoom, pan, click events) rendered in the browser or Jupyter/Colab environment, while Matplotlib produces static figures.

Treemap — px.treemap()
A treemap visualizes hierarchical data as a set of nested rectangles. Each rectangle's area is proportional to the value it represents, making it easy to compare sizes within and across hierarchy levels. Treemaps are used when visualizing budget allocation, disk usage, portfolio weights, or any other part-to-whole relationship with a hierarchical structure.

Dataset used: df = pd.DataFrame({ 'Department': ['HR', 'IT', 'Sales', 'Marketing'], 'Budget': [20000, 50000, 40000, 30000] })

Function and parameter breakdown:

px.treemap(df, path, values, title):
df: The Pandas DataFrame containing the data.
path=['Department']: A list defining the hierarchy levels. A single-element list produces a flat treemap with one level of rectangles. For multi-level hierarchies, additional columns can be added to the list, e.g., path=['Region', 'Department'].
values='Budget': The column whose values determine the area of each rectangle. Larger budget entries produce proportionally larger tiles.
title='Pranav': Adds a title to the interactive Plotly figure.
fig.show(): Renders the interactive figure in a browser tab or inline in Colab/Jupyter. Unlike plt.show(), which renders a static PNG, fig.show() opens a live interactive Plotly figure with hover tooltips, zoom, and click functionality.
Dendrogram — dendrogram() and linkage()
A dendrogram is the output of hierarchical clustering. It is a tree-like diagram that shows the arrangement of clusters formed by progressively merging the most similar data points or groups. The y-axis (distance) indicates how similar two clusters are at the moment they are merged — lower merges indicate higher similarity; higher merges indicate groups that are more dissimilar.

Dendrograms are used in bioinformatics (gene expression clustering), customer segmentation, document similarity analysis, and any domain requiring grouping without a pre-specified number of clusters.

Dataset used: data = np.array([ [5, 3], [10, 15], [15, 12], [24, 10], [30, 30] ])

This is a 2D dataset with 5 data points, each described by two features.

Function and parameter breakdown:

linkage(data, method='ward'): Performs hierarchical agglomerative clustering on the data. At each step, the two closest clusters are merged. The result is a linkage matrix Z encoding the full merge history.
method='ward': The Ward linkage criterion merges clusters by minimizing the total within-cluster variance. It tends to produce compact, evenly sized clusters and is the most widely used linkage method for general analysis. Other methods include 'single' (minimum distance), 'complete' (maximum distance), and 'average'.
The returned linkage matrix Z has shape (n-1, 4), where each row records the two cluster indices merged, the distance at which they merged, and the number of original observations in the new cluster.
dendrogram(linked): Takes the linkage matrix and renders the hierarchical tree structure as a dendrogram plot. The leaves correspond to individual data points; the branching points correspond to merges. The height of each horizontal link represents the distance between the two merged clusters.
plt.figure(figsize=(6, 4)): Creates the figure with specified dimensions before calling dendrogram(), which plots into the active axes.
plt.xlabel("Data Points"): Labels the x-axis, which displays the indices of the original data points as leaves.
plt.ylabel("Distance"): Labels the y-axis showing the merge distances.
Venn Diagram — venn2()
A Venn diagram uses overlapping circles to visualize the logical relationships between two or more sets. The overlapping region represents elements that belong to both sets (intersection), while the non-overlapping regions represent elements exclusive to each set. Venn diagrams are used to compare datasets, identify shared features, and illustrate set-theoretic relationships.

Sets used: A = {1, 2, 3, 4} B = {3, 4, 5, 6}

Intersection A ∩ B = {3, 4} — 2 elements
Only in A = {1, 2} — 2 elements
Only in B = {5, 6} — 2 elements
Function and parameter breakdown:

venn2([A, B], set_labels=('Set A', 'Set B')): Draws a two-circle Venn diagram.
The first argument is a list of the two Python sets to compare.
set_labels: A tuple of strings labeling each circle. These appear beside the circles.
venn2 automatically counts the elements in each region (only A, only B, A∩B) and displays the counts inside the respective regions of the diagram.
The venn2 function is from the matplotlib_venn library, which must be installed separately (pip install matplotlib-venn) as it is not part of core Matplotlib.
For three-set comparisons, venn3([A, B, C], set_labels=(...)) is used.
Sankey Diagram — go.Sankey()
A Sankey diagram visualizes flow quantities between nodes. The width of each flow (link) is proportional to the quantity flowing through it. Sankey diagrams are widely used for energy flow analysis, budget flow, network traffic, and student progression tracking.

Flow represented: Admission (100) → First Year (80) → Second Year (60) → Placed

This models student attrition across academic stages.

Function and parameter breakdown:

go.Figure(data=[go.Sankey(...)]): Creates a Plotly Figure containing a Sankey trace.
go.Sankey(node, link): The core Sankey object.
node=dict(label=[...]): Defines the nodes of the diagram. Each element in the label list is a node name. Nodes are indexed by their position (0, 1, 2, ...).
link=dict(source, target, value):
source=[0, 1, 2]: A list of source node indices for each flow.
target=[1, 2, 3]: A list of destination node indices for each flow.
value=[100, 80, 60]: The quantity of each flow. Flow widths are drawn proportionally to these values.
The link from source[i] to target[i] carries value[i] units, so: source=0 (Admission) → target=1 (First Year), value=100 source=1 (First Year) → target=2 (Second Year), value=80 source=2 (Second Year) → target=3 (Placed), value=60
fig.show(): Renders the interactive Plotly Sankey figure. Hovering over nodes or links in the interactive view displays the exact flow quantities.
3D Scatter Plot — px.scatter_3d()
A 3D scatter plot extends the standard 2D scatter plot by adding a third axis (z), allowing three numerical variables to be visualized simultaneously in three-dimensional space. It is used to explore three-way correlations and spatial clustering in multivariate datasets.

Dataset used: df = pd.DataFrame({ 'Study_Hours': [2, 4, 6, 8, 5], 'Marks': [50, 65, 75, 90, 70], 'Attendance': [60, 75, 80, 90, 70] })

This dataset models the relationship between study hours, academic marks, and attendance percentage for 5 students. An upward trend in all three variables would indicate that higher study hours and attendance correlate with higher marks.

Function and parameter breakdown:

px.scatter_3d(df, x, y, z, title):
df: The DataFrame containing the data.
x='Study_Hours': The column to map to the x-axis.
y='Marks': The column to map to the y-axis.
z='Attendance': The column to map to the z-axis.
title='Pranav': Adds a title to the figure.
The resulting Plotly figure is fully interactive — it can be rotated, zoomed, and panned in 3D. Each point can be hovered to inspect its exact (x, y, z) values.
Additional Plotly Express parameters such as color=, size=, and symbol= can encode further variables visually on the 3D scatter.
Radar Chart — go.Scatterpolar()
A radar chart (also called a spider chart or web chart) displays multivariate data on a two-dimensional plane by arranging multiple axes radially at equal angles from a center point. Each axis represents one variable, and a data point is plotted as a polygon connecting its values on each axis. Radar charts are used to compare the overall profile of an entity across multiple categories — for example, a student's skill scores across different subjects.

Data used: skills = ['Python', 'ML', 'DBMS', 'DSA', 'Communication'] values = [4, 3, 5, 4, 3]

This encodes a student's self-rated proficiency (out of 5) across five skill areas.

Function and parameter breakdown:

go.Figure(): Creates an empty Plotly Figure to which traces are added.
fig.add_trace(go.Scatterpolar(...)): Adds a polar scatter trace to the figure.
r=values: The radial distances for each data point. Higher values plot further from the center, representing higher proficiency.
theta=skills: The angular positions for each spoke. Each skill name is placed at an equal angular interval around the chart.
fill='toself': Fills the area enclosed by the polygon back to itself, creating a solid shape rather than just an outline. This makes the area coverage immediately visible, facilitating comparison across variables.
name='Skills': Labels this trace in the Plotly legend.
The polygon's shape reveals strengths and weaknesses at a glance — spikes toward the perimeter indicate strong areas, indentations toward the center indicate weak areas.
Comparison of Visualization Types Covered
Chart Type	Library Used	Primary Use Case
Treemap	plotly.express	Hierarchical part-to-whole size comparison
Dendrogram	scipy + matplotlib	Visualizing hierarchical clustering merge tree
Venn Diagram	matplotlib_venn	Set intersection and difference visualization
Sankey Diagram	plotly.graph_objects	Flow quantities between sequential nodes
3D Scatter Plot	plotly.express	Three-variable correlation in 3D space
Radar Chart	plotly.graph_objects	Multi-variable profile comparison
Static vs. Interactive Visualizations
Matplotlib-based charts (dendrogram, Venn diagram) produce static PNG images embedded inline in the notebook. They cannot be interacted with after rendering.

Plotly-based charts (treemap, Sankey diagram, 3D scatter plot, radar chart) produce fully interactive HTML figures. Key interactive capabilities include:

Hover tooltips: Hovering over any element displays its label and value.
Zoom and pan: The figure can be zoomed into any region.
3D rotation: 3D scatter plots can be rotated freely by click-and-drag.
Legend toggling: Clicking a legend entry hides or shows the corresponding trace.
This interactivity makes Plotly figures particularly effective for presentations, dashboards, and exploratory analysis where the viewer needs to investigate specific data points rather than read a static summary.

Summary of New Functions Introduced in Experiment 19
px.treemap(df, path, values, title): Hierarchical rectangle area chart.
linkage(data, method): Computes hierarchical clustering linkage matrix.
dendrogram(Z): Plots the hierarchical clustering tree.
venn2([A, B], set_labels): Draws a two-circle Venn set diagram.
go.Figure(data=[...]): Creates an empty interactive Plotly figure.
go.Sankey(node, link): Plotly Sankey flow diagram trace.
px.scatter_3d(df, x, y, z, title): Interactive 3D scatter plot.
go.Scatterpolar(r, theta, fill, name): Polar (radar/spider) chart trace.
fig.add_trace(trace): Adds a trace to an existing Plotly figure.
fig.show(): Renders an interactive Plotly figure.
## CONCLUSION
