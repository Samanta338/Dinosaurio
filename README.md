# Dinosaurio
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class DinosaurioDibujo extends JPanel implements ActionListener {

    private int x = 100; // Posición inicial en X
    private Timer timer;

    public DinosaurioDibujo() {
        timer = new Timer(30, this); // Actualiza cada 30 milisegundos
        timer.start();
    }

    @Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);
        Graphics2D g2d = (Graphics2D) g;

        // Fondo
        setBackground(Color.WHITE);

        // Cuerpo del dinosaurio (verde)
        g2d.setColor(new Color(34, 139, 34)); // Verde oscuro
        g2d.fillOval(x, 200, 200, 100); // Cuerpo
        g2d.fillOval(x + 30, 150, 80, 80); // Cabeza

        // Sombra para cuerpo
        g2d.setColor(new Color(0, 0, 0, 100)); // Sombra gris oscura
        g2d.fillOval(x + 10, 250, 180, 40); // Sombra bajo el cuerpo

        // Ojos
        g2d.setColor(Color.WHITE);
        g2d.fillOval(x + 55, 165, 15, 15); // Ojo izquierdo
        g2d.setColor(Color.BLACK);
        g2d.fillOval(x + 60, 170, 5, 5); // Pupila izquierda
        
        g2d.setColor(Color.WHITE);
        g2d.fillOval(x + 115, 165, 15, 15); // Ojo derecho
        g2d.setColor(Color.BLACK);
        g2d.fillOval(x + 120, 170, 5, 5); // Pupila derecha

        // Cola
        Polygon cola = new Polygon();
        cola.addPoint(x + 200, 250);
        cola.addPoint(x + 250, 230);
        cola.addPoint(x + 200, 270);
        g2d.fillPolygon(cola);

        // --- Picos en la cola ---
        g2d.setColor(new Color(34, 139, 34)); // Mismo color del cuerpo
        int[] xPicosCola = {x + 215, x + 230, x + 245}; // Coordenadas en X de los picos
        int[] yPicosCola = {245, 215, 245}; // Coordenadas en Y de los picos
        g2d.fillPolygon(xPicosCola, yPicosCola, 3); // Primer pico en la cola

        // Otro pico
        xPicosCola = new int[] {x + 230, x + 245, x + 260};
        yPicosCola = new int[] {245, 215, 245};
        g2d.fillPolygon(xPicosCola, yPicosCola, 3); // Segundo pico

        // Más picos si lo deseas
        xPicosCola = new int[] {x + 245, x + 260, x + 275};
        yPicosCola = new int[] {245, 215, 245};
        g2d.fillPolygon(xPicosCola, yPicosCola, 3); // Tercer pico

        // Piernas
        g2d.fillOval(x + 30, 280, 40, 60);
        g2d.fillOval(x + 120, 280, 40, 60);

        // --- Camiseta del Barcelona ---
        // Parte azulgrana sobre el cuerpo
        g2d.setColor(new Color(0, 0, 139)); // Azul oscuro
        g2d.fillRect(x + 20, 210, 160, 40);

        g2d.setColor(new Color(178, 34, 34)); // Rojo fuerte
        g2d.fillRect(x + 40, 210, 20, 40);
        g2d.fillRect(x + 80, 210, 20, 40);
        g2d.fillRect(x + 120, 210, 20, 40);

        // Escudo simplificado
        g2d.setColor(Color.YELLOW);
        g2d.fillOval(x + 85, 220, 20, 20);

        // Texto Barcelona
        g2d.setColor(Color.BLACK);
        g2d.setFont(new Font("Arial", Font.BOLD, 12));
        g2d.drawString("Barca", x + 70, 250);

        // Sombra de la camiseta
        g2d.setColor(new Color(0, 0, 0, 100)); // Gris oscuro
        g2d.fillRect(x + 20, 250, 160, 20);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        x += 2; // Movimiento hacia la derecha
        if (x > getWidth()) {
            x = -200; // Reinicia el dinosaurio cuando sale de la pantalla
        }
        repaint();
    }

    public static void main(String[] args) {
        JFrame frame = new JFrame("Dinosaurio Barcelona");
        DinosaurioDibujo panel = new DinosaurioDibujo();
        frame.add(panel);
        frame.setSize(800, 600);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }
}
