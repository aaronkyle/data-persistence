# Data Persistence

```js
// needed to correctly initialize the chart
const template_data = ({
    name: "Template Project",
    description: "Template Project Data",
    status: "-"
})

// test data
const file_data = ({
    name: "File Project",
    description: "Changed project data",
    status: "pending"
})
```

```js
/// initialize with localStorage, or use a template data file to pre-populate required data fields
let state_data = Mutable(JSON.parse(localStorage.getItem("state_data")) ?? template_data);

function swap_data(data) {
  state_data.value = data;
}

(async function(d) {
    return d === null ? "pending file selection" : state_data.value = await d.json();
})(local_data);
```

```js
const load_template_data = view(Inputs.button("Reset Template", {reduce: () => swap_data(template_data)}))
```

```js
const local_data = view(Inputs.file({
//    label : "Load Project",
    multiple : false,
}))
```

```js
// display( download(serialize(file_data), download_name, "Download Test File"))
```

```js
// const load_file_data = view(Inputs.button("Load File Data", {reduce: () => swap_data(file_data)}))
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
//const persist_current_state = view(Inputs.button("Persist Changed Data", {
//    reduce: () => {
//        localStorage.setItem('state_data', JSON.stringify(current_state))    }
//}))
```

```js
// auto-persist changes
localStorage.setItem('state_data', JSON.stringify(current_state));
"Data Persisted";
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


```js
const download_name = name
```

```js
display(download(serialize(current_state), download_name, "Download Updated Data"))
```