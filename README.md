# Webpack

webpack is a `static module bundler` for modern JavaScript applications. 

webpack-cli init is used to initialize webpack projects quickly by `scaffolding configuration` and `installing modules required` for the project as per user preferences.


-----------

## Input related configurations

### context
> The base directory, an **absolute path**, for resolving entry points and loaders from configuration.

```js
module.exports = {
  context: path.resolve(__dirname, 'app')
};
```

### entry
> The point or points to enter the application.

```js
module.exports = {
  entry: ['@babel/polyfill', 'src/index.js']
};
```

### resolve
> change how modules are resolved.

- resolve.modules
>What `directories` should be searched when resolving **modules**

```js
module.exports = {
  // The src takes precedence over node_modules/
  resolve: {
    modules: [path.resolve(__dirname, 'src'), 'node_modules']
  }
};
```

- resolve.alias
> Create aliases to import or require certain modules more easily.

```js
module.exports = {
  resolve: {
    alias: {
      Utilities: path.resolve(__dirname, 'src/utilities/'),
      Templates: path.resolve(__dirname, 'src/templates/')
    }
  }
};

- import Utility from '../../utilities/utility';
+ import Utility from 'Utilities/utility';
```

- resolve.extensions
> Attempt to resolve these extensions in order. If multiple files share the same name but have 
different extensions, webpack will resolve the one with the extension listed first in the array 
and skip the rest.

```js
module.exports = {
  extensions: ['.js', '.json', '.jsx'],
};


```

- resolve.mainFiles
> The `filename` to be used while resolving **directories**.

```js
module.exports = {
  resolve: {
    mainFiles: ['index']
  }
};
```

## Process related configurations

### module
>  Determine how the different types of modules within a project will be treated.

```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        loader: 'babel-loader',
        options: {
          presets: ['@babel/preset-env']
        }
      }
    ]
  }
};

```

### plugins
> Customize the webpack build process in a variety of ways.

```js
module.exports = {
  plugins: [
    new webpack.DefinePlugin({
      'process.env.NODE_ENV': '"production"',
    }),
    new CleanWebpackPlugin(),
    new HtmlWebpackPlugin({title: 'Development'})
  ]
};
```

## Output related configurations

### target
> Instructs webpack to target a specific environment.

```js
module.exports = {
  target: 'node' // defaults to web
}
```

### output
> Instructing webpack on `how` and `where` it should output your bundles, assets and something else.

```js
module.exports = {
  output: {
    library: 'someLibName',
    libraryTarget: 'umd',
    filename: 'someLibName.js',
  }
}
```

-----------------------

## Mode related configurations

### mode
> Providing the `mode` configuration option tells webpack to use its `built-in` optimizations accordingly.

```js
module.exports = {
  mode: 'production' // none, development or production(default)
};
```

### devServer
> Affect the behavior of webpack-dev-server

```js
module.exports = {
  devServer: {
    contentBase: path.join(__dirname, 'dist'),
    compress: true,
    port: 9000
  }
};
```

### optimization
> optimizations for you depending on the chosen **mode**, available for manual configuration and overrides.

```js
module.exports = {
  //...
  optimization: {
    namedModules: true
  }
};
```

### devtool
> Controls `if` and `how` **source maps** are generated.

```js
module.exports = {
    mode: 'development',
+   devtool: 'inline-source-map',
}

module.exports = {
    mode: 'production',
+   devtool: 'source-map ',
}

```
