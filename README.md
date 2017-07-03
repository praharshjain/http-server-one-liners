http-server-one-liners
==========

List of http static server one-liners

Each of these commands will run an ad hoc http static server in your current (or specified) directory, available at http://localhost:8000. Use this power wisely.

### Python 2.x

```shell
$ python -m SimpleHTTPServer 8000
```

### Python 3.x

```shell
$ python -m http.server 8000
```

### Twisted <sub><sup>(Python)</sup></sub>

```shell
$ twistd -n web -p 8000 --path .
```

Or:

```shell
$ python -c 'from twisted.web.server import Site; from twisted.web.static import File; from twisted.internet import reactor; reactor.listenTCP(8000, Site(File("."))); reactor.run()'
```

Depends on [Twisted](http://twistedmatrix.com/trac/wiki/Downloads).

### Ruby

```shell
$ ruby -rwebrick -e'WEBrick::HTTPServer.new(:Port => 8000, :DocumentRoot => Dir.pwd).start'
```

### Ruby 1.9.2+

```shell
$ ruby -run -ehttpd . -p8000
```

### adsf <sub><sup>(Ruby)</sup></sub>

```shell
$ gem install adsf   # install dependency
$ adsf -p 8000
```

*No directory listings.*

### Sinatra <sub><sup>(Ruby)</sup></sub>

```shell
$ gem install sinatra   # install dependency
$ ruby -rsinatra -e'set :public_folder, "."; set :port, 8000'
```

*No directory listings.*

### Perl

```shell
$ cpan HTTP::Server::Brick   # install dependency
$ perl -MHTTP::Server::Brick -e '$s=HTTP::Server::Brick->new(port=>8000); $s->mount("/"=>{path=>"."}); $s->start'
```

### Plack <sub><sup>(Perl)</sup></sub>

```shell
$ cpan Plack   # install dependency
$ plackup -MPlack::App::Directory -e 'Plack::App::Directory->new(root=>".");' -p 8000
```

### Mojolicious <sub><sup>(Perl)</sup></sub>

```shell
$ cpan Mojolicious::Lite   # install dependency
$ perl -MMojolicious::Lite -MCwd -e 'app->static->paths->[0]=getcwd; app->start' daemon -l http://*:8000
```

*No directory listings.*

### http-server <sub><sup>(Node.js)</sup></sub>

```shell
$ npm install -g http-server   # install dependency
$ http-server -p 8000
```

*Note: This server does funky things with relative paths. For example, if you have a file `/tests/index.html`, it will load `index.html` if you go to `/test`, but will treat relative paths as if they were coming from `/`.*

### node-static <sub><sup>(Node.js)</sup></sub>

```shell
$ npm install -g node-static   # install dependency
$ static -p 8000
```

*No directory listings.*

### PHP <sub><sup>(>= 5.4)</sup></sub>

```shell
$ php -S 127.0.0.1:8000
```

*No directory listings.*

### Erlang

```shell
$ erl -s inets -eval 'inets:start(httpd,[{server_name,"NAME"},{document_root, "."},{server_root, "."},{port, 8000},{mime_types,[{"html","text/html"},{"htm","text/html"},{"js","text/javascript"},{"css","text/css"},{"gif","image/gif"},{"jpg","image/jpeg"},{"jpeg","image/jpeg"},{"png","image/png"}]}]).'
```

*No directory listings.*

### busybox httpd

```shell
$ busybox httpd -f -p 8000
```

### webfs

```shell
$ webfsd -F -p 8000
```

Depends on [webfs](http://linux.bytesex.org/misc/webfs.html).

### IIS Express

```shell
C:\> "C:\Program Files (x86)\IIS Express\iisexpress.exe" /path:C:\MyWeb /port:8000
```

Depends on [IIS Express](http://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview).

*No directory listings. `/path` must be an absolute path.*
  
### Clojure
```
$ lein simpleton 8080
```
### Spark(Go)
```
$ go get github.com/rif/spark
$ spark -port 8000 .
``` 
### PowerShell
```
$Hso=New-Object Net.HttpListener;$Hso.Prefixes.Add("http://+:8000/");$Hso.Start();While ($Hso.IsListening){$HC=$Hso.GetContext();$HRes=$HC.Response;$HRes.Headers.Add("Content-Type","text/plain");$Buf=[Text.Encoding]::UTF8.GetBytes((GC (Join-Path $Pwd ($HC.Request).RawUrl)));$HRes.ContentLength64=$Buf.Length;$HRes.OutputStream.Write($Buf,0,$Buf.Length);$HRes.Close()};$Hso.Stop()
```
### NPM
```
$ npm install -g beefy
$ beefy
```
### Rack (ruby)
```
gem install rack --no-ri --no-rdoc
rackup -b 'use Rack::Static, :index => 'README.html'; run Rack::File.new('.')"
```
### Djangothis (Python)
```
$ pip install djangothis
$ djangothis
```
### OCaml
```
$ opam install cohttp async
$ cohttp-server-async
```
### Docker
```
docker run -d -p 8080:80 --name my-apache-app -v "$PWD":/usr/local/apache2/htdocs/ httpd:2.4-alpine
```
### R

Using the servr package:
```
$ Rscript -e 'servr::httd()' -p8000
```

License
----------------
MIT
