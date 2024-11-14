# Data Persistence

```js echo
display(state_data)
```

```js echo
let state_data = Mutable ({})

function swap_data(data) {
  state_data.value = data;
  display(state_data.value)
}
```

```js
const ephemeral_state = (function() {
    const ephemeral_state = localStorage.getItem('state_data');
    return ephemeral_state !== null && ephemeral_state !== 'null'
        ? state_data.value = JSON.parse(ephemeral_state)
        : state_data.value = template_data;
})();
```




```js echo
const template_data = ({
    name: "Sample Project",
    description: "Initial project data",
    status: "active"
})
```

```js
const load_template_data = view(Inputs.button("Load Template", {reduce: () => swap_data(template_data)}))
```



```js echo
const file_data = ({
    name: "File Project",
    description: "Changed project data",
    status: "pending"
})
```

```js
const load_file_data = view(Inputs.button("Load File Data", {reduce: () => swap_data(file_data)}))
```

```js
let name =  view(Inputs.text({value : state_data.name}))
```

```js
let description =  view(Inputs.text({value : state_data.description}))
```

```js
let status =  view(Inputs.text({value : state_data.status}))
```


```js
let current_state = display(({
  name: name,
  description: description,
  status: status
}))
```


```js
// we will not auto-persist changes
const persist_current_state = view(Inputs.button("Persist Changed Data", {
    reduce: () => {
        localStorage.setItem('state_data', JSON.stringify(current_state))    }
}))
```

```js echo
//localStorage.setItem('state_data', JSON.stringify(current_state));
//"Function applied";
```


```js
import {download} from "./components/download.js";
```


```js
function serialize (data) {
 let s = JSON.stringify(data);
 return new Blob([s], {type: "application/json"}) 
}
```


```js echo
const download_name = "state_data"
```

```js
display(download(serialize(current_state), download_name, "Download Current State"))
```