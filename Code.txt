package game_environment;

import java.awt.Color;
import java.awt.Graphics;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;

import javax.swing.JFrame;
import javax.swing.JPanel;

public class Best2 extends JPanel implements KeyListener {
	/**
	 * 
	 */
	private static final long serialVersionUID = 1L;
	int x, y;
	int sqsize;
	int speed;
	Color building_a;
	Color building_b;
	private int i, j;

	public Best2(int N, int S) {
		addKeyListener(this);
		setFocusable(true);
		sqsize = N;
		speed = S;
		x = 0;
		y = 40;
		setBackground(new Color(255, 204, 153));
		building_a = new Color(102, 255, 255);
		building_b = new Color(255, 106, 77);
	}

	public void paintComponent(Graphics g) {
		boolean proceed = true;
		super.paintComponent(g);
		for (int i = 0; i <= 1520 / sqsize; i++) {
			for (int j = 0; j <= 820 / sqsize; j++) {
				g.setColor(g.getColor() == building_a ? building_b : building_a);// initially (by default) it is black
				g.fillRect(sqsize * i, sqsize * j, sqsize / 2, sqsize / 2);

			}

		}
		g.setColor(new Color(255, 230, 255));
		g.fillRect(x, y, sqsize / 4, sqsize / 4);
		// System.out.println("("+x+","+y+")");*
	}

	public static void main(String[] args) {
		Best2 obj = new Best2(80, 10);
		JFrame frame = new JFrame();
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		frame.setSize(1600, 900);
		frame.setVisible(true);
		frame.add(obj);
	}

	public void keyTyped(KeyEvent e) {
	}

	public void keyPressed(KeyEvent e) {
		// System.out.println(x+" "+y);
		if (e.getKeyCode() == KeyEvent.VK_W) {
			outer: for (i = 0; i <= 820; i++)
				if ((y == (sqsize * i + sqsize / 2)))
					for (j = 0; j <= 1520; j++)
						if ((x + 20) > sqsize * j && ((x) < (sqsize * j + sqsize / 2))) {
							y += speed;
							// System.out.print(j+" "+i);

							if ((i % 2 == 0 && j % 2 == 0) || (i % 2 == 1 && j % 2 == 1)) {
								y = y - (sqsize + sqsize / 2 + sqsize / 4);
								y = y < 0 ? (y + (sqsize + sqsize / 2 + sqsize / 4)) : y;
							}
							break outer;
						}

			y -= speed;

		}
		if (e.getKeyCode() == KeyEvent.VK_S) {
			outer: for (i = 0; i <= 820; i++)
				if ((y == (sqsize * i - 20)))
					for (j = 0; j <= 1520; j++)
						if ((x + 20) > sqsize * j && ((x) < (sqsize * j + sqsize / 2))) {
							y -= speed;
							// System.out.print(j+" "+i);

							if ((i % 2 == 0 && j % 2 == 0) || (i % 2 == 1 && j % 2 == 1)) {
								y = y +(sqsize + sqsize / 2+sqsize/4);
								y = y >820 ? (y - (sqsize + sqsize / 2 + sqsize / 4)) : y;
							}

							break outer;
						}
			y += speed;

		}
		if (e.getKeyCode() == KeyEvent.VK_A) {

			outer: for (i = 0; i <= 1520; i++)
				if ((x == (sqsize * i + sqsize / 2)))
					for (j = 0; j <= 820; j++)
						if ((y + 20) > sqsize * j && ((y) < (sqsize * j + sqsize / 2))) {
							x += speed;
							// System.out.print(i+" "+j);
							i %= 2;
							j %= 2;
							if ((i % 2 == 0 && j % 2 == 0) || (i % 2 == 1 && j % 2 == 1))
							{
								x=x-(sqsize + sqsize / 2 + sqsize / 4);
								x=x<0?x+(sqsize + sqsize / 2 + sqsize / 4):x;
							}
							break outer;
						}
			x -= speed;

		}
		if (e.getKeyCode() == KeyEvent.VK_D) {
			outer: for (i = 0; i <= 1520; i++)
				if ((x == (sqsize * i - 20)))
					for (j = 0; j <= 820; j++)
						if ((y + 20) > sqsize * j && ((y) < (sqsize * j + sqsize / 2))) {
							x -= speed;
							// System.out.print(i+" "+j);
							i %= 2;
							j %= 2;
							if ((i % 2 == 0 && j % 2 == 0) || (i % 2 == 1 && j % 2 == 1))
							{
								x=x+(sqsize + sqsize / 2 + sqsize / 4);
								x=x>1520?x-(sqsize + sqsize / 2 + sqsize / 4):x;
							}
							break outer;
						}
			x += speed;
		}
		x = x > 1520 ? 1520 : x;
		y = y > 820 ? 820 : y;
		x = x < 0 ? 0 : x;
		y = y < 0 ? 0 : y;

		repaint();

	}

	public void keyReleased(KeyEvent e) {
	}
}
