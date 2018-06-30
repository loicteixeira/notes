# Demystifying Machine Learning on AWS

## Haven't I Heard All This Before? Why now?

- Machine Learning needs a lot of good clean data which is only available now
- Algorithms, something something..
- Compute power is now available in the cloud (low barrier entry) and can be turned off (cost saving)

## Stack

From higher level to lower level:

1. Application services
   - `Rekognition`, `Transcribe`, `Polly`, `Translate`, `Comprehend`, `Lex`
2. Platform services
   - Amazon Machine Learning
   - Mechanical Turk: Marketplace to get access to human skills for supervised algorithms
   - Spark & EMR
   - SageMaker: End-to-End, fully managed Machine Learning platform
3. Framework and Infrastructures
   - AWS Deep Learning AMI: TensorFlow, Keras, Cognitive Toolkit, etc.

## Carsales Cyclops 2.0

Custom built image recognition engine which can classify a car with an accuracy of 98%.

Common Object Recognition is easy, car recognisation is hard (also because it has to work with low resolution source images)

They used Tensorflow with a Convolution Neural Network, Inception v4 (?) and Transfer Learning.

Process was hard. A lot of time spend on infra and setup. Would be better to spend this time on developing the model.

## SageMaker

- End-to-End Machine learning platform
- Zero setup
- Flexible Model Training
- Pay by the second

Machine Learning in 3 steps:

1. Clean, format, prepare and transform data
2. Train and evaluate model without the need to worry about setup, management of instances (scaling up and down to accommodate growth or saves cost)
3. Integrate with production with deployment to autoscaling group

SageMaker also:

- Offers managed notebooks. It's a wonderful tool for exploration but are normally hard to share.
- Can run simultaneous models to compare them

Old process was 6-18 months to go from an idea to a solution. With SageMaker, it can be done in days.
