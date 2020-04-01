# XMLHttpRequest

```javascript
function xml (url, method, data = null) {
      return new Promise((resolve, reject) => {
        let xmlhttp;
        if (window.XMLHttpRequest) {
          xmlhttp = new XMLHttpRequest();
        }

        if (xmlhttp != null) {
          xmlhttp.onreadystatechange = state_Change;
          xmlhttp.open(method, url, true);
          xmlhttp.send(data);
        }
        else {
          alert("Your browser does not support XMLHTTP.");
        }
        function state_Change () {
          if (xmlhttp.readyState == 4) {
            if (xmlhttp.status == 200) {
              resolve(xmlhttp.responseText)
            }
            else {
              reject("Problem retrieving XML data");
            }
          }
        }
      })
    }
```

