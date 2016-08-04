# UIView

## 스토리보드에서 UIButton 테두리 색 변경하기

`@IBInspectable`을 이용하면 스토리보드(Storyboard) 에서도 쉽게 테두리를 설정할 수 있다.
http://stackoverflow.com/a/38068594/4622153

```Swift
extension UIView {

    @IBInspectable var cornerRadius: CGFloat {
        get {
            return layer.cornerRadius
        }
        set {
            layer.cornerRadius = newValue
            layer.masksToBounds = newValue > 0
        }
    }

    @IBInspectable var borderWidth: CGFloat {
        get {
            return layer.borderWidth
        }
        set {
            layer.borderWidth = newValue
        }
    }

    @IBInspectable var borderColor: UIColor? {
        get {
            return UIColor(CGColor: layer.borderColor!)
        }
        set {
            layer.borderColor = newValue?.CGColor
        }
    }
}
```
