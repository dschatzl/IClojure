![IClojure](https://i.imgur.com/PkyAoD7.png)
# A Jupyter kernel for Clojure based on the Unrepl protocol.
  - Inspired by (and bootstrapped from) the Clojupyter project.
  - Evaluate Clojure code on either a local or remote socket repl (port-forwarding)
  - Ship dependencies to remote repl only when needed
  - Avoids printing large results with configurable data structure elision
  - Render HTML, Latex, and Markdown

### Try it!

```sh
docker run -p 8888:8888 cgrand/iclojure
```

Watch the output for a url and/or a token, for example:
```
[I 13:10:02.189 LabApp] The Jupyter Notebook is running at:
[I 13:10:02.189 LabApp] http://(c94e72d6fe5f or 127.0.0.1):8888/?token=0212d3870d2feb2a4148045e5b1df77460dc4618fe6854d2
```

Go to localhost:8888 and enter the token (`0212d3870d2feb2a4148045e5b1df77460dc4618fe6854d2` above).

This docker image is built using the `Dockerfile` provided in this repository. In addition to the kernel istelf, the `iclojure_extension` is enabled which allows interactive browsing (both elided collections and REBL-like view).

A volume can be mounted under `/notebooks` to persist notebooks.

### Installation

IClojure is designed to work with either [Jupyter](https://github.com/jupyter/notebook) or [Jupyter Lab](https://github.com/jupyterlab/jupyterlab).  Future work is primarly targeting the Juptyer Lab environment.

[Conda](https://conda.io/docs/user-guide/install/index.html) v.4.5+ is required.

Install the dependencies .

```sh
$ conda upgrade conda
$ conda install jupyter
$ git clone https://github.com/HCADatalab/IClojure
$ cd IClojure
$ make; make install; cd -
```
### Usage
By default when you open a new notebook you are connected to the JVM running the kernel.

To connect to a Remote Socket REPL, use:
```Connect to a Remote Socket REPL
/connect localhost:port
```

To reconnect to the local JVM:
```Connect to Local JVM
/connect -
```

Add clojure dependencies to classpath
```
/cp some-deps.edn-map
```
```
/cp (form that evaluates to a deps.edn map)
```

Render MIME
```
#unrepl/mime {:content-type "text/html" :content "<h1>Hello <i>#unrepl</i></h1>"}
```
```
#unrepl/mime {:content-type "text/markdown" :content "# Hello *unrepl* in Markdown"}
```
```
#unrepl/mime {:content-type "text/latex" :content "$$E=mc^2$$"}
```
```
#unrepl/mime {:content-type "application/vnd.vegalite.v2+json"
              :content   {:data {:values [{:animal :horse :amount 40}{:animal :dog :amount 60}]}
                          :mark :bar
                          :encoding {:x {:field :amount} 
                                     :y {:field :animal :type :ordinal}}}}
```
![Alt text](images/vega-lite-bar-plot.png)

### Experimental
Currently working on IClojure JupyterLab Extension for mouse-driven lazy-loading.  Code is included in this repo, but documentation is still forth coming.

### License

Copyright © 2015-2017 HCA

Distributed under the Eclipse Public License either version 1.0 or (at your option) any later version.

Initially derived from MIT-Licensed Clojupyter © 2014 Rory Kirchner. 
