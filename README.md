# Tensorflow-MultiLabel-Classification

Modified retrain.py script from tensorflow to allow multi-label image classification using pretrained Inception net. 

Labels for classification are generated and used based on folder estructure. The images need to be putted on in this way: 

mobile
  |
   - samsung
     xiaomi
     huawey
tablet
  |
   - samsung
     xiaomi
     huawey
tv
  |
   - samsung
     lg
    
This example structure would generate this output_labels.txt
    
mobile
samsung
xiaomi
huawey
tablet
tv
lg

    

The label_image.py has also been slightly modified to write out the resulting class percentages into results.txt.
