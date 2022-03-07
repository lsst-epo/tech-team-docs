Helper function creates reusable axios instance with `baseUrl` set based on node environmental variable:

```
import axios from 'axios';

const getBaseUrl = function(env) {
  const envs = {
    development: '/',
    staging: '/',
    production: 'https://lsst-epo.github.io/a-window-to-the-stars/',
  };

  return envs[env] || '/';
};

export default axios.create({
  baseURL: getBaseUrl(process.env.NODE_ENV),
});
```

In the `componentDidMount()` lifeycle method of a React Component:

```
import API from 'PATH/TO/API';

...

API.get('static-data/EXAMPLE-DATA.json')
  .then(res => {
    console.log(res.data)
    this.setState(prevState => {
      ...prevState,
      data: res.data
    });

...
```
