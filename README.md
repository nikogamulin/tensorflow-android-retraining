# tensorflow-android-retraining

TensorFlow version: 0.11.0rc0 [Download and Setup](https://www.tensorflow.org/versions/r0.11/get_started/os_setup.html)

For each object or group of objects create a folder in /images/source.

##Image preparation

The script resizes the source images and stores the processed images to image/processed. If parameter PERFORM_BLUR_ANALYSIS is set to True, the script will skip blurred images (might be helpful if source images were collected as sequence of snapshots).

All processed images are added to log so if the script is interrupted, all images processed so far are not processed again next time the script runs.

##Retraining

After the images have been resized, the model can be retrained by simpy running the scripts and copying generated commands to console.

##Android

To use the retrained model in Android App, simply copy the graph and labels files to assets folder and modify the Android example code in order to match used model (in this case inception v3).

For more info check [TensorFlow Android Camera Demo](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/examples/android)

settings in TensorFlowImageListener.java:
```
private static final int NUM_CLASSES = [number of classes (number of images/processed folders)];
private static final int INPUT_SIZE = 299; //adapted to inception v3
private static final int IMAGE_MEAN = 128; //adapted to inception v3
private static final float IMAGE_STD = 128; //adapted to inception v3
private static final String INPUT_NAME = "Mul:0"; //adapted to inception v3
private static final String OUTPUT_NAME = "final_result:0"; //adapted to parameter in optimized graph

private static final String MODEL_FILE = "file:///android_asset/inception_v3_optimized.pb";
private static final String LABEL_FILE = "file:///android_asset/labels.txt";
```



