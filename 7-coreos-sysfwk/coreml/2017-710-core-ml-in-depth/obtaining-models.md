





### Demo Summary

```python
import coremltools
caffe_model = ('flowers.caffemodel','flowers.prototxt')
model = coremltools.converters.caffe.convert(
caffe_model, image_input_names = 'data', class_labels = 'labels.txt')
model.save('FlowerClassifier.mlmodel')
```
