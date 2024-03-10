# AlgoritmoDeWuA201091
Ejemplo de trazado de lineas con el algoritmo de Wu con SwiftUI
//
//  ContentView.swift
//  AlgoritmoWu
//
//  Created by Jorge Alfredo on 07/03/24.
//
import SwiftUI
//  Se define una estructura llamada WuLineDrawingShape que implementa el protocolo Shape de SwiftUI, un Shape en SwiftUi es una vista que puede dibujarse mediante un trazado.
struct WuLineDrawingShape: Shape {
    var startX: CGFloat
    var startY: CGFloat
    var endX: CGFloat
    var endY: CGFloat
    var lineOpacity: Double
    var lineColor: Color

    func path(in rect: CGRect) -> Path {
        var path = Path()

       //   Dentro de la función path se crea un objeto     Path que representa la forma que se dibujará.

        // Utiliza las variables startX, startY, endX y endY

        // Mueve el punto de inicio y agrega una línea hasta el punto final
        path.move(to: CGPoint(x: startX, y: startY))
        path.addLine(to: CGPoint(x: endX, y: endY))

        // Se ajusta el color de la línea con la opacidad
        let lineColorWithOpacity = lineColor.opacity(lineOpacity)

        // No necesitamos .fill aquí, simplemente devolvemos el camino
        return path
            .strokedPath(StrokeStyle(lineWidth: 2, lineCap: .round, lineJoin: .round))
    }
}
//  Se define otra estructura llamada ‘wu Line drawing view’ que implementa la vista principal.

struct WuLineDrawingView: View {
    
    //  Se utilizan propiedades de estado ('@State') para las coordenadas de inicio y fin, la opacidad de la línea y se establece un valor predeterminado.
    @State private var startX: CGFloat = 50
    @State private var startY: CGFloat = 50
    @State private var endX: CGFloat = 200
    @State private var endY: CGFloat = 200
    @State private var lineOpacity: Double = 1.0
    
//  En el cuerpo (‘body’) de la vista, se crea una pila vertical (‘Vstack’) que contiene la forma ‘wu Line drawing shape’ con valores iniciales y un botón para regenerar la línea.
    var body: some View {
        VStack {
            WuLineDrawingShape(startX: startX, startY: startY, endX: endX, endY: endY, lineOpacity: lineOpacity, lineColor: Color.blue)
                .frame(width: 300, height: 300)
                .padding()

            Button("Regenerate Line") {
                regenerateLine()
            }
            .padding()
        }
    }
    
//  La función ‘regenerateLine’ se encarga de generar nuevas coordenadas aleatorias para la línea y ajustar la opacidad al hacer click en el botón RegenerateLine.
    private func regenerateLine() {
        startX = CGFloat.random(in: 0..<300)
        startY = CGFloat.random(in: 0..<300)
        endX = CGFloat.random(in: 0..<300)
        endY = CGFloat.random(in: 0..<300)

        // Se ajusta la opacidad al regenerar la línea
        lineOpacity = Double.random(in: 0.5...1.0)
    }
}

//  Contentview_Previews’ proporciona una vista previa para el diseño en el lienzo de desarrollo de Xcode
struct ContentView_Previews: PreviewProvider {
    static var previews: some View {
        WuLineDrawingView()
    }
}

//  AlgoritmoWuApp es la aplicación principal que inicia la ventana con WuLineDrawingView.
@main
struct AlgoritmoWuApp: App {
    var body: some Scene {
        WindowGroup {
            WuLineDrawingView()
        }
    }
}
