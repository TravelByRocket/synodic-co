- isShowing vs show  
- subgroups at top of group in navigator  
- avoid extra Spacer  
// no  
VStack {  
    Image(systemName: "star.fill")  
        .foregroundColor(marker.isFavorite ? .orange : .clear)  
        .accessibilityLabel("starred")  
    Spacer()  
}  
  
// yes  
Image(systemName: "star.fill")  
    .foregroundColor(marker.isFavorite ? .orange : .clear)  
    .accessibilityLabel("starred")  
    .frame(maxHeight: .infinity, alignment: .top)```  
- all placeholder values with TODO and in top area declaration, not within body