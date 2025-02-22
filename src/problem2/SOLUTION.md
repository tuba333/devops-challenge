Provide your solution here:
We are going to need some of the component :
- Frontend 
- Backend
- Loadbalancer
- Database 
- Datastreaming  
- Caching layer
- Worker node for pubsub datastream
- Certification
Since the limit is Cloudprovider Amazon Web Services (AWS) :
- I'll choosing Single Page Application VueJS for frontend service , hosted on S3 bucket with ACL public rule , request rated with WAF + cloudfront, and route DNS from route53.
- For backend , it will be expressJS. Since nodeJS can only handle single thread , this will need to be horizontal scaled with elasticbeanstalk based on cpu consumtion(>=50%) with region availability to achieve p99 response time of <100ms.
- For loadbalancing , I recommend using AWS  Elastic Load Balancer , pointed backend api directly to this ,request rated with WAF , point to Elastic Beanstalk.
- For database , I'll using noSQL database DocumentDB for optimize cost and query effectiveness , it's should be on 3 replicaset nodes minimum for high availability with on-demand backup readiness. The alternative would be DynamoDB , which is more expensive when you can't pay in hour.
- Datastreaming allows you to ingest, process, and analyze high volumes of datas , Kinesis would be a good starting point for cost effectiveness but as our application grow , we need planning to move on with MSK.
- Caching in AWS is painless with ElastiCache Redis, with AWS handling maintenance, patching , security , backup,... The alternative would be memchache (which is older version of redis).
- Worker node should be in the same language with api , for handling datastreaming , emitting socket , centralize control from this node. As the workload scales , we are going to need horizontal scale this consumers as well.
- With AWS resouce you can only use certification have Amazon Issued. You can request one needed with Certificate Manager.
- The overview diagram will be in the png located on the same folder as this solution.