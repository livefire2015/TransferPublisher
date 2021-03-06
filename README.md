# TransferPublisher


XCode 11 lets you use the new Combine framework with URLSession by directly creating a URLSessionTask publisher, but not for an download or upload task (which perform better for transferring lots of data, plus background capability)

> _I don't use this package myself anymore. It's just as easy to create KVO based Publisher's for the URLSessionDownload or Upload Task properties directly (or from their Progress property which is also KVO compliant)._ 

Here are three extensions to `URLSession`:
1. `func downloadTaskPublisher(with request: URLRequest) -> AnyPublisher<DownloadOutput, Error>`
2. `func uploadTaskPublisher(with request: URLRequest, data: Data?) -> AnyPublisher<UploadOutput, Error>`
3. `func fileUploadTaskPublisher(with request: URLRequest, fromFile fileURL: URL) -> AnyPublisher<FileUploadOutput, Error>`

The publisher will publish periodically (every 0.1 sec) until finished Output as an enum either of: 
* `downloading`/`uploading` with tuple (bytes received/sent, total bytes expected to send/receive); or 
* `completed` with the downloaded data or upload response body data or URL

The publisher Failure is an `Error`.

Here it is as just a gist: https://gist.github.com/cenkbilgen/d28a1ab12aca6bdf89c3e3c878052ea8

