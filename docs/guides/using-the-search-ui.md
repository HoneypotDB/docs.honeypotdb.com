# Using the Search UI 

This guide walks you through the process of using the Search UI to query our database. 

## Preforming a simple query

### Navigation

Firstly, navigate to the search page by selecting "Search" in the Navigation Menu.

![Search Page Navigation](\img\honeypotdb-search-page.png "Search Page Navigation"){ width=1250 }

### Defining Query Parameters

Here, we can define our query. Let's start by adding our date range: 


![Search Page Date Population](\img\honeypotdb-search-dates-populated.png "Search Page Date Population"){ width=1250 }

Next, we can add the field we would like to set our conditions on. We use a simple to use dot notation for all our data. For example, here I would like all pots from Gunzenhausen, upon reviewing the scheama, or examples, I can see that data is held in hpdb.pot.city. We can add this like so. 

![Search Page Field Population](\img\honeypotdb-search-fields-populated.png "Search Page Field Population"){ width=1250 }

Once we are happy with the query we set up, we can add it by pressing "Add to Search" 

![Search Page Added Notification](\img\honeypotdb-search-added.png "Search Page Added Notification"){ width=1250 }

### Response 

Once your happy with your compiled query, select "Search" and all matched records will be returned below.

![Search Page Query Results](\img\honeypotdb-search-results.png "Search Page Query Results"){ width=1250 }

## Next Steps

That's it, you're ready to start querying our threat intelligence through our UI. Take a look at the guides below as suggestions on what to do next:

* [Using the Search UI](/guides/using-the-search-ui)
* [Creating an API Key](/guides/creating-an-api-key)
* [Querying with the Search API](/guides/querying-with-the-search-api)
