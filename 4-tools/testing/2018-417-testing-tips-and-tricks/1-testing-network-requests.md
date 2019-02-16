
## [Testing network requests](1-testing-network-requests.md) | 155 | p5


```swift
struct PointsOfInterestRequest {
    func makeRequest(from coordinate: CLLocationCoordinate2D) throws -> URLRequest {
        guard CLLocationCoordinate2DIsValid(coordinate) else {
            throw RequestError.invalidCoordinate
        }
        var components = URLComponents(string: "https://example.com/locations")!
        components.queryItems = [
            URLQueryItem(name: "lat", value: "\(coordinate.latitude)"),
            URLQueryItem(name: "long", value: "\(coordinate.longitude)")
        ]
        return URLRequest(url: components.url!)
    }

    func parseResponse(data: Data) throws -> [PointOfInterest] {
        return try JSONDecoder().decode([PointOfInterest].self, from: data)
    }
}
```

Unit Tests

```swift
protocol APIRequest {
    associatedtype RequestDataType
    associatedtype ResponseDataType
    
    func makeRequest(from data: RequestDataType) throws -> URLRequest
    func parseResponse(data: Data) throws -> ResponseDataType
}
class APIRequestLoader<T: APIRequest> {
    let apiRequest: T
    let urlSession: URLSession

    init(apiRequest: T, urlSession: URLSession = .shared) {
        self.apiRequest = apiRequest
        self.urlSession = urlSession
    }
}
```

xxx

```swift
class APIRequestLoader<T: APIRequest> {

    func loadAPIRequest(requestData: T.RequestDataType,
        completionHandler: @escaping (T.ResponseDataType?, Error?) -> Void) {

        do {
            let urlRequest = try apiRequest.makeRequest(from: requestData)
            urlSession.dataTask(with: urlRequest) { data, response, error in
                guard let data = data else { return completionHandler(nil, error) }
                do {
                    let parsedResponse = try self.apiRequest.parseResponse(data: data)
                    completionHandler(parsedResponse, nil)
                } catch {
                    completionHandler(nil, error)
                }
            }.resume()
        } catch { return completionHandler(nil, error) }
    }
}
```

Integration Tests

### How to Use URLProtocol

```swift
class MockURLProtocol: URLProtocol {
    override class func canInit(with request: URLRequest) -> Bool {
        return true
    }
    override class func canonicalRequest(for request: URLRequest) -> URLRequest {
        return request
    }

    static var requestHandler: ((URLRequest) throws -> (HTTPURLResponse, Data))?
    override func startLoading() {
        guard let handler = MockURLProtocol.requestHandler else {
            XCTFail("Received unexpected request with no handler set")
            return
        }
        do {
            let (response, data) = try handler(request)
            client?.urlProtocol(self, didReceive: response, cacheStoragePolicy: .notAllowed)
            client?.urlProtocol(self, didLoad: data)
            client?.urlProtocolDidFinishLoading(self)
        catch {
            client?.urlProtocol(self, didFailWithError: error)
        }


    }

```

End-to-End Tests | | p71


