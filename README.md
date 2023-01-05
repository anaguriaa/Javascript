# Javascript
Jogo de Pong em Javascript

//variaveis da bolinha

let xBolinha = 300;
let yBolinha = 200;
let dBolinha = 20;
let raio = dBolinha / 2;


//velicidade da bolinha

let vBolinhax = 5;
let vBolinhay = 5;
let raqueteComprimento = 10;
let raqueteAltura = 60;

//variaveis da raquete
let xRaquete = 5;
let yRaquete =150;

//variaveis do oponente
let xRaqueteOpo = 585;
let yRaqueteOpo = 150;
let vyOpo;
let vBolinhaxOpo ;
let vBolinhayOpo ;

let colidiu = false;

//placar jogo
let meusPontos = 0;
let pontosOpo = 0;

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
  mostraBolinha();
  movimentaBolinha();
  verificaColisaoBolinha();
  mostraRaquete(xRaquete, yRaquete);
  movimentaMinhaRaquete();
  //verificaColisaoRaquete();
  verificaColisaoRaquete(xRaquete,yRaquete);
  mostraRaquete(xRaqueteOpo,yRaqueteOpo);
  movimentaRaqueteOpo();
  verificaColisaoRaquete(xraqueteOpo, yraqueteOpo);
  rect( xraquete,yraquete,raqueteComprimento,raqueteAltura);
  incluirPlacar();
  marcaPonto();
}
function mostraBolinha (){
    circle(xBolinha,yBolinha,dBolinha);
}
function movimentaBolinha(){
  //circle(xBolinha,yBolinha,dBolinha);
  xBolinha += vBolinhax;
  yBolinha += vBolinhay;
}
function verificaColisaoBolinha(){
    
  if(xBolinha  + raio > width || xBolinha - raio < 0){
    vBolinhax *=-1;
  }
    
    if(yBolinha + raio > height|| yBolinha - raio < 0){
      vBolinhay *= -1;
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
function verificaColisaoRaquete(){
  if (xBolinha - raio < xRaquete + raqueteComprimento && yBolinha - raio < yRaquete + raqueteAltura && yBolinha + raio > yRaquete){
    vBolinhax *=-1;
    raquetada.play();
  }
  
}

function verificacolisaoraquete(x,y){
  colidiu =collideRectCircle(x,y, raqueteComprimento, raqueteAltura, xBolinha, yBolinha, raio);
  if(colidiu){
    vBolinhax *=-1;
    raquetada.play();
  }
  
}
function movimentaRaqueteOpo(){
 if(keyIsDown(87)){
    yRaqueteOpo -=10;
  }
  if (keyIsDown(83)){
    yRaqueteOpo +=10;
  }
  
  //vyOpo = yBolinha - yRaqueteOpo - raqueteComprimento / 2 - 30;
 // yRaqueteOpo += vyOpo
}

function incluirPlacar(){
  stroke(255);
  textAlign(CENTER);
  textSize (18);
  fill(color(75,0,130)); 
  rect(150,10,40,20);
  fill(255);
  text(meusPontos, 170,26);
  fill(color(75,0,130)); 
  rect(450,10,40,20);
  fill(255);
  text(pontosDoOpo, 470,26);
}
 function marcaPonto(){
  if (xBolinha > 590){
    meusPontos +=1;
    //ponto.play();
  }
  if(xBolinha < 10){
    pontosDoOpo +=1;
   // ponto.play();
  }
}
