# Гайдлайн по разработке iOS-приложения на SwiftUI

Все правила из [гайдлайна на Swift](https://github.com/ILYA-2606/SwiftGuideline) также действуют и на SwiftUI

- Название UI-компонентов должно иметь суффикс, относящийся к типу SwiftUI-компонента. Например: UserView, BlueButton, VerticalGrid, SortableList
- Не рекомендуется использовать @EnvironmentObject по той же причине, что и использование Force Unwrapping
- Не рекомендуется писать логику во View
- Если тело View более 50 строк, то рекомендуется выносить части в вычисляемые переменные или другие кастомные View
- Рекомендуется выносить содержимое ForEach

## Порядок написания свойств

- Типы (enum/struct) в порядке доступа от наиболее открытого к закрытому (open, public, internal, fileprivate, private)
- Константы и переменные (let/var) в порядке врапперов (Environment, ObservedObject, StateObject, Binding, State, без враппера) и доступа
- Инициализаторы
- Приватные методы

Пример корректного порядка свойств внутри View:  
```swift
struct MyView: some View {
    enum State {
        case opened
        case closed
    }
    
    struct Container { ... }
    
    private enum Mode {
        case showed
        case hided
    }
    
    let state: State = .closed
    
    @Environment(\.presentationMode) var presentationMode
    
    @ObservedObject var storage = ScreenStorage.shared
    
    @StateObject var viewModel = MyViewModel()
    
    @Binding var isOn: Bool
    
    @State var title = ""
    
    var body: some View { ... }
    
    private let mode: Mode = .hided
    
    @Environment(\.openURL) private var openURL
    
    init() { ... }
    
    private func processLoading() { ... }
}
```
