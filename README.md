# Visualization & Storytelling (Tableau)

### Communicating information about data visually
> Why are data visualizations more useful for delivering insight than just using summary statistics?
> How visual encodings influences the way we interpret information and in turn how well we can draw insights from the data? 
> What plot do you build in a given situation?
> How to encode our visuals to best communicate our findings? How to design components? 

__[two components]__
 - artistic: to be eyecatching (engaging)
 - scientific: to deliver the right insights (informative)
Summary statistics like the mean and standard deviation can be great for attempting to quickly understand aspects of a dataset, but they can also be misleading. 
<img src="https://user-images.githubusercontent.com/31917400/33559462-bf77609c-d904-11e7-8dbb-b60ae351e93b.jpg"  />

%Anscombe's Quartet: In the 4 datasets with X,Y pairs above, they all share the same stats, but data points are very different one another. Relying on only summarry statistics can be misleading!    

__[What to care?]__
 - Data type(continuous? discrete? ordinal? categorical?)
 - number of columns 
 - Quantitative over time: Line Chart
 - a couple, correlation-coefficient("strength + direction" of linear relationship): Scatter Plot
<img src="https://user-images.githubusercontent.com/31917400/33561533-cf9a5528-d90a-11e7-8f8d-4361b221a62f.jpg" width="350" height="130" />

 - Univariate: Histogram / Box and Whisker Plot / Stem and Leaf Plot / Normal Quantile Plot 
<img src="https://user-images.githubusercontent.com/31917400/33560553-f8cfd8b2-d907-11e7-92fe-6d7103b5426d.jpg"  />

 - Multivariate: Bar Chart(categorical bin) / Pareto Chart(ordinal bin, which has the most problem?) / Pie Chart
<img src="https://user-images.githubusercontent.com/31917400/33560699-65ceff06-d908-11e7-823c-06035aef8008.jpg" width="350" height="200" />
 
 - Categorical Intensive: 
   - Categorical vs Categorical vs Quantitative: Side-by-Side Bar Chart, Multi-Line Charts, Stacked Bar Chart 
<img src="https://user-images.githubusercontent.com/31917400/33563471-fba1d5b0-d90f-11e7-8ce0-61ac69a2d491.jpg" />

__[Design]__
Example in R 
```
install.packages('ggplot2')
library(ggplot2)

df = read.csv(..............) 
df2 = head(df, 30)

qplot(df2$Math.SAT, df2$Verbal.SAT, xlab = 'Math SAT Score', 
      ylab = 'Verbal SAT Score', main = 'Average SAT Scores By College')

qplot(df2$Math.SAT, df2$Verbal.SAT, xlab = 'Math SAT Score', 
      ylab = 'Verbal SAT Score', main = 'Average SAT Scores By College', 
      color = as.factor(df2$Public..1...Private..2.))

qplot(df2$Math.SAT, df2$Verbal.SAT, xlab = 'Math SAT Score',
      ylab = 'Verbal SAT Score', main = 'Average SAT Scores By College',
      shape = as.factor(df2$Public..1...Private..2.), color = df2$stud..fac..ratio)

ggplot(df2, aes(x=Math.SAT, y=Verbal.SAT, group=stud..fac..ratio)) +
  geom_point(aes(shape=stud..fac..ratio, color=as.factor(df2$Public..1...Private..2.))
```
__[tableau]__

 - I. Connecting to Data
 - II. Combining Data (connect data from multiple sources)
 - III. Worksheets
 - IV. Aggregations
 - V. Hierarchies (look at the data at a year, month, day, hour, or another level)
 - VI. Marks & Filters (controls the colors, shapes and other attributes of our data)
 - VII. Show Me (controls what our ending visual looks like)
 - VIII. Small Multiples & Dual Axis (to visualize data that needs to share an axis for comparison purposes)
 - IX. Groups & Sets (categorize our data within a visualization)
 - X. Calculated Fields (add calculated fields to a visualization on the fly)
 - XI. Table Calculations (perform comparisons of our data over time or between groups)

### I. Connecting to Data
In the left sidebar you'll see the data sources you can connect to. For file sources, you can connect to an Excel file, a text file such as a CSV, or statistical files such as from SAS, SPSS, and R. If Tableau detects sub-tables, unique formatting, or some extraneous information, the **Data Interpreter** option becomes available. 

### II. Combining Data 
Dragging multiple sheets(tables) into the top panel and get two different outcomes depending on where to drag it, a **union** or a **join**.

__Union:__ Drag the second sheet below the first sheet, we get a **union** (if we have multiple sheets with **columns in common** as the columns will match up). Unions stack the data on top of each other, the second sheet ends up being appended to the end of the first sheet.  

__Join:__ Drag the second sheet beside the first, we get a **join** (if both have columns that we can use for the common values).Joins combines data from the sheets based on common values. We can click on the join symbol to change the type of join being performed - Inner/Left/Right/Outter. 

### III. Worksheets
There are three main products that we can create using Tableau: 1)Worksheets, 2)Dashboards, 3)Stories. Worksheets are the core of creating dashboards and stories. On the left, fields are split between "dimensions" and "measures". Categorical, qualitative, and time data are listed as "dimensions". Quantitative numerical data is listed as "measure". Tableau automatically aggregates measures, but not dimensions. Dimensions are used to group the data and set the level of granularity.  

__Plotting:__ Select 'sheet1' in the lower left corner to start visualization. Select the data you want to plot by dragging the fields to the "columns or rows shelves". Dragging dimension to "column-shelve" and measure fields to "row-shelves" in general. It is aggregating the measure data for each dimension and summing the values. 

__Tips__
>Q. Exporting a worksheet - `Worksheet > Export > Image >`
>Q. Working with 'Extract Data'
 - Create an 'extract' for Tableau to work from (Copy and Save some data from the original)
 - When you start working with big, dynamic dataset that often changes...just like a version control... 
<img src="https://user-images.githubusercontent.com/31917400/35773041-edb09144-093e-11e8-8fe4-ffa6c7cd9fa3.jpg" width="600" height="200" /> 

### IV. Aggregations

__[1) Altering aggregation]__ 
Aggregation(for numerical) and granularity(for categorical) govern how Tableau operates. Let's get straight into it !

**Time Series**
We want to see how 'certain rate' is changing as 'period' changes. 
 - 'period': Discrete or Contiguous ?
 - 'Year/Quarter/Month/Day' --- Changing the granularity(NO.of ticks) of the timeline.  
<img src="https://user-images.githubusercontent.com/31917400/35773435-70a794b6-094a-11e8-853d-b0dec8360ce3.jpg" /> 

**A.** When we create a plot, selecting 'dimension'(categorical) and 'measure'(numerical), Tableau is automatically aggregating them over all records in the data set.
 - We can switch off 'aggregation measures' from the manu bar...it will give a scatter.   

**B.** Next, we can introduce a 'dimension' that will change the level of granularity thus affect the aggregation, dragging it into the 'Marks'box(color/size/label/detail/tooltip/shape). Of course we can introduce more 'dimension'sss to increase granularity further.    

**C.** To change the aggregation method, we can select 'measure' then Sum, Average, Median, and others. To get more points, we need to increase the **granularity**. That means we need to aggregate not over all the records, but over 'dimensions'(categories). By increasing the granularity, Tableau is aggregating the data over each dimension. 
 - We get sums of 'measure' aggregated over groups in selected categories. The level of granularity is set by the total number of groups we have in our dimensions. We should be aware of **how many groups the selected category field has**. 
<img src="https://user-images.githubusercontent.com/31917400/35777698-3d7b674c-09aa-11e8-823a-d6e0dca1699e.jpg" />

 - Aggregations assist in our ability to draw insights, but other times having a point for every row might be better.
 
 - __Highlighting__
   - 'Highlighting' interrogates one of the levels in a category more specifically. Just click the legend.  
   - 'detail' in the 'Marks'box is a dark templer. The 'dimension' on the 'detail' affects the granularity but is not represented anywhere in the chart. So if we want to highlight the 'dimension' on the 'detail', we drag the 'dimension' into 'shape' then click the legend.
 - __Area Chart__
<img src="https://user-images.githubusercontent.com/31917400/35778439-2332fdee-09b6-11e8-83fb-dacc32b67f8e.jpg" /> 

>Q. Adding **filters**: We built a chart, but there is a missing 'dimension' that need to be considered, then we put this 'dimension' into a 'filter'shelve. We can customize our filter to check and isolate the chart of a particular level of the 'dimension'. 
<img src="https://user-images.githubusercontent.com/31917400/35781017-0d572b1e-09dc-11e8-807b-153390fe86c0.jpg" /> 

>Q. Adding new **custom variable**(a column of aggregation): Let's say we have, as measures, 'Units' and 'Unit_Price'. But we need to create  'total_dollar_value'. What are you gonna do? 
 - We need to multiply 'Units' by 'Unit_Price'
   - RightClick on measures and select `Create Calculated Field` then  
<img src="https://user-images.githubusercontent.com/31917400/35745386-0cc475a0-083b-11e8-9348-fc92d836ec95.jpg" /> 

% Seemingly, Richard is not the best seller overall. Now we know who deserves the bonus. 

>Q. Adding **Color**: Discrete / Continuous
 - Discrete Coloring 
<img src="https://user-images.githubusercontent.com/31917400/35746661-7496ef88-083f-11e8-80fb-ea991702daea.jpg" /> 

 - Continuous Coloring 
<img src="https://user-images.githubusercontent.com/31917400/35747886-f2fa97ae-0843-11e8-9967-3f8d9cca6fbc.jpg" width="700" height="200" />

>Q. Adding **Labels and Formatting**
 - Adding Labels: We can type our own text like.."Sales: <SUM(total_dollar_value)>"
<img src="https://user-images.githubusercontent.com/31917400/35748792-26a6b0f8-0847-11e8-965d-74eea386fc86.jpg" width="700" height="200" />

% When some text does not appear because of its size: RightClicking -> Choose `mark label > Always Show`   
 - Formatting Labels 
<img src="https://user-images.githubusercontent.com/31917400/35749792-aaf41f64-084a-11e8-8203-4f9480e91a9a.jpg" /> 

 - Formatting Axis
<img src="https://user-images.githubusercontent.com/31917400/35754487-7c8c3146-085b-11e8-9383-b0dfc087971a.jpg" width="700" height="200" /> 


__[2) ]__  

 









### V. Hierarchies
When you drag "Datetime" variable to Columns, there is a little plus symbol on the "Datetime" field pill. Tableau automatically makes a hierarchy of time periods from "date" and "time" data fields. As we drill down, we get more fine divisions, from year, to quarter, to month, then day. Clicking on minus sign in them, it will go back up the hierarchy. We can make some column to absorb other column as a sub-category. Select both the catgory(mom) and sub-category(child), then, in the drop down for the category(mom), create hierarchy.  

<img src="https://user-images.githubusercontent.com/31917400/33630630-f9b0e8fe-d9ff-11e7-8347-15c03b04a734.jpg" width="600" height="150" />

### VI. Marks & Filters
__Mark card:__ Often, we’ll want to include more dimensions in our graph. We can add dimensions to the plot (increasing granularity) by dragging dimensions or measures to the Marks shelf. It has options such as color, size, and shape. 
 - __Color:__ Most often we'll be encoding data with color. We simply drag the field to "Color" in the Marks card.
 
<img src="https://user-images.githubusercontent.com/31917400/33633792-e86d17f2-da09-11e7-854a-316439db3bb6.png" />

 - __Size:__ Dragging a field, either discrete or continuous, to "Size" will encode the data in the size of the markers. We'll most often use this encoding in a scatter plot. Below is a scatter plot with average quantity vs average profit for each country. I encoded the average discount using the size of the markers, it's clear that discounts are responsible for the countries with negative profits.

<img src="https://user-images.githubusercontent.com/31917400/33633961-7fcd4d42-da0a-11e7-92d8-8efa666c150d.png" width="400" height="250" />

 - __Shape:__ As with color and size, we can use the shape of the markers to encode data. We'll want to use **discrete data only** for this. Also, if we have too many categories the shapes are too difficult to identify.

<img src="https://user-images.githubusercontent.com/31917400/33634227-6bf14520-da0b-11e7-9714-02808609bad5.png" width="400" height="250" />

 - __Detail:__ The "Detail" card allows us to bring in a field without any visual encoding. This enables us to increase granularity without adding any graphical effect. The "Label" card adds in labels for all of our markers.

__Mark & Filter card:__ This way we can view only the data we are interested in. 

<img src="https://user-images.githubusercontent.com/31917400/33634715-1357dbf2-da0d-11e7-8551-7118d09c3768.jpg" />

### VII. Show Me
The Show Me feature is a quick way to start with a basic graph which we can add to afterwards. We can find it in the top-right of the sheet. Selecting multiple fields we want simultaneously then clicking the show me graph. From there you can customize the graph. Show Me is usually a good start once you decide what you want to look at or show. Here, filters would definitely help us narrow to look at one question at a time. 

<img src="https://user-images.githubusercontent.com/31917400/33668273-33e708f4-da97-11e7-9f27-eb2f8d187029.jpg" width="500" height="200" /> 

### VIII. Small Multiples & Dual Axis
__Small Multiple:__ (split) Simply dragging multiple dimensions to the Columns and Rows shelves creates a small multiple. We saw this before when learning about hierarchies. The main advantages of the Small Multiples view is to be able to see 'little ranges' of our data at a time.

<img src="https://user-images.githubusercontent.com/31917400/33672299-d19de4c8-daa1-11e7-9ef7-16882b930330.png" width="600" height="210" /> 

__Dual Axis:__ (overlap) When we drag multiple Measures to the Rows shelf, we get multiple plots. If we want them in one plot, we use dual axis.   
 
<img src="https://user-images.githubusercontent.com/31917400/33672987-85b9942e-daa3-11e7-8e62-81ce7499bad9.png" width="600" height="210" />

### IX. Groups & Sets
__Groups:__ Groups are typically created from the view by selecting multiple data points in the view. We can use it in other sheets. For instance, create a map that shows how the low quantity countries (grouped) are distributed in the world. Here we used the group we created (Low Quantity Countries) to color the map. The blue countries are the ones in the group, the ones with low average quantity.

<img src="https://user-images.githubusercontent.com/31917400/33680974-261d075e-dabb-11e7-83c5-a32b1007c182.png" />

__Sets:__ Sets are similar to groups in that we can select data points and create a set from them. However, sets can be dynamic where the members of the set will change as the underlying data changes. Groups on the other hand are static, the members will always be the members. For example, say we want to see how our poor performing products are affecting the overall profits. We can create a set from the product names or IDs which lose money, where the average profit is below zero. To create the set, open the menu for the Product Name field and choose Create > Set...Click the "Condition" tab. Then select By field: Profit Average < 0 as seen below.

<img src="https://user-images.githubusercontent.com/31917400/33681307-09ca5484-dabc-11e7-8daf-ac41e4967a76.png" width="600" height="290" />

We can use the set in plots to encode these products that are losing money. Let's look at the total profits for the different sub-categories of products. With the set you just made, you can split these bars into losses and gains. The red bars are showing how much money is lost due to the bad products. It looks like Office Supplies products are almost all winners, but Furniture is losing a lot of money.

<img src="https://user-images.githubusercontent.com/31917400/33681549-cd9233fa-dabc-11e7-87c4-7bfb8573667a.png" />

### X. Calculated Fields
With more than a **binary split** (just two categories), using a Group or Set might not be the best option. Instead, you should use a Calculated Field. There will be times when we want to look at something but there isn't a specific field for it. For instance, maybe we want to know the 'profit' per item for each 'order' record. It seems pretty simple, just divide 'profit' by 'order' for each record, then aggregate it, but how do you actually do the division in Tableau? The answer is calculated fields. Calculated fields let us create new fields to use in our visualizations. To create a calculated field, open the menu on a field (such as 'Profit'), then Create > Calculated Field....Fields in the editor show up in brackets, like [Profit]. We can do simple arithmetic here, like adding a constant, or multiplying the field. We can also use functions such as absolute value, sine, square root, etc. Here we want to create a new field that calculates the profit per item for each record - [Profit]/[Quantity]. We also renamed the calculated field to "Profit per item". 

<img src="https://user-images.githubusercontent.com/31917400/33688641-0890a632-dad4-11e7-8401-43b4e9465d92.png" />

You can also do aggregation directly in a calculated field. For instance, we can also calculate the profit per item by SUM([Profit])/SUM([Quantity]). The two methods for calculating the profit per item look basically the same, but there are some discrepancies like in "Tables". Now we see there are some weird things going on. A lot of the results from the two methods are extremely different. The third product has a profit per item of $9 or -$5. Looking at the values of Profit and Quantity, it appears that the aggregation method (SUM([Profit])/SUM([Quantity]) is doing the right thing.

<img src="https://user-images.githubusercontent.com/31917400/33690599-24191cec-dadc-11e7-91d9-7a67238fe20e.png" />

At the row level, the two calculations are the same. It's the averaging of the [Profit]/[Quantity] calculation that is causing the difference. For the the "Atlantic Mobile 4-Shelf Bookcases" product, all the ratios are correct. But when you average them, (28-112+28+42+28+42)/6 = 9.333, you get what we see at the product name level. The aggregation in the other calculation takes care of that for us. It always calculates the ratios for the level of granularity we're at. You can see the columns Profit and Quantity doing the summation at the level of granularity and the ratio SUM([Profit])/SUM([Quantity]) is taken from those numbers. The two calculations are answering different questions.
 - What is the profit ratio for a single order within any product or any other category level?
   - Average of [Profit]/[Quantity]
 - What is the profit ratio at any level of a category?
   - SUM([Profit])/SUM([Quantity])

> __Conditional statements__
We can use conditional statements like IF, THEN, ELSE in calculations. For example to make a new field to categorize sales as "good" and bad", we could do: 
> - IF SUM([Sales]) > 10000 THEN "Good" ELSE "Bad"
> - IIF(SUM([Sales]) > 10000, "Good", "Bad") ==> If true, If false

### XI. Table Calculations
Table calculations can be useful for helping us to compare the data that exists in a plot to other parts of the plot. What if we want to compare the percent of profits that went into each market to the total profit. Select the drop down associated with SUM(Profit), and select ```Quick Table Calculation... > Percent of Total```. Alternatively, it could be useful to look at compounding profit. A lot of table calculations work well for line plots. Let's take a look at an example. Add the Order Date to the Columns and Sales to the Rows. Make sure the Order Date is continuous. Drill down to the Quarter level, and select ```Quick Table Calculation... > Percent Difference```. 

<img src="https://user-images.githubusercontent.com/31917400/33713970-3271b880-db45-11e7-9652-1a1349868053.png" />

In order to get a better idea of how things are moving over time, we might use a **moving average**. You can see below how this is done using the table calculations. Additionally, I broke out the Category to see how things change over time for each. This plot is great for seeing the trend of the data, and that sales are increasing, but they aren't great for seeing how sales are changing over time from one quarter to the next. Instead, the last question on the next concept requires the plot below.

<img src="https://user-images.githubusercontent.com/31917400/33714331-78fd815c-db46-11e7-842c-9b4cec9700d7.png" />


### Filter



 



  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
