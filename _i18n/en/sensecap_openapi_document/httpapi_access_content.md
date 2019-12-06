## HTTP Methods
The SenseCAP API utilizes five HTTP methods for accessing resources:
- GET
    - Make a GET request to retrieve data. GET requests will never cause an update or change to your data because they're safe and idempotent.
- POST
    - Use a POST request to create new resources. For example, make a POST request to a device group where the body of your request JSON is a new group.
- PATCH
    - Make a PATCH request to update a resource. With PATCH request, you only need to provide the data you want to change.
- PUT
    - Use a PUT request to create or update a resource. This is most useful for syncing subscriber data.
- DELETE
    - Make a DELETE request to remove a resource.

{% include note.html content="If your ISP doesn't permit HTTP operations other than GET or POST, please use HTTP Method tunneling - make your call with POST, but include the method you intend to use in an X-HTTP-Method-Override header." %}

## HTTP Request and Response
Requests are authenticated with the HTTP Basic Authentication.

### HTTP Basic Authentication
[HTTP Basic Authentication](https://en.wikipedia.org/wiki/Basic_access_authentication) is one of the most common ways for RESTfull API authentication. We use Access ID as username and Access Key as password. Every HTTP client library should have its built-in support for Basic Authentication, in this documentation we use curl, which uses the --user option to specify Basic Authentication credential.

u can create access keys via [SenseCAP  Web Portal](https://sensecap.seeed.cc/portal). Please refer to quickstart to see how to get an access key.

### API Response
All response fields follow the lowercase and underscore convention

#### Successful Response with String
```ruby
   {
       "code":"0",
       "data":"
           // string
       "
   }
```

#### Successful Response with Object
```ruby
   {
       "code":"0",
       "data":{
           // object
       }
   }
```
#### Successful response with Array
```ruby
   {
       "code":"0",
       "data":[
           // Array
       ]
   }
```
#### Error Response
```ruby
   {
       "code":"1001",
       "msg":"error message"
   }
```
