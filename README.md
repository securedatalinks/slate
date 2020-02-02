<p align="center">sCORe API documentation using slate.</p>

<p align="center"><em>Check the documentation at <a href="https://securedatalinks.github.io/slate">securedatalinks.github.io/slate</a>.</em></p>

Changing and deploying the documentation
------------------------------

### Prerequisites

You're going to need:

 - **Linux or macOS** — Windows may work, but is unsupported.
 - **yaml2js** - `npm install -g yamljs`
 - **widdershins** - `npm install -g widdershins`
 - **Ruby, version 2.3.1 or newer**
 - **Bundler** — If Ruby is already installed, but the `bundle` command doesn't work, just run `gem install bundler` in a terminal.
               — Or you can install directly `sudo apt install ruby-bundler`

### Changing documentation

The whole documentation is generated from *swagger.yaml* file in root directory.
You can use <a href="https://editor.swagger.io">https://editor.swagger.io</a> to comfortably edit *swagger.yaml *and than save the changes locally.

### Deploying locally

1. Change the swagger.yaml source code
2. Run ./deploy.sh --local
3. Visit <a href="http://127.0.0.1:4567/">http://127.0.0.1:4567/</a>

### Deploying to github pages
1. Change the swagger.yaml source code
2. Commit your changes to the swagger.yaml source: `git commit -a -m "Update swagger.yaml"`
3. Push the changes to GitHub: `git push`
4. Run ./deploy.sh

