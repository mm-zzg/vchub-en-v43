# System.Page.getPropertyValue

## Description
Get the value of the current page's custom property or control property.
## Grammar
                                                                                                                               
System.Page.getPropertyValue(path: string): any 

     - Parameter 

        path - Path of the page's custom property or control property 

    - Return 

        Property value


## Code Example                                                                                                                                                                                                                                                                                                          
Get the value of the custom property "no" for the page.
```typescript 

const value = System.Page.getPropertyValue('#custom.no');
console.log(value);

```   
Get the text property value of TextInput1.
```typescript 

const value = System.Page.getPropertyValue('TextInput1#text');
console.log(value);

```   

