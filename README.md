package paint; 
import java.awt.*; 
import javax.swing.*; 
import javax.swing.event.ChangeEvent; 
import javax.swing.event.ChangeListener; 
 
public class SimplePaint extends JFrame { 
 
 static public Color c; 
 private static final long serialVersionUID = 1L; 
 //Конструктор класса 
 public SimplePaint(String s) { 
//Вызываем конструктор суперкласса, то есть класса JFrame 
//и передаем в него строку заголовка окна 
 super(s); 
//Запрещаем менять размеры окна 
 this.setResizable(false); 
//Устанавливаем размеры окна 
 this.setSize(800, 800); 
//Создаем объект класса PaintPanel, который описан ниже 
 PaintPanel panel = new PaintPanel(this, 800, 800); 
//Добавляем к созданному объекту обработчики событий 
//В нашем случае этот объект сам будет обрабатывать свои события 
 panel.addMouseListener(panel); 
 panel.addMouseMotionListener(panel); 
 panel.addMouseWheelListener(panel); 
//Создаем скроллируемую панел, чтобы посмотреть, как это делается 
//Скроллировать эта панель будет панель для рисования panel, её и 
//передаем в конструктор JScrollPane 
 JScrollPane pane = new JScrollPane(panel); 
//Определяем, чтобы вертикальная и горизонтальная полосы прокрутки 
// панели показывались всегда 
 pane.setVerticalScrollBarPolicy(ScrollPaneConstants. VERTICAL_SCROLLBAR_ALWAYS); 
 pane.setHorizontalScrollBarPolicy(ScrollPaneConstants.HORIZONTAL_SCROLLBAR_ALWAYS); 
//Добавляем панель для рисования в центральную область нашего окна 
//this - ссылка на самого себя, то есть в нашем случае объект 
//класса SimplePaint 
 this.add(pane, BorderLayout.CENTER); 
//Создаем новую панель 
 JPanel p = new JPanel(); 
//Добавляем эту панель в нижнюю часть нашего (южную) окна 
 this.add(p, BorderLayout.SOUTH); 
//Создаем несколько кнопок, каждую из которых добавляем на панель 
//Определяем обработчика событий для каждой кнопки 
 JButton b1 = new JButton("Change color"); 
 p.add(b1); 
 b1.addActionListener(panel); 
 JColorChooser jCC = new JColorChooser(); 
 p.add(jCC); 
 jCC.getSelectionModel().addChangeListener(new ChangeListener() { 
 public void stateChanged(ChangeEvent e) { 
 Color chosenColor = jCC.getColor(); 
 panel.setCurColor(chosenColor); 
 
 } 
 }); 
// p.add(jCC); 
// c = jCC.getColor(); 
 
//Определяем действие при закрытии окна 
 this.setDefaultCloseOperation(EXIT_ON_CLOSE); 
//Делаем окно видимым 
 this.setVisible(true); 
 this.setResizable(true); 
 } 
 public static void main(String[] args) { 
//Создаем окно как безымянный объект, потому что имя его нам не нужно 
 new SimplePaint("Очень простой редактор"); 
 } 
}
