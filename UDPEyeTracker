//Processing sketch for Eyetracker. This sketch is used to map out the area for the tracker.


import gazetrack.*;
import hypermedia.net.*;


UDP udp; // define the UDP object
GazeTrack gt;
color backgroundColor;

String ip = "192.168.0.132"; // the remote IP address
int port = 8888; // the destination port


long previousMillis = 0;
int light = 0;
long interval = 500;
int flicker = 0;
int held = 0;

int x1;
int x2;
int x3;

int y1;
int y2;
int y3;

int Color1 = 0;
int Color2 = 0;
int Color3 = 0;
int Color4 = 0;

void setup(){
  udp = new UDP( this, 8888 );
  udp.listen( true ); 
  background(255);
  //size(200, 200);
  fullScreen();
  
  x1 = 0;
  x2 = width/2;
  x3 = height;
  
  y1 = 0;
  y2 = height/2;
  y3 = height;
  
  gt = new GazeTrack(this);
  
}

void draw(){
  
  background(255);
  
  if (flicker == 1){
if (previousMillis < millis() - interval){
previousMillis = previousMillis + interval;
if (light == 0){
byte[] message = new byte[2];
message[0] = 0;
message[1] = 0;
udp.send(message, ip , port);
light = 1;
}
else {
byte[] message = new byte[2];
message[0] = 0;
message[1] = 1;
udp.send(message, ip , port);
light = 0;
}
}
 }
 
  fill(#000000);
  rect(gt.getGazeX(), gt.getGazeY(), 20, 20);
  
  line(0, height/2, width, height/2); //Horizontal Line
  
  line(width/2, height, width/2, 0); //Vertical Line
  
  if(gt.getGazeX() <= x2 && gt.getGazeX() > x1 && gt.getGazeY() <= y2){   // Top Left
    fill(Color1);
    rect(x1, y1, x2, y2);
    
    
    Color1 = Color1 + 1;
    
    Color2 = 0;
    Color3 = 0;
    Color4 = 0;
    
    {byte[] message = new byte[2];
message[0] = 0;
message[1] = 0;
udp.send(message, ip , port);
light = 1;}
   
  }
  else if(gt.getGazeX() <= x2 && gt.getGazeX() > x1 && gt.getGazeY() <= y3){   // Bottom Left
    fill(Color2);
    rect(x1,y2,x2,y2);
    
    Color2 = Color2 + 1;
    
    Color1 = 0;
    Color3 = 0;
    Color4 = 0;
 
  }
  else if(gt.getGazeX() >= x2 && gt.getGazeX() >= y1 && gt.getGazeY() <= y2){ // Top Right
    fill(Color3);
    rect(x2, y1, x3, y2);
    
    Color3 = Color3 + 1;
    
    Color1 = 0;
    Color2 = 0;
    Color4 = 0;
   
  }
  else if(gt.getGazeX() >= x2 && gt.getGazeY() >= y2 && gt.getGazeY() < y3){ // Bottom Right
    fill(Color4);
    rect(x2, y2, x3, y3);
    
    Color4 = Color4 + 1;
    
    Color1 = 0;
    Color3 = 0;
    Color2 = 0;
    
   { byte[] message = new byte[2];
message[0] = 0;
message[1] = 1;
udp.send(message, ip , port);
light = 0;}
    
    
  }
  else{
    Color1 = 0;
    Color2 = 0;
    Color3 = 0;
    Color4 = 0;
  }
  
}


void gazeStopped()
{
  println("Where is the user?!");
  backgroundColor = #FFFFFF;
}

void gazeStarted()
{
  println("Here he is!");
  backgroundColor = #ADFFB1;
}
