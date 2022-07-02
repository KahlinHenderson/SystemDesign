Control Plane: responsible for uploading new content that will eventually be distributed across a CDN. It’s comprised of a CDN Health Checker Service and a Content Uploader Service.

CDN Health Checker Service: periodically performs health checks on a CDN

Content Uploader Service: uploads content to the CDN and stores metadata about the video in data storage.

Metadata includes:

title

description

cdn\_urls

content\_creator

cast\_members

Data Storage: stores video metadata

Data Plane: handles requests for content. It’s comprised of a Playback Service and a Steering Service.

Playback Service: determines the files needed to serve the request

Steering Service: determines optimal URLs for serving content and returns them to the client

Once the client has the URLs it sends a request to the CDN

APIs:

Video Upload

Search Video

Stream Video

