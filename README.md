# tesing
tesing repo

gst-launch-1.0 ximagesrc use-damage=0 ! video/x-raw,framerate=30/1 ! videoconvert ! videoscale ! video/x-raw,width=1280,height=720 ! queue ! videoconvert ! x264enc bitrate=1000 speed-preset=superfast tune=zerolatency ! rtph264pay config-interval=1 pt=96 ! udpsink host=239.0.0.1 port=5000  
// mytheme.script
theme.imageDir = "ImageDir";
theme.frameCount = 100; // Change this to the number of frames you have
theme.framePrefix = "frame_";
theme.frameSuffix = ".png";
theme.frameRate = 30; // Frames per second

for (var i = 0; i < theme.frameCount; i++) {
    theme.frames[i] = Image(theme.imageDir + theme.framePrefix + i.toString().padStart(3, '0') + theme.frameSuffix);
}

// Main animation loop
function updateFrame() {
    var time = Time();
    var frame = Math.floor(time * theme.frameRate) % theme.frameCount;
    theme.imageSprite.SetImage(theme.frames[frame]);
}

// Initialize the animation
theme.imageSprite = Sprite();
theme.imageSprite.SetImage(theme.frames[0]);
theme.imageSprite.SetPosition("center", 0.5, 0.5);
theme.imageSprite.SetScale(1, 1);
theme.imageSprite.Show();

Plymouth.Play(updateFrame);

