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
   pm.expect(pm.response.code)).to.be.one.of([201,202])
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
   pm.expect(pm.response.header.get("Content-Type")).to.be.eql("application/json");
});
```
# Cookies testing 

```
pm.test("Check Cookie has language present", function()=>{
   pm.expect(pm.cookies.has("language")).to.be.true;
});
```
```
pm.test("Check Cookie has language set to en-gb", function()=>{
   pm.expect(pm.cookies.get("language")).to.be.eql("en-gb");
});
```
# Response time testing

```
pm.test("response time < 300ms", function()=>{
   pm.expect(pm.response.responseTime).to.be.below(300);
});
```
# Response body testing

Get the json body

Example body :
```
{
   "id": 1,
   "supplier": "vegman";
   "products": ["cabbage","lettuce","cucumber"]
}
```

```
const jsonData = pm.response.json();
```
```
pm.test("jsonData is an object", function()=>{
   pm.expect(jsonData).to.be.an("object");
});
```
```
pm.test("id is a number", function()=>{
   pm.expect(jsonData.id).to.be.a("number");
});
```
```
pm.test("supplier is a string", function()=>{
   pm.expect(jsonData.supplier).to.be.a("string");
});
```

```
pm.test("products to have members", function()=>{
   pm.expect(jsonData.products).to.have.members(["lettuce","cucumber"]);
});
```
```
pm.test("id is correct value", function()=>{
   pm.expect(jsonData.id).to.eql(1);
});
```
```
pm.test("products is include a value", function()=>{
   pm.expect(jsonData.products).to.include("cucumber");
});
```

```
pm.test("products has a value at index", function()=>{
   pm.expect(jsonData.products[2]).to.equal("cucumber");
});
```
# JSON schema validation

```
var jsonData = {
    "categories": [
        {
            "aNumber": "31000",
            "aString": "Yarp",
            "aBoolean": true
        }
    ]
}



var Ajv = require('ajv'),
    ajv = new Ajv({logger: console, allErrors: true}),
    schema =  {
    "type": "object",
    "required": [ "categories"],
    "properties": {
      "categories": {
          "type": "array",
          "items": {
              "type": "object",
              "required": [ "aStringOne", "aStringTwo", "aStringThree" ],
              "properties": {
                  "aNumber": { "type": "string" },
                  "aString": { "type": "integer"},
                  "aBoolean": { "type": "boolean"},
         }
       }
     }
   }
}

pm.test('Schema is valid', function() {
    pm.expect(ajv.validate(schema, jsonData), JSON.stringify(ajv.errors)).to.be.true
});
```

allErrors flag set so that it will return all the errors and not stop on the first.
SON.stringify(ajv.errors) included to see the error(s) in the Test Result tab.
