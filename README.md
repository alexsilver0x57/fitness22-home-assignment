# Fullstack home assignment

# **Assignment**

You are given a task to create a web application that allows to see Retention and Revenue data for a given mobile in-app product.

The application should have the following functionality:

- A homepage that allows a user to fetch data for an in-app product based on its identifier.
- A page or section that displays the Retention data per calendar month.
- A page or section that will display Revenue data (total and per month)

The application should use the MEVN (preferred) stack and should meet the following requirements:

- A Node.js/Express backend that includes an endpoint to handle webhooks and save any additional data received.
- The backend should be able to fetch and handle data from a database based on search criteria (in this case, query ALL and query by in-app product identifier)
- Use Vue.js/react.js/Angular to build the client-side single-page application (Vue.js is preferred).

Here are the specific requirements for each part of the application:

# Backend

You are given a JSON file that contains mock data.

The file should be imported into a database of your choice

The mock data contains two in-app products:

- "1M.sub.gym.20” which will be used for Retention Data and Revenue Data
- "LT.5K.30” which will be used for Revenue Data only.

The backend should have the following features:

1. An endpoint to handle additional data received in the same structure and save them to the same database.
2. Retrieving retention data for a given product by **“product_id”** (fetch from the mock data saved):
    - Retention data is calculated by searching for the **`INITIAL_PURCHASE`** type in the event, and then seeing how many users did the **`RENEWAL`** type event later on. The connection between the initial purchase event and the renewal events is the **`app_user_id`**.
    - Retention data should be displayed per month, starting from the month of the initial purchase. Each consecutive month should show how many users renewed the selected subscription for each month, displayed as a percentage.
    - It should do this for up to 36 consecutive months (3 years), with each row starting with the month of the initial purchase.
3. Retrieving revenue data for a given product or for all products:
    - If the product ID is provided, calculate the revenue data for that product only.
    - If no product ID parameter is provided, calculate the revenue data for all products.
    - Revenue data is calculated by summing the price in the event data.
    - Revenue data should be displayed per month, with a graph visualizing the data for each month and a total revenue amount.
4. Error handling.

Data example:

```json
{"eventID":"04d876de-11a3-4503-843f-55efdd6810ac","type":"INITIAL_PURCHASE","currency":"AUD","event_timestamp_ms":1675669128674,"app_user_id":"F22-C0A8AD0A-B2A0-4805-90F4-5E91C5463839","price":"19.711","price_in_purchased_currency":"28.49","product_id":"1M.sub.gym.20","takehome_percentage":"0.7"}
```

# Client-side SPA

- The SPA should have a homepage that allows the user to search for a specific product or select one from a list (reminder: 2 products are given).
- After selecting a product, it should display the retention data for that product in a table, with each row representing a month starting from the month of the initial purchase. Each consecutive month should show how many users renewed the selected subscription for each month, displayed as a percentage. If no retention is present it should display 0% or “-”.
- The SPA should have revenue data section in a graph that visualizes the data for each month and a total revenue amount for the selected product and for all products.
- The SPA should display appropriate error messages if the API returns an error.

An example of how the retention data could be displayed:

| Month | Initial Purchases | Retention After 1 Month | Retention After 2 Months | Retention After 3 Months |
| --- | --- | --- | --- | --- |
| 01/22 | 1000 | 25% | 10% | 5% |
| 02/22 | 1500 | 30% | 15% | - |
| 03/22 | 1200 | 20% | - | - |

In this example, the first column shows the month of the initial purchase. The second column shows the number of unique users who subscribed during that month. The third, fourth, and fifth columns show the retention percentage for the first, second, and third months after the initial purchase, respectively. If there are no renewals for a particular month, the cell should be left blank or display a dash ("-").

In January 2022, 1000 unique users subscribed to the product. Of those 1000 users, 250 (25%) continued to renew their subscription in February 2022 and 100 (10%) continued to renew their subscription in March 2022 as well.

# Bonus

- Add pagination to the retention data results so that only 12 months are displayed at once.
- Add a date picker to narrow down the search query and display the starting months based on the selected date ranges.
