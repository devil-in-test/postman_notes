# Postman Notes

The Postman JavaScript API functionality enables you to programmatically access and alter request and response data and variables using the pm object.
It also provides a test object pm.test

pm.test("Test case", function()=>{
   //assertion
});

# Status Code Validation

pm.test("StatusCode is 200", function()=>{
   pm.response.to.have.Status(200);
});

pm.test("Successful post request", function()=>{
   pm.expect(pm.response.code).to.be.one.of([201,202])
});

pm.test("Status code has name string", function()=>{
   pm.response.to.have.status("created");
});
