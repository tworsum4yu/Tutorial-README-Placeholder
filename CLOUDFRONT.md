# Cloudfront Details

***FYI:*** *Please remove the '' around the '>' in the final steps of the commands. Doesn't display properly if I don't include it. Also had to convert these from powershell to bash so I am not sure if they run correctly.*

# Commands used

> aws cloudwatch get-metric-statistics \
>  --namespace AWS/S3 \
>  --metric-name AllRequests \
>  --dimensions Name=BucketName,Value=mthree-peregrine-s3-1 Name=FilterId,Value=entireBucket \
>  --start-time "$(date -u -d '7 days ago' +%Y-%m-%dT%H:%M:%SZ)" \
>  --end-time "$(date -u +%Y-%m-%dT%H:%M:%SZ)" \
>  --period 420 \
>  --statistics Sum \
>  --output json \
>  '>' metrics.json                             

Above command gets all requests to the s3 bucket over the last week and sums them together by day. The results are outputted to a metrics.json file to be used else where. Will show later.

> aws cloudwatch get-metric-data \
>  --start-time "$(date -u -d '7 days ago' +%Y-%m-%dT%H:%M:%SZ)" \
>  --end-time "$(date -u +%Y-%m-%dT%H:%M:%SZ)" \
>  --region us-east-1 \
>  --metric-data-queries file://metrics_pull_requests.json \
>  '>' metrics_requests.json                              
                       
Above does the same thing as the previous one, but instead of just getting the AllRequest metrics, it has the ability to get multiple metrics at once, based on the json file provided. Image of the json file 'metrics_pull_requests.json' given below for reference.

![Example of json import file structure](./assets/Cloudfront1.png) <br>

These are the only commands I have used to pull the metrics. I just played around with those to understand what is happening.

# Displaying the metrics

To display the metrics I got claude to spin up a quick static site that accepts the json files generated from the commands and displays it nicely on a page. See reference below for example of what it looks like.

![Cloudfront display site](./assets/Cloudfront2.png) <br>

The site should be able to accept any json file produced, using the two commands anyway. Can provide the site if you want to try anything out 👍.


