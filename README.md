# Postman Notes

The Postman JavaScript API functionality enables you to programmatically access and alter request and response data and variables using the pm object.
It also provides a test object pm.test.
```
pm.test("Test case", function()=>{
   //assertion
});
```
# Status code testing
```
pm.test("StatusCode is 200", function()=>{
   pm.response.to.have.status(200);
});
```
```
pm.test("Successful post request", function()=>{
   pm.expect(pm.response.code).to.be.one.of([201,202])
});
```
```
pm.test("Status code has name string", function()=>{
   pm.response.to.have.status("created");
});
```
# Headers testing
```
pm.test("Header contains Content-Type", function()=>{
   pm.response.to.have.header("Content-Type");
});
```
```
pm.test("Content-Type is application/json", function()=>{
   pm.expect(pm.response.header.get("Content-Type").to.be.eql("application/json"));
});
```
# Cookies testing 

```
pm.test("Check Cookie has language present", function()=>{
   pm.expect(pm.cookies.has("language").to.be.true);
});
```
```
pm.test("Check Cookie has language set to en-gb", function()=>{
   pm.expect(pm.cookies.get("language").to.be.eql("en-gb");
});
```
# Test response
