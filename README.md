
Intro
-----

This Docker container will send free disk space metric to AWS CloudWatch.

How to run it ?
----------------

Simple add crontab entry and script will figure out rest of details.

    sudo crontab -e ->
    */2 * * * * docker run -v /:/host_root:ro --rm --log-driver=syslog ogavrisevs/ec2-diskfreespace-to-cloudwatch:latest --verbose

You need to share host disk (read only) with container.

    -v /:/host_root:ro

Any additional permissions ?
-----------------------------

Yes you need to grant additional policies to push AWS CloudWatch metrics
If you are running docker on AWS ECS add following policies to your instance profile role:

    cloudwatch:PutMetricData
    cloudwatch:GetMetricStatistics
    cloudwatch:ListMetrics
    ec2:DescribeTags  

What is footprint ?
---------------------

Not much alpine + perl + scripts == ~ 64 MB

    REPOSITORY              TAG     IMAGE ID      CREATED       SIZE
    ogavrisevs/ec2-disk2cw  latest  b950474d5f1b  2 hours ago   64.62 MB

Any copyrights ?
----------------

  Container are based on AWS [CloudWatchMonitoringScripts](
http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/mon-scripts.html)
