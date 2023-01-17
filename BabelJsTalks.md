how to enable import in my js file

To enable import statements in your JavaScript file, you will need to use a JavaScript transpiler, such as Babel, to convert your code to a version of JavaScript that is compatible with the version that your runtime environment supports.

You can use Babel to transpile your code by installing it as a development dependency in your project:
```
npm install --save-dev @babel/core @babel/cli @babel/preset-env
```
You also need to create a configuration file .babelrc in the root of your project with the following contents:
```
{
  "presets": ["@babel/preset-env"]
}
```
This tells Babel to use the @babel/preset-env preset, which automatically determines the necessary transformations for your code to run in the target environment.

Once you have done this, you can use the command line to transpile your code:
```
npx babel yourFile.js --out-file yourTranspiledFile.js
```
This will create a new file yourTranspiledFile.js that can be used in your runtime environment, which includes the import and export statements.

You also can use babel-loader with webpack to transpile your code during the build process.

Please note that, starting from ECMAScript 6, JavaScript natively supports the import and export statements. Some environments also supports it by default, such as Node.js version 12.0.0 and above.
Musarrat Chowdhury
i have web pack 

Great! If you have webpack set up in your project, you can use babel-loader to transpile your JavaScript code during the build process.

You will need to install babel-loader and any necessary dependencies for your project:
```
npm install --save-dev babel-loader @babel/core @babel/preset-env
```
Then, you will need to add the babel-loader to your webpack configuration file, typically called webpack.config.js. The configuration should look something like this:
```
module.exports = {
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env']
          }
        }
      }
    ]
  }
};
```
This configuration tells webpack to use babel-loader to transpile all files with a .js extension, except for files in the node_modules directory, using the @babel/preset-env preset.

You can also configure babel to add additional plugins or preset to your configuration.

You should also create a .babelrc file in the root of your project, with at least the following contents:
```
{
  "presets": ["@babel/preset-env"]
}
```
This tells Babel to use the @babel/preset-env preset, which automatically determines the necessary transformations for your code to run in the target environment.

Once you have done this, you can run your webpack build command, and it will transpile your code using babel and bundle it.

You also can use babel-polyfill to support the features not supported by your target environment.