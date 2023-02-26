USEFUL CODE SNIPPETS FOR FURTHER USE ON HTML5 CANVAS!

1.constructor function to make a moving background!with a long image
class background{
constructor(srcX,srcY,fullwidth,swidth,sheight,x,y,width,height,src,type){
this.srcX=srcX;
this.srcY=srcY;
this.swidth=swidth;
this.sheight = sheight;
this.fullwidth=fullwidth;
this.type=type;
this.x=x;
this.y=y;
this.width = width;
this.height = height;
this.image = new Image();
this.image.src = src;
this.curFrame = 0;
}
draw(){
this.updateFrame()
ctx=gameArea.context;
ctx.drawImage(this.image,this.srcX,this.srcY,this.swidth,this.sheight,this.x,this.y,this.width,this.height)
}
updateFrame(){
if(this.srcX>=this.fullwidth-this.width){
this.srcX=0;  
 }
if(!showEndScreen&&!showStartScreen){
if(this.type=='road')this.srcX+=(3.5+speed);
this.srcX+=(0.6+speed);
}

    }

}

2.everyinterval function

function everyinterval(n) {
return ((gameArea.frameNo / n) % 1 == 0) ? true : false;
}

3.Random Number Generator

function getRndInteger(min, max) {
return Math.floor(Math.random() \* (max - min) ) + min;
}

4.JUMP FUNCTIONS SET:
//with an fps of 100;

function moveup(){
if(keyboardMoveUp){
console.log("up called")
//jumpSound.play()
becky.gravitySpeed=-4;
becky.gravity=-.10;
keyboardMoveUp=false;
}

}
function motion(){
console.log('motion called');
becky.gravity=.11;
}
//inside the constructor function
newpos(){
console.log(this.gravitySpeed);
this.gravitySpeed += this.gravity;
this.y +=this.gravitySpeed;

        if(this.y<=160){//less value higher jump performs
            //console.log("exceeds");
            return this.gravity=+.28;//.......the gravitional pull when he reaches maximum height..........!!!!!!!!!!

        }
    }
    hitbottom(){
        let rockbottom=gameArea.canvas.height-this.height;
        if(this.y>rockbottom){
            this.y=rockbottom;

            this.gravitySpeed = -(this.gravitySpeed * this.bounce);
            keyboardMoveUp=true;
        }
    }

//inside the constructor function

//for keyboard Input Handlers
function keyDownHandler(e){
switch (e.keyCode){
case SPACEBAR:moveup();break;
}
}

function keyUpHandler(e){
switch(e.keyCode){//capital c is must camel case
case SPACEBAR:motion();break;
}
}
//for keyboard Input

//if the game starts at a mouseclick

function mouseclick(){
if(showStartScreen){
becky.y=canvas_height-beckyH+.1;

        gameArea.frameNo=0;
        showStartScreen=false;
    }

}

5.To Make the Score appear with zeroes at the front

function MakeScore(y){
if(y<10){
z=`0000000${y}`
}
else if(y>=10&&y<100){
z=`000000${y}`
}
else if(y>=100&&y<1000){
z=`00000${y}`
}
else if(y>=1000&&y<10000){
z=`0000${y}`
}
else if(y>=10000&&y<100000)
{
z=`000${y}`
}
else if(y>=100000&&y<1000000){
z=`00${y}`
}
else if(y>=1000000&&y<10000000){
z=`0${y}`
}
else if(y>=10000000&&y<100000000){
z=`${y}`
}
return z;
}

6.A normal image constructor function

class imageBuilder{
constructor(x,y,width,height,color,type){
this.x=x;
this.y=y;
this.width=width;
this.height=height;
this.image = new Image();
this.image.src = color;  
 this.type=type;
}
draw(){
ctx=gameArea.context;
ctx.drawImage(this.image,this.x, this.y, this.width, this.height);
}

}

7.ScoreDraw function

scoredraw(){
ctx = gameArea.context;
ctx.font = "13px Arial";
score=(gameArea.frameNo/10).toFixed();
// let newScore=MakeScore(score);

            ctx.fillStyle="#535353"
            ctx.fillText(newScore,canvas_width-100,50);//positioning
    }

8.Collision Checker FUNCTION

crashWith(otherobj){
var myleft = this.x;
var myright = this.x + (this.width);
var mytop = this.y;
var mybottom = this.y + (this.height);
var otherleft = otherobj.x;
var otherright = otherobj.x + (otherobj.width);
var othertop = otherobj.y;
var otherbottom = otherobj.y + (otherobj.height);
var crash = true;
if ((mybottom < othertop) || (mytop > otherbottom) || (myright < otherleft) || (myleft > otherright)) {
crash = false;
}
return crash;
}
9.constructor function for spritesheet images

class SPRITEIMAGE{
constructor(srcX,srcY,spritewidth,spriteheight,col,x,y,width,height,src){
this.srcX=srcX;
this.srcY=srcY;
this.swidth=spritewidth/col;
this.sheight = spriteheight;
this.x=x;
this.y=y;
this.width = width;
this.height = height;
this.image = new Image();
this.image.src = src;
this.bounce=0.2;
this.gravity = 0;
this.gravitySpeed = 0;

        this.curFrame = 0;
        this.frameCount = col;

    }
    draw(){
     this.updateFrame()
       ctx=gameArea.context;
       ctx.drawImage(this.image,this.srcX,this.srcY,this.swidth,this.sheight,this.x,this.y,this.width,this.height)

    }
    staticdraw(){
        ctx=gameArea.context;
       ctx.drawImage(this.image,this.srcX,this.srcY,this.swidth,this.sheight,this.x,this.y,this.width,this.height)
    }

    updateFrame(){
        if(this.curFrame>=this.frameCount){
            this.curFrame=0;
        }
        this.srcX = this.curFrame*this.swidth;
        this.curFrame++;
    }

}

10.A sample gameArea Object

var gameArea = {
canvas:document.getElementById('gameCanvas'),

    start:function(){

        this.canvas.width=canvas_width;
        this.canvas.height=canvas_height;

        this.canvas.addEventListener('click',()=>{
            mouseClick();
        })
        this.canvas.addEventListener('touchstart',()=>{
            mouseClick()
        })

        this.context=this.canvas.getContext("2d");
        this.frameNo=0;
        this.interval=setInterval(function(){
           // moveBecky();
            drawEverything();
        },1000/fps);
        document.body.addEventListener("touchstart",moveup);
        document.body.addEventListener("touchend",motion);
    },
    sound:function(src) {//.......................................created audio constructor function here !!!..........
          this.sound = document.createElement("audio");
          this.sound.src = src;
          this.sound.setAttribute("preload", "auto");
          this.sound.setAttribute("controls", "none");
          this.sound.style.display = "none";
          this.sound.volume=0.1;
          document.body.appendChild(this.sound);
          this.play = function(){
            this.sound.play();
          }
          this.stop = function(){
            this.sound.pause();
          }
      },

    clear:function(){
        this.context.clearRect(0, 0, this.canvas.width, this.canvas.height);
    },

    stop:function(){

        clearInterval(this.interval);
    }

}

11.StartGame function with keyboard setup

function startGame(){
window.onkeydown=keyDownHandler;
window.onkeyup=keyUpHandler;

}

12.TO insert random obstacle at a time interval

//this goes inside the drawEverything function
if(gameArea.frameNo==1||everyinterval(250)){//creating obstacle array!!

        gap=(getRndInteger(400,600));
        let i=getRndInteger(0,7);
       // console.log(gameArea.canvas.width+cactus_gap);
        myObstacles.push(obsInput(gameArea.canvas.width,gameArea.canvas.height,gap,objects[i]));

    }

//helper function to insert random objects
function obsInput(canvasW,canvasH,gap,obj){
let img;

    img = new imageBuilder(canvasW+gap,canvasH-obj.height,obj.width,obj.height,obj.src,obj.type);


    return img;

}

13.for loop and arr.slice() to remove an array element after collision check:

for(let i=0;i<myBridies.length;i++){//checking clash with the birds........................................!!!!
if(becky.crashWith(myBridies[i])){

            myBridies.splice(i,2);
            i--;
            becky.reset();
        }
    }

14.TO calculate mousepostion……….
function calculateMousePos(evt){//............................Calculating mouse position.................................
var rect = gameArea.canvas.getBoundingClientRect();
var root = document.documentElement;
var mouseX=evt.clientX - rect.left - root.scrollLeft;
var mouseY= evt.clientY - rect.top - root.scrollTop;
return{
x:mouseX,
y:mouseY
};

}

this.canvas.addEventListener('mousemove',function(evt){ //............Using the calculated mouse position
var mousePos = calculateMousePos(evt);
console.log(mousePos.x,mousePos.y)

            });

15.TO save score in the localStorage!

function saveScore(){//new functions added here........................
let name = prompt('Enter UserName');
let pass = prompt('Enter passWord');

    localStorageCheck();
    infos.forEach(element => {
        if(element[0]==name&&element[2]==pass){
            element.push(score);
            errorElement.innerText='ScoreSaved!Check The LeaderBoard!';
       }

    });
    localStorage.setItem("infos",JSON.stringify(infos));

}
function localStorageCheck(){//checking for local storage availability..........

if(localStorage.getItem('infos')==null){
infos=[];
}else{
infos=JSON.parse(localStorage.getItem('infos'));
}

}

16.mobile device detector:
function detectMob() {
const toMatch = [
/Android/i,
/webOS/i,
/iPhone/i,
/iPad/i,
/iPod/i,
/BlackBerry/i,
/Windows Phone/i
];

    return toMatch.some((toMatchItem) => {
        return navigator.userAgent.match(toMatchItem);
    });

}

17.To add Sinusoidal movement to an object :
sinusoidalMove()
{
this.x-=2;
this.y=(canvas_height/2-ufo_h/2+100)+Math.cos(this.x*0.025)*35;
}

Here .025 is the angle , 35 is the amplitude , and ((canvas_height/2 - ufo_h/2 -100 )is the primary spawn height;

18.To Draw a line On canvas

function lineDraw(x1,y1,x2,y2)
{
ctx = myGameArea.context
// set line stroke and line width
ctx.strokeStyle = 'red';
ctx.lineWidth = 5;

     // draw a red line
     ctx.beginPath();
     ctx.moveTo(x1, y1);
     ctx.lineTo(x2, y2);
     ctx.stroke();

}

19.Date Formatter Function

class DateTime {
constructor(date) {
this.date = date;
this.ctime = Date.parse(this.date);
}
time() {
return (this.time = Date.parse(this.date));
}
formattedDate() {
return dateToYMD(this.date);
}
}
function dateToYMD(date) {
let dateArr = date.split("-");
let months = [
"Jan",
"Feb",
"Mar",
"Apr",
"May",
"Jun",
"Jul",
"Aug",
"Sep",
"Oct",
"Nov",
"Dec",
];
let year = dateArr[0];
let month = dateArr[1];
let day = dateArr[2];
switch (month) {
case "01":
month = months[0];
break;
case "02":
month = months[1];
break;
case "03":
month = months[2];
break;
case "04":
month = months[3];
break;
case "05":
month = months[4];
break;
case "06":
month = months[5];
break;
case "07":
month = months[6];
break;
case "08":
month = months[7];
break;
case "09":
month = months[8];
break;
case "10":
month = months[9];
break;
case "11":
month = months[10];
break;
case "12":
month = months[11];
break;

    default:
      break;

}

return `${day}-${month}-${year}`;
}
