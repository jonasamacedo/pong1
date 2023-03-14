# pong1
//Usar S e R para o Player 1
//Usar setas parao Player 2
//variáveis da bolinha
//let xBolinha = 300;
//let yBolinha = 200;
let xBolinha = 300;
let yBolinha = 200;
let l1 = 50;
let l2 = 50;

//verificação da velocidade da bolinha
let velocidadexBolinha = 4;
let velocidadeyBolinha = 4;

//variáveis da raquete
let xRaquete = 5;
let yRaquete = 150;
let raqueteComprimento = 100;
let raqueteAltura = 90;
let colidiu = false;

//variáveis do oponente
let xRaqueteOponente = 485;
let yRaqueteOponente = 150;
let velocidadeYOponente;
let dOponenteBolinha;

//variáveis para inclusao das imagens
let img1;
let img2;
let img3;
let img4;
let img5;

//placar do jogo
let meusPontos = 0;
let pontosOponente = 0;

//som do jogo
let raquetada;
let pontoPlayer1;
let pontoPlayer2;
let trilha;

//erro da raquete do oponente
let chanceDeErrar = 0;

function preload(){
  trilha = loadSound("TrilhaDinheiro.mp3");
  pontoPlayer1 = loadSound("pontoPlay1Joao.wav");
  pontoPlayer2 = loadSound("pontoPlay2IloIA.wav");
  raquetada = loadSound("Low Whoosh.wav");
  img1 = loadImage('fundo.jpg')
  img2 = loadImage('player 1.png');
  img3 = loadImage('Dinheiro.png');
  img4 = loadImage('player 1.png');
  img5 = loadImage('player 2.png');
 
}

function setup() {
  createCanvas(600, 400);
  trilha.loop();
}

function draw() {
  background(img1);
  mostraBolinha();
  movimentaBolinha();
  verificaColisaoBorda();
  mostrarRaquetePlayer1();
  movimentaRaquete();
  //verificaColisaoRaquete();
  verificacolisaoRaqueteBibliotecaPlayer1(xRaquete,yRaquete);
  mostrarRaquetePlayer2();
  movimentaRaqueteOponente();
  verificacolisaoRaqueteBibliotecaPlayer2(xRaqueteOponente,yRaqueteOponente);
  incluePlacar();
  marcaPonto();
  calculaChanceDeErrar();
  bolinhaNaoFicaPresaPlayer1();
//  bolinhaNaoFicaPresaPlayer2();
}

function mostraBolinha(){
  // fill(138, 43, 226);
  image(img3, xBolinha, yBolinha, l1, l2);
  //circle(xBolinha, yBolinha, diametro);
}

function movimentaBolinha(){
  xBolinha += velocidadexBolinha;
  yBolinha += velocidadeyBolinha;
}

function verificaColisaoBorda(){
    if (xBolinha + l2 > width || xBolinha < 0){
    velocidadexBolinha *= -1;
  }
   if (yBolinha + l2 > height || yBolinha < 0){
    velocidadeyBolinha *= -1;
  }
}

function mostrarRaquetePlayer1(x,y){
 // fill(255, 117, 24);
  image(img4, xRaquete,yRaquete, raqueteComprimento, raqueteAltura);
  // rect(x, y, raqueteComprimento, raqueteAltura);
}

function mostrarRaquetePlayer2(x,y){
  image(img5,xRaqueteOponente,yRaqueteOponente, raqueteComprimento, raqueteAltura);
}

function movimentaRaquete(){
   if (keyIsDown(87)){
    yRaquete -= 10;
  }
  if (keyIsDown(83)){
    yRaquete += 10;
  }
}

function verificaColisaoRaquete(){
  if (xBolinha - raio < xRaquete + raqueteComprimento && yBolinha - raio < yRaquete + raqueteAltura && yBolinha + raio > yRaquete){
    velocidadexBolinha *= -1;
  } 
}

function verificacolisaoRaqueteBibliotecaPlayer1(x,y){
  colidiu = 
  collideRectRect(x, y, raqueteComprimento, raqueteAltura, xBolinha, yBolinha, l1, l2)
 if (colidiu){velocidadexBolinha *= -1
              raquetada.play();}
}

function verificacolisaoRaqueteBibliotecaPlayer2(x,y){
  colidiu = 
  collideRectRect(x, y, raqueteComprimento, raqueteAltura, xBolinha, yBolinha, l1, l2)
 if (colidiu){velocidadexBolinha *= -1
              raquetada.play();}
}

function movimentaRaqueteOponente(){
    if (keyIsDown(UP_ARROW)){
    yRaqueteOponente -= 10;
  }
    if (keyIsDown(DOWN_ARROW)){
   yRaqueteOponente += 10;
  }  

//  velocidadeYOponente = yBolinha - yRaqueteOponente - raqueteComprimento / 2 - 25
//  yRaqueteOponente += velocidadeYOponente + chanceDeErrar;
  
}


function incluePlacar(){
  stroke(255, 255, 0);
  textAlign(CENTER);
  textSize (21);
  fill(255, 117, 24);
  rect(150,10,40,26);
  fill(255);
  text(meusPontos, 170, 29);
  fill(255, 117, 24);
  rect(450,10,40,26);
  fill(255);
  text(pontosOponente, 470, 29);
}

function marcaPonto(){
  if (xBolinha > 549){
    meusPontos += 1
    pontoPlayer1.play();
  }
  if (xBolinha < 1){
    pontosOponente += 1
    pontoPlayer2.play();
  }
}

function calculaChanceDeErrar() {
  if (pontosOponente >= meusPontos) {
    chanceDeErrar += 1
    if (chanceDeErrar >= 39){
    chanceDeErrar = 40
    }
  } else {
    chanceDeErrar -= 1
    if (chanceDeErrar <= 35){
    chanceDeErrar = 35
    }
  }
}

function bolinhaNaoFicaPresaPlayer1(){
    if (xBolinha - 1 <= 0){
    xBolinha = 99
    }
}

//function bolinhaNaoFicaPresaPlayer2(){
//   if (xBolinha - 500 > 0){
 //   yBolinha = 300;
//    }
//}
