# Thread

1. Thread in Swift
    - 프로그램을 독립적 실행하는 주체, 여기서 프로그램은 하나의 함수
    - 여러개의 함수가 순서적으로 들어가있는 Queue 개념 도임
    - Serial : 한개의 스레드가 Queue의 함수들을 순차적으로 실행
    - Concurrent : 여러개의 스레드가 Queue의 함수들을 동시에 실행 (또는 병렬큐)
    
    ![스크린샷 2023-04-19 21.02.54.png](Thread%20d8826e5b872548ee888af65e8e407d42/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-19_21.02.54.png)
    
2. Queue
    
    ![스크린샷 2023-04-19 21.03.23.png](Thread%20d8826e5b872548ee888af65e8e407d42/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-19_21.03.23.png)
    
3. async, sync test
    
    ![스크린샷 2023-04-19 21.04.20.png](Thread%20d8826e5b872548ee888af65e8e407d42/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-19_21.04.20.png)
    
4. DispatchQueue & OperationQueue
    
    ![스크린샷 2023-04-19 21.05.10.png](Thread%20d8826e5b872548ee888af65e8e407d42/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-19_21.05.10.png)
    

### code

```swift
//
//  MapViewController.swift
//  ch06-tabBarController
//
//  Created by 유영재 on 2023/04/10.
//

import UIKit
import MapKit

class MapViewController: UIViewController {

    @IBOutlet weak var mapView: MKMapView!
    let baseURLString = "https://api.openweathermap.org/data/2.5/weather"
    let apiKey = "f0520dc1a85e5d0432ee0adbaedc0f1b"

    override func viewDidLoad() {
        super.viewDidLoad()
    }
    override func viewWillAppear(_ animated: Bool) {

        let parent = self.parent as! UITabBarController
        let cityViewController = parent.viewControllers![0] as! CityViewController
        var (city, longitute, latitute) = cityViewController.getCurrentLonLat()
        getWeatherData(cityName: city)

//        updateMap(title: city, longitute: longitute, latitute: latitute)
    }
    override func viewWillDisappear(_ animated: Bool) {
        mapView.removeAnnotations(mapView.annotations)
    }
    @IBAction func sgcValueChanged(_ sender: UISegmentedControl) {
        switch sender.selectedSegmentIndex {
            case 0:
                mapView.mapType = .standard
            case 1:
                mapView.mapType = .hybrid
            case 2:
                mapView.mapType = .satellite
            default:
                break
            }
    }
}

extension MapViewController{

    func updateMap(title: String, longitute: Double?, latitute: Double?){

        let span = MKCoordinateSpan(latitudeDelta: 1, longitudeDelta: 1)
        var center = mapView.centerCoordinate // 일단 기존의 중심을 저장
        if let longitute = longitute, let latitute = latitute{
            center = CLLocationCoordinate2D(latitude: latitute, longitude: longitute) // 새로운 중심 설정
        }
        let region = MKCoordinateRegion(center: center, span: span)
        mapView.setRegion(region, animated: true) // 주어진 영역으로 지도를 설정
        
        let annotation = MKPointAnnotation()
        annotation.coordinate = center    // 센터에 annotation을 설치
        annotation.title = title
        mapView.addAnnotation(annotation)
    }
}
extension MapViewController {
    func extractWeatherData(jsonData: Data) -> (Double?, Double?, Double?){
        
        let json = try! JSONSerialization.jsonObject(with: jsonData, options: []) as! [String: Any]

        // {"cod":"404","message":"city not found"} for unknown city
        if let code = json["cod"] {
            if code is String, code as! String == "404"{
                return (nil, nil, nil)
            }
        }
        
        let latitude = (json["coord"] as! [String: Double])["lat"]
        let longitude = (json["coord"] as! [String: Double])["lon"]
        
        guard var temperature = (json["main"] as! [String: Double])["temp"] else{
            return (nil, longitude, latitude)
        }
        temperature = temperature - 273.0
        return (temperature, longitude, latitude)
    }
}

extension MapViewController {
    func getWeatherData(cityName city: String){
        
        var urlStr = baseURLString+"?"+"q="+city+"&"+"appid="+apiKey
        urlStr = urlStr.addingPercentEncoding(withAllowedCharacters: .urlQueryAllowed)!
        
        let session = URLSession(configuration: .default)
        let url = URL(string: urlStr)
        let request = URLRequest(url: url!)
        
        let dataTask = session.dataTask(with: request){
            (data, response, error) in
            guard let jsonData = data else{ print(error!); return }
            if let jsonStr = String(data:jsonData, encoding: .utf8){
                print(jsonStr)
            }

            let (temperature, longitute, latitute) = self.extractWeatherData(jsonData: jsonData)
            var title = city
            if let temperature = temperature{
                title += String.init(format: ": %.2f℃", temperature)
            }
            DispatchQueue.main.async {
                self.updateMap(title: title, longitute: longitute, latitute: latitute)
                print(1)
            }
            print(2)
        }
        dataTask.resume()
    }
}
```

```swift
//
//  ChatViewController.swift
//  ch07-유영재-webService
//
//  Created by 유영재 on 2023/04/19.
//

import UIKit

class ChatViewController: UIViewController {

    @IBOutlet weak var queryTextView: UITextView!
    @IBOutlet weak var queryTextField: UITextField!
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // Do any additional setup after loading the view.
    }
    
    override func viewWillAppear(_ animated: Bool) {
        let tabBarController = self.parent as! UITabBarController
        let cityViewController = tabBarController.viewControllers![0] as! CityViewController
        let (city, _, _) = cityViewController.getCurrentLonLat()
        
        queryTextField.text = city
    }

    @IBAction func sendQuery(_ sender: Any) {
        let apiKey = "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"
        let apiEndpoint = "https://api.openai.com/v1/engines/curie/completions"
        
        let parameters: [String: Any] = [
            "prompt" : "\(queryTextField.text!)",
            "temperature" : 0.5,
            "max_tokens" : 500
        ]
        
        guard let url = URL(string: apiEndpoint) else {
            print("Invaild URL")
            return
        }
        
        var request = URLRequest(url: url)
        request.setValue("Bearer \(apiKey)", forHTTPHeaderField: "Authorization")
        request.setValue("application/json", forHTTPHeaderField: "Content-Type")
        request.httpMethod = "POST"
        let httpBody = try? JSONSerialization.data(withJSONObject: parameters)
        request.httpBody = httpBody
        
        let task = URLSession.shared.dataTask(with: request) {
            (data, response, error) in
            guard let jsonData = data else { print(error!); return }
            if let jsonStr = String(data: jsonData, encoding: .utf8) {
                print(jsonStr)
            }
            
            let json = try! JSONSerialization.jsonObject(with: jsonData, options: []) as! [String: Any]
            guard let choices = json["choices"] as? [[String: Any]], let text = choices.first?["text"] as? String else {
                print("Invalid response data")
                return
            }
            DispatchQueue.main.async {
                self.queryTextView.text = text
            }
        }
        task.resume()
        
    }

}
```