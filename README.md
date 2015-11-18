# facebook-agent
# A facebook client for Flume to extract public group posts periodically.
# 1. The client uses the searchKeyword to search groups. Group posts will be extracted from open groups
# 2. You can skip a group by configuring stopWords. If the group's name containes a stopWord it will be skipped
# 3. The extracted data saved in JSON. 

#Config file example:
FacebookAgent.sources=Facebook
FacebookAgent.sinks=sink1
FacebookAgent.channels=FileChannel

FacebookAgent.sources.Facebook.type=com.leadgen.FacebookSource
FacebookAgent.sources.Facebook.appSecret=<YOUR_APP_SECRET>
FacebookAgent.sources.Facebook.accessToken=<YOUR_ACCES_TOKEN>
FacebookAgent.sources.Facebook.hoursFromNow=12 //sinceDate = now - hoursFromNow
FacebookAgent.sources.Facebook.searchKeywords=marketing
FacebookAgent.sources.Facebook.stopWords="indian,andaman,nicobar"
FacebookAgent.sources.Facebook.channels=FileChannel
FacebookAgent.sources.Facebook.maxBatchSize=5000
FacebookAgent.sources.Facebook.maxBatchDurationMillis=100000

FacebookAgent.sinks.sink1.type = hdfs  
FacebookAgent.sinks.sink1.hdfs.path = hdfs://ip:9000/user/ubuntu/facebook_data/
FacebookAgent.sinks.sink1.hdfs.fileType = DataStream
FacebookAgent.sinks.sink1.hdfs.writeFormat = Text
FacebookAgent.sinks.sink1.hdfs.batchSize = 2000000
FacebookAgent.sinks.sink1.hdfs.rollSize = 0
FacebookAgent.sinks.sink1.hdfs.rollCount = 2000000
FacebookAgent.sinks.sink1.channel = FileChannel

FacebookAgent.channels.FileChannel.type = file
FacebookAgent.channels.FileChannel.checkpointDir=/var/log/flume/checkpoint/
FacebookAgent.channels.FileChannel.dataDirs=/var/log/flume/data/

#Extracted data example
[
 {
      "from": {
        "name": "Venchito Jun",
        "id": "876269622390874",
        "link": "https://www.facebook.com/app_scoped_user_id/876269622390874/",
        "picture_medium": {
          "data": {
            "height": 160,
            "is_silhouette": false,
            "url": "https://scontent.xx.fbcdn.net/hprofile-xlp1/v/t1.0-1/p160x160/11953260_1068652793152555_5253711052999205322_n.jpg?oh=46447f675a56eb6fffc88de10566d8b6&oe=56ADBA0C",
            "width": 160
          }
        }
      },
      "message": "We are a startup company - SharpRocket! We are currently looking for 4 Marketing and Research Assistants. Kindly send your resume to venchitotampon@gmail.com. Note: 3 positions available",
      "updated_time": "2015-11-18T17:11:11+0000",
      "id": "277534272382470_661781237291103"
    }
]
