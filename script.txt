var fgImage = null, temp = null;
var fgCan;

function upload(){
  //Get input from the input
	var fileinput = document.getElementById("imgfile");
	//Make new SimpleImage from fileinput
	fgImage = new SimpleImage(fileinput);
  temp = fgImage;
	//Get Canvas
	fgCan = document.getElementById("can");
	fgImage.drawTo(fgCan);
}

function getrandomint(min, max) {
  return Math.round(Math.random() * (max - min) + min);
}

function makeBlur(){
  var fileinput = document.getElementById("imgfile");
  //Make new SimpleImage from fileinput
  temp = new SimpleImage(fileinput);
  var randomInt = getrandomint(-10, 10);
  for (var pixel of fgImage.values()) {
    if (Math.random() < 0.5) {
      var newPosX = pixel.getX() + randomInt;
      var newPosY = pixel.getY() + randomInt;
      if (newPosX < 0) {
        newPosX = pixel.getX();
      }
      if (newPosY < 0) {
        newPosY = pixel.getY();
      }
      if (newPosX > fgImage.getWidth() - 1) {
        newPosX = pixel.getWidth() - 1;
      }
      if (newPosY > fgImage.getHeight() - 1) {
        newPosY = pixel.getHeight() - 1;
      }
      fgImage.setPixel(
        pixel.getX(),
        pixel.getY(),
        fgImage.getPixel(newPosX, newPosY)
      );
    }
  }
  //Get Canvas
  fgCan = document.getElementById("can");
  //Display new image
  fgImage.drawTo(fgCan);
}

function makeGrayscale(){
  var fileinput = document.getElementById("imgfile");
	//Make new SimpleImage from fileinput
	temp = new SimpleImage(fileinput);
  //change all pixels of image to gray
  for (var pixel of fgImage.values()) {
    var avg = (pixel.getRed() + pixel.getGreen() + pixel.getBlue())/3;
    pixel.setRed(avg);
    pixel.setGreen(avg);
    pixel.setBlue(avg);
  }
  //Get Canvas
  fgCan = document.getElementById("can");
  //Display new image
  fgImage.drawTo(fgCan);
}

function makeRainbow(){
  var fileinput = document.getElementById("imgfile");
  //Make new SimpleImage from fileinput
  temp = new SimpleImage(fileinput);
  var sect = fgImage.getHeight() / 7;
  for (var pixel of fgImage.values()) {
    var avg = (pixel.getRed() + pixel.getBlue() + pixel.getGreen()) / 3;
    if (avg < 128 && pixel.getY() < sect) {
      pixel.setRed(avg * 2);
      pixel.setGreen(0);
      pixel.setBlue(0);
    } else if (avg >= 128 && pixel.getY() < sect) {
      pixel.setRed(255);
      pixel.setGreen(2 * avg - 255);
      pixel.setBlue(2 * avg - 255);
    } else if (avg < 128 && pixel.getY() > sect && pixel.getY() < sect * 2) {
      pixel.setRed(avg * 2);
      pixel.setGreen(0.8 * avg);
      pixel.setBlue(0);
    } else if (avg >= 128 && pixel.getY() > sect && pixel.getY() < sect * 2) {
      pixel.setRed(255);
      pixel.setGreen(1.2 * avg - 51);
      pixel.setBlue(2 * avg - 255);
    } else if (
      avg < 128 &&
      pixel.getY() > sect * 2 &&
      pixel.getY() < sect * 3
    ) {
      pixel.setRed(avg * 2);
      pixel.setGreen(avg * 2);
      pixel.setBlue(0);
    } else if (
      avg >= 128 &&
      pixel.getY() > sect * 2 &&
      pixel.getY() < sect * 3
    ) {
      pixel.setRed(255);
      pixel.setGreen(255);
      pixel.setBlue(2 * avg - 255);
    } else if (
      avg < 128 &&
      pixel.getY() > sect * 3 &&
      pixel.getY() < sect * 4
    ) {
      pixel.setRed(0);
      pixel.setGreen(avg * 2);
      pixel.setBlue(0);
    } else if (
      avg >= 128 &&
      pixel.getY() > sect * 3 &&
      pixel.getY() < sect * 4
    ) {
      pixel.setRed(2 * avg - 255);
      pixel.setGreen(255);
      pixel.setBlue(2 * avg - 255);
    } else if (
      avg < 128 &&
      pixel.getY() > sect * 4 &&
      pixel.getY() < sect * 5
    ) {
      pixel.setRed(0);
      pixel.setGreen(0);
      pixel.setBlue(avg * 2);
    } else if (
      avg >= 128 &&
      pixel.getY() > sect * 4 &&
      pixel.getY() < sect * 5
    ) {
      pixel.setRed(2 * avg - 255);
      pixel.setGreen(2 * avg - 255);
      pixel.setBlue(255);
    } else if (
      avg < 128 &&
      pixel.getY() > sect * 5 &&
      pixel.getY() < sect * 6
    ) {
      pixel.setRed(0.8 * avg);
      pixel.setGreen(0);
      pixel.setBlue(avg * 2);
    } else if (
      avg >= 128 &&
      pixel.getY() > sect * 5 &&
      pixel.getY() < sect * 6
    ) {
      pixel.setRed(1.2 * avg - 51);
      pixel.setGreen(2 * avg - 255);
      pixel.setBlue(255);
    } else if (avg < 128) {
      pixel.setRed(1.6 * avg);
      pixel.setGreen(0);
      pixel.setBlue(1.6 * avg);
    } else if (avg >= 128) {
      pixel.setRed(0.4 * avg + 153);
      pixel.setGreen(2 * avg - 255);
      pixel.setBlue(0.4 * avg + 153);
    }
  }
  //Get Canvas
  fgCan = document.getElementById("can");
  //Display new image
  fgImage.drawTo(fgCan);
}

function makeRed(){
  var fileinput = document.getElementById("imgfile");
	//Make new SimpleImage from fileinput
	temp = new SimpleImage(fileinput);
  for (var pixel of fgImage.values()){
    var avg = (pixel.getRed() + pixel.getGreen() + pixel.getBlue())/3;
    pixel.setRed(avg*2);
    pixel.setGreen(0);
    pixel.setBlue(0);
  }
  //Get Canvas
  fgCan = document.getElementById("can");
  //Display new image
  fgImage.drawTo(fgCan);
}

function reset(){
  fgImage=temp;
  //Get Canvas
  fgCan = document.getElementById("can");
  //Display new image
  fgImage.drawTo(fgCan);
}