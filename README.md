# Angular2 Skeleton - new libs
Node, Express, TypeScript, Gulp, BrowserSync, Angular2 application skeleton.

Provided for developing **Angular2** applications using **Typescript** served over **node-express** server.

### Prerequisites
Must have node and npm installed

### How to use
No need to install npm packages because we are using **https://unpkg.com**.

Install typescript definitions using:
```sh
$ typings install
```

Start application with 
```sh
$ gulp
```

Application will be initialy compiled and started. By default the server is listening on port 3036. Client application (Angular2) can be accessed through your web browser on the following url **localhost:3036/angular**. If everything is ok you should see the message *Proba*. displayed in your browser.

### Under the hood

**Server application** in *typescript* and transpiled application are located in **./server** folder. Build application using **gulp** build system. 

**Server application** is **node-express** web server initialy configured to listen for requests on **localhost:3036**. All request are redirected to SPA Angular2 application.

BrowserSync is proxing from **localhost:3000**.   


**Client application** in *typescript* and transpiled application are located in **./client/app** folder.

Folder **./client/app/** contains following *TypeScript* files

```
app.component.ts
app.module.ts
main.ts
```
taken from the official Angular2 web page quickstart https://angular.io

###History
- changed *server_app.ts*:
1. **_renderPage** method to
```
private _renderPage(req: express.Request, res: express.Response){ 
        res.sendFile(path.resolve(__dirname, '../client'+req.params[0]));
    }
```
2. no more /www path configured from server

####27-03-2017
- switched to commonjs modules in client application (changed tsconfig.json).
1. Changes in template *app.component.html* :
With *system* modules we define:
```
@Component({
  moduleId: __moduleName,
  selector: 'my-app',
  templateUrl: './app.component.html'
})
```
With *commonjs* modules we define
```
     moduleId: module.id,
     selector: 'my-app',
     templateUrl: './app.component.html'
```
because **module.id** is provided by the **commonjs** module. Now relative paths are operational.

####28-03-2017
- created gulp tasks **clean_docs** and **make_docs** to clean dir and copy necessary files to docs
folder for github pages
- removed docs3 from tracking but leave locally 