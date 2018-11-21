---
layout: post
title: Using dotnet to read gzip streams from s3
image: /assets/img/gzip-elastic/cover.png
readtime: 3 minutes
tags: gzip, dotnet, csharp
---

I came across a bug recently when reading gzip streams.

I was working on a project where the logs from an ALB were being stored in s3. Periodically, my code would
call s3 and read the streams and process them into elasticsearch. What I found was that the official dotnet 
gzip library would only read about the first 6 or 7 lines.


```
var s3Object = _s3Client.GetObjectAsync(s3Notification.S3.Bucket.Name, s3Notification.S3.Object.Key).GetAwaiter().GetResult();
using (var decompressionStream = new GZipStream(s3Object.ResponseStream, CompressionMode.Decompress))
using (var decompressedStream = new MemoryStream())
var request = new GetObjectRequest
{
    decompressionStream.CopyTo(decompressedStream);
    decompressionStream.Flush();
    decompressedStream.Flush();
    decompressedStream.Position = 0;
    string line;
    var lines = new List<String>();
    using (var sr = new StreamReader(decompressedStream))
        while ((line = sr.ReadLine()) != null)
            lines.Add(line);
};
```

<amp-img src="/assets/img/gzip-elastic/gzip.svg"
  width="586"
  height="586"
  layout="responsive">
</amp-img>


It had me head scratching for a long time, and it turns out there's a bug in the dotnet library for decompression.
It seems like there's a lot of people out there struggling with this.

What I did was to use the SharpZipLib nuget library instead, which worked a charm

```
using (var response = _s3Client.GetObjectStreamAsync(s3Object.BucketName, s3Object.Key, null).GetAwaiter().GetResult())
{
    byte[] dataBuffer = new byte[4096];
    using (var gzipStream = new GZipInputStream(response))
    using (var decodedStream = new MemoryStream())
    {
        StreamUtils.Copy(gzipStream, decodedStream, dataBuffer);
        gzipStream.Flush();
        decodedStream.Flush();
        decodedStream.Position = 0;
        using (var reader = new StreamReader(decodedStream))
        {
            var lines = new List<string>();
            while (!reader.EndOfStream)
                lines.Add(reader.ReadLineAsync().GetAwaiter().GetResult());

            var data = lines.Select(x => _parser.Parse(x));
            _elasticSearchAdapter.CreateElasticRecord(data);
            _s3Client.DeleteObjectAsync(s3Object.BucketName, s3Object.Key).GetAwaiter().GetResult();
        }
    }
}
```

I will blog about the solution I created for this in a later post, something I was trying out. 
In the past I've used logstash to process logs into elastic, but I wanted somethat that I could run
serverless, and only process when I wanted, which is why I went down this route.

<amp-img src="/assets/img/gzip-elastic/elastic.jpg"
  width="500"
  height="327"
  layout="responsive">
</amp-img>
