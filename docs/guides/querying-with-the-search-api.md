
# Using the search API

This guide walks you through the process of using your generated API key to preform a basic query to honeypotdb using Insomina. 

### Setup

Here, I will use Insomnia, but feel free to use other tools such as Postman or cURL. 

### Creating a HTTP Request

Create a HTTP request on your software of choice.


![Insomina HTTP Request Creation](\img\honeypotdb-Insomina-http-request-creation.png "Insomina HTTP Request Creation"){ width=1250 }

### Setting up authentication

Navigate to your Auth configuration pannel

![Insomina Auth Navigation](\img\honeypotdb-Insomina-http-navigating-to-auth.png "Insomina Auth Navigation"){ width=1250 }

You will need to configure a new authentication header, with the key "X-API-KEY" and populate the value with your API Key. You may also use a JWT Authentication token. For more infomration on Authentication, please refer to [Authentication Docs](https://api.honeypotdb.com/docs#section/Authentication)

![Insomina Auth Setup](\img\honeypotdb-Insomina-http-auth-setup.png "Insomina Auth Setup"){ width=1250 }


### Map the URL and Body

We now need to populate the body of the request. This is where we can configure our query parameters. 

![Insomina Body Configuration](\img\honeypotdb-Insomina-http-switch-body-to-JSON.png "Insomina Body Configuration"){ width=1250 }

You can see an example body below, this query will return all ssh crowie pots deployed between July 8th and August 8th. For more details, see [Query Docs](https://api.honeypotdb.com/docs#tag/Search/operation/querySearch)

![Insomina URL Configuration](\img\honeypotdb-Insomina-http-enter-URL.png "Insomina URL Configuration"){ width=1250 }

### Switch Method POST

Switch the HTTP method to Post. 

![Insomina Method Configuration](\img\honeypotdb-Insomina-http-switch-method-to-post.png "Insomina Method Configuration"){ width=1250 }

### Response 

We are now ready to send the request, simply press send. 

![Insomina Query Response](\img\honeypotdb-Insomina-http-search-response.png "Insomina Query Response"){ width=1250 }


Here we can see results from the API. 

## Next Steps

For more details, please refer to our [API Documentation](https://api.honeypotdb.com/docs)

That's it, you're ready to start querying our threat intelligence. Take a look at the guides below as suggestions on what to do next:


* [Using the Search UI](/guides/using-the-search-ui)
* [Creating an API Key](/guides/creating-an-api-key)
* [Querying with the Search API](/guides/querying-with-the-search-api)
