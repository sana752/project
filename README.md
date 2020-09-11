# project
cs50's project file

Final Project Report on “Introduction to Computer Science” Final Project Report for CS50X                    Course - Introduction to Computer Science Multi Apps Software   On Java Programming language
CS50’s
CS50’s

[This is a Final project report for CS50’s (Introduction to Computer Science) – Multi App software with synopsis , Screen shots and codes]
Text Type Doc

 
It is a software designed in Core Java which has multiple operations like calculator,notepad,tik tak toe game,puzzle and many more . It is a complete software which is a stress bustor and a user can get multiple screen on one screen .
Objective/ Vision
A Java Application Multi App Software where user can use applications developed in Java such as calculator, notepad+, puzzle game, ip finder, word count tool, source code generator, picture puzzle game, tic tac toe game and exam system.
Users of the System
1.	User
Functional Requirements
1. User
1.	Can use calculator
2.	Can use notepad+
3.	Can use puzzle game
4.	Can use picture puzzle game
5.	Can use tic tac toe game
6.	Can use ip finder
7.	Can use word count tool
8.	Can use source code generator
9.	Can use exam system
Tools to be used
1.	Use any IDE to develop the project. It may be Eclipse /Myeclipse / Netbeans etc.
Front End and Back End
1.	Front End: Java Swing
2.	Back End: No

Screen Shots with Code
 

Word counter code

import java.awt.*;  
import javax.swing.*;  
import java.awt.event.*;  
public class CharCount extends JFrame implements ActionListener{  
    JLabel lb1,lb2;  
    JTextArea ta;  
    JButton b;  
    JButton pad,text;  
    CharCount(){  
        super("Char Word Count Tool - JTP");  
        lb1=new JLabel("Characters: ");  
        lb1.setBounds(50,50,100,20);  
        lb2=new JLabel("Words: ");  
        lb2.setBounds(50,80,100,20);  
          
        ta=new JTextArea();  
        JScrollPane sp=new JScrollPane(ta);
        sp.setBounds(50,110,300,200);  
          
        b=new JButton("Count");  
        b.setBounds(50,320, 80,30);//x,y,w,h  
        b.addActionListener(this);  
      
        pad=new JButton("Pad Color");  
        pad.setBounds(140,320, 110,30);//x,y,w,h  
        pad.addActionListener(this);  
  
        text=new JButton("Text Color");  
        text.setBounds(260,320, 110,30);//x,y,w,h  
        text.addActionListener(this);  
  
        add(lb1);add(lb2);add(sp);add(b);add(pad);add(text);  
          
        setSize(400,400);  
        setLayout(null);//using no layout manager  
        setVisible(true);  
        setDefaultCloseOperation(DISPOSE_ON_CLOSE);  
    }  
    public void actionPerformed(ActionEvent e){  
        if(e.getSource()==b){  
        String text=ta.getText();  
        lb1.setText("Characters: "+text.length());  
        String words[]=text.split("\\s");  
        lb2.setText("Words: "+words.length);  
        }else if(e.getSource()==pad){  
            Color c=JColorChooser.showDialog(this,"Choose Color",Color.BLACK);  
            ta.setBackground(c);  
        }else if(e.getSource()==text){  
            Color c=JColorChooser.showDialog(this,"Choose Color",Color.BLACK);  
            ta.setForeground(c);  
        }  
    }  
public static void main(String[] args) {  
    new CharCount();  
}}  

 Font chooser code

import java.io.*;
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import javax.swing.event.*;
class FontDemo extends JFrame
{
FontChooser dialog=null; 
JTextArea ta;
JButton fontButton;

FontDemo()
{
super("Font");

ta=new JTextArea(7,20);
fontButton=new JButton("Set Font");

ActionListener ac=new ActionListener()
{
public void actionPerformed(ActionEvent ev)
{
if(dialog==null)
	dialog=new FontChooser(ta.getFont());
if(dialog.showDialog(FontDemo.this,"Choose a font"))
	{
	FontDemo.this.ta.setFont(dialog.createFont());
	}
}
};
fontButton.addActionListener(ac);

add(ta,BorderLayout.CENTER);
add(fontButton,BorderLayout.SOUTH);

setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
setBounds(50,50,400,400);
ta.append("Hello dear. how r u?");
ta.append("\n\n A quick brown fox jumps over the lazy dog.");
ta.append("\n\n0123456789");
ta.append("\n~!@#$%^&*()_+|?><");
setVisible(true);
}
public static void main(String[] args)
{
new FontDemo();
}

}
public class FontChooser extends JPanel //implements ActionListener
{
private Font thisFont;

private JList jFace, jStyle, jSize;

private JDialog dialog;
private JButton okButton;

JTextArea tf;

private boolean ok;

public FontChooser(Font withFont)
{
thisFont=withFont;
String[] fontNames=
	GraphicsEnvironment
	.getLocalGraphicsEnvironment()
	.getAvailableFontFamilyNames();
jFace=new JList(fontNames); jFace.setSelectedIndex(0);

jFace.addListSelectionListener(new ListSelectionListener()
{public void valueChanged(ListSelectionEvent ev){tf.setFont(createFont());}});

String[] fontStyles={"Regular","Italic","Bold","Bold Italic"};
jStyle=new JList(fontStyles);jStyle.setSelectedIndex(0); 

jStyle.addListSelectionListener(new ListSelectionListener()
{public void valueChanged(ListSelectionEvent ev){tf.setFont(createFont());}});

String[] fontSizes=new String[30];
for(int j=0; j<30; j++)
	fontSizes[j]=new String(10+j*2+"");
jSize=new JList(fontSizes); jSize.setSelectedIndex(0); 

jSize.addListSelectionListener(new ListSelectionListener()
{public void valueChanged(ListSelectionEvent ev){tf.setFont(createFont());}});

JPanel jpLabel=new JPanel();
jpLabel.setLayout(new GridLayout(1,3));

jpLabel.add(new JLabel("Font",JLabel.CENTER));
jpLabel.add(new JLabel("Font Style",JLabel.CENTER));
jpLabel.add(new JLabel("Size",JLabel.CENTER));

JPanel jpList=new JPanel();
jpList.setLayout(new GridLayout(1,3));

jpList.add(new JScrollPane(jFace));
jpList.add(new JScrollPane(jStyle));
jpList.add(new JScrollPane(jSize));

okButton=new JButton("OK");
JButton cancelButton=new JButton("Cancel");

okButton.addActionListener(
new ActionListener()
{
public void actionPerformed(ActionEvent ev)
{
ok=true;
FontChooser.this.thisFont=FontChooser.this.createFont();
dialog.setVisible(false);
}
});

cancelButton.addActionListener(
new ActionListener()
{
public void actionPerformed(ActionEvent ev)
{
dialog.setVisible(false);
}
});

JPanel jpButton=new JPanel();
jpButton.setLayout(new FlowLayout());
jpButton.add(okButton);
jpButton.add(new JLabel("          "));//dummy Label
jpButton.add(cancelButton);

tf=new JTextArea(5,30);
JPanel jpTextField=new JPanel();
jpTextField.add(new JScrollPane(tf));

JPanel centerPanel=new JPanel();
centerPanel.setLayout(new GridLayout(2,1));
centerPanel.add(jpList);
centerPanel.add(jpTextField);

setLayout(new BorderLayout());
add(jpLabel,BorderLayout.NORTH);
add(centerPanel,BorderLayout.CENTER);
add(jpButton,BorderLayout.SOUTH);
add(new JLabel("  "),BorderLayout.EAST);//dummy label
add(new JLabel("  "),BorderLayout.WEST);//dummy label

tf.setFont(thisFont);
tf.append("\nA quick brown fox jumps over the lazy dog.");
tf.append("\n0123456789");
tf.append("\n~!@#$%^&*()_+|?><\n");

}
public Font createFont()
{
Font fnt=thisFont;
int fontstyle=Font.PLAIN;
int x=jStyle.getSelectedIndex();

switch(x)
{
case 0:
	fontstyle=Font.PLAIN;	break;
case 1:
	fontstyle=Font.ITALIC;	break;
case 2:
	fontstyle=Font.BOLD;	break;
case 3:
	fontstyle=Font.BOLD+Font.ITALIC;	break;
}

int fontsize=Integer.parseInt((String)jSize.getSelectedValue());
String fontname=(String)jFace.getSelectedValue();

fnt=new Font(fontname,fontstyle,fontsize);

return fnt;

}
public boolean showDialog(Component parent, String title)
{
ok=false;

Frame owner=null;
if(parent instanceof Frame) 
	owner=(Frame)parent;
else
	owner=(Frame)SwingUtilities.getAncestorOfClass(Frame.class,parent);
if(dialog==null || dialog.getOwner()!=owner)
{
dialog=new JDialog(owner,true);
dialog.add(this);
dialog.getRootPane().setDefaultButton(okButton);
dialog.setSize(400,325);
}

dialog.setTitle(title);
dialog.setVisible(true);
return ok;
}

}

IP Address Finder

import javax.swing.*;  
import java.awt.event.*;  
import java.net.*;  
public class IPFinder extends JFrame implements ActionListener{  
    JLabel l;  
    JTextField tf;  
    JButton b;  
IPFinder(){  
    super("IP Finder Tool");  
    l=new JLabel("Enter Website URL:");  
    l.setBounds(50,70,150,20);;  
    tf=new JTextField();  
    tf.setBounds(50,100,200,20);  
      
    b=new JButton("Find IP");  
    b.setBounds(100,150,80,30);  
    b.addActionListener(this);  
    add(l);  
    add(tf);  
    add(b);  
    setSize(400,300);  
    setLayout(null);  
    setVisible(true);  
}  
public void actionPerformed(ActionEvent e){  
    String url=tf.getText();  
    try {  
        InetAddress ia=InetAddress.getByName(url);  
        String ip=ia.getHostAddress();  
        JOptionPane.showMessageDialog(this,"IP of "+url+" is: "+ip);  
    } catch (UnknownHostException e1) {  
        JOptionPane.showMessageDialog(this,e1.toString());  
    }  
}  
public static void main(String[] args) {  
    new IPFinder();  
}  
}

JApp Code

import java.awt.BorderLayout;
import java.awt.EventQueue;

import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;
import javax.swing.GroupLayout;
import javax.swing.GroupLayout.Alignment;
import javax.swing.JButton;
import javax.swing.ImageIcon;
import javax.swing.JLabel;
import java.awt.Color;
import java.awt.Font;
import javax.swing.LayoutStyle.ComponentPlacement;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;

public class JApps extends JFrame {

	private JPanel contentPane;

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					JApps frame = new JApps();
					frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}

	/**
	 * Create the frame.
	 */
	public JApps() {
		setTitle("Java Application World");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 700, 771);
		contentPane = new JPanel();
		contentPane.setBackground(new Color(204, 255, 204));
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		
		JButton btnNewButton = new JButton("");
		btnNewButton.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent arg0) {
				Notepad.main(new String[]{});
			}
		});
		btnNewButton.setIcon(new ImageIcon(JApps.class.getResource("/com/javatpoint/notepad.jpg")));
		
		JLabel lblJavaApplicationWorld = new JLabel("Java Application World");
		lblJavaApplicationWorld.setFont(new Font("Tahoma", Font.PLAIN, 21));
		lblJavaApplicationWorld.setForeground(new Color(204, 51, 51));
		
		JButton button = new JButton("");
		button.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				MyCalculator.main(new String[]{});
			}
		});
		button.setIcon(new ImageIcon(JApps.class.getResource("/com/javatpoint/calculator.jpg")));
		
		JButton button_1 = new JButton("");
		button_1.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				IPFinder.main(new String[]{});
			}
		});
		button_1.setIcon(new ImageIcon(JApps.class.getResource("/com/javatpoint/ip.jpg")));
		
		JButton button_2 = new JButton("");
		button_2.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				TTT1.main(new String[]{});
			}
		});
		button_2.setIcon(new ImageIcon(JApps.class.getResource("/com/javatpoint/tictactoe.jpg")));
		
		JButton button_3 = new JButton("");
		button_3.setIcon(new ImageIcon(JApps.class.getResource("/com/javatpoint/picturepuzzle.jpg")));
		
		JButton button_4 = new JButton("");
		button_4.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				CharCount.main(new String[]{});
			}
		});
		button_4.setIcon(new ImageIcon(JApps.class.getResource("/com/javatpoint/wct.jpg")));
		
		JButton button_5 = new JButton("");
		button_5.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				Puzzle.main(new String[]{});
			}
		});
		button_5.setIcon(new ImageIcon(JApps.class.getResource("/com/javatpoint/Puzzle Game.jpg")));
		
		JButton button_6 = new JButton("");
		button_6.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				OnlineTest.main(new String[]{});
			}
		});
		button_6.setIcon(new ImageIcon(JApps.class.getResource("/com/javatpoint/Exam System.jpg")));
		
		JButton button_7 = new JButton("");
		button_7.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				SourceGetter.main(new String[]{});
			}
		});
		button_7.setIcon(new ImageIcon(JApps.class.getResource("/com/javatpoint/Source Code Generator.jpg")));
		GroupLayout gl_contentPane = new GroupLayout(contentPane);
		gl_contentPane.setHorizontalGroup(
			gl_contentPane.createParallelGroup(Alignment.LEADING)
				.addGroup(gl_contentPane.createSequentialGroup()
					.addGroup(gl_contentPane.createParallelGroup(Alignment.LEADING)
						.addGroup(gl_contentPane.createSequentialGroup()
							.addContainerGap()
							.addComponent(btnNewButton, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE)
							.addPreferredGap(ComponentPlacement.UNRELATED)
							.addComponent(button, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE)
							.addPreferredGap(ComponentPlacement.UNRELATED)
							.addComponent(button_1, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE))
						.addGroup(gl_contentPane.createSequentialGroup()
							.addGap(186)
							.addComponent(lblJavaApplicationWorld))
						.addGroup(gl_contentPane.createSequentialGroup()
							.addContainerGap()
							.addComponent(button_2, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE)
							.addPreferredGap(ComponentPlacement.UNRELATED)
							.addComponent(button_3, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE)
							.addPreferredGap(ComponentPlacement.UNRELATED)
							.addComponent(button_4, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE))
						.addGroup(gl_contentPane.createSequentialGroup()
							.addContainerGap()
							.addComponent(button_5, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE)
							.addPreferredGap(ComponentPlacement.UNRELATED)
							.addComponent(button_6, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE)
							.addPreferredGap(ComponentPlacement.UNRELATED)
							.addComponent(button_7, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE)))
					.addContainerGap(17, Short.MAX_VALUE))
		);
		gl_contentPane.setVerticalGroup(
			gl_contentPane.createParallelGroup(Alignment.LEADING)
				.addGroup(gl_contentPane.createSequentialGroup()
					.addGap(12)
					.addComponent(lblJavaApplicationWorld)
					.addGap(18)
					.addGroup(gl_contentPane.createParallelGroup(Alignment.LEADING)
						.addComponent(button_1, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE)
						.addComponent(btnNewButton)
						.addComponent(button, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE))
					.addPreferredGap(ComponentPlacement.UNRELATED)
					.addGroup(gl_contentPane.createParallelGroup(Alignment.LEADING)
						.addComponent(button_2, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE)
						.addComponent(button_3, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE)
						.addComponent(button_4, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE))
					.addPreferredGap(ComponentPlacement.UNRELATED)
					.addGroup(gl_contentPane.createParallelGroup(Alignment.LEADING)
						.addComponent(button_5, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE)
						.addComponent(button_6, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE)
						.addComponent(button_7, GroupLayout.PREFERRED_SIZE, 209, GroupLayout.PREFERRED_SIZE))
					.addContainerGap(17, Short.MAX_VALUE))
		);
		contentPane.setLayout(gl_contentPane);
	}
}
 
Look and Feel Menu


import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

class LookAndFeelDemo  
extends JFrame
{
JLabel myLabel;
JMenuBar jmb;
JMenu fileMenu;

LookAndFeelDemo()
{
super("Look and Feel  
Demo");
add(myLabel=new JLabel 
("This is a Label"));
add(new JButton 
("Button")); 
add(new JCheckBox 
("CheckBox"));
add(new JRadioButton 
("RadioButton"));
setLayout(new FlowLayout 
());
setSize(350,350);
setDefaultCloseOperation 
(WindowConstants.EXIT_ON_ 
CLOSE);
jmb=new JMenuBar();
setJMenuBar(jmb);
fileMenu=new JMenu("Look  
and Feel");
jmb.add(fileMenu);
LookAndFeelMenu.createLoo 
kAndFeelMenuItem 
(fileMenu,this);
setVisible(true);
}
public static void main 
(String[] args)
{
new LookAndFeelDemo();
}

}
public class  
LookAndFeelMenu
{

public static void  
createLookAndFeelMenuItem 
(JMenu jmenu,Component  
cmp)
{
final  
UIManager.LookAndFeelInfo 
[]  
infos=UIManager.getInstal 
ledLookAndFeels();

JRadioButtonMenuItem rbm 
[]=new  
JRadioButtonMenuItem 
[infos.length];
ButtonGroup bg=new  
ButtonGroup();
JMenu tmp=new JMenu 
("Change Look and Feel");
tmp.setMnemonic('C');
for(int i=0;  
i<infos.length; i++)
{
rbm[i]=new  
JRadioButtonMenuItem 
(infos[i].getName());
rbm[i].setMnemonic(infos 
[i].getName().charAt(0));
tmp.add(rbm[i]);
bg.add(rbm[i]);
rbm[i].addActionListener 
(new  
LookAndFeelMenuListener 
(infos[i].getClassName 
(),cmp));
}

rbm[0].setSelected(true);
jmenu.add(tmp);

}

}
class  
LookAndFeelMenuListener  
implements ActionListener
{
String classname;
Component jf;

LookAndFeelMenuListener 
(String cln,Component jf)
{
this.jf=jf;
classname=new String 
(cln);
}

public void  
actionPerformed 
(ActionEvent ev)
{
try
{
UIManager.setLookAndFeel 
(classname);
SwingUtilities.updateComp 
onentTreeUI(jf);
}
catch(Exception e) 
{System.out.println(e);}
}
} 

Calculator Code-


/*
Save this file as MyCalculator.java
to compile it use
	javac MyCalculator.java
to use the calculator 
Apply this-
	java MyCalculator

*/
import java.awt.*;
import java.awt.event.*;
*/

public class MyCalculator extends Frame
{

public boolean setClear=true;
double number, memValue;
char op;

String digitButtonText[] = {"7", "8", "9", "4", "5", "6", "1", "2", "3", "0", "+/-", "." };
String operatorButtonText[] = {"/", "sqrt", "*", "%", "-", "1/X", "+", "=" };
String memoryButtonText[] = {"MC", "MR", "MS", "M+" };
String specialButtonText[] = {"Backspc", "C", "CE" };

MyDigitButton digitButton[]=new MyDigitButton[digitButtonText.length];
MyOperatorButton operatorButton[]=new MyOperatorButton[operatorButtonText.length];
MyMemoryButton memoryButton[]=new MyMemoryButton[memoryButtonText.length];
MySpecialButton specialButton[]=new MySpecialButton[specialButtonText.length];

Label displayLabel=new Label("0",Label.RIGHT);
Label memLabel=new Label(" ",Label.RIGHT);

final int FRAME_WIDTH=325,FRAME_HEIGHT=325;
final int HEIGHT=30, WIDTH=30, H_SPACE=10,V_SPACE=10;
final int TOPX=30, TOPY=50;

MyCalculator(String frameText)//constructor
{
super(frameText);

int tempX=TOPX, y=TOPY;
displayLabel.setBounds(tempX,y,240,HEIGHT);
displayLabel.setBackground(Color.BLUE);
displayLabel.setForeground(Color.WHITE);
add(displayLabel);

memLabel.setBounds(TOPX,  TOPY+HEIGHT+ V_SPACE,WIDTH, HEIGHT);
add(memLabel);

// set Co-ordinates for //Memory Buttons

tempX=TOPX;	
y=TOPY+2*(HEIGHT+V_SPACE);
for(int i=0; i<memoryButton.length; i++)
{
memoryButton[i]=new MyMemoryButton(tempX,y,WIDTH,HEIGHT,memoryButtonText[i], this);
memoryButton[i].setForeground(Color.RED);
y+=HEIGHT+V_SPACE;
}

/*set Co-ordinates for Special Buttons*/
tempX=TOPX+1*(WIDTH+H_SPACE); y=TOPY+1*(HEIGHT+V_SPACE);
for(int i=0;i<specialButton.length;i++)
{
specialButton[i]=new MySpecialButton(tempX,y,WIDTH*2,HEIGHT,specialButtonText[i], this);
specialButton[i].setForeground(Color.RED);
tempX=tempX+2*WIDTH+H_SPACE;
}

//set Co-ordinates for Digit Buttons
int digitX=TOPX+WIDTH+H_SPACE;
int digitY=TOPY+2*(HEIGHT+V_SPACE);
tempX=digitX;  y=digitY;
for(int i=0;i<digitButton.length;i++)
{
digitButton[i]=new MyDigitButton(tempX,y,WIDTH,HEIGHT,digitButtonText[i], this);
digitButton[i].setForeground(Color.BLUE);
tempX+=WIDTH+H_SPACE;
if((i+1)%3==0){tempX=digitX; y+=HEIGHT+V_SPACE;}
}

//set Co-ordinates for Operator Buttons
int opsX=digitX+2*(WIDTH+H_SPACE)+H_SPACE;
int opsY=digitY;
tempX=opsX;  y=opsY;
for(int i=0;i<operatorButton.length;i++)
{
tempX+=WIDTH+H_SPACE;
operatorButton[i]=new MyOperatorButton(tempX,y,WIDTH,HEIGHT,operatorButtonText[i], this);
operatorButton[i].setForeground(Color.RED);
if((i+1)%2==0){tempX=opsX; y+=HEIGHT+V_SPACE;}
}

addWindowListener(new WindowAdapter()
{
public void windowClosing(WindowEvent ev)
{System.exit(0);}
});

setLayout(null);
setSize(FRAME_WIDTH,FRAME_HEIGHT);
setVisible(true);
}
static String getFormattedText(double temp)
{
String resText=""+temp;
if(resText.lastIndexOf(".0")>0)
	resText=resText.substring(0,resText.length()-2);
return resText;
}

public static void main(String []args)
{
new MyCalculator("Calculator");
}
}



class MyDigitButton extends Button implements ActionListener
{
MyCalculator cl;
MyDigitButton(int x,int y, int width,int height,String cap, MyCalculator clc)
{
super(cap);
setBounds(x,y,width,height);
this.cl=clc;
this.cl.add(this);
addActionListener(this);
}

static boolean isInString(String s, char ch)
{
for(int i=0; i<s.length();i++) if(s.charAt(i)==ch) return true;
return false;
}
public void actionPerformed(ActionEvent ev)
{
String tempText=((MyDigitButton)ev.getSource()).getLabel();

if(tempText.equals("."))
{
 if(cl.setClear) 
	{cl.displayLabel.setText("0.");cl.setClear=false;}
 else if(!isInString(cl.displayLabel.getText(),'.'))
	cl.displayLabel.setText(cl.displayLabel.getText()+".");
 return;
}

int index=0;
try{
        index=Integer.parseInt(tempText);
    }catch(NumberFormatException e){return;}

if (index==0 && cl.displayLabel.getText().equals("0")) return;

if(cl.setClear)
        	{cl.displayLabel.setText(""+index);cl.setClear=false;}
else
	cl.displayLabel.setText(cl.displayLabel.getText()+index);
}//actionPerformed
}//class defination

class MyOperatorButton extends Button implements ActionListener
{
MyCalculator cl;

MyOperatorButton(int x,int y, int width,int height,String cap, MyCalculator clc)
{
super(cap);
setBounds(x,y,width,height);
this.cl=clc;
this.cl.add(this);
addActionListener(this);
}
///////////////////////
public void actionPerformed(ActionEvent ev)
{
String opText=((MyOperatorButton)ev.getSource()).getLabel();

cl.setClear=true;
double temp=Double.parseDouble(cl.displayLabel.getText());

if(opText.equals("1/x"))
	{
	try
		{double tempd=1/(double)temp;
		cl.displayLabel.setText(MyCalculator.getFormattedText(tempd));}
 	catch(ArithmeticException excp)
                		{cl.displayLabel.setText("Divide by 0.");}
	return;
	}
if(opText.equals("sqrt"))
	{
	try
		{double tempd=Math.sqrt(temp);
		cl.displayLabel.setText(MyCalculator.getFormattedText(tempd));}
        	catch(ArithmeticException excp)
	                {cl.displayLabel.setText("Divide by 0.");}
	return;
	}
if(!opText.equals("="))
	{
	cl.number=temp;
	cl.op=opText.charAt(0);
	return;
	}
// process = button pressed
switch(cl.op)
{
case '+':
	temp+=cl.number;break;
case '-':
	temp=cl.number-temp;break;
case '*':
	temp*=cl.number;break;
case '%':
	try{temp=cl.number%temp;}
	catch(ArithmeticException excp)
		{cl.displayLabel.setText("Divide by 0."); return;}
	break;
case '/':
	try{temp=cl.number/temp;}
        catch(ArithmeticException excp)
                {cl.displayLabel.setText("Divide by 0."); return;}
	break;
}//switch

cl.displayLabel.setText(MyCalculator.getFormattedText(temp));
//cl.number=temp;
}//actionPerformed
}//class


class MyMemoryButton extends Button implements ActionListener
{
MyCalculator cl;


MyMemoryButton(int x,int y, int width,int height,String cap, MyCalculator clc)
{
super(cap);
setBounds(x,y,width,height);
this.cl=clc;
this.cl.add(this);
addActionListener(this);
}

public void actionPerformed(ActionEvent ev)
{
char memop=((MyMemoryButton)ev.getSource()).getLabel().charAt(1);

cl.setClear=true;
double temp=Double.parseDouble(cl.displayLabel.getText());

switch(memop)
{
case 'C': 
	cl.memLabel.setText(" ");cl.memValue=0.0;break;
case 'R': 
	cl.displayLabel.setText(MyCalculator.getFormattedText(cl.memValue));break;
case 'S':
	cl.memValue=0.0;
case '+': 
	cl.memValue+=Double.parseDouble(cl.displayLabel.getText());
	if(cl.displayLabel.getText().equals("0") || cl.displayLabel.getText().equals("0.0")  )
		cl.memLabel.setText(" ");
	else 
		cl.memLabel.setText("M");	
	break;
}//switch
}//actionPerformed
}//class


class MySpecialButton extends Button implements ActionListener
{
MyCalculator cl;

MySpecialButton(int x,int y, int width,int height,String cap, MyCalculator clc)
{
super(cap);
setBounds(x,y,width,height);
this.cl=clc;
this.cl.add(this);
addActionListener(this);
}

static String backSpace(String s)
{
String Res="";
for(int i=0; i<s.length()-1; i++) Res+=s.charAt(i);
return Res;
}
public void actionPerformed(ActionEvent ev)
{
String opText=((MySpecialButton)ev.getSource()).getLabel();
//check for backspace button
if(opText.equals("Backspc"))
{
String tempText=backSpace(cl.displayLabel.getText());
if(tempText.equals("")) 
	cl.displayLabel.setText("0");
else 
	cl.displayLabel.setText(tempText);
return;
}
//check for "C" button i.e. Reset
if(opText.equals("C")) 
{
cl.number=0.0; cl.op=' '; cl.memValue=0.0;
cl.memLabel.setText(" ");
}

//it must be CE button pressed
cl.displayLabel.setText("0");cl.setClear=true;
}//actionPerformed
}//class

/*********************************************

Features not implemented and few bugs

i)  No coding done for "+/-" button.
ii) Menubar is not included.
iii)Not for Scientific calculation
iv)Some of the computation may lead to unexpected result
   due to the representation of Floating point numbers in computer
   is an approximation to the given value that can be stored
   physically in memory.

***********************************************/
Note Pad Code

import java.io.*;
import java.util.Date;
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import javax.swing.event.*;
//import p1.FontChooser;
//import p1.FontDialog;
//import p1.FindDialog;
//import p1.LookAndFeelMenu;
//import p1.MyFileFilter;
/************************************/
class FileOperation
{
Notepad npd;

boolean saved;
boolean newFileFlag;
String fileName;
String applicationTitle="Notepad+";

File fileRef;
JFileChooser chooser;
/////////////////////////////
boolean isSave(){return saved;}
void setSave(boolean saved){this.saved=saved;}
String getFileName(){return new String(fileName);}
void setFileName(String fileName){this.fileName=new String(fileName);}
/////////////////////////
FileOperation(Notepad npd)
{
this.npd=npd;

saved=true;
newFileFlag=true;
fileName=new String("Untitled");
fileRef=new File(fileName);
this.npd.f.setTitle(fileName+" - "+applicationTitle);

chooser=new JFileChooser();
chooser.addChoosableFileFilter(new MyFileFilter(".java","Java Source Files(*.java)"));
chooser.addChoosableFileFilter(new MyFileFilter(".txt","Text Files(*.txt)"));
chooser.setCurrentDirectory(new File("."));

}
//////////////////////////////////////

boolean saveFile(File temp)
{
FileWriter fout=null;
try
{
fout=new FileWriter(temp);
fout.write(npd.ta.getText());
}
catch(IOException ioe){updateStatus(temp,false);return false;}
finally
{try{fout.close();}catch(IOException excp){}}
updateStatus(temp,true);
return true;
}
////////////////////////
boolean saveThisFile()
{

if(!newFileFlag)
	{return saveFile(fileRef);}

return saveAsFile();
}
////////////////////////////////////
boolean saveAsFile()
{
File temp=null;
chooser.setDialogTitle("Save As...");
chooser.setApproveButtonText("Save Now"); 
chooser.setApproveButtonMnemonic(KeyEvent.VK_S);
chooser.setApproveButtonToolTipText("Click me to save!");

do
{
if(chooser.showSaveDialog(this.npd.f)!=JFileChooser.APPROVE_OPTION)
	return false;
temp=chooser.getSelectedFile();
if(!temp.exists()) break;
if(   JOptionPane.showConfirmDialog(
	this.npd.f,"<html>"+temp.getPath()+" already exists.<br>Do you want to replace it?<html>",
	"Save As",JOptionPane.YES_NO_OPTION
				)==JOptionPane.YES_OPTION)
	break;
}while(true);


return saveFile(temp);
}

////////////////////////
boolean openFile(File temp)
{
FileInputStream fin=null;
BufferedReader din=null;

try
{
fin=new FileInputStream(temp);
din=new BufferedReader(new InputStreamReader(fin));
String str=" ";
while(str!=null)
{
str=din.readLine();
if(str==null)
break;
this.npd.ta.append(str+"\n");
}

}
catch(IOException ioe){updateStatus(temp,false);return false;}
finally
{try{din.close();fin.close();}catch(IOException excp){}}
updateStatus(temp,true);
this.npd.ta.setCaretPosition(0);
return true;
}
///////////////////////
void openFile()
{
if(!confirmSave()) return;
chooser.setDialogTitle("Open File...");
chooser.setApproveButtonText("Open this"); 
chooser.setApproveButtonMnemonic(KeyEvent.VK_O);
chooser.setApproveButtonToolTipText("Click me to open the selected file.!");

File temp=null;
do
{
if(chooser.showOpenDialog(this.npd.f)!=JFileChooser.APPROVE_OPTION)
	return;
temp=chooser.getSelectedFile();

if(temp.exists())	break;

JOptionPane.showMessageDialog(this.npd.f,
	"<html>"+temp.getName()+"<br>file not found.<br>"+
	"Please verify the correct file name was given.<html>",
	"Open",	JOptionPane.INFORMATION_MESSAGE);

} while(true);

this.npd.ta.setText("");

if(!openFile(temp))
	{
	fileName="Untitled"; saved=true; 
	this.npd.f.setTitle(fileName+" - "+applicationTitle);
	}
if(!temp.canWrite())
	newFileFlag=true;

}
////////////////////////
void updateStatus(File temp,boolean saved)
{
if(saved)
{
this.saved=true;
fileName=new String(temp.getName());
if(!temp.canWrite())
	{fileName+="(Read only)"; newFileFlag=true;}
fileRef=temp;
npd.f.setTitle(fileName + " - "+applicationTitle);
npd.statusBar.setText("File : "+temp.getPath()+" saved/opened successfully.");
newFileFlag=false;
}
else
{
npd.statusBar.setText("Failed to save/open : "+temp.getPath());
}
}
///////////////////////
boolean confirmSave()
{
String strMsg="<html>The text in the "+fileName+" file has been changed.<br>"+
	"Do you want to save the changes?<html>";
if(!saved)
{
int x=JOptionPane.showConfirmDialog(this.npd.f,strMsg,applicationTitle,JOptionPane.YES_NO_CANCEL_OPTION);

if(x==JOptionPane.CANCEL_OPTION) return false;
if(x==JOptionPane.YES_OPTION && !saveAsFile()) return false;
}
return true;
}
///////////////////////////////////////
void newFile()
{
if(!confirmSave()) return;

this.npd.ta.setText("");
fileName=new String("Untitled");
fileRef=new File(fileName);
saved=true;
newFileFlag=true;
this.npd.f.setTitle(fileName+" - "+applicationTitle);
}
//////////////////////////////////////
}// end defination of class FileOperation
/************************************/
public class Notepad  implements ActionListener, MenuConstants
{

JFrame f;
JTextArea ta;
JLabel statusBar;

private String fileName="Untitled";
private boolean saved=true;
String applicationName="Javapad";

String searchString, replaceString;
int lastSearchIndex;

FileOperation fileHandler;
FontChooser fontDialog=null;
FindDialog findReplaceDialog=null; 
JColorChooser bcolorChooser=null;
JColorChooser fcolorChooser=null;
JDialog backgroundDialog=null;
JDialog foregroundDialog=null;
JMenuItem cutItem,copyItem, deleteItem, findItem, findNextItem, replaceItem, gotoItem, selectAllItem;
/****************************/
Notepad()
{
f=new JFrame(fileName+" - "+applicationName);
ta=new JTextArea(30,60);
statusBar=new JLabel("||       Ln 1, Col 1  ",JLabel.RIGHT);
f.add(new JScrollPane(ta),BorderLayout.CENTER);
f.add(statusBar,BorderLayout.SOUTH);
f.add(new JLabel("  "),BorderLayout.EAST);
f.add(new JLabel("  "),BorderLayout.WEST);
createMenuBar(f);
//f.setSize(350,350);
f.pack();
f.setLocation(100,50);
f.setVisible(true);
f.setLocation(150,50);
f.setDefaultCloseOperation(JFrame.DO_NOTHING_ON_CLOSE);

fileHandler=new FileOperation(this);

/////////////////////

ta.addCaretListener(
new CaretListener()
{
public void caretUpdate(CaretEvent e)
{
int lineNumber=0, column=0, pos=0;

try
{
pos=ta.getCaretPosition();
lineNumber=ta.getLineOfOffset(pos);
column=pos-ta.getLineStartOffset(lineNumber);
}catch(Exception excp){}
if(ta.getText().length()==0){lineNumber=0; column=0;}
statusBar.setText("||       Ln "+(lineNumber+1)+", Col "+(column+1));
}
});
//////////////////
DocumentListener myListener = new DocumentListener()
{
public void changedUpdate(DocumentEvent e){fileHandler.saved=false;}
public void removeUpdate(DocumentEvent e){fileHandler.saved=false;}
public void insertUpdate(DocumentEvent e){fileHandler.saved=false;}
};
ta.getDocument().addDocumentListener(myListener);
/////////
WindowListener frameClose=new WindowAdapter()
{
public void windowClosing(WindowEvent we)
{
if(fileHandler.confirmSave())System.exit(0);
}
};
f.addWindowListener(frameClose);
//////////////////
/*
ta.append("Hello dear hello hi");
ta.append("\nwho are u dear mister hello");
ta.append("\nhello bye hel");
ta.append("\nHello");
ta.append("\nMiss u mister hello hell");
fileHandler.saved=true;
*/
}
////////////////////////////////////
void goTo()
{
int lineNumber=0;
try
{
lineNumber=ta.getLineOfOffset(ta.getCaretPosition())+1;
String tempStr=JOptionPane.showInputDialog(f,"Enter Line Number:",""+lineNumber);
if(tempStr==null)
	{return;}
lineNumber=Integer.parseInt(tempStr);
ta.setCaretPosition(ta.getLineStartOffset(lineNumber-1));
}catch(Exception e){}
}
///////////////////////////////////
public void actionPerformed(ActionEvent ev)
{
String cmdText=ev.getActionCommand();
////////////////////////////////////
if(cmdText.equals(fileNew))
	fileHandler.newFile();
else if(cmdText.equals(fileOpen))
	fileHandler.openFile();
////////////////////////////////////
else if(cmdText.equals(fileSave))
	fileHandler.saveThisFile();
////////////////////////////////////
else if(cmdText.equals(fileSaveAs))
	fileHandler.saveAsFile();
////////////////////////////////////
else if(cmdText.equals(fileExit))
	{if(fileHandler.confirmSave())System.exit(0);}
////////////////////////////////////
else if(cmdText.equals(filePrint))
JOptionPane.showMessageDialog(
	Notepad.this.f,
	"Get ur printer repaired first! It seems u dont have one!",
	"Bad Printer",
	JOptionPane.INFORMATION_MESSAGE
	);
////////////////////////////////////
else if(cmdText.equals(editCut))
	ta.cut();
////////////////////////////////////
else if(cmdText.equals(editCopy))
	ta.copy();
////////////////////////////////////
else if(cmdText.equals(editPaste))
	ta.paste();
////////////////////////////////////
else if(cmdText.equals(editDelete))
	ta.replaceSelection("");
////////////////////////////////////
else if(cmdText.equals(editFind))
{
if(Notepad.this.ta.getText().length()==0)
	return;	// text box have no text
if(findReplaceDialog==null)
	findReplaceDialog=new FindDialog(Notepad.this.ta);
findReplaceDialog.showDialog(Notepad.this.f,true);//find
}
////////////////////////////////////
else if(cmdText.equals(editFindNext))
{
if(Notepad.this.ta.getText().length()==0)
	return;	// text box have no text

if(findReplaceDialog==null)
	statusBar.setText("Nothing to search for, use Find option of Edit Menu first !!!!");
else
	findReplaceDialog.findNextWithSelection();
}
////////////////////////////////////
else if(cmdText.equals(editReplace))
{
if(Notepad.this.ta.getText().length()==0)
	return;	// text box have no text

if(findReplaceDialog==null)
	findReplaceDialog=new FindDialog(Notepad.this.ta);
findReplaceDialog.showDialog(Notepad.this.f,false);//replace
}
////////////////////////////////////
else if(cmdText.equals(editGoTo))
{
if(Notepad.this.ta.getText().length()==0)
	return;	// text box have no text
goTo();
}
////////////////////////////////////
else if(cmdText.equals(editSelectAll))
	ta.selectAll();
////////////////////////////////////
else if(cmdText.equals(editTimeDate))
	ta.insert(new Date().toString(),ta.getSelectionStart());
////////////////////////////////////
else if(cmdText.equals(formatWordWrap))
{
JCheckBoxMenuItem temp=(JCheckBoxMenuItem)ev.getSource();
ta.setLineWrap(temp.isSelected());
}
////////////////////////////////////
else if(cmdText.equals(formatFont))
{
if(fontDialog==null)
	fontDialog=new FontChooser(ta.getFont());

if(fontDialog.showDialog(Notepad.this.f,"Choose a font"))
	Notepad.this.ta.setFont(fontDialog.createFont());
}
////////////////////////////////////
else if(cmdText.equals(formatForeground))
	showForegroundColorDialog();
////////////////////////////////////
else if(cmdText.equals(formatBackground))
	showBackgroundColorDialog();
////////////////////////////////////

else if(cmdText.equals(viewStatusBar))
{
JCheckBoxMenuItem temp=(JCheckBoxMenuItem)ev.getSource();
statusBar.setVisible(temp.isSelected());
}
////////////////////////////////////
else if(cmdText.equals(helpAboutNotepad))
{
JOptionPane.showMessageDialog(Notepad.this.f,aboutText,"Dedicated 2 u!",JOptionPane.INFORMATION_MESSAGE);
}
else
	statusBar.setText("This "+cmdText+" command is yet to be implemented");
}//action Performed
////////////////////////////////////
void showBackgroundColorDialog()
{
if(bcolorChooser==null)
	bcolorChooser=new JColorChooser();
if(backgroundDialog==null)
	backgroundDialog=JColorChooser.createDialog
		(Notepad.this.f,
		formatBackground,
		false,
		bcolorChooser,
		new ActionListener()
		{public void actionPerformed(ActionEvent evvv){
			Notepad.this.ta.setBackground(bcolorChooser.getColor());}},
		null);		

backgroundDialog.setVisible(true);
}
////////////////////////////////////
void showForegroundColorDialog()
{
if(fcolorChooser==null)
	fcolorChooser=new JColorChooser();
if(foregroundDialog==null)
	foregroundDialog=JColorChooser.createDialog
		(Notepad.this.f,
		formatForeground,
		false,
		fcolorChooser,
		new ActionListener()
		{public void actionPerformed(ActionEvent evvv){
			Notepad.this.ta.setForeground(fcolorChooser.getColor());}},
		null);		

foregroundDialog.setVisible(true);
}

///////////////////////////////////
JMenuItem createMenuItem(String s, int key,JMenu toMenu,ActionListener al)
{
JMenuItem temp=new JMenuItem(s,key);
temp.addActionListener(al);
toMenu.add(temp);

return temp;
}
////////////////////////////////////
JMenuItem createMenuItem(String s, int key,JMenu toMenu,int aclKey,ActionListener al)
{
JMenuItem temp=new JMenuItem(s,key);
temp.addActionListener(al);
temp.setAccelerator(KeyStroke.getKeyStroke(aclKey,ActionEvent.CTRL_MASK));
toMenu.add(temp);

return temp;
}
////////////////////////////////////
JCheckBoxMenuItem createCheckBoxMenuItem(String s, int key,JMenu toMenu,ActionListener al)
{
JCheckBoxMenuItem temp=new JCheckBoxMenuItem(s);
temp.setMnemonic(key);
temp.addActionListener(al);
temp.setSelected(false);
toMenu.add(temp);

return temp;
}
////////////////////////////////////
JMenu createMenu(String s,int key,JMenuBar toMenuBar)
{
JMenu temp=new JMenu(s);
temp.setMnemonic(key);
toMenuBar.add(temp);
return temp;
}
/*********************************/
void createMenuBar(JFrame f)
{
JMenuBar mb=new JMenuBar();
JMenuItem temp;

JMenu fileMenu=createMenu(fileText,KeyEvent.VK_F,mb);
JMenu editMenu=createMenu(editText,KeyEvent.VK_E,mb);
JMenu formatMenu=createMenu(formatText,KeyEvent.VK_O,mb);
JMenu viewMenu=createMenu(viewText,KeyEvent.VK_V,mb);
JMenu helpMenu=createMenu(helpText,KeyEvent.VK_H,mb);

createMenuItem(fileNew,KeyEvent.VK_N,fileMenu,KeyEvent.VK_N,this);
createMenuItem(fileOpen,KeyEvent.VK_O,fileMenu,KeyEvent.VK_O,this);
createMenuItem(fileSave,KeyEvent.VK_S,fileMenu,KeyEvent.VK_S,this);
createMenuItem(fileSaveAs,KeyEvent.VK_A,fileMenu,this);
fileMenu.addSeparator();
temp=createMenuItem(filePageSetup,KeyEvent.VK_U,fileMenu,this);
temp.setEnabled(false);
createMenuItem(filePrint,KeyEvent.VK_P,fileMenu,KeyEvent.VK_P,this);
fileMenu.addSeparator();
createMenuItem(fileExit,KeyEvent.VK_X,fileMenu,this);

temp=createMenuItem(editUndo,KeyEvent.VK_U,editMenu,KeyEvent.VK_Z,this);
temp.setEnabled(false);
editMenu.addSeparator();
cutItem=createMenuItem(editCut,KeyEvent.VK_T,editMenu,KeyEvent.VK_X,this);
copyItem=createMenuItem(editCopy,KeyEvent.VK_C,editMenu,KeyEvent.VK_C,this);
createMenuItem(editPaste,KeyEvent.VK_P,editMenu,KeyEvent.VK_V,this);
deleteItem=createMenuItem(editDelete,KeyEvent.VK_L,editMenu,this);
deleteItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_DELETE,0));
editMenu.addSeparator();
findItem=createMenuItem(editFind,KeyEvent.VK_F,editMenu,KeyEvent.VK_F,this);
findNextItem=createMenuItem(editFindNext,KeyEvent.VK_N,editMenu,this);
findNextItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_F3,0));
replaceItem=createMenuItem(editReplace,KeyEvent.VK_R,editMenu,KeyEvent.VK_H,this);
gotoItem=createMenuItem(editGoTo,KeyEvent.VK_G,editMenu,KeyEvent.VK_G,this);
editMenu.addSeparator();
selectAllItem=createMenuItem(editSelectAll,KeyEvent.VK_A,editMenu,KeyEvent.VK_A,this);
createMenuItem(editTimeDate,KeyEvent.VK_D,editMenu,this).setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_F5,0));

createCheckBoxMenuItem(formatWordWrap,KeyEvent.VK_W,formatMenu,this);

createMenuItem(formatFont,KeyEvent.VK_F,formatMenu,this);
formatMenu.addSeparator();
createMenuItem(formatForeground,KeyEvent.VK_T,formatMenu,this);
createMenuItem(formatBackground,KeyEvent.VK_P,formatMenu,this);

createCheckBoxMenuItem(viewStatusBar,KeyEvent.VK_S,viewMenu,this).setSelected(true);
/************For Look and Feel, May not work properly on different operating environment***/
LookAndFeelMenu.createLookAndFeelMenuItem(viewMenu,this.f);


temp=createMenuItem(helpHelpTopic,KeyEvent.VK_H,helpMenu,this);
temp.setEnabled(false);
helpMenu.addSeparator();
createMenuItem(helpAboutNotepad,KeyEvent.VK_A,helpMenu,this);

MenuListener editMenuListener=new MenuListener()
{
   public void menuSelected(MenuEvent evvvv)
	{
	if(Notepad.this.ta.getText().length()==0)
	{
	findItem.setEnabled(false);
	findNextItem.setEnabled(false);
	replaceItem.setEnabled(false);
	selectAllItem.setEnabled(false);
	gotoItem.setEnabled(false);
	}
	else
	{
	findItem.setEnabled(true);
	findNextItem.setEnabled(true);
	replaceItem.setEnabled(true);
	selectAllItem.setEnabled(true);
	gotoItem.setEnabled(true);
	}
	if(Notepad.this.ta.getSelectionStart()==ta.getSelectionEnd())
	{
	cutItem.setEnabled(false);
	copyItem.setEnabled(false);
	deleteItem.setEnabled(false);
	}
	else
	{
	cutItem.setEnabled(true);
	copyItem.setEnabled(true);
	deleteItem.setEnabled(true);
	}
	}
   public void menuDeselected(MenuEvent evvvv){}
   public void menuCanceled(MenuEvent evvvv){}
};
editMenu.addMenuListener(editMenuListener);
f.setJMenuBar(mb);
}
/*************Constructor**************/
////////////////////////////////////
public static void main(String[] s)
{
new Notepad();
}
}
/**************************************/
//public
interface MenuConstants
{
final String fileText="File";
final String editText="Edit";
final String formatText="Format";
final String viewText="View";
final String helpText="Help";

final String fileNew="New";
final String fileOpen="Open...";
final String fileSave="Save";
final String fileSaveAs="Save As...";
final String filePageSetup="Page Setup...";
final String filePrint="Print";
final String fileExit="Exit";

final String editUndo="Undo";
final String editCut="Cut";
final String editCopy="Copy";
final String editPaste="Paste";
final String editDelete="Delete";
final String editFind="Find...";
final String editFindNext="Find Next";
final String editReplace="Replace";
final String editGoTo="Go To...";
final String editSelectAll="Select All";
final String editTimeDate="Time/Date";

final String formatWordWrap="Word Wrap";
final String formatFont="Font...";
final String formatForeground="Set Text color...";
final String formatBackground="Set Pad color...";

final String viewStatusBar="Status Bar";

final String helpHelpTopic="Help Topic";
final String helpAboutNotepad="About Javapad";

final String aboutText=
	"<html><big>Your Javapad</big><hr><hr>"
	+"<p align=right>Prepared by a JavaTpoint!"
	+"<hr><p align=left>I Used jdk1.5 to compile the source code.<br><br>"
	+"<strong>Thanx for using Javapad</strong><br>"
	+"Ur Comments as well as bug reports r very welcome at<p align=center>"
	+"<hr><em><big>hr@javatpoint.com</big></em><hr><html>";
}

Online Test Module


/*Online Java Paper Test*/

import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

class OnlineTest extends JFrame implements ActionListener
{
	JLabel l;
	JRadioButton jb[]=new JRadioButton[5];
	JButton b1,b2;
	ButtonGroup bg;
	int count=0,current=0,x=1,y=1,now=0;
	int m[]=new int[10];	
	OnlineTest(String s)
	{
		super(s);
		l=new JLabel();
		add(l);
		bg=new ButtonGroup();
		for(int i=0;i<5;i++)
		{
			jb[i]=new JRadioButton();	
			add(jb[i]);
			bg.add(jb[i]);
		}
		b1=new JButton("Next");
		b2=new JButton("Bookmark");
		b1.addActionListener(this);
		b2.addActionListener(this);
		add(b1);add(b2);
		set();
		l.setBounds(30,40,450,20);
		jb[0].setBounds(50,80,100,20);
		jb[1].setBounds(50,110,100,20);
		jb[2].setBounds(50,140,100,20);
		jb[3].setBounds(50,170,100,20);
		b1.setBounds(100,240,100,30);
		b2.setBounds(270,240,100,30);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setLayout(null);
		setLocation(250,100);
		setVisible(true);
		setSize(600,350);
	}
	public void actionPerformed(ActionEvent e)
	{
		if(e.getSource()==b1)
		{
			if(check())
				count=count+1;
			current++;
			set();	
			if(current==9)
			{
				b1.setEnabled(false);
				b2.setText("Result");
			}
		}
		if(e.getActionCommand().equals("Bookmark"))
		{
			JButton bk=new JButton("Bookmark"+x);
			bk.setBounds(480,20+30*x,100,30);
			add(bk);
			bk.addActionListener(this);
			m[x]=current;
			x++;
			current++;
			set();	
			if(current==9)
				b2.setText("Result");
			setVisible(false);
			setVisible(true);
		}
		for(int i=0,y=1;i<x;i++,y++)
		{
		if(e.getActionCommand().equals("Bookmark"+y))
		{
			if(check())
				count=count+1;
			now=current;
			current=m[y];
			set();
			((JButton)e.getSource()).setEnabled(false);
			current=now;
		}
		}
	
		if(e.getActionCommand().equals("Result"))
		{
			if(check())
				count=count+1;
			current++;
			//System.out.println("correct ans="+count);
			JOptionPane.showMessageDialog(this,"Correct answers: "+count);
			System.exit(0);
		}
	}
	void set()
	{
		jb[4].setSelected(true);
		if(current==0)
		{
			l.setText("Que1: Which one among these is not a primitive datatype?");
			jb[0].setText("int");jb[1].setText("Float");jb[2].setText("boolean");jb[3].setText("char");	
		}
		if(current==1)
		{
			l.setText("Que2: Which class is the parent class of all classes in java?");
			jb[0].setText("Swing");jb[1].setText("Applet");jb[2].setText("Object");jb[3].setText("ActionEvent");
		}
		if(current==2)
		{
			l.setText("Que3: Which package is directly available to our classes?");
			jb[0].setText("swing");jb[1].setText("applet");jb[2].setText("net");jb[3].setText("lang");
		}
		if(current==3)
		{
			l.setText("Que4: String class is defined in ___ package.");
			jb[0].setText("lang");jb[1].setText("Swing");jb[2].setText("Applet");jb[3].setText("awt");
		}
		if(current==4)
		{
			l.setText("Que5: Which institute is best for java coaching?");
			jb[0].setText("Utek");jb[1].setText("Aptech");jb[2].setText("JavaTpoint");jb[3].setText("jtek");
		}
		if(current==5)
		{
			l.setText("Que6: Which one among these is not a keyword?");
			jb[0].setText("class");jb[1].setText("int");jb[2].setText("get");jb[3].setText("if");
		}
		if(current==6)
		{
			l.setText("Que7: Which one among these is not a class?");
			jb[0].setText("Applet");jb[1].setText("Actionperformed");jb[2].setText("ActionEvent");jb[3].setText("Button");
		}
		if(current==7)
		{
			l.setText("Que8: Which among these is not a function of Object class?");
			jb[0].setText("toString");jb[1].setText("finalize");jb[2].setText("equals");jb[3].setText("getDocumentBase");		
		}
		if(current==8)
		{
			l.setText("Que9: Which function is not found in Applet class?");
			jb[0].setText("init");jb[1].setText("main");jb[2].setText("start");jb[3].setText("destroy");
		}
		if(current==9)
		{
			l.setText("Que10: Which one among these is not a valid component?");
			jb[0].setText("JButton");jb[1].setText("JList");jb[2].setText("JButtonGroup");jb[3].setText("JTextArea");
		}
		l.setBounds(30,40,450,20);
		for(int i=0,j=0;i<=90;i+=30,j++)
			jb[j].setBounds(50,80+i,200,20);
	}
	boolean check()
	{
		if(current==0)
			return(jb[1].isSelected());
		if(current==1)
			return(jb[2].isSelected());
		if(current==2)
			return(jb[3].isSelected());
		if(current==3)
			return(jb[0].isSelected());
		if(current==4)
			return(jb[2].isSelected());
		if(current==5)
			return(jb[2].isSelected());
		if(current==6)
			return(jb[1].isSelected());
		if(current==7)
			return(jb[3].isSelected());
		if(current==8)
			return(jb[1].isSelected());
		if(current==9)
			return(jb[2].isSelected());
		return false;
	}
	public static void main(String s[])
	{
		new OnlineTest("Online Test Of Java");
	}


}


Puzzle code



import java.awt.event.*;
import java.awt.*;
import javax.swing.*;
class picpuzzle2 extends JFrame implements ActionListener{
JButton b1,b2,b3,b4,b5,b6,b7,b8,b9,sample,starB;
Icon star;
Icon ic0=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/starB0.jpg"));
Icon ic10=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/starB10.jpg"));
Icon ic20=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/starB20.jpg"));
Icon samicon1=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/main.jpg"));
Icon samicon2=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/main2.jpg"));
Icon samicon3=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/main3.jpg"));
Icon ic1=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/1.jpg"));
Icon ic2=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/5.jpg"));
Icon ic3=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/2.jpg"));
Icon ic4=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/7.jpg"));
Icon ic5=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/4.jpg"));
Icon ic6=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/6.jpg"));
Icon ic7=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/8.jpg"));
Icon ic8=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/9.jpg"));
Icon ic9=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/3.jpg"));

Icon ic11=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/12.jpg"));
Icon ic12=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/13.jpg"));
Icon ic13=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/16.jpg"));
Icon ic14=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/11.jpg"));
Icon ic15=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/14.jpg"));
Icon ic16=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/19.jpg"));
Icon ic17=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/17.jpg"));
Icon ic18=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/15.jpg"));
Icon ic19=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/18.jpg"));

Icon ic21=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/24.jpg"));
Icon ic22=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/25.jpg"));
Icon ic23=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/21.jpg"));
Icon ic24=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/27.jpg"));
Icon ic25=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/23.jpg"));
Icon ic26=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/29.jpg"));
Icon ic27=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/28.jpg"));
Icon ic28=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/22.jpg"));
Icon ic29=new ImageIcon(JApps.class.getResource("/com/javatpoint/pic/26.jpg"));

picpuzzle2(){

super("Picture Puzzle");

b1=new JButton(ic1);
b1.setBounds(10,80,100,100);
b2=new JButton(ic2);
b2.setBounds(110,80,100,100);
b3=new JButton(ic3);
b3.setBounds(210,80,100,100);
b4=new JButton(ic4);
b4.setBounds(10,180,100,100);
b5=new JButton(ic5);
b5.setBounds(110,180,100,100);
b6=new JButton(ic6);
b6.setBounds(210,180,100,100);
b7=new JButton(ic7);
b7.setBounds(10,280,100,100);
b8=new JButton(ic8);
b8.setBounds(110,280,100,100);
b9=new JButton(ic9);
b9.setBounds(210,280,100,100);
sample=new JButton(samicon1);
sample.setBounds(380,100,200,200);

JLabel l1=new JLabel("Sample:");
l1.setBounds(330,200,70,20);
JLabel l2=new JLabel("NOTE:: icon has power to swap with neighbour icon=>");
l2.setBounds(5,15,500,20);
JLabel l3=new JLabel("click sample picture to next puzzle");
l3.setBounds(380,320,200,20);
l3.setForeground(Color.red);

starB=new JButton(ic0);
starB.setBounds(330,5,50,50);
star=b9.getIcon();

add(b1);add(b2);add(b3);add(b4);add(b5);add(b6);add(b7);add(b8);add(b9);add(sample);add(l1);add(l2);add(starB);add(l3);
b1.addActionListener(this); b2.addActionListener(this); b3.addActionListener(this); b4.addActionListener(this); b5.addActionListener(this); b6.addActionListener(this); b7.addActionListener(this); b8.addActionListener(this); b9.addActionListener(this); 
sample.addActionListener(this);
setLayout(null);
setSize(600,500);
setVisible(true);
setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
}

public void actionPerformed(ActionEvent e){
if(e.getSource()==b1){
    Icon s1=b1.getIcon();
      if(b2.getIcon()==star){
        b2.setIcon(s1);
        b1.setIcon(star);
      } else if(b4.getIcon()==star){
                    b4.setIcon(s1);
                    b1.setIcon(star);
                   }
  }//end of if

if(e.getSource()==b2){
    Icon s1=b2.getIcon();
      if(b1.getIcon()==star){
        b1.setIcon(s1);
        b2.setIcon(star);
      } else if(b5.getIcon()==star){
                    b5.setIcon(s1);
                    b2.setIcon(star);
                   }
         else if(b3.getIcon()==star){
                    b3.setIcon(s1);
                    b2.setIcon(star);
                   }
  }//end of if

if(e.getSource()==b3){
    Icon s1=b3.getIcon();
      if(b2.getIcon()==star){
        b2.setIcon(s1);
        b3.setIcon(star);
      } else if(b6.getIcon()==star){
                    b6.setIcon(s1);
                    b3.setIcon(star);
                   }
  }//end of if

if(e.getSource()==b4){
    Icon s1=b4.getIcon();
      if(b1.getIcon()==star){
        b1.setIcon(s1);
        b4.setIcon(star);
      } else if(b5.getIcon()==star){
                    b5.setIcon(s1);
                    b4.setIcon(star);
                   }
         else if(b7.getIcon()==star){
                    b7.setIcon(s1);
                    b4.setIcon(star);
                   }
  }//end of if

if(e.getSource()==b5){
    Icon s1=b5.getIcon();
      if(b2.getIcon()==star){
        b2.setIcon(s1);
        b5.setIcon(star);
      } else if(b4.getIcon()==star){
                    b4.setIcon(s1);
                    b5.setIcon(star);
                   }
         else if(b6.getIcon()==star){
                    b6.setIcon(s1);
                    b5.setIcon(star);
                   }
          else if(b8.getIcon()==star){
                    b8.setIcon(s1);
                    b5.setIcon(star);
                   }
  }//end of if

if(e.getSource()==b6){
    Icon s1=b6.getIcon();
      if(b3.getIcon()==star){
        b3.setIcon(s1);
        b6.setIcon(star);
      } else if(b5.getIcon()==star){
                    b5.setIcon(s1);
                    b6.setIcon(star);
                   }
         else if(b9.getIcon()==star){
                    b9.setIcon(s1);
                    b6.setIcon(star);
                   }
}//end of if

if(e.getSource()==b7){
    Icon s1=b7.getIcon();
      if(b4.getIcon()==star){
        b4.setIcon(s1);
        b7.setIcon(star);
      } else if(b8.getIcon()==star){
                    b8.setIcon(s1);
                    b7.setIcon(star);
                   }
 }//end of if

   if(e.getSource()==b8){
    Icon s1=b8.getIcon();
      if(b7.getIcon()==star){
        b7.setIcon(s1);
        b8.setIcon(star);
      } else if(b5.getIcon()==star){
                    b5.setIcon(s1);
                    b8.setIcon(star);
                   }
         else if(b9.getIcon()==star){
                    b9.setIcon(s1);
                    b8.setIcon(star);
                   }

  }//end of if

 if(e.getSource()==b9){
    Icon s1=b9.getIcon();
      if(b8.getIcon()==star){
        b8.setIcon(s1);
        b9.setIcon(star);
      } else if(b6.getIcon()==star){
                    b6.setIcon(s1);
                    b9.setIcon(star);
                   }
  }//end of if

if(e.getSource()==sample){
Icon s1=sample.getIcon();
 if(s1==samicon3){
sample.setIcon(samicon1);
b1.setIcon(ic1);
b2.setIcon(ic2);
b3.setIcon(ic3);
b4.setIcon(ic4);
b5.setIcon(ic5);
b6.setIcon(ic6);
b7.setIcon(ic7);
b8.setIcon(ic8);
b9.setIcon(ic9);
star=b9.getIcon();
starB.setIcon(ic0);
}//eof if
else if(s1==samicon1){
sample.setIcon(samicon2);
b1.setIcon(ic11);
b2.setIcon(ic12);
b3.setIcon(ic13);
b4.setIcon(ic14);
b5.setIcon(ic15);
b6.setIcon(ic16);
b7.setIcon(ic17);
b8.setIcon(ic18);
b9.setIcon(ic19);
star=b6.getIcon();
starB.setIcon(ic10);
}//eof else
else{
sample.setIcon(samicon3);
b1.setIcon(ic21);
b2.setIcon(ic22);
b3.setIcon(ic23);
b4.setIcon(ic24);
b5.setIcon(ic25);
b6.setIcon(ic26);
b7.setIcon(ic27);
b8.setIcon(ic28);
b9.setIcon(ic29);
star=b6.getIcon();
starB.setIcon(ic20);
}//eof else

}
}//end of actionPerformed

public static void main(String args[]){
new picpuzzle2();
}//end of main
}//end of class

Tic Tac Toe
Module



import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
class TTT1 extends JFrame implements ItemListener, ActionListener{
int i,j,ii,jj,x,y,yesnull; 
int a[][]={{10,1,2,3,11},{10,1,4,7,11},{10,1,5,9,11},{10,2,5,8,11},
                {10,3,5,7,11},{10,3,6,9,11},{10,4,5,6,11},{10,7,8,9,11} };
int a1[][]={{10,1,2,3,11},{10,1,4,7,11},{10,1,5,9,11},{10,2,5,8,11},
                {10,3,5,7,11},{10,3,6,9,11},{10,4,5,6,11},{10,7,8,9,11} };
				
boolean state,type,set;

Icon ic1,ic2,icon,ic11,ic22;
Checkbox c1,c2;
JLabel l1,l2;
JButton b[]=new JButton[9];
JButton reset;

public void showButton(){

x=10; y=10;j=0;
for(i=0;i<=8;i++,x+=100,j++){
 b[i]=new JButton();
if(j==3)
{j=0; y+=100; x=10;}
 b[i].setBounds(x,y,100,100);
add(b[i]);
b[i].addActionListener(this);
}//eof for

reset=new JButton("RESET");
reset.setBounds(100,350,100,50);
add(reset);
reset.addActionListener(this);

}//eof showButton

/*********************************************************/
public  void check(int num1){
for(ii=0;ii<=7;ii++){
   for(jj=1;jj<=3;jj++){
        if(a[ii][jj]==num1){ a[ii][4]=11;  }

   }//eof for jj

}//eof for ii
}//eof check
/**********************************************************/

/*********************************************************/

public void complogic(int num){

 for(i=0;i<=7;i++){
   for(j=1;j<=3;j++){
      if(a[i][j]==num){  a[i][0]=11; a[i][4]=10;    }
	  }
  }
   for(i=0;i<=7;i++){                                // for 1
     set=true;  		   
   if(a[i][4]==10){                                 //if 1 
       int count=0;
       for(j=1;j<=3;j++){                                                //for 2 
           if(b[(a[i][j]-1)].getIcon()!=null){                               //if 2
             count++;
               }                                                                   //eof if 2
            else{ yesnull=a[i][j]; }
        }                                                                         //eof for 2
      if(count==2){                                                        //if 2
         b[yesnull-1].setIcon(ic2); 
         this.check(yesnull); set=false;break;
         }                                                                     //eof if 2
      }                                                                     //eof if 1
      else
	  if(a[i][0]==10){
                for(j=1;j<=3;j++){                                            //for2
                    if(b[(a[i][j]-1)].getIcon()==null){                                          //if 1
                      b[(a[i][j]-1)].setIcon(ic2);
                        this.check(a[i][j]);
                         set=false;
						 break;
                    }                                                    //eof if1
                }                                                              //eof for 2
                if(set==false)
                      break;                                                       
            }//eof elseif

    if(set==false)
         break;    
 }//eof for 1


}//eof complogic


/*********************************************************/

TTT1(){
super("Tic tac toe");

CheckboxGroup cbg=new CheckboxGroup();
c1=new Checkbox("vs computer",cbg,false);
c2=new Checkbox("vs friend",cbg,false);
c1.setBounds(120,80,100,40);
c2.setBounds(120,150,100,40);
add(c1); add(c2);
c1.addItemListener(this);
c2.addItemListener(this);


state=true;type=true;set=true;
ic1=new ImageIcon(JApps.class.getResource("/com/javatpoint/ic1.jpg"));
ic2=new ImageIcon(JApps.class.getResource("/com/javatpoint/ic2.jpg"));
ic11=new ImageIcon(JApps.class.getResource("/com/javatpoint/ic11.JPG"));
ic22=new ImageIcon(JApps.class.getResource("/com/javatpoint/ic22.JPG"));

setLayout(null);
setSize(330,450);
setVisible(true);
setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);
}//eof constructor

/*************************************************************/
public void itemStateChanged(ItemEvent e){
 if(c1.getState())
  { 
 type=false;
 }

 else if(c2.getState())
  { type=true;
  }
remove(c1);remove(c2);
 repaint(0,0,330,450);
 showButton();
}//eof itemstate
/************************************************************/

public void actionPerformed(ActionEvent e){
/********************************/
if(type==true)//logicfriend
{
if(e.getSource()==reset){
 for(i=0;i<=8;i++){
   b[i].setIcon(null);
  }//eof for  
}
else{ 
  for(i=0;i<=8;i++){
      if(e.getSource()==b[i]){
       
           if(b[i].getIcon()==null){
              if(state==true){ icon=ic2;         
               state=false;} else{ icon=ic1; state=true; }
            b[i].setIcon(icon);
            }
       } 
  }//eof for
}//eof else
}//eof logicfriend
else if(type==false){                                     //  complogic
      if(e.getSource()==reset){
          for(i=0;i<=8;i++){
            b[i].setIcon(null);
          }//eof for 
       for(i=0;i<=7;i++)
        for(j=0;j<=4;j++)
		a[i][j]=a1[i][j];   //again initialsing array
        }
        else{  //complogic
            for(i=0;i<=8;i++){
               if(e.getSource()==b[i]){
                  if(b[i].getIcon()==null){ 
                           b[i].setIcon(ic1);  
                            if(b[4].getIcon()==null){
						      b[4].setIcon(ic2);
							  this.check(5);
							  } else{
						         this.complogic(i);
								 }
                    }
                 }
             }//eof for
        }
    }//eof complogic

for(i=0;i<=7;i++){
  
  Icon icon1=b[(a[i][1]-1)].getIcon();
  Icon icon2=b[(a[i][2]-1)].getIcon();
  Icon icon3=b[(a[i][3]-1)].getIcon();
     if((icon1==icon2)&&(icon2==icon3)&&(icon1!=null)){
               if(icon1==ic1){ 
                 b[(a[i][1]-1)].setIcon(ic11);
                 b[(a[i][2]-1)].setIcon(ic11); 
                 b[(a[i][3]-1)].setIcon(ic11);
	JOptionPane.showMessageDialog(TTT1.this,"You won! Click reset");			 break;
                   }
             else if(icon1==ic2){ 
             b[(a[i][1]-1)].setIcon(ic22);
             b[(a[i][2]-1)].setIcon(ic22);
             b[(a[i][3]-1)].setIcon(ic22); 
               JOptionPane.showMessageDialog(TTT1.this,"Computer won! Click reset");
                break;			 
               }
         }
    }  


}//eof actionperformed
/************************************************************/

public static void main(String []args){
new TTT1();
}//eof main
}//eof class

