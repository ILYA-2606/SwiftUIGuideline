# Гайдлайн по разработке iOS-приложения на SwiftUI

Все правила из [гайдлайна на Swift](https://github.com/ILYA-2606/SwiftGuideline) также действуют и на SwiftUI

- Название UI-компонентов должно иметь суффикс, относящийся к типу SwiftUI-компонента. Например: UserView, BlueButton, VerticalGrid, SortableList
- Не рекомендуется использовать @EnvironmentObject по той же причине, что и использование Force Unwrapping
- Не рекомендуется писать логику во View
- Если тело View более 50 строк, то рекомендуется выносить части в вычисляемые переменные или другие кастомные View
- Рекомендуется выносить содержимое ForEach

## Порядок написания свойств

- Порядок написания должен соответствовать в первую очередь от принадлежности (enum, let, var, func)
- Далее по модификаторам доступа от наиболее открытого к закрытому (open, public, internal, fileprivate, private)
- Далее по порядку врапперов (Environment, ObservedObject, StateObject, Binding, State, без враппера)
- Пример корректного порядка свойств внутри View:  
```swift
struct MyView: some View {
    enum State {
        case opened
        case closed
    }
    
    let state: State
    
    @Environment(\.presentationMode) var presentationMode
    
    @ObservedObject var storage = ScreenStorage.shared
    
    @StateObject var viewModel = MyViewModel()
    
    @Binding var isOn: Bool
    
    @State var title = ""
    
    var body: some View { ... }

    @Environment(\.openURL) private var openURL
}
```
