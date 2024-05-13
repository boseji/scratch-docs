# Javascript Snippets

## Converting String to and from Arrays in Javascript

```js
let msg="Testing";
let encode = new TextEncoder('utf-8');
let buf = new Uint8Array(encode.encode(msg));
console.log(buf);
let decode = new TextDecoder('utf-8');
console.log(decode.decode(buf));
```

----
<!-- Footer Begins Here -->
## Links

- [Back to Root Document](../README.md)
