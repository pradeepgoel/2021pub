

## Import your first API

* Go to your api instance
* Click on `Add API`
* Select OpenAPI
* Use a ready api provided by Microsoft
* https://conferenceapi.azurewebsites.net?format=json
* Select "Full" switch
* Enter url in OpenAPI specification
* Display name, Name and Description is auto filled

* URL scheme select "https"
* API URL suffic, this is important as this will append with the base URI and it should be unique 
* It needs to be part of your api
* Products select unlimited
* Gateways select managed, other option is self hosted gateway
* Version identifier, check this if a version needs to be created
* Review, design and setting tab
* In setting tab, add Webservice URL as https://conferenceapi.azurewebsites.net , remove query string
* If above URL is not added will get 500 error
* Go to test tab and select "GetSpeakers"
* Click on "Send" and a response will be returned with some json data

## Create and publish a product
* Select product in left navigation and click on "Add"
* Enter product name, product id and description
* Select published, subscription and approval required
* Click on "Create"
* Once product is created, navigate to created product and proceed with adding an API
* Select "Demo Conference API" 
* Add more configuration as needed

## Mock API responses
* As per tutorial, need to select blank api, this option was not available, selected HTTP manually define API option
* Switch to full and add a display name, ensure that gateways as managed and products as unlimited
* Click on `Create`
#### Add Operation
* Click on `Add operation`
* Enter `Test call` as name of the operation
* In URL field, select `GET` from the dropdown and enter `/test`
* Go to responses tab and add click on `Add response`, select `200 OK`
* Click on `+Add representation` it will be blank, enter `application/json` and search
* Select above from the returned results, enter following in the sample field
* `{'sampleFields' : 'test'}`
* Click `Save`
#### Enable mock response
* Go to Inbound policy, select `mock-response`, in the API management response field, ensure that 200 OK, application/json is available
* Click `Save`
#### Test mock API
* Go to test tab
* Ensure that request url ends with /test
* Click on `Send`
* You should see earlier entered object in the sample representation field

