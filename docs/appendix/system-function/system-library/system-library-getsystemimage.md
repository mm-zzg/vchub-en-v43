
# System.Library.getSystemImage


## Description
Obtain images from the system library.

## Grammar
System.Library.getSystemImage(path:string): Promise<string> 

Parameter 

path - The path of the image  

Return 

base64

## Code Example                                                                                                                                                                                                                                                                                                          
Obtain"Transformer. svg" under "Power" in the system library.

```typescript 
const base64 = await System.Library.getSystemImage('Power.Transformer.svg');
console.log(base64)


```   

