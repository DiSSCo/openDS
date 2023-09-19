# Machine Annotation Service

In this document we will show how you can build a machine annotation service (MAS) which fully integrates with the DiSSCo infrastructure.

#### Disclaimer
The development is currently in piloting phase.
We are testing different service to see if our set-up covers all use cases.
As our data models for the objects are still under development please contact sam.leeflang@naturalis.nl or wouter.addink@naturalis.nl for their latest version.

## Background
To enable large scale data enrichment we use machina annotation services. 
These machine annotation services can provide a wide range of functionalities.
However, the flow for each MAS is the same.
It gets scheduled on a Digital Object (DO), in most cases this will be a Digital Specimen or a Digital Media Object.
The MAS will use some part of the DO to add more information to the object.
This new information always gets published as an annotation on the target object.

Within the DiSSCo core infrastructure we use an event-driven microservices approach.
This means that we try to keep different functionality disconnected and couple the service through queues.
For the MAS this means that for each MAS we will create a dedicated queue

## Technical Implementation
When these steps are followed, DiSSCo will be able to deploy, scale and run your MAS and make it available for all relevant digital objects.

In general, we expect a MAS to consists of three steps:
1. Receive Digital Object
2. Work with the object, this could be anything from calling external APIs to data cleaning
3. Publish Annotations
4. Publish code as container image

This tutorial with help with steps 1 and 3.
Step 2 is up to the provider to implement.

For receiving and publishing data DiSSCo uses Kafka.
Kafka helps with the decoupling as well as the automatically scaling the applications.
The MAS will receive a message on its own queue, will be triggered to consume the message and publishes its results also on a queue.
From there the annotation will be created by the annotation-processing service and becomes available in the infrastructure.

### Receiving the digital object
Receiving the digital object can be done by subscribing to the Kafka queue.
The Kafka queue is created when the MAS is deployed and is specific for the MAS, no other application reads messages from this queue.
The details for the Kafka cluster as well as the Kafka queue name (called topic) is provided to the application through environmental variables.
- KAFKA_CONSUMER_TOPIC
- KAFKA_CONSUMER_GROUP
- KAFKA_CONSUMER_HOST

In the first step we will also setup a Kafka publisher for which we use environmental values:
- KAFKA_PRODUCER_HOST

The consumer and the producer can use different Kafka clusters.
However, in reality it is expected that this will always be the same.

```
import os
import json
from kafka import KafkaConsumer, KafkaProducer

consumer = KafkaConsumer(os.environ.get('KAFKA_CONSUMER_TOPIC'), group_id=os.environ.get('KAFKA_CONSUMER_GROUP'),
                         bootstrap_servers=[os.environ.get('KAFKA_CONSUMER_HOST')],
                         value_deserializer=lambda m: json.loads(m.decode('utf-8')),
                         enable_auto_commit=True)
producer = KafkaProducer(bootstrap_servers=[os.environ.get('KAFKA_PRODUCER_HOST')],
                         value_serializer=lambda m: json.dumps(m).encode('utf-8'))
```
Now that our consumer and producer are defined we can start consuming messages on the queue
```
for msg in consumer:
    json_value = msg.value
    object_data = json_value['data']
```
Here we indicate that for each message of the consumer we would like to retrieve the value of the message (instead of the message headers or other information).
From this value we want to gather the data which contains all relevant data of the digital objects.
For full schema's of the objects please contact DiSSCo's developers.

### Working the object
Now that we have the object data in memory we can start with creating new information about the object.
This could be anything, we could geo-reference against a range of external service by calling their API.
We could also follow a image url (of the Digital Media Object) and ran AI over the image.
Possibilities are endless.
The below example extracts additional metadata about the Digital Media Object, with the use of the library [Pillow] (https://pillow.readthedocs.io/en/stable/).

```
from PIL import Image
from io import BytesIO

img = Image.open(requests.get(image_uri, stream=True).raw)
img_file = BytesIO()
img.save(img_file, img.format, quality='keep')
additional_info = {'exif:PixelXDimension': img.width,
                   'exif:PixelYDimension': img.height,
                   'dcterms:format': img.format.lower(),
                   'dcterms:extent': str(round(img_file.tell() / 1000000, 2)) + 'MB'
                   }
```

### Publishing annotations
Now that we have extracted some additional data about the object we want to publish this data as annotations on the subject.
This means we have to mold the new data in the Annotation object.
The datamodel for the Annotation is currently being developed and will be explained here shortly.
After we create the Annotation object or objects we publish them to the Kafka topic

`producer.send('annotation', annotation)`

The first parameter indicates the topic name it needs to be published to which should be "annotation".
The second parameter is the annotation.
This can always be only one annotation, if a service generates multiple annotations it needs to publish these individually.

### Publish as container image
Now we have all components in place we can package the code into a Docker container with a Docker Image.
An example of a Docker Image can be:
```dockerfile
# set base image (host OS)
FROM python:3.8-alpine

# set the working directory in the container
WORKDIR /code

# Create new user with UID
RUN adduser --disabled-password --gecos '' --system --uid 1001 python && chown -R python /code

# Set user to newly created user
USER 1001

# copy the dependencies file to the working directory
COPY requirements.txt .

# install dependencies
RUN pip install -r requirements.txt

# copy the content of the local src directory to the working directory
COPY main.py .

# command to run on container start
CMD [ "python", "main.py" ]
```
The creates a container image of the code which can then be published to a public image registry.
Let us know if you don't have your own image registry we could look if we can give you access to DiSSCo's image registry.
There are a couple of things to keep in mind when creating the image:
- The container won't have root access when run in the DiSSCo cluster
- The container won't have write access to the underlying file system
- The container will scale based on the amount of messages in the topic so should be stateless
- The container image needs a specific version, latest will not be accepted

## Conclusion
Feel free to reach out to us whenever you have a question or a use case of which you are unsure if it will fit.
For working examples see please check: https://github.com/DiSSCo/demo-enrichment-service-image
We will continuously update and improve this guide
