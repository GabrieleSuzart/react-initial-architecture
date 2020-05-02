## How setup ReactJS from scratch


1 - Create package.json
```
yarn init -y
```

2 - Add React
```
yarn add react react-dom
```

3 - Add Babel and Webpack
```
yarn add @babel/core @babel/preset-env @babel/preset-react webpack webpack-cli
```

```
yarn add webpack-dev-server -D
```

4 - Create file `babel.config.js`
```
module.exports = {
  presets: [
    '@babel/preset-env',
    '@babel/preset-react'
  ]
}
```

5 - Add loaders

5.1 - Babel
```
yarn add babel-loader
```

5.2 - Styles
```
yarn add style-loader css-loader
```

5.3 - Images
```
yarn add file-loader
```


6 - Create folder `public` with file `index.html` 
```
`! + enter` to structure html initial
```

6.1 - Add element root in tag `<body>`
```
<div id="app"></div>
```

7 - Create folder `src` with files `App.js` and `index.js` 

7.1 - src/App.js
```
import React from 'react'

const App = () => {
  return (
    <h1>My app</h1>
  )
}

export default App
```

7.2 - src/index.js
```
import React from 'react'
import { render } from 'react-dom'
import App from './App'

render(<App />, document.getElementById('app'))
```


8 - Create file `webpack.config.js`
```
const path = require('path')

module.exports = {
  entry : path.resolve(__dirname, 'src', 'index.js'),
  output: {
    path: path.resolve(__dirname, 'public'),
    filename: 'bundle.js'
  },
  devServer: {
    contentBase: path.resolve(__dirname, 'public')
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader'
        }
      },
      {
        test: /\.css$/,
        exclude: /node_modules/,
        use: [
          { loader: 'style-loader' },
          { loader: 'css-loader' },
        ]
      },
      {
        test: /.*\.(gif|png|jpe?g)$/i,
        use: [
          { loader: 'file-loader' },
        ]
      }
    ]
  }
}
```

9 - Create scripts in `package.json`
```
"scripts": {
  "dev": "webpack-dev-server --mode development",
  "build": "webpack --mode production"
},
```
