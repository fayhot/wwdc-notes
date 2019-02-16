
# [2018 417 Testing Tips & Tricks](https://developer.apple.com/videos/play/wwdc2018/417)



2018-417-testing-tips-tricks


- Brian Croom, XCTest Engineer
- Stuart Montgomery, XCTest Engineer


TOC 


Topic|Speaker|Time|Page
---|---|---|---
Testing network requests | Brian | 155 | p5
[Working with Notifications](2-working-with-notifications.md) | Stuart |  |p78
[Mocking with protocols](3-mocking-with-protocols.md) | Stuart | 1950 | p105
[Test Execution Speed](4-test-execution-speed.md) | Stuart | 2835 | p146

## Testing network requests | Brian | 155 | p5

Pyramid of Tests
Recap

- End-to-end
- Integration
- Unit


Networking Stack

```swift
func loadData(near coord: CLLocationCoordinate2D) {
    let url = URL(string: "/locations?lat=\(coord.latitude)&long=\(coord.longitude)")!
    URLSession.shared.dataTask(with: url) { data, response, error in
        guard let data = data else { self.handleError(error); return }
        do {
            let values = try JSONDecoder().decode([PointOfInterest].self, from: data)
            DispatchQueue.main.async {
                self.tableValues = values
                self.tableView.reloadData()
            }
        } catch {
            self.handleError(error)
        }
    }.resume()
}
```

### Unit Tests


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

Integration Tests

## How to Use URLProtocol


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
        // ...
    }
    override func stopLoading() {
        // ...
    }

}
```


### Tests class

```swift
class APILoaderTests: XCTestCase {
    var loader: APIRequestLoader<PointsOfInterestRequest>!
    override func setUp() {
        let request = PointsOfInterestRequest()
        let configuration = URLSessionConfiguration.ephemeral
        configuration.protocolClasses = [MockURLProtocol.self]
        let urlSession = URLSession(configuration: configuration)
        loader = APIRequestLoader(apiRequest: request, urlSession: urlSession)
    }

    func testLoaderSuccess() {
        let inputCoordinate = CLLocationCoordinate2D(latitude: 37.3293, longitude: -121.8893)
        let mockJSONData = "[{\"name\":\"MyPointOfInterest\"}]".data(using: .utf8)!
        MockURLProtocol.requestHandler = { request in
            XCTAssertEqual(request.url?.query?.contains("lat=37.3293"), true)
            return (HTTPURLResponse(), mockJSONData)
        }

        let expectation = XCTestExpectation(description: "response")
        loader.loadAPIRequest(requestData: inputCoordinate) { pointsOfInterest, error in
        XCTAssertEqual(pointsOfInterest, [PointOfInterest(name: "MyPointOfInterest")])
        expectation.fulfill()
        }
    wait(for: [expectation], timeout: 1)
    }
}
```

