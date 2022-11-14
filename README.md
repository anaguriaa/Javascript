# Javascript
Jogo de Pong em Javascript

//variaveis da bolinha

let xbolinha = 300;
let ybolinha = 200;
let dbolinha = 20;
let raio = dbolinha / 2;


//velicidade da bolinha

let vbolinhax = 5;
let vbolinhay = 5;
let raquetecomprimento = 10;
let raquetealtura = 60;

//variaveis da raquete
let xraquete = 5;
let yraquete =150;

//variaveis do oponente
let xraqueteopo = 585;
let yraqueteopo = 150;
let vyopo;
let vbolinhaxopo ;
let vbolinhayopo ;

let colidiu = false;

//placar jogo
let meuspontos = 0;
let pontosdoopo = 0;

//sons do jogo 
let raquetada ;
let ponto;
let trilha;

function preload(){
  trilha = loadSound("trilha[1].mp3");
  pontos = loadSound("ponto[2].mp3");
  raquetada = loadSound("raquetada[1].mp3");
}
function setup() {
  createCanvas(600, 400);
  trilha.loop();
  //ponto.play();
}
function draw() {
  background(0); 
  mostrabolinha();
  movimentabolinha();
  verificacolisaobolinha();
  mostraraquete(xraquete, yraquete);
  movimentaminharaquete();
  //verificacolisaoraquete();
  verificacolisaoraquete(xraquete,yraquete);
  mostraraquete(xraqueteopo,yraqueteopo);
  movimentaraqueteopo();
  verificacolisaoraquete(xraqueteopo, yraqueteopo);
  rect( xraquete,yraquete,raquetecomprimento,raquetealtura);
  incluirplacar();
  marcaPonto();
}
function mostrabolinha (){
    circle(xbolinha,ybolinha,dbolinha);
}
function movimentabolinha(){
  //circle(xbolinha,ybolinha,dbolinha);
  xbolinha += vbolinhax;
  ybolinha += vbolinhay;
}
function verificacolisaobolinha(){
    
  if(xbolinha  + raio > width || xbolinha - raio < 0){
    vbolinhax *=-1;
  }
    
    if(ybolinha + raio > height|| ybolinha - raio < 0){
      vbolinhay *= -1;
    }
  
}
function mostraraquete(x,y){
  rect( x,y,raquetecomprimento,
       raquetealtura);
}
function movimentaminharaquete(){
  if(keyIsDown(UP_ARROW)){
    yraquete -=10;
  }
  if (keyIsDown(DOWN_ARROW)){
    yraquete +=10;
  }
}
function verificacolisaoraquete(){
  if (xbolinha - raio < xraquete + raquetecomprimento && ybolinha - raio < yraquete + raquetealtura && ybolinha + raio > yraquete){
    vbolinhax *=-1;
    raquetada.play();
  }
  
}

function verificacolisaoraquete(x,y){
  colidiu =collideRectCircle(x,y, raquetecomprimento, raquetealtura, xbolinha, ybolinha, raio);
  if(colidiu){
    vbolinhax *=-1;
    raquetada.play();
  }
  
}
function movimentaraqueteopo(){
 if(keyIsDown(87)){
    yraqueteopo -=10;
  }
  if (keyIsDown(83)){
    yraqueteopo +=10;
  }
  
  //vyopo = ybolinha - yraqueteopo - raquetecomprimento / 2 - 30;
 // yraqueteopo += vyopo
}

function incluirplacar(){
  stroke(255);
  textAlign(CENTER);
  textSize (18);
  fill(color(75,0,130)); 
  rect(150,10,40,20);
  fill(255);
  text(meuspontos, 170,26);
  fill(color(75,0,130)); 
  rect(450,10,40,20);
  fill(255);
  text(pontosdoopo, 470,26);
}
 function marcaPonto(){
  if (xbolinha > 590){
    meuspontos +=1;
    //ponto.play();
  }
  if(xbolinha < 10){
    pontosdoopo +=1;
   // ponto.play();
  }
}
