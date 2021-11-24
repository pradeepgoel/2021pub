

## Import your first API

* Go to your api instance
* Click on `Add API`
* Select OpenAPI
* Use a ready api provided by Microsoft
* https://conferenceapi.azurewebsites.net?format=json
* Select `Full` switch
* Enter url in OpenAPI specification
* Display name, Name and Description is auto filled

* URL scheme select `https`
* API URL suffix, this is important as this will append with the base URI and it should be unique and needs to be part of your api
* Products select `unlimited`
* Gateways select `managed`, other option is self hosted gateway
* Version identifier, check this if a version needs to be created
* Review, design and settings tab
* In setting tab, add Webservice URL as https://conferenceapi.azurewebsites.net , remove query string
* If above URL is not added, will get 500 error
* Go to test tab and select `GetSpeakers`
* Click on "Send" and a response will be returned with some json data

## Create and publish a product
* Select product in left navigation and click on `Add`
* Enter product name, product id and description
* Select published, subscription and approval required
* Click on `Create`
* Once product is created, navigate to created product and proceed with adding an API
* Select `Demo Conference API`
* Add more configuration as needed

## Mock API responses
* As per tutorial, need to select blank api, this option was not available, selected HTTP manually define API option
* Switch to full and add a display name, ensure that gateways as managed and products as unlimited
* Click on `Create`
#### Add operation
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

## Protect your API
* Strip response headers
* Replace original API urls with API gateway urls
* Apply rate-limit for the api
#### Strip response headers
* Go to Test tab and click on `GetSpeakers`
* Click on `Send`
* In the response, note down 2 custom headers `X-AspNet-Version` and `X-Powered-By`
* Next, we will update outbound policies to strip these headers
* Go to design tab, click on `All operations` --> `code editor </> ` in Outbound processing
* Place cursor after `Outbound` element and click on `Show snippets` and click twice on `Set HTTP header` to insert 2 header elements
* Update elements as
`<set-header name="X-Powered-By" exists-action="delete" />
<set-header name="X-AspNet-Version" exists-action="delete" />`

* Go to `Test` --> `GetSpeakers` --> `Send`
* Review the response, above 2 headers should not be in the response
#### Mask API headers
* From the response note down url, it should be 
* `https://conferenceapi.azurewebsites.net`
* Go to design tab, click on `All operations` --> `code editor </> ` in Outbound processing
* Place cursor after `Outbound` element and click on `Show snippets` and click on `Mask URL content` 
* Add opening and closing tag around this, save changes
* From the test tab, test this and your api gateway URL should be visible
#### Limit request rate
* Go to desing tab, click on `All operations` --> `code editor </> ` in Inbound processing
*  Place cursor after `Inbound` element and click on `Show snippets` and click on `Limit call rate per key`
* Update tag as <rate-limit-by-key calls="3" renewal-period="15" counter-key="@(context.Subscription.Id)" />
* Go to `Test` --> `GetSpeakers` and send 4 requests in quick succession, for 4th request a 403 message wil return 

#### Monitoring
* Metrics 
    - Capacity
    - Requests
* Alerts
* Capacity let you know the utilization of CPU and memory
* Requests can be further filtered as needed to see errors, backend response time
* Set up alerts on static and dynamic threshold
* Activity log

#### Revison
* Revisions are to make non breaking changes in your API that you can release to test before you roll out to customers
* Need to add `;rev=revision_number` before query string to call a specific revision
* Once a revison has been tested, it can be made as current

#### Version
* API can have multiple versions that can be identified by different version numbers
* There are multiple ways to define versions
    - Path
    - Header
    _ Query
* Once a version is added, previous version becomes `Original` and a version number is not needed to be passed if this does not have a version scheme

