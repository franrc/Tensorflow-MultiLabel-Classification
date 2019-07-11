# Tensorflow-MultiLabel-Classification

Modified retrain.py script from tensorflow to allow multi-label image classification using pretrained Inception net. 

It works on tensorflow 1.1.0 and above versions.

Labels for classification are generated and used based on folder estructure. The images need to be putted on in this way: 

* mobile
  * samsung
    * image_mobile_samsung
    * image_mobile_samsung
    * ....
  * xiaomi
    * image_mobile_xiaomi
    * image_mobile_xiaomi
    * ....
  * huawey
    * image_mobile_huawey
    * image_mobile_huawey
    * ....
* tablet
  * samsung
    * image_tablet_samsung
    * image_tablet_samsung
    * ....
  * xiaomi
    * image_tablet_xiaomi
    * image_tablet_xiami
    * ....
  * huawey
    * image_tablet_huawey
    * image_tablet_huawey
    * ....
* tv
  * samsung
    * image_tv_samsung
    * image_tv_samsung
    * ....
  * lg
    * image_tv_lg
    * image_tv_lg
    * ....
    
This example structure would generate this output_labels.txt
 
```
mobile  
samsung  
xiaomi  
huawey  
tablet  
tv  
lg  
```
and will categorize the images onto each directory of the structure tree, for example 'image_tablet_samsung' will be trained as tablet and samsung categories.

All the training images must be in JPG format.  

Several changes has been based on https://github.com/BartyzalRadek/Multi-label-Inception-net retrain modifications.

# How to use

Create a folder called 'images' and generate inside the desired folder estructure and put images inside on it.

Once all images are on it's own folder, you can train your model with this sentence (feel free playing with arguments) : 

**python retrain.py --image_dir images/ --learning_rate=0.0005 --testing_percentage=15 --validation_percentage=15 --train_batch_size=32 --validation_batch_size=-1 --flip_left_right True --random_scale=30 --random_brightness=30 --eval_step_interval=100 --how_many_training_steps=1000 --architecture mobilenet_1.0_128_quantized**
  
  
When the model has been trained, you can call this for check the traning: 
  
**python label_image.py --graph=tmp/output_graph.pb --labels=tmp/output_labels.txt --input_layer=Placeholder --output_layer=final_result --input_mean=128 --input_std=128 --input_width=224 --input_height=224 --image=images/.....**
  
This will return totally independent results for each label

```
tablet 99.35184121131897%
samsung 98.91063570976257%
mobile 3.713225945830345%
xiaomi 2.3000916466116905%
tv 1.0949322022497654%
```
