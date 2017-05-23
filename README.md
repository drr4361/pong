# pong
//David Rasmussen 5/23/17

PFont font5;

int score = 0;
int paddle_x = 140;
int paddle_len = 50;
int paddle_height = 15;
int ball_xvel = 3; 
int ball_yvel = 3;
int ball_rad = 25;
int ball_xpos = int(random(0,300)); 
int ball_ypos = int(random(0,320));
int game_over = 0;
float x, y, speedX, speedY;
float colo1 = random(255);
float colo2 = random(255);
float colo3 = random(255);


void setup(){
 size(300, 320);
}
void draw(){
 x = width/3;
 y= height/3;
  if (game_over == 0){
    background(colo1, colo2, colo3);
    font5 = loadFont("font5.vlw");
    
   int time = millis()/1000;
        textFont(font5);
        fill(255, 0, 0);
        text("time:" +time, 50, 70);
  
  textFont(font5);
  fill(76, 252, 3);
    text("score:" + score, 35, 20);
  textAlign(TOP, CENTER);
  textSize(30);
    fill(255);
    rect(paddle_x, height-paddle_height, paddle_len, paddle_height);
      ellipse(ball_xpos, ball_ypos, ball_rad, ball_rad);
    if (keyPressed && (key == CODED)) { 
      if (keyCode == LEFT) {
        if (paddle_x > 0){ 
          paddle_x-=2;
       }
      }
      else if (keyCode == RIGHT) {
        if (paddle_x < 270){
          paddle_x+=2;
        }
      }
    }
  
    ball_xpos += ball_xvel;
    ball_ypos += ball_yvel;
    
    if(ball_xpos < 3){
      ball_xvel = 3;
    }
    else if(ball_xpos > (width-3)){
      ball_xvel = -3;
    }
  
    if(ball_ypos < 3){
      ball_yvel = 3;
    }
    else if(ball_ypos > (height-paddle_height-3)){
      if((ball_xpos > paddle_x) && (ball_xpos < (paddle_x+paddle_len))){
        ball_yvel = -3;
        score+=1;
      }
      else{
        game_over = 1;
        background(255);
        textSize(30);
        fill(0);
        text("LOL, u just lost", 40, height/2);
      }
    } 
  }
}
