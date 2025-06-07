# NTT DATA Bootcamp - Engenharia de Dados com Python, by Digital Innovation One

## Project Challenge - Star Schema using DAX

The challenge this time entailed the creation of a star schema utilizing Power Query and DAX functions, ensuring, at the maximum, a one to many relationship to avoid Power BI freaking out.

### Creating the Schema

With the help of the instructor, the following Fact and Dimenisonal tables were modelled:

```text
D_Products:
  product_id
  product_name
  units_sold
  min_sale_price
  max_sale_price
  sale_price_avg
  sale_price_median
  manufacture_avg
```

This table, outside of being translated to english, is unchanged from what was shown by the instructor. The columns were all made within Power Query, using the Group By functionality. The unnecessary ones were removed.

```text
D_Discounts:
  discount_id
  Discount Band
  Discount
```

A column called "discount_id" was added to this one, so that this table can connect to the Fact table.

```text
F_Sales:
  SK_ID
  product_id
  discount_id
  details_id
  sale_details_id
  Date
```

This Fact table is the last one made with the instructor, and the most modified from the one made by them. Nothing is the same except for "SK_ID", "product_id" and "Date", the rest, "discount_id", "details_id" and "sale_details_id" were made to go along with the rest of the Dimension tables.

```text
D_Details:
  details_id
  Segment
  Country
```

This table only has "details_id", "Segment" and "Country", the duplicates were removed.

```text
D_Sale_Details:
  sale_details_id
  Units Sold
  Manufacturing Price
  Sale Price
  Gross Sales
  Sales
  COGS
  Profit
```

This table has "sale_details_id" and every original column not used in the previous tables, except the ones relating to dates.

```text
D_Calendar:
  Date
  Day
  Month
  Month Name
  Week Day
  Week Number
  Year
```

this particular table was made using DAX in the model view area of Power BI, it does not have an ID column, instead, Date is used as the relationship between Fact and Dimension table. The function used is as follows:

```text
D_Calendar = ADDCOLUMNS(
    CALENDAR(DATE(2013, 1, 1), DATE(2014, 12, 31)),
    "Year", YEAR([Date]),
    "Month", MONTH([Date]),
    "Month Name", FORMAT([Date], "MMMM"),
    "Day", DAY([Date]),
    "Week Number", WEEKDAY([Date]),
    "Week Day", FORMAT([Date], "DDDD")
)
```

This is the resulting model, after creating the relationships:

| ![star-schema-print](https://github.com/user-attachments/assets/864dad1c-1596-44a3-a8d2-5c220375e047)
|:--:|
| *"financials" is the original dataset table, "D_Dates" is a test table made with Power Query, both were hidden in report view.* |
