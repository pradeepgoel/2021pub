

-- Go to your api instance
-- click on `Add API`
-- there are multiple options, select OpenAPI
-- Use a ready api provided by Microsoft
-- https://conferenceapi.azurewebsites.net?format=json
-- Select "Full" switch
-- Enter url in OpenAPI specification
-- Display name, Name and Description is auto filled

-- URL scheme select "https"
-- API URL suffic, this is important as this will append with the base URI and it should be unique 
-- it needs to be part of your api
-- Products select unlimited
-- Gateways select managed, other option is self hosted gateway
-- version identifier, check this if a version needs to be created
-- review, design and setting tab
-- in setting tab, add Webservice URL as https://conferenceapi.azurewebsites.net , remove query string
-- if not added will get 500 error
-- Go to test tab and 
