# ang2-phaser

### What Am I?!
An easy way to implement the Phaser game engine for Angular2 components.

### Installation
First, make sure you include phaser in your node_modules.  This will need to be linked to the phaser directive directly (example below).
```
npm install phaser
```
<br>
Next, alter your systemjs.config.js to include the right pathing.<br>
```
  var map = {
    'app':                        'app', // 'dist',
    '@angular':                   'node_modules/@angular',
    'angular2-in-memory-web-api': 'node_modules/angular2-in-memory-web-api',
    'rxjs':                       'node_modules/rxjs',
    'ang2-phaser':                'node_modules/ang2-phaser'
  };
  
  var packages = {
    'app':                        { main: 'main.js',  defaultExtension: 'js' },
    'rxjs':                       { defaultExtension: 'js' },
    'angular2-in-memory-web-api': { main: 'index.js', defaultExtension: 'js' },
    'ang2-phaser':                { defaultExtension: 'js' }
  };

```
Then include the module in your scripts (including the functions and declarations).<br>
```

import {Component} from '@angular/core';
import {NG2_PHASER}  from '../../../node_modules/ang2-phaser/ng2phaser'

declare var __phaser:any;

@Component({
    selector: 'my-app',
    templateUrl: './app/components/my-app/main.html',
    directives: [ NG2_PHASER ],
   template: `
     <center>
       <h1>Angular2 - Phaser Demo</h1>
       <phaser (phaser)="phaserLink1($event)" [settings]="{file:'node_modules/phaser/build/phaser.min.js'}"></phaser>
     </center>
   `
})
export class AppComponent {


   //---------------
   phaserLink1(phaser:any){

      var js = document.createElement("script");
          js.type = "text/javascript";
          js.src = '../../../node_modules/ang2-phaser/game/phaser1_demo.js';
          document.body.appendChild(js);
          js.onload = function(){
             __phaser.game.init(phaser.container, this);
          }
   }
   //---------------

   //---------------
   destroyGame(){
      __phaser.destroyGame(function(){
            // do something
      });
   }
   //---------------


}
```

### What's up with the declare var __phaser:any;
So if you look at the demo game file (in game/phaser1_demo.js), you'll see that the whole thing is wrapped in the object __phaser.  Because of how everything is loaded, the __phaser object makes it so that they all eventually line up.  While we're on the subject, I'd recommend leaving the __phaser if you're just starting out but it doesn't *have* to be setup this way.  

```
//--------------
__phaser = {

    gameObj: null,

    //-------------------
    game:{

      //-------------------
      init(canvasEle, appComponent){
              // create game object
              var game = new Phaser.Game(800, 500, Phaser.AUTO, canvasEle, { preload: preload, create: create, update: update });
              var gameState = "preload"

              // assign it
              __phaser.gameObj = game;


            //-----------------------  PRELOAD
            function preload() {
            }
            //-----------------------

            //-----------------------  CREATE
            function create() {


            }
            //-----------------------


            //-----------------------
            function loadStart() {
            }
            //-----------------------

            //-----------------------
            function fileComplete(progress, cacheKey, success, totalLoaded, totalFiles) {
            }
            //-----------------------

            //-----------------------
            function preloaderUpdate(){
            }
            //-----------------------

            //-----------------------
            function loadComplete() {
            }
            //-----------------------


            //-----------------------
            function startGame(){
            }
            //-----------------------

            //-----------------------
            function gameplayUpdate(){
            }
            //-----------------------


            //-----------------------  UPDATE
            function update() {
            }
            //-----------------------



      },



    },
    //-------------------


    //-------------------
    destroyGame(callback){
          this.gameObj.destroy();
          callback();
    }
    //-------------------


}
//--------------
```

### Version
1.0.0


### Live Demo 
Coming soon!

### Dependencies
- Phaser

### NPM / Bower
```
npm install ang2-phaser --save
```




License
----

MIT - go nuts y'all.
