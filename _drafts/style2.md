- Good way to add Text views  
Group {  
                Text("Create")  
                    .bold()  
                +  
                Text("with")  
                +  
                Text("Swift")  
                    .bold()  
            }  
  
[https://www.createwithswift.com/using-a-uisheetpresentationcontroller-in-swiftui/](https://www.createwithswift.com/using-a-uisheetpresentationcontroller-in-swiftui/)  
- seeminlgy preferred way to bring in content  
init(  
        _ isPresented: Binding<Bool>,  
        onDismiss: (() -> Void)? = nil,  
        detents: [UISheetPresentationController.Detent] = [.medium()],  
        @ViewBuilder content: () -> Content  
    ) {  
        self._isPresented = isPresented  
        self.onDismiss = onDismiss  
        self.detents = detents  
        self.content = content()  
- some way to insert views in between, like a `join`, and/or automatically a droplast etc (see note)  
VStack {  
                ForEach(markers.dropLast(), id: \.self) { marker in  
                    NutritionalMarkerRowStarLeft(marker: marker)  
                    Divider()  
                }  
                if let lastMarker = markers.last {  
                    NutritionalMarkerRowStarLeft(marker: lastMarker)  
                }  
            }  

- Gumroad as exemplar