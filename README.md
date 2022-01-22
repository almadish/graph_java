# Graph in Java
As my for this project, I created a canvas that plots a graph according to the mathematical equation. Values in the equation can be changed using the sliders.

import java.awt.Canvas;
import java.awt.Color;
import java.awt.EventQueue;
import java.awt.Graphics;

import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JSlider;
import javax.swing.event.ChangeEvent;
import javax.swing.event.ChangeListener;

public class Almadi {
	
	private double k;
	private double b;

	private JFrame frame;

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					Almadi window = new Almadi();
					window.frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}

	/**
	 * Create the application.
	 */
	public Almadi() {
		initialize();
		k=1;
		b=0;
	}

	/**
	 * Initialize the contents of the frame.
	 */
	private void initialize() {
		frame = new JFrame();
		frame.setBounds(100, 100, 500, 500);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		frame.getContentPane().setLayout(null);

		Canvas canvas = new Canvas();
		canvas.setBackground(Color.WHITE);
		canvas.setBounds(10, 10, 310, 310);
		frame.getContentPane().add(canvas);
		
		JLabel lblB = new JLabel("b= 0");
		JLabel lblM = new JLabel("k= 1");
		
		JSlider kSlider = new JSlider();
		kSlider.setPaintTicks(true);
		kSlider.setMinorTickSpacing(100);
		kSlider.setMaximum(400);
		kSlider.setMinimum(-400);
		kSlider.setValue(100);
		kSlider.addChangeListener(new ChangeListener() {
			public void stateChanged(ChangeEvent arg0) {
		
				k =kSlider.getValue();
				
				Graphics g =canvas.getGraphics();
				canvas.update(g);
			
				g.drawLine(0,canvas.getHeight()/2,canvas.getWidth(),canvas.getHeight()/2);
				g.drawLine(canvas.getWidth()/2,0, canvas.getWidth()/2, canvas.getHeight());
				
				
				g.translate(canvas.getWidth()/2, canvas.getHeight()/2);

				g.setColor(Color.red);

				double k2=k;
				double b2=b*10;
				
				lblM.setText("k= "+k2);
				
				double y=0;
				double y2=0;
				for(double x =-200;x<200;x++)
				{
					y=(k2/x)+b2;
					y2=(k2/(x+1))+b2;
					g.drawLine((int)x,(int) -y, (int)x,(int) -y2);
				}
			}
		});
		
		kSlider.setBounds(10, 329, 400, 23);
		frame.getContentPane().add(kSlider);
		
		JLabel lblYMxb = new JLabel("y= k/x+b");
		lblYMxb.setBounds(335, 10, 89, 14);
		frame.getContentPane().add(lblYMxb);
		
		
		lblM.setBounds(10, 363, 200, 14);
		frame.getContentPane().add(lblM);
		
		JSlider bSlider = new JSlider();
		bSlider.setValue(0);
		bSlider.setMajorTickSpacing(1);
		bSlider.setPaintTicks(true);
		bSlider.setMinimum(-10);
		bSlider.setMaximum(10);
		bSlider.setBounds(10, 388, 400, 23);
		frame.getContentPane().add(bSlider);
		
		bSlider.addChangeListener(new ChangeListener() {
			public void stateChanged(ChangeEvent arg0) {
				b=bSlider.getValue();
				
				Graphics g =canvas.getGraphics();
			
				canvas.update(g);
				
				g.drawLine(0,canvas.getHeight()/2,canvas.getWidth(),canvas.getHeight()/2);
				g.drawLine(canvas.getWidth()/2,0, canvas.getWidth()/2, canvas.getHeight());
				g.translate(canvas.getWidth()/2, canvas.getHeight()/2);

				g.setColor(Color.red);

				double k2=k;
				double b2=b*10;
				lblB.setText("b= "+b2);
				
				for(double x =-200, y=0,y2=0;x<200;x++)

				{
					
					y=(k2/x)+b2;
					y2=(k2/(x+1))+b2;
					g.drawLine((int)x,(int) -y, (int)x,(int) -y2);
				}
			}
		});
		
		
	
		lblB.setBounds(10, 422, 46, 14);
		frame.getContentPane().add(lblB);
	}

}
