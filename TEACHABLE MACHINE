
 // var b = p5.board('/dev/cu.usbmodem14301', 'arduino');
//var led1, led2;
  
  
  // Declare a "SerialPort" object
  let serial;
  let latestData = "waiting for data";  // you'll use this to write incoming data to the canvas

// Classifier Variable
  let classifier;
  // Model URL
  let imageModelURL = 'https://teachablemachine.withgoogle.com/models/IYhwSB6P/';
  
  // Video
  let video;
  let flippedVideo;
  // To store the classification
  let label = "";

  // Load the model first
  function preload() {
    classifier = ml5.imageClassifier(imageModelURL + 'model.json');
  }

  function setup() {
    createCanvas(320, 260);
    // Create the video
    video = createCapture(VIDEO);
    video.size(320, 240);
    video.hide();
    
    // Instantiate our SerialPort object
    serial = new p5.SerialPort();
    
    // Get a list the ports available
  // You should have a callback defined to see the results
    serial.list();
    
    // Assuming our Arduino is connected, let's open the connection to it
  // Change this to the name of your arduino's serial port
  serial.open("/dev/tty.usbmodem14301");
    
 //   led1 = b.pin(8, 'LED');
 //   led2 = b.pin(9, 'LED');
    

    flippedVideo = ml5.flipImage(video)
    // Start classifying
    classifyVideo();
  }

  function draw() {
    background(0);
    // Draw the video
    image(flippedVideo, 0, 0);

    
    // Draw the label
    fill(255);
    textSize(16);
    textAlign(CENTER);
    text(label, width / 2, height - 4);
  }

  // Get a prediction for the current video frame
  function classifyVideo() {
    flippedVideo = ml5.flipImage(video)
    classifier.classify(flippedVideo, gotResult);
  }

  // When we get a result
  function gotResult(error, results) {
    // If there is an error
    if (error) {
      console.error(error);
      return;
    }
    // The results are in an array ordered by confidence.
    // console.log(results[0]);
    label = results[0].label;
    
    
    if(label == "Mint"){
      serial.write(1);
    }else if(label == "Oregano"){
      serial.write(2);
    }else{
      serial.write(3);
    }
    // Classifiy again!
    classifyVideo();
  }
 
