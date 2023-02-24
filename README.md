# Superstore Europe

This is a personal project produced during my free time to demonstrate my personal skills in SQL and Tableau.

## Step 1: Ask

### 1.Superstore  

The Superstore operates mainly online and in Europe.

### 2.Business task

Define KPIs based on the data available and produce a dashboard to have a quick look around of the business.

### 3.Key Stakeholders

**Anella Van Crup**: She is the manager and the director of marketing..

**Executive team**: The notoriously detail-oriented executives team will decide whether to approve the recommended analysis.

## Step 2: Prepare

### 1.Information on data

The data has been shared publicly by Tableau to show off their new tools and options. The dataset includes columns like order_id, order_date, ship_date, ship_mode, customer_id, segment, city, state, country, category, sub_category, sales and profit.

### 2.Limitations of data.

The data obtained is from 2015 to 2018. The analysis can only be judged as a multi-year analysis. As it is publicly shared by Tableau, I have no doubt on its integrity.

### 3.Is the data ROCC ?

A good data source is ROCCC which stands for Reliable, Original, Comprehensive, Current, and Cited.

Reliable - High - It has all the information related to an online superstore.

Original - Med - It is made up data to exercise.

Comprehensive - High - All the columns are understandable.

Current - Med - The data is 4 year old.

Cited - Med - It is made up data.

# Step 3: Process

I loaded the file in Gsheet to have a better look at the data. I have seen no errors, no null values and clear stated columns. Then, I used Google's Big Query to query the data.

### 1. Google's Big Query.

I created the table on Google's Big Query and loaded the data onto the table.

# Step 4: Analyse

### 1. Determine the number of orders.

I wanted to know how many customers ordered.

```{r}
SELECT COUNT(Order_ID) as nb_orders
FROM `utopian-outlet-358815.EU_superstore.EU_superstore_orders`
```

### 2. Number of orders per Year.

Then, I wanted to see the number of orders per year.

```{r}
SELECT COUNT(Order_ID) as nb_orders,
EXTRACT (YEAR from Order_Date) as year
FROM `utopian-outlet-358815.EU_superstore.EU_superstore_orders`
GROUP BY year
ORDER BY year
```

### 3. Number of orders per Segment.

I wondered about the number of orders by segment.  

```{r}
SELECT COUNT(Order_ID) as nb_order, Segment
FROM `utopian-outlet-358815.EU_superstore.EU_superstore_orders`
Group By Segment
ORDER BY nb_order DESC
```

### 4.Determine the sales by Segment.

I wanted to determine the sales by customers. Consumers are the one that order the most (50% of the order), then Corporate and Home Office.

```{r}
SELECT SUM(Sales) as Sales, Segment
FROM `utopian-outlet-358815.EU_superstore.EU_superstore_orders`
GROUP BY Segment
ORDER BY Sales DESC
```

### 5.Getting the sales by State.

I wanted to be more precise by having the sales by city.  

```{r}
Sales per State :
SELECT SUM(Sales) as Sales, State
FROM `utopian-outlet-358815.EU_superstore.EU_superstore_orders`
GROUP BY State
ORDER BY Sales DESC
```

### 6.Getting the sales by Country.

```{r}
SELECT SUM(Sales) as Sales, Country
FROM `utopian-outlet-358815.EU_superstore.EU_superstore_orders`
GROUP BY Country
ORDER BY Sales DESC
```

### 7.Determine the sales by Category.

I wanted to know which category had the biggest sale.

```{r}
SELECT SUM(Sales) as Sales, Category
FROM `utopian-outlet-358815.EU_superstore.EU_superstore_orders`
GROUP BY Category
ORDER BY Sales DESC
```
### 8.Determine the sales by Year.

```{r}
SELECT SUM(Sales) as sales,
EXTRACT (YEAR from Order_Date) as year
FROM `utopian-outlet-358815.EU_superstore.EU_superstore_orders`
GROUP BY year
ORDER BY year,
```

### 9.Determine the average sale by Segment and Year.

```{r}
Average sales by Segment and Year
SELECT AVG(Sales)/ COUNT(Order_ID), Segment,
EXTRACT (YEAR from Order_Date) as year,
FROM `utopian-outlet-358815.EU_superstore.EU_superstore_orders`
GROUP BY Segment, Year
```

### 10.Determine the total profit.

```{r}
SELECT SUM(Profit) as Total_profit
FROM `utopian-outlet-358815.EU_superstore.EU_superstore_orders`
```

# Step 5: Share phase

I created a dashboard on Tableau to expose my findings.

[Superstore_EU](https://public.tableau.com/app/profile/maxime3299/viz/Superstore_EU/SuperstoreEUDashboardin2015-2018?publish=yes)

# Step 6: Act phase

1/ From 2015 to 2018, there's been 1000 orders from 16 European countries.

2/ Consumers are the ones that order the most (50% of the order), then Corporate and Home Office. On the other hand, consumers are the one that has the lowest average sale by year ($251,5 in 2015 to $104,3 in 2018). Their average sale decreased by 58%. Home Office is the one with the biggest average sale ($418,4 in 2015 to $428.9 in 2018); It represents a 2,44% increase.  

3/ France, Germany and the UK are the biggest markets for the Superstore.

4/ The technology category is the most sought-after, then furniture and office supplies. In the technology category : copiers, phones and machines are the biggest sales.

5/ In 2015, sales were $289 872 081 and $701 333 790 in 2018. It represents a 141% increase. 
