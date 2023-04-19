# ProgrammingView

1. LayoutGuide
    - 오토레이아웃을 위한 사각형 영역
    - 10개의 앵커 → 8개는 좌표, 2개는 크기
        
        ![스크린샷 2023-04-19 19.25.20.png](ProgrammingView%208b913ba461824d0f98f286fe4eef90ca/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-19_19.25.20.png)
        
2. AutoResizing
    - 초기 iOS에서 도입한 개념. 그러나 다양성의 한계를 느끼고 AutoLayout이 추가됨
    - Interface Builder에서 컨트롤을 놓으면 자동으로 AutoLayout만 적용됨
    - Programming에서는 AutoResizing이 기본적으로 동작하도록 설정되어있기 때문에 `translatesAutoresizingMaskIntoConstraints=false`
3. AutoLayout
    1. view.safeAreaLayoutGuide
        
        ```swift
        class ConversionViewController : UIViewController { 
        	override func viewDidLoad() {
        		super.viewDidLoad()
        		... 
        		view.addSubview(helloLabel)
        		helloLabel.translatesAutoresizingMaskIntoConstraints = false
        		helloLabel.leadingAnchor.constraint(equalTo: view.safeAreaLayoutGuide.leadingAnchor, constant: 20).isActive = true
        		helloLabel.trailingAnchor.constraint(equalTo: view.safeAreaLayoutGuide.trailingAnchor, constant: -20).isActive = true
        		helloLabel.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor, constant: 100).isActive = true
        	} 
        }
        ```
        
    2. 코드 단순화 `NSLayoutConstraints.activate`
        
        ```swift
        class ConversionViewController : UIViewController {
        	override func viewDidLoad() {
        	super.viewDidLoad()
        	...
        	view.addSubview(helloLabel) helloLabel.translatesAutoresizingMaskIntoConstraints = false
        	NSLayoutConstraint.activate([
        	helloLabel.leadingAnchor.constraint(equalTo: view.safeAreaLayoutGuide.leadingAnchor,
        	constant: 20),
        	helloLabel.trailingAnchor.constraint(equalTo: view.safeAreaLayoutGuide.trailingAnchor,
        	constant: -20),
        	helloLabel.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor, constant: 100)
        		]); 
        ```
        
    3. 두개의 컨트롤 
        1. UILabel(name),UITextField + Hugging Priority 적용
            
            ```swift
            override func viewDidLoad() { 
            	super.viewDidLoad()
            	let nameLabel = UILabel(frame: CGRect(x: 0, y: 0, width: 0, height: 0)) nameLabel.text = "Name"
            	nameLabel.backgroundColor = UIColor.green
            	nameLabel.font = UIFont.systemFont(ofSize: 30, weight: .bold) nameLabel.textAlignment = .center
            	let nameTextField = UITextField(frame: CGRect(x: 0, y: 0, width: 0, height: 0)) nameTextField.backgroundColor = UIColor.brown
            	nameTextField.font = UIFont.systemFont(ofSize: 30, weight: .bold) nameTextField.textAlignment = .left
            	view.addSubview(nameLabel)
            	view.addSubview(nameTextField) 
            	nameLabel.translatesAutoresizingMaskIntoConstraints = false 
            	nameTextField.translatesAutoresizingMaskIntoConstraints = false
            
            	NSLayoutConstraint.activate([
            		nameLabel.leadingAnchor.constraint(equalTo: view.safeAreaLayoutGuide.leadingAnchor, constant: 20),
            		nameLabel.trailingAnchor.constraint(equalTo: nameTextField.leadingAnchor, constant: -10),
            		nameLabel.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor, constant: 100),
            		nameTextField.trailingAnchor.constraint(equalTo: view.safeAreaLayoutGuide.trailingAnchor, constant: -20),
            		nameTextField.centerYAnchor.constraint(equalTo: nameLabel.centerYAnchor) 
            	])
            
            	nameLabel.setContentHuggingPriority(.defaultHigh, for: .horizontal)
            	nameTextField.setContentHuggingPriority(defaultLow, for: .horizontal)
            }
            ```
            
        2. setContentCompressionResistance 적용
            
            ```swift
            override func viewDidLoad() { 
            	super.viewDidLoad()
            	...
            	nameLabel.setContentCompressionResistancePriority(.defaultLow, for: .horizontal) 
            	nameTextField.setContentCompressionResistancePriority(.defaultHigh, for: .horizontal)
            	nameLabel.widthAnchor.constraint(greaterThanOrEqualToConstant: 20).isActive = true
            }
            ```
            
4. Action
    1. UIControl.addTarget
        - 특정 이벤트가 발생하면 target에 있는 Selector 함수를 실행하라
        - Selector 함수 주소로 `#selector(func)` 이렇게 줘야 함
        - 함수는 `@objc` 키워드 줘야 함
        
        ```swift
        class ViewController: UIViewController {
        override func viewDidLoad() { 
        	super.viewDidLoad()
        	... // 앞의 코드
        	nameLabel.widthAnchor.constraint(greaterThanOrEqualToConstant: 20).isActive = true
        	// editingDidEnd 액션을 추가
        	nameTextField.addTarget(self, action: #selector(editingDidEnd), for: .editingDidEnd)
        	// editingDidEnd이 끝났다는 것을 UITextField에 알리기 위해
        	let tapGesture = UITapGestureRecognizer(target: self, action: #selector(dismissKeyboard)) 
        	view.addGestureRecognizer(tapGesture)
        }
        	@objc func dismissKeyboard(sender: UITapGestureRecognizer){
        		view.endEditing(true) // view에 여러개의 UITextField가 있는 경우, 모두에 대하여 resignFirstResponder호출 
        	}
        	@objc func editingDidEnd(sender: UITextField){
        		if let text = sender.text, let fahrenheitValue = Double(text){
        			sender.text = String.init(format: "%2f", (5.0/9.0)*(fahrenheitValue - 32.0)) 
        		}
        	} 
        }
        ```
        
5. Controlls Connect
    
    ![스크린샷 2023-04-19 19.44.33.png](ProgrammingView%208b913ba461824d0f98f286fe4eef90ca/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-19_19.44.33.png)
    
    ```swift
    extension ConversionViewController{ 
    	override func viewDidLoad() {
    		super.viewDidLoad()
    		let isLabel = createLabel("is", fontSize: 36)
    		isLabel.translatesAutoresizingMaskIntoConstraints = false 
    		isLabel.centerXAnchor.constraint(equalTo: view.safeAreaLayoutGuide.centerXAnchor).isActive = true
    		isLabel.centerYAnchor.constraint(equalTo: view.safeAreaLayoutGuide.centerYAnchor).isActive = true
    		fahrenheitTextField = createTextField(placeHolder: "VALUE")
    		fdegreeLabel = createLabel("degrees Fahrenheit", fontSize: 36)
    		celsiusLabel = createLabel("degrees Celsius", fontSize: 36)
    		connectVertically(views: fahrenheitTextField, fdegreeLabel, isLabel, celsiusLabel, cdegreeLabel, spacing: -10)
        connectHorizontally(views: fahrenheitTextField, fdegreeLabel, isLabel, celsiusLabel, cdegreeLabel)
    	}
    }
    ```
    

### 전체 code

```swift
//
//  ViewController.swift
//  ch05-programmingView
//
//  Created by 유영재 on 2023/04/03.
//

import UIKit

class ConversionViewController: UIViewController {
    
    var nameLabel: UILabel!
    var nameTextField: UITextField!
    var fahrenheitTextField: UITextField!
    var celsiusLabel: UILabel!
    var isLabel, fdegreeLabel, cdegreeLabel: UILabel!
    var segmentedControl: UISegmentedControl!

    var myDelegate: MyDelegate!        // 디폴트가 strong이다.

    override func viewDidLoad() {
        super.viewDidLoad()
        super.viewDidLoad()
        
        fahrenheitTextField?.delegate = self

        isLabel = createLabel("is", fontSize: 36)
        isLabel.translatesAutoresizingMaskIntoConstraints = false
        isLabel.centerXAnchor.constraint(equalTo: view.safeAreaLayoutGuide.centerXAnchor).isActive = true
        isLabel.centerYAnchor.constraint(equalTo: view.safeAreaLayoutGuide.centerYAnchor).isActive = true
        
        fahrenheitTextField = createTextField(placeHolder: "VALUE")
        fdegreeLabel = createLabel("degrees Fahrenheit", fontSize: 36)
        celsiusLabel = createLabel("???", fontSize: 70)
        cdegreeLabel = createLabel("degrees Celsius", fontSize: 36)
        
        fahrenheitTextField.backgroundColor = UIColor.red
        fdegreeLabel.backgroundColor = UIColor.orange
        celsiusLabel.backgroundColor = UIColor.yellow
        cdegreeLabel.backgroundColor = UIColor.green
        isLabel.backgroundColor = UIColor.lightGray
        
        connectVertically(views: fahrenheitTextField, fdegreeLabel, isLabel, celsiusLabel, cdegreeLabel, spacing: -10)
        connectHorizontally(views: fahrenheitTextField, fdegreeLabel, isLabel, celsiusLabel, cdegreeLabel)
        
        fahrenheitTextField.addTarget(self, action: #selector(fahrenheitEditingChanged), for: .editingChanged)
        let tap = UITapGestureRecognizer(target: self, action: #selector(dismissKeyboard))
                view.addGestureRecognizer(tap)
        
        myDelegate = MyDelegate()    // 일단 strong변수로 참조한다. 그래서 레퍼런스 카운트를 1로 만든다.
        fahrenheitTextField.delegate = myDelegate
        
        addSegmentedControl() // 맨마지막에

    }
}

class MyDelegate: NSObject, UITextFieldDelegate{
    func textField(_ textField: UITextField, shouldChangeCharactersIn range: NSRange, replacementString string: String) -> Bool {
        let existing = textField.text?.firstIndex(of: ".")
        let comming = string.firstIndex(of: ".")
        
        if let _ = existing, let _ = comming{
            return false
        }
        return true
    }
}

extension ConversionViewController {
    
    func createTextField(placeHolder: String) -> UITextField{
        let textField = UITextField(frame: CGRect())
        textField.textAlignment = .center
        textField.placeholder = placeHolder
        textField.font = UIFont(name: textField.font!.fontName, size: 70)
        textField.keyboardType = .decimalPad
        view.addSubview(textField)
        textField.translatesAutoresizingMaskIntoConstraints = false
        return textField
    }
    
    func createLabel(_ text: String, fontSize: CGFloat) -> UILabel{
        let label = UILabel(frame: CGRect())
        label.text = text
        label.textColor = UIColor(red: CGFloat(0xe1)/CGFloat(256), green: CGFloat(0x58)/CGFloat(256), blue: CGFloat(0x29)/CGFloat(256), alpha: CGFloat(1))
        label.textAlignment = .center
        label.font = UIFont(name: label.font!.fontName, size: fontSize)
        view.addSubview(label)
        label.translatesAutoresizingMaskIntoConstraints = false
        return label
    }
    
    func connectVertically(views: UIView..., spacing: CGFloat){
            for i in 0..<views.count - 1{
                views[i].bottomAnchor.constraint(equalTo: views[i+1].topAnchor, constant: spacing).isActive = true
        }
    }
    
    func connectHorizontally(views: UIView...){
            for view in views{
                view.centerXAnchor.constraint(equalTo: self.view.safeAreaLayoutGuide.centerXAnchor).isActive = true
        }
    }

    @objc func fahrenheitEditingChanged(sender: UITextField){
        if let text = sender.text {
            if let fahrenheitValue = Double(text){
                if segmentedControl.selectedSegmentIndex == 0{
                    let celsiusValue = 5.0/9.0*(fahrenheitValue - 32.0)
                    celsiusLabel.text = String.init(format: "%.2f", celsiusValue)
                }else{
                    let celsiusValue = 9.0/5.0*fahrenheitValue + 32.0
                    celsiusLabel.text = String.init(format: "%.2f", celsiusValue)
                }
            }else{
                celsiusLabel.text = "???"
            }
        }
    }

    @objc func dismissKeyboard(sender: UIGestureRecognizer){
        fahrenheitTextField.resignFirstResponder()
    }
    
    func addSegmentedControl(){
        segmentedControl = UISegmentedControl(items: ["Fahrenheit", "Celsius"])
        let font = UIFont.systemFont(ofSize: 20)
        segmentedControl!.setTitleTextAttributes([NSAttributedString.Key.font: font], for: .normal)
        segmentedControl.selectedSegmentIndex = 0
        view.addSubview(segmentedControl)
        segmentedControl.translatesAutoresizingMaskIntoConstraints = false
        
        segmentedControl.leadingAnchor.constraint(equalTo: view.safeAreaLayoutGuide.leadingAnchor, constant: 10).isActive = true
        segmentedControl.trailingAnchor.constraint(equalTo: view.safeAreaLayoutGuide.trailingAnchor, constant: -10).isActive = true
        segmentedControl.bottomAnchor.constraint(equalTo: view.safeAreaLayoutGuide.bottomAnchor, constant: -10).isActive = true

        segmentedControl.addTarget(self, action: #selector(changeDegrees), for: .valueChanged)
    }
    @objc func changeDegrees(sender: UISegmentedControl){
        if sender.selectedSegmentIndex == 0{
            fdegreeLabel.text = "degrees Fahrenheit"
            cdegreeLabel.text = "degrees Celsius"
        }else{
            fdegreeLabel.text = "degrees Celsius"
            cdegreeLabel.text = "degrees Fahrenheit"
        }
        fahrenheitTextField.text = ""
        celsiusLabel.text = "???"
    }

}

extension ConversionViewController: UITextFieldDelegate{

    func textField(_ textField: UITextField, shouldChangeCharactersIn range: NSRange,  replacementString string: String) -> Bool {
        let existingTextHasDecimalSeparator = textField.text?.range(of: ".")
        let replacementTextHasDecimalSeparator = string.range(of: ".")
        if existingTextHasDecimalSeparator != nil && replacementTextHasDecimalSeparator != nil {
            return false
        } else{
            return true
        }
    }
}
```